# linden-inventory-css-edited
https://github.com/thelindat/linden_inventory

This css edited for Revolution Indonesia Roleplay

For now, its just works for 1080 Resolution, will update it later for 1080 below

Dont forget to remove hotkey 5 on client/main.lua. since i just use 4 hotbar

Dont forget to load image on your fxmanifest

    "html/give.png", 
    "html/drop.png",
    "html/use.png",
    
Put Weight.png to html/images

just edited css for linden-inventory. inspired by NoPixel.3.0

https://i.imgur.com/p6OwrvT.png

If you want the Give Button works to show nearby players

go to client/main.lua and replace giveitem nuicallback with this

""RegisterNUICallback('giveItem', function(data, cb)
    if data.player then
        if data.inv == 'Playerinv' then
            if data.amount >= 1 then
                TriggerServerEvent('linden_inventory:giveItem', data, data.player)
                TriggerEvent('randPickupAnim')
            else 
				exports['rv-notify']:Icon({
					style = 'error', 
					title = 'Inventory',
					duration = 3000, 
					message = _U('give_amount'),
					icon = "fas fa-archive"
				}) end
        end
    else
        local players = ESX.Game.GetPlayersInArea(playerCoords, 3.0)
        if players ~= nil then
            for i = 1, #players do
                players[i] = GetPlayerServerId(players[i])
            end
            SendNUIMessage({
                message = 'nearPlayers',
                players = players,
                data = data
            })
        end
    end
end)""
