--Kavo Example
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()

local Window = Library.CreateLib("Kavo Hub", "DarkTheme")
local Tab = Window:NewTab("Main")
local Section = Tab:NewSection("LocalPlayer")


Section:NewButton("Godmode", "ButtonInfo", function()
    print("Clicked")
end)

Section:NewToggle("Kill All", "ToggleInfo", function(state)
    if state then
        print("Toggle On")
    else
        print("Toggle Off")
    end
end)
Section:NewSlider("Walkspeed", "SliderInfo", 500, 0, function(s) -- 500 (MaxValue) | 0 (MinValue)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = s
end)
Section:NewTextBox("Jumppower", "TextboxInfo", function(txt)
	print(txt)
end)

Section:NewKeybind("Toggle UI", "KeybindInfo", Enum.KeyCode.F, function()
	print("You just clicked the bind")
end)



Section:NewDropdown("Select Body Part", "DropdownInf", {"Option 1", "Option 2", "Option 3"}, function(currentOption)
    print(currentOption)
end)

Section:NewColorPicker("Select Color", "Color Info", Color3.fromRGB(0,0,0), function(color)
    print(color)
    -- Second argument is the default color
end)
