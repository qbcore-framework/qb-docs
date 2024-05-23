---
description: Keep your money safe and quickly access!
---

# 🏦 qb-banking

## Introduction

* Multiple ATM's & banks around the map to interact with
* Handles all player interaction with bank/job/gang/shared accounts
* ATM and bank card integration
* Shared accounts between players
* Auto creation of job/gang accounts on bank first open
* Boss-only access to job/gang accounts

## CreatePlayerAccount

Creates a new shared account for a player and returns where it was successful or not

```lua
exports['qb-banking']:CreatePlayerAccount(playerId, accountName, accountBalance, accountUsers)
```

* playerId: `number`
* accountName: `string`
* accountBalance: `number`
* accountUsers: `table`
* returns: `boolean`

```lua
RegisterCommand('createPlayerAccount', function(source)
    local playerId = source
    local accountName = 'My Shared Account'
    local accountBalance = 5000
    local accountUsers = {'LCC00307', 'LCC00308'} -- list of citizenid's
    exports['qb-banking']:CreatePlayerAccount(playerId, accountName, accountBalance, json.encode(accountUsers))
end, true)
```

## CreateJobAccount

Creates a new job type account, this is automatically done so shouldn't need this

```lua
exports['qb-banking']:CreateJobAccount(accountName, accountBalance)
```

* accountName: `string`
* accountBalance: `number`

#### Example:

```lua
RegisterCommand('createJobAccount', function()
    local accountName = 'police'
    local accountBalance = 10000
    exports['qb-banking']:CreateJobAccount(accountName, accountBalance)
end, true)
```

## CreateGangAccount

Creates a new gang type account, this is automatically done so shouldn't need this

```lua
exports['qb-banking']:CreateGangAccount(accountName, accountBalance)
```

* accountName: `string`
* accountBalance: `number`

#### Example:

```lua
RegisterCommand('createGangAccount', function()
    local accountName = 'ballas'
    local accountBalance = 10000
    exports['qb-banking']:CreateGangAccount(accountName, accountBalance)
end, true)
```

## AddMoney

Adds money to an account by name and returns where it was successful or not

```lua
exports['qb-banking']:AddMoney(accountName, amount, reason)
```

* accountName: `string`
* amount: `number`
* <mark style="color:yellow;">reason</mark>: `string`
* returns: `boolean`

```lua
RegisterCommand('addMoney', function()
    local accountName = 'police'
    local amount = 10000
    exports['qb-banking']:AddMoney(accountName, amount, 'test example')
end, true)
```

## RemoveMoney

Removes money from an account by name and returns where it was successful or not

```lua
exports['qb-banking']:RemoveMoney(accountName, amount, reason)
```

* accountName: `string`
* amount: `number`
* <mark style="color:yellow;">reason</mark>: `string`
* returns: `boolean`

```lua
RegisterCommand('removeMoney', function()
    local accountName = 'police'
    local amount = 10000
    exports['qb-banking']:RemoveMoney(accountName, amount, 'test example')
end, true)
```

## GetAccount

Returns all the information for the specified account by name

```lua
exports['qb-banking']:GetAccount(accountName)
```

* accountName: `string`
* returns: `table | nil`

```lua
RegisterCommand('getAccount', function()
    local accountName = 'police'
    local accountInfo = exports['qb-banking']:GetAccount(accountName)
    if not accountInfo then print('Account '..accountName..' does not exist') return end
    for _, info in pairs(accountInfo) do
        print('Account Name: '..info.account_name)
        print('Account Balance: '..info.account_balance)
        print('Account Type: '..info.account_type)
    end
end, true)
```

## GetAccountBalance

Returns just the balance of the specified account by name

```lua
exports['qb-banking']:GetAccountBalance(accountName)
```

* accountName: `string`
* returns: `number`

```lua
RegisterCommand('getBalance', function()
    local accountName = 'police'
    local balance = exports['qb-banking']:GetAccountBalance(accountName)
    print('Account: '..accountName..' Balance: '..balance)
end, true)
```

## CreateBankStatement

This will create a statement for a specified account and returns where it was successful or not

```lua
exports['qb-banking']:CreateBankStatement(playerId, account, amount, reason, statementType, accountType)
```

* playerId: `number`
* account: `string`
* amount: `number`
* reason: `string`
* statementType: `string`
* accountType: `string`
* returns: `boolean`

```lua
RegisterCommand('createBankStatement', function(source)
    local playerId = source
    local account = 'My Shared Account'
    local amount = 5000
    local reason = 'Removed money'
    local statementType = 'withdraw' -- deposit
    local accountType = 'shared' -- 'player', 'job', 'gang'
    local statementCreated = exports['qb-banking']:CreateBankStatement(playerId, account, amount, reason, statementType, accountType)
    if statementCreated then print('Statement Created') return end
    print('Error creating statement')
end, true)
```
