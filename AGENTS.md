# nas-packages-luci (AGENTS.md)

## 项目目标
这个仓库保存 `quickstart` 相关补丁，目标是让 `luci-app-quickstart` 在当前 ImmortalWrt/OpenWrt `24.10` 环境里至少具备：

- 稳定的中文入口标题（`首页`）
- 不再默认暴露 `NetworkGuide`
- Vue 资源语言有明确兜底
- `quickstart` 首页能读取 CPU/温度/内存状态

## 关键文件
- `luci/luci-app-quickstart/luasrc/controller/quickstart.lua`
- `luci/luci-app-quickstart/luasrc/controller/istore_backend.lua`
- `luci/luci-app-quickstart/luasrc/view/quickstart/main.htm`
- `luci/luci-app-quickstart/root/usr/share/luci/menu.d/luci-app-quickstart.json`

## 当前补丁原则
- 前端语言优先按 LuCI 传入 `lang` 加载，缺省回退 `zh-cn`。
- 系统信息接口优先在 `istore_backend.lua` 本地生成兜底结果，不依赖外部后端一定在线。
- 转发到 quickstart 后端时，优先使用 Unix socket `/var/run/quickstart/local.sock`，必要时才回退到 `127.0.0.1:3038`。
- 不要在这个仓库里混入 `luci-theme-design` 相关修复。

## 路由器验证
- 菜单应显示为 `首页`
- `/cgi-bin/luci/istore/system/status/` 应返回：
  - `code`
  - `result.cpuUsage`
  - `result.cpuTemperature`
  - `result.memAvailablePercentage`
- `/cgi-bin/luci/istore/system/cpu/temperature/` 应返回：
  - `result.temperature`
  - `result.cpuTemperature`
