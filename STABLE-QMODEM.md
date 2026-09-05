# XG-040G-MD 稳定版 QModem 构建说明

这套配置专用于 Nokia Bell XG-040G-MD，构建目标是稳定版、硬件加速和常见 USB 移动通信模组兼容。

## 固定的源码

- ImmortalWrt 正式版标签：`v25.12.1`
- ImmortalWrt 正式版提交：`a3378d1a2c15beb2faf4b0bce9c00f07143efa29`
- XG-040G-MD 支持：本仓库 `patch-25.12` 固定补丁集
- QModem v3.2.0：`dbe77b3cf262c2cb83916cf5c65bc18c98aa9b91`
- iStore：`3fca15b30aeed9ecacb3efc8b4a8b9c2584ad5c7`
- iStore 构建依赖：同时安装 `luci-lib-taskd`、`luci-lib-xterm` 和 `taskd`
- 在线软件源：ImmortalWrt 25.12.1 官方 `aarch64_cortex-a53` 软件仓库

## 已集成功能

- Airoha EN7581 NPU/PPE 硬件加速及管理页面
- QModem v3.2.0 Next 管理页面
- USB QMI、MBIM、NCM、RNDIS、CDC Ethernet、华为 NCM、Sierra 等驱动
- USB ACM、Option、Qualcomm、Sierra 串口驱动
- Android USB 共享网络、iPhone USB 共享网络
- Samba 4 网络共享、LuCI FileBrowser 文件管理
- ext4、exFAT、NTFS3、FAT USB 存储
- iStore 软件商店

## 构建

把本目录上传到 GitHub 仓库，在 Actions 中手动运行 `XG-040G-MD` 工作流。工作流会校验所有固定提交和必需软件包，然后生成 `sysupgrade.bin`、`factory.bin`、完整配置、软件包和 SHA-256 校验值。

`sysupgrade.bin` 只能在设备上先通过 `sysupgrade -T` 校验后再刷入。不要用 `factory.bin` 覆盖当前 tcboot/UBI 布局。

## 软件源说明

官方没有发布 XG-040G-MD 的 `airoha/an7581` 25.12.1 内核模块仓库。因此固件将所需内核驱动直接编译进镜像，在线列表仅保留可用的官方应用仓库。iStore 使用自己的独立仓库，不会替换 ImmortalWrt 官方源。
