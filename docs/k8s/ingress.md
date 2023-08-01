# Ingress

## Ingress Fanout


```yaml title="Fanout Ingress Example"
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: simple-fanout-example
spec:
  rules:
  - host: ammarjitdhillon.com
    http:
      paths:
      - path: /sa
        pathType: Prefix
        backend:
          service:
            name: serviceA
            port:
              number: 4200
      - path: /sb
        pathType: Prefix
        backend:
          service:
            name: serviceB
            port:
              number: 8080
```
