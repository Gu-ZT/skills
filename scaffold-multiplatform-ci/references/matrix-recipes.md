# 多平台与多架构矩阵配置参考

先根据下表盘点目标平台，再结合仓库实际的编译器、SDK、原生依赖和打包工具确认矩阵配置。

| 平台 | 常用 Runner | 目标三元组示例 | 常见产物格式 | 注意事项 |
| --- | --- | --- | --- | --- |
| Windows | `windows-latest` | `x86_64-pc-windows-msvc`、`aarch64-pc-windows-msvc` | NSIS `.exe`、`.msi` | 需安装对应架构的 Windows SDK；ARM64 可能需要专用 runner 或交叉链接器 |
| Linux | `ubuntu-22.04` | `x86_64-unknown-linux-gnu`、`aarch64-unknown-linux-gnu` | `.deb`、`.rpm`、`AppImage`、`.tar.gz` | 含 GUI 依赖时，ARM64 通常需要原生 ARM runner 或配置 sysroot 交叉工具链 |
| macOS | `macos-14`、`macos-13` | `aarch64-apple-darwin`、`x86_64-apple-darwin` | `.app`、`.dmg`、`.tar.gz` | 涉及原生 Framework 或签名公证时，runner 架构尽量与目标架构一致 |
| Android | `ubuntu-latest` | `aarch64-linux-android`、`x86_64-linux-android` | `.apk`、`.aab` | 使用项目配置的 Gradle/NDK 工具链，并将签名密钥输入隔离在独立步骤中 |

## 矩阵编写规范

从应用可支持的全部平台和架构出发，同时评估 Windows 与 Linux 的 `x86_64` / `aarch64`，以及 macOS 的 Apple Silicon（`aarch64`）与 Intel（`x86_64`）。仅当源码、依赖库、SDK、许可证或工具链存在明确阻塞时才移除对应条目，并在文档中记录原因。缺少某架构的原生 runner 只影响能否执行运行时冒烟测试，禁止仅因无法运行冒烟测试就将可交叉编译的目标从 CI 中删除。

当不同平台的依赖安装与打包参数存在差异时，优先使用显式 `matrix.include` 列表：

```yaml
strategy:
  fail-fast: false
  matrix:
    include:
      - platform: windows
        runner: windows-latest
        target: x86_64-pc-windows-msvc
        cache_key: windows-x86_64
        package: nsis
      - platform: linux
        runner: ubuntu-22.04
        target: x86_64-unknown-linux-gnu
        cache_key: linux-x86_64
        package: deb,appimage
      - platform: macos
        runner: macos-14
        target: aarch64-apple-darwin
        cache_key: macos-aarch64
        package: app,dmg
```

当某个平台的前置环境、签名流程或打包 Action 与其他平台差异过大时，拆分为独立 job；禁止用统一矩阵掩盖缺失的密钥或不支持的交叉编译器。

## 目标产物校验步骤

每个矩阵目标必须依次完成以下校验：

1. 通过工具链 Action 或系统包管理器安装目标架构编译环境。
2. 构建面向最终用户的实际安装包格式。
3. 校验产物文件名、二进制架构头信息（如 PE/ELF/Mach-O 架构标志）及内嵌运行时文件。
4. 当 runner 架构可直接运行目标产物时，执行安装或启动冒烟测试。
5. 当 runner 无法直接运行交叉编译产物时，必须在 CI 中完成编译、打包、二进制架构头校验与产物分类，并在文档和 Release Notes 中注明该架构未经过原生运行时验证、显式排除的目标架构及代码签名限制。
6. 交叉编译 GUI 或原生桌面应用时，除语言层编译通过外，必须独立校验链接器、系统 SDK、Framework 与系统扩展依赖并完成实际安装包构建。
