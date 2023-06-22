-- Preview: https://gyazo.com/02cfb4aa8659ba5f6ee67a90514cc34d
-- Made by Blissful#4992
local Settings = {
    Color = Color3.fromRGB(255, 203, 138), -- Color of the line
    Thickness = 1, -- Thickness of the line (Overruled by AutoThickness if activated)
    Transparency = 1, -- 1 Visible - 0 Not Visible
    AutoThickness = true, -- Makes Thickness above futile, scales according to distance, good for less encumbered screen
    Length = 15, -- In studs of the line
    Smoothness = 0.2 -- 0.01 - Less Smooth(Faster), 1 - Smoother (Slower)
}

local toggle = true -- use this variable if you wanna integrate into a GUI

local player = game:GetService("Players").LocalPlayer
local camera = game:GetService("Workspace").CurrentCamera

local function ESP(plr) --//Main function handling specific plr loop esp for line etc
    local line = Drawing.new("Line") --// Parse and Set the line for tracer
    line.Visible = false
    line.From = Vector2.new(0, 0)
    line.To = Vector2.new(0, 0)
    line.Color = Settings.Color
    line.Thickness = Settings.Thickness
    line.Transparency = Settings.Transparency

    local function Updater() --// Function to update the ESP therefore, line destinations etc every /render/
        local connection
        connection = game:GetService("RunService").RenderStepped:Connect(function() -- Putting function in a connection var in order to disconnect if needed, to save performance
            if toggle and plr.Character ~= nil and plr.Character:FindFirstChild("Humanoid") ~= nil and plr.Character:FindFirstChild("HumanoidRootPart") ~= nil and plr.Character.Humanoid.Health > 0 and plr.Character:FindFirstChild("Head") ~= nil then
                local headpos, OnScreen = camera:WorldToViewportPoint(plr.Character.Head.Position)
                if OnScreen then -- checks if player is on screen or not
                    local offsetCFrame = CFrame.new(0, 0, -Settings.Length)
                    local check = false
                    line.From = Vector2.new(headpos.X, headpos.Y)
                    if Settings.AutoThickness then
                        local distance = (player.Character.HumanoidRootPart.Position - plr.Character.HumanoidRootPart.Position).magnitude --//AutoThickness
                        local value = math.clamp(1/distance*100, 0.1, 3) --0.1 is min thickness, 4 is max
                        line.Thickness = value
                    end
                    repeat
                        local dir = plr.Character.Head.CFrame:ToWorldSpace(offsetCFrame)
                        offsetCFrame = offsetCFrame * CFrame.new(0, 0, Settings.Smoothness)
                        local dirpos, vis = camera:WorldToViewportPoint(Vector3.new(dir.X, dir.Y, dir.Z))
                        if vis then
                            check = true
                            line.To = Vector2.new(dirpos.X, dirpos.Y)
                            line.Visible = true
                            offsetCFrame = CFrame.new(0, 0, -Settings.Length)
                        end
                    until check == true
                else 
                    line.Visible = false
                end
            else 
                line.Visible = false
                if game.Players:FindFirstChild(plr.Name) == nil then
                    connection:Disconnect()
                end
            end
        end)
    end
    coroutine.wrap(Updater)()
end

for i, v in pairs(game:GetService("Players"):GetPlayers()) do
    if v.Name ~= player.Name then
        coroutine.wrap(ESP)(v)
    end
end

game.Players.PlayerAdded:Connect(function(newplr)
    if newplr.Name ~= player.Name then
        coroutine.wrap(ESP)(newplr)
    end
end)
