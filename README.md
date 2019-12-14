# setrex multisig

This document describes the preparation on the southafrica1 setrex multisig. This multisig uses the eosio::setrex action to update the total_rent field in the rexpool table from its current value of approximately 20000 TLOS to 100000 TLOS. 

Currently you will receive approximately 3000 TLOS for each TLOS rent paid. If REX borrowing reaches 80% of total_lendable the telos received drops to approximately 120 TLOS.

The effect of this change is to increase the cost of borrowing from REX by about 5x. After the change you will receive approximately 600 TLOS for each TLOS rent paid. If REX borrowing reaches 80% of total_lendable the telos received drops to approximately 25 TLOS.

Figures quoted are approximate because REX is a live system and prices change dynamically as purchased are made. The precise price resulting from the execution of the setrex action will be affected by the state of REX when it is executed.

If a large number of TLOS are borrowed through REX before this multisig is executed the result will be a lower price increase than expected. The result will however always be a price increase. The price will not inadvertently drop because of a major change in the state or REX.

# Multisig generation and proposal

## API

The multisig was prepared and proposed using the following API point.

```bash
API="--url https://api.telos.africa"
```

## Transaction

The transaction was prepared using the following cleos command.

```
cleos $API push action -sjd eosio setrex '["100000.0000 TLOS"]' -p eosio@active > trx.json
```

After running, the following manual edits were made to trx.json;

```json
  "expiration": "2019-12-21T16:30:51",
  "ref_block_num": 0,
  "ref_block_prefix": 0,
```

## Signatures

All Telos active and standby block producers were included in the multisig. The signatories.json file lists all signatories.

## Propose

The multisig was proposed using the following command.

```
cleos $API multisig propose_trx setrex signatories.json trx.json southafrica1 -p southafrica1@active
```

## Review

The multisig can be reviewed using;

```
cleos $API multisig review southafrica1 setrex 
```

Alternatively, it can be viewed on bloks.io at

https://telos.bloks.io/msig/southafrica1/setrex

## Approve

The multisig can be approves using;

```
cleos multisig approve southafrica1 setrex '{"actor": "<youraccount>", "permission": "active"}' -p <youraccount>@active
```

## Additional background information

Background details of this proposal may be found in the following medium post;

https://medium.com/@eoszaio/improving-eosio-resource-allocation-9902180be879
