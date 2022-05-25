# Kong-KIC-examples
This repo contains examples of creating Kong configurations against Kong Ingress Controller using K8s manifests

## Set up an echo-server
#### 1. Setup an echo-server application to demonstrate how to use the Kubernetes Ingress Controller:

```
kubectl apply -f https://bit.ly/echo-service
```

## 2. Create a Basic Proxy

```
kubectl apply -f 01-ingress.yml

```

This will apply the Ingress object to the Kubernetes API which will be intercepted by the Kong Ingress Controller and applied to Kong config.

## Using plugins in Kong
### 3. Enable the rate limiting advanced plugin on a route

We first apply the KongPlugin CRD

```
kubectl apply -f 02-rate-limiting.yml

```

Then, apply it to an ingress (Route or Routes) by annotating the ingress

```
kubectl apply -f 03-ingress-plugin.yml
```

**Note:** Running the above command will apply the same ingress definition as 01-ingress.yml except that we have added the follow annotation to the ingress manifest

```
konghq.com/plugins: rate-limiting-advanced-example
```

If you login to Kong Manager and look for the route named `default.demo.00` created from step 2, you should see the rate-limited-advanced plugin appear under Plugins