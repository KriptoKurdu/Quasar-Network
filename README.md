# Quasar-Network


### Sistem Gereksinimleri

**CPU:** 4 CPU

**RAM:** 16 GB

**SSD:** 200 GB

**OS:** Ubuntu 20.04




### Moniker adı belirle
```
MONIKER="monikerAd"
```

### Kurulum

```
source <(curl -s https://raw.githubusercontent.com/KriptoKurdu/Quasar-Network/main/quasar.sh)
```



Senkronizasyon kontrol
```
quasarnoded status 2>&1 | jq .SyncInfo
```
### Blok kontrol

[Explorer](https://testnet.ping.pub/quasar)


### Cüzdan ekleme

```
quasard keys add wallet
```
### Faucet

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
### Delege etme    
 ```   
quasard tx staking delegate <TO_VALOPER_ADDRESS> 1000000uqsr --from wallet --chain-id qsr-questnet-04 --gas-adjustment 1.4 --gas auto --gas-prices 0uqsr -y    
    
   ``` 


