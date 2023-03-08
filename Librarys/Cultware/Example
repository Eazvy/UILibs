        function notify(title,text,time)
            game.StarterGui:SetCore("SendNotification", {
                Title = "cultware.cc";
                Text = "made by tenaki and flash";
                Duration = "20";
            })
        end
    
    
    getgenv().OldAimPart = "LowerTorso"
    getgenv().AimPart = "LowerTorso" -- For R15 Games: {UpperTorso, LowerTorso, HumanoidRootPart, Head} | For R6 Games: {Head, Torso, HumanoidRootPart}  
        getgenv().AimlockKey = "q"
        getgenv().AimRadius = 30 -- How far away from someones character you want to lock on at
        getgenv().ThirdPerson = true 
        getgenv().FirstPerson = true
        getgenv().TeamCheck = false -- Check if Target is on your Team (True means it wont lock onto your teamates, false is vice versa) (Set it to false if there are no teams)
        getgenv().PredictMovement = true -- Predicts if they are moving in fast velocity (like jumping) so the aimbot will go a bit faster to match their speed 
        getgenv().PredictionVelocity = 7
        getgenv().CheckIfJumped = false
        getgenv().AutoPrediction = false
    
       
    
        local Players, Uis, RService, SGui = game:GetService"Players", game:GetService"UserInputService", game:GetService"RunService", game:GetService"StarterGui";
        local Client, Mouse, Camera, CF, RNew, Vec3, Vec2 = Players.LocalPlayer, Players.LocalPlayer:GetMouse(), workspace.CurrentCamera, CFrame.new, Ray.new, Vector3.new, Vector2.new;
        local Aimlock, MousePressed, CanNotify = false, false, false;
        local AimlockTarget;
        local OldPre;
        
        getgenv().CiazwareUniversalAimbotLoaded = true
        
        getgenv().WorldToViewportPoint = function(P)
            return Camera:WorldToViewportPoint(P)
        end
        
        getgenv().WorldToScreenPoint = function(P)
            return Camera.WorldToScreenPoint(Camera, P)
        end
        
        getgenv().GetObscuringObjects = function(T)
            if T and T:FindFirstChild(getgenv().AimPart) and Client and Client.Character:FindFirstChild("Head") then 
                local RayPos = workspace:FindPartOnRay(RNew(
                    T[getgenv().AimPart].Position, Client.Character.Head.Position)
                )
                if RayPos then return RayPos:IsDescendantOf(T) end
            end
        end
        
        getgenv().GetNearestTarget = function()
            -- Credits to whoever made this, i didnt make it, and my own mouse2plr function kinda sucks
            local players = {}
            local PLAYER_HOLD  = {}
            local DISTANCES = {}
            for i, v in pairs(Players:GetPlayers()) do
                if v ~= Client then
                    table.insert(players, v)
                end
            end
            for i, v in pairs(players) do
                if v.Character ~= nil then
                    local AIM = v.Character:FindFirstChild("Head")
                    if getgenv().TeamCheck == true and v.Team ~= Client.Team then
                        local DISTANCE = (v.Character:FindFirstChild("Head").Position - game.Workspace.CurrentCamera.CFrame.p).magnitude
                        local RAY = Ray.new(game.Workspace.CurrentCamera.CFrame.p, (Mouse.Hit.p - game.Workspace.CurrentCamera.CFrame.p).unit * DISTANCE)
                        local HIT,POS = game.Workspace:FindPartOnRay(RAY, game.Workspace)
                        local DIFF = math.floor((POS - AIM.Position).magnitude)
                        PLAYER_HOLD[v.Name .. i] = {}
                        PLAYER_HOLD[v.Name .. i].dist= DISTANCE
                        PLAYER_HOLD[v.Name .. i].plr = v
                        PLAYER_HOLD[v.Name .. i].diff = DIFF
                        table.insert(DISTANCES, DIFF)
                    elseif getgenv().TeamCheck == false and v.Team == Client.Team then 
                        local DISTANCE = (v.Character:FindFirstChild("Head").Position - game.Workspace.CurrentCamera.CFrame.p).magnitude
                        local RAY = Ray.new(game.Workspace.CurrentCamera.CFrame.p, (Mouse.Hit.p - game.Workspace.CurrentCamera.CFrame.p).unit * DISTANCE)
                        local HIT,POS = game.Workspace:FindPartOnRay(RAY, game.Workspace)
                        local DIFF = math.floor((POS - AIM.Position).magnitude)
                        PLAYER_HOLD[v.Name .. i] = {}
                        PLAYER_HOLD[v.Name .. i].dist= DISTANCE
                        PLAYER_HOLD[v.Name .. i].plr = v
                        PLAYER_HOLD[v.Name .. i].diff = DIFF
                        table.insert(DISTANCES, DIFF)
                    end
                end
            end
            
            if unpack(DISTANCES) == nil then
                return nil
            end
            
            local L_DISTANCE = math.floor(math.min(unpack(DISTANCES)))
            if L_DISTANCE > getgenv().AimRadius then
                return nil
            end
            
            for i, v in pairs(PLAYER_HOLD) do
                if v.diff == L_DISTANCE then
                    return v.plr
                end
            end
            return nil
        end
        
        Mouse.KeyDown:Connect(function(a)
            if not (Uis:GetFocusedTextBox()) then 
                if a == AimlockKey and AimlockTarget == nil then
                    pcall(function()
                        if MousePressed ~= true then MousePressed = true end 
                        local Target;Target = GetNearestTarget()
                        if Target ~= nil then 
                            AimlockTarget = Target
                        end
                    end)
                elseif a == AimlockKey and AimlockTarget ~= nil then
                    if AimlockTarget ~= nil then AimlockTarget = nil end
                    if MousePressed ~= false then 
                        MousePressed = false 
                    end
                end
            end
        end)
        
        RService.RenderStepped:Connect(function()
            if getgenv().ThirdPerson == true and getgenv().FirstPerson == true then 
                if (Camera.Focus.p - Camera.CoordinateFrame.p).Magnitude > 1 or (Camera.Focus.p - Camera.CoordinateFrame.p).Magnitude <= 1 then 
                    CanNotify = true 
                else 
                    CanNotify = false 
                end
            elseif getgenv().ThirdPerson == true and getgenv().FirstPerson == false then 
                if (Camera.Focus.p - Camera.CoordinateFrame.p).Magnitude > 1 then 
                    CanNotify = true 
                else 
                    CanNotify = false 
                end
            elseif getgenv().ThirdPerson == false and getgenv().FirstPerson == true then 
                if (Camera.Focus.p - Camera.CoordinateFrame.p).Magnitude <= 1 then 
                    CanNotify = true 
                else 
                    CanNotify = false 
                end
            end
            if Aimlock == true and MousePressed == true then 
                if AimlockTarget and AimlockTarget.Character and AimlockTarget.Character:FindFirstChild(getgenv().AimPart) then 
                    if getgenv().FirstPerson == true then
                        if CanNotify == true then
                            if getgenv().PredictMovement == true then 
                                Camera.CFrame = CF(Camera.CFrame.p, AimlockTarget.Character[getgenv().AimPart].Position + AimlockTarget.Character[getgenv().AimPart].Velocity/PredictionVelocity)
                            elseif getgenv().PredictMovement == false then 
                                Camera.CFrame = CF(Camera.CFrame.p, AimlockTarget.Character[getgenv().AimPart].Position)
                            end
                        end
                    elseif getgenv().ThirdPerson == true then 
                        if CanNotify == true then
                            if getgenv().PredictMovement == true then 
                                Camera.CFrame = CF(Camera.CFrame.p, AimlockTarget.Character[getgenv().AimPart].Position + AimlockTarget.Character[getgenv().AimPart].Velocity/PredictionVelocity)
                            elseif getgenv().PredictMovement == false then 
                                Camera.CFrame = CF(Camera.CFrame.p, AimlockTarget.Character[getgenv().AimPart].Position)
                            end
                        end 
                    end
                end
            end
             if CheckIfJumped == true then
           if AimlockTarget.Character.Humanoid.FloorMaterial == Enum.Material.Air then
    
               getgenv().AimPart = "RightFoot"
           else
             getgenv().AimPart = getgenv().OldAimPart
    
           end
        end
    end)
    
    
    if getgenv().AutoPrediction == true then
        wait(5.2)
            local pingvalue = game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValueString()
            local split = string.split(pingvalue,'(')
            local ping = tonumber(split[1])
                local PingNumber = pingValue[1]
    
     if  ping < 250 then
            getgenv().PredictionVelocity = 4.89
            elseif ping < 150 then
                getgenv().PredictionVelocity = 5.43
            elseif ping < 130 then
                getgenv().PredictionVelocity = 6.34
            elseif ping < 120 then
                getgenv().PredictionVelocity = 6.54
            elseif ping < 110 then
                getgenv().PredictionVelocity = 6.6
            elseif ping < 105 then
                getgenv().PredictionVelocity = 7
            elseif ping < 90 then
                getgenv().PredictionVelocity = 7
            elseif ping < 80 then
                getgenv().PredictionVelocity = 7
            elseif ping < 70 then
                getgenv().PredictionVelocity = 9
            elseif ping < 60 then
                getgenv().PredictionVelocity = 9
            elseif ping < 50 then
                getgenv().PredictionVelocity = 8.7
            elseif ping < 40 then
                getgenv().PredictionVelocity = 10.39
            end
        end
    
    
    local Library = loadstring(game:HttpGet("https://pastebin.com/raw/7kbpJGDf"))()
    WindowYSize=545
    WindowTheme=Color3.fromRGB(185, 0, 191)
    Window=Library:Window("cultware.cc made by tenaki", WindowTheme, WindowYSize)


    getgenv().Settings = {
        Nigger = false
    }
    local Settings = getgenv().Settings
    
    
    Tab=Window:Tab("Rage")
    
    legittab=Window:Tab("Legit")

    Tab4=Window:Tab("Visuals")
    
    Tab5=Window:Tab("Miscellaneous")
    
    
    Section=Tab:Section("Aimbot")
    silentaimbottab=Tab:Section("Silent aimbot")
    ragecheatchar=Tab:Section("Character Rage")
    sectionlegit=legittab:Section("Silent aim")
    Visuals=Tab4:Section("Esp")
    fovsection=legittab:Section("Fov")
    ViewOF=Tab5:Section("Field Of View")
    Rindo=Tab5:Section("Player")
    Godlam=Tab5:Section("Teleports")

    Window:Label("1.0.0", Color3.fromRGB(207, 58, 255))

    
    Section:Toggle("Enabled", function(fffff)
    Aimlock = fffff
    end)
    
    
    Section:Textbox("Key", function(zzzzz)
        if string ~= '' then
    PredictionVelocity = zzzzz
        end
    end)
    
    Section:Textbox("Prediction Velocity", function(broid)
        if string ~= '' then
    getgenv().PredictionVelocity = broid
        end
    end)
    
    Section:Dropdown("Part", {"Head", "UpperTorso", "HumanoidRootPart", "LowerTorso", "LeftUpperLeg", "RightUpperLeg", "LeftLowerLeg", "RightLowerLeg", "LeftFoot", "RightFoot"}, function(dasdada)
    getgenv().AimPart = dasdada
    end)
    
    Section:Toggle("Airshot Func", function(novagang)
    CheckIfJumped = novagang
    end)
    
    Section:Toggle("Auto Pre", function(sneakinup)
    AutoPrediction = sneakinup
    end)
    
    local ESP = loadstring(game:HttpGet("https://pastebin.com/raw/L85CYGb8", true))()


    Visuals:Toggle("Enabled", function(bool)
        ESP.Enabled = bool
    end)
    
    Visuals:Toggle("Tracers", function(er)
        ESP.Tracers = er
        end)
    
    
    Visuals:Toggle("Names", function(be)
            ESP.Names = be
    end)
    
    
    Visuals:Toggle("Boxes", function(vc)
         ESP.Boxes = vc
        end)

        Visuals:Toggle("Chams", function()

           end)


        Visuals:Color("Colour", function(bool)
            ESP.Color = bool
          end)   
  

          


Max = 140
Min = 10
ViewOF:Slider("View", Max, Min, function(bruh)
    amount = bruh
    game:GetService'Workspace'.Camera.FieldOfView = amount
end)

Rindo:Toggle("Korblox", function()
game:GetService"RunService".RenderStepped:Connect(function()

    local Char = game.Players.LocalPlayer.Character
    local plr = game.Players.LocalPlayer.Character
    local head = Char.Head
    local face = head.face
    local c = plr.RightFoot
    local x = plr.RightLowerLeg
    local z = plr.RightUpperLeg
    local r = plr.LeftFoot
    local e = plr.LeftLowerLeg
    local w = plr.LeftUpperLeg
    
    -- Right
    c.MeshId = "http://www.roblox.com/asset/?id=902942093"
    x.MeshId = "http://www.roblox.com/asset/?id=902942093"
    z.MeshId = "http://www.roblox.com/asset/?id=902942096"
    z.TextureID = "http://roblox.com/asset/?id=902843398"
    c.Transparency = 1
    x.Transparency = 1
    end)
end)


Rindo:Toggle("Headless", function()
game:GetService("RunService").RenderStepped:Connect(function()
    local plr = game.Players.LocalPlayer.Character
    local head = plr:WaitForChild("Head")
    local face = head:WaitForChild("face")
    
    face.Transparency = 1 --Texture = "rbxassetid://209712379"
    head.Transparency = 1
    end)
end)

Godlam:Button("Admin", function()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-874.903992, -32.6492004, -525.215698)
end)

Godlam:Button("Roof", function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-589.37817382813, 66.657341003418, -678.16540527344)
end)

Godlam:Button("Shoe Store", function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-122.52713012695, 22.125370025635, -873.95684814453)
end)



    silentaimbottab:Button("Silent Aimbot", function()
        _G.KEY = "q"
    _G.PART = "HumanoidRootPart"
    _G.PRED = 0.037
    _G.Frame = Vector3.new(0,0.53,0)
    _G.AIR = -0.5
    _G.SHIT = 0.1
    
    local CC = game:GetService "Workspace".CurrentCamera
    local Plr
    local enabled = false
    local accomidationfactor = nil
    local mouse = game.Players.LocalPlayer:GetMouse()
    getgenv().placemarker = Instance.new("Part", game.Workspace)
    local guimain = Instance.new("Folder", game.CoreGui)
    
    getgenv().makemarker = function(Parent, Adornee, Color, Size, Size2)
        local e = Instance.new("BillboardGui", Parent)
        e.Name = "PP"
        e.Adornee = Adornee
        e.Size = UDim2.new(Size, Size2, Size, Size2)
        e.AlwaysOnTop = true
        local a = Instance.new("Frame", e)
        a.Size = UDim2.new(4, 0, 4, 0)
        a.BackgroundTransparency = 0.1
        a.BackgroundColor3 = Color
        local g = Instance.new("UICorner", a)
        g.CornerRadius = UDim.new(50, 50)
        return (e)
    end
    
    local data = game.Players:GetPlayers()
    function noob(player)
        local character
        repeat
            wait()
        until player.Character
        local handler = makemarker(guimain, player.Character:WaitForChild(_G.PART), Color3.fromRGB(255, 255, 255), 0.0, 0)
        handler.Name = player.Name
        player.CharacterAdded:connect(
            function(Char)
                handler.Adornee = Char:WaitForChild(_G.PART)
            end
        )
    
        local TextLabel = Instance.new("TextLabel", handler)
        TextLabel.BackgroundTransparency = 1
        TextLabel.Position = UDim2.new(0, 0, 0, -50)
        TextLabel.Size = UDim2.new(0, 100, 0, 100)
        TextLabel.Font = Enum.Font.SourceSansSemibold
        TextLabel.TextSize = 14
        TextLabel.TextColor3 = Color3.new(1, 1, 1)
        TextLabel.TextStrokeTransparency = 0
        TextLabel.TextYAlignment = Enum.TextYAlignment.Bottom
        TextLabel.Text = "Name: " .. player.Name
        TextLabel.ZIndex = 10
    
        spawn(
            function()
                while wait() do
                    if player.Character then
                    --TextLabel.Text = player.Name.." | Bounty: "..tostring(player:WaitForChild("leaderstats").Wanted.Value).." | "..tostring(math.floor(player.Character:WaitForChild("Humanoid").Health))
                    end
                end
            end
        )
    end
    
    for i = 1, #data do
        if data[i] ~= game.Players.LocalPlayer then
            noob(data[i])
        end
    end
    
    game.Players.PlayerAdded:connect(
        function(Player)
            noob(Player)
        end
    )
    
    game.Players.PlayerRemoving:Connect(
        function(player)
            guimain[player.Name]:Destroy()
        end
    )
    
    spawn(
        function()
            placemarker.Anchored = true
            placemarker.CanCollide = false
            placemarker.Size = Vector3.new(0.1, 0.1, 0.1)
            placemarker.Transparency = _G.SHIT
                    placemarker.Visible = false
    
            makemarker(placemarker, placemarker, Color3.fromRGB(255, 255, 255), 0.20, 0)
        end
    )
    
    mouse.KeyDown:Connect(
        function(k)
            if k ~= _G.KEY then
                return
            end
            if enabled then
                -- guimain[Plr.Name].Frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                enabled = false
                if Settings.Nigger then
                    notify("Cultware", "Unlocked", 1)
                end
                
    
            else
                --guimain[Plr.Name].Frame.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
                enabled = true
                Plr = getClosestPlayerToCursor()
                if Settings.Nigger then
                    notify("Cultware", "Locked Onto: "..tostring(Plr.Character.Humanoid.DisplayName).."", 1)
               
                end
                end
        end)
    
    function getClosestPlayerToCursor()
        local closestPlayer
        local shortestDistance = math.huge
    
        for i, v in pairs(game.Players:GetPlayers()) do
            if
                v ~= game.Players.LocalPlayer and v.Character and v.Character:FindFirstChild("Humanoid") and
                    v.Character.Humanoid.Health ~= 0 and
                    v.Character:FindFirstChild(_G.PART)
             then
                local pos = CC:WorldToViewportPoint(v.Character.PrimaryPart.Position)
                local magnitude = (Vector2.new(pos.X, pos.Y) - Vector2.new(mouse.X, mouse.Y)).magnitude
                if magnitude < shortestDistance then
                    closestPlayer = v
                    shortestDistance = magnitude
                end
            end
        end
        return closestPlayer
    end
    
    game:GetService "RunService".Stepped:connect(
        function()
            if enabled and Plr.Character and Plr.Character:FindFirstChild(_G.PART) then
                placemarker.CFrame =
                    CFrame.new(Plr.Character[_G.PART].Position + _G.Frame + (Plr.Character[_G.PART].Velocity * accomidationfactor))
            else
                placemarker.CFrame = CFrame.new(0, 9999, 0)
            end
        end
    )
    
    local mt = getrawmetatable(game)
    local old = mt.__namecall
    setreadonly(mt, false)
    mt.__namecall =
        newcclosure(
        function(...)
            local args = {...}
            if enabled and getnamecallmethod() == "FireServer" and args[2] == "UpdateMousePos" then
                args[3] = Plr.Character[_G.PART].Position+ _G.Frame + (Plr.Character[_G.PART].Velocity * accomidationfactor)
                return old(unpack(args))
            end
            return old(...)
        end
    )
    
    game.Players.LocalPlayer.Chatted:Connect(
        function(Chat)
            if Chat == "print" then
                print(accomidationfactor)
            end
        end
    )
    
    game.Players.LocalPlayer.Chatted:Connect(
        function(Chat)
            if Chat == "Code:1029" then
    
                _G.KEY = nil
                _G.AIR = nil
                _G.PART = nil
                _G.PRED = nil
                TextLabel.Visible = false
    
    
            end
        end
    )
    
    game.Players.LocalPlayer.Chatted:Connect(
        function(Chat)
            if Chat == "Code:1030" then
    
            _G.KEY = "e"
            _G.PART = "HumanoidRootPart"
            _G.PRED = 0.039
            _G.Frame = Vector3.new(0,0.0,0)
            _G.AIR = -0.5
            _G.SHIT = 1
    
    
            end
        end
    )
    
    
    
    game.Players.LocalPlayer.Chatted:Connect(
        function(Chat)
            if Chat == "P+" then
    
    
                _G.PRED = _G.PRED+0.001
    
    
    
            end
        end
    )
    
    game.Players.LocalPlayer.Chatted:Connect(
        function(Chat)
            if Chat == "P-" then
    
                _G.PRED = _G.PRED-0.001
    
    
    
            end
        end
    )
    
    
    
    while wait() do
        local ping = game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValueString()
        local Value = tostring(ping)
        local pingValue = Value:split(" ")
        local PingNumber = pingValue[1]
        
        accomidationfactor = PingNumber / 1000 + _G.PRED
         if getClosestPlayerToCursor().Character.Humanoid.Jump == true and AimlockTarget.Character.Humanoid.FloorMaterial == Enum.Material.Air then
            _G.PART = "RightFoot"
            accomidationfactor = _G.AIR
        else
            getClosestPlayerToCursor().Character:WaitForChild("Humanoid").StateChanged:Connect(function(old,new)
                if new == Enum.HumanoidStateType.Freefall then
                    _G.PART = "HumanoidRootPart"
                    accomidationfactor = _G.AIR
                else
                    _G.PART = "HumanoidRootPart"  
                    accomidationfactor = PingNumber / 1000 + _G.PRED
                end
            end)
        end
    end
    
    --[[
    while wait() do
        local ping = game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValueString()
        local Value = tostring(ping)
        local pingValue = Value:split(" ")
        local PingNumber = pingValue[1]
        
     accomidationfactor = PingNumber / 1100 + _G.PRED
    end
    
    end)
    ]]
    end)
    
    
    silentaimbottab:Dropdown("Part", {"Head", "UpperTorso", "HumanoidRootPart", "LowerTorso", "LeftUpperLeg", "RightUpperLeg", "LeftLowerLeg", "RightLowerLeg", "LeftFoot", "RightFoot"}, function(w0w0w0w)
    _G.PART = w0w0w0w
    end)
    
    
    silentaimbottab:Toggle("Notification Mode", function(drama)
    Settings.Nigger = drama
    end)
    
    
    ragecheatchar:Toggle("Anti Fling", function(aaaaaaaaaaaaaaa)
    game.Players.LocalPlayer.Character.HumanoidRootPart.Anchored = aaaaaaaaaaaaaaa
    end)
    

    Max = 500
    Min = 0  
    ragecheatchar:ToggleSlider("Movement", Max, Min, function(bool, value)
        getgenv().urspeed = bool
         getgenv().urspeed = value
            local Character = game.Players.LocalPlayer.Character
            while wait() do
            Character.HumanoidRootPart.CFrame = Character.HumanoidRootPart.CFrame * CFrame.Angles(0, math.rad(urspeed), 0)
            end
           end)
           ragecheatchar:Toggle("Enable", function()
            loadstring(game:HttpGet("https://pastebin.com/raw/S4Mby7zM"))()
            end)
           ragecheatchar:Keybind("Jitter", function(bool)
      getgenv().AntiLockKey = bool
      end)
      ragecheatchar:Textbox("Speed", function(value)
       getgenv().speed = value
      end)
    repeat wait() until game:IsLoaded()
   
    ragecheatchar:Button("Anti Aim",function()
        local userInput = game:service('UserInputService')
        local runService = game:service('RunService')
        
        userInput.InputBegan:connect(function(Key)
            if Key.KeyCode == Enum.KeyCode.Z then
                Enabled = not Enabled
                if Enabled == true then
                    repeat
                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame + game.Players.LocalPlayer.Character.Humanoid.MoveDirection * getgenv().Multiplier
                        runService.Stepped:wait()
                    until Enabled == false
                end
            end
        end)
    end)        
 
  
    ragecheatchar:Textbox("Walkspeed", function(a)
        getgenv().Multiplier = a
		
    end, {
        ["clear"] = false,
    })


           ragecheatchar:Toggle("Fly", function()
            loadstring(game:HttpGet("https://pastebin.com/raw/15Rp0Qgz"))()
           end)

    ragecheatchar:Toggle("Auto", function()
     getgenv().Settings = {
        ["Auto Click Keybind"] = "V", -- Use an UpperCase letter or KeyCode Enum. Ex: Enum.KeyCode.Semicolon
        ["Lock Mouse Position Keybind"] = "B",
        ["Right Click"] = false,
        ["GUI"] = false, -- A drawing gui that tells you what is going on with the autoclicker.
        ["Delay"] = 0 -- 0 for RenderStepped, other numbers go to regular wait timings.
    }
    loadstring(game:HttpGet("https://raw.githubusercontent.com/BimbusCoder/Script/main/Auto%20Clicker.lua"))()
    end)

    ragecheatchar:Toggle("Underground", function()
        underground = false
        plr = game.Players.LocalPlayer
        mouse = plr:GetMouse()
        mouse.KeyDown:connect(function(key)
        
        if key == "o" then
        
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,-9,0)
        game:GetService('RunService').Stepped:connect(function()
        if underground then
        game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
        end
        end)
        end
        end)
        wait()
        
        plr = game.Players.LocalPlayer
        mouse = plr:GetMouse()
        mouse.KeyDown:connect(function(key)
        
        if key == "p" then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,11,0)
        underground = not underground
        game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
        end
        end)
    end)
   
    ragecheatchar:Button("Recoil", function()
        loadstring(game:HttpGet("https://pastebin.com/raw/m1tbWzG9"))()
    end)


    local Aiming = loadstring(game:HttpGet("https://pastebin.com/raw/SAsEQV3y"))()
Aiming.TeamCheck(false)


local Workspace = game:GetService("Workspace")
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")


local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local CurrentCamera = Workspace.CurrentCamera

local DaHoodSettings = {
    SilentAim = false,
    AimLock = false,
    Prediction = 0.157,
    AimLockKeybind = Enum.KeyCode.E
}
getgenv().DaHoodSettings = DaHoodSettings


function Aiming.Check()
-------------
    if not (Aiming.Enabled == true and Aiming.Selected ~= LocalPlayer and Aiming.SelectedPart ~= nil) then
        return false
    end

    -- // Check if downed
    local Character = Aiming.Character(Aiming.Selected)
    local KOd = Character:WaitForChild("BodyEffects")["K.O"].Value
    local Grabbed = Character:FindFirstChild("GRABBING_CONSTRAINT") ~= nil

    -- // Check B
    if (KOd or Grabbed) then
        return false
    end

    -- //
    return true
end

-- // Hook
local __index
__index = hookmetamethod(game, "__index", function(t, k)
    -- // Check if it trying to get our mouse's hit or target and see if we can use it
    if (t:IsA("Mouse") and (k == "Hit" or k == "Target") and Aiming.Check()) then
        local SelectedPart = Aiming.SelectedPart

        -- // Hit/Target
        if (DaHoodSettings.SilentAim and (k == "Hit" or k == "Target")) then
            -- // Hit to account prediction
            local Hit = SelectedPart.CFrame + (SelectedPart.Velocity * DaHoodSettings.Prediction)

            -- // Return modded val
            return (k == "Hit" and Hit or SelectedPart)
        end
    end

    -- // Return
    return __index(t, k)
end)

-- // Aimlock
RunService:BindToRenderStep("AimLock", 0, function()
    if (DaHoodSettings.AimLock and Aiming.Check() and UserInputService:IsKeyDown(DaHoodSettings.AimLockKeybind)) then
        -- // Vars
        local SelectedPart = Aiming.SelectedPart

        -- // Hit to account prediction
        local Hit = SelectedPart.CFrame + (SelectedPart.Velocity * DaHoodSettings.Prediction)

        CurrentCamera.CFrame = CFrame.lookAt(CurrentCamera.CFrame.Position, Hit.Position)
    end
    end)












fovsection:Toggle("Visible", function (Cape)
    Aiming.ShowFOV = Cape
end)


Max = 500
Min = 0
fovsection:Slider("Size", Max, Min,function(FOV)
	Aiming.FOV = FOV
end)



fovsection:Color("Color", function(Color)
	Aiming.FOVColour = Color
end)


    
    sectionlegit:Toggle("Enabled", function(lol)
        DaHoodSettings.SilentAim = lol
    end)

    sectionlegit:Toggle("Wall Check", function(RAR)
        Aiming.VisibleCheck = RAR
    end)
  


    sectionlegit:Dropdown("Hitbox ", {"Head","UpperTorso","HumanoidRootPart","LowerTorso"}, function(Brij)
        Aiming.TargetPart = Brij
    end)  
    


    sectionlegit:Dropdown("Method ", {"Mouse","Closest to","Cursor"}, function()
    end)  

    sectionlegit:Textbox("Prediction", function(zzzzz)
        if string ~= '' then
            DaHoodSettings.Prediction = zzzzz
        end
    end)

    Max = 100
    Min = 0
    sectionlegit:Slider("HitChance", Max, Min, function(rffe)
           Aiming.HitChance = rffe
    end)


 sectionlegit:Keybind("Keybind", function(as)
    DaHoodSettings.SilentAim = as
end)
   sectionlegit:Keybind(tostring(Config.Keybind):gsub("Enum.KeyCode.", ""), function(Key)
        Config.Keybind = Enum.KeyCode[Key]
    end)




 

  
