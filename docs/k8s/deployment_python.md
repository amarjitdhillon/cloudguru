# Create K8S deployment via Python

Install the K8S client using

```sh
$ pip install kubernetes
```

Create 2 files

- `create-deployment.py`
- `k8s-deployment.yaml`


## Python file code

```py title="create-deployment.py"
from os import path
import yaml
from kubernetes import client, config

def main():
    # Configs can be set in Configuration class directly or using helper
    # utility. If no argument provided, the config will be loaded from
    # default location.
    config.load_kube_config()

    with open(path.join(path.dirname(__file__), "k8s-deployment.yaml")) as f:
        dep = yaml.safe_load(f)
        k8s_apps_v1 = client.AppsV1Api()
        resp = k8s_apps_v1.create_namespaced_deployment(
            body=dep, namespace="default")
        print("Deployment created. status='%s'" % resp.metadata.name)

if __name__ == '__main__':
    main()
```


## Deployment file

```yaml title='k8s-deployment.yaml'
apiVersion: apps/v1
kind: Deployment
metadata:
  name: k8s-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.15.4
        ports:
        - containerPort: 80
```

## Creating deployment

```py
python3 create-deployment.py
```