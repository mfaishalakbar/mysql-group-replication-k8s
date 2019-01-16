# MySQL 8.0 With Group Replication Support
For Kubernates / k8s / you name it.

## How to Use
```
# Make Service
kubectl create -t mysql-group-replication-master.service.yml
kubectl create -t mysql-group-replication-scalable-master.service.yml

# Make Instance
kubectl create -t mysql-group-replication-master.rc.yml
kubectl create -t mysql-group-replication-scalable-master.rc.yml

# Scale Up? OK...
kubectl scale -f mysql-group-replication-scalable-master.rc.yml --replicas=4
```

## Startup commands
### Master
```
SET GLOBAL group_replication_bootstrap_group=ON;
START GROUP_REPLICATION;
SET GLOBAL group_replication_bootstrap_group=OFF;
```
### Scalable Master (First Time)
```
reset master;
START GROUP_REPLICATION;
```
### Scalable Master (Next)
```
START GROUP_REPLICATION;
```