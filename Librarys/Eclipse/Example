local Mommy = {
Visuals = {
    World = {
        IndoorAmbience = false,
        IndoorAmbienceColor = false,
        OutdoorAmbience = false,
        OutdoorAmbienceColor = false,
        Fog = false,
        FogColor = false,
        Saturation = false,
        SaturationAmmount = false
        },
    FOV = {
        EnableFOV = false,
        FOVAmmount = 70
        },
    },  
Player = {
    Exploits = {
        Noclip = false,
        AntiStomp = false,
        AutoStomp = false,
        AutoReload = false,
        AntiFlingEnabled = false,
        AntiFling = false,
        AntiBag = false,
        AntiSlow = false,
        AntiJumpCooldown = false,
        Bhop = false,
        JumpStrafe = false,
        JumpStrafeSpeed = 1,
        FakeLag = false,
        FakeLagAmount = 0
        },
    Movement = {
        SpeedEnabled = false,
        Speed = false,
        SpeedValue = 0/100
        },
    AntiAim = {
        Reverse = false,
        Underground = false,
        Slingshot = false
        }
    },
Miscellaneous = {
    Teleportation = {
        AutoPurchase = false,
        Return = false,
        ReturnDelay = 0
        }
    }
}
-- [Variables] ------------------------------------------------------------------------------------------------------------------------------------------------------------
local Decimals = 4
local Clock = os.clock()

local playerlist = {} for i,v in pairs(game.Players:GetPlayers())do if v ~= game.Players.LocalPlayer then table.insert(playerlist,v.Name) end end

local esp, esp_renderstep, framework = loadstring(game:HttpGet("https://raw.githubusercontent.com/dohmai/Tokyo/main/Libraries/ESP"))();
-- [Libary] ------------------------------------------------------------------------------------------------------------------------------------------------------------
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/dohmai/Tokyo/main/Libraries/UI"))({cheatname = "Tokyo", gamename = "Da Hood"})
library:init()
-- [Window UI] ------------------------------------------------------------------------------------------------------------------------------------------------------------
local menu = library.NewWindow({title = "Tokyo | Da Hood", size = UDim2.new(0, 510, 0.6, 6)})
-- [Tabs UI] ------------------------------------------------------------------------------------------------------------------------------------------------------------
local Tab1 = menu:AddTab("  Combat  ")
local Tab2 = menu:AddTab("  Player  ")
local Tab3 = menu:AddTab("  Visuals  ")
local Tab4 = menu:AddTab("  Miscellaneous  ")
local SettingsTab = library:CreateSettingsTab(menu)
-- [Combat Sections UI] ------------------------------------------------------------------------------------------------------------------------------------------------------------
local Combat1 = Tab1:AddSection("Section 1", 1)
local Combat2 = Tab1:AddSection("Section 2", 2)
-- [Combat Tab UI] ------------------------------------------------------------------------------------------------------------------------------------------------------------
local ass = Combat1:AddText({text = "Timer"})
-- [Player Sections UI] ------------------------------------------------------------------------------------------------------------------------------------------------------------
local Player2 = Tab2:AddSection("Movement", 1)
local Player1 = Tab2:AddSection("Exploits", 2)
local Player3 = Tab2:AddSection("Anti Aim", 1)
-- [Movement Tab UI] ------------------------------------------------------------------------------------------------------------------------------------------------------------
Player2:AddToggle({text = "Noclip",flag = "",callback = function(bool)
Mommy.Player.Exploits.Noclip = bool
    if Mommy.Player.Exploits.Noclip then
    NoclipLoop = game:GetService("RunService").Stepped:Connect(function()
    for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
    if v:IsA("BasePart") and v.CanCollide == true then
    v.CanCollide = false
    end
    end
    end)
    elseif Mommy.Player.Exploits.Noclip == false and NoclipLoop then
    NoclipLoop:Disconnect()
    end
end})

Player2:AddToggle({text = "Speed",flag = "",callback = function(bool)
Mommy.Player.Movement.SpeedEnabled = bool
end})

:AddBind({text = "Speed",mode = 'toggle',bind = 'None',flag = "A2",callback = function(bool)
Mommy.Player.Movement.Speed = bool
    if Mommy.Player.Movement.SpeedEnabled == true then
    for _, v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
    if v:IsA("Script") and v.Name ~= "Health" and v.Name ~= "Sound" and v:FindFirstChild("LocalScript") then
    v:Destroy()
    end
    end
    game.Players.LocalPlayer.CharacterAdded:Connect(function(char)
    repeat
    wait()
    until game.Players.LocalPlayer.Character
    char.ChildAdded:Connect(function(child)
    if child:IsA("Script") then
    wait(0.1)
    if child:FindFirstChild("LocalScript") then
    child.LocalScript:FireServer()
    end
    end
    end)
    end)
    game:GetService("RunService").Heartbeat:Connect(
    function()
    if Mommy.Player.Movement.SpeedEnabled == true then
    if Mommy.Player.Movement.Speed == true then
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame =
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame +
    game.Players.LocalPlayer.Character.Humanoid.MoveDirection * Mommy.Player.Movement.SpeedValue
    end
    end
    end)
    end
end})

Player2:AddSlider({text = "Speed",flag = "A9",suffix = "",min = 0,max = 5,increment = 0.1,callback = function(bool)
Mommy.Player.Movement.SpeedValue = bool
end})
-- [Exploits Tab UI] ------------------------------------------------------------------------------------------------------------------------------------------------------------
Player1:AddToggle({text = "Anti Stomp",flag = "",callback = function(bool)
Mommy.Player.Exploits.AntiStomp = bool
    while Mommy.Player.Exploits.AntiStomp == true do wait()
    while game.Players.LocalPlayer.Character:WaitForChild("BodyEffects")["K.O"].Value == true or game.Players.LocalPlayer.Character:FindFirstChild("GRABBING_CONSTRAINT") do wait()
    for i, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
    if v:IsA("BasePart") then
    v:Destroy()
    end
    end
    end
    end
end})

Player1:AddToggle({text = "Auto Stomp",flag = "",callback = function(bool)
Mommy.Player.Exploits.AutoStomp = bool
    if Mommy.Player.Exploits.AutoStomp == true then
    game:GetService('RunService'):BindToRenderStep("Auto-Stomp", 0 , function()
    game:GetService("ReplicatedStorage").MainEvent:FireServer("Stomp")
    end)
    elseif Mommy.Player.Exploits.AutoStomp == false then
    game:GetService('RunService'):UnbindFromRenderStep("Auto-Stomp")
    end
end})

Player1:AddToggle({text = "Auto Reload",flag = "", callback = function(bool)
Mommy.Player.Exploits.AutoReload = bool
    while Mommy.Player.Exploits.AutoReload == true and game:GetService("RunService").Heartbeat:Wait() do
    if game:GetService("Players").LocalPlayer.Character:FindFirstChildWhichIsA("Tool") then
    if game:GetService("Players").LocalPlayer.Character:FindFirstChildWhichIsA("Tool"):FindFirstChild("Ammo") then
    if game:GetService("Players").LocalPlayer.Character:FindFirstChildWhichIsA("Tool"):FindFirstChild("Ammo").Value <= 0 then
    game:GetService("ReplicatedStorage").MainEvent:FireServer("Reload", game:GetService("Players").LocalPlayer.Character:FindFirstChildWhichIsA("Tool"))
    wait(1)
    end
    end
    end
    end
end})

Player1:AddToggle({text = "Anti Fling",flag = "",callback = function(bool)
Mommy.Player.Exploits.AntiFlingEnabled = bool
end})

:AddBind({text = "Anti Fling",state = false,mode = 'toggle',bind = 'None',flag = "A2",callback = function(bool)
Mommy.Player.Exploits.AntiFling = bool
    if Mommy.Player.Exploits.AntiFlingEnabled == true then
    if Mommy.Player.Exploits.AntiFling == true then
    game.Players.LocalPlayer.Character.HumanoidRootPart.Anchored = true
    else
    if Mommy.Player.Exploits.AntiFling == false then
    game.Players.LocalPlayer.Character.HumanoidRootPart.Anchored = false
    end
    end
    end
end})

Player1:AddToggle({text = "Anti Bag",flag = "",callback = function(bool)
Mommy.Player.Exploits.AntiBag = bool
    while Mommy.Player.Exploits.AntiBag == true do wait()
    pcall(function()
    game.Players.LocalPlayer.Character["Christmas_Sock"]:Destroy()
    end)
    end
end})

Player1:AddToggle({text = "Anti Slowdown",flag = "",callback = function(bool)
Mommy.Player.Exploits.AntiSlow = bool
    if Mommy.Player.Exploits.AntiSlow == true then
    game:GetService("RunService"):BindToRenderStep("Anti-Slow",0,
    function()
    if
    game.Players.LocalPlayer.Character.BodyEffects.Movement:FindFirstChild("NoWalkSpeed")
    then
    game.Players.LocalPlayer.Character.BodyEffects.Movement:FindFirstChild("NoWalkSpeed"):Destroy()
    end
    if
    game.Players.LocalPlayer.Character.BodyEffects.Movement:FindFirstChild("ReduceWalk")
    then
    game.Players.LocalPlayer.Character.BodyEffects.Movement:FindFirstChild("ReduceWalk"):Destroy()
    end
    if
    game.Players.LocalPlayer.Character.BodyEffects.Movement:FindFirstChild("NoJumping")
    then
    game.Players.LocalPlayer.Character.BodyEffects.Movement:FindFirstChild("NoJumping"):Destroy()
    end
    if game.Players.LocalPlayer.Character.BodyEffects.Reload.Value == true then
    game.Players.LocalPlayer.Character.BodyEffects.Reload.Value = false
    end
    end)
    elseif Mommy.Player.Exploits.AntiSlow == false then
    game:GetService("RunService"):UnbindFromRenderStep("Anti-Slow")
    end
end})

Player1:AddToggle({text = "Anti Jump Cooldown",flag = "",callback = function(bool)
Mommy.Player.Exploits.AntiJumpCooldown = bool
end})

Player1:AddToggle({text = "Bhop",flag = "",callback = function(bool)
Mommy.Player.Exploits.Bhop = bool
Mommy.Player.Exploits.AntiJumpCooldown = bool
    while Mommy.Player.Exploits.Bhop == true do
    wait()
    if game.Players.LocalPlayer.Character.Humanoid:GetState() ~= Enum.HumanoidStateType.Freefall then
    game.Players.LocalPlayer.Character.Humanoid:ChangeState("Jumping")
    end
    end
end})

Player1:AddToggle({text = "Jump Strafe",flag = "",callback = function(bool)
Mommy.Player.Exploits.JumpStrafe = bool
    while Mommy.Player.Exploits.JumpStrafe do
    wait()
    if game.Players.LocalPlayer.Character.Humanoid.MoveDirection.Magnitude > 0 and game.Players.LocalPlayer.Character.Humanoid:GetState() == Enum.HumanoidStateType.Freefall then
    game.Players.LocalPlayer.Character:TranslateBy(game.Players.LocalPlayer.Character.Humanoid.MoveDirection / Mommy.Player.Exploits.JumpStrafeSpeed)
    end
    end
end})

Player1:AddSlider({text = "Jump Strafe Ammount",flag = "A9",suffix = "",min = 1,max = 5,value = 1,increment = 1,callback = function(bool)
Mommy.Player.Exploits.JumpStrafeSpeed = bool
end})

Player1:AddToggle({text = "Fake Lag",flag = "",callback = function(bool)
Mommy.Player.Exploits.FakeLag = bool
    while Mommy.Player.Exploits.FakeLag == true do
    game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Anchored = true
    wait(Mommy.Player.Exploits.FakeLagAmount)
    game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Anchored = false
    wait()
    end
end})

Player1:AddSlider({text = "Fake Lag Ammount",flag = "A9",min = 0,max = 1,increment = 0.05,callback = function(Value)
Mommy.Player.Exploits.FakeLagAmount = Value/2.5
end})
-- [AntiJumpCooldown] --
a = hookfunction(wait, function(b) if b == 1.5 and Mommy.Player.Exploits.AntiJumpCooldown then return a() end return a(b) end)
-- [Visuals Sections UI] ------------------------------------------------------------------------------------------------------------------------------------------------------------
local Visuals1 = Tab3:AddSection("World", 2)
local Visuals2 = Tab3:AddSection("ESP", 1)
local Visuals3 = Tab3:AddSection("FOV", 2)
-- FOV Tab UI] ------------------------------------------------------------------------------------------------------------------------------------------------------------
Visuals3:AddToggle({text = "Enable",flag = "",callback = function(bool)
    Mommy.Visuals.FOV.EnableFOV = bool
    if Mommy.Visuals.FOV.EnableFOV == true then
    game:GetService'Workspace'.Camera.FieldOfView = Mommy.Visuals.FOV.FOVAmmount
    end
    if Mommy.Visuals.FOV.EnableFOV == false then
    game:GetService'Workspace'.Camera.FieldOfView = 70
    end
end})

Visuals3:AddSlider({text = "FOV Ammount",flag = "A9",suffix = "",min = 70,max = 120,value = 70,increment = 5,callback = function(bool)
    Mommy.Visuals.FOV.FOVAmmount = bool
    if Mommy.Visuals.FOV.EnableFOV == true then
    game:GetService'Workspace'.Camera.FieldOfView = Mommy.Visuals.FOV.FOVAmmount
    end
end})
-- [World Tab UI] ------------------------------------------------------------------------------------------------------------------------------------------------------------
Visuals1:AddToggle({text = "Indoor Ambience",flag = "",callback = function(bool)
Mommy.Visuals.World.IndoorAmbience = bool
    if Mommy.Visuals.World.IndoorAmbience == true then
    game:GetService("Lighting").Ambient = Mommy.Visuals.World.IndoorAmbienceColor
    end
    if Mommy.Visuals.World.IndoorAmbience == false then
    game:GetService("Lighting").Ambient = Color3.fromRGB(0,0,0)
    end
end})

:AddColor({text = "Color",color = Color3.fromRGB(124,97,196),flag = "",callback = function(bool)
Mommy.Visuals.World.IndoorAmbienceColor = bool
    if Mommy.Visuals.World.IndoorAmbience == true then
    game:GetService("Lighting").Ambient = Mommy.Visuals.World.IndoorAmbienceColor
    end
end})

Mommy.Visuals.World.IndoorAmbienceColor = Color3.fromRGB(124,97,196)

Visuals1:AddToggle({text = "Outdoor Ambience",flag = "",callback = function(bool)
Mommy.Visuals.World.OutdoorAmbient = bool
    if Mommy.Visuals.World.OutdoorAmbient then
    game:GetService("Lighting").OutdoorAmbient = Mommy.Visuals.World.OutdoorAmbientColor
    end
    if Mommy.Visuals.World.OutdoorAmbient == false then
    game:GetService("Lighting").OutdoorAmbient = Color3.fromRGB(152,152,146)
    end
end})

:AddColor({text = "Color",color = Color3.fromRGB(124,97,196),flag = "",callback = function(bool)
Mommy.Visuals.World.OutdoorAmbientColor = bool
    if Mommy.Visuals.World.OutdoorAmbient then
    game:GetService("Lighting").OutdoorAmbient = Mommy.Visuals.World.OutdoorAmbientColor
    end
end})

Mommy.Visuals.World.OutdoorAmbientColor = Color3.fromRGB(124,97,196)

Visuals1:AddToggle({text = "Fog Color",flag = "",callback = function(bool)
Mommy.Visuals.World.Fog = bool
    if Mommy.Visuals.World.Fog then
    game:GetService("Lighting").FogColor = Mommy.Visuals.World.FogColor
    end
    if Mommy.Visuals.World.Fog == false then
    game:GetService("Lighting").FogColor = Color3.fromRGB(100,87,72)
    end
end})

:AddColor({text = "Color",color = Color3.fromRGB(124,97,196),flag = "",callback = function(bool)
    Mommy.Visuals.World.FogColor = bool
    if Mommy.Visuals.World.Fog then
    game:GetService("Lighting").FogColor = Mommy.Visuals.World.FogColor
    end
end})

Mommy.Visuals.World.FogColor = Color3.fromRGB(124,97,196)

Visuals1:AddToggle({text = "Saturation",flag = "",callback = function(bool)
Mommy.Visuals.World.Saturation = bool
    if Mommy.Visuals.World.Saturation then
    game.Lighting.ColorCorrection.Saturation = Mommy.Visuals.World.SaturationAmmount
    end
    if Mommy.Visuals.World.Saturation == false then
    game.Lighting.ColorCorrection.Saturation = 0
    end
end})

:AddSlider({text = "Saturation Ammount",suffix = "",min = 0,max = 5,value = 0,increment = 0.1,flag = "A9",callback = function(bool)
Mommy.Visuals.World.SaturationAmmount = bool
    if Mommy.Visuals.World.Saturation then
    game.Lighting.ColorCorrection.Saturation = Mommy.Visuals.World.SaturationAmmount
    end
end})
-- [ESP Tab UI] ------------------------------------------------------------------------------------------------------------------------------------------------------------
Visuals2:AddToggle({text = "Enable",flag = "",callback = function(bool)
getgenv().ESP = bool esp.Settings.Enabled = bool
end})

:AddBind({text = "ESP",state = false,mode = 'toggle',bind = 'None',flag = "A2",callback = function(bool)
if getgenv().ESP then
esp.Settings.Enabled = bool
end
end})

Visuals2:AddToggle({text = "Boxes",flag = "",callback = function(bool)
esp.Settings.Box.Enabled = bool
end})

:AddColor({text = "Color",flag = "", color = Color3.fromRGB(124,97,196),callback = function(bool)
esp.Settings.Box.Color = bool
end})

Visuals2:AddToggle({text = "Names",flag = "",callback = function(bool)
esp.Settings.Name.Enabled = bool
end})

:AddColor({text = "Color",flag = "",color = Color3.fromRGB(124,97,196),callback = function(bool)
esp.Settings.Name.Color = bool
end})

Visuals2:AddToggle({text = "Distance",flag = "",callback = function(bool)
esp.Settings.Distance.Enabled = bool
end})
:AddColor({text = "Color",flag = "",color = Color3.fromRGB(124,97,196),callback = function(bool)
esp.Settings.Distance.Color = bool
end})

Visuals2:AddToggle({text = "Weapon",flag = "",callback = function(bool)
esp.Settings.Tool.Enabled = bool
end})

:AddColor({text = "Color",flag = "",color = Color3.fromRGB(124,97,196),callback = function(bool)
esp.Settings.Tool.Color = bool
end})

Visuals2:AddToggle({text = "Healthbar",flag = "",callback = function(bool)
esp.Settings.Healthbar.Enabled = bool
end})


Visuals2:AddToggle({text = "Health",flag = "", callback = function(bool)
esp.Settings.Health.Enabled = bool
end})

Visuals2:AddSlider({text = "Max Distance",flag = "A9",suffix = "",min = 0,max = 500,value = 500,increment = 10,callback = function(bool)
esp.Settings.Maximal_Distance = bool
end})
-- [Miscellaneous Sections UI] ------------------------------------------------------------------------------------------------------------------------------------------------------------
local Miscellaneous2 = Tab4:AddSection("Players", 1)
local Miscellaneous3 = Tab4:AddSection("Locations", 1)
local Miscellaneous1 = Tab4:AddSection("Teleportation", 2)

-- [Miscellaneous Tab UI] ------------------------------------------------------------------------------------------------------------------------------------------------------------
local list = Miscellaneous2:AddList(
{text = "Selection", selected = "", max = 5,
values = {unpack(playerlist)},
callback = function(a)
value = a
end})

list:AddValue(game.Players.LocalPlayer)

game.Players.PlayerAdded:Connect(function(player)
local name = player.Name
table.insert(playerlist,name)
list:AddValue(player.Name)
end)

game.Players.PlayerRemoving:Connect(function(player)
local name = player.Name
for i,v in pairs(playerlist)do
if v == name then
table.remove(playerlist,i)
end
end
list:RemoveValue(player.Name)
end)

Miscellaneous2:AddButton(
{text = "Teleport",
callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[value].Character.HumanoidRootPart.CFrame
end})

local butt = Miscellaneous2:AddButton(
{text = "View",
callback = function()
workspace.Camera.CameraSubject = game:GetService("Players")[value].Character.Humanoid
end})

butt:AddButton(
{text = "Unview",
callback = function()
workspace.Camera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
end})

Miscellaneous2:AddSeparator({text = "Auto Kill"})

Miscellaneous2:AddToggle(
{text = "Auto Kill",
flag = "", callback = function(bool)

end})

Miscellaneous1:AddToggle(
{text = "Auto Purchase",
flag = "", callback = function(bool)
Mommy.Player.Exploits.AutoPurchase = bool
end})

Miscellaneous1:AddToggle(
{text = "Return",
flag = "", callback = function(bool)
Mommy.Player.Exploits.Return = bool
end})

Miscellaneous1:AddSlider({text = "Return Delay", flag = "A9",
min = 0, max = 2, increment = 0.1,
callback = function(Value)
Mommy.Player.Exploits.ReturnDelay = Value
end})

Miscellaneous3:AddList(
{text = "Selection", selected = "", max = 5,
values = {"Bank", "Casino", "School", "Playground", "Admin Base"},
callback = function(b)
valueb = b
end})

Miscellaneous3:AddButton(
{text = "Teleport",
callback = function()
if valueb == "Bank" then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-417, 23, -285)
else
if valueb == "Casino" then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1006, 25, -158)
else
if valueb == "School" then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-653, 22, 256)
else
if valueb == "Playground" then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-244, 22, -797)
else
if valueb == "Admin Base" then
  game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-798, -40, -886)
end
end
end
end
end
end})

Miscellaneous1:AddSeparator({text = "Guns"})


Miscellaneous1:AddList(
{text = "Selection", selected = "", max = 5,
values = {"Revolver", "Double Barrel", "Tactical Shotgun", "Shotgun", "Silencer", "SMG"},
callback = function(d)
valued = d
end})

Miscellaneous1:AddButton(
{text = "Teleport",
callback = function()
if valued == "Revolver" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-868, -33, -529)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old -- teleports you back to your old position
end
else
if valued == "Double Barrel" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-869, -33, -524)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old -- teleports you back to your old position
end
else
if valued == "Shotgun" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-861, -33, -529)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old -- teleports you back to your old position
end
else
if valued == "Tactical Shotgun" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(471, 48, -620)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
  game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old -- teleports you back to your old position
end
else
if valued == "Silencer" then
  local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
  game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-889, -33, -529)
  wait(Mommy.Player.Exploits.ReturnDelay)
  if Mommy.Player.Exploits.Return == true then
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old -- teleports you back to your old position
  end
else
  if valued == "SMG" then
    local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-810, -40, -942)
    wait(Mommy.Player.Exploits.ReturnDelay)
    if Mommy.Player.Exploits.Return == true then
      game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old -- teleports you back to your old position
    end
  end
end
end
end
end
end
end})

Miscellaneous1:AddSeparator({text = "Ammo"})

Miscellaneous1:AddList(
{text = "Selection", selected = "", max = 5,
values = {"Revolver Ammo", "Double Barrel Ammo", "Tactical Shotgun Ammo", "Shotgun Ammo", "Silencer Ammo", "SMG Ammo"},
callback = function(d)
valuedd = d
end})

Miscellaneous1:AddButton(
{text = "Teleport",
callback = function()
if valuedd == "Revolver Ammo" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-877, -33, -529)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old -- teleports you back to your old position
end
else
if valuedd == "Double Barrel Ammo" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-875, -33, -524)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old -- teleports you back to your old position
end
else
if valuedd == "Shotgun Ammo" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-883, -33, -529)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old -- teleports you back to your old position
end
else
if valuedd == "Tactical Shotgun Ammo" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(493, 48, -620)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
  game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old -- teleports you back to your old position
end
else
if valuedd == "Silencer Ammo" then
  local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
  game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-891, -33, -533)
  wait(Mommy.Player.Exploits.ReturnDelay)
  if Mommy.Player.Exploits.Return == true then
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old -- teleports you back to your old position
  end
else
  if valuedd == "SMG Ammo" then
    local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-815, -40, -942)
    wait(Mommy.Player.Exploits.ReturnDelay)
    if Mommy.Player.Exploits.Return == true then
      game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old -- teleports you back to your old position
    end
  end
end
end
end
end
end
end})

Miscellaneous1:AddSeparator({text = "Food"})

Miscellaneous1:AddList(
{text = "Selection", selected = "", max = 5,
values = {"Chicken", "Hamburger", "Hotdog", "Lettuce", "Pizza", "Popcorn", "Taco"},
callback = function(p)
valuedda = p
end})

Miscellaneous1:AddButton(
{text = "Teleport",
callback = function()
if valuedda == "Chicken" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-795, -40, -938)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old
else wait(0.2)
if Mommy.Player.Exploits.AutoPurchase == true then
fireclickdetector(game.Workspace.Ignored.Shop["[Chicken] - $7"].ClickDetector)
end
end
else
if valuedda == "Hamburger" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-275, 23, -807)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old
else wait(0.2)
if Mommy.Player.Exploits.AutoPurchase == true then
fireclickdetector(game.Workspace.Ignored.Shop["[Hamburger] - $5"].ClickDetector)
end
end
else
if valuedda == "Hotdog" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-16, 29, -914)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old
else wait(0.2)
if Mommy.Player.Exploits.AutoPurchase == true then
  fireclickdetector(game.Workspace.Ignored.Shop["[HotDog] - $8"].ClickDetector)
end
end
else
if valuedda == "Lettuce" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-84, 25, -633)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
  game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old
else wait(0.2)
  if Mommy.Player.Exploits.AutoPurchase == true then
    fireclickdetector(game.Workspace.Ignored.Shop["[Lettuce] - $5"].ClickDetector)
  end
end
else
if valuedda == "Pizza" then
  local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
  game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-789, -40, -943)
  wait(Mommy.Player.Exploits.ReturnDelay)
  if Mommy.Player.Exploits.Return == true then
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old
  else wait(0.2)
    if Mommy.Player.Exploits.AutoPurchase == true then
      fireclickdetector(game.Workspace.Ignored.Shop["[Pizza] - $5"].ClickDetector)
    end
  end
else
  if valuedda == "Popcorn" then
    local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-995, 25, -153)
    wait(Mommy.Player.Exploits.ReturnDelay)
    if Mommy.Player.Exploits.Return == true then
      game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old
    else wait(0.2)
      if Mommy.Player.Exploits.AutoPurchase == true then
        fireclickdetector(game.Workspace.Ignored.Shop["[Popcorn] - $7"].ClickDetector)
      end
    end
  else
    if valuedda == "Taco" then
      local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
      game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(584, 51, -474)
      wait(Mommy.Player.Exploits.ReturnDelay)
      if Mommy.Player.Exploits.Return == true then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old
      else wait(0.2)
        if Mommy.Player.Exploits.AutoPurchase == true then
          fireclickdetector(game.Workspace.Ignored.Shop["[Taco] - $2"].ClickDetector)
        end
      end
    end
  end
end
end
end
end
end
end})

Miscellaneous1:AddSeparator({text = "Armor"})

Miscellaneous1:AddList({text = "Selection",selected = "",max = 5,
values = {"High Medium Armor","Medium Armor","Fire Armor"}, callback = function(c)
valuecc = c
end})

Miscellaneous1:AddButton({text = "Teleport",callback = function()
if valuecc == "High Medium Armor" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(99, 26, -890)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old
else wait(0.2)
if Mommy.Player.Exploits.AutoPurchase == true then
fireclickdetector(game.Workspace.Ignored.Shop["[High-Medium Armor] - $2163"].ClickDetector)
end
end
else
if valuecc == "Medium Armor" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-605, 10, -789)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old
else wait(0.2)
if Mommy.Player.Exploits.AutoPurchase == true then
fireclickdetector(game.Workspace.Ignored.Shop["[Medium Armor] - $1030"].ClickDetector)
end
end
else
if valuecc == "Fire Armor" then
local old = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(99, 26, -895)
wait(Mommy.Player.Exploits.ReturnDelay)
if Mommy.Player.Exploits.Return == true then
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = old
else wait(0.2)
if Mommy.Player.Exploits.AutoPurchase == true then
fireclickdetector(game.Workspace.Ignored.Shop["[Fire Armor] - $2060"].ClickDetector)
end
end
end
end
end
end})
-- [Loaded Time] ------------------------------------------------------------------------------------------------------------------------------------------------------------
local Time = (string.format("%."..tostring(Decimals).."f", os.clock() - Clock))
library:SendNotification(("Loaded In "..tostring(Time)), 3)
-- [ESP Stuff] ------------------------------------------------------------------------------------------------------------------------------------------------------------
local players = game.Players;
for _, player in pairs(players:GetPlayers()) do
if player == players.LocalPlayer then continue; end;
esp:Player(player);
end;
players.PlayerAdded:Connect(function(player)
esp:Player(player);
end);
players.PlayerAdded:Connect(function(player)
local obj = esp:GetObject(player)
if obj then
obj:Destroy();
end;
end);
