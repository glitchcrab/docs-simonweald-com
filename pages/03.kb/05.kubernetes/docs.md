---
title: kubernetes
date: '15:06 19-08-2021'
taxonomy:
    category:
        - docs
---

### misc
* get all pods on a node:

```bash
 kg po --field-selector spec.nodeName=worker-c7j8z-7bc5db6557-dbcfz
 ```

* get events for a specific resource:

```bash
kubectl get events --field-selector involvedObject.kind=Pod,involvedObject.name=kube-proxy-4x6h2
```

* show every resource in a namespace:

```bash
kubectl api-resources --verbs=list --namespaced -o name \
 | xargs -n 1 kubectl get --show-kind --ignore-not-found -n NAMESPACE
```

* impersonate a service account:

```bash
kubectl auth can-i $verb $resource/$name --as=system:serviceaccount:$namespace:$serviceaccount
kubectl auth can-i use psp/kong-kong-app-psp --as=system:serviceaccount:giantswarm:kong-kong-app
```

* get logs from previous pod if it has died:

```bash
kubectl logs --previous traefik-ingress-controller-zcspk --namespace kube-system
```

* temporarily disable a daemonset, and re-enable it later:

```bash
kubectl patch ds dsname -p '{"spec": {"template": {"spec": {"nodeSelector": {"non-existing": "true"}}}}}'
kubectl patch ds dsname -p --type json -p='[{"op": "remove", "path": "/spec/template/spec/nodeSelector/non-existing"}]'
```

* roll back a deployment:

```bash
kubectl rollout history deploy/name
deployment.extensions/name
REVISION  CHANGE-CAUSE
276       <none>
277       <none>
278       <none>
279       <none>
$ kubectl rollout undo deployment/happa --to-revision 279
deployment.extensions/happa rolled back
```

* get all evicted pods:

```bash
kubectl get pods --all-namespaces -o json | jq '.items[] | select(.status.reason!=null) | select(.status.reason | contains("Evicted"))'
```

* delete all failed pods:

```bash
kubectl -n default delete pods --field-selector=status.phase=Failed
```

* find pods consuming disk space:

```bash
TOP_STORAGE=$(du -hs /var/lib/docker/overlay2/* | grep -Ee '^[0-9]{3}[M]+|[0-9]G' | sort -h |tail -n 10 |tee -a /dev/stderr |awk '{print $2}'|xargs|sed 's/ /|/g')

docker inspect $(docker ps -q) | jq '.[]|.Config.Hostname,.Config.Labels."io.kubernetes.pod.name",.GraphDriver.Data.MergedDir,.hovno' | egrep -B2 "$TOP_STORAGE"

docker image inspect $(docker images -aq) | jq '.[]|.RepoDigests[0],.GraphDriver.Data.MergedDir,.hovno' |egrep -B2 "$TOP_STORAGE" 
```

* find service pods which can use a specific PSP:

```bash
kubectl get rolebindings,clusterrolebindings -A -o custom-columns='KIND:kind,NAMESPACE:metadata.namespace,NAME:metadata.name,SERVICE_ACCOUNTS:subjects[?(@.kind=="ServiceAccount")].name' | grep privileged
```

### nodes

```bash
kubectl get nodes
NAME       STATUS     ROLES     AGE       VERSION
memkube4   Ready      master    14d       v1.8.1+coreos.0
memkube5   NotReady   master    14d       v1.8.1+coreos.0
memkube6   NotReady   node      14d       v1.8.1+coreos.0
memkube7   NotReady   node      14d       v1.8.1+coreos.0
memkube8   NotReady   node      14d       v1.8.1+coreos.0
```

```bash
netstat -plunt | grep 10250
tcp        0      0 10.5.184.15:10250       0.0.0.0:*               LISTEN      24449/kubelet
```

```bash
curl -L https://10.5.184.15:10250/healthz
ok
```

### JSON trickery

* get all nodes and their taints:

```bash
kubectl get nodes -o=jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.io/role}{"\t"}{.spec.taints}{"\n"}{end}'
```

* show tainted nodes and their taints:

```bash
kubectl get nodes -o=jsonpath='{range .items[?(@.spec.taints)]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.io/role}{"\t"}{.spec.taints}{"\n"}{end}'
```
