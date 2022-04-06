# microplugin
## nacos(可用于micro v4的nacos v1注册中心)
示例代码
```go
package main

import (
	"github.com/nacos-group/nacos-sdk-go/common/constant"
	"github.com/zhang-jianqiang/microplugin/nacos"
	"go-micro.dev/v4"
)

var (
	service = "go-layout"
	version = "latest"
)

func main() {
	// Init registry
	r := nacos.NewRegistry(nacos.WithAddress([]string{
		"127.0.0.1:8848",
	}), nacos.WithClientConfig(constant.ClientConfig{
		NamespaceId: "2204843f-d11a-440f-ba15-00d33d3f2f91",
		LogLevel:    "error",
		CacheDir:    "/nacos",
	}))

	// Create service
	srv := micro.NewService(
		micro.Name(service),
		micro.Version(version),
		micro.Registry(r),
	)
	srv.Init()

	// Run service
	srv.Run()
}

```

说明：如果想让github仓库中某个目录单独作为一个go module依赖，那么打tag时，需要加上目录前缀，如项目中的nacos，只想将nacos目录作为一个依赖，那么打tag时，tag应为：nacos/v1.0.0
