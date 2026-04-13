# quickstart 24.10 local rules

- `首页` 标题和中文兜底属于预期补丁，不要回退成 `QuickStart / NetworkGuide`。
- `istore_backend.lua` 中的本地状态接口兜底优先保留。
- 温度显示修复必须落在后端接口层：
  - `/cgi-bin/luci/istore/system/status/`
  - `/cgi-bin/luci/istore/system/cpu/temperature/`
  这两条接口都要能返回 `cpuTemperature`，后续不要改回只在前端补字。
- `module-settings` 空配置时，`diableDisplay` 必须序列化为 `[]` 而不是 `{}`；这是 QuickStart 首页模块设置弹窗能否正常工作的前提。
- 涉及温度/状态显示的修复后，优先 bump `luci-app-quickstart` 包版本，确保 Actions 产出的 `ipk` 明确带上修复。
- `quickstart/home.htm` 必须继续渲染完整前端主页；不要再把它改成只有“欢迎使用 Quickstart / 网络向导 / 无线设置 / 系统状态”的简化页。
- 若后续补 `/system/module-settings/`、`taskd/xterm` 等问题，优先在 quickstart/iStore 对应仓库中按职责拆分，不要把无关逻辑塞进一个文件。
