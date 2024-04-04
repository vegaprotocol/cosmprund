# Cosmos-Pruner

The goal of this project is to be able to prune a tendermint data base of blocks and an Cosmos-sdk application DB of all but the last X versions. This will allow people to not have to state sync every x days. 

## How to use

### Download binary from the release

We build release for MacOS and Linux for the amd64 and arm64 architectures. You can find them in [the release page](https://github.com/vegaprotocol/cosmprund/releases/).

### Build from source code 

You need go 1.22 to build this repository

```
git clone https://github.com/vegaprotocol/cosmprund.git
go build -o ./cosmprund ./main.go
./cosmprund --help
```

## How to use with Vega

1. Stop your Vega node
2. Download [cosmprund tool](https://github.com/vegaprotocol/cosmprund/releases)
3. Run the following command with the same user which runs vega/visor process: 

```
 ./vega-cosmprund-linux-amd64 prune <tendermint_home>/data/ --blocks 100000
```
Note: It may take up to 2/3 hour depending on how much data you have in the tendermint blocks store

4. Start your Vega node

Note: It takes a few mins if you run it periodically e.g: once a week.

### Note
To use this with RocksDB you must:

```bash
go install -ldflags '-w -s -X github.com/cosmos/cosmos-sdk/types.DBBackend=rocksdb' -tags rocksdb ./...
```
