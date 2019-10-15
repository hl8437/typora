## ClientConn创建连接

### ClientConn结构

grpc/clientconn.go

```go
type ClientConn struct {
	ctx    context.Context
	cancel context.CancelFunc
	
	// 用户传入的目标
	target       string
	// 转化之后的target，包含scheme，authority，endpoint
	parsedTarget resolver.Target
	authority    string
	// 连接配置
	dopts        dialOptions
	// 连接状态管理器
	csMgr        *connectivityStateManager

	// 创建balancer的配置
	balancerBuildOpts balancer.BuildOptions
	
	blockingpicker    *pickerWrapper

	mu              sync.RWMutex
	// resolverwrapper 实现了resolver/clientConn接口
	// CCResolverWrapper的成员方法基本是直接调用了grpc/ClientConn的方法
	resolverWrapper *ccResolverWrapper
	sc              *ServiceConfig
	// 所有的子链接
	conns           map[*addrConn]struct{}
	// Keepalive parameter can be updated if a GoAway is received.
	mkp             keepalive.ClientParameters
	
	
	curBalancerName string
	// ccBalancerWrapper 实现了balancer/balancer接口
	// 其成员方法基本是直接调用了grpc/clientconn的成员方法
	balancerWrapper *ccBalancerWrapper
	
	retryThrottler  atomic.Value

	firstResolveEvent *grpcsync.Event

	channelzID int64 // channelz unique identification number
	czData     *channelzData
}
```

### 程序