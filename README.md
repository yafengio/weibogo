weibogo
======

[中文版本](README-CN.md)

Sina Weibo SDK for Go language, supporting all <a href="http://open.weibo.com/wiki/微博API">Weibo API features</a>

# Installation/Update

```
go get -u github.com/yafengio/weibogo
```

# Usage

Fetch the latest 10 posts from <a href="http://weibo.com/rmrb">@People's Daily</a>:

```go
package main

import (
	"flag"
	"fmt"
	"github.com/yafengio/weibogo"
)

var (
	weibo = weibogo.Weibo{}
	access_token = flag.String("access_token", "", "User's access token")
)

func main() {
	// Parse command line arguments
	flag.Parse()

	// Call API
	var statuses weibogo.Statuses
	params := weibogo.Params{"screen_name": "人民日报", "count": 10}
	err := weibo.Call("statuses/user_timeline", "get", *access_token, params, &statuses)
	
	// Process results
	if err != nil {
		fmt.Println(err)
		return
	}
	for _, status := range statuses.Statuses {
		fmt.Println(status.Text)
	}
}
```

Pass the access token via the command line parameter -access_token. The token can be obtained through the <a href="http://open.weibo.com/tools/console">API Testing Tool</a> or <a href="https://github.com/yafengio/weibogo/blob/master/examples/auth.go">weibogo.Authenticator</a>.

For more API call examples, see <a href="https://github.com/yafengio/weibogo/blob/master/examples/weibo.go">examples/weibo.go</a>.