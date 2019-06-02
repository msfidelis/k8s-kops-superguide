

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
    --node-count 3 \
    --zones us-east-1a,us-east-1b,us-east-1c \
    --networking weave \
    --name cluster.raj.ninja \
    --cloud aws \
    --state s3://raj-teste-muito-louco \
    --yes
```