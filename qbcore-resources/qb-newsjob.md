---
description: Hot off the press!
---

# 📰 qb-newsjob

## Introduction

* Allow players to play as a news reporter, use job vehicles and helicopters, and use commands to pull out news equipment

## Configuration

### Locations

```lua
Config.Locations = {
    ["main"] = { -- entrance teleporter
        label = "Weazle News HQ",
        coords = vector4(-597.89, -929.95, 24.0, 271.5),
    },
    ["inside"] = { -- spawn point / exit point
        label = "Weazle News HQ Inside",
        coords = vector4(-77.46, -833.77, 243.38, 67.5),
    },
    ["outside"] = { -- spawn point
        label = "Weazle News HQ Outside",
        coords = vector4(-598.25, -929.86, 23.86, 86.5),
    },
    ["vehicle"] = { -- vehicle withdraw point
        label = "Vehicle Storage",
        coords = vector4(-552.24, -925.61, 23.86, 242.5),
    },
    ["heli"] = { -- helicopter withdraw point
	label = "Helicopter Storage",
	coords = vector4(-583.08, -930.55, 36.83, 89.26),
    }
}
```

### Vehicles

```lua
Config.Vehicles = { -- list vehicles by grade
	-- Grade 0
	[0] = {
		["rumpo"] = "Rumpo",
	},
	-- Grade 1
	[1] = {
		["rumpo"] = "Rumpo",
	},
	-- Grade 2
	[2] = {
		["rumpo"] = "Rumpo",
	},
	-- Grade 3
	[3] = {
		["rumpo"] = "Rumpo",
	},
	-- Grade 4
	[4] = {
		["rumpo"] = "Rumpo",
	}
}
```

### Helicopters

```lua
Config.Helicopters = { -- list helicopters by grade
	-- Grade 0
	[0] = {
		["frogger"] = "Frogger",
	},
	-- Grade 1
	[1] = {
		["frogger"] = "Frogger",

	},
	-- Grade 2
	[2] = {
		["frogger"] = "Frogger",
	},
	-- Grade 3
	[3] = {
		["frogger"] = "Frogger",
	},
	-- Grade 4
	[4] = {
		["frogger"] = "Frogger",
	}
}
```

## Commands

* /newscam - Makes player pull out a news camera
* /newsmic - Makes player pull out a news microphone
* /newsbmic - Makes player pull out a news boom microphone
