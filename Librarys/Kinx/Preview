

--------------------------------------------------------------------

-- Lib

local UILib = loadstring(game:HttpGet('https://raw.githubusercontent.com/inceldom/kinx/main/ui'))()

local win = UILib:Window("NBT HUB",Color3.fromRGB(44, 120, 224), Enum.KeyCode.RightControl)

--------------------------------------------------------------------

-- Sections

-- Main

local MainSection = win:Tab("Main")

local client = game.Players.LocalPlayer
local char = client.Character

local noclip = false

MainSection:Slider("WalkSpeed",0,1000,16, function(t)
	game:GetService("Players").LocalPlayer.Character.Humanoid.WalkSpeed = t
end)

MainSection:Slider("Jump Power",0,1000,50, function(t)
	game:GetService("Players").LocalPlayer.Character.Humanoid.JumpPower = t
end)

MainSection:Toggle("Noclip",false, function(t)
    noclip = t
end)


game:GetService("RunService").RenderStepped:Connect(function()
    if noclip == true then
        game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
    end
end)

MainSection:Slider("Gravity",0,500,196, function(t)
    workspace.Gravity = t
end)

MainSection:Toggle("Autopick Gun",false, function(t)
	if t then
		sheriff.Character.Humanoid.Died:Connect(function() game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = sheriff.Character.HumanoidRootPart.CFrame end)
	end
end)


MainSection:Button("Find Murder", function()
    for i,v in pairs(game:GetService("Players"):GetPlayers()) do
        if v.Character:FindFirstChild("Knife") or v.Backpack:FindFirstChild("Knife") then
            UILib:Notification("Notification", v.Name.."Is Murder", "Okay")    
        end
    end
end)

MainSection:Button("Find Murder", function()
    for i,v in pairs(game:GetService("Players"):GetPlayers()) do
        if v.Character:FindFirstChild("Revolver") or v.Backpack:FindFirstChild("Revolver") then
            UILib:Notification("Notification", v.Name.."Is Sheriff", "Okay")    
        end
    end
end)

MainSection:Button("Tp Tp Murder", function()
    for i,v in pairs(game:GetService("Players"):GetPlayers()) do
		if v.Character:FindFirstChild("Knife") or v.Backpack:FindFirstChild("Knife") then
			game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = v.Character.HumanoidRootPart.CFrame * CFrame.new(0, 3, 0)
		end
	end
end)

MainSection:Button("Tp Tp Sheriff", function()
	for i,v in pairs(game:GetService("Players"):GetPlayers()) do
		if v.Character:FindFirstChild("Revolver") or v.Backpack:FindFirstChild("Revolver") or v.Character:FindFirstChild("Gun") or v.Backpack:FindFirstChild("Gun") then
			game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = v.Character.HumanoidRootPart.CFrame * CFrame.new(0, 3, 0)
		end
	end
end)

-- Emotes
local EmotesSection = win:Tab("Emotes")

EmotesSection:Button("Sit", function()
    local string_1 = "sit";
    local Target = game:GetService("ReplicatedStorage").PlayEmote;
    Target:Fire(string_1);
end)

EmotesSection:Button("Zombie", function()
    local string_1 = "zombie";
    local Target = game:GetService("ReplicatedStorage").PlayEmote;
    Target:Fire(string_1);
end)

EmotesSection:Button("Spray", function()
    local string_1 = "SprayPaint";
    local Target = game:GetService("ReplicatedStorage").PlayEmote;
    Target:Fire(string_1);
end)

EmotesSection:Button("Dab", function()
    local string_1 = "dab";
    local Target = game:GetService("ReplicatedStorage").PlayEmote;
    Target:Fire(string_1);
end)

EmotesSection:Button("Ninja", function()
    local string_1 = "ninja";
    local Target = game:GetService("ReplicatedStorage").PlayEmote;
    Target:Fire(string_1);
end)

EmotesSection:Button("Floss", function()
    local string_1 = "floss";
    local Target = game:GetService("ReplicatedStorage").PlayEmote;
    Target:Fire(string_1);
end)

EmotesSection:Button("Zen", function()
    local string_1 = "zen";
    local Target = game:GetService("ReplicatedStorage").PlayEmote;
    Target:Fire(string_1);
end)

function ReturnColor(model)
    if game:GetService("Players")[model.Name].Backpack:FindFirstChild("Knife") or game:GetService("Players")[model.Name]:FindFirstChild("Knife") then return Color3.fromRGB(255,0,0) end
    if game:GetService("Players")[model.Name].Backpack:FindFirstChild("Gun") or game:GetService("Players")[model.Name].Backpack:FindFirstChild("Revolver") or game:GetService("Players")[model.Name]:FindFirstChild("Revolver") or game:GetService("Players")[model.Name]:FindFirstChild("Gun") then return Color3.fromRGB(0,0,255) end
    return Color3.fromRGB(0, 255, 0)
end

-- ESP
-- Add UI
local ESPSection = win:Tab("ESP")

local ESPEnabled = false
local DistanceEnabled = true
local TracersEnabled = true

pcall(function()
	
	Camera = game:GetService("Workspace").CurrentCamera
	RunService = game:GetService("RunService")
	camera = workspace.CurrentCamera
	Bottom = Vector2.new(camera.ViewportSize.X/2, camera.ViewportSize.Y)

	function GetPoint(vector3)
		local vector, onScreen = camera:WorldToScreenPoint(vector3)
		return {Vector2.new(vector.X,vector.Y),onScreen,vector.Z}
	end
	
	function MakeESP(model)
		local CurrentParent = model.Parent
	
		local TopL = Drawing.new("Line")
		local BottomL = Drawing.new("Line")
		local LeftL = Drawing.new("Line")
		local RightL = Drawing.new("Line")
		local Tracer = Drawing.new("Line")
		local Display = Drawing.new("Text")

        coroutine.resume(coroutine.create(function()
			while model.Parent == CurrentParent and model.Humanoid.Health > 0 do
				
				local Distance = (Camera.CFrame.Position - model.HumanoidRootPart.Position).Magnitude
                local GetP = GetPoint(model.Head.Position)
                local headps = model.Head.CFrame
                
				if ESPEnabled and GetP[2] then
					
                    -- Calculate Cords
                    local topright = headps * CFrame.new(3,0.5, 0)
                    local topleft = headps * CFrame.new(-3,0.5, 0)
                    local bottomleft = headps * CFrame.new(-3,-7,0)
                    local bottomright = headps * CFrame.new(3,-7,0)
					topright = GetPoint(topright.p)[1]
					topleft = GetPoint(topleft.p)[1]
					bottomleft = GetPoint(bottomleft.p)[1]
					bottomright = GetPoint(bottomright.p)[1]

                    teamcolor = ReturnColor(model)
                    TopL.Color, BottomL.Color, RightL.Color, LeftL.Color = teamcolor, teamcolor, teamcolor, teamcolor
                    TopL.From, BottomL.From, RightL.From, LeftL.From = topleft, bottomleft, topright, topleft
                    TopL.To, BottomL.To, RightL.To, LeftL.To = topright, bottomright, bottomright, bottomleft
					TopL.Visible, BottomL.Visible, RightL.Visible, LeftL.Visible = true, true, true, true
				else
					TopL.Visible, BottomL.Visible, RightL.Visible, LeftL.Visible = false, false, false, false
                end
                
                if ESPEnabled and TracersEnabled and GetP[2] then
                    Tracer.Color = ReturnColor(model)
					Tracer.From = Bottom
					Tracer.To = GetPoint(headps.p)[1]
					Tracer.Thickness = 1.5
					Tracer.Visible = true
				else
					Tracer.Visible = false
                end
                
				if ESPEnabled and DistanceEnabled and GetP[2] then
					Display.Visible = true
					Display.Position = GetPoint(headps.p + Vector3.new(0,0.5,0))[1]
					Display.Center = true
					Display.Text = tostring(math.floor(Distance)).." studs"
				else
					Display.Visible = false
                end
                
				RunService.RenderStepped:Wait()
			end
	
			TopL:Remove()
			BottomL:Remove()
			RightL:Remove()
			LeftL:Remove()
			Tracer:Remove()
			Display:Remove()
        
        end))
    end
    
	for _, Player in next, game:GetService("Players"):GetChildren() do
		if Player.Name ~= game.Players.LocalPlayer.Name then
			MakeESP(Player.Character)
			Player.CharacterAdded:Connect(function()
				delay(0.5, function()
					MakeESP(Player.Character)
				end)
			end)
		end	
	end
	
	game:GetService("Players").PlayerAdded:Connect(function(player)
        player.CharacterAdded:Connect(function()
            delay(0.5, function()
                MakeESP(player.Character)
            end)
		end)
	end)
	
end)

-- Enables/Disables ESP. Main toggle
ESPSection:Toggle("ESP",false, function(t)
    ESPEnabled = t
end)

-- Toggles tracers
ESPSection:Toggle("Tracers",true, function(t)
    TracersEnabled = t
end)

-- Toggles distance display
ESPSection:Toggle("Distance Display",false, function(t)
    DistanceEnabled = t
end)

---------------------------------------------------------------------------------------------------

-- Other Func
-- Add UI
local Settings = win:Tab("Settings")


Settings:Label("UI Toggle Key:  Right-Ctrl")

Settings:Button("Copy Discord Invite", function()
    setclipboard("https://discord.gg/4KqkXRDdGE")
    UILib:Notification("Notification", "Copied!", "Okay")
end)

