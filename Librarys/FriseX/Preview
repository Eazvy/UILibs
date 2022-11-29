local omni = loadstring(game:HttpGet("https://raw.githubusercontent.com/TweedLeak-LeakScripts/FriseX/main/UI-Library"))()

local UI = omni.new({
    Name = "🔮 Frise X v1.1.2 🔮";
    Credit = "Created by Frise X";
    Color = Color3.fromRGB(122,28,187);
    Bind = "LeftControl";
    UseLoader = false;
    FullName = "Frise X v1.1.2";
    CheckKey = function(inputtedKey)
        return inputtedKey=="123"
    end;
    Discord = "IDI NAHUY";
})

local notifSound = Instance.new("Sound",workspace)
notifSound.PlaybackSpeed = 1
notifSound.Volume = 0.35
notifSound.SoundId = "rbxassetid://5829559206"
notifSound.PlayOnRemove = true
notifSound:Destroy()

UI:Notify({
  Title = "Welcome!";
  Content = "Toggle Hub 'LeftControl'";
})

local Pages = UI:CreatePage("Rag. Engine 🌈")

local Section = Pages:CreateSection("Ragdoll Engine (Toggles)")

Section:CreateToggle({
    Name = "🛡 Anti Kill";
    Flag = "MyToggle";
    Default = false;
    Callback = function(state)
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.15
        notifSound.SoundId = "rbxassetid://4590662766"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    if state then
    loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/Anti_Kill.lua"))()
    elseif not state then
    end
    end;
})

Section:CreateToggle({
    Name = "🛡 Anti Ragdoll";
    Flag = "MyToggle2";
    Default = false;
    Callback = function(state)
    game.Players.LocalPlayer.Character.Humanoid.Sit = false
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.15
        notifSound.SoundId = "rbxassetid://4590662766"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
if state then
plrs = game:GetService("Players")
plr = plrs.LocalPlayer
char = plr.Character
char.HumanoidRootPart.Size = Vector3.new(1000000, char.HumanoidRootPart.Size.Y, 1000000)
for i, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
   if string.find(v.Name, "Pushed") then
       v.Disabled = true
   end
end
for i, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
   if string.find(v.Name, "RagdollMe") then
       v.Disabled = true
   end
end
game.Players.LocalPlayer.Character.Humanoid.Died:connect(function()
plrs = game:GetService("Players")
plr = plrs.LocalPlayer
char = plr.Character
char.HumanoidRootPart.Size = Vector3.new(0.98, 1.62, 0.7225, char.HumanoidRootPart.Size.Y, 0.98, 1.62, 0.7225)
end)
elseif not state then
plrs = game:GetService("Players")
plr = plrs.LocalPlayer
char = plr.Character
char.HumanoidRootPart.Size = Vector3.new(0.98, 1.62, 0.7225, char.HumanoidRootPart.Size.Y, 0.98, 1.62, 0.7225)
for i, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
   if string.find(v.Name, "Pushed") then
       v.Disabled = false
   end
end
for i, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
   if string.find(v.Name, "RagdollMe") then
       v.Disabled = false
   end
end
end
    end;
})

Section:CreateToggle({
    Name = "🛡 Anti Fling";
    Flag = "MyToggle3";
    Default = false;
    Callback = function(state)
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.15
        notifSound.SoundId = "rbxassetid://4590662766"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
if state then
loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/Anti_Fling.lua"))()
elseif not state then
local h, n = sethiddenprop or sethiddenproperty or set_hidden_prop, "Default^0^511"
h(workspace,"CollisionGroups",n)

_G.Activo = false
repeat wait()
for i, v in pairs(game.Players:GetDescendants()) do
if v.Name == "InSide" then
v:Destroy()
end
end
for i, v in pairs(game.Players:GetDescendants()) do
if v.Name == "Cap" then
v:Destroy()
end
end
until _G.Activo == false
end
    end;
})

local Section2 = Pages:CreateSection("Ragdoll Engine (Need Potion)")

Section2:CreateInteractable({
    Name = "❗Crash Server (Big Head)❗";
    ActionText = "Crash";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.15
        notifSound.SoundId = "rbxassetid://2899948244"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/crash.lua"))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.15
        notifSound.SoundId = "rbxassetid://458243346"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
    Warning = "Crash: you need potion (Effect BIG HEAD) \n Your avatar must be similar to this avatar:\n www.roblox.com/users/3365409872/profile";
    WarningIcon = 11453115091;
})

Section2:CreateInteractable({
    Name = "👑Super Fling (BETA)";
    ActionText = "Fling";
    Callback = function()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/super_fl.lua"))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.15
        notifSound.SoundId = "rbxassetid://1584394759"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
    Warning = "Super Fling: drink your potion and Execute!\n Binds: F1, F2, F3, F4, F5, F6";
    WarningIcon = 11453115091;
})

Section2:CreateInteractable({
    Name = "💥Big Accessory (drink potion)";
    ActionText = "Execute";
    Callback = function()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/big%20access.lua"))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://1584394759"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
    Warning = "Big Accessory: drink your potion and Execute!";
    WarningIcon = 11453115091;
})

Section2:CreateToggle({
    Name = "🏈 Potion Fling";
    Flag = "MyToggle4";
    Default = false;
    Callback = function(state)
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.15
        notifSound.SoundId = "rbxassetid://4590662766"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
if state then
loadstring(game:HttpGet("https://raw.githubusercontent.com/wsMalware/Malware/main/enable.lua"))()
elseif not state then
loadstring(game:HttpGet("https://raw.githubusercontent.com/wsMalware/Malware/main/disable.lua"))()
end
    end;
        Warning = "Need Potion";
    WarningIcon = 11453046100;
})


local Section3 = Pages:CreateSection("Ragdoll Engine (Button)")

Section3:CreateButton({
    Name = "🔊 Spam chat GUI";
    Callback = function()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/Spam.lua"))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
    Warning = "Spaming chat lol";
    WarningIcon = 11453115091;
})


Section3:CreateButton({
    Name = "🖱 Bypassed Chat";
    Callback = function()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/bypass%20chat.lua"))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
    Warning = "Bypassed chat - anti ban";
    WarningIcon = 11453115091;
})

Section3:CreateButton({
    Name = "🎈 Flip (Toggle Z,X,C)";
    Callback = function()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/flip.lua"))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
    Warning = "Flip";
    WarningIcon = 11453115091;
})

local Section4 = Pages:CreateSection("Server")

Section4:CreateInteractable({
    Name = "Server Hop";
    ActionText = "Hop";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.15
        notifSound.SoundId = "rbxassetid://876800936"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()

        local player = game.Players.LocalPlayer
        player.Character.HumanoidRootPart.CFrame = CFrame.new(143.932, 22.5, -217.049)

        loadstring(game:HttpGet('https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/hop.lua'))()
    end;
})

Section4:CreateInteractable({
    Name = "Rejoin";
    ActionText = "Rejoin";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.15
        notifSound.SoundId = "rbxassetid://876800936"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()

        local player = game.Players.LocalPlayer
        player.Character.HumanoidRootPart.CFrame = CFrame.new(143.932, 50.5, -217.049)

        local TeleportService = game:GetService("TeleportService")
        local Players = game:GetService("Players")
        local LocalPlayer = Players.LocalPlayer
        local Rejoin = coroutine.create(function()
        local Success, ErrorMessage = pcall(function()
        TeleportService:Teleport(game.PlaceId, LocalPlayer)
    end)
    if ErrorMessage and not Success then
        warn(ErrorMessage)
    end
end)
coroutine.resume(Rejoin)
    end;
})




local Pages2 = UI:CreatePage("Teleport 🚀")

local Section = Pages2:CreateSection("Teleport")

Section:CreateInteractable({
    Name = "🪂 Balloon";
    ActionText = "Teleport to";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.20
        notifSound.SoundId = "rbxassetid://876800936"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local player = game.Players.LocalPlayer
        player.Character.HumanoidRootPart.CFrame = CFrame.new(-118, 20.696, -134)
    end;
})

Section:CreateInteractable({
    Name = "💧 Pool";
    ActionText = "Teleport to";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.20
        notifSound.SoundId = "rbxassetid://876800936"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local player = game.Players.LocalPlayer
        player.Character.HumanoidRootPart.CFrame = CFrame.new(-133.068, 62.5, -316.049)
    end;
})

Section:CreateInteractable({
    Name = "🕋 Big building";
    ActionText = "Teleport to";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.20
        notifSound.SoundId = "rbxassetid://876800936"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local player = game.Players.LocalPlayer
        player.Character.HumanoidRootPart.CFrame = CFrame.new(140.932, 1030.698, -191.049)
    end;
})

Section:CreateInteractable({
    Name = "🖇 Stairs";
    ActionText = "Teleport to";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.20
        notifSound.SoundId = "rbxassetid://876800936"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local player = game.Players.LocalPlayer
        player.Character.HumanoidRootPart.CFrame = CFrame.new(-6.068, 200.499, -512.049)
    end;
})

Section:CreateInteractable({
    Name = "🌌 Spiral stairs";
    ActionText = "Teleport to";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.20
        notifSound.SoundId = "rbxassetid://876800936"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local player = game.Players.LocalPlayer
        player.Character.HumanoidRootPart.CFrame = CFrame.new(151.932, 844.501, -300.049)
    end;
})

Section:CreateInteractable({
    Name = "🌫 Moving stairs";
    ActionText = "Teleport to";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.20
        notifSound.SoundId = "rbxassetid://876800936"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local player = game.Players.LocalPlayer
        player.Character.HumanoidRootPart.CFrame = CFrame.new(-215.068, 84.499, -224.049)
    end;
})

Section:CreateInteractable({
    Name = "🗑 Bunker";
    ActionText = "Teleport to";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.20
        notifSound.SoundId = "rbxassetid://876800936"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local player = game.Players.LocalPlayer
        player.Character.HumanoidRootPart.CFrame = CFrame.new(143.932, 22.5, -217.049)
    end;
})

Section:CreateInteractable({
    Name = "💣 Minefield";
    ActionText = "Teleport to";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.20
        notifSound.SoundId = "rbxassetid://876800936"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local player = game.Players.LocalPlayer
        player.Character.HumanoidRootPart.CFrame = CFrame.new(-62.068, 20.5, -112.049)
    end;
})

Section:CreateInteractable({
    Name = "🚀 Long road";
    ActionText = "Teleport to";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.20
        notifSound.SoundId = "rbxassetid://876800936"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local player = game.Players.LocalPlayer
        player.Character.HumanoidRootPart.CFrame = CFrame.new(17.932, 20.5, 662.951)
    end;
})

Section:CreateInteractable({
    Name = "⚰ Center";
    ActionText = "Teleport to";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.20
        notifSound.SoundId = "rbxassetid://876800936"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local player = game.Players.LocalPlayer
        player.Character.HumanoidRootPart.CFrame = CFrame.new(-6.068, 20.5, -228.049)
    end;
})





local Pages3 = UI:CreatePage("FE scripts 🧙‍")

local Section = Pages3:CreateSection("FE scripts")

Section:CreateInteractable({
    Name = "🧥 FE Nazi R15/R6";
    ActionText = "Execute";
    Warning = "Bind 'Q' ";
    WarningIcon = 11453115091;
    Callback = function()
        loadstring(game:HttpGet('https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/fe_naz.lua'))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})

Section:CreateInteractable({
    Name = "🔧 FE Dick R15";
    ActionText = "Execute";
    Warning = "Bind 'Q' ";
    WarningIcon = 11453115091;
    Callback = function()
        loadstring(game:HttpGet('https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/dick.lua'))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})

Section:CreateInteractable({
    Name = "🎃 Headless";
    ActionText = "Execute";
    Callback = function()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/hdless.lua"))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})


local Section2 = Pages3:CreateSection("FE fling")

Section2:CreateInteractable({
    Name = "🌜 FE Amogous";
    ActionText = "Execute";
    Warning = "Bind 'Q, Z, X' ";
    WarningIcon = 11453115091;
    Callback = function()
        loadstring(game:HttpGet('https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/amo.lua'))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 0.8
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5799014146"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})

Section2:CreateInteractable({
    Name = "⚡ FE Instakill R15/R6";
    ActionText = "Execute";
    Warning = "Bind 'Q' ";
    WarningIcon = 11453115091;
    Callback = function()
        loadstring(game:HttpGet('https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/fe_instakill.lua'))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 0.8
        notifSound.Volume = 1.15
        notifSound.SoundId = "rbxassetid://131961137"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})

Section2:CreateInteractable({
    Name = "🖱 Click fling R15";
    ActionText = "Execute";
    Callback = function()
        loadstring(game:HttpGet('https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/clckfling.lua'))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})

local Section3 = Pages3:CreateSection("Other")

Section3:CreateInteractable({
    Name = "🎢 FE Small/Titan";
    ActionText = "Execute";
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/wsMalware/Malware/main/small.lua'))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})





local Pages4 = UI:CreatePage("Character 🙋‍♂️ ")

local Section = Pages4:CreateSection("Character (Sliders)")

Section:CreateSlider({
    Name = "WalkSpeed";
    Flag = "MySlider";
    Min = 1;
    Max = 500;
    AllowOutOfRange = true;
    Digits = 3;
    Default = 16;
    Callback = function(arg)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = arg
    end;
})

Section:CreateSlider({
    Name = "JumpPower";
    Flag = "MySlider2";
    Min = 50;
    Max = 500;
    AllowOutOfRange = true;
    Digits = 3;
    Default = 50;
    Callback = function(arg)
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = arg
    end;
})

Section:CreateSlider({
    Name = "Gravity";
    Flag = "MySlider3";
    Min = 0;
    Max = 900;
    AllowOutOfRange = false;
    Digits = 3;
    Default = 194;
    Callback = function(t)
        game.Workspace.Gravity = t 
    end;
})

Section:CreateSlider({
    Name = "FOV";
    Flag = "MySlider4";
    Min = math.floor(workspace.CurrentCamera.FieldOfView);
    Max = 120;
    AllowOutOfRange = true;
    Digits = 3;
    Default = 70;
    Callback = function(v)
        workspace.CurrentCamera.FieldOfView = v;
    end;
})


Section:CreateToggle({
    Name = "🎥 Unlock Zoom";
    Flag = "MyToggle5";
    Default = false;
    Callback = function(state)
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.15
        notifSound.SoundId = "rbxassetid://4590662766"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    if state then
    game.Players.LocalPlayer.CameraMaxZoomDistance = (999999999999999)
    elseif not state then
    game.Players.LocalPlayer.CameraMaxZoomDistance = (400)
    end
    end;
})



local Section2 = Pages4:CreateSection("Character")

Section2:CreateInteractable({
    Name = "🎭 Client Custom";
    ActionText = "Execute";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5188022160"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/wsMalware/Malware/main/client.lua"))()
    end;
})

Section2:CreateInteractable({
    Name = "🚨 Enable reset button";
    ActionText = "Execute";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        game:GetService("StarterGui"):SetCore("ResetButtonCallback", true)
        game:GetService("RunService").RenderStepped:Wait()
    end;
})

Section2:CreateInteractable({
    Name = "💭 Anti AFK";
    ActionText = "Execute";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local vu = game:GetService("VirtualUser")
        game:GetService("Players").LocalPlayer.Idled:connect(function()
        vu:Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
        wait(1)
        vu:Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
        end)
    end;
})

local Section3 = Pages4:CreateSection("Tools")

Section3:CreateInteractable({
    Name = "🌍 Click Teleport tool";
    ActionText = "Execute";
    Callback = function()
        loadstring(game:HttpGet('https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/tools/tp.lua'))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})

Section3:CreateInteractable({
    Name = "🎩 Hats Tool";
    ActionText = "Execute";
    Callback = function()
        loadstring(game:HttpGet('https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/tools/hattool.lua'))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})



local Pages5 = UI:CreatePage("Fun 💩")

local Section = Pages5:CreateSection("Emoji picture")

Section:CreateButton({
    Name = "♟ Dick";
    Callback = function()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/cocl_pic.lua"))()
    end;
})

Section:CreateButton({
    Name = "💩 Sh!t";
    Callback = function()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/shit_pic.lua"))()
    end;
})

Section:CreateButton({
    Name = "🧥 Nazi";
    Callback = function()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/naz.lua"))()
    end;
})

Section:CreateButton({
    Name = "🇺🇦 Ukraine love";
    Callback = function()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/ua.lua"))()
    end;
})

Section:CreateButton({
    Name = "🇨🇳 Russia";
    Callback = function()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/rusia.lua"))()
    end;
})

local Section2 = Pages5:CreateSection("Fun Character")

Section2:CreateInteractable({
    Name = "Ball";
    ActionText = "Load";
    Callback = function()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/fun/ball.lua", true))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})

Section2:CreateInteractable({
    Name = "Teleport to a high altitude";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local baseplate = Instance.new("Part")
        baseplate.Parent = workspace
        baseplate.Size = Vector3.new(0,0,0) -- change size
        baseplate.Anchored = false
        baseplate.Position = game.Players.LocalPlayer.Character.HumanoidRootPart.Position + Vector3.new(0,15000,0) -- higher number for it to spawn higher
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = baseplate.CFrame + Vector3.new(0,-10,0)
        game.Players.LocalPlayer.Character.LeftLowerLeg.Anchored = false
    end;
})

Section2:CreateInteractable({
    Name = "Glitch Map (Jacket)";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        for _,s in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
            if s:IsA("Motor6D") and s.Name ~= "Neck" then
                local fard = s.Parent
                s:Destroy()
                fard.CFrame = CFrame.new(10000000000000000, 10000000000000000, -10000000000000000) 
                wait()
            end
        end
    end;
})


local Pages6 = UI:CreatePage("Visuals 🔮")

local Section = Pages6:CreateSection("Time set")

Section:CreateSlider({
    Name = "Time";
    Flag = "MySlider5";
    Min = 0;
    Max = 24;
    AllowOutOfRange = true;
    Digits = 1;
    Default = 12;
    Callback = function(arg)
        game:GetService("Lighting").TimeOfDay = arg
    end;
})


local Pages7 = UI:CreatePage("Animations 🐔")

local Section = Pages7:CreateSection("Animations")

Section:CreateInteractable({
    Name = "Default";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=2510196951"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=2510197257"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=2510202577"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=2510198475"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=2510197830"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=2510192778"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=2510195892"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Toy";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=782841498"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=782845736"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=782843345"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=782842708"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=782847020"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=782843869"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=782846423"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Robot";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=616088211"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=616089559"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=616095330"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=616091570"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=616090535"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=616086039"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=616087089"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Cartoony";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=742637544"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=742638445"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=742640026"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=742638842"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=742637942"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=742636889"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=742637151"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Zombie";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=616158929"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=616160636"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=616168032"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=616163682"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=616161997"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=616156119"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=616157476"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Stylish";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=616136790"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=616138447"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=616146177"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=616140816"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=616139451"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=616133594"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=616134815"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Mage";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=707742142"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=707855907"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=707897309"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=707861613"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=707853694"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=707826056"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=707829716"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Ninja";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=656117400"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=656118341"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=656121766"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=656118852"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=656117878"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=656114359"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=656115606"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Superhero";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=616111295"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=616113536"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=616122287"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=616117076"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=616115533"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=616104706"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=616108001"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Bubbly";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=910004836"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=910009958"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=910034870"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=910025107"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=910016857"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=910001910"
        Animate.swimidle.SwimIdle.AnimationId = "http://www.roblox.com/asset/?id=910030921"
        Animate.swim.Swim.AnimationId = "http://www.roblox.com/asset/?id=910028158"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Vampire";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=1083445855"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=1083450166"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=1083473930"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=1083462077"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=1083455352"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=1083439238"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=1083443587"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Levitation";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=616006778"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=616008087"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=616013216"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=616010382"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=616008936"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=616003713"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=616005863"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Elder";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=845397899"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=845400520"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=845403856"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=845386501"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=845398858"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=845392038"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=845396048"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Pirate";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=750781874"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=750782770"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=750785693"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=750783738"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=750782230"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=750779899"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=750780242"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Werewolf";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=1083195517"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=1083214717"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=1083178339"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=1083216690"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=1083218792"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=1083182000"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=1083189019"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Astronaut";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=891621366"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=891633237"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=891667138"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=891636393"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=891627522"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=891609353"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=891617961"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})

Section:CreateInteractable({
    Name = "Knight";
    ActionText = "Load";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        local Animate = game.Players.LocalPlayer.Character.Animate
        Animate.idle.Animation1.AnimationId = "http://www.roblox.com/asset/?id=657595757"
        Animate.idle.Animation2.AnimationId = "http://www.roblox.com/asset/?id=657568135"
        Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=657552124"
        Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=657564596"
        Animate.jump.JumpAnim.AnimationId = "http://www.roblox.com/asset/?id=658409194"
        Animate.climb.ClimbAnim.AnimationId = "http://www.roblox.com/asset/?id=658360781"
        Animate.fall.FallAnim.AnimationId = "http://www.roblox.com/asset/?id=657600338"
        game.Players.LocalPlayer.Character.Humanoid.Jump = false
    end;
})



local Pages8 = UI:CreatePage("Hub's 🐬")

local Section = Pages8:CreateSection("Admin scripts")

Section:CreateInteractable({
    Name = "Infinite Yield";
    ActionText = "Load";
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})

Section:CreateInteractable({
    Name = "CMD-X";
    ActionText = "Load";
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/CMD-X/CMD-X/master/Source", true))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})

local Section2 = Pages8:CreateSection("FE animations")

Section2:CreateInteractable({
    Name = "Pendulum HUB";
    ActionText = "Load";
    Callback = function()
        loadstring(game:HttpGet("https://gitlab.com/ivanovpogorely/2323313frrf/-/raw/main/pendul.lua", true))()
    end;
})

local Section3 = Pages8:CreateSection("Ragdoll Engine Hub's")

Section3:CreateInteractable({
    Name = "MalwareHub (Toggle V)";
    ActionText = "Load";
    Callback = function()
        loadstring(game:HttpGet("https://gist.githubusercontent.com/H20CalibreYT/731b5052013a54de121debdd5e43fa6d/raw/"))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})

Section3:CreateInteractable({
    Name = "Cryptonic HUB";
    ActionText = "Load";
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/martinelcrac/cryptonichub/main/Ragdollengine.lua'))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
})

local Section4 = Pages8:CreateSection("Other")

Section4:CreateInteractable({
    Name = "Outfit changer GUI (Toggle N)";
    ActionText = "Load";
    Callback = function()
        getgenv().show = "N"
        loadstring(game:HttpGet("https://raw.githubusercontent.com/mogolicoo/techware-shit/main/outfit-changer-gui.lua", true))()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.30
        notifSound.SoundId = "rbxassetid://5568992074"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
    end;
    Warning = "See: https://streamable.com/v91ko7";
    WarningIcon = 11453115091;
})



local Pages9 = UI:CreatePage("Settings ⚙️")

local Section2 = Pages9:CreateSection("GUI")

Section2:CreateInteractable({
    Name = "Restart GUI";
    ActionText = "Restart";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.40
        notifSound.SoundId = "rbxassetid://3673835822"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        loadstring(game:HttpGet("https://pastebin.com/raw/m81DRdtE", true))()
        UI:Destroy()
    end;
})

Section2:CreateInteractable({
    Name = "Destroy GUI";
    ActionText = "Destroy";
    Callback = function()
        local notifSound = Instance.new("Sound",workspace)
        notifSound.PlaybackSpeed = 1
        notifSound.Volume = 0.40
        notifSound.SoundId = "rbxassetid://3673835822"
        notifSound.PlayOnRemove = true
        notifSound:Destroy()
        wait(5)
        UI:Destroy()
    end;
})




local Pages10 = UI:CreatePage("Credits 🎲")

local Section = Pages10:CreateSection("Credits")

Section:CreateInteractable({
    ActionText = "I'M GAY";
    Name = "Created by frise and killerses";
})

Section:CreateInteractable({
    ActionText = "I'M GAY";
    Name = "Discord frise#8792";
})

Section:CreateInteractable({
    ActionText = "I'M GAY";
    Name = "Server dsc.gg/ragdoll-crasher";
})
