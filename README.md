# xsrftoken

This package provides methods for generating and validating secure XSRF tokens.

This is a fork of the original `golang.org/x/net/xsrftoken` package. The main difference is that this version uses **SHA-256** for hashing, whereas the original used SHA-1.

## Installation

To get the package, execute:

```sh
go get github.com/haturatu/xsrftoken
# or
GOPROXY=direct go get github.com/haturatu/xsrftoken@latest
```

## Usage

To use the package in your Go project, import it as follows:

```go
import "github.com/haturatu/xsrftoken"
```

Here is a simple example:

```go
package main

import (
	"fmt"
	"log"

	"github.com/haturatu/xsrftoken"
)

func main() {
	// A secret key for your application. Must be non-empty.
	key := "your-super-secret-key"
	// A unique identifier for the user.
	userID := "user123"
	// An identifier for the action being performed.
	actionID := "/profile/update"

	// Generate a token.
	token := xsrftoken.Generate(key, userID, actionID)
	fmt.Printf("Generated token: %s
", token)

	// Validate the token.
	isValid := xsrftoken.Valid(token, key, userID, actionID)
	if isValid {
		log.Println("Token is valid!")
	} else {
		log.Println("Token is invalid!")
	}

	// Example of an invalid token
	isInvalid := xsrftoken.Valid("an-obviously-invalid-token", key, userID, actionID)
	if !isInvalid {
		log.Println("As expected, the invalid token was correctly identified.")
	}
}
```

## Author

This modified version is by [haturatu](https://github.com/haturatu).

The original package was developed by The Go Authors.
