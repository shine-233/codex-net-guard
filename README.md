# codex-net-guard

> 重造 network-proxy 的 80% 能力，填补 dsh 网络管控缺口。

## 吸收来源
- 概念来源 network-proxy (16,834) —— 不搬源码，纯 JS 重造

## 功能边界
**做**：本地 HTTP/SOCKS 白名单代理（消费 policy-engine 域名规则）；自签 CA 方案 HTTPS 审计。

**不做**：放弃 Windows TCP 归因（内核活）；不做全量 MITM 解密（默认只看 SNI）。

## API 草图
```
startProxy(rules): ProxyHandle
```

## 验收标准
白名单外域名 100% 拦截；白名单内请求延迟增量 <5ms。

## 上游同步
基于 openai/codex@970b7f2ff4f6（Apache-2.0）。季度 diff 由 dsh-codex-ledger CI 触发，见 ledger/coverage.yaml 对应行。

## M5 状态（v0 已实建）
- ✅ 白名单代理：absolute-form 转发 + CONNECT 隧道拦截 + 域名后缀匹配
- ✅ 可注入 resolve（测试用本地上游）
- ⏳ TODO：HTTPS 审计（自签 CA）、token 预算联动 policy-engine 规则文件
