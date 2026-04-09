# miniqmt-xtquant-Ashare
1.MiniQMT 轻量级量化交易终端 + XtQuant Python API的Python量化交易框架，是目前最适合普通股民的本地实盘量化方案，低延迟、高稳定、全私密，包括环境搭建、行情获取、api使用、策略开发、实盘自动交易部署，专为A股交易者打造；2.Ashare（开源、极简的A股实时行情数据API），完全免费的沪深股票行情数据，Python最简封装接口，包含日线,历史K线,分时线,分钟线,全部实时采集，系统包括新浪腾讯双数据核心采集获取，自动故障切换，STOCK数据格式成DataFrame格式,可用来查询研究量化分析，股票程序自动化交易系统.为量化研究者在数据获取方面极大地减轻工作量，更加专注于策略和模型的研究与实现。
## 一、miniqmt+xtquant 券商级高速专业的行情数据交易软件及API接口
#### 1、MiniQMT + XtQuant 的核心量化特点
- 超低延迟、实盘级交易速度,券商官方通道，券商柜台直连，不是第三方模拟接口.  
- 纯本地运行，策略完全私密,策略代码跑在你自己电脑上，不会泄露策略逻辑、仓位、买卖点,适合不想开源、不想被平台看到策略的个人交易者.  
- Python 原生接口，自由度极高,XtQuant 是标准 Python 库，不受平台限制，想怎么写就怎么写.  
- 全市场覆盖：股票 / 场内基金 / 两融 / 期权 / 期货,一个接口通吃所有品种.  
- 轻量化、不吃资源,不像大 QMT 那样笨重.  
- 数据本地 + 实时推送,历史 K 线、Tick、财务数据本地缓存,推送式行情，不用反复拉取.  
- 券商官方认可，合规安全,不是第三方爬虫、不是模拟接口,是券商级量化通道，实盘稳定、合规.  

#### 2、MiniQMT 和 XtQuant 不是同一个软件，是「底层终端 + 上层 Python 接口库」的依赖关系：
- MiniQMT 软件： https://download.gjzq.com.cn/temp/organ/gjzqqmt_ceshi.rar
- Xtquant API文档：https://dict.thinktrader.net/nativeApi/start_now.html ；  https://dict.thinktrader.net/nativeApi/xtdata.html
- MiniQMT：是可独立运行的量化交易终端软件（你要打开、登录的那个程序），是底层的「交易通道 + 行情服务器」；是迅投（ThinkTrader）开发的 QMT 量化交易系统的「极简 / 轻量版本」，是一个可独立安装、运行的 Windows 桌面软件，是你量化交易的「底层执行终端」；对接券商，完成真实的股票 / 期货 / 期权报单、撤单、成交、资金 / 持仓管理，是你策略落地实盘的唯一通道；实时接收沪深交易所行情、存储历史 K 线 / Tick 数据，给你的策略提供数据支撑；作为本地服务运行，给 XtQuant 提供 API 交互的底层支持，是 XtQuant 能正常工作的前提。
- XtQuant：是MiniQMT 衍生出的 Python 库 / 框架，是连接你写的 Python 代码和 MiniQMT 终端的「桥梁」，本身不能独立运行，必须依赖 MiniQMT 客户端；作为 Python 代码和 MiniQMT 终端之间的「桥梁」，把 MiniQMT 的交易、行情能力，封装成 Python 可调用的函数 / 接口，让你用 Python 写量化策略，就能自动调用 MiniQMT 完成交易、获取数据；本身不能独立运行，必须先启动 MiniQMT 客户端、登录账号，XtQuant 才能通过 TCP 连接调用 MiniQMT 的服务；以 Python 库形式存在：安装 MiniQMT 后会自动附带，也可通过pip install xtquant单独安装；所有功能都是 MiniQMT 能力的 Python 封装，没有 MiniQMT 就没有 XtQuant；是你量化策略的「代码入口」，你写的所有 Python 量化代码，都要通过 XtQuant 的接口，才能落地到实盘交易。

#### 3、MiniQMT + XtQuant 安装配置流程
- 操作系统：Windows 10/11 64 位（MiniQMT 仅支持 Windows，不支持 Mac/Linux）
- Python 环境：推荐 Python 3.8~3.10 64 位（兼容性最好，避免版本过高导致的依赖问题）。
- 网络：稳定的互联网连接，用于登录券商服务器、接收行情
- 打开上面的miniqmt链接下载，然后按照向导完成安装，建议安装路径选择非系统盘（如D:\国金QMT\），避免 C 盘权限问题，安装完成后，桌面会生成「国金QMT」快捷方式。
- 双击打开国金qmt，输入楼主给的账密，并务必勾选「独立交易模式 / 极简模式」登录（MiniQMT 的核心运行模式，否则 XtQuant 无法连接）。
- 登录成功后，确认客户端正常接收行情、可手动下单，说明终端运行正常，保持 MiniQMT后台在线，这是 XtQuant 正常工作的唯一前提。
- 安装 Python（已有环境可跳过），打开 Python 官网：https://www.python.org/downloads/windows/ ，下载Python 3.9.13 64 位（稳定兼容版，避免最新版的兼容性问题），安装时务必勾选「Add Python.exe to PATH」，自动配置环境变量，安装完成后，打开 CMD 命令提示符，输入python --version，显示版本号即安装成功。
- 安装 XtQuant 库的方式 1：从 MiniQMT 本地安装（随客户端自带）（推荐），打开 CMD，进入 MiniQMT 的 Python 包目录：cd D:\国金QMT\bin.x64\Lib\site-packages ；执行本地安装命令：pip install xtquant --no-index --find-links=./ ；等待安装完成，显示Successfully installed xtquant即成功。
- 方式 2：pip 在线安装（备用），如果方式 1 失败，直接执行在线安装：pip install xtquant -i https://pypi.tuna.tsinghua.edu.cn/simple ，用清华源加速，避免下载超时，安装完成后，同样用pip show xtquant验证版本。
- 10、验证安装成功，打开 CMD，输入python进入 Python 交互环境，执行：import xtquant   //  print(xtquant.__version__) ;正常输出版本号（如2.0.12），说明 XtQuant 安装成功
- 下一步：开始量化策略开发,环境配置完成后，你可以直接基于 XtQuant 的 API 开发策略：用xtdata获取行情数据，编写策略逻辑（均线、MACD、因子等）;用xttrader实现自动下单、撤单、持仓管理;先在模拟盘测试策略，验证稳定后再上实盘;先在模拟盘测试策略，验证稳定后再上实盘.

---------------------------------------------------------------
![git量化技术群](https://github.com/user-attachments/assets/197be134-96d3-4be2-b7b8-748fbe53a229)
> #### 扫一扫获取miniqmt模拟和实盘账号
> #### 股市程序化交易大群, 圈内大咖量化策略分享
> #### 全是干货，无闲聊 ，物以类聚,人以群分，一起感受思维碰撞的力量!













