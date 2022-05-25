---
description: Truckin' and dumpin'
---

# 🚛 qb-truckerjob

## Introduction

* Allows players to rent a van from the warehouse and deliver packages to preset locations. With each delivery there's a chance they will get a cryptostick. Read more about those in[qb-crypto.md](qb-crypto.md "mention")

{% hint style="success" %}
This job is setup to restock random stores around the map as players complete deliveries!
{% endhint %}

## Configuration

### General

```lua
Config.BailPrice = 250 -- vehicle rental price

Config.Vehicles = { --Vehicles the job can rent to start their route
    ["rumpo"] = "Dumbo Delivery",
}
```

### Delivery locations

{% hint style="danger" %}
If you want this job to restock the stores, make sure the name inside the stores table matches the index name in [qb-shops.md](qb-shops.md "mention")
{% endhint %}

```lua
Config.Locations = {
    ["main"] = {
        label = "Truck Shed", -- map blip name
        coords = vector4(153.68, -3211.88, 5.91, 274.5), -- map blip location
    },
    ["vehicle"] = {
        label = "Truck Storage", -- map blip name
        coords = vector4(141.12, -3204.31, 5.85, 267.5), -- map blip location
    },
    ["stores"] ={
        [1] = {
            name = "ltdgasoline", -- store name referenced to qb-shops
            coords = vector4(-41.07, -1747.91, 29.4, 137.5), -- interact location
        },
        [2] = {
            name = "247supermarket",
            coords = vector4(31.62, -1315.87, 29.52, 179.5),
        },
    },
}
```
