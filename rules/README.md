# Siri AI 规则订阅

面向 Loon 的 Siri、Apple Intelligence、Private Cloud Compute 和 ChatGPT 扩展兼容规则，共 70 条。按使用者要求，保留相关 iCloud、CloudKit、Apple Account 及第三方共享依赖，不把它们仅因“与其他服务共用”而排除。

## 使用

订阅地址：

```text
https://raw.githubusercontent.com/GoldenLoaf24h/goldenloafs-loon/main/rules/SiriAI.list
```

在 `[Remote Rule]` 中**替换原 AppleIntelligence 订阅**，绑定已有的 `Siri AI` 策略组，无需重复创建策略组：

```ini
https://raw.githubusercontent.com/GoldenLoaf24h/goldenloafs-loon/main/rules/SiriAI.list, policy=Siri AI, tag=SiriAI, enabled=true
```

把这条订阅放在 Apple、iCloud、ChatGPT 和通用直连规则之前。若本地规则已有更早的 Apple/iCloud 直连或拒绝项，还需调整它们的顺序；订阅的排列无法覆盖已经命中的更早规则。

规则文件仅使用 `DOMAIN,域名` 与 `DOMAIN-SUFFIX,域名`，不带 `PROXY` 等策略列。使用 UTF-8 文本和 `#` 注释；无需 MitM、重写或脚本。本次只新增独立订阅与说明，未修改仓库原配置和插件。

## 范围与去重

- Siri/PCC 核心：Siri 请求、Search、Cloudflare/Fastly/Akamai Apple Relay 与 Apple Intelligence 扩展。
- 共享依赖：CloudKit、iCloud 内容、Private Relay、Apple DNS、账户认证，以及原清单中的定位、内容和更新服务。后者作为社区兼容项保留，不宣称全是 Apple 官方认定的 Siri 必需域名。
- ChatGPT：OpenAI、登录/验证、附件/静态资源、语音、功能开关及官方列明的支持和诊断依赖。官方 ChatGPT 通用网络清单也不等于 Siri 的每次请求都会使用所有这些域名。
- 语义去重：`apple-dns.net` 覆盖 `mask-api.fe/fe2.apple-dns.net`、`mask-t.apple-dns.net`、`apple-relay.mask.apple-dns.net` 等；`ls.apple.com` 覆盖 `gspe1-ssl.ls.apple.com`；`itunes.apple.com` 覆盖 `bag.itunes.apple.com`；`apple-cloudkit.com` 覆盖其 `api`/`cdn` 子域；`openai.com` 覆盖 `auth0.openai.com`。不重复写这些子项。
- 修正 OCR/拼写：`smoot. apple.com` → `smoot.apple.com`；`gspe1-Ss1.1s.apple.com` → `gspe1-ssl.ls.apple.com`；`authO.com` → `auth0.com`；Azure Front Door 主机使用两份维护规则共同采用的 `.z01.azurefd.net`。
- `aapps.mzstatic.com` 本次公共 DNS 查询为 NXDOMAIN，按疑似笔误移除，保留正常的 `apps.mzstatic.com`。DNS 存在与否不能单独证明某主机是 Siri 必需项。
- 未加入 `smp-device-content.apple.com`：Apple 官方用途是 ID Verifier；未加入 `ai.com`：截至整理日期，官网为独立 AI 产品，并非 OpenAI 的 Siri 扩展依赖。
- 将原 `DOMAIN-KEYWORD,siri` 改为明确的 Siri 域名，避免任意包含 `siri` 字符的无关网站命中。没有扩大到整个 Apple、iCloud、Cloudflare、Amazon 域名空间或云服务商 ASN/IP 段。

## 影响与边界

前置使用时，匹配到的 iCloud/CloudKit 同步、Apple 登录、地图定位、部分商店/更新请求、独立 ChatGPT 及第三方共享服务也会走 `Siri AI`，可能增加代理流量。这是为完整兼容保留共享依赖的结果；按域名无法区分同一服务由 Siri 还是其他 App 调用。

这是联网分流规则，不会改变设备销售地区、Apple Account 资格、系统功能开关或节点 IP 信誉，不能保证解锁。不要对 Apple Intelligence/认证流量进行 HTTPS 解密。未在 iPhone 上实际调用 Siri/ChatGPT 验收；不会因上游更新自动生成新规则，本文件由本仓库独立维护。

## 来源

整理日期：2026-11-13。

- [Apple 官方：企业网络所需主机](https://support.apple.com/en-us/101555)：Siri/PCC、iCloud、账户、内容和设备验证用途。
- [OpenAI 官方：ChatGPT 网络建议](https://help.openai.com/en/articles/9247338-network-recommendations-for-chatgpt-errors-on-web-and-apps)：共享登录、资源、支持和验证依赖。
- [Serein1202 原 AppleIntelligence 规则](https://github.com/Serein1202/ProxyHome/blob/main/Loon/Rule/AppleIntelligence/AppleIntelligence.list)：原配置使用的 21 项及兼容域名参考。
- [blackmatrix7 OpenAI 规则](https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Loon/OpenAI/OpenAI.list)：OpenAI 第三方依赖及资源主机参考。
- [MetaCubeX OpenAI 规则](https://raw.githubusercontent.com/MetaCubeX/meta-rules-dat/meta/geo/geosite/openai.list)：Azure、存储、语音等主机交叉核对。
- [ai.com 官方产品说明](https://ai.com/company-news/ai-com-launch)：确认其现为独立产品。
- 使用者提供的补充域名，已按以上资料修正和去重。
