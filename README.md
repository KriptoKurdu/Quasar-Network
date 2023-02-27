# Quasar-Network


### Kurulum

```
source <(curl -s https://raw.githubusercontent.com/KriptoKurdu/Quasar-Network/main/quasar.sh?token=GHSAT0AAAAAAB6LGPTX54GCNZYHADKMALSSY74WHUA)
```



Senkronizasyon kontrol
```
quasarnoded status 2>&1 | jq .SyncInfo
```
## Blok kontrol

[Explorer](https://testnet.ping.pub/quasar)


### Cüzdan ekleme

```
quasard keys add wallet
```
## Faucet

[Discord](https://discord.gg/quasarfi)

### Validator olusturma
```
quasard tx staking create-validator \
--amount=1000000uqsr \
--pubkey=$(quasard tendermint show-validator) \
--moniker="$NODE_MONIKER" \
--chain-id=qsr-questnet-04 \
--commission-rate=0.1 \
--commission-max-rate=0.2 \
--commission-max-change-rate=0.05 \
--min-self-delegation=1 \
--from=wallet \
-y
  ```
    
    
    
    


