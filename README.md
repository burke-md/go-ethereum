# Go Ethereum trace eth_call test

Install [Go lang](https://go.dev/doc/install)

Build Geth:
```bash
go install -v ./cmd/geth
```

Run specific test:
```bash
go test -v ./eth -run TestMethod
```

## Rough notes on path to follow:

`eth_call` is an RPC method that executes a new message call immediately without creating a transaction on the block chain. Read more from [alchemy](https://docs.alchemy.com/reference/eth-call)

Starting in `/internal/ethapi/api.go` see func `Call()` L:1107 <- This is essentially where the api takes eth_call

- No signature
- No sender address

See func ` DoCall()`

### TX vs Message:

`TX has no from feild, it has a signature that must be cryptographically recovered. Message has a 'from' field.`

See line `core.ApplyMessage()`.

`/core/state_transition.go` L:177
- ApplyMessage()
- create new state transition
- TransitionDb()
- preCheck() nounce, gas, block gas etc

### Side quest:
eth_call can be used to create contracts. Within the init code we can "do stuff". Essentially scripting. While eth_call doesnt require gas, it does check wallet address as if actually executing. The block state will not be mutated onchain - however functions will be run locally and data returned to API call, as if state had been changes. Additionally, eth_call accepts an `override` and specific block numbers. This could be usefull for mocking state or looking back. 

Intrinsic gas. This is no longer as simple as it once was. 
Transfer is call contained `msg.value`

L:344 Access List. See metamorphic RSA write up. Cross refference?




