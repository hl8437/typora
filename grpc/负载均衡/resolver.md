## resolver

### overview

+ 支持不同名称系统
+ 对于不同名称系统，可以注册自己的解析方法

### resolver.go

+ 可以注册多个 解析器工厂

```go
var (
	m = make(map[string]Builder)
	defaultScheme = "passthrough"
)

func Register(b Builder) {
	m[b.Scheme()] = b
}

func Get(scheme string) Builder {
	if b, ok := m[scheme]; ok {
		return b
	}
	return nil
}


func SetDefaultScheme(scheme string) {
	defaultScheme = scheme
}

func GetDefaultScheme() string {
	return defaultScheme
}
```

