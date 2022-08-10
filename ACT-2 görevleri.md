# Vortex, Sei Network üzerinde ki ilk protocol ve testnet.

Testnete katılmanız için node kurmanız "gerekmiyor"

Görev listesi:https://3pgv.notion.site/b7a73a18ef444b9483b5601bf833bae8?v=9111c2c97f2842c5aa75b8d5e5b00a1e

Ödüllü testnet ve Sei ACT-2 görevlerini kapsıyor..

## Place multiple Long/Short orders in one transaction (bundled order placement) in any market on Vortex. Currently this needs to be done via CLI
görevi için aşağıdaki kodları çalıştıracağız. cüzdan adresi yazan yere sei cüzdan adresinizi yazın.

```
echo '{
  "body": {
    "messages": [
      {
        "@type": "/seiprotocol.seichain.dex.MsgPlaceOrders",
        "creator": "sei1t36rv96q35dkhratcu2q73rpka3ryutze4vtlw",
        "orders": [
          {
            "id": "0",
            "status": "PLACED",
            "account": "cüzdanadresiniz",
            "contractAddr": "sei14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9sh9m79m",
            "price": "1.000000000000000000",
            "quantity": "0.000010000000000000",
            "priceDenom": "USDC",
            "assetDenom": "ATOM",
            "orderType": "LIMIT",
            "positionDirection": "SHORT",
            "data": "{\"position_effect\":\"Open\",\"leverage\":\"1\"}",
            "statusDescription": ""
          }
        ],
        "contractAddr": "sei14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9sh9m79m",
        "funds": [
          {
            "denom": "uusdc",
            "amount": "10"
          }
        ],
        "autoCalculateDeposit": false
      },
      {
        "@type": "/seiprotocol.seichain.dex.MsgPlaceOrders",
        "creator": "cüzdanadresiniz",
        "orders": [
          {
            "id": "0",
            "status": "PLACED",
            "account": "cüzdanadresiniz",
            "contractAddr": "sei14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9sh9m79m",
            "price": "1.000000000000000000",
            "quantity": "0.000010000000000000",
            "priceDenom": "USDC",
            "assetDenom": "ATOM",
            "orderType": "LIMIT",
            "positionDirection": "SHORT",
            "data": "{\"position_effect\":\"Open\",\"leverage\":\"1\"}",
            "statusDescription": ""
          }
        ],
        "contractAddr": "sei14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9sh9m79m",
        "funds": [
          {
            "denom": "uusdc",
            "amount": "10"
          }
        ],
        "autoCalculateDeposit": false
      }
    ],
    "memo": "",
    "timeout_height": "0",
    "extension_options": [],
    "non_critical_extension_options": []
  },
  "auth_info": {
    "signer_infos": [],
    "fee": {
      "amount": [
        {
          "denom": "usei",
          "amount": "0"
        }
      ],
      "gas_limit": "0",
      "payer": "",
      "granter": ""
    }
  },
  "signatures": []
}' > $HOME/gen_tx.json
```
cüzdan adresi yazan yere sei cüzdan adresinizi yazın.
```
ACC=$(seid q account cüzdanadresi -o json | jq -r .account_number)
```
cüzdan adresi yazan yere sei cüzdan adresinizi yazın.
```
seq=$(seid q account cüzdanadresi -o json | jq -r .sequence)
```
cüzdan yazan yerde cüzdan isminiz girin
```
seid tx sign $HOME/gen_tx.json -s $seq -a $ACC --offline \
--from cuzdan --chain-id atlantic-1 \
--output-document $HOME/txs.json
```

```
seid tx broadcast $HOME/txs.json
```
