# AutoX.js v7

<p align="center">
  <em>Android 上无障碍驱动的 JavaScript 自动化与开发平台</em><br>
  <img src="https://img.shields.io/github/downloads/aiselp/AutoX/total" alt="downloads" />
  <img src="https://img.shields.io/github/issues/aiselp/AutoX" alt="issues" />
  <img src="https://img.shields.io/github/actions/workflow/status/aiselp/AutoX/android-test.yml" alt="ci" />
  <img src="https://img.shields.io/github/v/release/aiselp/AutoX" alt="release" />
  <a href="https://app.codacy.com/gh/aiselp/AutoX/dashboard?utm_source=gh&utm_medium=referral&utm_content=&utm_campaign=Badge_grade">
    <img src="https://app.codacy.com/project/badge/Grade/ca72518c8bd548f9a350d5a15e2ed9ea" alt="codacy" />
  </a>
</p>

[English Document](README_en.md)

## 概要
- AutoX.js v7 是基于 hyb1996 [Auto.js](https://github.com/hyb1996/Auto.js) 的衍生版本，为 Android 提供无障碍驱动的自动化脚本运行时与 IDE，目标体验类似 JsBox/Workflow。
- 支持以 JavaScript/TypeScript 编写自动化脚本，具备代码补全、格式化、打包 APK、界面分析、录屏/截图找色找图等专业能力。
- 新版引入 Node.js 引擎（基于 [Javet](https://github.com/caoccao/Javet)），Material Design 3 UI、Vue3 + Jetpack Compose 框架、Shizuku 动态调试、完善的签名/打包工具链以及类型声明完善的 v7 API（持续完善中）。

## 仓库结构
- `app/`：Android 客户端（Compose + Vue3 混合 UI）、模板应用与打包逻辑。
- `autojs/`：核心脚本引擎与无障碍自动化实现，包含 v7 API 与测试。
- `automator/`：自动化执行器、Shizuku/无障碍适配等底层支持。
- `apkbuilder/`：打包与签名相关工具。
- `codeeditor/`：内置代码编辑器与类型声明支持。
- `paddleocr/`：OCR 能力集成。
- `common/`、`buildSrc/`：共享工具、Gradle 插件与构建脚本。
- 更多示例位于 `app/src/main/assets/sample/`，变更记录见 [CHANGELOG](CHANGELOG.md)。

## 快速开始（运行应用）
1. 前置条件：安装 JDK 17、Android Studio（含 Android SDK/NDK）、Node.js 20+。
2. 克隆仓库并进入根目录。
3. 首次构建前编译 JS 模块：
   ```shell
   ./gradlew autojs:buildJsModule
   ```
4. 构建并安装调试版到已连接的设备：
   ```shell
   ./gradlew app:buildDebugTemplateApp && ./gradlew app:assembleV7Debug && ./gradlew app:installV7Debug
   ```
5. 设备允许安装后即可在手机上启动 AutoX.js v7。

## 构建与安装
### 命令行（Gradle）
- 构建文档（如需刷新内置文档）：
  ```shell
  ./gradlew app:buildDocs
  ```
- 构建发布版（未签名）：
  ```shell
  ./gradlew app:buildTemplateApp && ./gradlew app:assembleV7
  ```
  产物位于 `app/build/outputs/apk/v6/release`，请按需签名后安装。

### Android Studio
1. 运行调试版：先执行 `./gradlew app:buildDebugTemplateApp`，再在 Android Studio 点击运行按钮选择连接设备。
2. 生成签名发布版：先执行 `./gradlew app:buildTemplateApp`，再在菜单 **Build → Generate Signed Bundle/APK...** 中选择 APK，配置证书，勾选 `v7Release` 变体并完成向导，生成产物位于 `app/v7/release`。

## 下载与文档
- 官方文档：https://autox-doc.vercel.app/
- 发行版下载：[Releases](https://github.com/aiselp/AutoX/releases)（若下载缓慢可复制 APK 链接至 https://toolwa.com/github/ 加速）。
- PC 端开发：VS Code 插件 [auto-js-vsce-fixed](https://marketplace.visualstudio.com/items?itemName=aaroncheng.auto-js-vsce-fixed)。
- 社区：论坛 [www.autoxjs.com](http://www.autoxjs.com)。
- 变更日志：[CHANGELOG](CHANGELOG.md)。

## 贡献与反馈
- 欢迎提交 Issue/PR 参与维护：可聚焦 bug 修复、v7 API 完善、TypeScript 类型、UI/文档优化等。
- 贡献前请先同步最新主分支，保持 commit 清晰；提交 PR 时附上必要的复现步骤或截图。
- 反馈问题时请提供设备型号、系统版本、AutoX.js 版本及复现脚本/日志，便于定位。

## 许可证
- 项目使用 [GPL-2.0](LICENSE-GPL-V2.md)，同时沿用上游 [MPL-2.0](https://www.mozilla.org/MPL/2.0) 约束；使用与分发需同时遵守两种许可的要求。
- 更多详情请参阅 `LICENSE-GPL-V2.md`、`LICENSE.md` 以及上游许可说明。

## 常见问题与排障
- **构建失败（Node 版本过低）**：确认已安装 Node.js 20+ 并重新执行 `./gradlew autojs:buildJsModule`。
- **Gradle 缓存或依赖异常**：执行 `./gradlew --refresh-dependencies`，或清理 `~/.gradle/caches` 后重试。
- **设备无法安装 APK**：检查是否允许从 USB 安装；发布版需使用有效证书签名。
- **Shizuku/无障碍权限问题**：确保已在设备上授予相应权限，或在应用设置中重新启用无障碍服务。
- **更多示例与帮助**：查看内置示例 `app/src/main/assets/sample/` 或访问官方文档。

