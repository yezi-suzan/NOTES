# 了解 Windows 的权限要求

此页面包含有关在 Windows 上运行和安装 Docker Desktop 的权限要求、特权助手进程的功能 com.docker.service 以及此方法背后的原因的信息。

它还提供了关于正在运行的容器的清晰度，而 root 不是 Administrator 在主机上的访问权限以及 Windows Docker 引擎和 Windows 容器的权限。

## 权限要求

虽然 Windows 上的 Docker Desktop 可以在没有特权的情况下运行 Administrator，但在安装过程中确实需要特权。安装时，用户会收到一个 UAC 提示，允许安装特权帮助程序服务。之后，Docker Desktop 可以由没有管理员权限的用户运行，前提是他们是该 docker-users 组的成员。执行安装的用户会自动添加到该组，但其他用户必须手动添加。这允许管理员控制谁有权访问 Docker Desktop。

采用这种方法的原因是 Docker Desktop 需要执行一组有限的特权操作，这些操作由特权助手进程执行 com.docker.service。遵循最小特权原则，这种方法允许 Administrator 仅将访问权限用于绝对必要的操作，同时仍然能够以非特权用户身份使用 Docker Desktop。

## 特权帮手

特权帮助程序 com.docker.service 是一种 Windows 服务，它在后台以 SYSTEM 特权运行。它侦听命名管道//./pipe/dockerBackendV2。开发人员运行 Docker Desktop 应用程序，该应用程序连接到命名管道并向服务发送命令。这个命名管道是受保护的，只有属于该 docker-users 组的用户才能访问它。

该服务执行以下功能：

- 确保 kubernetes.docker.internal 在 Win32 主机文件中定义。定义 DNS 名称 kubernetes.docker.internal 允许 Docker 与容器共享 Kubernetes 上下文。
- 安全地缓存对开发人员只读的注册表访问管理策略。
- 创建 Hyper-V VM"DockerDesktopVM"并管理其生命周期 - 启动、停止和销毁它。VM 名称硬编码在服务代码中，因此该服务不能用于创建或操作任何其他 VM。
- 获取 VHDX 磁盘大小。
- 移动 VHDX 文件或文件夹。
- 启动和停止 Windows Docker 引擎并查询它是否正在运行。
- 删除所有 Windows 容器数据文件。
- 检查是否启用了 Hyper-V。
- 检查引导加载程序是否激活 Hyper-V。
- 检查是否安装并启用了所需的 Windows 功能。
- 进行健康检查并检索服务本身的版本。

服务启动方式取决于选择的容器引擎：

- 对于 Windows 容器或 Hyper-v Linux 容器，该服务会在系统启动时启动并一直运行，即使 Docker Desktop 未运行时也是如此。这是用户能够在没有管理员权限的情况下启动 Docker Desktop 所必需的。如果用户切换到 WSL2 Linux 容器，该服务将停止并且不会在下次 Windows 启动时自动启动。
- 对于 WSL2 Linux 容器，该服务不是必需的，因此不会在系统启动时自动运行。如果用户切换到 Windows 容器或 Hyper-v Linux 容器，则会显示 UAC 提示，要求用户接受特权操作以启动服务。如果接受，该服务将启动并设置为在下次 Windows 启动时自动启动。

## 在 Linux VM 中以 root 身份运行的容器

Linux Docker 守护进程和容器在由 Docker 管理的最小的专用 Linux VM 中运行。它是不可变的，因此用户无法扩展它或更改已安装的软件。这意味着尽管容器默认运行为 root，但这不允许更改 VM 并且不授予 Administrator 对 Windows 主机的访问权限。Linux VM 充当安全边界并限制可以访问主机的哪些资源。文件共享使用用户空间精心制作的文件服务器，主机绑定到 Docker 容器中的任何目录仍然保留其原始权限。它不会授予用户访问其尚未访问的任何文件的权限。

## Windows 容器

与在 VM 中运行的 Linux Docker 引擎和容器不同，Windows 容器是一种操作系统功能，可以直接在具有 Administrator 特权的 Windows 主机上运行。对于不希望其开发人员运行 Windows 容器的组织，–no-windows-containers 从 4.11 版开始可以使用安装程序标志来禁用它们。

## 网络 🔗
对于网络连接，Docker Desktop 使用用户空间进程 ( vpnkit)，它从启动它的用户那里继承了防火墙规则、VPN、HTTP 代理属性等约束。
