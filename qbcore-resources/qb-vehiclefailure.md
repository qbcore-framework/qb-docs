---
description: Oh, you said you wanted realism?
---

# 🔨 qb-vehiclefailure

## Introduction

* Handles the logic for vehicle damage
* Has handling logic like `sundayDriver`&#x20;

{% hint style="info" %}
This resource is just a modified version of [Realistic Vehicle Failure](https://github.com/StockholmCityRP/fivem-realisticvehicle)
{% endhint %}

## Configuration

### General

```lua
deformationMultiplier = -1, -- How much should the vehicle visually deform from a collision. Range 0.0 to 10.0 Where 0.0 is no deformation and 10.0 is 10x deformation. -1 = Don't touch. Visual damage does not sync well to other players.
deformationExponent = 0.5, -- How much should the handling file deformation setting be compressed toward 1.0. (Make cars more similar). A value of 1=no change. Lower values will compress more, values above 1 it will expand. Dont set to zero or negative.
collisionDamageExponent = 0.5,	-- How much should the handling file deformation setting be compressed toward 1.0. (Make cars more similar). A value of 1=no change. Lower values will compress more, values above 1 it will expand. Dont set to zero or negative.
damageFactorEngine = 3.0, -- Some values are 1 to 100. Higher values means more damage to vehicle. A good starting point is 10
damageFactorBody = 3.0,	-- Some values are 1 to 100. Higher values means more damage to vehicle. A good starting point is 10
damageFactorPetrolTank = 32.0,	-- Some values are 1 to 200. Higher values means more damage to vehicle. A good starting point is 64
engineDamageExponent = 0.3,-- How much should the handling file engine damage setting be compressed toward 1.0. (Make cars more similar). A value of 1=no change. Lower values will compress more, values above 1 it will expand. Dont set to zero or negative.
weaponsDamageMultiplier = 1.2, -- How much damage should the vehicle get from weapons fire. Range 0.0 to 10.0, where 0.0 is no damage and 10.0 is 10x damage. -1 = don't touch
degradingHealthSpeedFactor = 2,	-- Speed of slowly degrading health, but not failure. Value of 10 means that it will take about 0.25 second per health point, so degradation from 800 to 305 will take about 2 minutes of clean driving. Higher values means faster degradation
cascadingFailureSpeedFactor = 4.0, -- Some values are 1 to 100. When vehicle health drops below a certain point, cascading failure sets in, and the health drops rapidly until the vehicle dies. Higher values means faster failure. A good starting point is 8
degradingFailureThreshold = 250.0, -- Below this value, slow health degradation will set in
cascadingFailureThreshold = 200.0, -- Below this value, health cascading failure will set in
engineSafeGuard = 50.0,	-- Final failure value. Set it too high, and the vehicle won't smoke when disabled. Set too low, and the car will catch fire from a single bullet to the engine. At health 100 a typical car can take 3-4 bullets to the engine before catching fire.
torqueMultiplierEnabled = true,	-- Decrease engine torque as engine gets more and more damaged
limpMode = false, -- If true, the engine never fails completely, so you will always be able to get to a mechanic unless you flip your vehicle and preventVehicleFlip is set to true
limpModeMultiplier = 0.15, -- The torque multiplier to use when vehicle is limping. Sane values are 0.05 to 0.25
preventVehicleFlip = true, -- If true, you can't turn over an upside down vehicle
sundayDriver = true, -- If true, the accelerator response is scaled to enable easy slow driving. Will not prevent full throttle. Does not work with binary accelerators like a keyboard. Set to false to disable. The included stop-without-reversing and brake-light-hold feature does also work for keyboards.
sundayDriverAcceleratorCurve = 7.5, -- The response curve to apply to the accelerator. Range 0.0 to 10.0. Higher values enables easier slow driving, meaning more pressure on the throttle is required to accelerate forward. Does nothing for keyboard drivers
sundayDriverBrakeCurve = 5.0, -- The response curve to apply to the Brake. Range 0.0 to 10.0. Higher values enables easier braking, meaning more pressure on the throttle is required to brake hard. Does nothing for keyboard drivers
displayBlips = false, -- Show blips for mechanics locations
compatibilityMode = false, -- prevents other scripts from modifying the fuel tank health to avoid random engine failure with BVA 2.01 (Downside is it disabled explosion prevention)
randomTireBurstInterval = 0, -- Number of minutes (statistically, not precisely) to drive above 22 mph before you get a tire puncture. 0=feature is disabled
```

### Vehicle class damage

```lua
classDamageMultiplier = { -- vehicle class damage modifier, index is class
        1.0, --	0: Compacts
        1.0, --	1: Sedans
        1.0, --	2: SUVs
        1.0, --	3: Coupes
        1.0, --	4: Muscle
        1.0, --	5: Sports Classics
        1.3, --	6: Sports
        1.3, --	7: Super
        0.25, --	8: Motorcycles
        0.7, --	9: Off-road
        0.25, --	10: Industrial
        1.0, --	11: Utility
        1.0, --	12: Vans
        1.0, --	13: Cycles
        10.5, --	14: Boats
        1.0, --	15: Helicopters
        1.0, --	16: Planes
        1.0, --	17: Service
        0.75, --	18: Emergency
        0.75, --	19: Military
        1.0, --	20: Commercial
        1.0 --	21: Trains
}
```

### Back engine vehicles

{% hint style="success" %}
These vehicles take less damage from impacts in the front and take more damage from impacts in the back
{% endhint %}

```lua
BackEngineVehicles = {
    [`ninef`] = true, -- vehicle hash
    [`adder`] = true,
    [`vagner`] = true,
    [`t20`] = true,
    [`infernus`] = true,
    [`zentorno`] = true,
    [`reaper`] = true,
    [`comet2`] = true,
    [`jester`] = true,
    [`jester2`] = true,
    [`cheetah`] = true,
    [`cheetah2`] = true,
    [`prototipo`] = true,
    [`turismor`] = true,
    [`pfister811`] = true,
    [`ardent`] = true,
    [`nero`] = true,
    [`nero2`] = true,
    [`tempesta`] = true,
    [`vacca`] = true,
    [`bullet`] = true,
    [`osiris`] = true,
    [`entityxf`] = true,
    [`turismo2`] = true,
    [`fmj`] = true,
    [`re7b`] = true,
    [`tyrus`] = true,
    [`italigtb`] = true,
    [`penetrator`] = true,
    [`monroe`] = true,
    [`ninef2`] = true,
    [`stingergt`] = true,
    [`surfer`] = true,
    [`surfer2`] = true,
    [`comet3`] = true,
}
```
