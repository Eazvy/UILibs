local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/laagginq/ui-libraries/main/coastified/src.lua"))()
local Window = Lib:Window("ui lib", "pro haxxx", Enum.KeyCode.RightShift)
local Test = Window:Tab("Silent Aimbot")

Test:Toggle('Enabled',function(state)
    print(state)
end)


Test:Slider('Fov Size',1,200,75,function(Value)
    print(Value)
end)

Test:Colorpicker("Color",Color3.fromRGB(0,0,0), function(color)
    print(color)
end)

Test:Dropdown("Part",{'Head',"UpperTorso","HumanoidRootPart","LowerTorso"}, function(objective)
    print(objective)
end)
