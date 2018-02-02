## Istio Setup

These notes are for information and are not necessarily designed to be shown in the demo. This should be setup ahead of presentation start.

1. Start Minikube

```bash
make minikube
```

2. Download latest istio release

```bash
make download
```

3. Deploy Istio control plane

```bash
make setup
```

4. Confirm control plane setup was successful (CTRL-C to stop watch)

```bash
make watch
```

5. Create Istio sidecar injector certificates

```bash
make create-cert
```

6. Confirm certificate creation was successful

```bash
make check-cert
```

7. Deploy istio-inject configmap 

```bash
make deploy-configmap
```

8. Confirm configmap creation was successful
```bash
make check-configmap
```

9. Create Istio sidecar CA bundle

```bash
make create-cabundle 
```

10. Deploy sidecar injector

```bash
make deploy-injector 
```

11. Check sidecar injector was deployed successfully

```bash
make check-injector 
```

12. Label default namespace to enable sidecar injection

```bash
make label-default 
```

13. Confirm injecion is working with sleep sample

```bash
make deploy sleep 
```
