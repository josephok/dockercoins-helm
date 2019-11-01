### Create 3 namespaces:
```bash
kubectl create namespace dev
kubectl create namespace uat
kubectl create namespace prod
```

### Create a single service:

#### In dev namespace:
1. Deploy worker:
```bash
helm install ./dockercoins-single-service \
--name worker \
--namespace=dev \
--set servicename=worker \
--set image.tag=0.1 \
--set service.enabled=false
```

2. Deploy hasher:
```bash
helm install ./dockercoins-single-service \
--name hasher \
--namespace=dev \
--set servicename=hasher \
--set image.tag=0.1
```

3. Deploy redis:
```bash
helm install ./dockercoins-single-service \
--name redis \
--namespace=dev \
--set servicename=redis \
--set image.tag=latest
```

4. Deploy rng:
```bash
helm install ./dockercoins-single-service \
--name rng \
--namespace=dev \
--set servicename=rng \
--set image.tag=0.1
```

5. Deploy webui:
```bash
helm install ./dockercoins-single-service \
--name webui \
--namespace=dev \
--set servicename=webui \
--set image.tag=0.1 \
--set ingress.enabled=true
```