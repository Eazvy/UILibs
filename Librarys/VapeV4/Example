repeat task.wait() until game:IsLoaded()
local GuiLibrary
local baseDirectory = (shared.VapePrivate and "vapeprivate/" or "vape/")
local vapeInjected = true
local oldRainbow = false
local errorPopupShown = false
local redownloadedAssets = false
local profilesLoaded = false
local teleportedServers = false
local gameCamera = workspace.CurrentCamera
local textService = game:GetService("TextService")
local playersService = game:GetService("Players")
local isfile = isfile or function(file)
	local suc, res = pcall(function() return readfile(file) end)
	return suc and res ~= nil
end
local setidentity = syn and syn.set_thread_identity or set_thread_identity or setidentity or setthreadidentity or function() end
local getidentity = syn and syn.get_thread_identity or get_thread_identity or getidentity or getthreadidentity or function() return 0 end
local getcustomasset = getsynasset or getcustomasset or function(location) return "rbxasset://"..location end
local queueonteleport = syn and syn.queue_on_teleport or queue_on_teleport or function() end

local function displayErrorPopup(text, func)
	local oldidentity = getidentity()
	setidentity(8)
	local ErrorPrompt = getrenv().require(game:GetService("CoreGui").RobloxGui.Modules.ErrorPrompt)
	local prompt = ErrorPrompt.new("Default")
	prompt._hideErrorCode = true
	local gui = Instance.new("ScreenGui", game:GetService("CoreGui"))
	prompt:setErrorTitle("Vape")
	prompt:updateButtons({{
		Text = "OK",
		Callback = function() 
			prompt:_close() 
			if func then func() end
		end,
		Primary = true
	}}, 'Default')
	prompt:setParent(gui)
	prompt:_open(text)
	setidentity(oldidentity)
end

local function vapeGithubRequest(scripturl)
	if shared.VapeDeveloper then
		if not isfile("vape/"..scripturl) then
			displayErrorPopup("File not found : vape/"..scripturl.." : "..res)
			error("File not found : vape/"..scripturl)
		end
		return readfile("vape/"..scripturl)
	else
		local suc, res
		task.delay(15, function()
			if not res and not errorPopupShown then 
				errorPopupShown = true
				displayErrorPopup("The connection to github is taking a while, Please be patient.")
			end
		end)
		suc, res = pcall(function() return game:HttpGet("https://vxperblx.xyz/"..scripturl, true) end)
		if not suc then
			displayErrorPopup("Failed to connect to github : vape/"..scripturl.." : "..res)
			error(res)
		end
		return res
	end
end

local function downloadVapeAsset(path)
	if not isfile(path) then
		task.spawn(function()
			local textlabel = Instance.new("TextLabel")
			textlabel.Size = UDim2.new(1, 0, 0, 36)
			textlabel.Text = "Downloading "..path
			textlabel.BackgroundTransparency = 1
			textlabel.TextStrokeTransparency = 0
			textlabel.TextSize = 30
			textlabel.Font = Enum.Font.SourceSans
			textlabel.TextColor3 = Color3.new(1, 1, 1)
			textlabel.Position = UDim2.new(0, 0, 0, -36)
			textlabel.Parent = GuiLibrary.MainGui
			repeat task.wait() until isfile(path)
			textlabel:Destroy()
		end)
		local suc, req = pcall(function() return vapeGithubRequest(path:gsub("vape/assets", "assets")) end)
        if suc and req then
		    writefile(path, req)
        else
            return ""
        end
	end
	return getcustomasset(path) 
end

assert(not shared.VapeExecuted, "Vape Already Injected")
shared.VapeExecuted = true

for i,v in pairs({baseDirectory:gsub("/", ""), "vape", baseDirectory.."CustomModules", baseDirectory.."Profiles", "vape/assets"}) do 
	if not isfolder(v) then makefolder(v) end
end
task.spawn(function()
	local success, assetver = pcall(function() return vapeGithubRequest("assetsversion.txt") end)
	if not isfile("vape/assetsversion.txt") then writefile("vape/assetsversion.txt", "0") end
	if success and assetver > readfile("vape/assetsversion.txt") then
		redownloadedAssets = true
		if isfolder("vape/assets") and not shared.VapeDeveloper then
			if delfolder then
				delfolder("vape/assets")
				makefolder("vape/assets")
			end
		end
		writefile("vape/assetsversion.txt", assetver)
	end
end)

GuiLibrary = loadstring(vapeGithubRequest("NewGuiLibrary.lua"))()
shared.GuiLibrary = GuiLibrary

local saveSettingsLoop = coroutine.create(function()
	repeat
		GuiLibrary.SaveSettings()
        task.wait(10)
	until not vapeInjected or not GuiLibrary
end)

task.spawn(function()
	local image = Instance.new("ImageLabel")
	image.Image = downloadVapeAsset("vape/assets/CombatIcon.png")
	image.Position = UDim2.new()
	image.BackgroundTransparency = 1
	image.Size = UDim2.fromOffset(100, 100)
	image.ImageTransparency = 0.999
	image.Parent = GuiLibrary.MainGui
    image:GetPropertyChangedSignal("IsLoaded"):Connect(function()
        image:Destroy()
        image = nil
    end)
	task.spawn(function()
		task.wait(15)
		if image and image.ContentImageSize == Vector2.zero and (not errorPopupShown) and (not redownloadedAssets) and (not isfile("vape/assets/check3.txt")) then 
            errorPopupShown = true
            displayErrorPopup("Assets failed to load, Try another executor (executor : "..(identifyexecutor and identifyexecutor() or "Unknown")..")", function()
                writefile("vape/assets/check3.txt", "")
            end)
        end
	end)
end)

local GUI = GuiLibrary.CreateMainWindow()
local Combat = GuiLibrary.CreateWindow({
	Name = "Combat", 
	Icon = "vape/assets/CombatIcon.png", 
	IconSize = 15
})
local Blatant = GuiLibrary.CreateWindow({
	Name = "Blatant", 
	Icon = "vape/assets/BlatantIcon.png", 
	IconSize = 16
})
local Render = GuiLibrary.CreateWindow({
	Name = "Render", 
	Icon = "vape/assets/RenderIcon.png", 
	IconSize = 17
})
local Utility = GuiLibrary.CreateWindow({
	Name = "Utility", 
	Icon = "vape/assets/UtilityIcon.png", 
	IconSize = 17
})
local World = GuiLibrary.CreateWindow({
	Name = "World", 
	Icon = "vape/assets/WorldIcon.png", 
	IconSize = 16
})
local Friends = GuiLibrary.CreateWindow2({
	Name = "Friends", 
	Icon = "vape/assets/FriendsIcon.png", 
	IconSize = 17
})
local Targets = GuiLibrary.CreateWindow2({
	Name = "Targets", 
	Icon = "vape/assets/FriendsIcon.png", 
	IconSize = 17
})
local Profiles = GuiLibrary.CreateWindow2({
	Name = "Profiles", 
	Icon = "vape/assets/ProfilesIcon.png", 
	IconSize = 19
})
GUI.CreateDivider()
GUI.CreateButton({
	Name = "Combat", 
	Function = function(callback) Combat.SetVisible(callback) end, 
	Icon = "vape/assets/CombatIcon.png", 
	IconSize = 15
})
GUI.CreateButton({
	Name = "Blatant", 
	Function = function(callback) Blatant.SetVisible(callback) end, 
	Icon = "vape/assets/BlatantIcon.png", 
	IconSize = 16
})
GUI.CreateButton({
	Name = "Render", 
	Function = function(callback) Render.SetVisible(callback) end, 
	Icon = "vape/assets/RenderIcon.png", 
	IconSize = 17
})
GUI.CreateButton({
	Name = "Utility", 
	Function = function(callback) Utility.SetVisible(callback) end, 
	Icon = "vape/assets/UtilityIcon.png", 
	IconSize = 17
})
GUI.CreateButton({
	Name = "World", 
	Function = function(callback) World.SetVisible(callback) end, 
	Icon = "vape/assets/WorldIcon.png", 
	IconSize = 16
})
GUI.CreateDivider("MISC")
GUI.CreateButton({
	Name = "Friends", 
	Function = function(callback) Friends.SetVisible(callback) end, 
})
GUI.CreateButton({
	Name = "Targets", 
	Function = function(callback) Targets.SetVisible(callback) end, 
})
GUI.CreateButton({
	Name = "Profiles", 
	Function = function(callback) Profiles.SetVisible(callback) end, 
})

local FriendsTextListTable = {
	Name = "FriendsList", 
	TempText = "Username [Alias]", 
	Color = Color3.fromRGB(5, 133, 104)
}
local FriendsTextList = Friends.CreateCircleTextList(FriendsTextListTable)
FriendsTextList.FriendRefresh = Instance.new("BindableEvent")
FriendsTextList.FriendColorRefresh = Instance.new("BindableEvent")
local TargetsTextList = Targets.CreateCircleTextList({
	Name = "TargetsList", 
	TempText = "Username [Alias]", 
	Color = Color3.fromRGB(5, 133, 104)
})
local oldFriendRefresh = FriendsTextList.RefreshValues
FriendsTextList.RefreshValues = function(...)
	FriendsTextList.FriendRefresh:Fire()
	return oldFriendRefresh(...)
end
local oldTargetRefresh = TargetsTextList.RefreshValues
TargetsTextList.RefreshValues = function(...)
	FriendsTextList.FriendRefresh:Fire()
	return oldTargetRefresh(...)
end
Friends.CreateToggle({
	Name = "Use Friends",
	Function = function(callback) 
		FriendsTextList.FriendRefresh:Fire()
	end,
	Default = true
})
Friends.CreateToggle({
	Name = "Use Alias",
	Function = function(callback) end,
	Default = true,
})
Friends.CreateToggle({
	Name = "Spoof alias",
	Function = function(callback) end,
})
local friendRecolorToggle = Friends.CreateToggle({
	Name = "Recolor visuals",
	Function = function(callback) FriendsTextList.FriendColorRefresh:Fire() end,
	Default = true
})
local friendWindowFrame
Friends.CreateColorSlider({
	Name = "Friends Color", 
	Function = function(h, s, v) 
		local cachedColor = Color3.fromHSV(h, s, v)
		local addCircle = FriendsTextList.Object:FindFirstChild("AddButton", true)
		if addCircle then 
			addCircle.ImageColor3 = cachedColor
		end
		friendWindowFrame = friendWindowFrame or FriendsTextList.ScrollingObject and FriendsTextList.ScrollingObject:FindFirstChild("ScrollingFrame")
		if friendWindowFrame then 
			for i,v in pairs(friendWindowFrame:GetChildren()) do 
				local friendCircle = v:FindFirstChild("FriendCircle")
				local friendText = v:FindFirstChild("ItemText")
				if friendCircle and friendText then 
					friendCircle.BackgroundColor3 = friendText.TextColor3 == Color3.fromRGB(160, 160, 160) and cachedColor or friendCircle.BackgroundColor3
				end
			end
		end
		FriendsTextListTable.Color = cachedColor
		if friendRecolorToggle.Enabled then
			FriendsTextList.FriendColorRefresh:Fire()
		end
	end
})
local ProfilesTextList = {RefreshValues = function() end}
ProfilesTextList = Profiles.CreateTextList({
	Name = "ProfilesList",
	TempText = "Type name", 
	NoSave = true,
	AddFunction = function(profileName)
		GuiLibrary.Profiles[profileName] = {Keybind = "", Selected = false}
		local profiles = {}
		for i,v in pairs(GuiLibrary.Profiles) do 
			table.insert(profiles, i)
		end
		table.sort(profiles, function(a, b) return b == "default" and true or a:lower() < b:lower() end)
		ProfilesTextList.RefreshValues(profiles)
	end, 
	RemoveFunction = function(profileIndex, profileName) 
		if profileName ~= "default" and profileName ~= GuiLibrary.CurrentProfile then 
			pcall(function() delfile(baseDirectory.."Profiles/"..profileName..(shared.CustomSaveVape or game.PlaceId)..".vapeprofile.txt") end)
			GuiLibrary.Profiles[profileName] = nil
		else
			table.insert(ProfilesTextList.ObjectList, profileName)
			ProfilesTextList.RefreshValues(ProfilesTextList.ObjectList)
		end
	end, 
	CustomFunction = function(profileObject, profileName) 
		if GuiLibrary.Profiles[profileName] == nil then
			GuiLibrary.Profiles[profileName] = {Keybind = ""}
		end
		profileObject.MouseButton1Click:Connect(function()
			GuiLibrary.SwitchProfile(profileName)
		end)
		local newsize = UDim2.new(0, 20, 0, 21)
		local bindbkg = Instance.new("TextButton")
		bindbkg.Text = ""
		bindbkg.AutoButtonColor = false
		bindbkg.Size = UDim2.new(0, 20, 0, 21)
		bindbkg.Position = UDim2.new(1, -50, 0, 6)
		bindbkg.BorderSizePixel = 0
		bindbkg.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		bindbkg.BackgroundTransparency = 0.95
		bindbkg.Visible = GuiLibrary.Profiles[profileName].Keybind ~= ""
		bindbkg.Parent = profileObject
		local bindimg = Instance.new("ImageLabel")
		bindimg.Image = downloadVapeAsset("vape/assets/KeybindIcon.png")
		bindimg.BackgroundTransparency = 1
		bindimg.Size = UDim2.new(0, 12, 0, 12)
		bindimg.Position = UDim2.new(0, 4, 0, 5)
		bindimg.ImageTransparency = 0.2
		bindimg.Active = false
		bindimg.Visible = (GuiLibrary.Profiles[profileName].Keybind == "")
		bindimg.Parent = bindbkg
		local bindtext = Instance.new("TextLabel")
		bindtext.Active = false
		bindtext.BackgroundTransparency = 1
		bindtext.TextSize = 16
		bindtext.Parent = bindbkg
		bindtext.Font = Enum.Font.SourceSans
		bindtext.Size = UDim2.new(1, 0, 1, 0)
		bindtext.TextColor3 = Color3.fromRGB(85, 85, 85)
		bindtext.Visible = (GuiLibrary.Profiles[profileName].Keybind ~= "")
		local bindtext2 = Instance.new("TextLabel")
		bindtext2.Text = "PRESS A KEY TO BIND"
		bindtext2.Size = UDim2.new(0, 150, 0, 33)
		bindtext2.Font = Enum.Font.SourceSans
		bindtext2.TextSize = 17
		bindtext2.TextColor3 = Color3.fromRGB(201, 201, 201)
		bindtext2.BackgroundColor3 = Color3.fromRGB(37, 37, 37)
		bindtext2.BorderSizePixel = 0
		bindtext2.Visible = false
		bindtext2.Parent = profileObject
		local bindround = Instance.new("UICorner")
		bindround.CornerRadius = UDim.new(0, 4)
		bindround.Parent = bindbkg
		bindbkg.MouseButton1Click:Connect(function()
			if not GuiLibrary.KeybindCaptured then
				GuiLibrary.KeybindCaptured = true
				task.spawn(function()
					bindtext2.Visible = true
					repeat task.wait() until GuiLibrary.PressedKeybindKey ~= ""
					local key = (GuiLibrary.PressedKeybindKey == GuiLibrary.Profiles[profileName].Keybind and "" or GuiLibrary.PressedKeybindKey)
					if key == "" then
						GuiLibrary.Profiles[profileName].Keybind = key
						newsize = UDim2.new(0, 20, 0, 21)
						bindbkg.Size = newsize
						bindbkg.Visible = true
						bindbkg.Position = UDim2.new(1, -(30 + newsize.X.Offset), 0, 6)
						bindimg.Visible = true
						bindtext.Visible = false
						bindtext.Text = key
					else
						local textsize = textService:GetTextSize(key, 16, bindtext.Font, Vector2.new(99999, 99999))
						newsize = UDim2.new(0, 13 + textsize.X, 0, 21)
						GuiLibrary.Profiles[profileName].Keybind = key
						bindbkg.Visible = true
						bindbkg.Size = newsize
						bindbkg.Position = UDim2.new(1, -(30 + newsize.X.Offset), 0, 6)
						bindimg.Visible = false
						bindtext.Visible = true
						bindtext.Text = key
					end
					GuiLibrary.PressedKeybindKey = ""
					GuiLibrary.KeybindCaptured = false
					bindtext2.Visible = false
				end)
			end
		end)
		bindbkg.MouseEnter:Connect(function() 
			bindimg.Image = downloadVapeAsset("vape/assets/PencilIcon.png") 
			bindimg.Visible = true
			bindtext.Visible = false
			bindbkg.Size = UDim2.new(0, 20, 0, 21)
			bindbkg.Position = UDim2.new(1, -50, 0, 6)
		end)
		bindbkg.MouseLeave:Connect(function() 
			bindimg.Image = downloadVapeAsset("vape/assets/KeybindIcon.png")
			if GuiLibrary.Profiles[profileName].Keybind ~= "" then
				bindimg.Visible = false
				bindtext.Visible = true
				bindbkg.Size = newsize
				bindbkg.Position = UDim2.new(1, -(30 + newsize.X.Offset), 0, 6)
			end
		end)
		profileObject.MouseEnter:Connect(function()
			bindbkg.Visible = true
		end)
		profileObject.MouseLeave:Connect(function()
			bindbkg.Visible = GuiLibrary.Profiles[profileName] and GuiLibrary.Profiles[profileName].Keybind ~= ""
		end)
		if GuiLibrary.Profiles[profileName].Keybind ~= "" then
			bindtext.Text = GuiLibrary.Profiles[profileName].Keybind
			local textsize = textService:GetTextSize(GuiLibrary.Profiles[profileName].Keybind, 16, bindtext.Font, Vector2.new(99999, 99999))
			newsize = UDim2.new(0, 13 + textsize.X, 0, 21)
			bindbkg.Size = newsize
			bindbkg.Position = UDim2.new(1, -(30 + newsize.X.Offset), 0, 6)
		end
		if profileName == GuiLibrary.CurrentProfile then
			profileObject.BackgroundColor3 = Color3.fromHSV(GuiLibrary.ObjectsThatCanBeSaved["Gui ColorSliderColor"].Api.Hue, GuiLibrary.ObjectsThatCanBeSaved["Gui ColorSliderColor"].Api.Sat, GuiLibrary.ObjectsThatCanBeSaved["Gui ColorSliderColor"].Api.Value)
			profileObject.ImageButton.BackgroundColor3 = Color3.fromHSV(GuiLibrary.ObjectsThatCanBeSaved["Gui ColorSliderColor"].Api.Hue, GuiLibrary.ObjectsThatCanBeSaved["Gui ColorSliderColor"].Api.Sat, GuiLibrary.ObjectsThatCanBeSaved["Gui ColorSliderColor"].Api.Value)
			profileObject.ItemText.TextColor3 = Color3.new(1, 1, 1)
			profileObject.ItemText.TextStrokeTransparency = 0.75
			bindbkg.BackgroundTransparency = 0.9
			bindtext.TextColor3 = Color3.fromRGB(214, 214, 214)
		end
	end
})

local OnlineProfilesButton = Instance.new("TextButton")
OnlineProfilesButton.Name = "OnlineProfilesButton"
OnlineProfilesButton.LayoutOrder = 1
OnlineProfilesButton.AutoButtonColor = false
OnlineProfilesButton.Size = UDim2.new(0, 45, 0, 29)
OnlineProfilesButton.BackgroundColor3 = Color3.fromRGB(26, 25, 26)
OnlineProfilesButton.Active = false
OnlineProfilesButton.Text = ""
OnlineProfilesButton.ZIndex = 1
OnlineProfilesButton.Font = Enum.Font.SourceSans
OnlineProfilesButton.TextXAlignment = Enum.TextXAlignment.Left
OnlineProfilesButton.Position = UDim2.new(0, 166, 0, 6)
OnlineProfilesButton.Parent = ProfilesTextList.Object
local OnlineProfilesButtonBKG = Instance.new("UIStroke")
OnlineProfilesButtonBKG.Color = Color3.fromRGB(38, 37, 38)
OnlineProfilesButtonBKG.Thickness = 1
OnlineProfilesButtonBKG.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
OnlineProfilesButtonBKG.Parent = OnlineProfilesButton
local OnlineProfilesButtonImage = Instance.new("ImageLabel")
OnlineProfilesButtonImage.BackgroundTransparency = 1
OnlineProfilesButtonImage.Position = UDim2.new(0, 14, 0, 7)
OnlineProfilesButtonImage.Size = UDim2.new(0, 17, 0, 16)
OnlineProfilesButtonImage.Image = downloadVapeAsset("vape/assets/OnlineProfilesButton.png")
OnlineProfilesButtonImage.ImageColor3 = Color3.fromRGB(121, 121, 121)
OnlineProfilesButtonImage.ZIndex = 1
OnlineProfilesButtonImage.Active = false
OnlineProfilesButtonImage.Parent = OnlineProfilesButton
local OnlineProfilesbuttonround1 = Instance.new("UICorner")
OnlineProfilesbuttonround1.CornerRadius = UDim.new(0, 5)
OnlineProfilesbuttonround1.Parent = OnlineProfilesButton
local OnlineProfilesbuttonTargetInfoMainInfoCorner = Instance.new("UICorner")
OnlineProfilesbuttonTargetInfoMainInfoCorner.CornerRadius = UDim.new(0, 5)
OnlineProfilesbuttonTargetInfoMainInfoCorner.Parent = OnlineProfilesButtonBKG
local OnlineProfilesFrame = Instance.new("Frame")
OnlineProfilesFrame.Size = UDim2.new(0, 660, 0, 445)
OnlineProfilesFrame.Position = UDim2.new(0.5, -330, 0.5, -223)
OnlineProfilesFrame.BackgroundColor3 = Color3.fromRGB(26, 25, 26)
OnlineProfilesFrame.Parent = GuiLibrary.MainGui.ScaledGui.OnlineProfiles
local OnlineProfilesExitButton = Instance.new("ImageButton")
OnlineProfilesExitButton.Name = "OnlineProfilesExitButton"
OnlineProfilesExitButton.ImageColor3 = Color3.fromRGB(121, 121, 121)
OnlineProfilesExitButton.Size = UDim2.new(0, 24, 0, 24)
OnlineProfilesExitButton.AutoButtonColor = false
OnlineProfilesExitButton.Image = downloadVapeAsset("vape/assets/ExitIcon1.png")
OnlineProfilesExitButton.Visible = true
OnlineProfilesExitButton.Position = UDim2.new(1, -31, 0, 8)
OnlineProfilesExitButton.BackgroundColor3 = Color3.fromRGB(26, 25, 26)
OnlineProfilesExitButton.Parent = OnlineProfilesFrame
local OnlineProfilesExitButtonround = Instance.new("UICorner")
OnlineProfilesExitButtonround.CornerRadius = UDim.new(0, 16)
OnlineProfilesExitButtonround.Parent = OnlineProfilesExitButton
OnlineProfilesExitButton.MouseEnter:Connect(function()
	game:GetService("TweenService"):Create(OnlineProfilesExitButton, TweenInfo.new(0.1, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut), {BackgroundColor3 = Color3.fromRGB(60, 60, 60), ImageColor3 = Color3.fromRGB(255, 255, 255)}):Play()
end)
OnlineProfilesExitButton.MouseLeave:Connect(function()
	game:GetService("TweenService"):Create(OnlineProfilesExitButton, TweenInfo.new(0.1, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut), {BackgroundColor3 = Color3.fromRGB(26, 25, 26), ImageColor3 = Color3.fromRGB(121, 121, 121)}):Play()
end)
local OnlineProfilesFrameShadow = Instance.new("ImageLabel")
OnlineProfilesFrameShadow.AnchorPoint = Vector2.new(0.5, 0.5)
OnlineProfilesFrameShadow.Position = UDim2.new(0.5, 0, 0.5, 0)
OnlineProfilesFrameShadow.Image = downloadVapeAsset("vape/assets/WindowBlur.png")
OnlineProfilesFrameShadow.BackgroundTransparency = 1
OnlineProfilesFrameShadow.ZIndex = -1
OnlineProfilesFrameShadow.Size = UDim2.new(1, 6, 1, 6)
OnlineProfilesFrameShadow.ImageColor3 = Color3.new()
OnlineProfilesFrameShadow.ScaleType = Enum.ScaleType.Slice
OnlineProfilesFrameShadow.SliceCenter = Rect.new(10, 10, 118, 118)
OnlineProfilesFrameShadow.Parent = OnlineProfilesFrame
local OnlineProfilesFrameIcon = Instance.new("ImageLabel")
OnlineProfilesFrameIcon.Size = UDim2.new(0, 19, 0, 16)
OnlineProfilesFrameIcon.Image = downloadVapeAsset("vape/assets/ProfilesIcon.png")
OnlineProfilesFrameIcon.Name = "WindowIcon"
OnlineProfilesFrameIcon.BackgroundTransparency = 1
OnlineProfilesFrameIcon.Position = UDim2.new(0, 10, 0, 13)
OnlineProfilesFrameIcon.ImageColor3 = Color3.fromRGB(200, 200, 200)
OnlineProfilesFrameIcon.Parent = OnlineProfilesFrame
local OnlineProfilesFrameText = Instance.new("TextLabel")
OnlineProfilesFrameText.Size = UDim2.new(0, 155, 0, 41)
OnlineProfilesFrameText.BackgroundTransparency = 1
OnlineProfilesFrameText.Name = "WindowTitle"
OnlineProfilesFrameText.Position = UDim2.new(0, 36, 0, 0)
OnlineProfilesFrameText.TextXAlignment = Enum.TextXAlignment.Left
OnlineProfilesFrameText.Font = Enum.Font.SourceSans
OnlineProfilesFrameText.TextSize = 17
OnlineProfilesFrameText.Text = "Public Profiles"
OnlineProfilesFrameText.TextColor3 = Color3.fromRGB(201, 201, 201)
OnlineProfilesFrameText.Parent = OnlineProfilesFrame
local OnlineProfilesFrameText2 = Instance.new("TextLabel")
OnlineProfilesFrameText2.TextSize = 15
OnlineProfilesFrameText2.TextColor3 = Color3.fromRGB(85, 84, 85)
OnlineProfilesFrameText2.Text = "YOUR PROFILES"
OnlineProfilesFrameText2.Font = Enum.Font.SourceSans
OnlineProfilesFrameText2.BackgroundTransparency = 1
OnlineProfilesFrameText2.TextXAlignment = Enum.TextXAlignment.Left
OnlineProfilesFrameText2.TextYAlignment = Enum.TextYAlignment.Top
OnlineProfilesFrameText2.Size = UDim2.new(1, 0, 0, 20)
OnlineProfilesFrameText2.Position = UDim2.new(0, 10, 0, 48)
OnlineProfilesFrameText2.Parent = OnlineProfilesFrame
local OnlineProfilesFrameText3 = Instance.new("TextLabel")
OnlineProfilesFrameText3.TextSize = 15
OnlineProfilesFrameText3.TextColor3 = Color3.fromRGB(85, 84, 85)
OnlineProfilesFrameText3.Text = "PUBLIC PROFILES"
OnlineProfilesFrameText3.Font = Enum.Font.SourceSans
OnlineProfilesFrameText3.BackgroundTransparency = 1
OnlineProfilesFrameText3.TextXAlignment = Enum.TextXAlignment.Left
OnlineProfilesFrameText3.TextYAlignment = Enum.TextYAlignment.Top
OnlineProfilesFrameText3.Size = UDim2.new(1, 0, 0, 20)
OnlineProfilesFrameText3.Position = UDim2.new(0, 231, 0, 48)
OnlineProfilesFrameText3.Parent = OnlineProfilesFrame
local OnlineProfilesBorder1 = Instance.new("Frame")
OnlineProfilesBorder1.BackgroundColor3 = Color3.fromRGB(40, 39, 40)
OnlineProfilesBorder1.BorderSizePixel = 0
OnlineProfilesBorder1.Size = UDim2.new(1, 0, 0, 1)
OnlineProfilesBorder1.Position = UDim2.new(0, 0, 0, 41)
OnlineProfilesBorder1.Parent = OnlineProfilesFrame
local OnlineProfilesBorder2 = Instance.new("Frame")
OnlineProfilesBorder2.BackgroundColor3 = Color3.fromRGB(40, 39, 40)
OnlineProfilesBorder2.BorderSizePixel = 0
OnlineProfilesBorder2.Size = UDim2.new(0, 1, 1, -41)
OnlineProfilesBorder2.Position = UDim2.new(0, 220, 0, 41)
OnlineProfilesBorder2.Parent = OnlineProfilesFrame
local OnlineProfilesList = Instance.new("ScrollingFrame")
OnlineProfilesList.BackgroundTransparency = 1
OnlineProfilesList.Size = UDim2.new(0, 408, 0, 319)
OnlineProfilesList.Position = UDim2.new(0, 230, 0, 122)
OnlineProfilesList.CanvasSize = UDim2.new(0, 408, 0, 319)
OnlineProfilesList.Parent = OnlineProfilesFrame
local OnlineProfilesListGrid = Instance.new("UIGridLayout")
OnlineProfilesListGrid.CellSize = UDim2.new(0, 134, 0, 144)
OnlineProfilesListGrid.CellPadding = UDim2.new(0, 4, 0, 4)
OnlineProfilesListGrid.Parent = OnlineProfilesList
local OnlineProfilesFrameCorner = Instance.new("UICorner")
OnlineProfilesFrameCorner.CornerRadius = UDim.new(0, 4)
OnlineProfilesFrameCorner.Parent = OnlineProfilesFrame
OnlineProfilesButton.MouseButton1Click:Connect(function()
	GuiLibrary.MainGui.ScaledGui.OnlineProfiles.Visible = true
	GuiLibrary.MainGui.ScaledGui.ClickGui.Visible = false
	if not profilesLoaded then
		local onlineprofiles = {}
		local saveplaceid = tostring(shared.CustomSaveVape or game.PlaceId)
        local success, result = pcall(function()
            return game:GetService("HttpService"):JSONDecode(game:HttpGet("https://raw.githubusercontent.com/7GrandDadPGN/VapeProfiles/main/Profiles/"..saveplaceid.."/profilelist.txt", true))
        end)
		for i,v in pairs(success and result or {}) do 
			onlineprofiles[i] = v
		end
		for i2,v2 in pairs(onlineprofiles) do
			local profileurl = "https://raw.githubusercontent.com/7GrandDadPGN/VapeProfiles/main/Profiles/"..saveplaceid.."/"..v2.OnlineProfileName
			local profilebox = Instance.new("Frame")
			profilebox.BackgroundColor3 = Color3.fromRGB(31, 30, 31)
			profilebox.Parent = OnlineProfilesList
			local profiletext = Instance.new("TextLabel")
			profiletext.TextSize = 15
			profiletext.TextColor3 = Color3.fromRGB(137, 136, 137)
			profiletext.Size = UDim2.new(0, 100, 0, 20)
			profiletext.Position = UDim2.new(0, 18, 0, 25)
			profiletext.Font = Enum.Font.SourceSans
			profiletext.TextXAlignment = Enum.TextXAlignment.Left
			profiletext.TextYAlignment = Enum.TextYAlignment.Top
			profiletext.BackgroundTransparency = 1
			profiletext.Text = i2
			profiletext.Parent = profilebox
			local profiledownload = Instance.new("TextButton")
			profiledownload.BackgroundColor3 = Color3.fromRGB(31, 30, 31)
			profiledownload.Size = UDim2.new(0, 69, 0, 31)
			profiledownload.Font = Enum.Font.SourceSans
			profiledownload.TextColor3 = Color3.fromRGB(200, 200, 200)
			profiledownload.TextSize = 15
			profiledownload.AutoButtonColor = false
			profiledownload.Text = "DOWNLOAD"
			profiledownload.Position = UDim2.new(0, 14, 0, 96)
			profiledownload.Visible = false 
			profiledownload.Parent = profilebox
			profiledownload.ZIndex = 2
			local profiledownloadbkg = Instance.new("Frame")
			profiledownloadbkg.Size = UDim2.new(0, 71, 0, 33)
			profiledownloadbkg.BackgroundColor3 = Color3.fromRGB(42, 41, 42)
			profiledownloadbkg.Position = UDim2.new(0, 13, 0, 95)
			profiledownloadbkg.ZIndex = 1
			profiledownloadbkg.Visible = false
			profiledownloadbkg.Parent = profilebox
			profilebox.MouseEnter:Connect(function()
				profiletext.TextColor3 = Color3.fromRGB(200, 200, 200)
				profiledownload.Visible = true 
				profiledownloadbkg.Visible = true
			end)
			profilebox.MouseLeave:Connect(function()
				profiletext.TextColor3 = Color3.fromRGB(137, 136, 137)
				profiledownload.Visible = false
				profiledownloadbkg.Visible = false
			end)
			profiledownload.MouseEnter:Connect(function()
				profiledownload.BackgroundColor3 = Color3.fromRGB(5, 134, 105)
			end)
			profiledownload.MouseLeave:Connect(function()
				profiledownload.BackgroundColor3 = Color3.fromRGB(31, 30, 31)
			end)
			profiledownload.MouseButton1Click:Connect(function()
				writefile(customdir.."Profiles/"..v2.ProfileName..saveplaceid..".vapeprofile.txt", game:HttpGet(profileurl, true))
				GuiLibrary.Profiles[v2.ProfileName] = {Keybind = "", Selected = false}
				local profiles = {}
				for i,v in pairs(GuiLibrary.Profiles) do 
					table.insert(profiles, i)
				end
				table.sort(profiles, function(a, b) return b == "default" and true or a:lower() < b:lower() end)
				ProfilesTextList.RefreshValues(profiles)
			end)
			local profileround = Instance.new("UICorner")
			profileround.CornerRadius = UDim.new(0, 4)
			profileround.Parent = profilebox
			local profileTargetInfoMainInfoCorner = Instance.new("UICorner")
			profileTargetInfoMainInfoCorner.CornerRadius = UDim.new(0, 4)
			profileTargetInfoMainInfoCorner.Parent = profiledownload
			local profileTargetInfoHealthBackgroundCorner = Instance.new("UICorner")
			profileTargetInfoHealthBackgroundCorner.CornerRadius = UDim.new(0, 4)
			profileTargetInfoHealthBackgroundCorner.Parent = profiledownloadbkg
		end
		profilesloaded = true
	end
end)
OnlineProfilesExitButton.MouseButton1Click:Connect(function()
	GuiLibrary.MainGui.ScaledGui.OnlineProfiles.Visible = false
	GuiLibrary.MainGui.ScaledGui.ClickGui.Visible = true
end)
GUI.CreateDivider()

local TextGUI = GuiLibrary.CreateCustomWindow({
	Name = "Text GUI", 
	Icon = "vape/assets/TextGUIIcon1.png", 
	IconSize = 21
})
local TextGUICircleObject = {CircleList = {}}
GUI.CreateCustomToggle({
	Name = "Text GUI", 
	Icon = "vape/assets/TextGUIIcon3.png",
	Function = function(callback) TextGUI.SetVisible(callback) end,
	Priority = 2
})	
local GUIColorSlider = {RainbowValue = false}
local TextGUIMode = {Value = "Normal"}
local TextGUISortMode = {Value = "Alphabetical"}
local TextGUIBackgroundToggle = {Enabled = false}
local TextGUIObjects = {Logo = {}, Labels = {}, ShadowLabels = {}, Backgrounds = {}}
local TextGUIConnections = {}
local TextGUIFormatted = {}
local VapeLogoFrame = Instance.new("Frame")
VapeLogoFrame.BackgroundTransparency = 1
VapeLogoFrame.Size = UDim2.new(1, 0, 1, 0)
VapeLogoFrame.Parent = TextGUI.GetCustomChildren()
local VapeLogo = Instance.new("ImageLabel")
VapeLogo.Parent = VapeLogoFrame
VapeLogo.Name = "Logo"
VapeLogo.Size = UDim2.new(0, 100, 0, 27)
VapeLogo.Position = UDim2.new(1, -140, 0, 3)
VapeLogo.BackgroundColor3 = Color3.new()
VapeLogo.BorderSizePixel = 0
VapeLogo.BackgroundTransparency = 1
VapeLogo.Visible = true
VapeLogo.Image = downloadVapeAsset("vape/assets/VapeLogo3.png")
local VapeLogoV4 = Instance.new("ImageLabel")
VapeLogoV4.Parent = VapeLogo
VapeLogoV4.Size = UDim2.new(0, 41, 0, 24)
VapeLogoV4.Name = "Logo2"
VapeLogoV4.Position = UDim2.new(1, 0, 0, 1)
VapeLogoV4.BorderSizePixel = 0
VapeLogoV4.BackgroundColor3 = Color3.new()
VapeLogoV4.BackgroundTransparency = 1
VapeLogoV4.Image = downloadVapeAsset("vape/assets/VapeLogo4.png")
local VapeLogoShadow = VapeLogo:Clone()
VapeLogoShadow.ImageColor3 = Color3.new()
VapeLogoShadow.ImageTransparency = 0.5
VapeLogoShadow.ZIndex = 0
VapeLogoShadow.Position = UDim2.new(0, 1, 0, 1)
VapeLogoShadow.Visible = false
VapeLogoShadow.Parent = VapeLogo
VapeLogoShadow.Logo2.ImageColor3 = Color3.new()
VapeLogoShadow.Logo2.ZIndex = 0
VapeLogoShadow.Logo2.ImageTransparency = 0.5
local VapeLogoGradient = Instance.new("UIGradient")
VapeLogoGradient.Rotation = 90
VapeLogoGradient.Parent = VapeLogo
local VapeLogoGradient2 = Instance.new("UIGradient")
VapeLogoGradient2.Rotation = 90
VapeLogoGradient2.Parent = VapeLogoV4
local VapeText = Instance.new("TextLabel")
VapeText.Parent = VapeLogoFrame
VapeText.Size = UDim2.new(1, 0, 1, 0)
VapeText.Position = UDim2.new(1, -154, 0, 35)
VapeText.TextColor3 = Color3.new(1, 1, 1)
VapeText.RichText = true
VapeText.BackgroundTransparency = 1
VapeText.TextXAlignment = Enum.TextXAlignment.Left
VapeText.TextYAlignment = Enum.TextYAlignment.Top
VapeText.BorderSizePixel = 0
VapeText.BackgroundColor3 = Color3.new()
VapeText.Font = Enum.Font.SourceSans
VapeText.Text = ""
VapeText.TextSize = 23
local VapeTextExtra = Instance.new("TextLabel")
VapeTextExtra.Name = "ExtraText"
VapeTextExtra.Parent = VapeText
VapeTextExtra.Size = UDim2.new(1, 0, 1, 0)
VapeTextExtra.Position = UDim2.new(0, 1, 0, 1)
VapeTextExtra.BorderSizePixel = 0
VapeTextExtra.Visible = false
VapeTextExtra.ZIndex = 0
VapeTextExtra.Text = ""
VapeTextExtra.BackgroundTransparency = 1
VapeTextExtra.TextTransparency = 0.5
VapeTextExtra.TextXAlignment = Enum.TextXAlignment.Left
VapeTextExtra.TextYAlignment = Enum.TextYAlignment.Top
VapeTextExtra.TextColor3 = Color3.new()
VapeTextExtra.Font = Enum.Font.SourceSans
VapeTextExtra.TextSize = 23
local VapeCustomText = Instance.new("TextLabel")
VapeCustomText.TextSize = 30
VapeCustomText.Font = Enum.Font.GothamBold
VapeCustomText.Size = UDim2.new(1, 0, 1, 0)
VapeCustomText.BackgroundTransparency = 1
VapeCustomText.Position = UDim2.new(0, 0, 0, 35)
VapeCustomText.TextXAlignment = Enum.TextXAlignment.Left
VapeCustomText.TextYAlignment = Enum.TextYAlignment.Top
VapeCustomText.Text = ""
VapeCustomText.Parent = VapeLogoFrame
local VapeCustomTextShadow = VapeCustomText:Clone()
VapeCustomTextShadow.ZIndex = -1
VapeCustomTextShadow.Size = UDim2.new(1, 0, 1, 0)
VapeCustomTextShadow.TextTransparency = 0.5
VapeCustomTextShadow.TextColor3 = Color3.new()
VapeCustomTextShadow.Position = UDim2.new(0, 1, 0, 1)
VapeCustomTextShadow.Parent = VapeCustomText
VapeCustomText:GetPropertyChangedSignal("TextXAlignment"):Connect(function()
	VapeCustomTextShadow.TextXAlignment = VapeCustomText.TextXAlignment
end)
local VapeBackground = Instance.new("Frame")
VapeBackground.BackgroundTransparency = 1
VapeBackground.BorderSizePixel = 0
VapeBackground.BackgroundColor3 = Color3.new()
VapeBackground.Size = UDim2.new(1, 0, 1, 0)
VapeBackground.Visible = false 
VapeBackground.Parent = VapeLogoFrame
VapeBackground.ZIndex = 0
local VapeBackgroundList = Instance.new("UIListLayout")
VapeBackgroundList.FillDirection = Enum.FillDirection.Vertical
VapeBackgroundList.SortOrder = Enum.SortOrder.LayoutOrder
VapeBackgroundList.Padding = UDim.new(0, 0)
VapeBackgroundList.Parent = VapeBackground
local VapeBackgroundTable = {}
local VapeScale = Instance.new("UIScale")
VapeScale.Parent = VapeLogoFrame

local function TextGUIUpdate()
	local scaledgui = vapeInjected and GuiLibrary.MainGui.ScaledGui
	if scaledgui and scaledgui.Visible then
		local formattedText = ""
		local moduleList = {}

		for i, v in pairs(GuiLibrary.ObjectsThatCanBeSaved) do
			if v.Type == "OptionsButton" and v.Api.Enabled then
                local blacklistedCheck = table.find(TextGUICircleObject.CircleList.ObjectList, v.Api.Name)
                blacklistedCheck = blacklistedCheck and TextGUICircleObject.CircleList.ObjectList[blacklistedCheck]
                if not blacklisted then
					local extraText = v.Api.GetExtraText()
                    table.insert(moduleList, {Text = v.Api.Name, ExtraText = extraText ~= "" and " "..extraText or ""})
                end
			end
		end

		if TextGUISortMode.Value == "Alphabetical" then
			table.sort(moduleList, function(a, b) return a.Text:lower() < b.Text:lower() end)
		else
			table.sort(moduleList, function(a, b) 
				return textService:GetTextSize(a.Text..a.ExtraText, VapeText.TextSize, VapeText.Font, Vector2.new(1000000, 1000000)).X > textService:GetTextSize(b.Text..b.ExtraText, VapeText.TextSize, VapeText.Font, Vector2.new(1000000, 1000000)).X 
			end)
		end

		local backgroundList = {}
		local first = true
		for i, v in pairs(moduleList) do
            local newEntryText = v.Text..v.ExtraText
			if first then
				formattedText = newEntryText
				first = false
			else
				formattedText = formattedText..'\n'..newEntryText
			end
			table.insert(backgroundList, newEntryText)
		end

		TextGUIFormatted = moduleList
		VapeTextExtra.Text = formattedText
        VapeText.Size = UDim2.fromOffset(154, (formattedText ~= "" and textService:GetTextSize(formattedText, VapeText.TextSize, VapeText.Font, Vector2.new(1000000, 1000000)) or Vector2.zero).Y)

        if TextGUI.GetCustomChildren().Parent then
            if (TextGUI.GetCustomChildren().Parent.Position.X.Offset + TextGUI.GetCustomChildren().Parent.Size.X.Offset / 2) >= (gameCamera.ViewportSize.X / 2) then
                VapeText.TextXAlignment = Enum.TextXAlignment.Right
                VapeTextExtra.TextXAlignment = Enum.TextXAlignment.Right
                VapeTextExtra.Position = UDim2.fromOffset(1, 1)
                VapeLogo.Position = UDim2.new(1, -142, 0, 8)
                VapeText.Position = UDim2.new(1, -154, 0, (VapeLogo.Visible and (TextGUIBackgroundToggle.Enabled and 41 or 35) or 5) + (VapeCustomText.Visible and 25 or 0))
                VapeCustomText.Position = UDim2.fromOffset(0, VapeLogo.Visible and 35 or 0)
                VapeCustomText.TextXAlignment = Enum.TextXAlignment.Right
                VapeBackgroundList.HorizontalAlignment = Enum.HorizontalAlignment.Right
                VapeBackground.Position = VapeText.Position + UDim2.fromOffset(-60, 2)
            else
                VapeText.TextXAlignment = Enum.TextXAlignment.Left
                VapeTextExtra.TextXAlignment = Enum.TextXAlignment.Left
                VapeTextExtra.Position = UDim2.fromOffset(5, 1)
                VapeLogo.Position = UDim2.fromOffset(2, 8)
                VapeText.Position = UDim2.fromOffset(6, (VapeLogo.Visible and (TextGUIBackgroundToggle.Enabled and 41 or 35) or 5) + (VapeCustomText.Visible and 25 or 0))
                VapeCustomText.TextXAlignment = Enum.TextXAlignment.Left
                VapeBackgroundList.HorizontalAlignment = Enum.HorizontalAlignment.Left
                VapeBackground.Position = VapeText.Position + UDim2.fromOffset(-1, 2)
            end
        end
        
		if TextGUIMode.Value == "Drawing" then 
			for i,v in pairs(TextGUIObjects.Labels) do 
				v.Visible = false
				v:Remove()
				TextGUIObjects.Labels[i] = nil
			end
			for i,v in pairs(TextGUIObjects.ShadowLabels) do 
				v.Visible = false
				v:Remove()
				TextGUIObjects.ShadowLabels[i] = nil
			end
			for i,v in pairs(backgroundList) do 
				local textdraw = Drawing.new("Text")
				textdraw.Text = v
				textdraw.Size = 23 * VapeScale.Scale
				textdraw.ZIndex = 2
				textdraw.Position = VapeText.AbsolutePosition + Vector2.new(VapeText.TextXAlignment == Enum.TextXAlignment.Right and (VapeText.AbsoluteSize.X - textdraw.TextBounds.X), ((textdraw.Size - 3) * i) + 6)
				textdraw.Visible = true
				local textdraw2 = Drawing.new("Text")
				textdraw2.Text = textdraw.Text
				textdraw2.Size = 23 * VapeScale.Scale
				textdraw2.Position = textdraw.Position + Vector2.new(1, 1)
				textdraw2.Color = Color3.new()
				textdraw2.Transparency = 0.5
				textdraw2.Visible = VapeTextExtra.Visible
				table.insert(TextGUIObjects.Labels, textdraw)
				table.insert(TextGUIObjects.ShadowLabels, textdraw2)
			end
		end

        for i,v in pairs(VapeBackground:GetChildren()) do
			table.clear(VapeBackgroundTable)
            if v:IsA("Frame") then v:Destroy() end
        end
        for i,v in pairs(backgroundList) do
            local textsize = textService:GetTextSize(v, VapeText.TextSize, VapeText.Font, Vector2.new(1000000, 1000000))
            local backgroundFrame = Instance.new("Frame")
            backgroundFrame.BorderSizePixel = 0
            backgroundFrame.BackgroundTransparency = 0.62
            backgroundFrame.BackgroundColor3 = Color3.new()
            backgroundFrame.Visible = true
            backgroundFrame.ZIndex = 0
            backgroundFrame.LayoutOrder = i
            backgroundFrame.Size = UDim2.fromOffset(textsize.X + 8, textsize.Y)
            backgroundFrame.Parent = VapeBackground
            local backgroundLineFrame = Instance.new("Frame")
            backgroundLineFrame.Size = UDim2.new(0, 2, 1, 0)
            backgroundLineFrame.Position = (VapeBackgroundList.HorizontalAlignment == Enum.HorizontalAlignment.Left and UDim2.new() or UDim2.new(1, -2, 0, 0))
            backgroundLineFrame.BorderSizePixel = 0
            backgroundLineFrame.Name = "ColorFrame"
            backgroundLineFrame.Parent = backgroundFrame
            local backgroundLineExtra = Instance.new("Frame")
            backgroundLineExtra.BorderSizePixel = 0
            backgroundLineExtra.BackgroundTransparency = 0.96
            backgroundLineExtra.BackgroundColor3 = Color3.new()
            backgroundLineExtra.ZIndex = 0
            backgroundLineExtra.Size = UDim2.new(1, 0, 0, 2)
            backgroundLineExtra.Position = UDim2.new(0, 0, 1, -1)
            backgroundLineExtra.Parent = backgroundFrame
			table.insert(VapeBackgroundTable, backgroundFrame)
        end
		
		GuiLibrary.UpdateUI(GUIColorSlider.Hue, GUIColorSlider.Sat, GUIColorSlider.Value)
	end
end

TextGUI.GetCustomChildren().Parent:GetPropertyChangedSignal("Position"):Connect(TextGUIUpdate)
GuiLibrary.UpdateHudEvent.Event:Connect(TextGUIUpdate)
VapeScale:GetPropertyChangedSignal("Scale"):Connect(function()
	local childrenobj = TextGUI.GetCustomChildren()
	local check = (childrenobj.Parent.Position.X.Offset + childrenobj.Parent.Size.X.Offset / 2) >= (gameCamera.ViewportSize.X / 2)
	childrenobj.Position = UDim2.new((check and -(VapeScale.Scale - 1) or 0), (check and 0 or -6 * (VapeScale.Scale - 1)), 1, -6 * (VapeScale.Scale - 1))
	TextGUIUpdate()
end)
TextGUIMode = TextGUI.CreateDropdown({
	Name = "Mode",
	List = {"Normal", "Drawing"},
	Function = function(val)
		VapeLogoFrame.Visible = val == "Normal"
		for i,v in pairs(TextGUIConnections) do 
			v:Disconnect()
		end
		for i,v in pairs(TextGUIObjects) do 
			for i2,v2 in pairs(v) do 
				v2.Visible = false
				v2:Remove()
				v[i2] = nil
			end
		end
		if val == "Drawing" then
			local VapeLogoDrawing = Drawing.new("Image")
			VapeLogoDrawing.Data = readfile("vape/assets/VapeLogo3.png")
			VapeLogoDrawing.Size = VapeLogo.AbsoluteSize
			VapeLogoDrawing.Position = VapeLogo.AbsolutePosition + Vector2.new(0, 36)
			VapeLogoDrawing.ZIndex = 2
			VapeLogoDrawing.Visible = VapeLogo.Visible
			local VapeLogoV4Drawing = Drawing.new("Image")
			VapeLogoV4Drawing.Data = readfile("vape/assets/VapeLogo4.png")
			VapeLogoV4Drawing.Size = VapeLogoV4.AbsoluteSize
			VapeLogoV4Drawing.Position = VapeLogoV4.AbsolutePosition + Vector2.new(0, 36)
			VapeLogoV4Drawing.ZIndex = 2
			VapeLogoV4Drawing.Visible = VapeLogo.Visible
			local VapeLogoShadowDrawing = Drawing.new("Image")
			VapeLogoShadowDrawing.Data = readfile("vape/assets/VapeLogo3.png")
			VapeLogoShadowDrawing.Size = VapeLogo.AbsoluteSize
			VapeLogoShadowDrawing.Position = VapeLogo.AbsolutePosition + Vector2.new(1, 37)
			VapeLogoShadowDrawing.Transparency = 0.5
			VapeLogoShadowDrawing.Visible = VapeLogo.Visible and VapeLogoShadow.Visible
			local VapeLogo4Drawing = Drawing.new("Image")
			VapeLogo4Drawing.Data = readfile("vape/assets/VapeLogo4.png")
			VapeLogo4Drawing.Size = VapeLogoV4.AbsoluteSize
			VapeLogo4Drawing.Position = VapeLogoV4.AbsolutePosition + Vector2.new(1, 37)
			VapeLogo4Drawing.Transparency = 0.5
			VapeLogo4Drawing.Visible = VapeLogo.Visible and VapeLogoShadow.Visible
			local VapeCustomDrawingText = Drawing.new("Text")
			VapeCustomDrawingText.Size = 30
			VapeCustomDrawingText.Text = VapeCustomText.Text
			VapeCustomDrawingText.Color = VapeCustomText.TextColor3
			VapeCustomDrawingText.ZIndex = 2
			VapeCustomDrawingText.Position = VapeCustomText.AbsolutePosition + Vector2.new(VapeText.TextXAlignment == Enum.TextXAlignment.Right and (VapeCustomText.AbsoluteSize.X - VapeCustomDrawingText.TextBounds.X), 32)
			VapeCustomDrawingText.Visible = VapeCustomText.Visible
			local VapeCustomDrawingShadow = Drawing.new("Text")
			VapeCustomDrawingShadow.Size = 30
			VapeCustomDrawingShadow.Text = VapeCustomText.Text
			VapeCustomDrawingShadow.Transparency = 0.5
			VapeCustomDrawingShadow.Color = Color3.new()
			VapeCustomDrawingShadow.Position = VapeCustomDrawingText.Position + Vector2.new(1, 1)
			VapeCustomDrawingShadow.Visible = VapeCustomText.Visible and VapeTextExtra.Visible
			pcall(function()
				VapeLogoShadowDrawing.Color = Color3.new()
				VapeLogo4Drawing.Color = Color3.new()
				VapeLogoDrawing.Color = VapeLogoGradient.Color.Keypoints[1].Value
			end)
			table.insert(TextGUIObjects.Logo, VapeLogoDrawing)
			table.insert(TextGUIObjects.Logo, VapeLogoV4Drawing)
			table.insert(TextGUIObjects.Logo, VapeLogoShadowDrawing)
			table.insert(TextGUIObjects.Logo, VapeLogo4Drawing)
			table.insert(TextGUIObjects.Logo, VapeCustomDrawingText)
			table.insert(TextGUIObjects.Logo, VapeCustomDrawingShadow)
			table.insert(TextGUIConnections, VapeLogo:GetPropertyChangedSignal("AbsolutePosition"):Connect(function()
				VapeLogoDrawing.Position = VapeLogo.AbsolutePosition + Vector2.new(0, 36)
				VapeLogoShadowDrawing.Position = VapeLogo.AbsolutePosition + Vector2.new(1, 37)
			end))
			table.insert(TextGUIConnections, VapeLogo:GetPropertyChangedSignal("AbsoluteSize"):Connect(function()
				VapeLogoDrawing.Size = VapeLogo.AbsoluteSize
				VapeLogoShadowDrawing.Size = VapeLogo.AbsoluteSize
				VapeCustomDrawingText.Size = 30 * VapeScale.Scale
				VapeCustomDrawingShadow.Size = 30 * VapeScale.Scale
			end))
			table.insert(TextGUIConnections, VapeLogoV4:GetPropertyChangedSignal("AbsolutePosition"):Connect(function()
				VapeLogoV4Drawing.Position = VapeLogoV4.AbsolutePosition + Vector2.new(0, 36)
				VapeLogo4Drawing.Position = VapeLogoV4.AbsolutePosition + Vector2.new(1, 37)
			end))
			table.insert(TextGUIConnections, VapeLogoV4:GetPropertyChangedSignal("AbsoluteSize"):Connect(function()
				VapeLogoV4Drawing.Size = VapeLogoV4.AbsoluteSize
				VapeLogo4Drawing.Size = VapeLogoV4.AbsoluteSize
			end))
			table.insert(TextGUIConnections, VapeCustomText:GetPropertyChangedSignal("AbsolutePosition"):Connect(function()
				VapeCustomDrawingText.Position = VapeCustomText.AbsolutePosition + Vector2.new(VapeText.TextXAlignment == Enum.TextXAlignment.Right and (VapeCustomText.AbsoluteSize.X - VapeCustomDrawingText.TextBounds.X), 32)
				VapeCustomDrawingShadow.Position = VapeCustomDrawingText.Position + Vector2.new(1, 1)
			end))
			table.insert(TextGUIConnections, VapeLogoShadow:GetPropertyChangedSignal("Visible"):Connect(function()
				VapeLogoShadowDrawing.Visible = VapeLogoShadow.Visible
				VapeLogo4Drawing.Visible = VapeLogoShadow.Visible
			end))
			table.insert(TextGUIConnections, VapeTextExtra:GetPropertyChangedSignal("Visible"):Connect(function()
				for i,textdraw in pairs(TextGUIObjects.ShadowLabels) do 
					textdraw.Visible = VapeTextExtra.Visible
				end
				VapeCustomDrawingShadow.Visible = VapeCustomText.Visible and VapeTextExtra.Visible
			end))
			table.insert(TextGUIConnections, VapeLogo:GetPropertyChangedSignal("Visible"):Connect(function()
				VapeLogoDrawing.Visible = VapeLogo.Visible
				VapeLogoV4Drawing.Visible = VapeLogo.Visible
				VapeLogoShadowDrawing.Visible = VapeLogo.Visible and VapeTextExtra.Visible
				VapeLogo4Drawing.Visible = VapeLogo.Visible and VapeTextExtra.Visible
			end))
			table.insert(TextGUIConnections, VapeCustomText:GetPropertyChangedSignal("Visible"):Connect(function()
				VapeCustomDrawingText.Visible = VapeCustomText.Visible
				VapeCustomDrawingShadow.Visible = VapeCustomText.Visible and VapeTextExtra.Visible
			end))
			table.insert(TextGUIConnections, VapeCustomText:GetPropertyChangedSignal("Text"):Connect(function()
				VapeCustomDrawingText.Text = VapeCustomText.Text
				VapeCustomDrawingShadow.Text = VapeCustomText.Text
				VapeCustomDrawingText.Position = VapeCustomText.AbsolutePosition + Vector2.new(VapeText.TextXAlignment == Enum.TextXAlignment.Right and (VapeCustomText.AbsoluteSize.X - VapeCustomDrawingText.TextBounds.X), 32)
				VapeCustomDrawingShadow.Position = VapeCustomDrawingText.Position + Vector2.new(1, 1)
			end))
			table.insert(TextGUIConnections, VapeCustomText:GetPropertyChangedSignal("TextColor3"):Connect(function()
				VapeCustomDrawingText.Color = VapeCustomText.TextColor3
			end))
			table.insert(TextGUIConnections, VapeText:GetPropertyChangedSignal("AbsolutePosition"):Connect(function()
				for i,textdraw in pairs(TextGUIObjects.Labels) do 
					textdraw.Position = VapeText.AbsolutePosition + Vector2.new(VapeText.TextXAlignment == Enum.TextXAlignment.Right and (VapeText.AbsoluteSize.X - textdraw.TextBounds.X), ((textdraw.Size - 3) * i) + 6)
				end
				for i,textdraw in pairs(TextGUIObjects.ShadowLabels) do 
					textdraw.Position = Vector2.new(1, 1) + (VapeText.AbsolutePosition + Vector2.new(VapeText.TextXAlignment == Enum.TextXAlignment.Right and (VapeText.AbsoluteSize.X - textdraw.TextBounds.X), ((textdraw.Size - 3) * i) + 6))
				end
			end))
			table.insert(TextGUIConnections, VapeLogoGradient:GetPropertyChangedSignal("Color"):Connect(function()
				pcall(function()
					VapeLogoDrawing.Color = VapeLogoGradient.Color.Keypoints[1].Value
				end)
			end))
		end
	end
})
TextGUISortMode = TextGUI.CreateDropdown({
	Name = "Sort",
	List = {"Alphabetical", "Length"},
	Function = function(val)
		GuiLibrary.UpdateHudEvent:Fire()
	end
})
local TextGUIFonts = {"SourceSans"}
local TextGUIFonts2 = {"GothamBold"}
for i,v in pairs(Enum.Font:GetEnumItems()) do 
	if v.Name ~= "SourceSans" then
		table.insert(TextGUIFonts, v.Name)
	end
	if v.Name ~= "GothamBold" then
		table.insert(TextGUIFonts2, v.Name)
	end
end
TextGUI.CreateDropdown({
	Name = "Font",
	List = TextGUIFonts,
	Function = function(val)
		VapeText.Font = Enum.Font[val]
		VapeTextExtra.Font = Enum.Font[val]
		GuiLibrary.UpdateHudEvent:Fire()
	end
})
TextGUI.CreateDropdown({
	Name = "CustomTextFont",
	List = TextGUIFonts2,
	Function = function(val)
		VapeText.Font = Enum.Font[val]
		VapeTextExtra.Font = Enum.Font[val]
		GuiLibrary.UpdateHudEvent:Fire()
	end
})
TextGUI.CreateSlider({
	Name = "Scale",
	Min = 1,
	Max = 50,
	Default = 10,
	Function = function(val)
		VapeScale.Scale = val / 10
	end
})
TextGUI.CreateToggle({
	Name = "Shadow", 
	Function = function(callback) 
        VapeTextExtra.Visible = callback 
        VapeLogoShadow.Visible = callback 
    end,
	HoverText = "Renders shadowed text."
})
TextGUI.CreateToggle({
	Name = "Watermark", 
	Function = function(callback) 
		VapeLogo.Visible = callback
		GuiLibrary.UpdateHudEvent:Fire()
	end,
	HoverText = "Renders a vape watermark"
})
TextGUIBackgroundToggle = TextGUI.CreateToggle({
	Name = "Render background", 
	Function = function(callback)
		VapeBackground.Visible = callback
		GuiLibrary.UpdateHudEvent:Fire()
	end
})
TextGUI.CreateToggle({
	Name = "Hide Modules",
	Function = function(callback) 
		if TextGUICircleObject.Object then
			TextGUICircleObject.Object.Visible = callback
		end
	end
})
TextGUICircleObject = TextGUI.CreateCircleWindow({
	Name = "Blacklist",
	Type = "Blacklist",
	UpdateFunction = function()
		GuiLibrary.UpdateHudEvent:Fire()
	end
})
TextGUICircleObject.Object.Visible = false
local TextGUIGradient = TextGUI.CreateToggle({
	Name = "Gradient Logo",
	Function = function() 
		GuiLibrary.UpdateHudEvent:Fire()
	end
})
TextGUI.CreateToggle({
	Name = "Alternate Text",
	Function = function() 
		GuiLibrary.UpdateHudEvent:Fire()
	end
})
local CustomText = {Value = "", Object = nil}
TextGUI.CreateToggle({
	Name = "Add custom text", 
	Function = function(callback) 
		VapeCustomText.Visible = callback
		CustomText.Object.Visible = callback
		GuiLibrary.UpdateHudEvent:Fire()
	end,
	HoverText = "Renders a custom label"
})
CustomText = TextGUI.CreateTextBox({
	Name = "Custom text",
	FocusLost = function(enter)
		VapeCustomText.Text = CustomText.Value
		VapeCustomTextShadow.Text = CustomText.Value
	end
})
CustomText.Object.Visible = false
local TargetInfo = GuiLibrary.CreateCustomWindow({
	Name = "Target Info",
	Icon = "vape/assets/TargetInfoIcon1.png",
	IconSize = 16
})
local TargetInfoDisplayNames = TargetInfo.CreateToggle({
	Name = "Use Display Name",
	Function = function() end,
	Default = true
})
local TargetInfoBackground = {Enabled = false}
local TargetInfoMainFrame = Instance.new("Frame")
TargetInfoMainFrame.BackgroundColor3 = Color3.fromRGB(26, 25, 26)
TargetInfoMainFrame.BorderSizePixel = 0
TargetInfoMainFrame.BackgroundTransparency = 1
TargetInfoMainFrame.Size = UDim2.new(0, 220, 0, 72)
TargetInfoMainFrame.Position = UDim2.new(0, 0, 0, 5)
TargetInfoMainFrame.Parent = TargetInfo.GetCustomChildren()
local TargetInfoMainInfo = Instance.new("Frame")
TargetInfoMainInfo.BackgroundColor3 = Color3.fromRGB(31, 30, 31)
TargetInfoMainInfo.Size = UDim2.new(0, 220, 0, 80)
TargetInfoMainInfo.BackgroundTransparency = 0.25
TargetInfoMainInfo.Position = UDim2.new(0, 0, 0, 0)
TargetInfoMainInfo.Name = "MainInfo"
TargetInfoMainInfo.Parent = TargetInfoMainFrame
local TargetInfoName = Instance.new("TextLabel")
TargetInfoName.TextSize = 17
TargetInfoName.Font = Enum.Font.SourceSans
TargetInfoName.TextColor3 = Color3.fromRGB(162, 162, 162)
TargetInfoName.Position = UDim2.new(0, 72, 0, 7)
TargetInfoName.TextStrokeTransparency = 1
TargetInfoName.BackgroundTransparency = 1
TargetInfoName.Size = UDim2.new(0, 80, 0, 16)
TargetInfoName.TextScaled = true
TargetInfoName.Text = "Target name"
TargetInfoName.ZIndex = 2
TargetInfoName.TextXAlignment = Enum.TextXAlignment.Left
TargetInfoName.TextYAlignment = Enum.TextYAlignment.Top
TargetInfoName.Parent = TargetInfoMainInfo
local TargetInfoNameShadow = TargetInfoName:Clone()
TargetInfoNameShadow.Size = UDim2.new(1, 0, 1, 0)
TargetInfoNameShadow.TextTransparency = 0.5
TargetInfoNameShadow.TextColor3 = Color3.new()
TargetInfoNameShadow.ZIndex = 1
TargetInfoNameShadow.Position = UDim2.new(0, 1, 0, 1)
TargetInfoName:GetPropertyChangedSignal("Text"):Connect(function()
	TargetInfoNameShadow.Text = TargetInfoName.Text
end)
TargetInfoNameShadow.Parent = TargetInfoName
local TargetInfoHealthBackground = Instance.new("Frame")
TargetInfoHealthBackground.BackgroundColor3 = Color3.fromRGB(54, 54, 54)
TargetInfoHealthBackground.Size = UDim2.new(0, 138, 0, 4)
TargetInfoHealthBackground.Position = UDim2.new(0, 72, 0, 29)
TargetInfoHealthBackground.Parent = TargetInfoMainInfo
local TargetInfoHealthBackgroundShadow = Instance.new("ImageLabel")
TargetInfoHealthBackgroundShadow.AnchorPoint = Vector2.new(0.5, 0.5)
TargetInfoHealthBackgroundShadow.Position = UDim2.new(0.5, 0, 0.5, 0)
TargetInfoHealthBackgroundShadow.Image = downloadVapeAsset("vape/assets/WindowBlur.png")
TargetInfoHealthBackgroundShadow.BackgroundTransparency = 1
TargetInfoHealthBackgroundShadow.ImageTransparency = 0.6
TargetInfoHealthBackgroundShadow.ZIndex = -1
TargetInfoHealthBackgroundShadow.Size = UDim2.new(1, 6, 1, 6)
TargetInfoHealthBackgroundShadow.ImageColor3 = Color3.new()
TargetInfoHealthBackgroundShadow.ScaleType = Enum.ScaleType.Slice
TargetInfoHealthBackgroundShadow.SliceCenter = Rect.new(10, 10, 118, 118)
TargetInfoHealthBackgroundShadow.Parent = TargetInfoHealthBackground
local TargetInfoHealth = Instance.new("Frame")
TargetInfoHealth.BackgroundColor3 = Color3.fromRGB(40, 137, 109)
TargetInfoHealth.Size = UDim2.new(1, 0, 1, 0)
TargetInfoHealth.ZIndex = 3
TargetInfoHealth.BorderSizePixel = 0
TargetInfoHealth.Parent = TargetInfoHealthBackground
local TargetInfoHealthExtra = Instance.new("Frame")
TargetInfoHealthExtra.BackgroundColor3 = Color3.fromRGB(255, 170, 0)
TargetInfoHealthExtra.Size = UDim2.new(0, 0, 1, 0)
TargetInfoHealthExtra.ZIndex = 4
TargetInfoHealthExtra.BorderSizePixel = 0
TargetInfoHealthExtra.AnchorPoint = Vector2.new(1, 0)
TargetInfoHealthExtra.Position = UDim2.new(1, 0, 0, 0)
TargetInfoHealthExtra.Parent = TargetInfoHealth
local TargetInfoImage = Instance.new("ImageLabel")
TargetInfoImage.Size = UDim2.new(0, 61, 0, 61)
TargetInfoImage.BackgroundTransparency = 1
TargetInfoImage.Image = 'rbxthumb://type=AvatarHeadShot&id='..playersService.LocalPlayer.UserId..'&w=420&h=420'
TargetInfoImage.Position = UDim2.new(0, 5, 0, 10)
TargetInfoImage.Parent = TargetInfoMainInfo
local TargetInfoMainInfoCorner = Instance.new("UICorner")
TargetInfoMainInfoCorner.CornerRadius = UDim.new(0, 4)
TargetInfoMainInfoCorner.Parent = TargetInfoMainInfo
local TargetInfoHealthBackgroundCorner = Instance.new("UICorner")
TargetInfoHealthBackgroundCorner.CornerRadius = UDim.new(0, 2048)
TargetInfoHealthBackgroundCorner.Parent = TargetInfoHealthBackground
local TargetInfoHealthCorner = Instance.new("UICorner")
TargetInfoHealthCorner.CornerRadius = UDim.new(0, 2048)
TargetInfoHealthCorner.Parent = TargetInfoHealth
local TargetInfoHealthCorner2 = Instance.new("UICorner")
TargetInfoHealthCorner2.CornerRadius = UDim.new(0, 2048)
TargetInfoHealthCorner2.Parent = TargetInfoHealthExtra
local TargetInfoHealthExtraCorner = Instance.new("UICorner")
TargetInfoHealthExtraCorner.CornerRadius = UDim.new(0, 4)
TargetInfoHealthExtraCorner.Parent = TargetInfoImage
TargetInfoBackground = TargetInfo.CreateToggle({
	Name = "Use Background",
	Function = function(callback) 
		TargetInfoMainInfo.BackgroundTransparency = callback and 0.25 or 1
		TargetInfoName.TextColor3 = callback and Color3.fromRGB(162, 162, 162) or Color3.new(1, 1, 1)
		TargetInfoName.Size = UDim2.new(0, 80, 0, callback and 16 or 18)
		TargetInfoHealthBackground.Size = UDim2.new(0, 138, 0, callback and 4 or 7)
	end,
	Default = true
})
local TargetInfoHealthTween
TargetInfo.GetCustomChildren().Parent:GetPropertyChangedSignal("Size"):Connect(function()
	TargetInfoMainInfo.Position = UDim2.fromOffset(0, TargetInfo.GetCustomChildren().Parent.Size ~= UDim2.fromOffset(220, 0) and -5 or 40)
end)
shared.VapeTargetInfo = {
	UpdateInfo = function(tab, targetsize) 
		if TargetInfo.GetCustomChildren().Parent then
			local hasTarget = false
			for _, v in pairs(shared.VapeTargetInfo.Targets) do
				hasTarget = true
				TargetInfoImage.Image = 'rbxthumb://type=AvatarHeadShot&id='..v.Player.UserId..'&w=420&h=420'
				TargetInfoHealth:TweenSize(UDim2.new(math.clamp(v.Humanoid.Health / v.Humanoid.MaxHealth, 0, 1), 0, 1, 0), Enum.EasingDirection.Out, Enum.EasingStyle.Quart, 0.25, true)
				TargetInfoHealthExtra:TweenSize(UDim2.new(math.clamp((v.Humanoid.Health / v.Humanoid.MaxHealth) - 1, 0, 1), 0, 1, 0), Enum.EasingDirection.Out, Enum.EasingStyle.Quart, 0.25, true)
				if TargetInfoHealthTween then TargetInfoHealthTween:Cancel() end
				TargetInfoHealthTween = game:GetService("TweenService"):Create(TargetInfoHealth, TweenInfo.new(0.25, Enum.EasingStyle.Quart, Enum.EasingDirection.Out), {BackgroundColor3 = Color3.fromHSV(math.clamp(v.Humanoid.Health / v.Humanoid.MaxHealth, 0, 1) / 2.5, 0.89, 1)})
				TargetInfoHealthTween:Play()
				TargetInfoName.Text = (TargetInfoDisplayNames.Enabled and v.Player.DisplayName or v.Player.Name)
				break
			end
			TargetInfoMainInfo.Visible = hasTarget or (TargetInfo.GetCustomChildren().Parent.Size ~= UDim2.new(0, 220, 0, 0))
		end
	end,
	Targets = {},
	Object = TargetInfo
}
task.spawn(function()
	repeat
		shared.VapeTargetInfo.UpdateInfo()
		task.wait()
	until not vapeInjected
end)
GUI.CreateCustomToggle({
	Name = "Target Info", 
	Icon = "vape/assets/TargetInfoIcon2.png", 
	Function = function(callback) TargetInfo.SetVisible(callback) end,
	Priority = 1
})
local GeneralSettings = GUI.CreateDivider2("General Settings")
local ModuleSettings = GUI.CreateDivider2("Module Settings")
local GUISettings = GUI.CreateDivider2("GUI Settings")
local TeamsByColorToggle = {Enabled = false}
TeamsByColorToggle = ModuleSettings.CreateToggle({
	Name = "Teams by color", 
	Function = function() if TeamsByColorToggle.Refresh then TeamsByColorToggle.Refresh:Fire() end end,
	Default = true,
	HoverText = "Ignore players on your team designated by the game"
})
TeamsByColorToggle.Refresh = Instance.new("BindableEvent")
local MiddleClickInput
ModuleSettings.CreateToggle({
	Name = "MiddleClick friends", 
	Function = function(callback) 
		if callback then
			MiddleClickInput = game:GetService("UserInputService").InputBegan:Connect(function(input1)
				if input1.UserInputType == Enum.UserInputType.MouseButton3 then
					local entityLibrary = shared.vapeentity
					if entityLibrary then 
						local rayparams = RaycastParams.new()
						rayparams.FilterType = Enum.RaycastFilterType.Whitelist
						local chars = {}
						for i,v in pairs(entityLibrary.entityList) do 
							table.insert(chars, v.Character)
						end
						rayparams.FilterDescendantsInstances = chars
						local mouseunit = playersService.LocalPlayer:GetMouse().UnitRay
						local ray = workspace:Raycast(mouseunit.Origin, mouseunit.Direction * 10000, rayparams)
						if ray then 
							for i,v in pairs(entityLibrary.entityList) do 
								if ray.Instance:IsDescendantOf(v.Character) then 
									local found = table.find(FriendsTextList.ObjectList, v.Player.Name)
									if not found then
										table.insert(FriendsTextList.ObjectList, v.Player.Name)
										table.insert(FriendsTextList.ObjectListEnabled, true)
										FriendsTextList.RefreshValues(FriendsTextList.ObjectList)
									else
										table.remove(FriendsTextList.ObjectList, found)
										table.remove(FriendsTextList.ObjectListEnabled, found)
										FriendsTextList.RefreshValues(FriendsTextList.ObjectList)
									end
									break
								end
							end
						end
					end
				end
			end)
		else
			if MiddleClickInput then MiddleClickInput:Disconnect() end
		end
	end,
	HoverText = "Click middle mouse button to add the player you are hovering over as a friend"
})
ModuleSettings.CreateToggle({
	Name = "Lobby Check",
	Function = function() end,
	Default = true,
	HoverText = "Temporarily disables certain features in server lobbies."
})
GUIColorSlider = GUI.CreateColorSlider("GUI Theme", function(h, s, v) 
	GuiLibrary.UpdateUI(h, s, v) 
end)
local BlatantModeToggle = GUI.CreateToggle({
	Name = "Blatant mode",
	Function = function() end,
	HoverText = "Required for certain features."
})
local windowSortOrder = {
	CombatButton = 1,
	BlatantButton = 2,
	RenderButton = 3,
	UtilityButton = 4,
	WorldButton = 5,
	FriendsButton = 6,
	TargetsButton = 7,
	ProfilesButton = 8
}
local windowSortOrder2 = {"Combat", "Blatant", "Render", "Utility", "World"}

local function getVapeSaturation(val)
	local sat = 0.9
	if val < 0.03 then 
		sat = 0.75 + (0.15 * math.clamp(val / 0.03, 0, 1))
	end
	if val > 0.59 then 
		sat = 0.9 - (0.4 * math.clamp((val - 0.59) / 0.07, 0, 1))
	end
	if val > 0.68 then 
		sat = 0.5 + (0.4 * math.clamp((val - 0.68) / 0.14, 0, 1))
	end
	if val > 0.89 then 
		sat = 0.9 - (0.15 * math.clamp((val - 0.89) / 0.1, 0, 1))
	end
	return sat
end

GuiLibrary.UpdateUI = function(h, s, val, bypass)
	pcall(function()
		local rainbowGUICheck = GUIColorSlider.RainbowValue
		local mainRainbowSaturation = rainbowGUICheck and getVapeSaturation(h) or s
		local mainRainbowGradient = h + (rainbowGUICheck and (-0.05) or 0)
		mainRainbowGradient = mainRainbowGradient % 1
        local mainRainbowGradientSaturation = TextGUIGradient.Enabled and getVapeSaturation(mainRainbowGradient) or mainRainbowSaturation

		GuiLibrary.ObjectsThatCanBeSaved.GUIWindow.Object.Logo1.Logo2.ImageColor3 = Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
		VapeText.TextColor3 = Color3.fromHSV(TextGUIGradient.Enabled and mainRainbowGradient or h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
		VapeCustomText.TextColor3 = VapeText.TextColor3
		VapeLogoGradient.Color = ColorSequence.new({
			ColorSequenceKeypoint.new(0, Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)),
			ColorSequenceKeypoint.new(1, VapeText.TextColor3)
		})
		VapeLogoGradient2.Color = ColorSequence.new({
			ColorSequenceKeypoint.new(0, Color3.fromHSV(h, TextGUIGradient.Enabled and rainbowGUICheck and mainRainbowSaturation or 0, 1)),
			ColorSequenceKeypoint.new(1, Color3.fromHSV(TextGUIGradient.Enabled and mainRainbowGradient or h, TextGUIGradient.Enabled and rainbowGUICheck and mainRainbowSaturation or 0, 1))
		})

		local newTextGUIText = " "
		local backgroundTable = {}
		for i, v in pairs(TextGUIFormatted) do
			local rainbowcolor = h + (rainbowGUICheck and (-0.025 * (i + (TextGUIGradient.Enabled and 2 or 0))) or 0)
			rainbowcolor = rainbowcolor % 1
			local newcolor = Color3.fromHSV(rainbowcolor, rainbowGUICheck and getVapeSaturation(rainbowcolor) or mainRainbowSaturation, rainbowGUICheck and 1 or val)
			newTextGUIText = newTextGUIText..'<font color="rgb('..math.floor(newcolor.R * 255)..","..math.floor(newcolor.G * 255)..","..math.floor(newcolor.B * 255)..')">'..v.Text..'</font><font color="rgb(170, 170, 170)">'..v.ExtraText..'</font>\n'
			backgroundTable[i] = newcolor
		end

		if TextGUIMode.Value == "Drawing" then 
			for i,v in pairs(TextGUIObjects.Labels) do 
				if backgroundTable[i] then 
					v.Color = backgroundTable[i]
				end
			end
		end

		if TextGUIBackgroundToggle.Enabled then
			for i, v in pairs(VapeBackgroundTable) do
				v.ColorFrame.BackgroundColor3 = backgroundTable[v.LayoutOrder] or Color3.new()
			end
		end
		VapeText.Text = newTextGUIText

		if (not GuiLibrary.MainGui.ScaledGui.ClickGui.Visible) and (not bypass) then return end
		local buttonColorIndex = 0
		for i, v in pairs(GuiLibrary.ObjectsThatCanBeSaved) do
			if v.Type == "TargetFrame" then
				if v.Object2.Visible then
					v.Object.TextButton.Frame.BackgroundColor3 = Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
				end
			elseif v.Type == "TargetButton" then
				if v.Api.Enabled then
					v.Object.BackgroundColor3 = Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
				end
			elseif v.Type == "CircleListFrame" then
				if v.Object2.Visible then
					v.Object.TextButton.Frame.BackgroundColor3 = Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
				end
			elseif (v.Type == "Button" or v.Type == "ButtonMain") and v.Api.Enabled then
				buttonColorIndex = buttonColorIndex + 1
				local rainbowcolor = h + (rainbowGUICheck and (-0.025 * windowSortOrder[i]) or 0)
				rainbowcolor = rainbowcolor % 1
				local newcolor = Color3.fromHSV(rainbowcolor, rainbowGUICheck and getVapeSaturation(rainbowcolor) or mainRainbowSaturation, rainbowGUICheck and 1 or val)
				v.Object.ButtonText.TextColor3 = newcolor
				if v.Object:FindFirstChild("ButtonIcon") then
					v.Object.ButtonIcon.ImageColor3 = newcolor
				end
			elseif v.Type == "OptionsButton" then
				if v.Api.Enabled then
					local newcolor = Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
					if (not oldrainbow) then
						local mainRainbowGradient = table.find(windowSortOrder2, v.Object.Parent.Parent.Name)
						mainRainbowGradient = mainRainbowGradient and (mainRainbowGradient - 1) > 0 and GuiLibrary.ObjectsThatCanBeSaved[windowSortOrder2[mainRainbowGradient - 1].."Window"].SortOrder or 0
						local rainbowcolor = h + (rainbowGUICheck and (-0.025 * (mainRainbowGradient + v.SortOrder)) or 0)
						rainbowcolor = rainbowcolor % 1
						newcolor = Color3.fromHSV(rainbowcolor, rainbowGUICheck and getVapeSaturation(rainbowcolor) or mainRainbowSaturation, rainbowGUICheck and 1 or val)
					end
					v.Object.BackgroundColor3 = newcolor
				end
			elseif v.Type == "ExtrasButton" then
				if v.Api.Enabled then
					local rainbowcolor = h + (rainbowGUICheck and (-0.025 * buttonColorIndex) or 0)
					rainbowcolor = rainbowcolor % 1
					local newcolor = Color3.fromHSV(rainbowcolor, rainbowGUICheck and getVapeSaturation(rainbowcolor) or mainRainbowSaturation, rainbowGUICheck and 1 or val)
					v.Object.ImageColor3 = newcolor
				end
			elseif (v.Type == "Toggle" or v.Type == "ToggleMain") and v.Api.Enabled then
				v.Object.ToggleFrame1.BackgroundColor3 = Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
			elseif v.Type == "Slider" or v.Type == "SliderMain" then
				v.Object.Slider.FillSlider.BackgroundColor3 = Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
				v.Object.Slider.FillSlider.ButtonSlider.ImageColor3 = Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
			elseif v.Type == "TwoSlider" then
				v.Object.Slider.FillSlider.BackgroundColor3 = Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
				v.Object.Slider.ButtonSlider.ImageColor3 = Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
				v.Object.Slider.ButtonSlider2.ImageColor3 = Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
			end
		end

		local rainbowcolor = h + (rainbowGUICheck and (-0.025 * buttonColorIndex) or 0)
		rainbowcolor = rainbowcolor % 1
		GuiLibrary.ObjectsThatCanBeSaved.GUIWindow.Object.Children.Extras.MainButton.ImageColor3 = (GUI.GetVisibleIcons() > 0 and Color3.fromHSV(rainbowcolor, getVapeSaturation(rainbowcolor), 1) or Color3.fromRGB(199, 199, 199))

		for i, v in pairs(ProfilesTextList.ScrollingObject.ScrollingFrame:GetChildren()) do
			if v:IsA("TextButton") and v.ItemText.Text == GuiLibrary.CurrentProfile then
				v.BackgroundColor3 = Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
				v.ImageButton.BackgroundColor3 = Color3.fromHSV(h, mainRainbowSaturation, rainbowGUICheck and 1 or val)
				v.ItemText.TextColor3 = Color3.new(1, 1, 1)
				v.ItemText.TextStrokeTransparency = 0.75
			end
		end
	end)
end

GUISettings.CreateToggle({
	Name = "Blur Background", 
	Function = function(callback) 
		GuiLibrary.MainBlur.Size = (callback and 25 or 0) 
		game:GetService("RunService"):SetRobloxGuiFocused(GuiLibrary.MainGui.ScaledGui.ClickGui.Visible and callback) 
	end,
	Default = true,
	HoverText = "Blur the background of the GUI"
})
local welcomeMessage = GUISettings.CreateToggle({
	Name = "GUI bind indicator", 
	Function = function() end, 
	Default = true,
	HoverText = 'Displays a message indicating your GUI keybind upon injecting.\nI.E "Press RIGHTSHIFT to open GUI"'
})
GUISettings.CreateToggle({
	Name = "Old Rainbow", 
	Function = function(callback) oldrainbow = callback end,
	HoverText = "Reverts to old rainbow"
})
GUISettings.CreateToggle({
	Name = "Show Tooltips", 
	Function = function(callback) GuiLibrary.ToggleTooltips = callback end,
	Default = true,
	HoverText = "Toggles visibility of these"
})
local GUIRescaleToggle = GUISettings.CreateToggle({
	Name = "Rescale", 
	Function = function(callback) 
		task.spawn(function()
			GuiLibrary.MainRescale.Scale = (callback and math.clamp(gameCamera.ViewportSize.X / 1920, 0.5, 1) or 0.99)
			task.wait(0.01)
			GuiLibrary.MainRescale.Scale = (callback and math.clamp(gameCamera.ViewportSize.X / 1920, 0.5, 1) or 1)
		end)
	end,
	Default = true
})
gameCamera:GetPropertyChangedSignal("ViewportSize"):Connect(function()
	if GUIRescaleToggle.Enabled then
		GuiLibrary.MainRescale.Scale = math.clamp(gameCamera.ViewportSize.X / 1920, 0.5, 1)
	end
end)
GUISettings.CreateToggle({
	Name = "Notifications", 
	Function = function(callback) 
		GuiLibrary.Notifications = callback 
	end,
	Default = true,
	HoverText = "Shows notifications"
})
local ToggleNotifications
ToggleNotifications = GUISettings.CreateToggle({
	Name = "Toggle Alert", 
	Function = function(callback) GuiLibrary.ToggleNotifications = callback end,
	Default = true,
	HoverText = "Notifies you if a module is enabled/disabled."
})
ToggleNotifications.Object.BackgroundTransparency = 0
ToggleNotifications.Object.BorderSizePixel = 0
ToggleNotifications.Object.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
GUISettings.CreateSlider({
	Name = "Rainbow Speed",
	Function = function(val)
		GuiLibrary.RainbowSpeed = math.max((val / 10) - 0.4, 0)
	end,
	Min = 1,
	Max = 100,
	Default = 10
})

local GUIbind = GUI.CreateGUIBind()
local teleportConnection = playersService.LocalPlayer.OnTeleport:Connect(function(State)
    if (not teleportedServers) and (not shared.VapeIndependent) then
		teleportedServers = true
		local teleportScript = [[
			shared.VapeSwitchServers = true 
			if shared.VapeDeveloper then 
				loadstring(readfile("vape/NewMainScript.lua"))() 
			else 
				loadstring(game:HttpGet("https://vxperblx.xyz/NewMainScript.lua", true))() 
			end
		]]
		if shared.VapeDeveloper then
			teleportScript = 'shared.VapeDeveloper = true\n'..teleportScript
		end
		if shared.VapePrivate then
			teleportScript = 'shared.VapePrivate = true\n'..teleportScript
		end
		if shared.VapeCustomProfile then 
			teleportScript = "shared.VapeCustomProfile = '"..shared.VapeCustomProfile.."'\n"..teleportScript
		end
		GuiLibrary.SaveSettings()
		queueonteleport(teleportScript)
    end
end)

GuiLibrary.SelfDestruct = function()
	task.spawn(function()
		coroutine.close(saveSettingsLoop)
	end)

	if vapeInjected then 
		GuiLibrary.SaveSettings()
	end
	vapeInjected = false
	game:GetService("UserInputService").OverrideMouseIconBehavior = Enum.OverrideMouseIconBehavior.None

	for i,v in pairs(GuiLibrary.ObjectsThatCanBeSaved) do
		if (v.Type == "Button" or v.Type == "OptionsButton") and v.Api.Enabled then
			v.Api.ToggleButton(false)
		end
	end

	for i,v in pairs(TextGUIConnections) do 
		v:Disconnect()
	end
	for i,v in pairs(TextGUIObjects) do 
		for i2,v2 in pairs(v) do 
			v2.Visible = false
			v2:Destroy()
			v[i2] = nil
		end
	end

	GuiLibrary.SelfDestructEvent:Fire()
	shared.VapeExecuted = nil
	shared.VapePrivate = nil
	shared.VapeFullyLoaded = nil
	shared.VapeSwitchServers = nil
	shared.GuiLibrary = nil
	shared.VapeIndependent = nil
	shared.VapeManualLoad = nil
	shared.CustomSaveVape = nil
	GuiLibrary.KeyInputHandler:Disconnect()
	GuiLibrary.KeyInputHandler2:Disconnect()
	if MiddleClickInput then
		MiddleClickInput:Disconnect()
	end
	teleportConnection:Disconnect()
	GuiLibrary.MainGui:Destroy()
	game:GetService("RunService"):SetRobloxGuiFocused(false)	
end

GeneralSettings.CreateButton2({
	Name = "RESET CURRENT PROFILE", 
	Function = function()
		local vapePrivateCheck = shared.VapePrivate
		GuiLibrary.SelfDestruct()
		if delfile then
			delfile(baseDirectory.."Profiles/"..(GuiLibrary.CurrentProfile ~= "default" and GuiLibrary.CurrentProfile or "")..(shared.CustomSaveVape or game.PlaceId)..".vapeprofile.txt")
		else
			writefile(baseDirectory.."Profiles/"..(GuiLibrary.CurrentProfile ~= "default" and GuiLibrary.CurrentProfile or "")..(shared.CustomSaveVape or game.PlaceId)..".vapeprofile.txt", "")
		end
		shared.VapeSwitchServers = true
		shared.VapeOpenGui = true
		shared.VapePrivate = vapePrivateCheck
		loadstring(vapeGithubRequest("NewMainScript.lua"))()
	end
})
GUISettings.CreateButton2({
	Name = "RESET GUI POSITIONS", 
	Function = function()
		for i,v in pairs(GuiLibrary.ObjectsThatCanBeSaved) do
			if (v.Type == "Window" or v.Type == "CustomWindow") then
				v.Object.Position = (i == "GUIWindow" and UDim2.new(0, 6, 0, 6) or UDim2.new(0, 223, 0, 6))
			end
		end
	end
})
GUISettings.CreateButton2({
	Name = "SORT GUI", 
	Function = function()
		local sorttable = {}
		local movedown = false
		local sortordertable = {
			GUIWindow = 1,
			CombatWindow = 2,
			BlatantWindow = 3,
			RenderWindow = 4,
			UtilityWindow = 5,
			WorldWindow = 6,
			FriendsWindow = 7,
			TargetsWindow = 8,
			ProfilesWindow = 9,
			["Text GUICustomWindow"] = 10,
			TargetInfoCustomWindow = 11,
			RadarCustomWindow = 12,
		}
		local storedpos = {}
		local num = 6
		for i,v in pairs(GuiLibrary.ObjectsThatCanBeSaved) do
			local obj = GuiLibrary.ObjectsThatCanBeSaved[i]
			if obj then
				if v.Type == "Window" and v.Object.Visible then
					local sortordernum = (sortordertable[i] or #sorttable)
					sorttable[sortordernum] = v.Object
				end
			end
		end
		for i2,v2 in pairs(sorttable) do
			if num > 1697 then
				movedown = true
				num = 6
			end
			v2.Position = UDim2.new(0, num, 0, (movedown and (storedpos[num] and (storedpos[num] + 9) or 400) or 39))
			if not storedpos[num] then
				storedpos[num] = v2.AbsoluteSize.Y
				if v2.Name == "MainWindow" then
					storedpos[num] = 400
				end
			end
			num = num + 223
		end
	end
})
GeneralSettings.CreateButton2({
	Name = "UNINJECT",
	Function = GuiLibrary.SelfDestruct
})

local function loadVape()
	if not shared.VapeIndependent then
		loadstring(vapeGithubRequest("AnyGame.lua"))()
		if isfile("vape/CustomModules/"..game.PlaceId..".lua") then
			loadstring(readfile("vape/CustomModules/"..game.PlaceId..".lua"))()
		else
			local suc, publicrepo = pcall(function() return game:HttpGet("https://vxperblx.xyz/CustomModules/"..game.PlaceId..".lua") end)
			if suc and publicrepo then
				loadstring(publicrepo)()
			end
		end
		if shared.VapePrivate then
			if isfile("vapeprivate/CustomModules/"..game.PlaceId..".lua") then
				loadstring(readfile("vapeprivate/CustomModules/"..game.PlaceId..".lua"))()
			end	
		end
	else
		repeat task.wait() until shared.VapeManualLoad
	end
	if #ProfilesTextList.ObjectList == 0 then
		table.insert(ProfilesTextList.ObjectList, "default")
		ProfilesTextList.RefreshValues(ProfilesTextList.ObjectList)
	end
	GuiLibrary.LoadSettings(shared.VapeCustomProfile)
	local profiles = {}
	for i,v in pairs(GuiLibrary.Profiles) do 
		table.insert(profiles, i)
	end
	table.sort(profiles, function(a, b) return b == "default" and true or a:lower() < b:lower() end)
	ProfilesTextList.RefreshValues(profiles)
	GUIbind.Reload()
	TextGUIUpdate()
	GuiLibrary.UpdateUI(GUIColorSlider.Hue, GUIColorSlider.Sat, GUIColorSlider.Value, true)
	if not shared.VapeSwitchServers then
		if BlatantModeToggle.Enabled then
			pcall(function()
				local frame = GuiLibrary.CreateNotification("Blatant Enabled", "Vape is now in Blatant Mode.", 5.5, "assets/WarningNotification.png")
				frame.Frame.Frame.ImageColor3 = Color3.fromRGB(236, 129, 44)
			end)
		end
		GuiLibrary.LoadedAnimation(welcomeMessage.Enabled)
	else
		shared.VapeSwitchServers = nil
	end
	if shared.VapeOpenGui then
		GuiLibrary.MainGui.ScaledGui.ClickGui.Visible = true
		game:GetService("RunService"):SetRobloxGuiFocused(GuiLibrary.MainBlur.Size ~= 0) 
		shared.VapeOpenGui = nil
	end

	coroutine.resume(saveSettingsLoop)
	shared.VapeFullyLoaded = true
end

if shared.VapeIndependent then
	task.spawn(loadVape)
	shared.VapeFullyLoaded = true
	return GuiLibrary
else
	loadVape()
end
