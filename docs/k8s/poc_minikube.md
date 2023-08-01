# Demo Python app using Minikube

## Simple echo container 🗳

Create a Dockerfile

```dockerfile title="Dockerfile"
FROM alpine 
CMD ["echo", "Welcome to my blog"]
```

Build image in minikube and run the pod 🚀

```bash title="Build image and run it"
minikube image build -t test . # build image to minikube directly

kubectl run test-pod --image=test --image-pull-policy=Never --restart=Never

k logs test-pod #check pod logs

# below is the output
Welcome to my blog
```

## Docker setup 🚢

### Build an image 👷🏻‍♂️

```bash
docker build -f ../pathToDockerFile/Dockerfile -t demo:latest .
```

### Run image 🏃‍♂️

```bash
# run image
docker run -p 5000:5000 demo # (1)

# get pid on a port num
lsof -i:port_num

kill -9 pid

# single liner to kill process on a certain port number
kill -9 $(lsof -t -i:5000)

# Remove all containers to unbind the port (Not recommended)
docker rm -fv $(docker ps -aq)  
```

1.  Here we are mapping the 5000 port of container to the 5000 port of host


### Remove image from registry ❌

!!! warning ""
    Before removing the image from docker registry, we need to stop and delete the container

```bash
docker ps -all            # see list of containers
docker rm CONTAINER_ID    # remove container that is running image we want to remove.

docker image ls           # list of all images
docker rmi -f IMAGE_ID    # remove the image
```


### Generic Docker commands 🖥

```bash title="Some important Docker commands 🛳"
# Build an image from a Dockerfile
docker image build	

# Show the history of an image
docker image history

# Import the contents from a tarball to create a filesystem image
docker image import	

# Display detailed information on one or more images
docker image inspect

# Load an image from a tar archive or STDIN
docker image load	

# List images
docker image ls

# Remove unused images
docker image prune	

# Pull an image or a repository from a registry
docker image pull	

# Push an image or a repository to a registry
docker image push	

# Remove one or more images
docker image rm

# Remove one or more images
docker image save	#Save one or more images to a tar archive (streamed to STDOUT by default)

# Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
docker image tag	
```

## ** Minikube setup ** ⚓️

!!! quesiton "What is Hyperkit?"
    HyperKit is an open-source hypervisor for macOS hypervisor, optimized for lightweight virtual machines and container deployment. This is the default hypervisor for Minikube in Mac.

### Start minikube

```bash
# using docker as hypervisor 
minikube start --driver=docker

# enable kubelet service, if needed
systemctl enable kubelet.service
```

### Check status 📈

` minikube status` will result in something similar as shown below

```yaml title="Output of minikube status is shown below"
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
```

Check the nodes of minikube using

```bash
kubectl get nodes # (1) 
```

1. This will show `control-plane` in case of minikube as whole setup is on local


### Lauch dashboard 🖥

This is helpful to see various resources in one place.

```bash
minikube dashboard
```
<center> <img src="../images/Kubernetes_Dashboard.png" width="100%"> </center>

### Registry options:

**Get current registry**

```sh
docker info | grep Regis
```

There are 3 options

1. Use existing docker resigtry
2. Setup a private registry
3. Directly build images on Minikube


#### 1. Docker container registry

```sh
minikube config set driver docker # set the driver

minikube config get driver        # confirm the driver status (1)
```

1. Should get `docker` as output

##### Setup registry addon 📢

```bash title="Steps to setup registry addon" 
$ minikube addons configure registry-creds # (1)

Do you want to enable AWS Elastic Container Registry? [y/n]: n

Do you want to enable Google Container Registry? [y/n]: n

Do you want to enable Docker Registry? [y/n]: y # (2)
-- Enter docker registry server url: https://index.docker.io/v1/
-- Enter docker registry username: amar
-- Enter docker registry password: 

Do you want to enable Azure Container Registry? [y/n]: n
✅  registry-creds was successfully configured
```

1.   `GCR/ECR/ACR/Docker`: minikube has an addon, registry-creds which maps credentials into minikube to support pulling from Google Container Registry (GCR), Amazon’s EC2 Container Registry (ECR), Azure Container Registry (ACR), and Private Docker registries. You will need to run minikube addons configure registry-creds and minikube addons enable registry-creds to get up and running.

2. Setup your own username and password

##### Cofigure to use Docker registry
If you want to create the `registry` on minikube's Docker then run 

```bash
eval $(minikube docker-env)
``` 

!!! info "What does this command do?"
    The command `minikube docker-env` returns a set of bash environment variable exports to configure your local environment to re-use the `Docker daemon` inside the Minikube instance.

    Passing this output through eval causes bash to evaluate these exports and put them into effect.

    You can review the specific commands which will be executed in your shell by omitting the evaluation step and running minikube docker-env directly. However, this will not perform the configuration – the output needs to be evaluated for that.

##### Enable registry addon 📌

```bash
$ minikube addons enable registry-creds
❗  registry-creds is a 3rd party addon and not maintained or verified by minikube maintainers, enable at your own risk.
    ▪ Using image upmcenterprises/registry-creds:1.10
🌟  The 'registry-creds' addon is enabled
```

check more info on https://minikube.sigs.k8s.io/docs/handbook/registry/

#### 2. Setup private registry 🗳

To make docker available on the host machine's terminal

Otherwise enter in the virtual machine via `minikube ssh`, and then proceed with the following steps

Depending on your operating system, minikube will automatically mount your homepath onto the VM.

you'll need to add the local registry as insecure in order to use http (may not apply when using localhost but does apply if using the local hostname)
Don't use http in production, make the effort for securing things up.

Use a local registry:


```bash title="Create a local resigtry" 
docker run -d -p 5000:5000 \
--restart=always \
--name local-registry registry:2
```

Now tag your image properly:

```bash title="Tag an image"
docker tag ubuntu localhost:5000/ubuntu
```

!!! note
    The localhost should be changed to dns name of the machine running registry container.

Now push your image to local registry:

```bash title="Push Image"
docker push localhost:5000/ubuntu
```
You should be able to pull it back:

```bash title="Pull Image"
docker pull localhost:5000/ubuntu
```

Now, change your `yaml file` to use the local registry.

#### 3.Building on Minikube

```bash
minikube image build -t otp-fast .
```

Confirm it using

```bash
minikube image ls
```

## Create K8S manifests: Generic

### Crate a pod

You can create a pod if needed as shown below

```bash title="create a pod manifest using dry run"
kubectl run mypod --image=docker.io/library/demo:latest \
--labels app=demo-dp \
--dry-run=client -o yaml > test_pod.yaml
```

In this example we are directly creating a deployment, so creating a pod is not required.

### Create a deployment

```bash title="Create depyloyment using declarative commands"
kubectl create deployment demo-dp \
--image=docker.io/library/demo:latest \
--replicas=1 -o yaml > dep_demo.yaml
```

### Create a service 🍻

The `service yaml` config can be

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: backend
  name: backend
spec:
  ports:
  - name: api
    protocol: TCP
    port: 10000
  selector:
    app: backend
```

### Confirm the resources

Check if service and deployment is created. You can check the endpoint using

```bash
k get ep # (1)
```

1.  Check if endpoint is created

`ssh` into pod using

```bash
 k exec -it POD_ID -- /bin/sh
 ```

Now check the servcie status using

```bash
$ k exec -it POD_ID -- /bin/sh

printenv | grep SERVICE # run this command after doing `exec -it`
```

```yaml  title="Sample output of printenv 📝"
KUBERNETES_SERVICE_PORT=443
HELLO_PYTHON_SERVICE_PORT_6000_TCP_ADDR=10.109.182.67
HELLO_PYTHON_SERVICE_PORT_6000_TCP_PORT=6000
HELLO_PYTHON_SERVICE_PORT_6000_TCP_PROTO=tcp
DEMO_SERVICE_PORT_6000_TCP_ADDR=10.103.151.245
DEMO_SERVICE_PORT_6000_TCP_PORT=6000
DEMO_SERVICE_PORT_6000_TCP_PROTO=tcp
HELLO_PYTHON_SERVICE_SERVICE_HOST=10.109.182.67
HELLO_PYTHON_SERVICE_PORT_6000_TCP=tcp://10.109.182.67:6000
DEMO_SERVICE_SERVICE_HOST=10.103.151.245
HELLO_PYTHON_SERVICE_PORT=tcp://10.109.182.67:6000
HELLO_PYTHON_SERVICE_SERVICE_PORT=6000
DEMO_SERVICE_PORT_6000_TCP=tcp://10.103.151.245:6000
KUBERNETES_SERVICE_PORT_HTTPS=443
DEMO_SERVICE_PORT=tcp://10.103.151.245:6000
DEMO_SERVICE_SERVICE_PORT=6000
KUBERNETES_SERVICE_HOST=10.96.0.1
```

## POC example using Fast API

Below are the steps to create a sample POC

### Install FastAPI on local 

Install fastapi using

```sh
$ python -m pip install fastapi uvicorn[standard]
```

Run server on local using

```bash
$ uvicorn demo_main:app --reload
```

Get access to swagger docs using

```yaml
http://127.0.0.1:8000/docs
```

Create the FastAPI Code

- Create an app directory and enter it.
- Create an empty file __init__.py.
- Create a main.py file with below code

```py title="FastAPI sample code 👨🏻‍💻"
from typing import Union

from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return {"Hello": "World"}


@app.get("/items/{item_id}")
def read_item(item_id: int, q: Union[str, None] = None):
    return {"item_id": item_id, "q": q}
```


!!! abstract "Why we need __init__.py?"
    Files named `__init__.py` are used to mark directories on disk as Python package directories. If you have the files

    ```py
    mydir/spam/__init__.py
    mydir/spam/module.py
    ```
    and `mydir` is on your path, you can import the code in `module.py` as

    ```
    import spam.module
    ```
    
    or

    ```
    from spam import module
    ```

    If you remove the `__init__.py` file, Python will no longer look for submodules inside that directory, so attempts to import the module will fail.

    The  `__init__.py` file is usually empty, but can be used to export selected portions of the package under more convenient name, hold convenience functions, etc. Given the example above, the contents of the init module can be accessed as

    `import spam`


### Requirements file
An `requirements.txt` is shown below 

```properties 
fastapi
pydantic
uvicorn
```

### Create a DockerFile

Now in the same project directory create a file Dockerfile with:

```dockerfile title="Dockerfile for FastAPI 🚀" 
FROM python:3.9
 
WORKDIR /code

COPY ./requirements.txt /code/requirements.txt
 
RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt
 
COPY ./app /code/app
 
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]
```

You should now have a directory structure like:

```bash 
.
├── app
│   ├── __init__.py
│   └── main.py
├── Dockerfile
└── requirements.txt

```

### Create image on Minikube

Create a image using the sample code 
   
```bash
minikube image build -t otp-fast .
```

### Create k8s manifests for POC

1. Using Kubectl
2. Using Python

#### Using Kubectl

Given the fact that we have 2 files

1. create_deployment.yaml
2. create_servcie.yaml

we can create a deployment using the following

```bash
kubectl apply -f create_service
kubectl apply -f create_deployment
```

#### Using Python 

Install the required package

```bash
pip install kubernetes
```

Confirm the installation using

```bash
$ pip list | grep kuber
kubernetes                 24.2.0
```

Imagine that we have below service and deployment code

```yaml title="create_service.yaml"
apiVersion: v1
kind: Service
metadata:
  name: demo-service-api
spec:
  selector:
    app: demo-api
  ports:
  - protocol: "TCP"
    port: 80
    targetPort: 80
  type: LoadBalancer
```

A sample deployment manifest

```yaml title="create_deployment.yaml"
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-deploy-api
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo-api
  template:
    metadata:
      labels:
        app: demo-api
    spec:
      containers:
      - name: demo-api
        image: fast
        imagePullPolicy: Never
        ports:
        - containerPort: 80
```

code to create manifests using Python K8S API

```py title="createApplication.py"
from os import path
import yaml
from kubernetes import client, config
from kubernetes.client import V1DeleteOptions

def main():
    # Configs can be set in Configuration class directly or using helper
    # utility. If no argument provided, the config will be loaded from
    # default location.
    config.load_kube_config()
    k8s_apps_v1 = client.AppsV1Api()
    core_v1_api = client.CoreV1Api()

    create_service(core_v1_api)
    create_deployment(k8s_apps_v1)

    del_opts = V1DeleteOptions()
    api_client = get_custom_objects_api_client()
   
def create_deployment(k8s_apps_v1):
    with open(path.join(path.dirname(__file__), "demo_deployment.yaml")) as f:
        dep = yaml.safe_load(f)
        resp = k8s_apps_v1.create_namespaced_deployment(body=dep, namespace="default")
        print("Deployment created. status='%s'" % resp.metadata.name)
        

def create_service(core_v1_api):
    with open(path.join(path.dirname(__file__), "demo_service.yaml")) as f:        
        service = yaml.safe_load(f)
        resp = core_v1_api.create_namespaced_service(body=service, namespace="default")
        resp = core_v1_api.delete
        print("Service status='%s'" % resp.metadata.name)
        
if __name__ == '__main__':
    main()
```

Create the resources using

```py
python createApplication.py
```

