## Go Ethereum trace transaction test

Install [Go lang](https://go.dev/doc/install)

Build Geth:
```bash
go install -v ./cmd/geth
```

Run specific test:
```bash
go test -v ./eth -run TestMethod
```
