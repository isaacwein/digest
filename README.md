# Digest
it's a go implementation for digest auth

### Download
```cmd
go get github.com/telebroad/digest
```

### DEMOS
#### Basic example

```go
package main

import (
	"fmt"
	"github.com/telebroad/digest"
)

var (
	method    = "POST"
	host      = "https://www.example.com"
	uri       = "/some/route"
	user      = "my-username"
	pass      = "my-password"
	userAgent = "test-user-agent"
)

func main() {
	token, err := digest.Token(method, host, uri, user, pass, userAgent, false)
	if err != nil {
		// handle error
	}

	fmt.Printf("http header token: %s\n",token)
}
```

#### more advance

```go
package main

import (
	"github.com/telebroad/digest"
	"net/http"
	"strings"
)

var (
	method    = "POST"
	host      = "https://www.example.com"
	uri       = "/some/route"
	user      = "my-username"
	pass      = "my-password"
	userAgent = "test-user-agent"
)

func main() {
	dig, err := digest.New(method, host, uri, user, pass, userAgent, false)
	if err != nil {
		// handle error
	}
	// this will return http request and append the header to it 
	req, err := dig.Request(strings.NewReader("<body>some example body</body>"))
	if err != nil {
		// handle error
	}

	client := &http.Client{}

	resp, err := client.Do(req)
	if err != nil {
		// handle error
	}
}
```