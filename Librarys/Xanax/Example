--Made by : https://v3rmillion.net/member.php?action=profile&uid=516055

local XanaxUILib = loadstring(game:HttpGet("https://pastebin.com/raw/XZz3Ytbu"))()
local Ui = XanaxUILib:CreateWindow("Example UI")
local Info = Ui:CreateSection("Info")
local ExampleSection = Ui:CreateSection("Example")

Info:CreateLabel("Made by Dylan Exploits#9999")
Info:CreateLabel("This is a UI Library example")
Info:CreateButton("Destroy UI", function() XanaxUILib.functions:DestroyGUI() end)

ExampleSection:CreateLabel("This is label")
ExampleSection:CreateButton("This is button", function() print("This is function") end)
ExampleSection:CreateToggle("This is toggle", "This is flag", function(Toggled) print("This is optional argument", Toggled) end)
ExampleSection:CreateSlider("This is walkspeed slider", "WalkSpeed", 16, 100, false, function(ws)
   game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = ws
end)
ExampleSection:CreateDropdown("Gender", "Default Text", "GenderFlag", {"Gay", "Lesbian", "Bi", "Nigga", "White"}, function(chosenOption)
   if chosenOption == "Gay" then
       local m = Instance.new("Message")
       m.Parent = game.CoreGui
       m.Text = "Allahu Akbar Sweetie"
       wait(2)
       Instance.new("Explosion", game.Players.LocalPlayer.Character.HumanoidRootPart)
       m:Destroy()
       return
   end
   print("ur safe my dude")
end)
