#### Resource 资源限制

##### 简述

resource指的是pod的计算资源，包含cpu和memory。

定义pod的时候可以为每个container指定需要的cpu和memory。在指定了资源需求后，调度器能够把pod分配到合适的节点。pod设置的资源的request和limit，会决定其QoS(服务质量)。

##### 定义资源请求

CPU请求以`cpu unit`为计量，内存请求以`bytes`为计量.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: memory-demo
  namespace: mem-example
spec:
  containers:
  - name: memory-demo-ctr
    image: polinux/stress
    resources:
      limits:
      	cpu: "1"
        memory: "200Mi"
      requests:
      	cpu: "0.5"
        memory: "100Mi"
```

创建pod的时候，k8s的调度器首先会对k8s节点进行容量检查并将pod分配到合适的节点，以保证cpu和memory的request均被满足。

##### Qos

根据pod的资源请求的request和limit，按照等级从高到低，QoS分为三种：

* Guaranteed
  * pod中所有容器都配置了CPU的request和limits，并且request和limits相等
  * pod中所有容器都设置了memory的request和limits，并且request和limits相等
* Burstable
  * 非guarnteed、非BestEffort
* BestEffort
  * pod里的任何容器都没有配置cpu和memory的request和limits

根据qos等级驱逐pod：

* 当k8s的节点cpu资源不足时候，pod不会被驱逐，但是会被暂时限制
* 当k8s的节点内存不足时候
  * BestEffort级别的pod可以使用所有空闲资源，但是如果节点内存资源紧张，会优先被杀死
  * Guaranted级别的pod不会杀死，除非使用资源超出了其limits，或者节点内存紧张且没有更低等级的pod
  * Burstable级别的驱逐策略位于以上两者之间。