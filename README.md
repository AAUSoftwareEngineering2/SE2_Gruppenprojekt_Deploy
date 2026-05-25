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

## Headlamp

Headlamp ist das Kubernetes-Web-Dashboard für den K3s-Cluster. Es wird über
Flux als HelmRelease aus `clusters/kuhhandel-k3s/infrastructure/headlamp`
installiert.

```text
Browser
  -> Cloudflare Access
  -> eigener Headlamp-Cloudflare-Tunnel
  -> headlamp.headlamp.svc.cluster.local:80
  -> Headlamp
```

Vor dem fertigen Betrieb braucht der Headlamp-Tunnel ein eigenes Secret im
Cluster:

```bash
kubectl -n cloudflare-headlamp create secret generic cloudflared-token \
  --from-literal=token='DEIN_HEADLAMP_TUNNEL_TOKEN'
```

Danach muss in Cloudflare am neuen Tunnel eine Public-Hostname-Route angelegt
werden:

```text
Hostname:      headlamp.se-aau.com
Service Type:  HTTP
Service URL:   headlamp.headlamp.svc.cluster.local:80
```

Der Login in Headlamp erfolgt mit einem live erzeugten Kubernetes-Token:

```bash
kubectl -n headlamp create token headlamp-viewer --duration=24h
```
