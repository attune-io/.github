# Attune

Kubernetes operator for **in-place pod resource right-sizing**. Attune continuously monitors your workloads via Prometheus, computes optimal CPU and memory requests, and applies them without restarts using the [In-Place Pod Resize](https://kubernetes.io/blog/2023/05/12/scalable-pod-startup/) API (Kubernetes 1.32+).

A smarter alternative to the Vertical Pod Autoscaler (VPA).

## Key Features

- **Zero-downtime resizing** via the `/resize` subresource (no pod restarts)
- **Composable recommendation engine** with percentile estimation, confidence scaling, safety margins, and change filters
- **HPA-aware** conflict detection prevents fights between horizontal and vertical scaling
- **Safety monitor** with automatic rollback on OOM kills
- **Multi-source metrics** from Prometheus, Datadog, or CloudWatch
- **Helm chart** with cert-manager webhook support
- **kubectl plugin** for dry-run recommendations

## Get Started

- [Documentation](https://attune-io.github.io/attune/)
- [GitHub Repository](https://github.com/attune-io/attune)
- [Installation Guide](https://attune-io.github.io/attune/getting-started/)
