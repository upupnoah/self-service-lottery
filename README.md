# Dacade-SuiMove-SelfServiceLottery

## 1 Entity Definition

- SELF_SERVICE_LOTTERY
- LotterySystem
- Lottery
- LotteryStub
- NewLotteryEvent
- WinEvent
- EndEvent

## 2 Entity Relationship && Economic Design

- use One-Time-Witness(`SELF_SERVICE_LOTTERY`) to create `Publisher`, who owned this object will charge 1% commission when the lottery draws.
- `LotterySystem` is a shared object, which stored detail infomation of `Lottery`.
- Everyone can create `Lottery` and customize selling prices, bonuses and other information.
- Everyone can purchase `Lottery` and get the corresponding `LotteryStub`.
- The lottery will be drawn automatically when the tickets are sold out, and anyone can have it drawn after the purchase period has expired.
- Winning users can hold the `LotteryStub` to redeem their prizes. At the same time, the income from the lottery will be transferred to the initiator's account. Of course, the publisher of the system will also receive a part of the commission.
- When a lottery ticket is not sold, or the redemption period has passed after the draw, you can choose to redeem the bonus, but the income is also real.
- `NewLotteryEvent`, `WinEvent`, `EndEvent` will trigger event announcements at key nodes.

## 3 API Definition

- **withdraw:** Publisher withdraws earnings.
- **create_lottery && create_lottery_with_epoch:** Create a new set of lottery tickets and customize the selling price and bonus. The difference between the two is whether the sale period is default.
- **fedeem_bonus:** Redeem the bonus, but the income is also real.
- **announcement:** The winning information will be announced after the draw.
- **buy_lottery:** When you pay a certain amount to purchase a lottery ticket, you will receive a corresponding voucher containing the prize redemption code.
- **redeem_lottery:** Prizes can be redeemed with vouchers after the draw.

## 4 Testing

## 4.1 publish

- **run command**

`sui client publish --gas-budget 100000000`

- **important outputs**

```bash
╭─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Object Changes                                                                                                          │
├─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Created Objects:                                                                                                        │
│  ┌──                                                                                                                    │
│  │ ObjectID: 0x469b2b4e2c59821d831e4726a73a74c1e117b80383eeae2041cf9b4ea242c0be                                         │
│  │ Sender: 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67                                           │
│  │ Owner: Account Address ( 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67 )                        │
│  │ ObjectType: 0x2::package::Publisher                                                                                  │
│  │ Version: 28132105                                                                                                    │
│  │ Digest: H9s7atWdJs4vG7YLTyFvUHqkMnBXQ1rQ2gTBsNKgfjPj                                                                 │
│  └──                                                                                                                    │
│  ┌──                                                                                                                    │
│  │ ObjectID: 0xdb674c063a7c4e3270d6b558adf3feb333da3498c044801d3d4680361ad077f1                                         │
│  │ Sender: 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67                                           │
│  │ Owner: Account Address ( 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67 )                        │
│  │ ObjectType: 0x2::package::UpgradeCap                                                                                 │
│  │ Version: 28132105                                                                                                    │
│  │ Digest: 9cjzK99qYszLtcLLYPN4t1GdVuWZ6piips62AkLP7QLq                                                                 │
│  └──                                                                                                                    │
│  ┌──                                                                                                                    │
│  │ ObjectID: 0xf430c82e627840a1c98439565974de87c1078b4be5014843f69d2702c1ae270f                                         │
│  │ Sender: 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67                                           │
│  │ Owner: Shared( 28132105 )                                                                                            │
│  │ ObjectType: 0xd57f516962ac634529d9a8005812462bce04cc89b457b566232dd818ab2aa9bd::self_service_lottery::LotterySystem  │
│  │ Version: 28132105                                                                                                    │
│  │ Digest: AxJJHX3tsPP3QCLbduZkGfZbx9vxtkHRpv8YSbMGYaSz                                                                 │
│  └──                                                                                                                    │
│ Mutated Objects:                                                                                                        │
│  ┌──                                                                                                                    │
│  │ ObjectID: 0x01676de212960b0689245914312ac6be3b4d5cffa0cae91ef527441b894f746a                                         │
│  │ Sender: 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67                                           │
│  │ Owner: Account Address ( 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67 )                        │
│  │ ObjectType: 0x2::coin::Coin<0x2::sui::SUI>                                                                           │
│  │ Version: 28132105                                                                                                    │
│  │ Digest: 4DLokvD6fC9WndtSz1eqDsp1xd9sBaxi5oLTXB9ZzBpk                                                                 │
│  └──                                                                                                                    │
│ Published Objects:                                                                                                      │
│  ┌──                                                                                                                    │
│  │ PackageID: 0xd57f516962ac634529d9a8005812462bce04cc89b457b566232dd818ab2aa9bd                                        │
│  │ Version: 1                                                                                                           │
│  │ Digest: 8MZ5RzHENjhzxKasWX4Ut1aHRFvFvjTHssSGurqfojTv                                                                 │
│  │ Modules: self_service_lottery                                                                                        │
│  └──                                                                                                                    │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```

- **record ID**

```bash
export PACKAGE=0xd57f516962ac634529d9a8005812462bce04cc89b457b566232dd818ab2aa9bd
export PUBLISHER=0x469b2b4e2c59821d831e4726a73a74c1e117b80383eeae2041cf9b4ea242c0be
export LOTTERYSYSTEM=0xf430c82e627840a1c98439565974de87c1078b4be5014843f69d2702c1ae270f

sui client gas
# output:
╭────────────────────────────────────────────────────────────────────┬────────────────────┬──────────────────╮
│ gasCoinId                                                          │ mistBalance (MIST) │ suiBalance (SUI) │
├────────────────────────────────────────────────────────────────────┼────────────────────┼──────────────────┤
│ 0x01676de212960b0689245914312ac6be3b4d5cffa0cae91ef527441b894f746a │ 2781685426         │ 2.78             │
│ 0x4138ff0b0ff27eeb46fcfb24da66059bb013e0bc05e39f47eea9dd969cff4d67 │ 1000000000         │ 1.00             │
│ 0x9b6a8d50f03bd3957e6fb5248bbc4e530f327fc4e42c8dfb27eafb2e9f45f093 │ 1000000000         │ 1.00             │
╰────────────────────────────────────────────────────────────────────┴────────────────────┴──────────────────╯

export COIN=0x4138ff0b0ff27eeb46fcfb24da66059bb013e0bc05e39f47eea9dd969cff4d67
```

## 4.2 create_lottery

- **run command**

`sui client call --package $PACKAGE --module self_service_lottery --function create_lottery --args $LOTTERYSYSTEM "TestLottery" 500000000 2 $COIN --gas-budget 100000000`

- **importand outputs**

```bash
╭─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Transaction Block Events                                                                                                │
├─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│  ┌──                                                                                                                    │
│  │ EventID: 7z4J6fGGdhEXj621mezkKwcJs1Qun4smHRaTqc9Uv3cF:0                                                              │
│  │ PackageID: 0xd57f516962ac634529d9a8005812462bce04cc89b457b566232dd818ab2aa9bd                                        │
│  │ Transaction Module: self_service_lottery                                                                             │
│  │ Sender: 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67                                           │
│  │ EventType: 0xd57f516962ac634529d9a8005812462bce04cc89b457b566232dd818ab2aa9bd::self_service_lottery::NewLotteryEvent │
│  │ ParsedJSON:                                                                                                          │
│  │   ┌──────────────┬────────────────────────────────────────────────────────────────────┐                              │
│  │   │ bonus_value  │ 1000000000                                                         │                              │
│  │   ├──────────────┼────────────────────────────────────────────────────────────────────┤                              │
│  │   │ end_epoch    │ 397                                                                │                              │
│  │   ├──────────────┼────────────────────────────────────────────────────────────────────┤                              │
│  │   │ lottery_id   │ 0x4e18914e22f53858dff84c0d1496c8b7df70ff6015b3d7a4a673b8aa690c43b6 │                              │
│  │   ├──────────────┼────────────────────────────────────────────────────────────────────┤                              │
│  │   │ lottery_name │ TestLottery                                                        │                              │
│  │   ├──────────────┼────────────────────────────────────────────────────────────────────┤                              │
│  │   │ price        │ 500000000                                                          │                              │
│  │   ├──────────────┼────────────────────────────────────────────────────────────────────┤                              │
│  │   │ total_amount │ 2                                                                  │                              │
│  │   └──────────────┴────────────────────────────────────────────────────────────────────┘                              │
│  └──                                                                                                                    │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```

- **record ID**

```bash
export LOTTERY=0x4e18914e22f53858dff84c0d1496c8b7df70ff6015b3d7a4a673b8aa690c43b6

sui client gas
# output:
╭────────────────────────────────────────────────────────────────────┬────────────────────┬──────────────────╮
│ gasCoinId                                                          │ mistBalance (MIST) │ suiBalance (SUI) │
├────────────────────────────────────────────────────────────────────┼────────────────────┼──────────────────┤
│ 0x01676de212960b0689245914312ac6be3b4d5cffa0cae91ef527441b894f746a │ 2778534778         │ 2.77             │
│ 0x9b6a8d50f03bd3957e6fb5248bbc4e530f327fc4e42c8dfb27eafb2e9f45f093 │ 1000000000         │ 1.00             │
╰────────────────────────────────────────────────────────────────────┴────────────────────┴──────────────────╯

export COIN=0x9b6a8d50f03bd3957e6fb5248bbc4e530f327fc4e42c8dfb27eafb2e9f45f093
```

## 4.3 buy_lottery

- **run command**

`sui client call --package $PACKAGE --module self_service_lottery --function buy_lottery --args $LOTTERYSYSTEM $LOTTERY $COIN --gas-budget 100000000`

- **important outputs**

```bash
╭───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Object Changes                                                                                                                                                │
├───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Created Objects:                                                                                                                                              │
│  ┌──                                                                                                                                                          │
│  │ ObjectID: 0x5a482ff5935840c89728184c68c478bead87a866f5b6bfdbbbf5da96f65c7dc3                                                                               │
│  │ Sender: 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67                                                                                 │
│  │ Owner: Account Address ( 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67 )                                                              │
│  │ ObjectType: 0xd57f516962ac634529d9a8005812462bce04cc89b457b566232dd818ab2aa9bd::self_service_lottery::LotteryStub                                          │
│  │ Version: 28132107                                                                                                                                          │
│  │ Digest: DpT2d3oC4iJzqUFbWg93GZNKm1hVDMekWoh5jCos9cCp                                                                                                       │
│  └──                                                                                                                                                          │
│ Mutated Objects:                                                                                                                                              │
│  ┌──                                                                                                                                                          │
│  │ ObjectID: 0x01676de212960b0689245914312ac6be3b4d5cffa0cae91ef527441b894f746a                                                                               │
│  │ Sender: 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67                                                                                 │
│  │ Owner: Account Address ( 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67 )                                                              │
│  │ ObjectType: 0x2::coin::Coin<0x2::sui::SUI>                                                                                                                 │
│  │ Version: 28132107                                                                                                                                          │
│  │ Digest: 2M5DBUCvu9hfyGXZunSqdiE6VrBHK7Q6i6Yeq8SC1rRz                                                                                                       │
│  └──                                                                                                                                                          │
│  ┌──                                                                                                                                                          │
│  │ ObjectID: 0x33ac04798ba0c6fca92804d42f579baad53bae331a097bbde809c4af2a0a33ae                                                                               │
│  │ Sender: 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67                                                                                 │
│  │ Owner: Object ID: ( 0x2643e8a8fe0b861ee1d8fad4cd5ddeffd40df3792303975ce6847a9108dbbdd8 )                                                                   │
│  │ ObjectType: 0x2::dynamic_field::Field<0x2::object::ID, 0xd57f516962ac634529d9a8005812462bce04cc89b457b566232dd818ab2aa9bd::self_service_lottery::Lottery>  │
│  │ Version: 28132107                                                                                                                                          │
│  │ Digest: 8uVWwgUJMG1LxWdhpTUXYxdGGdwTRfpKxPfTvU2Vs5MK                                                                                                       │
│  └──                                                                                                                                                          │
│  ┌──                                                                                                                                                          │
│  │ ObjectID: 0x9b6a8d50f03bd3957e6fb5248bbc4e530f327fc4e42c8dfb27eafb2e9f45f093                                                                               │
│  │ Sender: 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67                                                                                 │
│  │ Owner: Account Address ( 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67 )                                                              │
│  │ ObjectType: 0x2::coin::Coin<0x2::sui::SUI>                                                                                                                 │
│  │ Version: 28132107                                                                                                                                          │
│  │ Digest: 56EMyGyKoGSKEhcyb7EHF4AtMQ1kRGSw3osBNRQwsPh                                                                                                        │
│  └──                                                                                                                                                          │
│  ┌──                                                                                                                                                          │
│  │ ObjectID: 0xf430c82e627840a1c98439565974de87c1078b4be5014843f69d2702c1ae270f                                                                               │
│  │ Sender: 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67                                                                                 │
│  │ Owner: Shared( 28132105 )                                                                                                                                  │
│  │ ObjectType: 0xd57f516962ac634529d9a8005812462bce04cc89b457b566232dd818ab2aa9bd::self_service_lottery::LotterySystem                                        │
│  │ Version: 28132107                                                                                                                                          │
│  │ Digest: BdNzqt5Uimo7dQtp5UDjh371YuUR9WS1JN5AZrZMGymX                                                                                                       │
│  └──                                                                                                                                                          │
╰───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```

- **record ID**

`export LOTTERYSTUB1=0x5a482ff5935840c89728184c68c478bead87a866f5b6bfdbbbf5da96f65c7dc3`

Similarly, buy another one and set `export LOTTERYSTUB2=0xdd5b6a281e34104c3a9b3671ebe8fce770b68d75222a0b8844214972e9435ab5`<br>At this time, because the lottery tickets are sold out, the lottery is automatically triggered. You can see the lottery information from the $\mathit {Event}$ information:

```bash
╭──────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Transaction Block Events                                                                                         │
├──────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│  ┌──                                                                                                             │
│  │ EventID: FC812jAiEHLaNTtS66WRS9DQrxnGqa1bR81y7AHknNLh:0                                                       │
│  │ PackageID: 0xd57f516962ac634529d9a8005812462bce04cc89b457b566232dd818ab2aa9bd                                 │
│  │ Transaction Module: self_service_lottery                                                                      │
│  │ Sender: 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67                                    │
│  │ EventType: 0xd57f516962ac634529d9a8005812462bce04cc89b457b566232dd818ab2aa9bd::self_service_lottery::WinEvent │
│  │ ParsedJSON:                                                                                                   │
│  │   ┌──────────────┬──────────────────────────────────────────────┐                                             │
│  │   │ lottery_name │ TestLottery                                  │                                             │
│  │   ├──────────────┼──────────────────────────────────────────────┤                                             │
│  │   │ winner_code  │ rbaG/MO6rqDo0Ad/lK79EACIDTbKMhb6bSL3MkllhRc= │                                             │
│  │   └──────────────┴──────────────────────────────────────────────┘                                             │
│  └──                                                                                                             │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```

## 4.4 redeem_lottery

- **run command**

`sui client call --package $PACKAGE --module self_service_lottery --function redeem_lottery --args $LOTTERYSYSTEM $LOTTERYSTUB1 --gas-budget 100000000`

There is no trigger event information, but through $\mathit {Object\ Changes}$ you can find $\mathit {SUI}$ changes, so type `sui client gas` to verify:

```bash
╭────────────────────────────────────────────────────────────────────┬────────────────────┬──────────────────╮
│ gasCoinId                                                          │ mistBalance (MIST) │ suiBalance (SUI) │
├────────────────────────────────────────────────────────────────────┼────────────────────┼──────────────────┤
│ 0x01676de212960b0689245914312ac6be3b4d5cffa0cae91ef527441b894f746a │ 2775506430         │ 2.77             │
│ 0x9bb06c48c6173af94ba38f41a7ddba227451abfdb4356e68851ba8497cfeca05 │ 1000000000         │ 1.00             │
│ 0xe9a9be9af022aa5846d4549a6d97200dcebe576561beaa025a51cdbd84e9c361 │ 990000000          │ 0.99             │
╰────────────────────────────────────────────────────────────────────┴────────────────────┴──────────────────╯
```

At this time, if a second lottery voucher is used to redeem the prize, an event reminder will be triggered, and at the same time, the voucher will be destroyed:

```bash
╭──────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Transaction Block Events                                                                                         │
├──────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│  ┌──                                                                                                             │
│  │ EventID: 7eW7EgHkvtuhX6U2JGN3DjsedATNatcVpfttmFNNXD3:0                                                        │
│  │ PackageID: 0xd57f516962ac634529d9a8005812462bce04cc89b457b566232dd818ab2aa9bd                                 │
│  │ Transaction Module: self_service_lottery                                                                      │
│  │ Sender: 0x9e4092b6a894e6b168aa1c6c009f5c1c1fcb83fb95e5aa39144e1d2be4ee0d67                                    │
│  │ EventType: 0xd57f516962ac634529d9a8005812462bce04cc89b457b566232dd818ab2aa9bd::self_service_lottery::EndEvent │
│  │ ParsedJSON:                                                                                                   │
│  │   ┌──────┬────────────────────────────────────────────────────────────────┐                                   │
│  │   │ hint │ You have not won a prize or the redemption period has expired! │                                   │
│  │   └──────┴────────────────────────────────────────────────────────────────┘                                   │
│  └──                                                                                                             │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```

## 4.5 withdraw

- **run command**

`sui client call --package $PACKAGE --module self_service_lottery --function withdraw --args $PUBLISHER $LOTTERYSYSTEM --gas-budget 100000000`

- **verify**

```bash
sui client gas

# output:
╭────────────────────────────────────────────────────────────────────┬────────────────────┬──────────────────╮
│ gasCoinId                                                          │ mistBalance (MIST) │ suiBalance (SUI) │
├────────────────────────────────────────────────────────────────────┼────────────────────┼──────────────────┤
│ 0x01676de212960b0689245914312ac6be3b4d5cffa0cae91ef527441b894f746a │ 2774346382         │ 2.77             │
│ 0x9bb06c48c6173af94ba38f41a7ddba227451abfdb4356e68851ba8497cfeca05 │ 1000000000         │ 1.00             │
│ 0xd107cdb05b93da5262fc2b5b9f03f9aa60539555303a1cf2ee935f1087787bee │ 10000000           │ 0.01             │
│ 0xe9a9be9af022aa5846d4549a6d97200dcebe576561beaa025a51cdbd84e9c361 │ 990000000          │ 0.99             │
╰────────────────────────────────────────────────────────────────────┴────────────────────┴──────────────────╯
```

Through simple calculation, it can be found that it meets the prior expectations.

## 5 Disclaimer

This project is for learning purposes only.<br>The code logic and testing are still imperfect and unsafe.<br>If you want to use it for commercial purposes, please bear the possible consequences.
