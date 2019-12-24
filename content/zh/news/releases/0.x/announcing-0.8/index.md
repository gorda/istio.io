---
title: Istio 0.8 发布公告
linktitle: 0.8
subtitle: 重大更新
description: Istio 0.8 发布公告。
publishdate: 2018-06-01
release: 0.8.0
aliases:
    - /zh/about/notes/0.8
    - /zh/about/notes/0.8/index.html
    - /zh/news/2018/announcing-0.8
    - /zh/news/announcing-0.8
---

这是迈向 Istio 1.0 前的一个重要版本。除了常规的 bug 修复和性能改进之外，还包含许多新功能和体系结构改进。

{{< relnote >}}

## 网络{#networking}

- **改良的流量管理模型**。我们终于准备好完成我们的[新流量管理 API](/zh/blog/2018/v1alpha3-routing/) 的总结。 我们相信，在涵盖更多实际部署[用例](/zh/docs/tasks/traffic-management/)的同时，这种新模型更易于理解。 对于从早期发行版升级的人，这儿有一个[迁移指南](/zh/docs/setup/upgrade/)和内置在 `istioctl` 中的转换工具，可帮助您从旧模型转换配置。

- **流 Envoy 配置**。默认情况下，Pilot现在使用其 [ADS API](https://github.com/envoyproxy/data-plane-api/blob/master/xds_protocol.rst) 将配置流式传输到 Envoy。 这种新方法提高了有效的可伸缩性，减少了推出延迟，应该能消除虚假的 404 错误。

- **Gateway for Ingress/Egress**. We no longer support combining Kubernetes Ingress specs with Istio routing rules as it has led to several bugs and reliability issues. Istio now supports a platform independent [Gateway](/zh/docs/concepts/traffic-management/#gateways) model for ingress & egress proxies that works across Kubernetes and Cloud Foundry and works seamlessly with routing. The Gateway supports [Server Name Indication](https://en.wikipedia.org/wiki/Server_Name_Indication) based routing,
as well as serving a certificate based on the server name presented by the client.

- **Constrained Inbound Ports**. We now restrict the inbound ports in a pod to the ones declared by the apps running inside that pod.

## Security

- **Introducing Citadel**. We've finally given a name to our security component. What was formerly known as Istio-Auth or Istio-CA is now called Citadel.

- **Multicluster Support**. We support per-cluster Citadel in multicluster deployments such that all Citadels share the same root certificate and workloads can authenticate each other across the mesh.

- **Authentication Policy**. We've created a unified API for [authentication policy](/zh/docs/tasks/security/authentication/authn-policy/) that controls whether service-to-service communication uses mutual TLS as well as end user authentication. This is now the recommended way to control these behaviors.

## Telemetry

- **Self-Reporting**. Mixer and Pilot now produce telemetry that flows through the normal
Istio telemetry pipeline, just like services in the mesh.

## Setup

- **A la Carte Istio**. Istio has a rich set of features, however you don't need to install or consume them all together. By using
Helm or `istioctl gen-deploy`, users can install only the features they want. For example, users can install Pilot only and enjoy traffic
management functionality without dealing with Mixer or Citadel.

## Mixer adapters

- **CloudWatch**. Mixer can now report metrics to AWS CloudWatch.
[Learn more](/zh/docs/reference/config/policy-and-telemetry/adapters/cloudwatch/)

## Known issues with 0.8

- A gateway with virtual services pointing to a headless service won't work ([Issue #5005](https://github.com/istio/istio/issues/5005)).

- There is a [problem with Google Kubernetes Engine 1.10.2](https://github.com/istio/istio/issues/5723). The workaround is to use Kubernetes 1.9 or switch the node image to Ubuntu. A fix is expected in GKE 1.10.4.

- There is a known namespace issue with `istioctl experimental convert-networking-config` tool where the desired namespace may be changed to the `istio-system` namespace, please manually adjust to use the desired namespace after running the conversation tool.   [Learn more](https://github.com/istio/istio/issues/5817)
