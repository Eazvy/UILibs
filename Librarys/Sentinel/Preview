local Library = loadstring(game:HttpGet('https://raw.githubusercontent.com/astraln/SentinelUILIB/main/UI.lua', true))()

local window = Library:Window('Sentinel')

local tab = window:Tab('Home')

tab:Button('Button', function()
   
end)

tab:Toggle('Toggle',false, function(t)
   
end)

tab:Label("Label")

tab:Keybind("Keybind", Enum.KeyCode.E, function(t)
   
end)

local dropdown = tab:Dropdown("Dropdown", {"1", "2",'3','4','5','6','7','8'}, function(item)
    print(item)
end)

tab:Button('Refresh', function()
    dropdown:RefreshDropdown({'69'})
end)

tab:Slider("Slider", 16, 1000, 16, function()

end)
