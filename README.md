<img src="https://content.arduino.cc/website/Arduino_logo_teal.svg" height="100" align="right" />

# Arduino IDE 2.x

[![Build status](https://github.com/arduino/arduino-ide/actions/workflows/build.yml/badge.svg)](https://github.com/arduino/arduino-ide/actions/workflows/build.yml)
[![Check JavaScript status](https://github.com/arduino/arduino-ide/actions/workflows/check-javascript.yml/badge.svg)](https://github.com/arduino/arduino-ide/actions/workflows/check-javascript.yml)
[![Test JavaScript status](https://github.com/arduino/arduino-ide/actions/workflows/test-javascript.yml/badge.svg)](https://github.com/arduino/arduino-ide/actions/workflows/test-javascript.yml)

## 项目简介

This repository contains the source code of the Arduino IDE 2.x. If you're looking for the old IDE, go to the [repository of the 1.x version](https://github.com/arduino/Arduino).

The Arduino IDE 2.x is a major rewrite, sharing no code with the IDE 1.x. It is based on the [Theia IDE](https://theia-ide.org/) framework and built with [Electron](https://www.electronjs.org/). The backend operations such as compilation and uploading are offloaded to an [arduino-cli](https://github.com/arduino/arduino-cli) instance running in daemon mode. This new IDE was developed with the goal of preserving the same interface and user experience of the previous major version in order to provide a frictionless upgrade.

![](static/screenshot.png)

## 快速开始

### 下载

You can download the latest release version and nightly builds from the [software download page on the Arduino website](https://www.arduino.cc/en/software).

### 中文用户编译报错修复

Windows 系统下使用中文用户名的用户在编译 Arduino 草图时可能会遇到编译失败的问题，主要原因是默认的构建路径包含中文，导致链接器无法正确处理路径。

#### 解决方案

1. **配置 settings.json 文件**
   - **文件路径**：`C:\Users\您的用户名\AppData\Roaming\Arduino IDE\settings.json`
   - **核心配置**：
     ```json
     {
       "window.titleBarStyle": "native",
       "editor.fontSize": 14,
       "workbench.colorTheme": "arduino-theme",
       "files.autoSave": "afterDelay",
       "editor.quickSuggestions": {
         "other": false,
         "comments": false,
         "strings": false
       },
       "arduino.window.autoScale": true,
       "window.zoomLevel": 0,
       "arduino.compile.verbose": true,
       "arduino.compile.warnings": "None",
       "arduino.upload.verbose": false,
       "arduino.upload.verify": false,
       "arduino.sketchbook.showAllFiles": false,
       "arduino.build.path": "C:\\buildpath"
     }
     ```

2. **配置 arduino-cli.yaml 文件**
   - **文件路径**：`C:\Users\您的用户名\.arduinoIDE\arduino-cli.yaml`
   - **核心配置**：
     ```yaml
     board_manager:
       additional_urls: []
     build_cache:
       compile: true
       path: C:\project\buildpath
     daemon:
       port: "50051"
     directories:
       data: C:\project\arduino15
       downloads: C:\project\arduino15\staging
       user: C:\project\Arduino
     library:
       enable_unsafe_install: false
     logging:
       file: ""
       format: text
       level: info
     sketch:
       always_export_binaries: false
     updater:
       enable_notification: true
     ```

#### 配置说明

- **arduino.build.path**：Arduino IDE 的构建路径，必须使用不含中文和特殊字符的路径
- **build_cache.path**：Arduino CLI 的构建缓存路径，建议与 IDE 的 build.path 保持一致
- **directories**：Arduino 数据目录配置，包括板卡包、库等存储位置

#### 使用步骤

1. 按照上述格式创建或修改配置文件
2. 完全关闭并重新启动 Arduino IDE
3. 打开并编译一个草图，验证编译是否成功
4. 检查编译输出，确认构建路径已更改为您指定的路径

#### 注意事项

- **路径选择**：选择一个不含中文、空格和特殊字符的路径
- **目录存在**：确保指定的目录已存在，IDE 可能不会自动创建目录结构
- **权限问题**：确保对指定目录有读写权限
- **重启要求**：修改配置后必须重启 IDE 才能生效
- **路径长度**：避免使用过长的路径，以免遇到 Windows 路径长度限制

## 支持

If you need assistance, see the [Help Center](https://support.arduino.cc/hc/en-us/categories/360002212660-Software-and-Downloads) and browse the [forum](https://forum.arduino.cc/index.php?board=150.0).

## Bugs & Issues

If you want to report an issue, you can submit it to the [issue tracker](https://github.com/arduino/arduino-ide/issues) of this repository.

See [**the issue report guide**](docs/contributor-guide/issues.md#issue-report-guide) for instructions.

### Security

If you think you found a vulnerability or other security-related bug in this project, please read our
[security policy](https://github.com/arduino/arduino-ide/security/policy) and report the bug to our Security Team 🛡️
Thank you!

e-mail contact: security@arduino.cc

## 贡献和开发

Contributions are very welcome! There are several ways to participate in this project, including:

- Fixing bugs
- Beta testing
- Translation

See [**the contributor guide**](docs/CONTRIBUTING.md#contributor-guide) for more information.

See the [**development guide**](docs/development.md) for a technical overview of the application and instructions for building the code.

### Support the project

This open source code was written by the Arduino team and is maintained on a daily basis with the help of the community. We invest a considerable amount of time in development, testing and optimization. Please consider [buying original Arduino boards](https://store.arduino.cc/) to support our work on the project.

## 许可证

The code contained in this repository and the executable distributions are licensed under the terms of the GNU AGPLv3. The executable distributions contain third-party code licensed under other compatible licenses such as GPLv2, MIT and BSD-3. If you have questions about licensing please contact us at [license@arduino.cc](mailto:license@arduino.cc).