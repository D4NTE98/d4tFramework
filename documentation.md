# d4tFramework Documentation

## Overview

d4tFramework is a modern modular framework for FiveM servers focused on:

* Performance
* Security
* Modular architecture
* Clean resource separation
* Modern UI/UX
* Scalable multiplayer systems
* Developer-friendly exports and APIs

Author: D4NTE
Current Version: `0.1.0`

---

# d4tCore

## Description

Main framework core resource.

Provides:

* Player lifecycle
* Framework exports
* Shared utility functions
* Module architecture
* Callback system
* Notification system
* Permission handling
* Resource bridge layer

## Structure

```text
client/modules/
server/modules/
shared/modules/
```

## Features

* Lightweight architecture
* Modern exports
* Event-driven systems
* Optimized player cache
* Clean coding standard
* Independent modules

## Example Export

```lua
local player = exports.d4tCore:GetPlayer(source)
```

---

# d4tConnection

## Description

Database abstraction layer for MySQL communication.

Replacement for traditional MySQL wrappers.

## Features

* Async queries
* Prepared statements
* Promise support
* Insert helpers
* Single-row queries
* Secure parameter binding
* Connection pooling

## Example

```lua
local rows = exports.d4tConnection:Query('SELECT * FROM users WHERE id = ?', {
    playerId
})
```

---

# d4tData

## Description

Secure synchronized entity data system.

Alternative to elementData/state bags.

## Features

* Player data sync
* Vehicle data sync
* Object data sync
* Token validation
* Ownership protection
* Anti-spoof validation
* Scoped synchronization
* Secure replication

## Example

```lua
exports.d4tData:SetPlayerData(player, 'money', 500)
```

---

# d4tTarget

## Description

Modern target and interaction system.

## Features

* Ped targeting
* Vehicle targeting
* Object targeting
* Bone interactions
* Distance checks
* Dynamic options
* Icon support
* Permission restrictions

## Example

```lua
exports.d4tTarget:AddEntity(entity, {
    label = 'Open',
    icon = 'fa-box-open'
})
```

---

# d4tAdmin

## Description

Administration and moderation system.

## Features

* Spectate
* Teleport
* Player management
* Vehicle spawning
* Ban system
* Warning system
* Permission groups
* Animated admin UI

## UI

Includes:

```text
preview.html
```

---

# d4tAntiCheat

## Description

Security and anti-cheat resource.

## Features

* Weapon validation
* Explosion detection
* Event protection
* Injection detection
* Entity spam prevention
* Screenshot validation
* Resource integrity checks
* Trigger protection

## Security

Server-authoritative validation is used whenever possible.

---

# d4tAuth

## Description

Authentication and character creation system.

## Features

* Login
* Registration
* Character creation
* Character selection
* Character customization
* Session tokens
* Account persistence
* Secure password hashing

## Database Tables

```text
d4t_accounts
d4t_characters
d4t_sessions
```

## UI

Minimal modern interface matching d4tLoadingScreen.

---

# d4tInventory

## Description

Inventory and item management system.

## Features

* Drag and drop inventory
* Metadata items
* Hotbar
* Weapon support
* Vehicle stashes
* Player trading
* Weight system
* Container items

## Example Item

```lua
['water'] = {
    label = 'Water',
    weight = 1
}
```

---

# d4tJobs

## Description

Civilian job resource.

## Included Jobs

* Warehouse worker
* Potato farmer
* Bus driver

## Features

* NPC employers
* Route systems
* Reward payouts
* Animated UI
* Marker interactions
* Task progression
* Payment tracking

---

# d4tVehicles

## Description

Vehicle ownership and garage system.

## Features

* Vehicle ownership
* Garage system
* Vehicle keys
* Impound support
* Persistent vehicles
* Spawn management
* Plate handling
* Vehicle metadata

---

# d4tEvents

## Description

Server event and minigame resource.

## Included Events

### Hide and Seek

* Admin creates event
* Special detection weapon
* Last surviving player wins
* Automatic teleport return

### Pursuit Event

* Players chase admin vehicle
* First player entering target vehicle wins
* Automatic event finish

## Commands

```text
/cevent <name> <reward>
/devent
/oevent
```

---

# d4tLoadingScreen

## Description

Minimal animated loading screen.

## Features

* GTA-inspired background
* Animated loading bar
* Random pro tips
* Modern branding
* Smooth transitions
* Responsive design

## UI Style

* Minimal
* Glassmorphism
* Animated background
* Dynamic tips

---

# Resource Order

## Recommended Start Order

```cfg
ensure d4tConnection
ensure d4tCore
ensure d4tData
ensure d4tTarget
ensure d4tAdmin
ensure d4tAntiCheat
ensure d4tAuth
ensure d4tInventory
ensure d4tJobs
ensure d4tVehicles
ensure d4tEvents
ensure d4tLoadingScreen
```

---

# GitHub Links

## Framework

```text
https://github.com/D4NTE98/d4tFramework
```

## Author

```text
https://github.com/D4NTE98
```

---

# Developer Documentation

## Architecture

Every resource follows the same modular structure:

```text
resource/
├── client/
│   └── modules/
├── server/
│   └── modules/
├── shared/
│   └── modules/
├── web/
├── sql/
├── docs/
└── fxmanifest.lua
```

---

## Naming Convention

### Resources

```text
d4t<ResourceName>
```

Examples:

```text
d4tCore
d4tInventory
d4tVehicles
```

### Events

```lua
'd4t<Resource>:<side>:<action>'
```

Examples:

```lua
'd4tAuth:server:login'
'd4tInventory:client:update'
```

### Exports

Exports use PascalCase.

Example:

```lua
exports.d4tCore:GetPlayer(source)
exports.d4tData:SetPlayerData(player, key, value)
```

---

## Shared Principles

### 1. Server Authoritative Logic

Critical systems must always validate actions server-side.

Never trust client values directly.

### 2. Minimal Dependencies

Resources should avoid unnecessary external dependencies.

### 3. Modular Design

Each feature should exist inside isolated modules.

Avoid massive monolithic files.

### 4. Secure Networking

All network events should:

* Validate source
* Validate permissions
* Validate payload types
* Validate ownership
* Prevent spam

### 5. Clean UI Layer

NUI interfaces use:

* HTML
* CSS
* Vanilla JavaScript

No heavy frontend frameworks are required.

---

# d4tCore Developer API

## Player Object

```lua
local player = exports.d4tCore:GetPlayer(source)
```

### Methods

```lua
player:GetId()
player:GetName()
player:GetIdentifier()
player:GetCharacterId()
player:GetMoney(type)
player:AddMoney(type, amount)
player:RemoveMoney(type, amount)
player:SetJob(job, grade)
player:GetJob()
```

---

## Callback System

### Register Callback

```lua
exports.d4tCore:RegisterCallback('example:getData', function(source, cb)
    cb({ success = true })
end)
```

### Trigger Callback

```lua
exports.d4tCore:TriggerCallback('example:getData', function(response)
    print(json.encode(response))
end)
```

---

# d4tData Developer API

## Player Data

### Set Data

```lua
exports.d4tData:SetPlayerData(player, key, value)
```

### Get Data

```lua
local value = exports.d4tData:GetPlayerData(player, key)
```

### Remove Data

```lua
exports.d4tData:RemovePlayerData(player, key)
```

---

## Vehicle Data

```lua
exports.d4tData:SetVehicleData(vehicle, key, value)
exports.d4tData:GetVehicleData(vehicle, key)
```

---

## Data Replication

The system automatically:

* Replicates entity data
* Validates ownership
* Prevents spoofing
* Protects synchronized keys

---

# d4tInventory Developer API

## Add Item

```lua
exports.d4tInventory:AddItem(player, 'water', 1)
```

## Remove Item

```lua
exports.d4tInventory:RemoveItem(player, 'water', 1)
```

## Get Inventory

```lua
local inventory = exports.d4tInventory:GetInventory(player)
```

## Register Item

```lua
exports.d4tInventory:RegisterItem('water', {
    label = 'Water',
    weight = 1,
    stack = true,
    usable = true
})
```

---

# d4tVehicles Developer API

## Spawn Vehicle

```lua
exports.d4tVehicles:SpawnOwnedVehicle(player, {
    model = 'sultan',
    plate = 'D4T001'
})
```

## Vehicle Ownership

```lua
exports.d4tVehicles:SetVehicleOwner(vehicleId, characterId)
```

---

# d4tAuth Developer Flow

## Authentication Flow

```text
Client opens UI
-> Login/Register
-> Server validation
-> Session token creation
-> Character list fetch
-> Character selection
-> Spawn player
```

## Character Object

```lua
{
    id = 1,
    firstname = 'John',
    lastname = 'Walker',
    sex = 'male',
    position = {},
    money = {}
}
```

---

# Security Recommendations

## Always Validate

Never trust:

* Client money values
* Inventory values
* Coordinates
* Entity ownership
* Vehicle ownership
* Job permissions

## Recommended Checks

```lua
if source ~= player then
    return
end
```

```lua
if type(amount) ~= 'number' then
    return
end
```

```lua
if amount < 0 then
    return
end
```

---

# UI Development

## Style Guidelines

All d4tFramework interfaces follow:

* Minimal design
* Glassmorphism
* Soft animations
* Dark UI palette
* GTA-inspired backgrounds
* Responsive layouts

## UI Structure

```text
web/
├── index.html
├── preview.html
├── style.css
└── app.js
```

---

# Coding Standards

## Lua

* Use readable multi-line formatting
* Avoid one-line compression
* Use descriptive naming
* Separate logic into modules
* Avoid duplicated logic

## JavaScript

* Prefer vanilla JavaScript
* Avoid unnecessary libraries
* Keep UI modular
* Use event-driven architecture

## SQL

* Use prepared statements
* Never concatenate unsafe values
* Use indexes on heavy tables
* Use JSON columns carefully

---

# Performance Notes

## Recommended

* Cache player objects
* Avoid unnecessary loops
* Use local variables
* Avoid excessive synchronization
* Use scoped replication

## Avoid

* Massive global tables
* Unvalidated client events
* Infinite loops without waits
* Heavy per-frame calculations

---

# Development Philosophy

The d4tFramework ecosystem follows these principles:

* Secure-by-default systems
* Modern UI/UX
* Minimal dependencies
* Modular architecture
* Scalable server logic
* Optimized networking
* Readable codebase
* Consistent resource naming

---

# License

All rights reserved.

Created by D4NTE.
