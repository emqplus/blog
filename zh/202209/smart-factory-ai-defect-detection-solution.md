>**导语**
>
>随着工业 4.0 时代的来临，数字化、智能化转型成为工业领域企业保持核心竞争力的必经之路。工业制造涉及环节和场景众多，对于各类生产数据的收集与处理能力是决定其自动化程度的关键。构建可靠的工业物联网数据接入层，为上层平台与应用提供实时可靠的数据源以供分析决策，可以极大提高工作效率。
>
>在本专题系列文章中，我们将结合 EMQ 多年来服务工业领域客户的实践经验，从能耗监控、预测性维护、产品质量溯源等工业领域常见场景需求入手，为从业者提供针对性的的解决方案参考。

## 背景

在数以万计的智能工厂中，一个零部件的质量往往关系到整个产品是否合格、整条生产线的合格率、整个工厂的生产效率和经济成本，甚至是整个企业的市场竞争力。因此，产品的质量检测是生产企业管理者必须重视的关键环节。

随着工业智能化的迅速发展，视觉 AI 缺陷检测技术已逐步成熟并得到广泛应用。采用视觉 AI 缺陷检测技术进行工业缺陷检测，具有非接触、高效、低成本、自动化程度高等优点，在检测缺陷和防止缺陷产品方面具有不可估量的价值。

基于视觉 AI 缺陷检测技术，工厂如何实现零缺陷生产和自我工艺优化升级的「智慧化」，将在两个维度对现有的技术提出挑战，一方面需要不断训练、优化AI算法模型以提升视觉检测技术覆盖范围和精准度；另一方面，数据可自动上传到生产执行系统和企业云大数据分析平台，便于后续大数据分析做工艺的持续性优化、生产线的效率提升以及管理模式的不断改善，最终实现整个工厂自我纠错、不断改善的智慧化能力。

## 视觉 AI 缺陷检测技术现状分析

### 缺乏在近生产线的边缘端独立处理事件能力

产品缺陷有时是工艺上不可避免，有时是生产线设备参数设置异常、设备故障或操作错误等原因导致，一旦视觉 AI 缺陷检测到产品缺陷，需要通过声光等告警信号及时告知现场工程师进行故障排查，或通过生产线的自动化系统执行分流、纠错等流程，避免造成更大的经济损失。告警信号触发或执行流程一般是通过声光报警器或 PLC 执行完成，边缘端运算能力需要保障告警事件处理的实时性、高效性和独立性。

### 数据异构化、汇聚难

在智能制造生产过程中，产品的质量数据不仅涉及缺陷检测的图像流，还涉及到现场多工序多产线生产设备的多源异构协议数据、生产经营相关业务数据和产品设计工艺数据采集，以及 MES、WMS、ERP 等工厂管理系统的对接。这些设备或系统处于不同的网络环境中，如生产网、办公网或者云平台等，需要构建一条信息通道打通各个设备和系统之间数据交互壁垒，进行相关数据的全面感知和采集，才能实现基于视觉 AI 缺陷检测和其他生产、业务数据的大数据分析。

### 新趋势：基于「云-边」架构的 AI 算法模型

「云-边」的架构成为视觉 AI 缺陷检测架构的新趋势。「云」设立在厂级信息中心或集团的总部，掌握总体管控的功能，还可根据实际生产需要，选用合适的模型进行集中训练，再将训练好的模型发布给 「边缘」进行就近推理，并接收其返回的推理结果进行存储、管理；「边缘」则设立在工厂内每条生产线上，进行前端的数据采集、预处理以及简单的推理工作，也在「云」的管控下，对生产线产品进行实时缺陷检测。

![全新工业视觉平台系统架构图](https://assets.emqx.com/images/5614d6880fa33fa3c08cccc157216f75.png)

<center>全新工业视觉平台系统架构图</center>


## EMQ 视觉 AI 缺陷检测解决方案

针对工业领域视觉 AI 缺陷检测场景现状，EMQ 通过云原生技术以及云边协同架构提供了完整解决方案，实现对视觉 AI 缺陷检测图像流及海量工业设备数据在「产线-工厂-集团」的连接、移动、处理、存储与分析。

![EMQ 视觉 AI 缺陷检测解决方案](https://assets.emqx.com/images/9235c7aedec6ad0cd897ca9bd6ae04f9.png)

该方案主要由以下产品构成：

| **组件**       | **产品名称**                                                 |
| -------------- | ------------------------------------------------------------ |
| 边缘数采软件   | [Neuron](https://www.emqx.com/zh/products/neuron) - 工业协议网关软件 |
| 边缘 Broker    | [NanoMQ](https://nanomq.io/zh) - 超轻量级边缘MQTT消息服务器  |
| 边缘计算软件   | [eKuiper](https://ekuiper.org/zh) - 超轻量物联网边缘数据流式分析引擎 |
| 物联网接入平台 | EMQX BC - 云原生分布式物联网接入平台                         |

1. EMQ 在边缘端提供视觉 AI 缺陷检测数据对接处理能力。eKuiper 支持 Rest、gRPC、msgpack RPC 服务对接视觉 AI 缺陷检测数据，获取缺陷产品图像流，进行实时压缩后在边缘端存储和汇聚到厂级数据中心或云端。
2. 边缘端实现视觉 AI 缺陷检测设备和自动化设备联动，在生产线上视觉 AI 缺陷检测设备检测出产品缺陷，可以直接通过 Neuron 下发指令到声光报警器和 PLC，进行告警通知或者执行分流、纠错流程。
3. 构建「产线-工厂-集团」图像流及海量工业设备数据传输通道。数据通过 EMQ 边缘计算平台汇聚，传输到工厂的 EMQX，再桥接到云端 EMQX，并通过其规则引擎流入到时序数据库与 AI 分析应用，为基于全集团工厂缺陷检测图像数据和业务数据的大数据分析应用奠定基础，实现生产质量追溯、生产工艺优化等数据价值挖掘与应用。
4. 通过 EMQ 的这套方案可以构建完整、自循环的云边一体 AI 模型训练流程：边缘端的图像流实时汇聚、持久化到云端，云端 AI 及时进行模型训练并周期性优化算法模型发布到边缘端，同时实时汇聚、持久化新模型推理结果，为工厂生产工艺进一步优化、智慧化做好准备。


## EMQ 架构优势

### 多维度的数据汇聚和逻辑处理能力

EMQ 整体解决方案可以采集与反向控制工厂内 PLC、非标自动化设备、各类仪器仪表、视觉 AI 缺陷检测设备的图像流和实时数据，可以响应边缘端、工厂 MES 系统、云中心各级数据逻辑运算、事件流处理需求。

### 多维度的数据持久化能力

通过 ekuiper 和 EMQX 内置规则引擎功能，可以在边缘端、厂级信息中心和云端，把图像流和业务数据流实时推送到各类数据库中，包括 InfluxDB、TimescaleDB、MySQL、PostgreSQL 等各类时序数据库和关系型数据库。EMQX 支持每秒 10万+TPS 的数据库数据写入性能，可满足每秒千万级数据测点的实时入库。EMQX 将多端 Neuron、eKuiper 采集分析的数据进行统一汇聚，数据推送到数据库及大数据系统进行持久化存储，为企业构建生产质量分析和优化构建了健壮的底层数据架构。

### 云边协同管理提升企业 IT 水平

EMQ 的云边协同框架将 Neuron、eKuiper 等众多边缘软件进行远程统一管理，无论云边之间的网络是直连模式还是穿透模式，都可以方便地进实现参数配置、日志查看、实时监控等远程管理。 

此外，方案利用 KubeEdge 对边缘软件进行编排管理，实现了边缘软件的高可用、远程部署、软件升级以及边缘离线自治等功能，实现应用的边缘自治，极大提升了整体系统的稳定性，并降低运维成本。

## 结语

通过构建图像流和业务数据流到厂级数据中心和云中心的数据高速通道，EMQ 面向视觉 AI 缺陷检测场景的解决方案打破了检测系统和产线自动化设备之间的信息孤岛，基于不同业务层对事件处理的需求提供对应的逻辑分析和数据持久化能力，为企业通过 AI 模型训练不断优化视觉 AI 缺陷检测算法以及基于大数据分析持续改进工厂生产工艺和企业管理模式提供了保障，助力企业实现数字化转型，提升市场竞争力。



<section class="promotion">
    <div>
        联系 EMQ 工业领域解决方案专家
    </div>
    <a href="https://www.emqx.com/zh/contact?product=solutions" class="button is-gradient px-5">联系我们 →</a>
</section>
