# 在 Windows 上安装 Docker 桌面

欢迎使用适用于 Windows 的 Docker 桌面。此页面包含有关适用于 Windows 的 Docker Desktop 系统要求、下载 URL、安装和更新适用于 Windows 的 Docker Desktop 的说明的信息。

[适用于 Windows 的 Docker 桌面](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe)

_有关校验和，请参阅[发行说明](https://docs.docker.com/desktop/release-notes/)_

> **Docker 桌面术语**
>
> 大型企业（超过 250 名员工或年收入超过 1000 万美元）对 Docker Desktop 的商业使用需要付费订阅。

## 系统要求

您的 Windows 计算机必须满足以下要求才能成功安装 Docker Desktop。

### WSL 2 后端

- Windows 11 64 位：家庭版或专业版 21H2 或更高版本，或者企业版或教育版 21H2 或更高版本。
- Windows 10 64 位：家庭版或专业版 21H1（内部版本 19043）或更高版本，或者企业版或教育版 20H2（内部版本 19042）或更高版本。
- 在 Windows 上启用 WSL 2 功能。有关详细说明，请参阅 Microsoft 文档。
- 在 Windows 10 或 Windows 11 上成功运行 WSL 2 需要以下硬件先决条件：

  - 具有二级地址转换 (SLAT)的 64 位处理器
  - 4GB 系统内存
  - 必须在 BIOS 设置中启用 BIOS 级硬件虚拟化支持。有关详细信息，请参阅 虚拟化。
    下载并安装 Linux 内核更新包。

### Hyper-V 后端和 Windows 容器

- Windows 11 64 位：专业版 21H2 或更高版本，或者企业版或教育版 21H2 或更高版本。
- Windows 10 64 位：Pro 21H1（内部版本 19043）或更高版本，或者企业版或教育版 20H2（内部版本 19042）或更高版本。

    对于 Windows 10 和 Windows 11 家庭版，请参阅 WSL 2 后端选项卡中的系统要求。

- 必须启用 Hyper-V 和容器 Windows 功能。
- 在 Windows 10 上成功运行 Client Hyper-V 需要以下硬件先决条件：
  - 具有二级地址转换 (SLAT)的 64 位处理器
  - 4GB 系统内存
  - 必须在 BIOS 设置中启用 BIOS 级硬件虚拟化支持。有关详细信息，请参阅 虚拟化。

> **笔记**
>
> Docker 仅支持 Windows 上的 Docker Desktop 适用于仍在 Microsoft 服务时间表内的 Windows 10 版本。

使用 Docker Desktop 创建的容器和图像在安装它的机器上的所有用户帐户之间共享。这是因为所有 Windows 帐户都使用相同的 VM 来构建和运行容器。请注意，使用 Docker Desktop WSL 2 后端时，无法在用户帐户之间共享容器和图像。

Docker Business 客户支持在 VMware ESXi 或 Azure VM 中运行 Docker Desktop。它需要首先在管理程序上启用嵌套虚拟化。有关详细信息，请参阅在 VM 或 VDI 环境中运行 Docker Desktop。

### 关于 Windows 容器
寻找有关使用 Windows 容器的信息？

在 Windows 和 Linux 容器之间切换 介绍了如何在 Docker Desktop 中的 Linux 和 Windows 容器之间切换，并指向下面提到的教程。
Windows 容器入门（实验室） 提供了有关如何在 Windows 10、Windows Server 2016 和 Windows Server 2019 上设置和运行 Windows 容器的教程。它向您展示了如何将 MusicStore 应用程序与 Windows 容器一起使用。
Docker 网站上的适用于 Windows 的 Docker 容器平台文章和博客文章。
> 笔记
>
> 要运行 Windows 容器，您需要 Windows 10 或 Windows 11 专业版或企业版。Windows 家庭版或教育版将只允许您运行 Linux 容器。

## 在 Windows 上安装 Docker Desktop
### 交互式安装
1. 双击 Docker Desktop Installer.exe 运行安装程序。

    如果您还没有下载安装程序 ( )，您可以从 Docker HubDocker Desktop Installer.exe 获取它 。它通常会下载到您的文件夹，或者您可以从 Web 浏览器底部的最近下载栏运行它。Downloads
2. 出现提示时，请确保根据您选择的后端选择或不选择“配置”页面上的“使用 WSL 2 而不是 Hyper-V”选项。
3. 如果您的系统仅支持这两个选项之一，您将无法选择要使用的后端。
4. 按照安装向导上的说明授权安装程序并继续安装。

安装成功后，单击关闭以完成安装过程。

如果您的管理员帐户与您的用户帐户不同，您必须将用户添加到 docker-users 组。以管理员身份运行 Computer Management 并导航到 Local Users and Groups > Groups > docker-users。右键单击以将用户添加到组中。注销并重新登录以使更改生效。

从命令行安装
下载 Docker Desktop Installer.exe 后，在终端中运行以下命令来安装 Docker Desktop：

"Docker Desktop Installer.exe" install
如果您使用的是 PowerShell，则应将其运行为：

Start-Process 'Docker Desktop Installer.exe' -Wait install
如果使用 Windows 命令提示符：

start /w "" "Docker Desktop Installer.exe" install
该 install 命令接受以下标志：

--quiet：运行安装程序时抑制信息输出
--accept-license：现在接受 Docker 订阅服务协议，而不是要求在应用程序首次运行时接受它
--no-windows-containers: 禁用 Windows 容器集成
--allowed-org=<org name>：要求用户在运行应用程序时登录并加入指定的 Docker Hub 组织
--backend=<backend name>：选择用于 Docker Desktop 的默认后端，hyper-v 或 windows（wsl-2 默认）
--installation-dir=<path>: 更改默认安装位置 ( C:\Program Files\Docker\Docker)
--admin-settings：自动创建一个 admin-settings.json 文件，管理员使用该文件来控制其组织内客户端计算机上的某些 Docker Desktop 设置。有关详细信息，请参阅设置管理。
它必须与标志一起使用--allowed-org=<org name>。
例如： --allowed-org=<org name> --admin-settings='{"configurationFileVersion": 2, "enhancedContainerIsolation": {"value": true, "locked": false}}'
如果您的管理员帐户与您的用户帐户不同，您必须将用户添加到 docker-users 组：

net localgroup docker-users <user> /add
启动 Docker 桌面
安装后 Docker Desktop 不会自动启动。启动 Docker 桌面：

搜索 Docker，然后在搜索结果中选择 Docker Desktop 。

搜索 Docker 应用程序

Docker 菜单 ( 鲸鱼菜单) 显示 Docker 订阅服务协议窗口。

以下是要点的摘要：

Docker Desktop 对小型企业（少于 250 名员工且年收入少于 1000 万美元）、个人使用、教育和非商业开源项目免费。
否则，专业用途需要付费订阅。
政府实体也需要付费订阅。
Docker Pro、Team 和 Business 订阅包括 Docker Desktop 的商业用途。
选择接受以继续。Docker Desktop 在您接受条款后启动。

请注意，如果您不同意这些条款，Docker Desktop 将不会运行。您可以选择稍后通过打开 Docker Desktop 来接受这些条款。

更多信息，请参见 Docker Desktop 订阅服务协议。我们建议您也阅读常见问题解答。

接下来要去哪里
Docker 入门是教您如何部署多服务堆栈的教程。
故障排除描述了常见问题、解决方法以及如何获得支持。
常见问题解答提供常见问题的答案。
发行说明列出了与 Docker Desktop 版本相关的组件更新、新功能和改进。
备份和恢复数据提供了有关备份和恢复与 Docker 相关的数据的说明。
