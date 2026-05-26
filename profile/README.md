<p align="center">
  <img src="https://raw.githubusercontent.com/attune-io/attune/main/docs/logo.png" alt="Attune" width="120">
</p>

<h3 align="center">Safe, in-place Kubernetes pod resource right-sizing</h3>

<p align="center">
  <a href="https://github.com/attune-io/attune/actions/workflows/ci.yaml"><img src="https://github.com/attune-io/attune/actions/workflows/ci.yaml/badge.svg" alt="CI"></a>
  <a href="https://github.com/attune-io/attune"><img src="https://img.shields.io/badge/go-1.26-blue" alt="Go 1.26"></a>
  <a href="https://github.com/attune-io/attune/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-Apache%202.0-blue" alt="Apache 2.0"></a>
</p>

---

Attune is a Kubernetes operator that right-sizes pod CPU and memory
without restarts, using [In-Place Pod Resize](https://kubernetes.io/blog/2025/12/19/kubernetes-v1-35-in-place-pod-resize-ga/)
(Kubernetes 1.33+ beta, 1.32 alpha). It replaces the Vertical Pod Autoscaler
with something that actually works in production.

## Why not VPA?

| | VPA | Attune |
|---|---|---|
| Resize method | Evicts pods | In-place (no restarts) |
| HPA compatible | No (death spirals) | Yes (adjusts base, not %) |
| Safety | Minimal guardrails | Auto-revert on OOM, throttle, restarts |
| Confidence | Backward-looking histograms | Time-of-day-aware + graduated rollout |

## Features

- Zero-downtime resizing via the `/resize` subresource
- Composable recommendation engine with percentile, confidence, margins, and change filters
- HPA-aware conflict detection prevents horizontal/vertical scaling fights
- Safety monitor with automatic rollback on OOM kills, CPU throttle, or restart spikes
- Graduated rollout: Observe, Recommend, OneShot, Canary, Auto
- Multi-source metrics from Prometheus, Thanos, VictoriaMetrics, and Grafana Mimir
- Cost savings estimation per workload with `kubectl attune savings`
- Helm chart with cert-manager webhook support and Grafana dashboard

## Quick Start

```bash
helm install attune oci://ghcr.io/attune-io/charts/attune \
  --namespace attune-system --create-namespace
```

## Learn More

- [Documentation](https://attune-io.github.io/attune/) -- full guides, API reference, and examples
- [GitHub Repository](https://github.com/attune-io/attune) -- source, issues, and contributing
- [Migrating from VPA](https://attune-io.github.io/attune/guides/migrating-from-vpa/) -- step-by-step replacement guide
