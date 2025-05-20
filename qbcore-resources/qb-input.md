---
description: Enter stuff here
---

# 📝 qb-input

## Introduction

The **QB Input** system provides an interactive Lua-based user input form integrated with a web-based interface

### Features

* Multiple input types (text, password, number, radio, select, checkbox, color)
* Customizable form submission
* Dynamic styling through configuration
* Easy-to-use Lua and JavaScript integration

## ShowInput

Displays an input form and returns user input data.

* data: `table`
  * header :_`string` (optional)_
  * submitText:_`string` (optional)_
  * inputs: `table`
    * type: _`string`_
    * name: _`string`_
    * text: _`string`_
    * default: _`any` (optional)_
    * isRequired: _`boolean` (optional)_
    * options: _`table` (optional)_
      * text: _`string`_
      * value: _`string`_
      * checked: _`boolean` (optional)_

```lua
RegisterCommand('testinput', function()
    local dialog = exports['qb-input']:ShowInput({
        header = "Test",
        submitText = "Bill",
        inputs = {
            {
                text = "Citizen ID (#)",
                name = "citizenid",
                type = "text",
                isRequired = true,
                default = "CID-1234",
            },
            {
                text = "Secret Code (Give to Nobody)",
                name = "code",
                type = "password",
                isRequired = true,
                default = "password123",
            },
            {
                text = "Bill Price ($)",
                name = "billprice",
                type = "number",
                isRequired = false,
                default = 1,
            },
            {
                text = "Bill Type",
                name = "billtype",
                type = "radio",
                options = {
                    { value = "bill", text = "Bill" },
                    { value = "cash", text = "Cash" },
                    { value = "bank", text = "Bank" }
                },
                default = "cash",
            },
            {
                text = "Include Tax?",
                name = "taxincl",
                type = "checkbox",
                options = {
                    { value = "gst", text = "10% incl."},
                    { value = "business", text = "35% incl.", checked = true },
                    { value = "othertax", text = "15% incl."}
                }
            },
            {
                text = "Some Select",
                name = "someselect",
                type = "select",
                options = {
                    { value = "none", text = "None" },
                    { value = "other", text = "Other"},
                    { value = "other2", text = "Other2" },
                    { value = "other3", text = "Other3" },
                    { value = "other4", text = "Other4" },
                    { value = "other5", text = "Other5" },
                    { value = "other6", text = "Other6" },
                },
                default = "other3",
            },
            {
                text = "Favorite Color",
                name = "favoritecolor",
                type = "color",
                default = "#ff0000",
            }
        }
    })

    if dialog ~= nil then
        for k,v in pairs(dialog) do
            print(k .. " : " .. v)
        end
    end
end, false)
```

## CloseMenu

Closes the menu

```lua
exports['qb-input']:CloseMenu()
```
