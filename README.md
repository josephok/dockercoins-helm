### Create 3 namespaces:
```bash
kubectl create namespace dev
kubectl create namespace uat
kubectl create namespace prod
```

### Create a single service in `dev` and `uat` namespace:

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

#### In uat namespace:
1. Deploy worker:
```bash
helm install ./dockercoins-single-service \
--name worker-uat \
--namespace=uat \
--set servicename=worker \
--set image.tag=0.1 \
--set service.enabled=false \
--set healthcheck.enabled=true
```

2. Deploy hasher:
```bash
helm install ./dockercoins-single-service \
--name hasher-uat \
--namespace=uat \
--set servicename=hasher \
--set image.tag=0.1 \
--set healthcheck.enabled=true
```

3. Deploy redis:
```bash
helm install ./dockercoins-single-service \
--name redis-uat \
--namespace=uat \
--set servicename=redis \
--set image.tag=latest \
--set healthcheck.enabled=true
```

4. Deploy rng:
```bash
helm install ./dockercoins-single-service \
--name rng-uat \
--namespace=uat \
--set servicename=rng \
--set image.tag=0.1 \
--set healthcheck.enabled=true
```

5. Deploy webui:
```bash
helm install ./dockercoins-single-service \
--name webui-uat \
--namespace=uat \
--set servicename=webui \
--set image.tag=0.1 \
--set ingress.enabled=true \
--set healthcheck.enabled=true
```

### Create all services in `prod` namespace:
1. Deploy redis in master node:

```bash
apt get install redis
```
And change bind address to your public interface ip, mine is `192.168.56.6`

2. Deploy services in `prod` namespace:

```bash
helm install ./dockercoins-all-service \
--name dockercoins \
--namespace=prod
```