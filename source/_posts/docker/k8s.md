

#### StatefulSet

    https://draveness.me/kubernetes-statefulset/

是用于管理有状态应用的工作负载对象，与 ReplicaSet 和 Deployment 这两个对象不同，StatefulSet 不仅能管理 Pod 的对象，还它能够保证这些 Pod 的顺序性和唯一性。


### 查看运行时间

    kubectl get pod -A --sort-by=.status.startTime
    kubectl get pod -A --sort-by=.status.startTime -o custom-columns=jettech_name:.spec.containers[0].name,jettech_image:.spec.containers[0].image

    .metadata.name
    .items[0].metadata.namespace
    
    kubectl get pod -A --sort-by=.status.startTime -o custom-columns=ns:.items[0].metadata.namespace,age:
    kubectl get pod -A --sort-by=.status.startTime -o custom-columns=ns:.metadata.namespace,age:.metadata.creationTimestamp,age1:.AGE | more
    