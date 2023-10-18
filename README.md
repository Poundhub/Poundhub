local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Pound hub", "DarkTheme")
local Tab = Window:NewTab("auto")
local Section = Tab:NewSection("blade ball")
Section:NewButton("ButtonText", "ButtonInfo", function()
    _G.UI_Size = 20 -- config ui size
loadstring(game:HttpGet("https://raw.githubusercontent.com/3345-c-a-t-s-u-s/-beta-/main/AutoParry.lua"))()
end)
local Tab = Window:NewTab("fly")
local Section = Tab:NewSection("fly")
Section:NewButton("ButtonText", "ButtonInfo", function()
 loadstring("\108\111\97\100\115\116\114\105\110\103\40\103\97\109\101\58\72\116\116\112\71\101\116\40\40\39\104\116\116\112\115\58\47\47\103\105\115\116\46\103\105\116\104\117\98\117\115\101\114\99\111\110\116\101\110\116\46\99\111\109\47\109\101\111\122\111\110\101\89\84\47\98\102\48\51\55\100\102\102\57\102\48\97\55\48\48\49\55\51\48\52\100\100\100\54\55\102\100\99\100\51\55\48\47\114\97\119\47\101\49\52\101\55\52\102\52\50\53\98\48\54\48\100\102\53\50\51\51\52\51\99\102\51\48\98\55\56\55\48\55\52\101\98\51\99\53\100\50\47\97\114\99\101\117\115\37\50\53\50\48\120\37\50\53\50\48\102\108\121\37\50\53\50\48\50\37\50\53\50\48\111\98\102\108\117\99\97\116\111\114\39\41\44\116\114\117\101\41\41\40\41\10\10")()
end)
local Tab = Window:NewTab("acs")
local Section = Tab:NewSection("farm")
Section:NewButton("ButtonText", "ButtonInfo", function()
 loadstring(game:HttpGet('https://raw.githubusercontent.com/SKOIXLL/RIVERHUB-SKYHUB/main/WL.lua'))();
 end)
 -- teleports a unit to a location
-- author Putnam
-- edited by expwnent
--@module = true
--[====[

teleport
========
Teleports a unit to given coordinates.

.. note::

    `gui/teleport` is an in-game UI for this script.

Examples:

* prints ID of unit beneath cursor::

    teleport -showunitid

* prints coordinates beneath cursor::

    teleport -showpos

* teleports unit ``1234`` to ``56,115,26``

    teleport -unit 1234 -x 56 -y 115 -z 26

]====]

function teleport(unit,pos)
 dfhack.units.teleport(unit, pos)
end

local utils = require('utils')

local validArgs = utils.invert({
 'unit',
 'x',
 'y',
 'z',
 'showunitid',
 'showpos'
})

if moduleMode then
 return
end

local args = utils.processArgs({...}, validArgs)

if args.showunitid or args.showpos then
 if args.showunitid then
  print(dfhack.gui.getSelectedUnit(true).id)
 else
  printall(df.global.cursor)
 end
else
 local unit = tonumber(args.unit) and df.unit.find(tonumber(args.unit)) or dfhack.gui.getSelectedUnit(true)
 local pos = not(not args.x or not args.y or not args.z) and {x=args.x,y=args.y,z=args.z} or {x=df.global.cursor.x,y=df.global.cursor.y,z=df.global.cursor.z}
 if not unit then qerror('A unit needs to be selected or specified. Use teleport -showunitid to get a unit\'s ID.') end
 if not pos.x or pos.x==-30000 then qerror('A position needs to be highlighted or specified. Use teleport -showpos to get a position\'s exact xyz values.') end
 teleport(unit,pos)
end
