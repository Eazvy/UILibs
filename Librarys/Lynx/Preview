local lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/ScriptsLynX/LynX/main/UI-Library/Source.lua"))()

local win = lib:Window("LynX",Color3.fromRGB(229,49,90))

local page1 = win:Page("FirstPage","7072978559")
local page2 = win:Page("SecondPage","7072718524")

local section1 = page1:Section("Section 1")
local section2 = page1:Section("Section 2")
local section3 = page2:Section("Section 3")

section1:Label("Simple Label")
section1:TinyLabel("Tiny Label")

section1:Button("Nice Button",function()
    print("Hi")
end)

section1:Toggle("Nice Toggle 1",false,function(state)
    lib:Notify("Notification",state,3)
end)

section1:Toggle("Nice Toggle 2",true,function(state)
    print(state)
end)

section1:Slider("Nice Slider",1,100,50,function(state)
    game:GetService("Players").LocalPlayer.Character:WaitForChild("Humanoid").WalkSpeed = state
end)

section2:TextBox("Nice Textbox","0-100",function(state)
    print(state)
end)

section2:Dropdown("Nice Dropdown",{"Nice","Dropdown","LynX"},function(state)
    print(state)
end)

section2:KeyBind("Nice Keybind",function()
    print("Binded")
end)

LoadPage("FirstPage")
