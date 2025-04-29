

<span style="color:red" > 嵌入包和编译的pyc文件，基本上大版本一致好像就没问题，具体我没有去尝试  </span>



适用于 Python 的 Windows 可嵌入包是一种最小的可移植 Python 发行版，旨在嵌入到其他应用程序中或在 Windows 上分发基于 Python 的应用程序，而无需安装完整的 Python。它以 ZIP 文件的形式提供，并与用户系统隔离，非常适合将 Python 与应用程序捆绑在一起的场景。以下是详细说明和设置指南，包括带有示例配置的构件。

### Windows Embeddable 程序包概述

目的：适用于需要在其应用程序（例如桌面应用程序、游戏或工具）中包含 Python 运行时而不向最终用户公开 Python 或要求他们单独安装 Python 的开发人员。

特点：
最小大小：通常为 10-15 MB，仅包含核心 Python 运行时（例如，python.exe、python3.dll、ZIP 格式的 .pyc 文件等标准库）。

隔离：不依赖于系统环境变量、注册表设置或全局安装的软件包。

限制：
默认缺少 pip、Tkinter、Python 文档和其他工具。
不包括 Microsoft C 运行时 （ucrtbase.dll），它必须由应用程序安装程序提供或已存在于系统上。
不是为直接最终用户交互而设计的;第三方软件包必须手动管理或供应商管理。

使用案例：
分发独立的 Python 应用程序（例如，使用 PyInstaller 或自定义安装程序）。
将 Python 嵌入到 C/C++ 应用程序或游戏引擎（例如 Unreal Engine）中。
在限制安装 Python 的系统（例如，锁定的企业环境）上运行 Python 脚本。
关键组件

ZIP 中的文件：
python.exe：命令行 Python 解释器。
pythonw.exe：对于 GUI 应用程序（禁止控制台输出）。
python3.dll / pythonXX.dll：Python 运行时库。
pythonXX.zip：包含预编译的 .pyc 文件形式的标准库。
pythonXX._pth：控制 sys.path 和解释器行为的配置文件。
PythonXX._pth 文件：
定义嵌入式 Python 的模块搜索路径 （sys.path）。
默认情况下，限制路径以确保隔离。
可以修改以包含其他路径（例如，对于第三方包）。