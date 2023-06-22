# Watcher

[![Go Reference](https://pkg.go.dev/badge/github.com/livebud/watcher.svg)](https://pkg.go.dev/github.com/livebud/watcher)

Resilient file watcher. Used in [Bud](https://github.com/livebud/bud).

## Features

- Watches a directory recursively
- Debounces multiple events into a single function call
- Smooths over differences between operating systems
- Ignores files in your `.gitignore`
- Generally does what you'd expect

## Install

```sh
go get -u github.com/livebud/watcher
```

## Example

```go
package main

import (
  "context"
  "fmt"
  "os"

  "github.com/livebud/watcher"
)

func main() {
  ctx := context.Background()
  if err := run(ctx); err != nil {
    fmt.Fprintln(os.Stderr, err)
    os.Exit(1)
  }
}

func run(ctx context.Context) error {
  return watcher.Watch(ctx, ".", func(events []watcher.Event) error {
    for _, event := range events {
      fmt.Println(string(event.Op), event.Path)
    }
    return nil
  })
}
```

## Contributing

Thank you for your interest in contributing! To get started, first clone the repo:

```sh
git clone https://github.com/livebud/watcher
cd watcher
```

Next, install the dependencies:

```sh
go mod tidy
```

Finally, try running the tests:

```sh
go test ./...
```

## License

MIT
