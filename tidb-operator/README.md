# PingCAP tidb-operator

1. Install tidb-operator
```
git clone https://github.com/pingcap/tidb-on-k8s
helm install tidb-on-k8s/tidb-operator --name mycluster
```

2. Modify tidb-operator-charts/values.yaml, set `cluster.enabled` to true, and change cluster specific values

3. Start a tidb-cluster

tidb-cluster can be created only when [TPR](https://kubernetes.io/docs/user-guide/thirdpartyresources/) is created.
```
$ kubectl get thirdpartyresource tidb-cluster.pingcap.com
NAME                       DESCRIPTION             VERSION(S)
tidb-cluster.pingcap.com   Managed tidb clusters   v1
```
then create tidb-cluster
```
helm upgrade mycluster tidb-on-k8s/tidb-operator/
```

4. Run `helm status mycluster` to view cluster status

5. Delete tidb-cluster
```
helm delete mycluster
```

To delete cluster name `mycluster` from helm, run `helm delete --purge mycluster`

*Note*: tidb-cluster would not bootstrap even when `cluster.enabled` is `true`, because TPR must be installed first. So tidb-cluster will only be created after charts be upgraded with `cluster.enabled` set to `true`
