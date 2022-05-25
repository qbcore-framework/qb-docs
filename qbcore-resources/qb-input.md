---
description: Enter stuff here
---

# 📝 qb-input

## Introduction

* An interactive NUI menu that allows users to input various values and can be used in all sorts of ways

## Preview

![](../.gitbook/assets/qbinput.png)

## Usage Example

```etlua
RegisterCommand('testinput', function()
    local dialog = exports['qb-input']:ShowInput({
        header = "Test",
        submitText = "Bill",
        inputs = {
            {
                text = "Citizen ID (#)", -- text you want to be displayed as a place holder
                name = "citizenid", -- name of the input should be unique otherwise it might override
                type = "text", -- type of the input
                isRequired = true, -- Optional [accepted values: true | false] but will submit the form if no value is inputted
                -- default = "CID-1234", -- Default text option, this is optional
            },
            {
                text = "Secret Code (Give to Nobody)", -- text you want to be displayed as a place holder
                name = "code", -- name of the input should be unique otherwise it might override
                type = "password", -- type of the input
                isRequired = true, -- Optional [accepted values: true | false] but will submit the form if no value is inputted
                -- default = "password123", -- Default text option, this is optional
            },
            {
                text = "Bill Price ($)", -- text you want to be displayed as a place holder
                name = "billprice", -- name of the input should be unique otherwise it might override
                type = "number", -- type of the input - number will not allow non-number characters in the field so only accepts 0-9
                isRequired = false, -- Optional [accepted values: true | false] but will submit the form if no value is inputted
                -- default = 1, -- Default number option, this is optional
            },
            {
                text = "Bill Type", -- text you want to be displayed as a input header
                name = "billtype", -- name of the input should be unique otherwise it might override
                type = "radio", -- type of the input - Radio is useful for "or" options e.g; billtype = Cash OR Bill OR bank
                options = { -- The options (in this case for a radio) you want displayed, more than 6 is not recommended
                    { value = "bill", text = "Bill" }, -- Options MUST include a value and a text option
                    { value = "cash", text = "Cash" }, -- Options MUST include a value and a text option
                    { value = "bank", text = "Bank" }  -- Options MUST include a value and a text option
                },
                -- default = "cash", -- Default radio option, must match a value from above, this is optional
            },
            {
                text = "Include Tax?", -- text you want to be displayed as a input header
                name = "taxincl", -- name of the input should be unique otherwise it might override
                type = "checkbox", -- type of the input - Check is useful for "AND" options e.g; taxincle = gst AND business AND othertax
                options = { -- The options (in this case for a check) you want displayed, more than 6 is not recommended
                    { value = "gst", text = "10% incl."}, -- Options MUST include a value and a text option
                    { value = "business", text = "35% incl.", checked = true }, -- Options MUST include a value and a text option, checked = true is default value, optional
                    { value = "othertax", text = "15% incl."}  -- Options MUST include a value and a text option
                }
            },
            {
                text = "Some Select", -- text you want to be displayed as a input header
                name = "someselect", -- name of the input should be unique otherwise it might override
                type = "select", -- type of the input - Select is useful for 3+ amount of "or" options e.g; someselect = none OR other OR other2 OR other3...etc
                options = { -- Select drop down options, the first option will by default be selected
                    { value = "none", text = "None" }, -- Options MUST include a value and a text option
                    { value = "other", text = "Other"}, -- Options MUST include a value and a text option
                    { value = "other2", text = "Other2" }, -- Options MUST include a value and a text option
                    { value = "other3", text = "Other3" }, -- Options MUST include a value and a text option
                    { value = "other4", text = "Other4" }, -- Options MUST include a value and a text option
                    { value = "other5", text = "Other5" }, -- Options MUST include a value and a text option
                    { value = "other6", text = "Other6" }, -- Options MUST include a value and a text option
                },
                -- default = 'other3', -- Default select option, must match a value from above, this is optional
            }
        },
    })

    if dialog ~= nil then
        for k,v in pairs(dialog) do
            print(k .. " : " .. v)
        end
    end
end, false)
```
