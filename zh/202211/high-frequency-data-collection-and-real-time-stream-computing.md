2020 年，中国提出了「碳达峰、碳中和」的目标，开始大力投入风能和太阳能发电建设。根据国家能源局发布的数据，到 2022 年 8 月为止，风电和太阳能在全国电网的装机容量占比已经超过 28%。

风电和太阳能发电具有随机性、间歇性和波动性的特点，这给电网调峰、运行控制和供电质量等带来巨大挑战。通过储能调节风能和太阳能大规模入网给电网带来的冲击是一种重要的技术手段。2022 年 1 月，发改委、能源局联合印发《“十四五”新型储能发展实施方案》，设定了储能产业的发展目标，储能系统的建设进入高速发展期。

与此同时，其安全问题也日益凸显。通过现代化的技术保障储能系统的安全运营成为储能系统建设需要关注的一个重要议题。

## 储能系统安全保障技术现状

传统的储能系统建设主要包含以下几个部分：

- BMS 电池管理系统：电池管理系统主要功能是管理及维护各个电池单元的充放电，防止电池出现过充或者过放，延长电池的使用寿命。电池管理系统单元由采集模组、控制模组和电池管理应用组成。采集模组主要采集电池模组和电池单体的电压、电流、温度等参数据数据；控制模组控制电池的充放电，电池管理应用管理电池的充放电和维护电池的充放电安全。
- PCS 储能变流器：储能变流器主要控制储能系统的充电和放电过程，进行直交流的转换并根据功率指令控制变流器对电池进行充电或放电，实现对电网有功功率及无功功率的调节，是储能系统充放电策略的执行单元。
- EMS 能源管理系统：能源管理系统全面采集了BMS、PCS 和其他辅助管理系统的信息，技针电池储能系统实现调控一体化能量管理，实现储能系统实时监控、诊断预警、全景分析、高级控制等功能，满足储能系统监视全面化、安全分析智能化、全景分析动态化等需求，保证储能系统安全、可靠、稳定地运行。
- 辅助系统：储能辅助系统包含空调系统和消防系统，主要是维护储能系统的运行在相对安全的环境，并在出现火灾时实现告警和灭火。

传统储能系统一般是采用固定的运行策略脱网运行的模式，随着智能微网和虚拟电厂等应用的出现，储能系统需要联网并提供接口供智能调度系统进行调度，这需要引入物联网的技术实现储能系统的技术升级。电力生产系统联网有严格的安全要求和规范，网络架构需要符合电力生产系统的安全规范，在物联网的基础上增加单向网闸穿透的功能成为必要。

此外，原有的 EMS 系统虽具备一定的分析、告警功能，但其设计目标重点在整体的系统的监控，系统数据一般存储在结构化的数据库中，对大数据的存储和分析支持的能力有限，拓展和整合其他技术的能力也比较弱。要想实现储能系统的模型优化、参数调优、提前预警、可预测维护等智能运维功能，需要引入大数据、人工智能、深度学习等技术，完成储能系统物联网化升级。

## 云边协同储能可预测维护系统方案

针对储能系统物联网化和运维智能化的需求，EMQ 提供了云边协同可预测维护系统的基础技术架构。通过低代码、可配置低方式实现储能系统数据接入、边缘计算、数据汇聚、网闸穿透、数据存储和分析，在边缘实现预测性维护算法，云端实现算法、模型、参数的优化，并通过边缘计算提供的流计算框架更新参数到边缘计算预测模型，从而实现云边协同的可预测维护系统。

![云边协同可预测维护系统架构](https://assets.emqx.com/images/2a92471627094189a5cce31585bf7652.png)

<center>云边协同可预测维护系统架构</center>


### 毫秒级高频数据采集

储能系统的数据采集需要基于传统的 EMS 系统实现，EMS 系统已经支持 BMS、PCS 以及辅助系统的数据采集，储能系统的数据可通过 EMS 系统获取完整的数据。目前，EMS 能源管理系统一般可以对外提供传统工业协议数据接口，例如 Modbus/TCP、OPC-UA、IEC104 等。通过传统的工业协议接口采集超过 10000点位数据，往往需要数秒的时间，而储能系统数据采集频率要求达到亚秒级。

EMQ 旗下[边缘工业协议网关软件 Neuron](https://www.emqx.com/zh/products/neuron) 提供改进的 Modbus 协议，支持每 100 毫秒一次采集数千点位的数据，可以满足储能系统数据高频的数据采集需求。

### 支持迭代流计算的边缘计算框架

储能系统的可预测性维护是通过电池一致性、电池健康度、电池健康变化的趋势等参数预测电池的工作状况，其中包含通过电池的等效模型估算其电量和健康度状态的算法。目前 SoC 和 SoH 估算比较常用的算法是基于卡尔曼滤波器实现，而卡尔曼滤波器算法的核心是需要基于上一个时刻的状态估算结果和状态协方差矩阵，结合当前时刻的观测值更新状态协方差矩阵、计算滤波增益和预估值，计算 SoC/SoH 的估计值。此类算法要求在边缘计算框架中需要支持流数据的迭代算法。

EMQ 提供开源的[边缘流计算产品 eKuiper](https://ekuiper.org/zh)，支持流式计算结果保留在流中，满足下次计算对上次计算结果的调用。eKuiper 还支持流式数据按照不同的模式切片，并基于切片数据执行内置或者拓展的聚合计算算法，实现储能系统状态的实时预测。

### 灵活的流数据汇聚

储能系统数据汇聚系统需要提供设备连接和消息的双向通讯，保证数据采集和方向控制通道，数据汇聚服务除了提供连接服务和消息通道以外，还需要提供灵活的机制实现储能系统数据持久化到数据库并转发数据到大数据分析系统。在实际的应用系统中，还需要考虑电力系统安全生产的需要，支持网闸并降低数据通过网闸的带宽。

EMQ 提供[企业级物联网 MQTT 接入平台 EMQX](https://www.emqx.com/zh/products/emqx)，基于 MQTT 提供储能系统的连接和双向解耦的消息传递方案，并内置基于规则引擎之上的网闸穿透、数据编码、数据持久化和数据转发的功能，实现储能数据的汇聚和灵活应用。

### 内置网闸穿透

电力生产系统的网络安全要求生产控制区、生产非控制区和生产管理区之间的网络通讯通过单向网闸设备保障网络安全。EMQX 内置了正向网闸穿透代理模块，通过配置可以启用此功能，实现储能数据通过标准的 MQTT 协议在不同的生产区之间传输。

### 流式数据存储和分析

高频采集的储能数据是一种持续的系统状态数据流，不同类型的数据需要通过不同的处理和分析再持久化或者转发到其他的应用系统和服务。

[流处理数据库 HStreamDB](https://hstream.io/zh) 提供存储和分析一体化的产品，实现储能流数据的实时去重、检测相邻数据的变化范围、实时流分析、分析算法的拓展以及数据集成和存储等功能。

### 云边协同与管理

EMQ 提供云边协同一体化的方案实现储能系统的云边协同可预测维护的方案，eKuiper 提供可拓展的边缘计算框架，通过迭代计算、数据流窗口化、插件式的函数、流式表等功能实现边缘预测算法及参数的更新；HStreamDB 提供脚本编程的方式实现云端数据的大数据分析，进行预测参数的不断优化；优化的参数可以通过 MQTT 协议更新到 eKuiper 流式表中；通过流式表，实时流数据可以合并更新后的参数，实现算法参数的更新，不断优化储能系统的可预测维护模型。 

### 穿透网闸的反向控制

可预测维护系统的算法模型参数更新和控制指令等数据需要通过反向网闸发送到生产非控区，反向网闸提供文件转发的功能实现两个生产区之间通讯。

EMQX 通过规则引擎提供十六进制数据和字符互相转换的功能，实现消息数据文本化并可在穿透网闸后恢复为消息数据。具体实现方式为：在生产管理区，通过 eKuiper 文件动作插件把需要传输消息的十六进制字符串写到反向网闸指定的目录；反向网闸自动传输指定目录下的文件到生产非控制区；在生产非控制区由文本读取服务获取由反向网闸传输过来的文件，并将文件中的十六进制字符串发送到 MQTT 消息代理服务 EMQX 的指定主题，以此实现算法模型参数更新和控制指令下发等功能。

## 结语

通过 EMQ 云边一体化的方案，可实现数据高频率的数万点位采集，为边缘端赋予实时分析和预测储能系统运行状态的能力，使云端具备大数据分析能力。通过定时的执行策略，定期调整预测模型的参数，实现储能系统云边协同一体化的可预测运维，助力新能源储能系统的安全、高效运营。



<section class="promotion">
    <div>
        联系 EMQ 工业领域解决方案专家
    </div>
    <a href="https://www.emqx.com/zh/contact?product=solutions" class="button is-gradient px-5">联系我们 →</a>
</section>