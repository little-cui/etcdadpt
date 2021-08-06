# etcd-adapter
Expose a standard KV operation [API](api.go), adapt to embeded etcd and etcd client

## How to use?

Step 1. Import the module and it's all plugins.

```go
import (
	github.com/little-cui/etcdadpt
	_ "github.com/little-cui/etcdadpt/embedded"
	_ "github.com/little-cui/etcdadpt/remote"
)
```

Step 2. Select one mode and do initialization.

**With embedded etcd mode:**
```go
etcdadpt.Init(etcdadpt.Config{
	Kind:             "embedded_etcd", 
	ClusterName:      "c-0", 
	ClusterAddresses: "c-0=http://127.0.0.1:2380",
})
```
This mode will start an embedded etcd server.

**With remote etcd mode:**
```go
etcdadpt.Init(etcdadpt.Config{
	Kind:             "etcd", 
	ClusterAddresses: "127.0.0.1:2379",
})
```

Step 3. call the API and enjoy it!

```go
kv, err := etcdadpt.Get(context.Background(), "/key")
log.Println(fmt.Sprintf("%v", kv))
```
and you will see log print below:
```shell
key:"/key" create_revision:4 mod_revision:4 version:1 value:"abc"
```

## Examples

Also see the full demo [HERE](examples/dev/main.go)!