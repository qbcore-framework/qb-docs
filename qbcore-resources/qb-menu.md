---
description: I like buttons
---

# ↖️ qb-menu

## Introduction

The **QB Menu** system is a Lua-based interactive menu integrated with a web-based user interface

{% hint style="success" %}
Menu icons can be found on the [Font Awesome](https://fontawesome.com/) website
{% endhint %}

### Features

* Dynamic menu creation
* Support for icons and images
* Menu sorting functionality
* Client-server communication
* Easy-to-use Lua and JavaScript interfaces
* Exports and events for extensive integration

## openMenu

Opens the menu with provided data

* data: `table`&#x20;
  * header: `string` (optional)
  * txt: `string` (optional)
  * icon: `string` (optional)
  * isMenuHeader: `boolean` (optional)
  * disabled: `boolean` (optional)
  * hidden: `boolean` (optional)
  * params: `table` (optional)
    * event: `string`
    * args: `any` (optional)
    * isServer: `boolean` (optional)
    * isCommand: `boolean` (optional)
    * isQBCommand: `boolean` (optional)
    * isAction: `boolean` (optional)
* sort: `boolean`
* skipFirst: `boolean`

```lua
exports['qb-menu']:openMenu({
    { 
        header = "First Item", 
        icon = "icon-name", 
        txt = "Description",
        isMenuHeader = false,
        disabled = false,
        hidden = false,
        params = {
            event = "event:name",
            args = { arg1 = "value1" },
            isServer = false,
            isCommand = false,
            isQBCommand = false,
            isAction = false
        }
    },
    { 
        header = "Second Item", 
        txt = "Another description",
        isMenuHeader = false,
        disabled = true,
        hidden = false
    }
}, true, false)
```

## closeMenu

Closes the menu

```lua
exports['qb-menu']:closeMenu()
```
