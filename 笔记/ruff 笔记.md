---
date: 2016-09-14 23:42
status: public
title: 'Ruff 笔记'
---

# 配网
执行 `rap wifi` 不能进行配网设置，原理应该类似 `EasyLink` 吧，但是蓝色 LED 没有闪烁，应该没能收到配置。
根据官网文档，按 `FUNC` 按键进入 AP 模式，执行 `rap wifi --lan ap` 根据提示完成了配网。
# 固件升级
配网之后，想尝试部署一下 demo，执行 `rap deploy -s` 的时候提示：
```
WARN The RuffOS version (0.9.1) does not match rap version (1.4.0), please consider upgrading RuffOS or SDK.
```
然而下载新的固件准备执行命令升级：
```
rap system upgrade --hostname ip-address path-to-firmware-file
```
然而提示：
```
WARN The RuffOS version (0.9.1) does not match rap version (1.4.0), please consider upgrading RuffOS or SDK.
```
想了想，收到的板子固件版本是 `0.9.1` 的，刚开始设定 SDK 的时候直接制定的是最新 `1.4.0` 版本。切换到 `0.9.1` 版本的 SDK，然后执行命令升级开发版固件到 `1.4.0`，然后再将 SDK 版本切回到 `1.4.0`，重新配网，即可正常部署程序。