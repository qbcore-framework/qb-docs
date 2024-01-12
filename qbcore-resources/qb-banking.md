---
description: Keep your money safe and quickly access!
---

# 🏦 qb-banking

## Introduction

* Multiple ATM's & banks around the map to interact with.
* Shared accounts & debit cards

## Preview

![](https://camo.githubusercontent.com/66e8f478098a6ff4458fef951745f16d18281c648a72259a13e40082c3f638ee/68747470733a2f2f692e696d6775722e636f6d2f58617a615959492e706e67)

### Features

* Handles all player interaction with bank/job/gang/shared accounts
* ATM and bank card integration
* Shared accounts between players
* Auto creation of job/gang accounts on bank first open
* Boss-only access to job/gang accounts

### Exports

```lua
exports['qb-banking']:ExportName() -- replace export name with desired from below and needed arguments
```

#### CreatePlayerAccount

Creates a new shared account for a player

```lua
    CreatePlayerAccount(
        playerId, -- id of the player account is being created for
        accountName, -- name of the account, must be a string
        accountBalance, -- balance of the account on creation, must be a number
        json.encode({'LCC00307', 'LCC00308'}) -- table of users on account by citizenid
    )
```

#### CreateJobAccount

Creates a new job type account, this is automatically done so shouldn't need this

```lua
    CreateJobAccount(
        accountName, -- name of the account, must be a string
        accountBalance, -- balance of the account on creation, must be a number
    )
```

#### CreateGangAccount

Creates a new gang type account, this is automatically done so shouldn't need this

```lua
    CreateGangAccount(
        accountName, -- name of the account, must be a string
        accountBalance, -- balance of the account on creation, must be a number
    )
```

#### AddMoney

Adds money to an account by name, checks for regular account first If playerId is provided and a regular account isn't found then it will check for shared account

```lua
    AddMoney(
        accountName, -- name of the account, must be a string
        accountBalance, -- balance of the account on creation, must be a number
        reason -- optional, must be a string
    )
```

#### RemoveMoney

Removes money from an account by name, checks for regular account first If playerId is provided and a regular account isn't found then it will check for shared account

```lua
    RemoveMoney(
        accountName, -- name of the account, must be a string
        accountBalance, -- balance of the account on creation, must be a number
        reason -- optional, must be a string
    )
```

#### GetAccount

Returns all the information for the specified account by name

```lua
    GetAccount(
        accountName, -- name of the account
    )
```

#### GetAccountBalance

Returns just the balance of the specified account by name

```lua
    GetAccountBalance(
        accountName, -- name of the account
    )
```

#### CreateBankStatement

This will create a statement for a specified account

```lua
    CreateBankStatement(
        playerId, -- id of the player to create the statement for
        account, -- name of the shared account, must be a string
        amount, -- amount of the transaction, must be a number
        reason, -- reason for the transaction , must be a string
        statementType, -- type of statement, must be a string 'withdraw' or 'deposit'
        accountType -- type of account, must be a string 'player', 'shared', 'job', 'gang'
    )
```
