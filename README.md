# keep-bags

![Keep-bags](.github/images/keep-bags.jpg)

keep-bags is a script designed to enhance the inventory management experience for players. With a range of key features.

## Key Features

- **Expanded Inventory Capacity**: Players can carry more materials and items within their inventory, allowing for greater flexibility and resource management.

- **Props**: The script provides realistic visuals by displaying bag props on the player's back or hands, indicating that they are equipped with a bag.

- **Blacklisted Items**: A flexible option allows you to specify blacklisted items, ensuring that certain items cannot be stored in the bag. This feature helps maintain balance and prevents abuse.

- **Smooth Animation**: Opening and closing animations provide an immersive and visually appealing experience when accessing the backpack. These animations enhance realism and immersion within the game.

- **Locking System**: Bags can be equipped with a locking system, offering an additional layer of security for valuable items.

- **Prevents Exploits**: The script actively prevents the "bag in bag" exploit, ensuring fair gameplay and maintaining the integrity of the inventory system.

## ❤️ Support Development

If you enjoy my work and would like to show your appreciation, please consider making a donation to support the ongoing development of the script. Your contribution goes a long way in helping me add more exciting features and improvements. 🚀

- Click Here -> [ko-fi](https://ko-fi.com/swkeep)

Thank you for your generosity and support! 🙏

### Support

- [Discord](https://discord.gg/ccMArCwrPV)

# Preview

Check out Keep-bags preview for a better understanding of the mod's functionality.

## [Click HERE (Youtube)](https://youtu.be/4FCx1_pOTpE)

# Resource Usage

![Keep-bags](.github/images/test.png)

- i renamed the script from keep-backpack to keep-bags ;)

# Dependencies

- qb-core/esx
- qb-inventory/ox_inventory
- ox_lib (required on esx/optional for qbcore)
- **[keep-harmony](https://swkeep.tebex.io/package/5592482)**
- [illenium-appearance](https://github.com/iLLeniumStudios/illenium-appearance) / [qb-clothing](https://github.com/qbcore-framework/qb-clothing)

# How to Install

Follow the steps mentioned below to install keep-bags:

## step 1:

- Add images inside `inventoryimages` to `qb-inventory/html/images`

## step 2:

- Add Below code to `qb-core/shared/items.lua`

```lua
 backpack1                    = { name = "backpack1", label = "Backpack", weight = 7500, type = "item", image = "backpack1.png", unique = true, useable = true, shouldClose = true, combinable = nil, description = "A stylish backpack" },
    backpack2                    = { name = "backpack2", label = "Backpack", weight = 15000, type = "item", image = "backpack2.png", unique = true, useable = true, shouldClose = true, combinable = nil, description = "A stylish backpack" },
    duffle1                      = { name = "duffle1", label = "Duffle bag", weight = 15000, type = "item", image = "duffle1.png", unique = true, useable = true, shouldClose = true, combinable = nil, description = "A stylish duffle bag" },
    briefcase                    = { name = "briefcase", label = "Briefcase", weight = 10000, type = "item", image = "briefcase.png", unique = true, useable = true, shouldClose = true, combinable = nil, description = "A portable rectangular case used for carrying important documents, files, or other personal belongings." },
    paramedicbag                 = { name = "paramedicbag", label = "Paramedic bag", weight = 5000, type = "item", image = "paramedicbag.png", unique = true, useable = true, shouldClose = true, combinable = nil, description = "A medical bag used by paramedics, containing essential supplies for emergency care." },
    policepouches                = { name = "policepouches", label = "Police Pouch", weight = 5000, type = "item", image = "policepouches.png", unique = true, useable = true, shouldClose = true, combinable = nil, description = "A pouch used by police officers to store and carry essential supplies such as handcuffs, pepper spray, and other tactical equipment." },
    policepouches1               = { name = "policepouches1", label = "Police Pouch", weight = 5000, type = "item", image = "policepouches1.png", unique = true, useable = true, shouldClose = true, combinable = nil, description = "A larger version of the police pouch used to store additional tactical gear and equipment." },
    briefcaselockpicker          = { name = "briefcaselockpicker", label = "Briefcase Lockpicker", weight = 500, type = "item", image = "lockpick.png", unique = false, useable = true, shouldClose = true, combinable = nil, description = "Briefcase Lockpicker" },
```

## ESX (ox_inventory)

```lua
["backpack1"] = {
     label = "backpack1",
     weight = 15,
     stack = false,
     close = true,
     description = "A stylish backpack"
},
["backpack2"] = {
     label = "backpack2",
     weight = 15,
     stack = false,
     close = true,
     description = "A stylish backpack"
},
["duffle1"] = {
     label = "Duffle bag",
     weight = 15,
     stack = false,
     close = true,
     description = "A stylish duffle bag"
},
["briefcase"] = {
     label = "Briefcase",
     weight = 10,
     stack = false,
     close = true,
     description = "A portable rectangular case used for carrying important documents, files, or other personal belongings."
},
["paramedicbag"] = {
     label = "Paramedic bag",
     weight = 5,
     stack = false,
     close = true,
     description = "A medical bag used by paramedics, containing essential supplies for emergency care."
},
["policepouches"] = {
     label = "Police Pouch",
     weight = 5,
     stack = false,
     close = true,
     description = "A pouch used by police officers to store and carry essential supplies such as handcuffs, pepper spray, and other tactical equipment."
},
["policepouches1"] = {
     label = "Police Pouch",
     weight = 5,
     stack = false,
     close = true,
     description = "A larger version of the police pouch used to store additional tactical gear and equipment."
},

["briefcaselockpicker"] = {
     label = "Briefcase Lockpicker",
     weight = 0.5,
     stack = true,
     close = true,
     description = "Briefcase Lockpicker"
}
```

## Only if you're using qb-clothing 
Find the `openMenu` function in `client/main.lua` and then add this event at the end of it:

```lua
local function openMenu(allowedMenus)
     -- existing code up there ...

    TriggerEvent('qb-clothing:client->open')
end
```

## Only if you're using qb-inventory-legacy (version 1.2.4)
Find the `SaveStashItems()` function in `server/main.lua` and then add this event at the end of it 

```lua
TriggerEvent('keep-harmony:stash->close', stashId)
```

after editing the function. The modified function should look like this:

```lua
local function SaveStashItems(stashId, items)
	if Stashes[stashId].label == 'Stash-None' or not items then return end

	for _, item in pairs(items) do
		item.description = nil
	end

	MySQL.insert('INSERT INTO stashitems (stash, items) VALUES (:stash, :items) ON DUPLICATE KEY UPDATE items = :items',
		{
			['stash'] = stashId,
			['items'] = json.encode(items)
		})

	Stashes[stashId].isOpen = false
	TriggerEvent('keep-harmony:stash->close', stashId) --- this is the line 
end
```

## Only if you're using qb-inventory (version 2.0.0+)
Find the `qb-inventory:server:closeInventory` Register Net Event in `server/main.lua` and then add this event at the end of it


```lua
TriggerEvent('keep-harmony:stash->close', stashId)
```

after editing the Register Net Event. The modified function should look like this:


```lua
RegisterNetEvent('qb-inventory:server:closeInventory', function(inventory)
    local src = source
    local QBPlayer = QBCore.Functions.GetPlayer(src)
    if not QBPlayer then return end
    Player(source).state.inv_busy = false
    if inventory:find('shop%-') then return end
    if inventory:find('otherplayer%-') then
        local targetId = tonumber(inventory:match('otherplayer%-(.+)'))
        Player(targetId).state.inv_busy = false
        return
    end
    if Drops[inventory] then
        Drops[inventory].isOpen = false
        if #Drops[inventory].items == 0 and not Drops[inventory].isOpen then -- if no listeed items in the drop on close
            TriggerClientEvent('qb-inventory:client:removeDropTarget', -1, Drops[inventory].entityId)
            Wait(500)
            local entity = NetworkGetEntityFromNetworkId(Drops[inventory].entityId)
            if DoesEntityExist(entity) then DeleteEntity(entity) end
            Drops[inventory] = nil
        end
        return
    end
    if not Inventories[inventory] then return end
    Inventories[inventory].isOpen = false
    TriggerEvent('keep-harmony:stash->close', stashId)
    MySQL.prepare('INSERT INTO inventories (identifier, items) VALUES (?, ?) ON DUPLICATE KEY UPDATE items = ?', { inventory, json.encode(Inventories[inventory].items), json.encode(Inventories[inventory].items) })
end)
```

And then add this export at the end of `server/main.lua`:

```lua
exports('GetInventoryData', function(type, id)
	if type == 'stash' then
		return Stashes[id]
	end
end)
```

Copy, and paste the code below at the end of `server/functions.lua1` ONLY FOR qb-inventory (version 2.0.0)
```lua
exports('GetInventory', function (id)
    return Inventories[id]
end)

exports('SetInventoryItems', function (id, items)
    if not Inventories[id] then return end
    Inventories[id].items = items

    -- for slot, item in pairs(items) do item.description = nil end
    items = json.encode(items)
    MySQL.prepare('INSERT INTO inventories (identifier, items) VALUES (?, ?) ON DUPLICATE KEY UPDATE items = ?', { id, items, items })

    return Inventories[id].items
end)
```


- done
