# 🔐 Kubernetes RBAC + Autoscaling for an Apache Service

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)

Namespace-scoped **RBAC** for a team working on an Apache deployment, plus **HPA and VPA** for the same workload.

## 📦 Resources (namespace `apache`)

| File | Resource |
|---|---|
| `deployment.yml` | Apache (`httpd`) Deployment with requests/limits |
| `service.yml` | ClusterIP Service on port 80 |
| `service-account.yml` | `apache-user` ServiceAccount |
| `role.yml` | `apache-lead` Role |
| `rolebinding.yml` | Binds the role to `apache-user` |
| `hpa.yml` | CPU-based HorizontalPodAutoscaler (1 to 5 replicas) |
| `vpa.yml` | VerticalPodAutoscaler (Auto mode) |

## 🚀 Usage

```bash
kubectl create namespace apache
kubectl apply -f .

# verify permissions
kubectl auth can-i create deployments -n apache --as apache-user
kubectl auth can-i get pods -n default --as apache-user
```

## 🔒 Least privilege

The Role uses wildcards for practice. For real teams, scope it down, e.g.:

```yaml
rules:
  - apiGroups: ["", "apps"]
    resources: ["pods", "services", "deployments"]
    verbs: ["get", "list", "watch", "create", "update"]
```

---

## 👤 Author

**Abdur Rehman** · DevSecOps Engineer · Founder of [ARTechOps](https://artechops.com)

[LinkedIn](https://www.linkedin.com/in/muhamad-abdur-rehman-81777b366/) · [GitHub](https://github.com/abdur-rehman-tech) · [artechops.com](https://artechops.com)
