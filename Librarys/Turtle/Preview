local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/miroeramaa/TurtleLib/main/TurtleUiLib.lua"))()
local window = library:Window("Window")
-- Name of button, callback

window:Button("Button name", function()
   print("pressed button")
end)

-- Name of the toggle, default state of the toggle, callback

window:Toggle("Example toggle", true, function(bool)
    print(bool) -- bool is true or false depending on the state of the toggle
end)

-- Name of slider, minimum value, maximum value, default value, callback

window:Slider("Example Slider",0,100,20, function(value)
   print(value)
end)

-- Text, color: setting color to true will give it a rainbow effect!

window:Label("Credits to Intrer#0421", Color3.fromRGB(127, 143, 166))


-- Name, callback

window:Box("Walkspeed", function(text, focuslost)
   if focuslost then
   print(text)
   end
end)
-- The callback will be called with two arguments, the text that the player inputted and whether the player has stopped writing

-- Name, table with names of the button that you want, callback that will be called with the name of the button that was pressed

local dropdown = window:Dropdown("Example dropdown", {"Button 1", "Button 2", "Third button"}, function(name)
   print(name)
end)

-- Name

dropdown:Button("New button")

-- Key

library:Keybind("P")
