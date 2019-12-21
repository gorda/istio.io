---
title: Istio 1.0 发布公告
linktitle: "1.0"
subtitle: service mesh 生产就绪
description: Istio 1.0 已经生产就绪。
publishdate: 2018-07-31
release: 1.0.0
aliases:
    - /zh/about/notes/1.0
    - /zh/blog/2018/announcing-1.0
    - /zh/news/2018/announcing-1.0
    - /zh/news/announcing-1.0.0
    - /zh/news/announcing-1.0
---

Today, we’re excited to announce Istio 1.0! It’s been a little over a year since our initial 0.1 release. Since then, Istio has evolved significantly with the help of a thriving and growing community of contributors and users. We’ve now reached the point where many companies have successfully adopted Istio in production and have gotten real value from the insight and control it provides over their deployments. We’ve helped large enterprises and fast-moving startups like [eBay](https://www.ebay.com/), [Auto Trader UK](https://www.autotrader.co.uk/), [Descartes Labs](http://www.descarteslabs.com/), [HP FitStation](https://www.fitstation.com/), [JUSPAY](https://juspay.in), [Namely](https://www.namely.com/), [PubNub](https://www.pubnub.com/) and [Trulia](https://www.trulia.com/) use Istio to connect, manage and secure their services from the ground up. Shipping this release as 1.0 is recognition that we’ve built a core set of functionality that our users can rely on for production use.

今天，我们激动的宣布，Istio 1.0 正式发布！自我们最初发布 0.1 版以来已经一年多了。从那时起，一个由贡献者和用户组成的蓬勃发展的社区，使得 Istio 有了长足的发展。现在，许多公司已成功将 Istio 投入生产，并从 Istio 对部署的洞察力和控制力中获得了真正的价值。我们帮助了很多大型企业和快速发展的初创企业，例如：[eBay](https://www.ebay.com/)、[Auto Trader UK](https://www.autotrader.co.uk/)、[Descartes Labs](http://www.descarteslabs.com/)、[HP FitStation](https://www.fitstation.com/)、[JUSPAY](https://juspay.in)、[Namely](https://www.namely.com/)、[PubNub](https://www.pubnub.com/) 和 [Trulia](https://www.trulia.com/) 已经使用 Istio 从头开始连接、管理和保护其服务。将此版本发布为 1.0 表示我们已经建立了一套核心功能，可供用户在生产中使用。

{{< relnote >}}

## 生态系统{#ecosystem}

去年，我们发现 Istio 的生态系统有了大幅增长。
[Envoy](https://www.envoyproxy.io/) 继续保持惊人的增长，并增加了许多对服务网格生产质量至关重要的功能。
诸如 [Datadog](https://www.datadoghq.com/)、[SolarWinds](https://www.solarwinds.com/)、[Sysdig](https://sysdig.com/blog/monitor-istio/)、[Google Stackdriver](https://cloud.google.com/stackdriver/) 和 [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) 之类的可观察性提供商已经编写了将 Istio 与他们的产品集成的插件。
[Tigera](https://www.tigera.io/resources/using-network-policy-concert-istio-2/)、[Aporeto](https://www.aporeto.com/)、[Cilium](https://cilium.io/) 和 [Styra](https://styra.com/) 为我们的策略执行和网络功能构建了扩展。
[Red Hat](https://www.redhat.com/en)  构建了 [Kiali](https://www.kiali.io)，以围绕网格管理和可观察性提供不错的用户体验。
[Cloud Foundry](https://www.cloudfoundry.org/) 基于Istio的下一代流量路由栈，
最近宣布的 [Knative](https://github.com/knative/docs) serverless 项目也在做同样的事情，并且 [Apigee](https://apigee.com/) 宣布他们计划在其 API 管理中使用它。
这些只是社区去年添加集成中的一部分。

## 特性{#features}

自 0.8 版以来，我们添加了一些重要的新功能，更重要的是将许多现有功能标记为 Beta，表明它们已可以投入生产。以下是一些要点：

- 现在可以将多个Kubernetes集群 [添加到单个网格](/zh/docs/setup/install/multicluster/) 中，并实现跨集群通信和一致的策略实施。多群集支持现在为Beta。

- Networking APIs that enable fine grained control over the flow of traffic through a mesh are now Beta. Explicitly modeling ingress and egress concerns using Gateways allows operators to [control the network topology](/zh/blog/2018/v1alpha3-routing/) and meet access security requirements at the edge.

- Mutual TLS can now be [rolled out incrementally](/zh/docs/tasks/security/authentication/mtls-migration) without requiring all clients of a service to be updated. This is a critical feature that unblocks adoption in-place by existing production deployments.

- Mixer now has support for [developing out-of-process adapters](https://github.com/istio/istio/wiki/Out-Of-Process-gRPC-Adapter-Dev-Guide). This will become the default way to extend Mixer over the coming releases and makes building adapters much simpler.

- [Authorization policies](/zh/docs/concepts/security/#authorization) which control access to services are now entirely evaluated locally in Envoy increasing
their performance and reliability.

- [Helm chart installation](/zh/docs/setup/install/helm/) is now the recommended install method offering rich customization options to adopt Istio on your terms.

- We’ve put a lot of effort into performance including continuous regression testing, large scale environment simulation and targeted fixes. We’re very happy with the results and will share more on this in detail in the coming weeks.

## What’s next?

While this is a significant milestone for the project there’s lots more to do. In working with adopters we’ve gotten a lot of great feedback about what to focus next. We’ve heard consistent themes around support for hybrid-cloud, install modularity, richer networking features and scalability for massive deployments. We’ve already taken some of this feedback into account in the 1.0 release and we’ll continue to aggressively tackle this work in the coming months.

## Getting started

If you’re new to Istio and looking to use it for your deployment we’d love to hear from you. Take a look at [our docs](/zh/docs/) or stop by our
[chat forum](https://discuss.istio.io). If you’d like
to go deeper and [contribute to the project](/zh/about/community) come to one of our community meetings and say hello.

## Thanks

The Istio team would like to give huge thanks to everyone who has made a contribution to the project. It wouldn’t be where it is today without your help. The last year has been pretty amazing and we look forward to the next one with excitement about what we can achieve together as a community.

## Release notes

### Networking

- **SNI Routing using Virtual Services**. Newly introduced `TLS` sections in
[`VirtualService`](/zh/docs/reference/config/networking/virtual-service/) can be used to route TLS traffic
based on SNI values. Service ports named as TLS/HTTPS can be used in conjunction with
virtual service TLS routes. TLS/HTTPS ports without an accompanying virtual service will be treated as opaque TCP.

- **Streaming gRPC Restored**. Istio 0.8 caused periodic termination of long running streaming gRPC connections. This has been fixed in 1.0.

- **Old (v1alpha1) Networking APIs Removed**. Support for the old `v1alpha1` traffic management model
has been removed.

- **Istio Ingress Deprecated**. The old Istio ingress is deprecated and disabled by default. We encourage users to use [gateways](/zh/docs/concepts/traffic-management/#gateways) instead.

### Policy and telemetry

- **Updated Attributes**. The set of [attributes](/zh/docs/reference/config/policy-and-telemetry/attribute-vocabulary/) used to describe the source and
destination of traffic have been completely revamped in order to be more
precise and comprehensive.

- **Policy Check Cache**. Mixer now features a large level 2 cache for policy checks, complementing the level 1 cache
present in the sidecar proxy. This further reduces the average latency of externally-enforced
policy checks.

- **Telemetry Buffering**. Mixer now buffers report calls before dispatching to adapters, which gives an opportunity for
adapters to process telemetry data in bigger chunks, reducing overall computational overhead
in Mixer and its adapters.

- **Out of Process Adapters**. Mixer now includes initial support for out-of-process adapters. This will
be the recommended approach moving forward for integrating with Mixer. Initial documentation on
how to build an out-of-process adapter is provided by the
[Out Of Process Adapter Dev Guide](https://github.com/istio/istio/wiki/Mixer-Out-Of-Process-Adapter-Dev-Guide)
and the [Out Of Process Adapter Walk-through](https://github.com/istio/istio/wiki/Mixer-Out-Of-Process-Adapter-Walkthrough).

- **Client-Side Telemetry**. It's now possible to collect telemetry from the client of an interaction,
in addition to the server-side telemetry.

#### Adapters

- **SignalFX**. There is a new `signalfx` adapter.

- **Stackdriver**. The [`stackdriver`](/zh/docs/reference/config/policy-and-telemetry/adapters/stackdriver/) adapter has been substantially enhanced in this
release to add new features and improve performance.

### Security

- **Authorization**. We've reimplemented our [authorization functionality](/zh/docs/concepts/security/#authorization).
RPC-level authorization policies can now be implemented without the need for Mixer and Mixer adapters.

- **Improved Mutual TLS Authentication Control**. It's now easier to [control mutual TLS authentication](/zh/docs/concepts/security/#authentication) between services. We provide 'PERMISSIVE' mode so that you can
[incrementally turn on mutual TLS](/zh/docs/tasks/security/authentication/mtls-migration/) for your services.
We removed service annotations and have a [unique approach to turn on mutual TLS](/zh/docs/tasks/security/authentication/authn-policy/),
coupled with client-side [destination rules](/zh/docs/concepts/traffic-management/#destination-rules).

- **JWT Authentication**. We now support [JWT authentication](/zh/docs/concepts/security/#authentication) which can
be configured using [authentication policies](/zh/docs/concepts/security/#authentication-policies).

### `istioctl`

- Added the [`istioctl authn tls-check`](/zh/docs/reference/commands/istioctl/#istioctl-authn-tls-check) command.

- Added the [`istioctl proxy-status`](/zh/docs/reference/commands/istioctl/#istioctl-proxy-status) command.

- Added the `istioctl experimental convert-ingress` command.

- Removed the `istioctl experimental convert-networking-config` command.

- Enhancements and bug fixes:

    - Align `kubeconfig` handling with `kubectl`

    - `istioctl get all` returns all types of networking and authentication configuration.

    - Added the `--all-namespaces` flag to `istioctl get` to retrieve resources across all namespaces.

### Known issues with 1.0

- Amazon's EKS service does not implement automatic sidecar injection.  Istio can be used in Amazon's
  EKS by using [manual injection](/zh/docs/setup/additional-setup/sidecar-injection/#manual-sidecar-injection) for
  sidecars and turning off galley using the [Helm parameter](/zh/docs/setup/install/helm)
  `--set galley.enabled=false`.

- In a [multicluster deployment](/zh/docs/setup/install/multicluster) the mixer-telemetry
  and mixer-policy components do not connect to the Kubernetes API endpoints of any of the remote
  clusters.  This results in a loss of telemetry fidelity as some of the metadata associated
  with workloads on remote clusters is incomplete.

- There are Kubernetes manifests available for using Citadel standalone or with Citadel health checking enabled.
  There is not a Helm implementation of these modes.  See [Issue 6922](https://github.com/istio/istio/issues/6922)
  for more details.

- Mesh expansion functionality, which lets you add raw VMs to a mesh is broken in 1.0. We're expecting to produce a
patch that fixes this problem within a few days.
