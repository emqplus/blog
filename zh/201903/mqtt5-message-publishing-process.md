[MQTT 5.0](https://www.emqx.com/zh/mqtt/mqtt5) 协议对部分 QoS 报文，以及报文处理的流程做了一些升级，本文对此这部分升级的内容做简单的介绍。

## QoS 报文格式及处理流程

在 [MQTT 协议](https://www.emqx.com/zh/mqtt-guide)中，消息分为 3 个等级，分别用 QoS0, QoS1, QoS2, 这三个不同的 QoS 值所代表的是不同的服务质量等级。以下是每一个服务质量级别的具体描述：

- 0 ： 最多一次发送（若消息等级为 QoS 0，发布者在发布消息时只会发送一次，不管消息是否送达）；
- 1 ： 至少一次消息发送（若消息等级为 QoS 1，发布者在发布消息时会重复发送以确保消息发送成功）；
- 2 ： 消息只发送一次，并保证送达。（若消息等级为 QoS 2, 发布者在发布消息时确保接收者只接收到一个消息并且消息不会重复）。

在三种 QoS 消息等级中，QoS 0 是最节省计算资源的， 而 QoS 1 在发布完消息后还需要去接收到一个发布确认报文来停止重复的报文发送， QoS 2 消息的传输则需要更多的步骤，它需要 4 次报文发送来确保消息是单次送达的，是所有消息类型中最费计算资源和带宽的。

以下是 3 种不同 QoS 值的处理流程图。

### QoS 0 消息

在 MQTT 3.0 中，QoS 0 的消息发布流程是这样

| 发送者                   | 控制报文流向 | 接受者                         |
| ------------------------ | ------------ | ------------------------------ |
| PUBLISH QoS = 0, DUP = 0 |              |                                |
|                          | —>           |                                |
|                          |              | 接收消息（可能不会收到）并处理 |

  
### QoS 1 消息

| 发送者                                    | 控制报文流向 | 接受者                               |
| ----------------------------------------- | ------------ | ------------------------------------ |
| 存储消息                                  |              |                                      |
| 发送 PUBLISH QoS1, DUP = 0，带有 Packetld | —>           |                                      |
|                                           |              | 接收消息并处理                       |
|                                           |              | 发送带有 Packetld 和 PUBACK 确认报文 |
| 丢弃消息                                  |              |                                      |

若接收者没有接收到 QoS1 消息或者接收到的 QoS 1 消息有问题，是不会去发送 PUBACK 确认报文的，因此发送者不会丢弃 QoS1 消息，它还会再发送这个消息，所以 QoS1 消息是有可能被重复发布的。

### QoS 2 消息

| 发送者                                                       | 控制报文流向 | 接受者                                          |
| ------------------------------------------------------------ | ------------ | ----------------------------------------------- |
| 存储消息                                                     |              |                                                 |
| 发送 PUBLISH QoS1, DUP = 0，带有 Packetld                    |              |                                                 |
|                                                              | —>           |                                                 |
|                                                              |              | 存储 Packet ID 然后准备应用消息的发送           |
|                                                              |              | 发布带有 Packetld 和 Reason Code 的 PUBREC 报文 |
|                                                              | <---         |                                                 |
| 丢弃存储的消息，存储接收到的带有相同 packet ID 的 PUBREC 报文 |              |                                                 |
| 发送 PUBREC 报文                                             | —>           | 丢弃 Packetld                                   |
|                                                              |              | 发送带有 Packetld 的 PUBCOMP 报文               |
|                                                              | <---         |                                                 |
| 丢弃存储的状态                                               |              |                                                 |

为了保证消息单次发送且能送达。首先它要发布一个 PUBLISH 报文，然后接收者在接收完成时并不会返回确认报文，它会存储接收到的消息，然后返回 PUBREC 报文给发送者，发送者在接收到 PUBREC 报文后， 将存储的 PUBLISH 报文替换成收到的 PUBREC 报文，然后发送 PUBREL 报文给接收者。 接收者收到 PUBREL 消息后丢弃之前存储的状态，此时消息已经到达接收者，并且能够确保只到达了一次。

MQTT 协议面对的是计算能力低下的嵌入式设备，虽然 MQTT 5.0 协议中对 QoS2 消息的处理流程做了一些轻微的优化，然而使用用 QoS2 消息通信仍然是非常耗资源的操作，所以通常情况下，如果对于消息传输的优先级要示不是特别高的话，请尽量不要传送 QoS 2 消息。

### MQTT 5.0 升级

MQTT 5.0 在 QoS 上的升级主要体现在 QoS2 的接收者在处理报文的时候一点变化，

- 在 MQTT 5.0 协议中，这里对 QoS2 消息的发布处理流程与 MQTT 3.0 协议稍有不同，在 MQTT 3.0 中，接收者接收到 QoS2 消息后既可以存储消息，也可以存储 Packet ID, 在 5.0 中则强制协议实现者只能存储 Packet Id。这么做是为了强制 MQTT 协议开发者减少 QoS2 消息的带宽损耗。
- 在 QoS2 的接收者端，除了之前返回的 PacketId 之外，还返回了标识 Reason Code 的 PUBREC 报文。


<section class="promotion">
    <div>
        免费试用 EMQX Cloud
        <div class="is-size-14 is-text-normal has-text-weight-normal">全托管的云原生 MQTT 消息服务</div>
    </div>
    <a href="https://accounts-zh.emqx.com/signup?continue=https://cloud.emqx.com/console/deployments/0?oper=new" class="button is-gradient px-5">开始试用 →</a>
</section>
