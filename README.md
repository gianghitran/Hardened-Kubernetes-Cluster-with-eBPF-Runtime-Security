# Hardened-Kubernetes-Cluster-with-eBPF-Runtime-Security
Deployed a 3-node RKE2 cluster secured with Falco eBPF runtime IDS and Cilium eBPF networking, achieving kernel-level threat visibility with zero overlay overhead.


> Tech Stack: Kubernetes (RKE2), Cilium & Hubble (eBPF CNI / observability), Falco (eBPF runtime IDS), Falcosidekick, ELK Stack (Elasticsearch, Logstash, Kibana), Helm, Docker, Linux Kernel/BTF, Bash, MITRE ATT&CK

### Implementation:

- Architected and deployed a 3-node RKE2 Kubernetes cluster secured with Cilium eBPF native routing (no VXLAN encapsulation) and kube-proxy replacement, delivering kernel-level network visibility with zero overlay overhead.
- Engineered and validated 7 end-to-end attack use cases mapped to MITRE ATT&CK (webshell upload, web-shell command execution, reverse shell, privilege escalation, sensitive-file/credential access, and lateral movement), with each technique detected within seconds of execution.
- Authored custom Falco eBPF detection rules enriched with Kubernetes pod metadata, cutting false positives by whitelisting trusted container-runtime processes while flagging anomalous root and reverse-shell activity.
- Enforced Cilium Network Policies (default-deny egress) that blocked outbound C2 / reverse-shell connections on ports 4444/443/80 at the kernel level, containing compromised pods even after successful webshell upload.
- Built a centralized detection pipeline (Falco → Falcosidekick → Logstash → Elasticsearch → Kibana), streaming runtime alerts and Hubble network flows into searchable dashboards for real-time incident investigation and forensics.



<img width="850" height="770" alt="image" src="https://github.com/user-attachments/assets/1a40cfd4-5ed4-4a2f-a52a-d1df96e9a99f" />
