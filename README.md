# geth-regtest
Regtest like ethereum private network setup

# Motivation 

Normally, at Bitcoin, Rootstock or other blockchains there are regression test configurations for development. Those configs allows:

- Mine blocks fast for when we are under development (like Truffle or Ganache i.e) 
- Test our dApps, Smart Contracts or layer two solutions
- Just focus on setup one unique node

There is no regtest client for geth, at least at this moment (*) but we can create a private network with one miner. 


(*)
- https://ethereum.stackexchange.com/questions/1839/regtest-mode-on-ethereum
- https://ethereum.stackexchange.com/questions/22906/geth-dev-mining

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

- node1: folder where the private chain data is stored. 
- geth: node database
- keystore: the address that we are going to use to interact with our node.
- password: the password of the keystore file
- regtest-low-dif.json: genesis file

2. Put your keystore on the keystore folder, just as the example. 
3. Modify the password.txt file and put your keystore password
4. Modify the regtest-low-dif.json genesis file: replace the example address d025f1e3f633eb4816661c68155b6bf9cc43be16 for your address under the alloc config. This will give you some ETH when you create your chain
5. The regtest-low-dif-json uses a low mining dificulty (0x1) in order to have fast blocks and set up your chain with the chain-id = 33. You can change both values if you want


# Initialize the regtest blockchain 

`eth-regtest$ geth datadir --node1 init regtest-low-dif.json`

# Run your regtest node

`eth-regtest$ geth --networkid 33 --mine --minerthreads 3 --datadir ./node1 --nodiscover --rpc --rpcport "4444" --port "30303" --rpccorsdomain "*" --nat "any" --rpcapi eth,web3,personal,net --unlock 'd025f1e3f633eb4816661c68155b6bf9cc43be16' --password ./node1/password.txt`


```
INFO [02-09|16:09:09.062] Maximum peer count                       ETH=25 LES=0 total=25
INFO [02-09|16:09:09.062] Starting peer-to-peer node               instance=Geth/v1.8.23-stable-c9427004/linux-amd64/go1.10.4
INFO [02-09|16:09:09.062] Allocated cache and file handles         database=/home/marcos/rsk/eth-regtest/node1/geth/chaindata cache=512 handles=2048
INFO [02-09|16:09:09.080] Initialised chain configuration          config="{ChainID: 33 Homestead: 1 DAO: <nil> DAOSupport: false EIP150: 2 EIP155: 3 EIP158: 3 Byzantium: 4 Constantinople: 5  ConstantinopleFix: <nil> Engine: ethash}"
INFO [02-09|16:09:09.080] Disk storage enabled for ethash caches   dir=/home/marcos/rsk/eth-regtest/node1/geth/ethash count=3
INFO [02-09|16:09:09.080] Disk storage enabled for ethash DAGs     dir=/home/marcos/.ethash                           count=2
INFO [02-09|16:09:09.080] Initialising Ethereum protocol           versions="[63 62]" network=33
INFO [02-09|16:09:09.128] Loaded most recent local header          number=6705 hash=abc2c8…07a603 td=3571614539 age=1m20s
INFO [02-09|16:09:09.128] Loaded most recent local full block      number=6705 hash=abc2c8…07a603 td=3571614539 age=1m20s
INFO [02-09|16:09:09.128] Loaded most recent local fast block      number=6705 hash=abc2c8…07a603 td=3571614539 age=1m20s
INFO [02-09|16:09:09.128] Loaded local transaction journal         transactions=0 dropped=0
INFO [02-09|16:09:09.128] Regenerated local transaction journal    transactions=0 accounts=0
WARN [02-09|16:09:09.128] Blockchain not empty, fast sync disabled 
INFO [02-09|16:09:09.142] New local node record                    seq=11 id=275d7cb01779cbf6 ip=127.0.0.1 udp=0 tcp=30303
INFO [02-09|16:09:09.142] Started P2P networking                   self="enode://75303aae389b6e0ea4eda77fc75493e926b3409ded287f7791611f00fefbec0bd8abc2f93cbbc13aadd13c9db9931b39d045250eaf918cd6bd4d35b35d55fda0@127.0.0.1:30303?discport=0"
INFO [02-09|16:09:09.144] IPC endpoint opened                      url=/home/marcos/rsk/eth-regtest/node1/geth.ipc
INFO [02-09|16:09:09.144] HTTP endpoint opened                     url=http://127.0.0.1:4444                       cors=* vhosts=localhost
INFO [02-09|16:09:09.821] Unlocked account                         address=0xd025f1E3f633eB4816661c68155B6bF9cc43BE16
INFO [02-09|16:09:09.821] Transaction pool price threshold updated price=1000000000
INFO [02-09|16:09:09.821] Updated mining threads                   threads=3
INFO [02-09|16:09:09.821] Transaction pool price threshold updated price=1000000000
INFO [02-09|16:09:09.821] Etherbase automatically configured       address=0xd025f1E3f633eB4816661c68155B6bF9cc43BE16
INFO [02-09|16:09:09.822] Commit new mining work                   number=6706 sealhash=8ff187…4b2b3a uncles=0 txs=0 gas=0 fees=0 elapsed=257.182µs
INFO [02-09|16:09:11.848] Successfully sealed new block            number=6706 sealhash=8ff187…4b2b3a hash=e13f56…5d1981 elapsed=2.026s
INFO [02-09|16:09:11.848] 🔨 mined potential block                  number=6706 hash=e13f56…5d1981
INFO [02-09|16:09:11.849] Commit new mining work                   number=6707 sealhash=22e781…8d6f16 uncles=0 txs=0 gas=0 fees=0 elapsed=171.242µs
INFO [02-09|16:09:13.928] Successfully sealed new block            number=6707 sealhash=22e781…8d6f16 hash=c650c5…e9b2e7 elapsed=2.079s
INFO [02-09|16:09:13.928] 🔨 mined potential block                  number=6707 hash=c650c5…e9b2e7
INFO [02-09|16:09:13.928] Commit new mining work                   number=6708 sealhash=5df8d0…924b47 uncles=0 txs=0 gas=0 fees=0 elapsed=111.544µs
INFO [02-09|16:09:18.259] Successfully sealed new block            number=6708 sealhash=5df8d0…924b47 hash=ba19e4…38b6ed elapsed=4.331s
INFO [02-09|16:09:18.259] 🔨 mined potential block                  number=6708 hash=ba19e4…38b6ed
INFO [02-09|16:09:18.260] Commit new mining work                   number=6709 sealhash=63698a…463d9c uncles=0 txs=0 gas=0 fees=0 elapsed=140.689µs
INFO [02-09|16:09:22.660] Successfully sealed new block            number=6709 sealhash=63698a…463d9c hash=e481c3…f9693d elapsed=4.400s
INFO [02-09|16:09:22.660] 🔨 mined potential block                  number=6709 hash=e481c3…f9693d
INFO [02-09|16:09:22.660] Commit new mining work                   number=6710 sealhash=ccb589…e299d1 uncles=0 txs=0 gas=0 fees=0 elapsed=118.789µs
INFO [02-09|16:09:26.982] Successfully sealed new block            number=6710 sealhash=ccb589…e299d1 hash=03319b…88ddac elapsed=4.322s
INFO [02-09|16:09:26.982] 🔨 mined potential block                  number=6710 hash=03319b…88ddac
INFO [02-09|16:09:26.983] Commit new mining work                   number=6711 sealhash=9c072b…896a6b uncles=0 txs=0 gas=0 fees=0 elapsed=162.305µs
INFO [02-09|16:09:27.526] Successfully sealed new block            number=6711 sealhash=9c072b…896a6b hash=b9dc04…44932c elapsed=542.988ms
INFO [02-09|16:09:27.526] 🔨 mined potential block                  number=6711 hash=b9dc04…44932c
INFO [02-09|16:09:27.526] Commit new mining work                   number=6712 sealhash=c54c20…678f8e uncles=0 txs=0 gas=0 fees=0 elapsed=148.437µs
INFO [02-09|16:09:28.407] Successfully sealed new block            number=6712 sealhash=c54c20…678f8e hash=f5d972…79ee30 elapsed=880.776ms
INFO [02-09|16:09:28.407] 🔨 mined potential block                  number=6712 hash=f5d972…79ee30
INFO [02-09|16:09:28.407] Commit new mining work                   number=6713 sealhash=920406…8b47e1 uncles=0 txs=0 gas=0 fees=0 elapsed=142.682µs
INFO [02-09|16:09:30.260] Successfully sealed new block            number=6713 sealhash=920406…8b47e1 hash=ff103c…e7f8e0 elapsed=1.853s
INFO [02-09|16:09:30.260] 🔗 block reached canonical chain          number=6706 hash=e13f56…5d1981
INFO [02-09|16:09:30.260] 🔨 mined potential block                  number=6713 hash=ff103c…e7f8e0
INFO [02-09|16:09:30.260] Commit new mining work                   number=6714 sealhash=54f358…22d2ab uncles=0 txs=0 gas=0 fees=0 elapsed=125.791µs
INFO [02-09|16:09:33.469] Successfully sealed new block            number=6714 sealhash=54f358…22d2ab hash=fd71d0…8b4613 elapsed=3.208s
INFO [02-09|16:09:33.469] 🔗 block reached canonical chain          number=6707 hash=c650c5…e9b2e7
INFO [02-09|16:09:33.469] 🔨 mined potential block                  number=6714 hash=fd71d0…8b4613
INFO [02-09|16:09:33.469] Commit new mining work                   number=6715 sealhash=d2a0c5…feef7f uncles=0 txs=0 gas=0 fees=0 elapsed=117.018µs
INFO [02-09|16:09:40.532] Successfully sealed new block            number=6715 sealhash=d2a0c5…feef7f hash=89d9be…895291 elapsed=7.062s
INFO [02-09|16:09:40.532] 🔗 block reached canonical chain          number=6708 hash=ba19e4…38b6ed
INFO [02-09|16:09:40.532] 🔨 mined potential block                  number=6715 hash=89d9be…895291
INFO [02-09|16:09:40.533] Commit new mining work                   number=6716 sealhash=8c7495…f32197 uncles=0 txs=0 gas=0 fees=0 elapsed=156.685µs
INFO [02-09|16:09:43.473] Successfully sealed new block            number=6716 sealhash=8c7495…f32197 hash=bfb07e…6fcafa elapsed=2.940s
INFO [02-09|16:09:43.473] 🔗 block reached canonical chain          number=6709 hash=e481c3…f9693d
INFO [02-09|16:09:43.473] 🔨 mined potential block                  number=6716 hash=bfb07e…6fcafa
INFO [02-09|16:09:43.473] Commit new mining work                   number=6717 sealhash=63dc28…ccda48 uncles=0 txs=0 gas=0 fees=0 elapsed=139.749µs
INFO [02-09|16:09:43.681] Successfully sealed new block            number=6717 sealhash=63dc28…ccda48 hash=e34f81…c8fee4 elapsed=207.575ms
INFO [02-09|16:09:43.681] 🔗 block reached canonical chain          number=6710 hash=03319b…88ddac
INFO [02-09|16:09:43.681] 🔨 mined potential block                  number=6717 hash=e34f81…c8fee4
INFO [02-09|16:09:43.681] Commit new mining work                   number=6718 sealhash=dc6abd…2e08c0 uncles=0 txs=0 gas=0 fees=0 elapsed=131.695µs
INFO [02-09|16:09:48.390] Successfully sealed new block            number=6718 sealhash=dc6abd…2e08c0 hash=d8b2b8…7be11b elapsed=4.709s
INFO [02-09|16:09:48.390] 🔗 block reached canonical chain          number=6711 hash=b9dc04…44932c
INFO [02-09|16:09:48.390] 🔨 mined potential block                  number=6718 hash=d8b2b8…7be11b
INFO [02-09|16:09:48.391] Commit new mining work                   number=6719 sealhash=35a0de…00b244 uncles=0 txs=0 gas=0 fees=0 elapsed=165.806µs
INFO [02-09|16:09:48.938] Successfully sealed new block            number=6719 sealhash=35a0de…00b244 hash=d777cd…6b85a5 elapsed=547.503ms
INFO [02-09|16:09:48.938] 🔗 block reached canonical chain          number=6712 hash=f5d972…79ee30
INFO [02-09|16:09:48.938] 🔨 mined potential block                  number=6719 hash=d777cd…6b85a5
INFO [02-09|16:09:48.938] Commit new mining work                   number=6720 sealhash=ebb4d5…d1fcb0 uncles=0 txs=0 gas=0 fees=0 elapsed=121.517µs
INFO [02-09|16:09:51.268] Successfully sealed new block            number=6720 sealhash=ebb4d5…d1fcb0 hash=20bb58…317c30 elapsed=2.329s
INFO [02-09|16:09:51.268] 🔗 block reached canonical chain          number=6713 hash=ff103c…e7f8e0
INFO [02-09|16:09:51.268] 🔨 mined potential block                  number=6720 hash=20bb58…317c30
INFO [02-09|16:09:51.268] Commit new mining work                   number=6721 sealhash=bfdadb…550757 uncles=0 txs=0 gas=0 fees=0 elapsed=150.088µs
INFO [02-09|16:09:54.897] Successfully sealed new block            number=6721 sealhash=bfdadb…550757 hash=dc72a0…9b74a4 elapsed=3.629s
INFO [02-09|16:09:54.897] 🔗 block reached canonical chain          number=6714 hash=fd71d0…8b4613
INFO [02-09|16:09:54.897] 🔨 mined potential block                  number=6721 hash=dc72a0…9b74a4
INFO [02-09|16:09:54.897] Commit new mining work                   number=6722 sealhash=73be42…bcfbf9 uncles=0 txs=0 gas=0 fees=0 elapsed=124.424µs
INFO [02-09|16:10:04.084] Successfully sealed new block            number=6722 sealhash=73be42…bcfbf9 hash=d9d661…73beea elapsed=9.186s
INFO [02-09|16:10:04.084] 🔗 block reached canonical chain          number=6715 hash=89d9be…895291
INFO [02-09|16:10:04.084] 🔨 mined potential block                  number=6722 hash=d9d661…73beea
INFO [02-09|16:10:04.084] Commit new mining work                   number=6723 sealhash=91f9ad…4107f4 uncles=0 txs=0 gas=0 fees=0 elapsed=131.926µs
INFO [02-09|16:10:04.450] Successfully sealed new block            number=6723 sealhash=91f9ad…4107f4 hash=39d875…4f7941 elapsed=366.059ms
INFO [02-09|16:10:04.450] 🔗 block reached canonical chain          number=6716 hash=bfb07e…6fcafa
INFO [02-09|16:10:04.450] 🔨 mined potential block                  number=6723 hash=39d875…4f7941

```






