# quickstart 24.10 local rules

- `首页` 标题和中文兜底属于预期补丁，不要回退成 `QuickStart / NetworkGuide`。
- `istore_backend.lua` 中的本地状态接口兜底优先保留。
- 若后续补 `/system/module-settings/`、`taskd/xterm` 等问题，优先在 quickstart/iStore 对应仓库中按职责拆分，不要把无关逻辑塞进一个文件。
