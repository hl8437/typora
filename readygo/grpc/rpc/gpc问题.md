## gprc相关问题

+ 是否能够通过用户自己编写的 go struct 结构体生成对应的序列化/反序列化声明
+ 相关文件该存放在 readygo 项目中的哪些文件夹中？作为什么样的 package 出现？
  + 
+ 如何对提供 RPC 的服务进行测试？
+ 如何改造 RPC 客户端，使得能够对 RPC 调用进行超时控制或失败自动重试？
+ RPC 客户端是否支持 k8s 服务发现？
+ RPC 客户端的负载均衡策略是否合理？



## 简化复杂度

+ 每个工程仅仅支持一个server
  +  



## proto文件及生成文件位置

+ 方案一
  + 新建一个repo，专门用于存放每个部门的proto文件及生成文件