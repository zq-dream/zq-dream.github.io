---
title: Windows 自动更新暂停「续杯」
date: 2023-09-08 11:09:12
categories:
- Windows
tags:
---

# Windows 自动更新暂停「续杯」

按下 `Win-R` 打开「运行」对话框，在输入 `cmd` 后按下`Ctrl-Shift-Enter`，在弹出来的黑色窗口中输入下列代码，并敲击回车。

```shell
reg add “HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings” /v FlightSettingsMaxPauseDays /t reg_dword /d 3000 /f

```

打开「Windows 设置」，前往「更新和安全」-「Windows 更新」，点击「暂停更新 7 天」的按钮，直至满足暂停时长的需要。
