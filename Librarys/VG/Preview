local Lib = loadstring(game:HttpGet('https://pastebin.com/raw/GaRF4FDA'))()
local CategoryVariableHere= Lib:Category("Muscle Legends")
CategoryVariableHere:Toggle("Auto strength",function(State)
deku = State

while deku do wait(1)
local args = {
    [1] = "rep"
}
game:GetService("Players").LocalPlayer.muscleEvent:FireServer(unpack(args))
for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do 
if v.ClassName == "Tool" and v.Name == "Handstands" then 
v.Parent = game.Players.LocalPlayer.Character
end
end
for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do 
if v.ClassName == "Tool" and v.Name == "Situps" then 
v.Parent = game.Players.LocalPlayer.Character
end
end
for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do 
if v.ClassName == "Tool" and v.Name == "Pushups" then 
v.Parent = game.Players.LocalPlayer.Character
end
end
for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do 
if v.ClassName == "Tool" and v.Name == "Weight" then 
v.Parent = game.Players.LocalPlayer.Character
end
end


end
end)
CategoryVariableHere:Toggle("Auto Rebirth",function(State)
dragons= State
while dragons do wait(0.1)
local args = {
    [1] = "rebirthRequest"
}

game:GetService("ReplicatedStorage").rEvents.rebirthRemote:InvokeServer(unpack(args))

end
end)
CategoryVariableHere:Button("Fe invis",function()
local Player = game.Players.LocalPlayer
local savepos = Player.Character.HumanoidRootPart.CFrame

game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(915.095215, 37.5268936, 349.808533)
wait(0.5)
local Character = game:GetService('Players').LocalPlayer.Character
local Clone = Character.LowerTorso.Root:Clone()
Character.LowerTorso.Root:Destroy()
Clone.Parent = Character.LowerTorso
wait(0.5)

Player.Character.HumanoidRootPart.CFrame = savepos

game.Players.LocalPlayer.CharacterAdded:Connect(function()
wait(3)
local Player = game.Players.LocalPlayer
local savepos = Player.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(915.095215, 37.5268936, 349.808533)

local Character = game:GetService('Players').LocalPlayer.Character
local Clone = Character.LowerTorso.Root:Clone()
Character.LowerTorso.Root:Destroy()
Clone.Parent = Character.LowerTorso
wait(0.5)

Player.Character.HumanoidRootPart.CFrame = savepos 
  end) end)
CategoryVariableHere:Toggle("Auto Speed Keypress",function(State)
China = State
local args = {
    [1] = "changeSize",
    [2] = 1
}

game:GetService("ReplicatedStorage").rEvents.changeSpeedSizeRemote:InvokeServer(unpack(args))
while China do wait()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(243.039078, 4.8158493, 361.3414)
keypress(0x57) wait(.1) keyrelease(0x57)
end    
end)
CategoryVariableHere:Toggle("Do not disturb",function(State)
china1 = State
game:GetService('RunService').RenderStepped:connect(function()
if china1 then
game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(4011, 26043, -2394)
 end end)
end)
CategoryVariableHere:Toggle("Auto Chests",function(State)
tootooisgay = State
while tootooisgay do wait()
local args = {
    [1] = "Magma Chest"
}

game:GetService("ReplicatedStorage").rEvents.checkChestRemote:InvokeServer(unpack(args))
local args = {
    [1] = "Mythical Chest"
}

game:GetService("ReplicatedStorage").rEvents.checkChestRemote:InvokeServer(unpack(args))
local args = {
    [1] = "Golden Chest"
}
game:GetService("ReplicatedStorage").rEvents.checkChestRemote:InvokeServer(unpack(args))
local args = {
    [1] = "Enchanted Chest"
}
game:GetService("ReplicatedStorage").rEvents.checkChestRemote:InvokeServer(unpack(args))
local args = {
    [1] = "Legends Chest"
}
game:GetService("ReplicatedStorage").rEvents.checkChestRemote:InvokeServer(unpack(args))
end 
end)
CategoryVariableHere:Toggle("Auto join brawl",function(State)
hot = State
while hot do wait(2)
local args = {
    [1] = "joinBrawl"
}

game:GetService("ReplicatedStorage").rEvents.brawlEvent:FireServer(unpack(args))
end
end)
CategoryVariableHere:Button("Turn Small",function()   
local args = {
    [1] = "changeSize",
    [2] = 1
}

game:GetService("ReplicatedStorage").rEvents.changeSpeedSizeRemote:InvokeServer(unpack(args))
end)

CategoryVariableHere:Button("Blue Crystal",function()
local args = {
    [1] = "openCrystal",
    [2] = "Blue Crystal"
}
game:GetService("ReplicatedStorage").rEvents.openCrystalRemote:InvokeServer(unpack(args))
end)
CategoryVariableHere:Button("Green Crystal",function()
local args = {
    [1] = "openCrystal",
    [2] = "Green Crystal"
}

game:GetService("ReplicatedStorage").rEvents.openCrystalRemote:InvokeServer(unpack(args))
end)
CategoryVariableHere:Button("Mythical Crystal",function()
local args = {
    [1] = "openCrystal",
    [2] = "Mythical Crystal"
}

game:GetService("ReplicatedStorage").rEvents.openCrystalRemote:InvokeServer(unpack(args))
end)
CategoryVariableHere:Button("Frost Crystal",function()
local args = {
    [1] = "openCrystal",
    [2] = "Frost Crystal"
}

game:GetService("ReplicatedStorage").rEvents.openCrystalRemote:InvokeServer(unpack(args))
end)
CategoryVariableHere:Button("Inferno Crystal",function()
local args = {
    [1] = "openCrystal",
    [2] = "Inferno Crystal"
}

game:GetService("ReplicatedStorage").rEvents.openCrystalRemote:InvokeServer(unpack(args))
end)
CategoryVariableHere:Button("Legends Crystal",function()
local args = {
    [1] = "openCrystal",
    [2] = "Legends Crystal"
}

game:GetService("ReplicatedStorage").rEvents.openCrystalRemote:InvokeServer(unpack(args))
end)
CategoryVariableHere:Button("Muscle Elite Crystal",function()
local args = {
    [1] = "openCrystal",
    [2] = "Muscle Elite Crystal"
}

game:GetService("ReplicatedStorage").rEvents.openCrystalRemote:InvokeServer(unpack(args))
end)
CategoryVariableHere:Slider("WalkSpeed",16,16,100,function(Val) game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Val end)
CategoryVariableHere:Slider("JumpPower",16,16,100,function(Val) game.Players.LocalPlayer.Character.Humanoid.JumpPower = Val end)
CategoryVariableHere:Button("BTools",function() 
game.StarterGui:SetCoreGuiEnabled(2, true)
a = Instance.new("HopperBin", game.Players.LocalPlayer.Backpack)
a.BinType = 2
b = Instance.new("HopperBin", game.Players.LocalPlayer.Backpack)
b.BinType = 3
c = Instance.new("HopperBin", game.Players.LocalPlayer.Backpack)
c.BinType = 4 end)
CategoryVariableHere:Button("G NoClip",function() 
noclip = false
game:GetService('RunService').Stepped:connect(function()
if noclip then
game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
end
end)
plr = game.Players.LocalPlayer
mouse = plr:GetMouse()
mouse.KeyDown:connect(function(key)

if key == "g" then
noclip = not noclip
game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
end
end) end)
CategoryVariableHere:Button("B Fly",function()
    local gogo1000 = 0
local LP = game:service('Players').LocalPlayer
local MOUSE = LP:GetMouse()
 
MOUSE.KeyDown:connect(function(KEY)
 if KEY:lower() == 'b' then
    local LP = game:service('Players').LocalPlayer
local MOUSE = LP:GetMouse()
 
    gogo1000 = gogo1000 + 1
    _G.FLYING = false
 
local T = LP.Character.UpperTorso
local CONTROL = {F = 0, B = 0, L = 0, R = 0}
local lCONTROL = {F = 0, B = 0, L = 0, R = 0}
local SPEED = 5
 
 
 
local function FLY()
    _G.FLYING = true
    local BG = Instance.new('BodyGyro', T)
    local BV = Instance.new('BodyVelocity', T)
    BG.P = 9e4
    BG.maxTorque = Vector3.new(9e9, 9e9, 9e9)
    BG.cframe = T.CFrame
    BV.velocity = Vector3.new(0, 0.1, 0)
    BV.maxForce = Vector3.new(9e9, 9e9, 9e9)
 
 
    spawn(function()
      repeat wait()
        LP.Character.Humanoid.PlatformStand = true
        if CONTROL.L + CONTROL.R ~= 0 or CONTROL.F + CONTROL.B ~= 0 then
          SPEED = 50
        elseif not (CONTROL.L + CONTROL.R ~= 0 or CONTROL.F + CONTROL.B ~= 0) and SPEED ~= 0 then
          SPEED = 0
        end
        if (CONTROL.L + CONTROL.R) ~= 0 or (CONTROL.F + CONTROL.B) ~= 0 then
          BV.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (CONTROL.F + CONTROL.B)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(CONTROL.L + CONTROL.R, (CONTROL.F + CONTROL.B) * 0.2, 0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p)) * SPEED
          lCONTROL = {F = CONTROL.F, B = CONTROL.B, L = CONTROL.L, R = CONTROL.R}
        elseif (CONTROL.L + CONTROL.R) == 0 and (CONTROL.F + CONTROL.B) == 0 and SPEED ~= 0 then
          BV.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lCONTROL.F + lCONTROL.B)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lCONTROL.L + lCONTROL.R, (lCONTROL.F + lCONTROL.B) * 0.2, 0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p)) * SPEED
        else
          BV.velocity = Vector3.new(0, 0.1, 0)
        end
        BG.cframe = game.Workspace.CurrentCamera.CoordinateFrame
      until not _G.FLYING
      CONTROL = {F = 0, B = 0, L = 0, R = 0}
      lCONTROL = {F = 0, B = 0, L = 0, R = 0}
      SPEED = 0
      BG:destroy()
      BV:destroy()
      LP.Character.Humanoid.PlatformStand = false
    end)
  end
 
  MOUSE.KeyDown:connect(function(KEY)
    if KEY:lower() == 'w' then
      CONTROL.F = 1
    elseif KEY:lower() == 's' then
      CONTROL.B = -1
    elseif KEY:lower() == 'a' then
      CONTROL.L = -1 
    elseif KEY:lower() == 'd' then 
      CONTROL.R = 1
    end
  end)
 
  MOUSE.KeyUp:connect(function(KEY)
    if KEY:lower() == 'w' then
      CONTROL.F = 0
    elseif KEY:lower() == 's' then
      CONTROL.B = 0
    elseif KEY:lower() == 'a' then
      CONTROL.L = 0
    elseif KEY:lower() == 'd' then
      CONTROL.R = 0
    end
  end)
 
 
 
 
  FLY()
 
    if gogo1000 == 2 then
    _G.FLYING = false
    gogo1000 = 0
 
    end
 
 
 
end
end) end)

CategoryVariableHere:Button("teleport to Random Player",function()
local randomPlayer = game.Players:GetPlayers()
[math.random(1,#game.Players:GetPlayers())]

game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(Vector3.new(randomPlayer.Character.Head.Position.X, randomPlayer.Character.Head.Position.Y, randomPlayer.Character.Head.Position.Z)) end)
CategoryVariableHere:Button("Lag Switch F3",function()
local a = false
local b = settings()

game:service'UserInputService'.InputEnded:connect(function(i)
if i.KeyCode == Enum.KeyCode.F3 then
a = not a
b.Network.IncomingReplicationLag = a and 10 or 0
end
end) end) 
CategoryVariableHere:Button("ServerHop",function()
local PlaceID = game.PlaceId
local AllIDs = {}
local foundAnything = ""
local actualHour = os.date("!*t").hour
local Deleted = false
local File = pcall(function()
    AllIDs = game:GetService('HttpService'):JSONDecode(readfile("NotSameServers.json"))
end)
if not File then
    table.insert(AllIDs, actualHour)
    writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
end
function TPReturner()
    local Site;
    if foundAnything == "" then
        Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
    else
        Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
    end
    local ID = ""
    if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
        foundAnything = Site.nextPageCursor
    end
    local num = 0;
    for i,v in pairs(Site.data) do
        local Possible = true
        ID = tostring(v.id)
        if tonumber(v.maxPlayers) > tonumber(v.playing) then
            for _,Existing in pairs(AllIDs) do
                if num ~= 0 then
                    if ID == tostring(Existing) then
                        Possible = false
                    end
                else
                    if tonumber(actualHour) ~= tonumber(Existing) then
                        local delFile = pcall(function()
                            delfile("NotSameServers.json")
                            AllIDs = {}
                            table.insert(AllIDs, actualHour)
                        end)
                    end
                end
                num = num + 1
            end
            if Possible == true then
                table.insert(AllIDs, ID)
                wait()
                pcall(function()
                    writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
                    wait()
                    game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
                end)
                wait(4)
            end
        end
    end
end

function Teleport()
    while wait() do
        pcall(function()
            TPReturner()
            if foundAnything ~= "" then
                TPReturner()
            end
        end)
    end
end

-- If you'd like to use a script before server hopping (Like a Automatic Chest collector you can put the Teleport() after it collected everything.
Teleport()
end)
CategoryVariableHere:Button("Rejoin",function()
    local ts = game:GetService("TeleportService")
local p = game:GetService("Players").LocalPlayer
ts:Teleport(game.PlaceId, p) end)
local CategoryVariableHere= Lib:Category("Teleports")
CategoryVariableHere:Button("Go to Legends gym",function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(4298.60059, 1121.89404, -3898.68066)
end)
CategoryVariableHere:Button("Go to Mythical gym",function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(2386.89038, 139.607956, 1094.26367)
end)
CategoryVariableHere:Button("Go to Frost gym",function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-2752.56543, 125.822533, -386.73703)
end)
CategoryVariableHere:Button("Go to Eternal gym",function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-6917.79248, 182.352829, -1336.63928)
end)
CategoryVariableHere:Button("Go to Tiny island",function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-4.25301933, 220.993713, 1963.60168)
end)
CategoryVariableHere:Button("Go to Brawl aura 1",function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(985.910645, 163.795364, -7037.80615)
end)
CategoryVariableHere:Button("Go to Brawl aura 2",function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(4466.75342, 334.973602, -8425.74512)
end)
CategoryVariableHere:Button("Go to Brawl aura 3",function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1901.87695, 251.895432, -5899.64795)
end)

local CategoryVariableHere= Lib:Category("Credits")
CategoryVariableHere:Label("Credits to a r q for ui liba")
CategoryVariableHere:Label("Credits to DekuDimz#7960 aka me lol")
Lib:Reload()

while wait() do
wait(600)
game.Players.LocalPlayer.Character.Head:Destroy() end
game.StarterGui:SetCore("SendNotification", {
Title = "Warning";
Text = "RightShift to toggle";
})
game.StarterGui:SetCore("SendNotification", {
Title = "Credis";
Text = "CharWar Serverhops Toxic Mods screen thingy";
})
