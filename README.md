# geth-regtest
Regtest like ethereum private network setup


# Motivation 

Normally, at `Bitcoin`, `Rootstock` or other blockchains there are regression test configurations for development. Those configs allows:

- Mine blocks fast for when we are under development (like `Truffle` or `Ganache` i.e) 
- Test our dApps, Smart Contracts or layer two solutions
- Just focus on setup one unique node

There is no `regtest` client for `geth`, at least at this moment (*) but we can create a private network with one miner. 

(*)
- https://ethereum.stackexchange.com/questions/1839/regtest-mode-on-ethereum
- https://ethereum.stackexchange.com/questions/22906/geth-dev-mining



# Prerequisite

`geth` installed: https://github.com/ethereum/go-ethereum/wiki/Installing-Geth



# Setup

1. Git clone the repo. You will find a structure like this: 

```
.
├── node1
│   ├── geth
│   ├── keystore
│   │   └── UTC--2020-02-05T21-41-26.785694343Z--d025f1e3f633eb4816661c68155b6bf9cc43be16
│   └── password.txt
└── regtest-low-dif.json

```

Where: 

- `node1`: folder where the private chain data is stored. 
- `geth`: node database
- `keystore`: the address that we are going to use to interact with our node.
- `password`: the password of the keystore file
- `regtest-low-dif.json`: genesis file

2. Put your keystore on the `keystore` folder, just as the example. 
3. Modify the `password.txt` file and put your keystore password
4. Modify the `regtest-low-dif.json` genesis file: replace the example address `d025f1e3f633eb4816661c68155b6bf9cc43be16` for your address under the `alloc` config. This will give you some ETH when you create your chain
5. The `regtest-low-dif-json` uses a low mining dificulty (`0x1`) in order to have fast blocks and set up your chain with the `chain-id` = `33`. You can change both values if you want

Note: 

The `regtest-low-dif-json` was created using `puppeth`, only the account balance and difficulty were modified. Feel free to use `puppeth` to create the genesis file instead of using the provided.


# Initialize the regtest blockchain 

`eth-regtest$ geth --datadir ./node1 init regtest-low-dif.json`

# Run your regtest node

`eth-regtest$ geth --networkid 33 --mine --minerthreads 3 --datadir ./node1 --nodiscover --rpc --rpcport "4444" --port "30303" --rpccorsdomain "*" --nat "any" --rpcapi eth,web3,personal,net --unlock 'd025f1e3f633eb4816661c68155b6bf9cc43be16' --password ./node1/password.txt`


```
INFO [02-09|16:20:44.525] Maximum peer count                       ETH=25 LES=0 total=25
INFO [02-09|16:20:44.526] Starting peer-to-peer node               instance=Geth/v1.8.23-stable-c9427004/linux-amd64/go1.10.4
INFO [02-09|16:20:44.526] Allocated cache and file handles         database=/home/marcos/sandbox/geth-regtest/node1/geth/chaindata cache=512 handles=2048
INFO [02-09|16:20:44.546] Initialised chain configuration          config="{ChainID: 33 Homestead: 1 DAO: <nil> DAOSupport: false EIP150: 2 EIP155: 3 EIP158: 3 Byzantium: 4 Constantinople: 5  ConstantinopleFix: <nil> Engine: ethash}"
INFO [02-09|16:20:44.547] Disk storage enabled for ethash caches   dir=/home/marcos/sandbox/geth-regtest/node1/geth/ethash count=3
INFO [02-09|16:20:44.547] Disk storage enabled for ethash DAGs     dir=/home/marcos/.ethash                                count=2
INFO [02-09|16:20:44.547] Initialising Ethereum protocol           versions="[63 62]" network=33
INFO [02-09|16:20:44.591] Loaded most recent local header          number=0 hash=3936cc…c5fa46 td=1 age=4d21h7m
INFO [02-09|16:20:44.591] Loaded most recent local full block      number=0 hash=3936cc…c5fa46 td=1 age=4d21h7m
INFO [02-09|16:20:44.591] Loaded most recent local fast block      number=0 hash=3936cc…c5fa46 td=1 age=4d21h7m
INFO [02-09|16:20:44.591] Regenerated local transaction journal    transactions=0 accounts=0
INFO [02-09|16:20:44.602] New local node record                    seq=1 id=edbe7cc451162274 ip=127.0.0.1 udp=0 tcp=30303
INFO [02-09|16:20:44.602] Started P2P networking                   self="enode://2601d63ca35a67b8db582df6bba5ea3c088e8b5d3188877215eeecc53f86ab0bddb3de2b81eb8ba5c58a90e62eadbc6516bc08120f427c1bd262981d498be997@127.0.0.1:30303?discport=0"
INFO [02-09|16:20:44.603] IPC endpoint opened                      url=/home/marcos/sandbox/geth-regtest/node1/geth.ipc
INFO [02-09|16:20:44.604] HTTP endpoint opened                     url=http://127.0.0.1:4444                            cors=* vhosts=localhost
INFO [02-09|16:20:45.298] Unlocked account                         address=0xd025f1E3f633eB4816661c68155B6bF9cc43BE16
INFO [02-09|16:20:45.299] Transaction pool price threshold updated price=1000000000
INFO [02-09|16:20:45.299] Updated mining threads                   threads=3
INFO [02-09|16:20:45.299] Transaction pool price threshold updated price=1000000000
INFO [02-09|16:20:45.299] Etherbase automatically configured       address=0xd025f1E3f633eB4816661c68155B6bF9cc43BE16
INFO [02-09|16:20:45.299] Commit new mining work                   number=1 sealhash=87abe7…2ac51d uncles=0 txs=0 gas=0 fees=0 elapsed=234.691µs
INFO [02-09|16:20:46.775] Successfully sealed new block            number=1 sealhash=87abe7…2ac51d hash=b68ceb…e96fa1 elapsed=1.475s
INFO [02-09|16:20:46.775] 🔨 mined potential block                  number=1 hash=b68ceb…e96fa1
INFO [02-09|16:20:46.775] Commit new mining work                   number=2 sealhash=a52e98…33c3ec uncles=0 txs=0 gas=0 fees=0 elapsed=178.11µs
INFO [02-09|16:20:49.861] Successfully sealed new block            number=2 sealhash=a52e98…33c3ec hash=329a69…5197c2 elapsed=3.086s
INFO [02-09|16:20:49.861] 🔨 mined potential block                  number=2 hash=329a69…5197c2
INFO [02-09|16:20:49.862] Commit new mining work                   number=3 sealhash=08c3f5…35bd94 uncles=0 txs=0 gas=0 fees=0 elapsed=121.208µs
INFO [02-09|16:20:50.702] Successfully sealed new block            number=3 sealhash=08c3f5…35bd94 hash=91c34a…d26417 elapsed=840.245ms
INFO [02-09|16:20:50.702] 🔨 mined potential block                  number=3 hash=91c34a…d26417
INFO [02-09|16:20:50.702] Commit new mining work                   number=4 sealhash=bbaf59…f5a148 uncles=0 txs=0 gas=0 fees=0 elapsed=141.451µs
INFO [02-09|16:20:51.096] Successfully sealed new block            number=4 sealhash=bbaf59…f5a148 hash=fa626c…d5b414 elapsed=394.091ms
INFO [02-09|16:20:51.096] 🔨 mined potential block                  number=4 hash=fa626c…d5b414
INFO [02-09|16:20:51.096] Commit new mining work                   number=5 sealhash=ae6b01…7d3f14 uncles=0 txs=0 gas=0 fees=0 elapsed=156.355µs
INFO [02-09|16:20:51.542] Successfully sealed new block            number=5 sealhash=ae6b01…7d3f14 hash=192229…d4f1d9 elapsed=445.586ms
INFO [02-09|16:20:51.542] 🔨 mined potential block                  number=5 hash=192229…d4f1d9
INFO [02-09|16:20:51.542] Commit new mining work                   number=6 sealhash=740436…9fc5f7 uncles=0 txs=0 gas=0 fees=0 elapsed=122.621µs
INFO [02-09|16:20:51.595] Successfully sealed new block            number=6 sealhash=740436…9fc5f7 hash=f13bf6…fb0451 elapsed=52.757ms
INFO [02-09|16:20:51.595] 🔨 mined potential block                  number=6 hash=f13bf6…fb0451
INFO [02-09|16:20:51.595] Mining too far in the future             wait=2s
INFO [02-09|16:20:53.596] Commit new mining work                   number=7 sealhash=7c59ec…6304fd uncles=0 txs=0 gas=0 fees=0 elapsed=2.000s
INFO [02-09|16:20:54.713] Successfully sealed new block            number=7 sealhash=7c59ec…6304fd hash=ecf40e…2a81de elapsed=1.117s
INFO [02-09|16:20:54.713] 🔨 mined potential block                  number=7 hash=ecf40e…2a81de
INFO [02-09|16:20:54.714] Commit new mining work                   number=8 sealhash=44f506…110e28 uncles=0 txs=0 gas=0 fees=0 elapsed=146.576µs
INFO [02-09|16:20:57.884] Successfully sealed new block            number=8 sealhash=44f506…110e28 hash=790bcc…27f819 elapsed=3.170s
INFO [02-09|16:20:57.884] 🔗 block reached canonical chain          number=1 hash=b68ceb…e96fa1
INFO [02-09|16:20:57.884] 🔨 mined potential block                  number=8 hash=790bcc…27f819
INFO [02-09|16:20:57.884] Commit new mining work                   number=9 sealhash=84ad2a…a1b713 uncles=0 txs=0 gas=0 fees=0 elapsed=127.872µs
INFO [02-09|16:20:58.094] Successfully sealed new block            number=9 sealhash=84ad2a…a1b713 hash=7daa37…bf9c2a elapsed=210.094ms
INFO [02-09|16:20:58.094] 🔗 block reached canonical chain          number=2 hash=329a69…5197c2
INFO [02-09|16:20:58.094] 🔨 mined potential block                  number=9 hash=7daa37…bf9c2a
INFO [02-09|16:20:58.095] Commit new mining work                   number=10 sealhash=500112…576194 uncles=0 txs=0 gas=0 fees=0 elapsed=122.243µs
INFO [02-09|16:20:58.430] Successfully sealed new block            number=10 sealhash=500112…576194 hash=8a99f6…1ee9ed elapsed=335.433ms
INFO [02-09|16:20:58.430] 🔗 block reached canonical chain          number=3  hash=91c34a…d26417
INFO [02-09|16:20:58.430] 🔨 mined potential block                  number=10 hash=8a99f6…1ee9ed
INFO [02-09|16:20:58.430] Commit new mining work                   number=11 sealhash=54e074…3e8573 uncles=0 txs=0 gas=0 fees=0 elapsed=152.655µs

```


# Restart from genesis block 

If you want to restart the chain just

- remove the `node1/geth` folder
- initialize again the chain ( `eth-regtest$ geth --datadir ./node1 init regtest-low-dif.json` )
- run! 


