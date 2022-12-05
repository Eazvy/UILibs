local Finity = loadstring(game:HttpGet("https://raw.githubusercontent.com/LocalSmail/Finity/main/Library"))()


local FinityWindow = Finity.new("Finity Menu", true, false, "Example") 
FinityWindow.ChangeToggleKey("Semicolon")
local VisualsCategory = FinityWindow:Category("Visuals")
local AimbotCategory = FinityWindow:Category("Aimbot")
-- Visuals Sectors
local VisualsESPSettings = VisualsCategory:Sector("ESP Settings")
local VisualsPlayerESP = VisualsCategory:Sector("Player ESP")
local VisualsItemESP = VisualsCategory:Sector("Item ESP")
-- Aimbot Sectors
local AimbotColors = AimbotCategory:Sector("Aimbot Colors")
local AimbotHotkeys = AimbotCategory:Sector("Aimbot Hotkeys")
local AimbotConfigurations = AimbotCategory:Sector("Aimbot Configurations")
-- Uncondensed
VisualsESPSettings:Cheat(
	"Checkbox", -- Type
	"ESP Enabled", -- Name
	function(State) -- Callback function
		print("Checkbox state changed:", State)
	end
)

-- Condensed
VisualsESPSettings:Cheat("Checkbox", "ESP Enabled", function(State)
	print("Checkbox state changed:", State)
end)





-- Visuals Textboxes
VisualsItemESP:Cheat("Textbox", "Item To Whitelist", function(Value)
	print("Textbox value changed:", Value)
end, {
	placeholder = "Item Name"
})
VisualsPlayerESP:Cheat("Textbox", "Player To Whitelist", function(Value)
	print("Textbox value changed:", Value)
end, {
	placeholder = "Player Name"
})

-- Aimbot Textboxes
AimbotColors:Cheat("Textbox", "BrickColor Input", function(Value)
	print("Textbox value changed:", Value)
end, {
	placeholder = "BrickColor"
})
AimbotHotkeys:Cheat("Textbox", "Quick Toggle Hotkey", function(Value)
	print("Textbox value changed:", Value)
end, {
	placeholder = "KeyCode"
})
AimbotHotkeys:Cheat("Textbox", "Panic Hotkey", function(Value)
	print("Textbox value changed:", Value)
end, {
	placeholder = "KeyCode"
})

VisualsPlayerESP:Cheat("Button", "Reset Whitelist", function()
	print("Button pressed")
end)

AimbotColors:Cheat("Button", "Reset Color", function()
	print("Button pressed")
end)

AimbotHotkeys:Cheat("Button", "Reset Key", function()
	print("Button pressed")
end)

-- Create category
local CreditsCategory = FinityWindow:Category("Credits")

-- Create sectors
local CreditsCreator = CreditsCategory:Sector("Finity Library Creator")
local CreditsSpecialThanks = CreditsCategory:Sector("Special Thanks")
local CreditsTesters = CreditsCategory:Sector("Testers")

-- Create labels
CreditsCreator:Cheat("Label", "detourious @ v3rmillion.net")
CreditsCreator:Cheat("Label", "deto#7612 @ discord.gg")

CreditsSpecialThanks:Cheat("Label", "wallythebird - held me hostage")
CreditsSpecialThanks:Cheat("Label", "Jan - some inspiration from his lib showcase")
CreditsSpecialThanks:Cheat("Label", "& all of you for supporting me <3")

CreditsTesters:Cheat("Label", "detourious - made the darn thing")


