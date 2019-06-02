

ssh-keygen -t rsa -b 4096


## Create a cluster especification

```bash
kops create cluster \
    --node-count 3 \
    --zones us-east-1a,us-east-1b,us-east-1c \
    --networking weave \
    --name cluster.raj.ninja \
    --cloud aws \
    --state s3://raj-teste-muito-louco
```

* `node-count` :
* `zones` :
* `networking` :
* `name` :
* `cloud` :
* `state` :


## Apply Cluster Specs

```bash
kops update cluster \
    --name cluster.raj.ninja \
    --state s3://raj-teste-muito-louco \
    --yes
```


## Validate Cluster

```bash
kops validate cluster cluster.raj.ninja \
    --state s3://raj-teste-muito-louco
```

## How to Connect on Master

by default, the master and nodes uses a Debian. The default user on VM's is `admin`

```bash
ssh admin@ip-do-master
```


```bash
kubectl get nodes
```

```
NAME                            STATUS   ROLES    AGE     VERSION
ip-172-20-51-235.ec2.internal   Ready    master   7m30s   v1.12.7
ip-172-20-61-17.ec2.internal    Ready    node     5m59s   v1.12.7
ip-172-20-79-42.ec2.internal    Ready    node     6m1s    v1.12.7
ip-172-20-97-13.ec2.internal    Ready    node     5m22s   v1.12.7
```


### Default Public Key

```bash
kops create secret \
    --name cluster.raj.ninja \
    sshpublickey admin \
    -i ~/.ssh/id_rsa.pub \
    --state s3://raj-teste-muito-louco
```

## Delete Cluster

```bash
kops delete cluster \
    cluster.raj.ninja \
    --state s3://raj-teste-muito-louco \
    --yes
```
------

## Another Options

```bash
kops create cluster \
    --master-size m4.large \
    --node-size c4.large \
    --api-loadbalancer-type public \
    --master-count 3 \
    --node-count 3 \
    --zones us-east-1a,us-east-1b,us-east-1c \
    --networking weave \
    --name cluster.raj.ninja \
    --cloud aws \
    --state s3://raj-teste-muito-louco \
    --yes
```

* `master-size` :
* `node-size` :
* `api-loadbalancer-type` :
* `master-count` :
* `node-count` :