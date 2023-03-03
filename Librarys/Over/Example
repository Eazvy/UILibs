local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Patskorn/GUI/main/Copy-SynapOver.lua"))()

local GUI = library:new("SynapOver","[ RightControl ]")
local Tab1 = GUI:Tap("Menu 1")
local Tab2 = GUI:Tap("Menu 2")

Tab1:Button("Button",function()
    print("Button")
end)

Tab1:Label("Label")

Tab1:Toggle("Toggle",nil,function(value)
    print(value)
end)

Tab1:Line()

Tab1:Dropdown("Dropdown",{"test1","test3"},function(t)
    print(t)
end)

Tab1:TextBox("TextBox",function(value)
    print(value)
end)
Tab1:Slider("Slider",1,100,5,function(value)
    print(value)
end)
