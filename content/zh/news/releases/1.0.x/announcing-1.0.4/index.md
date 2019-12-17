---
title: Istio 1.0.4 发布公告
linktitle: 1.0.4
subtitle: 补丁发布
description: Istio 1.0.4 补丁发布。
publishdate: 2018-11-21
release: 1.0.4
aliases:
    - /zh/about/notes/1.0.4
    - /zh/blog/2018/announcing-1.0.4
    - /zh/news/2018/announcing-1.0.4
    - /zh/news/announcing-1.0.4
---

我们荣幸的宣布 Istio 1.0.4 现已正式发布。请查看下面的内容获取更新详情。

{{< relnote >}}

## 已知问题{#known-issues}

- 使用 [`istioctl proxy-status`](/zh/docs/reference/commands/istioctl/#istioctl-proxy-status) 来获取代理同步状态时，可能会导致 Pilot 死锁。
  临时的解决方法是不使用 `istioctl proxy-status`。
  一旦 Pilot 进入死锁状态，它将表现出持续的内存增长，最终耗尽内存。

## 网络{#networking}

- 修复了缺少 removal 导致 503 错误的远古 endpoint 问题。

- 修复了 Pod 标签包含 `/` 时 sidecar 的注入问题。

## 策略和遥测{#policy-and-telemetry}

- 修复了进程外 Mixer 适配器造成的不正确行为，偶尔导致数据损坏的问题。

- 修复了在等待失踪的 CRD 时，Mixer 过度使用 CPU 的问题。
