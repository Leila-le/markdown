# screen
常用的 screen 命令：

    screen：启动一个新的screen会话。
    screen -S session_name：启动一个新的具有指定名称的screen会话。
    screen -ls：列出所有正在运行的screen会话。
    screen -r session_id：恢复到指定的screen会话。
    Ctrl + A，然后按 c：在当前screen会话中创建一个新的终端窗口。
    Ctrl + A，然后按 n：在screen会话中切换到下一个窗口。
    Ctrl + A，然后按 p：在screen会话中切换到上一个窗口。
    Ctrl + A，然后按 d：分离（detach）当前screen会话，返回到原始终端窗口。
    screen -X -S session_id quit：关闭指定的screen会话。

  ## 将screen中Attached转为Detached，可以使用命令screen -d [session_id]。

    其中，[session_id]是screen会话的ID或名称。执行此命令后，将把指定会话从Attached状态转换为Detached状态，以便您可以在后台继续运行该会话，而不会影响您当前终端的使用。

    需要注意的是，如果您直接关闭了shell，但服务器不知道您要detached该screen，可能会导致下次无法访问。此时，您可以使用screen -r [session_id]命令恢复之前detached的screen会话。

# htop
    htop 是一个交互式的系统监视工具，用于在终端中实时监视系统资源的使用情况。它提供了一个更友好和直观的界面，相比于传统的 top 命令，更易于使用和理解。

使用 htop，您可以查看系统中正在运行的进程、CPU 使用情况、内存使用情况、磁盘活动、网络流量等系统资源的信息。

以下是一些常用的 htop 命令和功能：

    运行 htop：在终端中直接输入 htop 命令即可启动 htop。

    进程列表：htop 显示运行在系统上的进程列表，包括每个进程的 PID、用户、CPU 使用率、内存使用率等信息。进程列表按照 CPU 使用率或内存使用率进行排序。

    快捷键：htop 提供了一些快捷键来执行不同的操作，例如：
        F1 或 h：显示 htop 的帮助文档。
        F2 或 S：对进程进行排序，可以根据不同的属性进行排序。
        F3 或 /：根据进程的名称进行筛选。
        F4 或 I：显示或隐藏内部线程。
        F5 或 t：在进程列表中切换不同的显示模式。
        F9 或 k：发送信号给选定的进程。
        F10 或 q：退出 htop。

    CPU 和内存信息：htop 显示 CPU 和内存的使用情况，包括总体使用率、每个 CPU 核心的使用率、物理和交换内存的使用情况等。

    实时刷新：htop 实时刷新并显示系统资源的变化情况。您可以通过查看实时更新的数据来监视系统的性能和资源使用情况。

请注意，htop 可能不是默认安装在所有 Linux 发行版上，您可能需要先安装它。您可以使用相应的包管理器来安装 htop，例如 apt（Ubuntu/Debian）、yum（CentOS/RHEL）或 dnf（Fedora）等。

总之，htop 是一个强大的系统监视工具，提供了更好的用户界面和交互体验，使您能够更方便地监视和管理系统资源。
