# Kubernetes taint-toleration example

```ruby
kubectl taint nodes labk8sworker key=green:NoSchedule
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx
spec:
  selector:
    matchLabels:
      run: my-nginx
  replicas: 2
  template:
    metadata:
      labels:
        run: my-nginx
    spec:
      containers:
      - name: my-nginx
        image: nginx
        ports:
        - containerPort: 80
      tolerations:
      - key: "nginx"
        operator: "Equal"
        value: "green"
        effect: "NoExecute"
```