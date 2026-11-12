# GoldenLoaf's Loon

GoldenLoaf 的 Loon 配置与自定义策略组图标。

## 文件

- [`Astra-Loon.lcf`](Astra-Loon.lcf)：公开、脱敏版 Loon 配置。
- [`icons/`](icons/)：Loon 策略组自定义图标。

## 使用

1. 下载或复制 `Astra-Loon.lcf`。
2. 在 `[Remote Proxy]` 段填入自己的机场订阅。
3. 导入 Loon 后，建议设置：
   - 运行模式：`RULE`
   - DoH 流量模式：`RULE`
   - DNS 查询回落：关闭

公开配置已删除真实机场订阅、机场专用解析域名和个人 MitM 证书。导入后仅保留规则、策略组和插件结构，因此需要自行添加订阅才能获得节点。

## 图标集合

图标统一按常见 Loon/Qure 资源规格整理为 `144×144` RGBA PNG。
仓库中的 `Astra-Loon.lcf` 已将 `Siri AI` 策略组直接绑定到 `siri.png`。

在 Loon 的“策略 → 图标集合 → 添加”中，应导入 JSON 索引，而不是单张 PNG：

```text
https://raw.githubusercontent.com/GoldenLoaf24h/goldenloafs-loon/main/icons/iconset.json
```

GitHub Raw 较慢时可以使用 jsDelivr：

```text
https://cdn.jsdelivr.net/gh/GoldenLoaf24h/goldenloafs-loon@main/icons/iconset.json
```

如果只给某个策略组设置图标，则在策略组配置中使用单张 PNG：

```text
img-url = https://cdn.jsdelivr.net/gh/GoldenLoaf24h/goldenloafs-loon@main/icons/siri.png
```

每个图标的具体说明见 [`icons/README.md`](icons/README.md)。
