---
description: Learn how to use the built-in NUI drawtext function!
---

# 💬 DrawText

{% hint style="success" %}
Accepted positions: Left, Right, Top
{% endhint %}

| Function or Event                                                          | Description                                                                                                                                                |
| -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| exports\['qb-core']:DrawText('message','position')                         | This is a client export that will draw a message at the specified position (listed below)                                                                  |
| exports\['qb-core']:ChangeText('message','position')                       | This is a client export that will change the currently displayed message at the specified position (listed below)                                          |
| exports\['qb-core']:HideText()                                             | This will hide the text display                                                                                                                            |
| exports\['qb-core']:KeyPressed()                                           | This is useful if you want to change the background and hide the text on keypress (if not handled correctly users will have to renter the zone to display) |
| TriggerClientEvent('qb-core:client:DrawText', source, message, position)   | The same as the export but as an event                                                                                                                     |
| TriggerClientEvent('qb-core:client:ChangeText', source, message, position) | The same as the export but as an event                                                                                                                     |
| TriggerClientEvent('qb-core:client:HideText', source)                      | The same as the export but as an event                                                                                                                     |
| TriggerClientEvent('qb-core:client:KeyPressed', source)                    | The same as the export but as an event                                                                                                                     |

### HideText

* Function to hide the currently displayed text

```lua
-- Source code for reference

local function hideText()
    SendNUIMessage({
        action = 'HIDE_TEXT',
    })
end
exports('HideText', hideText)

-- Export example

local function examplefunction()
    exports['qb-core']:DrawText('This is a test', 'left')
    Wait(5000) -- display text for 5 seconds
    exports['qb-core']:HideText()
end

-- Client example

local function examplefunction()
    TriggerEvent('qb-core:client:DrawText', 'This is a test', 'left')
    Wait(5000) -- display text for 5 seconds
    TriggerEvent('qb-core:client:HideText')
end

-- Server example

local function examplefunction()
    TriggerClientEvent('qb-core:client:DrawText', source, 'This is a test', 'left')
    Wait(5000) -- display text for 5 seconds
    TriggerClientEvent('qb-core:client:HideText', source)
end
```

### DrawText

* Function to draw the text on the screen

```lua
-- Source code for reference

local function drawText(text, position)
    if not type(position) == "string" then position = "left" end
    SendNUIMessage({
        action = 'DRAW_TEXT',
        data = {
            text = text,
            position = position
        }
    })
end
exports('DrawText', drawText)

-- Export example

local function examplefunction()
    exports['qb-core']:DrawText('This is a test', 'left')
    Wait(5000) -- display text for 5 seconds
    exports['qb-core']:HideText()
end

-- Client example

local function examplefunction()
    TriggerEvent('qb-core:client:DrawText', 'This is a test', 'left')
    Wait(5000) -- display text for 5 seconds
    TriggerEvent('qb-core:client:HideText')
end

-- Server example

local function examplefunction()
    TriggerClientEvent('qb-core:client:DrawText', source, 'This is a test', 'left')
    Wait(5000) -- display text for 5 seconds
    TriggerClientEvent('qb-core:client:HideText', source)
end
```

### ChangeText

* Function to change the currently displayed text

```lua
-- Source code for reference

local function changeText(text, position)
    if not type(position) == "string" then position = "left" end
    SendNUIMessage({
        action = 'CHANGE_TEXT',
        data = {
            text = text,
            position = position
        }
    })
end
exports('ChangeText', changeText)

-- Export example

local function examplefunction()
    exports['qb-core']:DrawText('This is a test', 'left')
    Wait(5000) -- change text after 5 seconds
    exports['qb-core']:ChangeText('This is your changed text', 'left')
    Wait(5000) -- display changed text for 5 seconds
    exports['qb-core']:HideText()
end

-- Client example

local function examplefunction()
    TriggerEvent('qb-core:client:DrawText', 'This is a test', 'left')
    Wait(5000) -- change text after 5 seconds
    TriggerEvent('qb-core:client:ChangeText', 'This is your changed text', 'left')
    Wait(5000) -- display changed text for 5 seconds
    TriggerEvent('qb-core:client:HideText')
end

-- Server example

local function examplefunction()
    TriggerClientEvent('qb-core:client:ChangeText', source, 'This is your changed text', 'left')
end
```

### KeyPressed

* Optional function that is used for displaying an animation on key press then hides the currently displayed text

```lua
-- Source code for reference

local function keyPressed()
    CreateThread(function()
        SendNUIMessage({
            action = 'KEY_PRESSED',
        })
        Wait(500)
        hideText()
    end)
end
exports('KeyPressed', keyPressed)

-- Export example

CreateThread(function()
    local textDrawn = false
    while true do
        Wait(0)
        if not textDrawn then
            exports['qb-core']:DrawText('This is a test','left')
            textDrawn = true
        end
        if IsControlJustPressed(0, 38) then
            exports['qb-core']:KeyPressed()
        end
    end
end)

-- Client example

CreateThread(function()
    local textDrawn = false
    while true do
        Wait(0)
        if not textDrawn then
            TriggerEvent('qb-core:client:DrawText', 'This is a test','left')
            textDrawn = true
        end
        if IsControlJustPressed(0, 38) then
            TriggerEvent('qb-core:client:KeyPressed')
        end
    end
end)
```
