# gRPC资料

## 相关概念

### http2

#### 链接

* [http2简介](https://developers.google.com/web/fundamentals/performance/http2/)

  http2简单介绍以及http2的新特性。简单介绍了http2的二进制分帧层、请求与响应多路复用、数据优先级、流控制、服务器推送、标头压缩、hpack等

* [http1.0、http1.1、http2.0等版本区别](https://www.jianshu.com/p/be29d679cbff)



## gRPC概念

### 负载均衡

* [grpc负载均衡官方文档](https://github.com/grpc/grpc/blob/master/doc/load-balancing.md)

  介绍了常见的三种负载均衡的实现方式，代理实现、客户端实现、sidecar。

  之后介绍了grpc本身推荐的负载均衡实现方式

* [在k8s上实现grpc的负载均衡](https://kubernetes.io/blog/2018/11/07/grpc-load-balancing-on-kubernetes-without-tears/)

  由于grpc基于HTTP2，使用长连接进行负载均衡，默认的kube-proxy均衡失效。

  本文是用来推广linker工具的，同时在文中提到了三种解决grpc在k8s上的负载均衡问题的方法。

  * 手动维护连接池
  * 使用headless service
  * 使用轻量级代理

#### KeepAlive

* [官方文档](https://github.com/grpc/grpc/blob/master/doc/keepalive.md)

  keep alive 指的是：grpc为了检查



## gRPC生态

* [grpc-ecosystem](https://github.com/grpc-ecosystem)

  grpc生态，包含各种中间件

* [awesome-grpc](https://github.com/grpc-ecosystem/awesome-grpc)

  有用的grpc资源精选列表