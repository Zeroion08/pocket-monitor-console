# Redmi G Pro 27U 手机控制台 (Pocket Monitor Console)

> **基于 [YiHoooong/Mimonitor_Toolbox](https://github.com/YiHoooong/Mimonitor_Toolbox) 二次开发**

用手机 ADB 无线控制红米 G Pro 27U 显示器 —— 亮度、对比度、图像模式、信号源、精密控光、HDR/SDR 记忆，还有 ADB 保活守护，重启显示器再也不用手动开 ADB。

## 致谢与声明

**本项目的命令层、参数映射、ADB 协议实现、ADB 保活守护均源自原作者的工作。**

| | |
|---|---|
| **原作者** | [@YiHoooong](https://github.com/YiHoooong) |
| **原仓库** | [YiHoooong/Mimonitor_Toolbox](https://github.com/YiHoooong/Mimonitor_Toolbox) |
| **原项目描述** | Redmi G Pro 27U 2026 显示器 ADB 控制工具（第三方桌面控制台） |

> ⚠️ 原仓库当前**未声明开源许可证**，版权归 @YiHoooong 所有。本仓库是基于其研究与实现的**移动端移植 + 功能扩展**，仅供学习交流使用。如需商用或二次分发，请先联系原作者获取授权。

### 本项目额外做的事情

- 📱 **手机 App**（Android）：完整的手机端控制器，不再需要电脑
- 🔄 **自动重连**：后台挂久了自动恢复连接，不再报 Broken pipe
- 🎯 **HDR/SDR 分档**：图像模式按信号源自动切换 HDR/SDR 枚举
- 🧠 **HDR/SDR 精密控光记忆**：SDR/HDR 各存一个档位，切换自动应用
- 🛡️ **ADB 保活一键部署**：内置守护 APK，全新显示器一键安装
- 🎨 **全新 UI**：深色主题 + 橙色点缀，排版适配手机

## 下载

| 文件 | 说明 |
|---|---|
| [`PocketMonitorConsole.apk`](./dist/PocketMonitorConsole.apk) | 手机 App 安装包（推荐） |
| [`ADB保活部署教程.txt`](./dist/ADB保活部署教程.txt) | 保活守护保姆级教程 |
| [`Fix-ADB-Connect.zip`](./dist/Fix-ADB-Connect.zip) | 电脑端 ADB 连接修复脚本（分享版） |

> APK 版本 2.5（versionCode 25），覆盖安装即可升级。

## 快速开始

### 1. 安装 APK

把 `PocketMonitorConsole.apk` 传到手机上安装。

### 2. 连接显示器

- 手机和显示器连**同一个 WiFi**（不要用访客网络）
- 打开 App → 输入显示器 IP（默认 `192.168.1.8`）→ 点「连接」
- 显示器 IP 在：遥控器 → 设置 → 网络

### 3. 部署 ADB 保活（推荐，一次性）

- 点底部「设置」→ 找到「ADB 保活守护」→ 点「**一键部署 / 修复**」
- 之后重启显示器，ADB 自动恢复，不用再手动开

详细步骤见 [`ADB保活部署教程.txt`](./dist/ADB保活部署教程.txt)

## 功能

| 页面 | 功能 |
|---|---|
| **主控台** | 图像模式（标准/游戏/电影）、亮度、精密控光、快捷控制 |
| **画面** | 亮度、对比度、色温、动态对比度、HDR 色调映射、动态清晰度、暗部增强等 |
| **信号源** | HDMI 1 / HDMI 2 / DP / USB-C 一键切换 |
| **设置** | 设备地址管理、ADB 保活部署、HDR/SDR 记忆、自动重连 |

### HDR/SDR 分档

| 按钮 | SDR 信号 | HDR 信号 |
|---|---|---|
| 标准 | 14 | 22 |
| 游戏 | 10 | 15 |
| 电影 | 9 | 17 |

### HDR/SDR 精密控光记忆

开启后，手动调精密控光会自动记入当前档位（SDR 或 HDR）；切换信号时自动应用对应档位的值。

## 电脑端工具

如果需要电脑控制台：

- **Windows**：`RedmiMonitorConsole.exe`（完整桌面版）
- **ADB 修复脚本**：`Fix-ADB-Connect.bat`（解决 adb daemon 冷启动慢导致的连接超时）

## 技术细节

- **纯 Java 实现**，无 Gradle，无 Android Studio，无第三方依赖
- **ADB 协议层**：TCP 直连 adbd（端口 5555），含 AUTH SHA1 签名、shell/sync 通道
- **构建**：`bash build_apk.sh`（aapt2 → javac → d8 → zipalign → apksigner）
- **min SDK 24**（Android 7.0+），target SDK 34

## 仓库结构

```
├── android_app/              # 手机 App 源码 + 构建脚本
│   ├── src/com/pocket/mimonitor/
│   ├── assets/               # 内置 ADB 密钥 + 守护 APK
│   └── build_apk.sh          # 构建脚本
├── dist/                     # 发布文件（APK + 教程 + 修复脚本）
├── minimal_ui/               # Windows 桌面版源码（极简控制台）
├── adb-fix-share/            # ADB 连接修复脚本
└── README.md
```

## 免责声明

- 本工具通过 ADB 调试接口控制显示器，属非官方用法
- 小米可能在后续系统更新中限制此行为，请谨慎使用
- 使用本工具造成的任何后果自负
- **请尊重原作者的劳动成果，保留本声明与致谢**

## License

原仓库 [YiHoooong/Mimonitor_Toolbox](https://github.com/YiHoooong/Mimonitor_Toolbox) 未声明许可证。

本仓库的**手机端移植代码**以 [MIT License](./LICENSE) 发布；原作者的命令层/协议实现/守护 APK 仍归原作者所有。
