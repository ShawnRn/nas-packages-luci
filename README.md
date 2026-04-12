# nas-packages-luci

这个 fork 主要用来承载 `ImmortalWrt/OpenWrt 24.10` 兼容补丁，当前重点放在 `luci-app-quickstart`：

- 菜单标题固定为中文 `首页`
- 移除 `NetworkGuide` 入口
- 前端语言缺省回退到 `zh-cn`
- `/cgi-bin/luci/istore/system/status/` 提供本地兜底
- `istore_backend.lua` 优先转发到 `/var/run/quickstart/local.sock`，兼容当前 quickstart 服务

## 包构建

仓库内提供 GitHub Actions，可按 OpenWrt `24.10.0` SDK 为多个目标架构构建 `luci-app-quickstart` 的 `ipk` 工件。

## 说明

这个仓库只保存 `LuCI` 与 `quickstart/iStore` 兼容层补丁，不包含 `luci-theme-design` 相关改动。
luci for [nas-packages](https://github.com/linkease/nas-packages)

## 使用方法

### 增加feed源

```shell
echo >> feeds.conf.default
echo 'src-git nas https://github.com/linkease/nas-packages.git;master' >> feeds.conf.default
echo 'src-git nas_luci https://github.com/linkease/nas-packages-luci.git;main' >> feeds.conf.default
./scripts/feeds update nas nas_luci
./scripts/feeds install -a -p nas
./scripts/feeds install -a -p nas_luci
```

### 集成软件包

```shell
make menuconfig
```

选择软件包
```plain
LuCI --->
3. Applications --->
<*> luci-app-ddnsto.................................. LuCI support for ddnsto
<*> luci-app-linkease.................................. LuCI support for linkease
```

### 构建固件
```shell
make
```
