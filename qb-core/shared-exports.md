---
description: Learn how to use exports to update the shared dynamically!
---

# ↗ Shared Exports

<table><thead><tr><th>Function or Event</th><th width="150" align="center">Scope</th><th width="206.79646017699116" align="center">Description</th><th align="center">returns</th></tr></thead><tbody><tr><td>exports['qb-core']:AddItem(itemName, item)</td><td align="center">Server</td><td align="center">Accepts an item name and item object - will add new entry to QBCore.Shared.Items</td><td align="center">boolean, string</td></tr><tr><td>exports['qb-core']:AddJob(jobName, job)</td><td align="center">Server</td><td align="center">Accepts an job name and job object - will add new entry to QBCore.Shared.Jobs</td><td align="center">boolean, string</td></tr><tr><td>exports['qb-core']:AddGang(gangName, gang)</td><td align="center">Server</td><td align="center">Accepts an gang name and gang object - will add new entry to QBCore.Shared.Gangs</td><td align="center">boolean, string</td></tr><tr><td>exports['qb-core']:AddItems(items)</td><td align="center">Server</td><td align="center">Accepts a table or array - will loop through the table and add new entries to QBCore.Shared.Items</td><td align="center">boolean, string, errorItem</td></tr><tr><td>exports['qb-core']:AddJobs(jobs)</td><td align="center">Server</td><td align="center">Accepts a table or array - will loop through the table and add new entries to QBCore.Shared.Jobs</td><td align="center">boolean, string, errorItem</td></tr><tr><td>exports['qb-core']:AddGangs(gangs)</td><td align="center">Server</td><td align="center">Accepts a table or array - will loop through the table and add new entries to QBCore.Shared.Gangs</td><td align="center">boolean, string, errorItem</td></tr><tr><td>QBCore.Functions.AddItem(itemName, item)</td><td align="center">Server</td><td align="center">Accepts an item name and item object - will add new entry to QBCore.Shared.Items</td><td align="center">boolean, string</td></tr><tr><td>QBCore.Functions.AddJob(jobName, Job)</td><td align="center">Server</td><td align="center">Accepts an job name and job object - will add new entry to QBCore.Shared.Jobs</td><td align="center">boolean, string</td></tr><tr><td>QBCore.Functions.AddGang(gangName, gang)</td><td align="center">Server</td><td align="center">Accepts an gang name and gang object - will add new entry to QBCore.Shared.Gangs</td><td align="center">boolean, string</td></tr><tr><td>QBCore.Functions.AddItems(items)</td><td align="center">Server</td><td align="center">Accepts a table or array - will loop through the table and add new entries to QBCore.Shared.Items</td><td align="center">boolean, string, errorItem</td></tr><tr><td>QBCore.Functions.AddJobs(jobs)</td><td align="center">Server</td><td align="center">Accepts a table or array - will loop through the table and add new entries to QBCore.Shared.Jobs</td><td align="center">boolean, string, errorItem</td></tr><tr><td>QBCore.Functions.AddGangs(gangs)</td><td align="center">Server</td><td align="center">Accepts a table or array - will loop through the table and add new entries to QBCore.Shared.Gangs</td><td align="center">boolean, string, errorItem</td></tr><tr><td>TriggerServerEvent('QBCore:Sever:UpdateObject')</td><td align="center">Server</td><td align="center">Accepts nothing - used to update the core object (PLEASE USE THE BELOW EXAMPLE)</td><td align="center">none</td></tr><tr><td>TriggerClientEvent('QBCore:Client:UpdateObject')</td><td align="center">Client</td><td align="center">Accepts nothing - used to update the core object (PLEASE USE THE BELOW EXAMPLE)</td><td align="center">none</td></tr></tbody></table>

## Import Jobs

* This method allows for any resource to insert job data into the shared file for the core. That means that you can make a resource, and on load, make those jobs available for use. This can be accomplished through one the ways shown below. Utilizing the function requires importing the core but using the export does not

{% hint style="danger" %}
Read over and learn the [shared.md](shared.md "mention") structure before attempting to use these
{% endhint %}

{% hint style="warning" %}
You must add this code to the client-side file of your resource when using these if you need the core object!
{% endhint %}

```lua
RegisterNetEvent('QBCore:Client:UpdateObject', function()
	QBCore = exports['qb-core']:GetCoreObject()
end)
```

{% hint style="warning" %}
You must add this code to the server-side file of your resource when using these if you need the core object!
{% endhint %}

```lua
RegisterNetEvent('QBCore:Server:UpdateObject', function()
	if source ~= '' then return false end
	QBCore = exports['qb-core']:GetCoreObject()
end)
```

### QBCore.Functions.AddJob

```lua
QBCore.Functions.AddJob(jobName --[[string]], job --[[table]])

-- Example
QBCore.Functions.AddJob('unemployed', {
    label = 'Civilian',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = {
            name = 'Freelancer',
            payment = 10
        }
    }
})
```

### exports\['qb-core']:AddJob

```lua
exports['qb-core']:AddJob(jobName --[[string]], job --[[table]])

-- Example
exports['qb-core']:AddJob('unemployed', {
    label = 'Civilian',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = {
            name = 'Freelancer',
            payment = 10
        }
    }
})
```

### QBCore.Functions.AddJobs

```lua
QBCore.Functions.AddJobs(jobs --[[table]])

-- Example
QBCore.Functions.AddJobs({
    ['unemployed'] = {
        label = 'Civilian',
        defaultDuty = true,
        offDutyPay = false,
        grades = {
            ['0'] = {
                name = 'Freelancer',
                payment = 10
        }
    },
    ['trucker'] = {
	label = 'Trucker',
	defaultDuty = true,
	offDutyPay = false,
	grades = {
            ['0'] = {
                name = 'Driver',
                payment = 50
        }
    }
})
```

### exports\['qb-core']:AddJobs

```lua
exports['qb-core']:AddJobs(jobs --[[table]])

-- Example
exports['qb-core']:AddJobs({
    ['unemployed'] = {
        label = 'Civilian',
        defaultDuty = true,
        offDutyPay = false,
        grades = {
            ['0'] = {
                name = 'Freelancer',
                payment = 10
        }
    },
    ['trucker'] = {
	label = 'Trucker',
	defaultDuty = true,
	offDutyPay = false,
	grades = {
            ['0'] = {
                name = 'Driver',
                payment = 50
        }
    }
})
```

## Import Gangs

* This method allows for any resource to insert gang data into the shared file for the core. That means that you can make a resource, and on load, make those gangs available for use. This can be accomplished through one the ways shown below. Utilizing the function requires importing the core but using the export does not

### QBCore.Functions.AddGang

```lua
QBCore.Functions.AddGang(gangName --[[string]], gang --[[table]])

-- Example
QBCore.Functions.AddGang('azteca', {
    label = 'Azteca',
    grades = {
        ['0'] = {
            name = 'Recruit'
        }
    }
})
```

### exports\['qb-core']:AddGang

```lua
exports['qb-core']:AddGang(gangName --[[string]], gang --[[table]])

-- Example
exports['qb-core']:AddGang('azteca', {
    label = 'Azteca',
    grades = {
        ['0'] = {
            name = 'Recruit'
        }
    }
})
```

### QBCore.Functions.AddGangs

```lua
QBCore.Functions.AddGangs(gangs --[[table]])

-- Example
QBCore.Functions.AddGangs({
    ['lostmc'] = {
        label = 'Lost MC',
        grades = {
            ['0'] = {
                name = 'Recruit'
            }
        }
    },
    ['ballas'] = {
        label = 'Ballas',
        grades = {
            ['0'] = {
                name = 'Recruit'
            }
        }
    }
})
```

### exports\['qb-core']:AddGangs

```lua
exports['qb-core']:AddGangs(gangs --[[table]])

-- Example
exports['qb-core']:AddGangs({
    ['lostmc'] = {
        label = 'Lost MC',
        grades = {
            ['0'] = {
                name = 'Recruit'
            }
        }
    },
    ['ballas'] = {
        label = 'Ballas',
        grades = {
            ['0'] = {
                name = 'Recruit'
            }
        }
    }
})
```

## Import Items

* This method allows for any resource to insert item data into the shared file for the core. That means that you can make a resource, and on load, make those items available for use. This can be accomplished through one the ways shown below. Utilizing the function requires importing the core but using the export does not

### QBCore.Functions.AddItem

```lua
QBCore.Functions.AddItem(itemName --[[string]], item --[[table]])

-- Example
QBCore.Functions.AddItem('water_bottle', {
    name = 'water_bottle',
    label = 'Bottle of Water',
    weight = 10,
    type = 'item',
    image = 'water_bottle.png',
    unique = false,
    useable = true,
    shouldClose = true,
    combinable = nil,
    description = 'For all the thirsty out there'
})
```

### exports\['qb-core']:AddItem

```lua
exports['qb-core']:AddItem(itemName --[[string]], item --[[table]])

-- Example
exports['qb-core']:AddItem('water_bottle', {
    name = 'water_bottle',
    label = 'Bottle of Water',
    weight = 10,
    type = 'item',
    image = 'water_bottle.png',
    unique = false,
    useable = true,
    shouldClose = true,
    combinable = nil,
    description = 'For all the thirsty out there'
})
```

### QBCore.Functions.AddItems

```lua
QBCore.Functions.AddItems(items --[[table]])

-- Example
QBCore.Functions.AddItems({
    ['water_bottle'] = {
        name = 'water_bottle',
        label = 'Bottle of Water',
        weight = 10,
        type = 'item',
        image = 'water_bottle.png',
        unique = false,
        useable = true,
        shouldClose = true,
        combinable = nil,
        description = 'For all the thirsty out there'
    },
    ['sandwich'] = {
        name = 'sandwich',
        label = 'Sandwich',
        weight = 10,
        type = 'item',
        image = 'sandwich.png',
        unique = false,
        useable = true,
        shouldClose = true,
        combinable = nil,
        description = 'Nice bread for your stomach'
    }
})
```

### exports\['qb-core']:AddItems

```lua
exports['qb-core']:AddItems(items --[[table]])

-- Example
exports['qb-core']:AddItems({
    ['water_bottle'] = {
        name = 'water_bottle',
        label = 'Bottle of Water',
        weight = 10,
        type = 'item',
        image = 'water_bottle.png',
        unique = false,
        useable = true,
        shouldClose = true,
        combinable = nil,
        description = 'For all the thirsty out there'
    },
    ['sandwich'] = {
        name = 'sandwich',
        label = 'Sandwich',
        weight = 10,
        type = 'item',
        image = 'sandwich.png',
        unique = false,
        useable = true,
        shouldClose = true,
        combinable = nil,
        description = 'Nice bread for your stomach'
    }
})
```
