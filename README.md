# WLOC 设置位置 - iOS 虚拟定位快捷指令

从地图 App 分享链接，一键设置虚拟定位。

## 工作原理

```
地图 App 分享链接
    ↓
快捷指令解析经纬度（调用 worker API）
    ↓
调用 gs-loc.apple.com/wloc-settings/save 存储坐标
    ↓（MITM 拦截此请求）
Shadowrocket 脚本把坐标存到本地
    ↓
弹出通知，打开定位服务设置页
    ↓
手动开关定位服务，刷新生效
```

## 使用步骤

### 1. 安装 Shadowrocket 模块

导入模块：
```
https://raw.githubusercontent.com/chengsh2024/wloc-shortcut/main/wloc.sgmodule
```

### 2. 信任证书

- Shadowrocket → 设置 → 安装证书
- iOS 设置 → 通用 → 关于本机 → 证书信任设置 → 开启信任

### 3. 添加快捷指令

点击链接添加：
```
https://www.icloud.com/shortcuts/8319af2fba8f4e46926d8cffee4fa5db
```

### 4. 使用方法

1. 打开苹果地图或高德地图
2. 找到想设置的地点，点「分享」
3. 选择「WLOC设置位置」快捷指令
4. 等待通知提示"改点成功"
5. 自动跳转到定位服务设置页
6. 手动关闭再开启定位服务，刷新生效

## 文件说明

| 文件 | 说明 |
|------|------|
| `WLOC-设置位置.shortcut` | iOS 快捷指令文件 |
| `wloc.sgmodule` | Shadowrocket 模块配置 |
| `wloc-spoofer.js` | MITM 拦截脚本 |
| `wloc-settings.js` | 坐标存储脚本 |

## 常见问题

### 定位不生效？

1. 检查 Shadowrocket 是否开启
2. 检查证书是否信任
3. 确保手动开关了定位服务
4. 检查模块是否正确导入

### 高德短链解析失败？

确认能访问外网，解析接口部署在 Cloudflare Workers 上。
