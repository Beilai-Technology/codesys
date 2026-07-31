# 前言

欢迎使用 CODESYS  
CODESYS 是一款专为工业自动化控制设计的通用编程软件平台。通过直观的集成开发环境(IDE)，帮助您快速完成 PLC 逻辑编写、运动控制配置及 HMI 可视化设计，提升开发效率，是工业控制编程与调试的得力助手。

## 使用须知

感谢您使用 CODESYS 开发平台。为确保您能安全、顺畅地使用本工具，请知悉：  
本工具旨在为您提供符合 IEC 61131-3标准的便捷编程方案，但无法保证在所有非标准或老旧硬件环境下均完美适配。  
请在操作前确认硬件连接与驱动安装正确。重大程序变更或固件升级前建议备份项目文件，以免造成意外中断或数据丢失。  
因使用本工具进行的控制逻辑编写或参数配置所引发的任何间接或直接设备问题(如机械碰撞、生产停滞等)，开发团队不承担相关责任，请务必在安全环境下进行测试。

## 核心警告

本设备软件授权与硬件深度绑定。  
严禁重刷系统或修改底层文件！  
任何违规操作都将导致授权永久失效，且不在保修范围内。

## 版权声明

本说明书之所有权由公司授权方所有。未经本公司之书面许可，任何单位和个人无权以任何形式复制、传播和转载本手册之任何部分，否则一切后果由违者自负。

## 修订记录

| 更新日期 | 文档版本 | 说明 | 修订内容 | 作者 |
|----------|----------|------|----------|------|
| 2026.7.14 | Ver.1.0 | 首次发布 | | |
| 2026.7.16 | Ver.1.1 | 第一次修订 | 增加操作IO | |

# 1.产品认知与功能概述

## 1.1.产品简介

CODESYS是一款基于IEC61131-3国际标准的通用自动化工程软件平台。它集成了PLC逻辑编程、运动控制、HMI可视化、安全控制及通讯配置等功能，支持从嵌入式控制器到大型SCADA系统的全场景应用。无论您是进行单机设备开发，还是构建复杂的分布式控制系统，CODESYS都能提供统一、高效的工程环境。

## 1.2.核心功能优势

●硬件独立性：CODESYS运行时(Runtime)可移植至数百种不同的硬件平台。开发者只需编写一次逻辑代码，即可通过更换设备描述文件(Device Description)快速部署到不同的控制器上，极大降低了硬件绑定风险。  
●多语言支持：完整支持IEC61131-3定义的六种编程语言，包括梯形图(LD)、功能块图(FBD)、结构化文本(ST)、指令表(IL)、顺序功能图(SFC)及连续功能图(CFC)，满足不同工程师的编程习惯。  
●强大的库管理：内置丰富的标准库及行业专用库(如SoftMotion、Safety、WebVisu等)。支持自定义库的创建与版本管理，便于企业级代码资产的复用与维护。

# 2.软件授权

## 2.1. CODESYS 运行环境授权说明

本设备内置的 CODESYS 运行环境(Runtime)及相应功能库均已包含在设备售价中，用户无需另行向 CODESYS 官方购买授权。根据设备型号与配置不同，系统预置了以下三种等级的功能授权：

| 授权版本 | 核心功能解锁 | 适用场景描述 |
|----------|----------------|--------------|
| Pro版本 | EtherCAT Master, Modbus TCP Server | 通用自动化控制：适用于标准的逻辑控制、数据采集及普通自动化产线设备。 |
| SM版本 | Softmotion, EtherCATMaster, Modbus TCP Server | 高级运动控制：在Pro 版基础上增加多轴同步插补、电子凸轮等高级运动控制功能，适用于高速高精设备。 |
| CR 版本 | Softmotion,CNC,EtherCATMaster, Modbus TCP Server | 数控与机器人控制：在SM 版基础上集成 CNC 数控内核与机器人运动学算法，专用于机床、机械手及高端智能装备。 |

## 2.2.系统开放性与二次开发风险提示

虽然 CODESYS 官方标准成品通常限制二次开发接口，但为了满足本设备用户对灵活性与高性能计算的特殊需求，我们在出厂时特意开放了底层 Root 权限及部分系统接口，允许用户在设备上部署第三方应用与 CODESYS 协同工作。  

▲重要安全警示(请务必仔细阅读)：  
● 由于开放了底层权限，为防止内置的 CODESYS Runtime 及授权文件被非法拷贝至其他非授权设备，本设备的软件授权已与当前硬件系统的唯一环境信息进行了深度绑定。  
● 严禁重刷系统：请勿尝试重新烧录操作系统或格式化系统分区。  
● 严禁修改底层文件：请勿随意修改系统底层配置文件或破坏文件系统完整性。  
●后果自负：一旦检测到系统环境变更或文件损坏，绑定的授权信息与吕time将会自动失效并被删除。届时设备将无法正常运行CODESYS程序，且无法通过常规手段恢复。  
●售后政策：因上述违规操作导致的软件失效，不在免费保修范围内。如发生此类情况，用户需重新购买CODESYS控制器硬件以恢复使用。

# 3.环境搭建与配置

## 3.1.上位机软件安装

1.获取安装包：请从CODESYS官方网站或钡铼提供下载对应版本的安装包(如CODESYS V3.5.21 SP40)。  
2.安装步骤：  
●运行CODESYS 64 3.5.21.40. exe,接受许可协议。  
●选择安装类型：推荐选择"完整安装"以包含所有常用组件及示例工程。  
●设置安装路径（建议保持默认路径以避免权限问题）。

## 3.2.目标设备部署

购买钡铼的CODESYS产品出厂默认预装。

# 4.快速入门指南

## 4.1.创建第一个工程

1.新建项目：点击File> New Project,选择目标设备模板(如standard project),放置在合适的路径下。 

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p007_01_IM148.jpg)

2.配置任务：在标准工程下，确认设备和开发语言。

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p007_02_IM149.jpg)

3.添加描述文件：首次使用需要安装钡铼提供的 XML 描述文件，在菜单栏选择工具-设备存储库。在弹出的设备存储库窗口中，点击 安装(I)···按钮。

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p008_01_IM154.jpg)

4.安装：浏览并选择钡铼提供的设备描述文件，确认安装，此时在设备存储库中即可看到钡铼的设备型号(例如: Shenzhen Belai ARM 64 Pro) 。

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p008_02_IM155.jpg)

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p009_01_IM158.jpg)

5.更新设备：在左侧设备树中，右键点击默认的PLC Device。选择对应的文件更新设备。

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p009_02_IM159.jpg)

## 4.2.添加扩展模块

1. 添加 N/X/Y 系列模块  
右键点击已更新的钡铼 Device节点，和上述类似在菜单栏选择工具-设备存储库。在弹出的设备存储库窗口中，以N2162为例，安装对应的扩展模块 xml文件。

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p010_01_IM163.jpg)

2.更新设备  
右键设备名添加扩展模块。根据实际硬件需求，选择并添加对应的扩展模块。

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p010_02_IM164.jpg)

## 4.3.操作外部设备

1.连接网关：点击设备-通信设置-扫描网络进行连接，显示设备信息即为连接成功。

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p011_01_IM168.jpg)

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p011_02_IM169.jpg)

2.添加用户信息：初始设备需要添加用户信息，设置好账户密码，即可正常登录设备。

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p012_01_IM172.jpg)

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p012_02_IM173.jpg)

3.下载：对应默认应用。

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p013_01_IM176.jpg)

4.调试指引：启动文件之前需修改更新变量为使能总线扫描，点击登录按钮配置参数，确认登录无误后，再点击启动即可对设备进行正常的读写操作与逻辑控制。

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p013_02_IM177.jpg)

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p014_01_IM180.jpg)

5.I/O输出功能验证：测试的输出变量对应的“预备值”设定为TRUE，在顶部栏调试选项卡选择写入值下发到物理端口，对应I/O口闭合指示灯亮。

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p014_02_IM181.jpg)

## 4.4.Modbus RTU Client配置

1.安装和添加

按照上述模块方法添加了modbus拓展模块后如图模块即可正常使用。

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p015_01_IM185.jpg)

2. 自定义XML文件参数配置  
由于Modbus模块涉及功能字、串口波特率、位宽等配置，不同模块间可能存在差异。用户可通过修改自定义XML文件来适配不同的IO板。  
可修改的参数区域包括：-站地址(Station Address)：用于设置从站地址。-波特率设置(Bit rate setting)：配置串口通信速率。-校验位设置(Check bit setting)：配置奇偶校验。-数据位设置(Data bit setting)：配置数据位宽度。

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p015_02_IM186.jpg)

![](https://cdn.jsdelivr.net/gh/Beilai-Technology/img-bed/assets/p016_01_IM189.jpg)

4. 支持的功能码与后续规划  
当前支持: Modbus RTU Client 支持 0x01,0x02,0x03,0x04 命令字。  
后续规划:将完善其他命令字，并添加 Modbus RTU Server 和 Modbus TCP Client。  
License 说明: CODESYS 已内置购买 Modbus TCP Server 和 EtherCAT 模块，如需解锁使用请购买相应的 License。

# 5.技术支持与售后服务

## 5.1.技术支持

本设备的CODESYS运行环境为深度定制版本。  
●如果用户需要添加额外的通讯协议或功能库，请直接联系我司技术支持进行定制或获取。  
●禁止自行购买：请勿直接向CODESYS官方或其他第三方渠道购买标准版License或插件，因为标准版授权与本设备的定制化Runtime不兼容，无法激活使用。

## 5.2.售后支持

电话：0755-29451836
