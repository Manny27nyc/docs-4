# Testnets for smartBCH

You can test your DApp using a [local single-node testnet](developers-guide/runsinglenode.md) if you want to set one up. In most cases, though, you might not need to set up a testnet yourself. Instead, you can using an existing testnet. Here are the running testnets you can utilize.

You can run tests with [metamask](developers-guide/test-using-metamask.md), [truffle](developers-guide/deploy-contract-using-truffle.md), or [remix](developers-guide/deploy-contract-using-remix.md).



### The Amber Testnet

This is a testnet for smartBCH with votes from a BCHN testnet, which has a bitcoincashnode client which mines with CPU.The chain ID is 0x2711. You can use the following JSON-RPC nodes:

1. http://35.220.203.194:8545
2. https://moeing.tech:9545

Test coin faucet can be found at http://34.92.246.27:8080/faucet

We sincerely thank [Allen Day](https://github.com/allenday) for donating several cloud servers to bring up this testnet. 

In this testnet, the gas price can be as low as 0.2Gwei.

To join this testnet as a non-validator node, follow the steps below:

First, build the latest binary by running the step 0, 1, 2, 3 of [this document](developers-guide/runsinglenode.md).

Second, clone & build smartbch from amber branch:

```bash
cd ~/smart_bch
git clone -b v0.4.2 --depth 1 https://github.com/smartbch/smartbch
cd smartbch
go build -tags "params_amber cppbtree" github.com/smartbch/smartbch/cmd/smartbchd
```

Third, prepare the working directory:

```bash
cp ~/smart_bch/smartbch/smartbchd ~/build/smartbchd
cd ~
rm -rf .smartbchd
~/build/smartbchd init mynode --chain-id 0x2711
wget https://github.com/smartbch/artifacts/releases/download/v0.0.4/dot.smartbchd.tgz
tar zxvf dot.smartbchd.tgz
cp -rf dot.smartbchd/* .smartbchd/
```

Last, start smartbchd. 

```bash
~/build/smartbchd start --mainnet-genesis-height=602983
```

Then you can join the testnet as a non-validator. If want to become a validator, please follow  [this guide](developers-guide/runmultinode.md).

If you want to join the underlying BCH testnet, here is the configuration file for bitcoincashnode:

```
regtest=1

[regtest]

bind=0.0.0.0
port=8331
rpcbind=0.0.0.0
rpcport=8332

zmqpubhashtx=tcp://0.0.0.0:8333
zmqpubhashblock=tcp://0.0.0.0:8333

rpcuser=test
rpcpassword=test
rpcthreads=4

rpcallowip=0.0.0.0/0

whitelistrelay=0

addnode=47.115.171.70:28331
```

