--//Made by Blissful#4992
local settings = {
    Color = Color3.fromRGB(255, 0, 0),
    Size = 15,
    Transparency = 1, -- 1 Visible - 0 Not Visible
    AutoScale = true
}

local space = game:GetService("Workspace")
local player = game:GetService("Players").LocalPlayer
local camera = space.CurrentCamera

local function NewText(color, size, transparency)
    local text = Drawing.new("Text")
    text.Visible = false
    text.Text = ""
    text.Position = Vector2.new(0, 0)
    text.Color = color
    text.Size = size
    text.Center = true
    text.Transparency = transparency
    return text
end

local function Visibility(state, lib)
    for u, x in pairs(lib) do
        x.Visible = state
    end
end

local function Size(size, lib)
    for u, x in pairs(lib) do
        x.Size = size
    end
end

for i, v in pairs(game:GetService("Players"):GetPlayers()) do
    local library = {
        name = NewText(settings.Color, settings.Size, settings.Transparency)
    }
    local function ESP()
        local connection
        connection = game:GetService("RunService").RenderStepped:Connect(function()
            if v.Character ~= nil and v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("HumanoidRootPart") ~= nil and v.Name ~= player.Name and v.Character.Humanoid.Health > 0 then
                local HumanoidRootPart_Pos, OnScreen = camera:WorldToViewportPoint(v.Character.HumanoidRootPart.Position)
                if OnScreen then
                    library.name.Text = v.Name
                    library.name.Position = Vector2.new(HumanoidRootPart_Pos.X, HumanoidRootPart_Pos.Y)
                    --// AutoScale
                    if settings.AutoScale then
                        local distance = (Vector3.new(camera.CFrame.X, camera.CFrame.Y, camera.CFrame.Z) - v.Character.HumanoidRootPart.Position).magnitude
                        local textsize = math.clamp(1/distance*1000, 2, 30) -- 2 is min text size, 30 is max text size, change to your liking
                        Size(textsize, library)
                    else 
                        Size(settings.Size, library)
                    end
                    --//--
                    Visibility(true, library)
                else 
                    Visibility(false, library)
                end
            else 
                Visibility(false, library)
                if game.Players:FindFirstChild(v.Name) == nil then
                    connection:Disconnect()
                end
            end
        end)
    end
    coroutine.wrap(ESP)()
end

game.Players.PlayerAdded:Connect(function(newplr)
    print(newplr)
    local library = {
        name = NewText(settings.Color, settings.Size, settings.Transparency)
    }
    local function ESP()
        local connection
        connection = game:GetService("RunService").RenderStepped:Connect(function()
            if newplr.Character ~= nil and newplr.Character:FindFirstChild("Humanoid") ~= nil and newplr.Character:FindFirstChild("HumanoidRootPart") ~= nil and newplr.Name ~= player.Name and newplr.Character.Humanoid.Health > 0 then
                local HumanoidRootPart_Pos, OnScreen = camera:WorldToViewportPoint(newplr.Character.HumanoidRootPart.Position)
                if OnScreen then
                    library.name.Text = newplr.Name
                    library.name.Position = Vector2.new(HumanoidRootPart_Pos.X, HumanoidRootPart_Pos.Y)
                    --// AutoScale
                    if settings.AutoScale then
                        local distance = (Vector3.new(camera.CFrame.X, camera.CFrame.Y, camera.CFrame.Z) - newplr.Character.HumanoidRootPart.Position).magnitude
                        local textsize = math.clamp(1/distance*1000, 2, 30) -- 2 is min text size, 20 is max text size, change to your liking
                        Size(textsize, library)
                    else 
                        Size(settings.Size, library)
                    end
                    --//--
                    Visibility(true, library)
                else 
                    Visibility(false, library)
                end
            else 
                Visibility(false, library)
                if game.Players:FindFirstChild(newplr.Name) == nil then
                    connection:Disconnect()
                end
            end
        end)
    end
    coroutine.wrap(ESP)()
end)
