# Kuhhandel Deploy

Dieses Repo enthält nur den Flux-/GitOps-Teil für den K3s-Cluster.

Der Anwendungscode und die Kubernetes-Templates bleiben im normalen Repo:

```text
AAUSoftwareEngineering2/SE2_Gruppenprojekt
  deploy/k8s/
```

Dieses Repo sagt Flux:

```text
Lies die Templates aus dem App-Repo.
Setze für Production oder Staging den passenden Image-Tag.
Halte den K3s-Cluster auf diesem Stand.
```

Echte Secrets gehören nicht in dieses Repo.
