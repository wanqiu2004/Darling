Tauri 利用了每个用户系统中已有的原生 WebView。因此，Tauri 应用只包含特定于该应用的代码和资源，不需要为每个应用捆绑一个浏览器引擎。一个最小的 Tauri 应用体积可以小于 600KB。
依赖：MSVCv143-VS 2022 C++x64/x86Spectre 缓解
- Rust
- Desktop development with C++
- MSVCv143-VS 2022 C++x64/x86Spectre
- 如果你的系统未安装 WebView2，请按照以下步骤手动安装：访问 WebView2 Runtime 下载页面。下载并安装 “Evergreen Bootstrapper” 版本。


### 可以使用 Tauri CLI 单独初始化项目的后端部分。
```
yarn add -D @tauri-apps/cli@latest
yarn tauri init
yarn tauri dev
yarn tauri build --no-bundle
```

# TODO:Core Concepts and Security

Tauri 会自动监视你的 Rust 文件的变化。一旦你修改了其中的任何文件，Tauri 会自动重新构建应用并重启它。这与 webview 中实时反映变化的方式类似。
`yarn tauri dev --no-watch`

始终将 src-tauri/Cargo.lock 和 src-tauri/Cargo.toml 一起commit，以确保构建的确定性。
不要提交：避免提交 src-tauri/target 目录或其中的任何内容，因为它包含构建产物。


### 一定将构建和打包步骤分开
关于Distribute还少了 [Windows Installer](https://v2.tauri.app/distribute/windows-installer/)
对应用程序的可执行文件和打包文件进行数字签名


#  后端控制前端行为外观数据等等
Rust 端可以通过利用 Tauri 的事件系统、使用**通道**或**直接执行 JavaScript **代码来调用前端。


事件系统，您可以使用它在 Rust 和前端之间实现双向通信。适用于需要传输少量数据
