---
title: windows11/10鼠标右键菜单样式切换
date: 2023-09-07 10:52:52
categories:
- Windows
tags:
---

恢复win10右键

```
reg.exe add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve
```

重启任务管理器使修改生效

```
taskkill /f /im explorer.exe & start explorer.exe
```

恢复win11右键，执行后立即生效

```
reg.exe delete "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /va /f
```

