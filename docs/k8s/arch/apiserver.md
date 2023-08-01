# API Server

Main uses are
- Authenticate a user
- Validate a request
- Retrive data
- Update ETCD (only component to do that): The list of ETCD servers is updated in the API server
- Communicate with Scheduler
- Commnunicate with Kubelet

## View API sever options

```bash
cat /etc/systemd/system/kube-apisever.service
```


See the process

```bash
ps aux | grep kube-apiservice 
```

