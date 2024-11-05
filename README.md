# go-tron-demo

```go
package main

import (
	"log"

	tronacc "github.com/jnsand/go-tron/account"
	tronaddr "github.com/jnsand/go-tron/address"
	tronclient "github.com/jnsand/go-tron/client"
)

const (
	Mainnet       = "https://api.trongrid.io"
	ShastaTestnet = "https://api.shasta.trongrid.io"
	NileTestnet   = "https://nile.trongrid.io"
)

const (
	senderPrivateKey = "b293b70bfa21d394c3341cf8f45ec17c241d8e2996fd3f9ab00dc620f326a2f2"
	receiverAddress  = "TTSErV8W4g1ZNbHsQdXBbvL9v3GFu9VyUd"
)

func main() {
	client := tronclient.New(ShastaTestnet)

	sender, err := tronacc.FromPrivateKeyHex(senderPrivateKey)
	if err != nil {
		log.Fatal("Failed to parse private key hex - ", err)
	}

	receiver, err := tronaddr.FromBase58(receiverAddress)
	if err != nil {
		log.Fatal("Invalid base58 address - ", err)
	}

	// Send 1 TRX
	tx, nil := client.Transfer(sender, receiver, 1000000)
	if err != nil {
		log.Fatal("Failed to transfer token - ", err)
	}

	log.Printf("%#v\n", tx)
}

```