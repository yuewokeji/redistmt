# Redistmt

Redistmt return a short statement without values, which will be replaced with some characters(the default is '?').

# Initialization

```shell script
go get -u github.com/yuewokeji/redistmt
```

# Usage

```go
package main

import (
	"context"
	"fmt"
	"github.com/go-redis/redis/v8"
	"github.com/yuewokeji/redistmt"
	"time"
)

func main() {
	client := redis.NewClient(&redis.Options{
		Addr: "127.0.0.1",
	})

	cmd1 := client.Set(context.Background(), "key", "value", time.Minute)
	stmt1 := redistmt.NewStatement(cmd1.Args())
	fmt.Println(stmt1.ShortString())
	// set key ? ex 60

	cmd2 := client.MSet(context.Background(), "key1", "value1", "key2", "value2")
	stmt2 := redistmt.NewStatement(cmd2.Args())
	fmt.Println(stmt2.ShortString())
	// mset key1 ? key2 ?
}
```
