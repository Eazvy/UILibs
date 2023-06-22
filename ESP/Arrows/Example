-- Made by Blissful#4992

local DistFromCenter = 80
local TriangleHeight = 16
local TriangleWidth = 16
local TriangleFilled = true
local TriangleTransparency = 0
local TriangleThickness = 1
local TriangleColor = Color3.fromRGB(255, 255, 255)
local AntiAliasing = false

----------------------------------------------------------------

local Players = game:service("Players")
local Player = Players.LocalPlayer
local Camera = workspace.CurrentCamera
local RS = game:service("RunService")

local V3 = Vector3.new
local V2 = Vector2.new
local CF = CFrame.new
local COS = math.cos
local SIN = math.sin
local RAD = math.rad
local DRAWING = Drawing.new
local CWRAP = coroutine.wrap
local ROUND = math.round

local function GetRelative(pos, char)
    if not char then return V2(0,0) end

    local rootP = char.PrimaryPart.Position
    local camP = Camera.CFrame.Position
    local relative = CF(V3(rootP.X, camP.Y, rootP.Z), camP):PointToObjectSpace(pos)

    return V2(relative.X, relative.Z)
end

local function RelativeToCenter(v)
    return Camera.ViewportSize/2 - v
end

local function RotateVect(v, a)
    a = RAD(a)
    local x = v.x * COS(a) - v.y * SIN(a)
    local y = v.x * SIN(a) + v.y * COS(a)

    return V2(x, y)
end

local function DrawTriangle(color)
    local l = DRAWING("Triangle")
    l.Visible = false
    l.Color = color
    l.Filled = TriangleFilled
    l.Thickness = TriangleThickness
    l.Transparency = 1-TriangleTransparency
    return l
end

local function AntiA(v)
    if (not AntiAliasing) then return v end
    return V2(ROUND(v.x), ROUND(v.y))
end

local function ShowArrow(PLAYER)
    local Arrow = DrawTriangle(TriangleColor)

    local function Update()
        local c ; c = RS.RenderStepped:Connect(function()
            if PLAYER and PLAYER.Character then
                local CHAR = PLAYER.Character
                local HUM = CHAR:FindFirstChildOfClass("Humanoid")

                if HUM and CHAR.PrimaryPart ~= nil and HUM.Health > 0 then
                    local _,vis = Camera:WorldToViewportPoint(CHAR.PrimaryPart.Position)
                    if vis == false then
                        local rel = GetRelative(CHAR.PrimaryPart.Position, Player.Character)
                        local direction = rel.unit

                        local base  = direction * DistFromCenter
                        local sideLength = TriangleWidth/2
                        local baseL = base + RotateVect(direction, 90) * sideLength
                        local baseR = base + RotateVect(direction, -90) * sideLength

                        local tip = direction * (DistFromCenter + TriangleHeight)
                        
                        Arrow.PointA = AntiA(RelativeToCenter(baseL))
                        Arrow.PointB = AntiA(RelativeToCenter(baseR))

                        Arrow.PointC = AntiA(RelativeToCenter(tip))

                        Arrow.Visible = true

                    else Arrow.Visible = false end
                else Arrow.Visible = false end
            else 
                Arrow.Visible = false

                if not PLAYER or not PLAYER.Parent then
                    Arrow:Remove()
                    c:Disconnect()
                end
            end
        end)
    end

    CWRAP(Update)()
end

for _,v in pairs(Players:GetChildren()) do
    if v.Name ~= Player.Name then
        ShowArrow(v)
    end
end

Players.PlayerAdded:Connect(function(v)
    if v.Name ~= Player.Name then
        ShowArrow(v)
    end
end)
