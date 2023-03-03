local _, library = pcall(loadstring(game:HttpGet("https://raw.githubusercontent.com/TrixAde/Osmium/main/OsmiumLibrary.lua")))

local window = library:CreateWindow("Osmium UI Library")

local test = window:CreateTab("Main")
local info = window:CreateTab("Info")
local cred = window:CreateTab("Credits")

local dropdown = test:CreateDropdown("DropDown Exemple",{"Nami","Robin","Yamato"},function(val)
	print(val)
end)

local label = test:CreateLabel("This is a Title","this is an exemple of description")

local sld = test:CreateSlider("Slider Exemple",-100,100,function(arg)
	game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = arg
end)

test:CreateTextbox("TextBox Exemple", function(value)
    print("Value = ", value)
end, "Write Here")

local toggle = test:CreateToggle("Toggle Exemple",false,function()
    
end)

local batp = test:CreateButton("Button Exemple", function()
    print("c")
end)

local label = info:CreateLabel("KeyBind :","KeyBind to Close/Open the Gui Is 'Left Control'")

local label = cred:CreateLabel("Interface :","Made by Trix#2794")
local label = cred:CreateLabel("Interface Scripts :","Made by Trix#2794")
local label = cred:CreateLabel("Scripting :","by Trix#2794 / JulMan#1234")
local batp = cred:CreateButton("Copy Discord Server Link", function()
    setclipboard("discord.gg/TT3y4gkJtq")
end)
