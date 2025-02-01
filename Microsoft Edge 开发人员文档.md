- DevTools检查和调试网页、编辑源文件，模拟设备，调试JS，将更改同步到本地文件

- 扩展也叫加载项、对网站功能的加强

- WebDriver自动化、

- 渐进式Web 应用(PWA) 类原生

- WebView2 在本机应用中嵌入 web 技术使用 Microsoft Edge 作为绘制引擎，在本机应用中显示 web 内容。
可以在本机应用的不同部分嵌入 Web 代码，或在单个 WebView2 实例中生成所有本机应用。 


### Edge扩展

必不可少的是：**HTML CSS JS JSON**

浏览器选项卡是独立线程
扩展在独立于选项卡页的单个线程中运行。

扩展和选项卡页的数据和行为是相互独立的，需要通过指定的 API 进行通信。
确保它们的行为和数据不会相互干扰。

生成的扩展一般是 zip 文件，根目录含一个manifest.json文件
清单文件包括扩展的版本、标题、扩展运行所需的权限等。

浏览器启动时，会将扩展作为一个 Web “虚拟”服务器，专门为扩展提供服务。

当用户打开扩展时，浏览器会访问 Web 服务器上的 URL，下载文件并渲染页面。


#### EXAMPLE
第一个示例太简单啦，直接编写HTML文件，准备一个128的jpg的icon就好

content.js 文件，注入到网页中
popup.js 向content.js发送消息，指定要显示的图片和相关参数
content.js通过API监听到消息


#### 清单文件
```
{
  // 必需字段
  "manifest_version": 3,
  "name": "我的 V3 扩展",
  "version": "版本号",

  // 推荐字段
  "action": {...},
  "default_locale": "en",
  "description": "纯文本描述",
  "icons": {...},

  // 可选字段
  "author": "作者名称",
  "background": {
    // 如果包含 `background`，则必须指定 `service_worker`
    "service_worker": "脚本路径"
  },
  "chrome_settings_overrides": {...},
  "chrome_url_overrides": {...},
  "commands": {...},
  "content_capabilities": {...},
  "content_scripts": [{...}],
  "content_security_policy": "策略字符串",
  "devtools_page": "devtools.html",
  "externally_connectable": {
    "matches": ["*://*.example.com/*"]
  },
  "file_browser_handlers": [...],
  "host_permissions": ["*://*.example.com/*"],
  "permissions": ["tabs"],
  "options_ui": {
    "page": "options.html",
    "chrome_style": true
  },
  "short_name": "简短名称",
  "storage": {
    "managed_schema": "schema.json"
  },
  "update_url": "http://更新地址.xml",
  "web_accessible_resources": [...]
}
```


默认策略通过以下三种方式提升了扩展的安全性：

禁用 eval 及相关函数
禁止运行内联 JavaScript
仅加载本地脚本和对象资源


默认情况下，扩展程序只能加载本地资源，而不能从外部网络加载。例如，若需使用 jQuery，不应依赖 CDN，而是将 jQuery 文件直接打包到扩展程序中。
为增强安全性，可进一步收紧策略。例如，限制所有资源仅从扩展程序包中加载：
"content_security_policy": "default-src 'self'"


| API                     | 描述                                                                                                                      | Manifest 版本 |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------|--------------|
| accessibilityFeatures   | 管理浏览器的辅助功能设置。                                                                                               | MV2, MV3     |
| action                  | 控制扩展程序在浏览器工具栏中的图标。                                                                                     | MV3          |
| alarms                  | 定时执行代码，可设置为定期运行或在未来指定时间点运行。                                                                   | MV2, MV3     |
| bookmarks               | 创建、组织和操作书签。                                                                                                   | MV2, MV3     |
| browserAction           | 使用浏览器操作在 Microsoft Edge 工具栏中放置图标，并支持添加工具提示、徽章或弹出框。                                       | MV2          |
| browsingData            | 从用户的本地配置文件中移除浏览数据。                                                                                     | MV2, MV3     |
| commands                | 添加快捷键以触发扩展程序中的操作，例如打开浏览器或发送命令。                                                             | MV2, MV3     |
| contentSettings         | 自定义 Microsoft Edge 在每个站点上的行为，例如是否允许使用 Cookie、JavaScript 和插件等功能。                              | MV2, MV3     |
| contextMenus            | 向 Microsoft Edge 的上下文菜单（右键菜单）中添加条目，支持针对图像、超链接和页面等对象。                                  | MV2, MV3     |
| cookies                 | 查询和修改 Cookie，并接收 Cookie 更改的通知。                                                                            | MV2, MV3     |
| debugger                | 附加到选项卡以调试 JavaScript、修改 DOM、CSS 等内容，或监控网络交互。                                                    | MV2, MV3     |
| declarativeContent      | 根据页面内容执行操作，无需权限读取页面内容。                                                                              | MV2, MV3     |
| declarativeNetRequest   | 通过声明式规则阻止或修改网络请求，以增强隐私保护。无需拦截请求内容即可修改网络请求。                                       | MV2, MV3     |
| desktopCapture          | 捕获屏幕、单个窗口或选项卡的内容。                                                                                        | MV2, MV3     |
| devtools.inspectedWindow| 与开发者工具的被检查窗口交互，例如获取选项卡 ID、评估代码、刷新页面或获取页面资源。                                        | MV2, MV3     |
| devtools.network        | 获取开发者工具网络工具显示的网络请求信息。                                                                                | MV2, MV3     |
| devtools.panels         | 将扩展程序集成到开发者工具窗口的 UI 中，支持创建自定义面板、访问现有面板或添加侧边栏。                                    | MV2, MV3     |
| dns                     | 解析 DNS 地址。                                                                                                          | MV2, MV3（开发通道） |
| dom                     | 访问扩展程序的特殊 DOM API。                                                                                             | MV2, MV3     |
| downloads               | 编程方式启动、监控、操作和搜索下载任务。                                                                                  | MV2, MV3     |
| enterprise.hardwarePlatform | 获取浏览器运行设备的硬件平台制造商和型号（仅适用于企业策略安装的扩展程序）。                                         | MV2, MV3     |
| events                  | 提供常见的事件类型，用于通知用户发生了某些感兴趣的事件。                                                                | MV2, MV3     |
| extension               | 提供通用工具，例如在扩展程序与内容脚本之间或扩展程序之间交换消息的支持。                                                 | MV2, MV3     |
| extensionTypes          | 为 Microsoft Edge 扩展程序声明类型。                                                                                     | MV2, MV3     |
| fontSettings            | 管理 Microsoft Edge 的字体设置。                                                                                         | MV2, MV3     |
| history                 | 操作浏览器的历史记录，包括添加、删除或查询历史记录。可通过覆盖页面功能自定义历史记录页面。                                 | MV2, MV3     |
| i18n                    | 在整个应用程序或扩展程序中实现国际化功能。                                                                                | MV2, MV3     |
| identity                | 获取 OAuth2 访问令牌。不支持 `identity.getAccounts` 和 `identity.getAuthToken`，可使用 `identity.launchWebAuthFlow` 替代。| MV2, MV3     |
| idle                    | 检测设备空闲状态的变化。                                                                                                 | MV2, MV3     |
| input.ime               | 实现自定义输入法 (IME)，允许扩展程序处理按键、设置合成内容和管理候选窗口。                                                | MV2, MV3     |
| management              | 管理已安装或正在运行的扩展程序，并可覆盖内置的新标签页。                                                                 | MV2, MV3     |
| notifications           | 使用模板创建丰富的通知，并显示在系统托盘中。                                                                              | MV2, MV3     |
| offscreen               | 创建和管理离屏文档。                                                                                                     | MV3          |
| omnibox                 | 在 Microsoft Edge 地址栏（又称为 omnibox）中注册关键字。                                                                 | MV2, MV3     |
| pageAction              | 在 Microsoft Edge 工具栏的地址栏右侧添加图标，仅对当前页面适用，不适用于所有页面。                                          | MV2          |
| pageCapture             | 将选项卡保存为 MHTML 文件。                                                                                              | MV2, MV3     |
| permissions             | 在运行时而非安装时检索声明的可选权限，可向用户展示所需权限并请求批准。                                                    | MV2, MV3     |
| power                   | 覆盖系统电源管理功能。                                                                                                   | MV2, MV3     |
| printerProvider         | 使用事件查询打印机及其功能，并提交打印任务。                                                                              | MV2, MV3     |
| privacy                 | 控制影响用户隐私的 Microsoft Edge 功能，依赖 `EdgeSetting` 原型获取和设置配置。                                           | MV2, MV3     |
| processes               | 交互浏览器的进程。                                                                                                       | MV2, MV3（开发通道） |
| proxy                   | 管理 Microsoft Edge 的代理设置，依赖 `EdgeSetting` 原型设置代理配置。                                                    | MV2, MV3     |
| runtime                 | 检索后台页面、返回清单详情，并监听应用或扩展程序生命周期中的事件。                                                        | MV2, MV3     |
| scripting               | 在不同上下文中执行脚本。                                                                                                 | MV3          |
| search                  | 使用默认提供程序进行搜索。                                                                                               | MV2, MV3     |
| sessions                | 查询和恢复浏览会话中的选项卡和窗口。                                                                                      | MV2, MV3     |
| sidePanel               | 在浏览器的侧边栏中托管自定义内容，与网页的主要内容并排显示。                                                              | MV3          |
| storage                 | 存储、检索和跟踪用户数据的变化。                                                                                          | MV2, MV3     |
| system.cpu              | 查询 CPU 元数据。                                                                                                        | MV2, MV3     |
| system.display          | 查询显示器元数据。                                                                                                       | MV2, MV3     |
| system.memory           | 报告可用内存容量和总物理内存容量。                                                                                       | MV2, MV3     |
| system.storage          | 查询存储设备信息，并接收存储设备连接或断开通知。                                                                          | MV2, MV3     |
| tabCapture              | 交互选项卡的媒体流。                                                                                                     | MV2, MV3     |
| tabGroups               | 交互浏览器的标签组系统，支持修改和重新排列标签组。                                                                        | MV3          |
| tabs                    | 创建、修改和重新排列浏览器选项卡。                                                                                        | MV2, MV3     |
| topSites                | 访问显示在新标签页上的热门网站（不包括用户自定义的快捷方式）。                                                           | MV2, MV3     |
| tts                     | 播放合成的文本转语音 (TTS)。                                                                                             | MV2, MV3     |
| ttsEngine               | 使用扩展程序实现文本转语音 (TTS) 引擎。                                                                                   | MV2, MV3     |
| types                   | 为 Microsoft Edge 声明类型。                                                                                             | MV2, MV3     |
| userScripts             | 在用户脚本上下文中执行用户脚本。                                                                                          | MV3          |
| webAuthenticationProxy  | 允许远程桌面软件拦截 Web Authentication API 请求，以便在本地客户端处理。                                                  | MV3          |
| webNavigation           | 接收导航请求的状态通知。                                                                                                 | MV2, MV3     |
| webRequest              | 观察和分析流量，拦截、阻止或修改请求。                                                                                   | MV2, MV3     |
| windows                 | 交互浏览器窗口，支持创建、修改和重新排列窗口。                                                                            | MV2, MV3     |
