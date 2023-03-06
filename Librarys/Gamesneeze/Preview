local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/frel0/gamesneeze-ui/main/main.lua"))()

local Window = Library:New({Name = "Read If Gay", Style = 1, PageAmmount = 7, Size = Vector2.new(554, 629)})

-- Window:SetName("string")
-- Window:Unload()
-- Theres way more functions in the documentations. Check them out if you want to.

local Page = Window:Page({Name = "General"})
local Page2 = Window:Page({Name = "Player List"})

local Section = Page:Section({Name = "Aimbot", Fill = false, Side = "Left"})

local Label = Section:Label({Name = "Main Section", Center = true, Flag = "Section_Label"})

local Toggle = Section:Toggle({Name = "Aimbot Enabled", Default = false, Callback = function(State) 
    print(State) 
end, Flag = "Section_Toggle"
})

-- Toggle:Set(true)

local ToggleWKeybind = Section:Toggle({Name = "Aimbot Enabled (w/ key)", Default = false, Callback = function(State) 
    print(State) 
end, Flag = "Section_Toggle"
})

ToggleWKeybind:Keybind()

local Slider = Section:Slider({Name = "Aimbot FOV", default = 60, minimum = 0, maximum = 180, Callback = function(State)
    print(State) 
end})

-- Toggle:Set(25)

local Button = Section:Button({Name = "Reset Aimbot", Callback = function() 
    print("what the fuck!!") 
end, Flag = "Section_Button"
})

local Dropdown = Section:Dropdown({Name = "Prioritize Hitbox", Default = "Head", Options = {"Head", "Torso", "Legs", "Arms", "Upper", "Lower"}, Max = 6 , Callback = function(State) 
    print(State) 
end, Flag = "Section_Dropdown"
})

local Multibox = Section:Multibox({Name = "Hitboxes Allowed", Default = {"Head", "Torso"}, Options = {"Head", "Torso", "Legs", "Arms", "Upper", "Lower"}, Min = 1, Max = 6, Callback = function(State) 
    for i,v in pairs(State) do -- this doenst work but whateva, figure it out urself
        print(State)
    end
end, Flag = "Section_Multibox"
})

local Keybind = Section:Keybind({Name = "Aimbot Keybind", Default = Enum.KeyCode.E, KeybindName = "Random Keybind xD", Mode = "Toggle", Callback = function(Input, State) 
    print(Input, State) 
end, Flag = "Section_Keybind"
})

local Colorpicker = Section:Colorpicker({Name = "Target ESP Color", Default = Color3.fromRGB(255, 0, 0), Alpha = 0.25, Info = "colorpciker info 123", Callback = function(Color, Transparency) 
    print(Color, Transparency) 
    end, Flag = "Section_Colorpicker"
})

-- Player List
local PlayerList = Page2:PlayerList({})

Window:Initialize()
