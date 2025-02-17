## 背景

随着 5G、大数据、人工智能技术等的高速发展，各类智能物联设备 AR、巡检机器人、无人机、可穿戴便携设备等开始在工业领域中得到广泛应用，工业装备的结构和工业生产的环境日趋复杂。

对于整个工厂来说，智能化、数字化的实现不仅是通过新型工艺和生产设备的使用提升生产水平，还需要构建具备「眼-鼻-耳」的工厂智慧大脑，能够实时感知生产设备情况，对整个生产环境中的异常事件通过系统自动告警、多方联动应急等方式进行快速响应处理，实现提前感知、处理过程闭环、事后追溯的综合管理创新。

## 工厂异常事件感知与处理现状分析

### 缺少统一的设备感知和设备间数据贯通能力    

智能工厂的生产安全是整个系统协同的过程，一个系统的异常状态感知往往不只是通过对一个或一类设备运行的监控和判断，而是基于多维的、覆盖生产所有环节的人、机、料、法、环相关工业设备或智能物联设备的综合感知和联动。实现精确的异常事件告警和处理预案，需要感知所有的工业设备和智能物联网设备，构建各个设备之间的数据通道。

### 边缘端无独立数据逻辑处理和事件判断能力

传统工业在控制层之上的事件告警和预案处理都是通过信息中心统一的大脑进行控制和协调，网络延时、大脑处理信息量过大等情况会导致事件告警和处理滞后。

此外，一旦边缘端与中心的网络中断或者是大脑发生故障，整个感知系统将面临全面崩溃的风险。这对于整个生产系统的高效安全运行来说是一个巨大的隐患。

![工厂大脑](https://assets.emqx.com/images/d808b7b16c33672a4cff5b46c91c1d7e.png)

### 数据到企业集团云方案难度大、成本高

大数据和人工智能技术在云端的应用和创新，对企业数据贯穿「设备-工厂大脑-云」提出新的要求。企业可以在集团云上部署「指挥调度中心」，实现云端「专家」指导工厂「大脑」工作，对复杂系统情况统一感知、调度，并且对处理预案进行自我学习、优化与提升。传统的工业数据建立集团云一般是通过企业专网或 VPN 的方式构建，成本高昂，网络资源要求较高并且组网方式不灵活。


## EMQ 云边协同的事件异常处理解决方案

基于 EMQ 云边协同框架的数据感知、汇聚和上云的解决方案，可以为工业客户智慧工厂的构建提供以下能力：

- 边缘端独立逻辑运算感知异常、事件处理的能力；
- 事件异常告警数据持久化到数据库，为工厂大脑进行异常事件统计分析奠定基础的能力；
- 集团云指挥调度中心人工智能对工厂集统一指挥调度。通过工厂集的异常事件和处理结果的归纳总结，自动学习从而不断优化事件异常算法和处理方案。通过向工厂大脑和边缘运算模块发送优化指令，提升「边缘运算-工厂大脑-云指挥调度中心」整个系统的事件判断、预测和处理效率和能力。

![EMQ 云边协同的事件异常处理解决方案](https://assets.emqx.com/images/8cbc1d92657d41ef567c11d95beaff02.png)

边缘端[工业协议网关软件 Neuron](https://www.emqx.com/zh/products/neuron) 实现各类工业设备的接入，可基于轻量级 MQTT 协议传输，实现在工业生产弱网环境下的各类数据实时感知与稳定传输。边缘端[轻量级消息总线 NanoMQ](https://www.emqx.com/zh/products/nanomq) 实用于现数据的汇聚和缓存，打通处于不同网络中设备、不同系统间的数据壁垒，去除信息孤岛。同时，NanoMQ 可以在边缘端实现数据断点续传， 保障业务数据的完整性，防止异常事件数据信息的丢失。

随着 5G 网路在工厂或园区内大量建设，基于 5G 的各类智能终端和应用也越来越多，这类终端和应用对数据汇聚和处理实时性都有很高的要求。传统工业总线和工厂「大脑」资源有限，如果所有的事件都到工厂「大脑」进行处理，实时性和可靠性较差。EMQ 提供的超轻量[物联网边缘数据流式分析引擎 eKuiper](https://ekuiper.org/zh) 能够在近设备端部署，高效、独立判断异常事件并通过各类智能终端和应用的联动来完成异常事件的告警、处理和安全隐患消除。

![EMQ 云边协同的事件异常处理解决方案](https://assets.emqx.com/images/531c5a4965873efcb5135c84d617a8ba.png)

在云端，[大规模分布式物联网 MQTT 消息服务器 EMQX](https://www.emqx.com/zh/products/emqx) 部署在集团云上，可为集团调度指挥中心提供工厂各类工业设备和智慧物联设备的数据汇聚能力，为设备异常事件和处理提供对接 AI 算法的能力，为集团提供所有工厂的异常事件总集合和持久化能力。


## EMQ 基础架构优势

### 快速实现边缘端异常事件告警处理

具备边缘端工业软网关、消息总线和规则引擎模块，通过灵活的组合和简单的配置，即可为设备-工厂大脑-云指挥调度中心间建立完善的「神经网络」，轻松实现不同工业设备以及智慧物联设备数据感知、汇聚、异常事件判断、联动处理。

### 三层架构实现异常事件告警、调度、处理

边缘运算负责常规异常事件的判断与处理，工厂大脑负责工厂内异常事件的统计分析与本厂生产指导，集团云负责基于工厂的异常事件大数据和人工智能分析，对整个集团资源进行统一的指挥调度、异常事件预测和处理预案的优化。「边缘-工厂-云」各个层级的事件告警/处理行为符合整个系统的协同和业务需求，能对设备异常事件做出快速响应和高效处理，最大化利用整个系统的硬件和软件资源。

### 「边缘-工厂-云」一体化运维管理平台

基于 EMQ 云边协同架构， 实现部署在「边缘-工厂-云」的 EMQ 系列产品在云端的统一运维管理配置，轻松实现参数配置、日志查看、实时监控等功能。

另外，通过 EMQ 提供的 [EMQX Kubernetes Operator](https://www.emqx.com/zh/emqx-kubernetes-operator)，用户可以在 Kubernetes 的环境上快速创建和管理 EMQX Enterprise 集群，大大简化部署和管理 EMQX 集群的流程，把部署和管理的工作变成一种低成本的、标注化的、可重复性的能力。

## 结语

EMQ 构建了「边缘运算-工厂大脑-云指挥调度中心」全方位的异常事件告警/处理的数据链路，能够基于不同业务层对事件处理的需求提供对应的能力，为企业精益生产、安全管理以及数字价值创新提供了数据基座能力保障，助力工厂向着生产效率更高、生产环境更安全、管理方式更规范的方向进行数字化转型。





<section class="promotion">
    <div>
        联系 EMQ 工业领域解决方案专家
    </div>
    <a href="https://www.emqx.com/zh/contact?product=solutions" class="button is-gradient px-5">联系我们 →</a>
</section>
