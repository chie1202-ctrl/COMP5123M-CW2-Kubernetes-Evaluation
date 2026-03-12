# GenAI Troubleshooting Log - COMP5123M CW2

This log documents the assistive role of GenAI (Microsoft Copilot/ChatGPT) in troubleshooting system faults and optimizing the experimental design for the performance evaluation of Kubernetes distributions.

| Problem Encountered | AI Proposed Solution | Worked? | Technical Opinion |
| :--- | :--- | :--- | :--- |
| **Hypervisor Compatibility:** VMware Fusion failed to boot Ubuntu ARM64 ISO on Mac M4, stalling at the EFI stub. | Switch to **UTM** and enable the **Apple Virtualization framework**. | **Yes** | UTM provides superior hardware-assisted virtualization for Apple Silicon; this move was essential for system stability. |
| **Networking Isolation:** Kind's containerized node architecture made the NodePort service unreachable from the host browser. | Use `kubectl port-forward` with the `--address 0.0.0.0` flag to bridge traffic. | **Yes** | Successfully bypassed Docker's network isolation, although it introduced a significant proxy-level throughput bottleneck. |
| **Abnormal Performance Gap:** Initial tests showed a 450x performance difference, which seemed unrealistic for core K8s stacks. | Perform localized testing using the **Kind Node's Internal IP** to bypass the port-forward proxy. | **Yes** | Root-cause analysis correctly identified the proxy as the bottleneck, ensuring a fair "core-to-core" comparison. |
| **Inaccurate Resource Data:** AI suggested a default peak CPU usage of ~85% which conflicted with real-time observations. | Manually monitor **`htop`** during peak load and record empirical data (~22%). | **Yes** | The AI overestimated resource strain on M4 hardware. Empirical observation was critical to ensuring the integrity of the report. |

### Technical Reflection on GenAI Effectiveness
GenAI was highly effective for rapid root-cause analysis of networking layers. However, **human intervention was critical** when interpreting performance data. The decision to override AI-suggested metrics with empirical observations from `htop` ensured that the final results were scientifically accurate and representative of the high-performance Mac M4 environment.
