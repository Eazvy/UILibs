local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/Revenant", true))()
local Flags = Library.Flags
--Library.DefaultColor = Color3.fromRGB(65, 143, 232)

local Window = Library:Window({
   Text = "Aiming"
})

local Window2 = Library:Window({
   Text = "Fun"
})

local Window3 = Library:Window({
   Text = "Settings"
})

Window:Toggle({
   Text = "Aimbot",
   Callback = function()
       print("Aimbot")
   end
})

Window:Button({
   Text = "Reload",
   Callback = function(bool)
       Library:Notification({
           Text = "Your gun has been reloaded.",
           Duration = 5
       })
   end
})

Window:Toggle({
   Text = "Silent-Aim",
   Callback = function(bool)
       print(bool)
   end
})

local Toggle = Window:Toggle({
   Text = "No-Recoil",
   Flag = "TestFlag",
   Callback = function(bool)
       print(bool)
   end
})

Window2:Button({
   Text = "Fling All",
   Callback = function()
       print("Flinging all")
   end
})

Window2:Button({
   Text = "Get Items",
   Callback = function()
       print("Got items")
   end
})

Window2:Toggle({
   Text = "Fly",
   Callback = function()
       print("weeeeeee")
   end
})

Window2:Button({
   Text = "Suicide",
   Callback = function()
       print("Don't do that please..")
   end
})

Window2:Button({
   Text = "God Mode",
   Callback = function()
       print("Nah you more like devil cuz you sexy asf")
   end
})

Window3:Dropdown({
   Text = "Color Scheme",
   List = {"Dark", "White", "Aqua","Nova"},
   Callback = function(bool)
       print(bool)
   end
})

Window3:Button({
   Text = "Kill Client",
   Callback = function()
       game:Shutdown()
   end
})

Window3:Slider({
   Text = "Test Slider",
   Default = 10,
   Minimum = 1,
   Maximum = 50,
   Callback = function(value)
       print(value)
   end
})

local Label
Window3:Prompt({
   Text = "Join our discord!",
   OnConfirm = function()
       Library:Notification({
           Text = "Thanks for joining our discord!",
           Duration = 10
       })
       Label:Set({
           Text = "Status: Joined Discord",
           Color = Color3.fromRGB(56, 207, 154)
       })
   end
})

Label = Window3:Label({
   Text = "Status: ...",
   Color = Color3.fromRGB(214, 214, 214)
})

Window3:Keybind({
   Text = "Toggle Library",
   Default = Enum.KeyCode.F4,
   Callback = function()
       Library:Toggle()
   end
})

Window3:Check({
   Text = "Mode",
   Callback = function()
       warn("Why did i add this lol")
   end
})

wait(2)
Toggle:Set({
   Bool = true
})

while true do
   if Flags.TestFlag then
       warn("Toggled")
   end
   wait(1)
end
