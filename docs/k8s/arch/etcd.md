# ETCD

- It is a distributed key-value store
- Uses RAFT consensus protocol
- Only once change is written to ETCD, the change is considered as complete
- ETCD runs in an HA environment and in this case the service should be configured so that various ETCD servers knows about one another


The API version used by etcdctl to speak to etcd may be set to version 2 or 3 via the ETCDCTL_API environment variable. By default, etcdctl on master (3.4) uses the v3 API and earlier versions (3.3 and earlier) default to the v2 API.


```bash title="set version"
export ETCDCTL_API=3
```

!!! warning
    When API version is not set, it is assumed to be set to version 2. And version 3 commands listed above don't work. When API version is set to version 3, version 2 commands listed above don't work.


## Write key

Applications store keys into the etcd cluster by writing to keys. Every stored key is replicated to all etcd cluster members through the Raft protocol to achieve consistency and reliability.

```bash title="set key"
$ ./etcdctl.exe put name amar
OK
```

## Get the key

```bash title="get key"
$ ./etcdctl.exe get name
name
amar
```

## get keys in k8s

```bash
k exec etcd-master -n kube-system etcdctl get / --prefix --keys-only 
```

