---
title: 安卓远程控制（切换用户，scrcpy等）
date: 2024-12-28
---

女朋友总是不喜欢给手机充电。有一次她要去上海，手机没电了，我只好把我的手机开了个账户借给她。

安卓上切换账户是需要当前账户的密码的。结果她从她的账户切成了我的，没密码进不去，但也切不走。最后把我的密码骗走了。

这不好吧！我就想，该怎么解决呢？于是有了下面这套方案：

1. [MagiskSSH](https://gitlab.com/d4rcm4rc/MagiskSSH)用于远程连接
2. [Magisk-Tailscaled](https://github.com/anasfanani/Magisk-Tailscaled)用于内网穿透（不在同一Wi-Fi也能连）
3. 切换用户：
    ```sh
    # First, list user and obtain user ID
    pm list users

    # Then, switch to the desired account
    am switch-user User_ID
    ```
4. 打开adb over tcp（这样就可以scrcpy了）：
    ```sh
    setprop service.adb.tcp.port 8897  # Specify your desired port here
    setprop ctl.restart adbd
    ```

    关闭adb over tcp：
    ```sh
    setprop service.adb.tcp.port -1
    setprop ctl.restart adbd
    ```
