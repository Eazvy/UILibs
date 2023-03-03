--Go to line 1138

repeat wait() until game:IsLoaded()

local games = {
    [833423526] = "Strucid",
    [88070565] = "Bloxburg",
    [848145103] = "Dungeon Quest",
    [245662005] = "Jailbreak",
    [964540701] = "Sound Space",
    [1247975681] = "Big Paintball",
    [1153781324] = "Adventure Up",
    [111958650] = "Arsenal",
    [301252049] = "Robeats",
    [115797356] = "Counter Blox"
}

Game = games[game.GameId] or "Universal"

if syn then
    pcall(function()
        syn.protect_gui(game:GetService("CoreGui"))
    end)
end

    syn_websocket_send = syn_websocket_send
    firesignal = firesignal
    makefolder = makefolder
    is_protosmasher_caller = is_protosmasher_caller
    clonefunction = clonefunction
    setrawmetatable = setrawmetatable 
    getrawmetatable = getrawmetatable
    getinstancefromstate = getinstancefromstate
    setfflag = setfflag
    getcallingscript = getcallingscript or get_calling_script
    getrenv = getrenv
    syn_crypt_b64_encode = syn_crypt_b64_encode
    newcclosure = newcclosure
    getspecialinfo = debug.getspecialinfo or getspecialinfo
    shared = shared
    decompile = decompile
    loadstring = loadstring
    getprotos = debug.getprotos or getprotos
    hookfunction = hookfunction or hookfunc
    isfile = isfile
    getproto = debug.getproto or getproto
    print = print
    isrbxactive = isrbxactive
    rconsoleinfo = rconsoleinfo
    make_readonly = make_readonly
    getstack = debug.getstack or getstack
    rconsolename = rconsolename
    unlockmodulescript = unlockmodulescript
    getupvalue = debug.getupvalue or getupvalue
    setproto = debug.setproto or setproto
    mouse1click = mouse1click
    setupvalue = debug.setupvalue or setupvalue
    getscripts = getscripts or get_scripts
    rconsoleerr = rconsoleerr
    dumpstring = dumpstring
    keypress = keypress
    syn_crypt_derive = syn_crypt_derive
    rconsoleclear = rconsoleclear
    is_redirection_enabled = is_redirection_enabled
    syn_context_set = syn_context_set
    isreadonly = isreadonly or function(tbl) return is_readonly; end;
    mouse2click = mouse2click
    getinfo = debug.getinfo or getinfo
    writefile = writefile
    loadfile = loadfile
    getconstant = debug.getconstant or getconstant
    is_synapse_function = is_synapse_function or issynapsefunction
    getconnections = getconnections
    checkcaller = checkcaller
    setreadonly = setreadonly or function(tbl, val) if val then make_readonly(tbl); else make_writeable(tbl); end; end;
    syn_crypt_encrypt = syn_crypt_encrypt
    warn = warn
    validfgwindow = validfgwindow
    saveinstance = saveinstance
    getinstances = getinstances or get_instances
    getconstants = debug.getconstants or getconstants
    getloadedmodules = getloadedmodules or get_loaded_modules
    require = require
    getnilinstances = getnilinstances or get_nil_instances
    setclipboard = setclipboard
    delfile = delfile
    firetouchinterest = firetouchinterest
    mouse1release = mouse1release
    syn_websocket_close = syn_websocket_close
    setnamecallmethod = setnamecallmethod
    rconsoleprint = rconsoleprint
    getsenv = getsenv
    messagebox = messagebox
    replaceclosure = replaceclosure
    delfolder = delfolder
    keyrelease = keyrelease
    isfolder = isfolder
    XPROTECT = XPROTECT or xprotect
    getcallstack = getcallstack
    appendfile = appendfile
    syn_crypt_hash = syn_crypt_hash
    syn_websocket_connect = syn_websocket_connect
    is_protosmasher_closure = is_protosmasher_closure or isprotosmasherclosure
    mousemoverel = mousemoverel
    printconsole = printconsole
    listfiles = listfiles or list_files
    islclosure = islclosure or is_lclosure
    rconsolewarn = rconsolewarn
    getstateenv = getstateenv
    syn_crypt_decrypt = syn_crypt_decrypt
    readfile = readfile
    mousescroll = mousescroll
    mousemoveabs = mousemoverel
    setconstant = debug.setconstant or setconstant
    getpropvalue = getpropvalue
    syn_crypt_b64_decode = syn_crypt_b64_decode
    mouse2release = mouse2release
    mouse2press = mouse2press
    getgc = getgc
    getstates = getstates
    getpointerfromstate = getpointerfromstate
    mouse1press = mouse1press
    getnamecallmethod = getnamecallmethod or get_namecall_method
    setpropvalue = setpropvalue
    rconsoleinputasync = rconsoleinputasync
    syn_crypt_random = syn_crypt_random
    fireclickdetector = fireclickdetector
    rconsoleinput = rconsoleinput
    getmenv = getmenv
    getreg = getreg or debug.getregistry or getregistry
    getgenv = getgenv
    messageboxasync = messageboxasync
    getupvalues = getupvalues or debug.getupvalues or getupvalues
    setstack = setstack or debug.setstack or setstack
    syn_context_get = syn_context_get
    syn_isactive = syn_isactive
    profilebegan = debug.profilebegin or profilebegin
    traceback = debug.traceback or traceback
    setmetatable = debug.setmetatable or setmetatable
    getmetatable = debug.getmetatable or getmetatable
    getfenv = debug.getfenv or getfenv
    setupvaluename = debug.setupvaluename or setupvaluename
    profileend = debug.profileend or profileend
    validlevel = debug.validlevel or validlevel

local library = {};

if game:GetService("CoreGui"):FindFirstChild("LibraryUI") then
	game:GetService("CoreGui"):FindFirstChild("LibraryUI"):Destroy()
end

local WinRarUI = Instance.new("ScreenGui")

WinRarUI.Name = "LibraryUI"
WinRarUI.Parent = game:GetService("CoreGui")
WinRarUI.ResetOnSpawn = false

game:GetService("UserInputService").InputBegan:Connect(function(I)
	if I.KeyCode == Enum.KeyCode.RightShift then
		local LibraryUI = game:GetService("CoreGui"):FindFirstChild("LibraryUI")
		LibraryUI.Enabled = not LibraryUI.Enabled
	end
end)

function library.new(name)
	local UI = {};
	local Main = Instance.new("ImageLabel")
	local Holder = Instance.new("Frame")
	local UIGradient = Instance.new("UIGradient")
	local TabHolder = Instance.new("Frame")
	local UIListLayout = Instance.new("UIListLayout")
	local UIPadding = Instance.new("UIPadding")
	local underline = Instance.new("Frame")
	local UIGradient_2 = Instance.new("UIGradient")
	local Title = Instance.new("TextLabel")
	local UIPadding_2 = Instance.new("UIPadding")

	Main.Name = "Main"
	Main.Parent = WinRarUI
	Main.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Main.BackgroundTransparency = 1.000
	Main.Position = UDim2.new(0.106694564, 0, 0.270889491, 0)
	Main.Size = UDim2.new(0, 577, 0, 32)
	Main.Image = "rbxassetid://3570695787"
	Main.ScaleType = Enum.ScaleType.Slice
	Main.SliceCenter = Rect.new(100, 100, 100, 100)
	Main.SliceScale = 0.030

	Holder.Name = "Holder"
	Holder.Parent = Main
	Holder.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
	Holder.BackgroundTransparency = 0.080
	Holder.BorderSizePixel = 0
	Holder.Position = UDim2.new(0, 0, 1.03125, 0)
	Holder.Size = UDim2.new(0, 577, 0, 343)

	UIGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(30, 30, 30)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(26, 26, 26))}
	UIGradient.Parent = Main

	TabHolder.Name = "TabHolder"
	TabHolder.Parent = Main
	TabHolder.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
	TabHolder.BackgroundTransparency = 1.000
	TabHolder.BorderSizePixel = 0
	TabHolder.Position = UDim2.new(0.211438477, 0, -4.76837158e-07, 0)
	TabHolder.Size = UDim2.new(0, 455, 0, 32)
	TabHolder.Visible = true
	TabHolder.ZIndex = 2

	UIPadding.Parent = TabHolder
	UIPadding.PaddingLeft = UDim.new(0, 3)
	UIPadding.PaddingTop = UDim.new(0, 7)

	UIListLayout.Parent = TabHolder
	UIListLayout.FillDirection = Enum.FillDirection.Horizontal
	UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
	UIListLayout.VerticalAlignment = Enum.VerticalAlignment.Center
	UIListLayout.Padding = UDim.new(0, 5)

	underline.Name = "underline"
	underline.Parent = Main
	underline.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	underline.BorderSizePixel = 0
	underline.Position = UDim2.new(0, 0, 0.8125, 0)
	underline.Size = UDim2.new(0, 577, 0, 7)

	UIGradient_2.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(30, 30, 30)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(26, 26, 26))}
	UIGradient_2.Parent = underline

	Title.Name = "Title"
	Title.Parent = Main
	Title.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Title.BackgroundTransparency = 1.000
	Title.BorderSizePixel = 0
	Title.Size = UDim2.new(0, 122, 0, 33)
	Title.ZIndex = 8
	Title.Font = Enum.Font.SourceSansSemibold
	Title.Text = name
	Title.TextColor3 = Color3.fromRGB(252, 252, 252)
	Title.TextSize = 15.000
	Title.TextXAlignment = Enum.TextXAlignment.Left

	UIPadding_2.Parent = Title
	UIPadding_2.PaddingBottom = UDim.new(0, 1)
	UIPadding_2.PaddingLeft = UDim.new(0, 6)

	local players = game:service('Players');
    local player = players.LocalPlayer;
    local mouse = player:GetMouse();
    local run = game:service('RunService'); -- Credits to Google Chrome!
    local stepped = run.Stepped;
    draggable = function(obj)
        spawn(function()
            obj.Active = true;
            local minitial;
            local initial;
            local isdragging;
            obj.InputBegan:Connect(function(input)
                if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
                    isdragging = true;
                    minitial = input.Position;
                    initial = obj.Position;
                    local con;
                    con = stepped:Connect(function()
                        if isdragging then
                            local delta = Vector3.new(mouse.X, mouse.Y, 0) - minitial;
                            obj.Position = UDim2.new(initial.X.Scale, initial.X.Offset + delta.X, initial.Y.Scale, initial.Y.Offset + delta.Y);
                        else
                            con:Disconnect();
                        end;
                    end);
                    input.Changed:Connect(function()
                        if input.UserInputState == Enum.UserInputState.End then
                            isdragging = false;
                        end;
                    end);
                end;
            end);
        end)
	end;

	draggable(Main)

	function UI.WindowTab(name)
		local UITabs = {};
		local Window = Instance.new("TextButton")
		local Container = Instance.new("Frame")
		local SideTabs = Instance.new("Frame")
		local UIPadding = Instance.new("UIPadding")
		local UIListLayout = Instance.new("UIListLayout")

		Window.Name = name
		Window.Parent = TabHolder
		Window.BackgroundColor3 = Color3.fromRGB(22, 195, 19)
		Window.BackgroundTransparency = 0.500
		Window.BorderColor3 = Color3.fromRGB(33, 83, 30)
		Window.Position = UDim2.new(0.00659340667, 0, 0.296875, 0)
		Window.Size = UDim2.new(0, 108, 0, 20)
		Window.ZIndex = 2
		Window.AutoButtonColor = false
		Window.Font = Enum.Font.SourceSans
		Window.Text = name
		Window.TextColor3 = Color3.fromRGB(240, 240, 240)
		Window.TextSize = 14.000

		Container.Name = "Container"
		Container.Parent = Holder
		Container.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
		Container.BackgroundTransparency = 0.080
		Container.BorderSizePixel = 0
		Container.Size = UDim2.new(0, 577, 0, 343)
		Container.Visible = false

		SideTabs.Name = "SideTabs"
		SideTabs.Parent = Container
		SideTabs.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
		SideTabs.BackgroundTransparency = 0.700
		SideTabs.BorderSizePixel = 0
		SideTabs.Position = UDim2.new(0.00173310225, 0, 0, 0)
		SideTabs.Size = UDim2.new(0, 122, 0, 342)
		SideTabs.ZIndex = 2
		SideTabs.Visible = false

		UIPadding.Parent = SideTabs
		UIPadding.PaddingLeft = UDim.new(0, 6)
		UIPadding.PaddingTop = UDim.new(0, 5)

		UIListLayout.Parent = SideTabs
		UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout.Padding = UDim.new(0, 4)

		function UITabs.ShowWindow()
			Container.Visible = true
			SideTabs.Visible = true
			Window.BackgroundTransparency = .32
			Window.Size = UDim2.new(0, 108,0, 23)
			Window.TextSize = 15
		end

		local NewHolder = Holder

		Window.MouseButton1Click:Connect(function()
			for i,v in pairs(NewHolder:GetChildren()) do
				if v:IsA("Frame") then
					v.Visible = false
				end
			end
			for i,v in pairs(TabHolder:GetChildren()) do
				if v:IsA('TextButton') then
					v.BackgroundTransparency = .5
					v.Size = UDim2.new(0, 108,0, 20)
					v.TextSize = 14
				end
			end
			Container.Visible = true
			SideTabs.Visible = true
			Window.BackgroundTransparency = .32
			Window.Size = UDim2.new(0, 108,0, 23)
			Window.TextSize = 15
		end)

		function UITabs.SideTab(name)
			local SideTabUI = {};
			local TabButton = Instance.new("TextButton")
			local Frame = Instance.new("Frame")
			local Tab = Instance.new("ScrollingFrame")
			local UIListLayout = Instance.new("UIListLayout")
			local UIPadding = Instance.new("UIPadding")

			TabButton.Name = name
			TabButton.Parent = SideTabs
			TabButton.BackgroundColor3 = Color3.fromRGB(48, 48, 48)
			TabButton.BackgroundTransparency = 1.000
			TabButton.BorderColor3 = Color3.fromRGB(63, 63, 63)
			TabButton.LayoutOrder = 1
			TabButton.Position = UDim2.new(0, 0, 0.171875, 0)
			TabButton.Size = UDim2.new(0, 110, 0, 20)
			TabButton.ZIndex = 2
			TabButton.AutoButtonColor = false
			TabButton.Font = Enum.Font.SourceSans
			TabButton.Text = name
			TabButton.TextColor3 = Color3.fromRGB(240, 240, 240)
			TabButton.TextSize = 14.000

			Frame.Parent = TabButton
			Frame.BackgroundColor3 = Color3.fromRGB(49, 218, 46)
			Frame.BorderSizePixel = 0
			Frame.Size = UDim2.new(0.0350000001, 0, 0, 20)
			Frame.Visible = false

			function SideTabUI.ShowTab()
				TabButton.TextSize = 15
				TabButton.BackgroundTransparency = .5
				Frame.Visible = true
				Tab.Visible = true
			end

			Tab.Name = "Tabs"
			Tab.Parent = Container
			Tab.Active = true
			Tab.BackgroundColor3 = Color3.fromRGB(31, 35, 37)
			Tab.BackgroundTransparency = 1.000
			Tab.BorderColor3 = Color3.fromRGB(27, 42, 53)
			Tab.BorderSizePixel = 0
			Tab.Position = UDim2.new(0.216637775, 0, 0.00290708849, 0)
			Tab.Size = UDim2.new(0, 450, 0, 342)
			Tab.ZIndex = 2
			Tab.CanvasSize = UDim2.new(0,0,3,0)
			Tab.ScrollBarThickness = 5
			Tab.Visible = false

			UIListLayout.Parent = Tab
			UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
			UIListLayout.Padding = UDim.new(0, 5)

			UIPadding.Parent = Tab
			UIPadding.PaddingBottom = UDim.new(0, 2)
			UIPadding.PaddingLeft = UDim.new(0, 2)
			UIPadding.PaddingTop = UDim.new(0, 5)

			TabButton.MouseButton1Click:Connect(function()
				for i,v in pairs(Container:GetChildren()) do
					if v.Name == "Tabs" then
						v.Visible = false
					end
				end
				for i,v in pairs(SideTabs:GetChildren()) do
					if v:IsA("TextButton") then
						v.TextSize = 14
						v.BackgroundTransparency = 1
						v.Frame.Visible = false
					end
				end
				Tab.Visible = true
				TabButton.TextSize = 15
				TabButton.BackgroundTransparency = .5
				TabButton.Frame.Visible = true
			end)

			function SideTabUI.Section(name)
				local SectionUI = {};
				local Section = Instance.new("Frame")
				local SectionTitle = Instance.new("TextLabel")
				local Underline = Instance.new("ImageLabel")

				Section.Name = name
				Section.Parent = Tab
				Section.BackgroundColor3 = Color3.fromRGB(55, 55, 55)
				Section.BorderSizePixel = 0
				Section.Position = UDim2.new(0.00447427295, 0, 0.0146198831, 0)
				Section.Size = UDim2.new(0, 438, 0, 200)

				SectionTitle.Name = "SectionName"
				SectionTitle.Parent = Section
				SectionTitle.Active = true
				SectionTitle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				SectionTitle.BackgroundTransparency = 1.000
				SectionTitle.BorderSizePixel = 0
				SectionTitle.LayoutOrder = 1
				SectionTitle.Size = UDim2.new(0, 442,0, 23)
				SectionTitle.ZIndex = 3
				SectionTitle.Font = Enum.Font.SourceSans
				SectionTitle.Text = name
				SectionTitle.TextColor3 = Color3.fromRGB(198, 198, 198)
				SectionTitle.TextSize = 22.000
				SectionTitle.TextXAlignment = Enum.TextXAlignment.Left

				local UIPadding = Instance.new("UIPadding")
				UIPadding.Parent = SectionTitle
				UIPadding.PaddingBottom = UDim.new(0, 2)
				UIPadding.PaddingLeft = UDim.new(0, 5)

				Underline.Name = "Underline"
				Underline.Parent = Section
				Underline.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				Underline.BackgroundTransparency = 1.000
				Underline.LayoutOrder = 2
				Underline.Position = UDim2.new(0.00894965976, 0, 0.100877196, 0)
				Underline.Size = UDim2.new(0, 433, 0, 3)
				Underline.ZIndex = 4
				Underline.Image = "rbxassetid://3570695787"
				Underline.ImageColor3 = Color3.fromRGB(59, 59, 59)
				Underline.ScaleType = Enum.ScaleType.Slice
				Underline.SliceCenter = Rect.new(100, 100, 100, 100)
				Underline.SliceScale = 0.120

				local UIListLayout2 = Instance.new("UIListLayout")
				UIListLayout2.Parent = Section
				UIListLayout2.HorizontalAlignment = Enum.HorizontalAlignment.Center
				UIListLayout2.SortOrder = Enum.SortOrder.LayoutOrder
				UIListLayout2.Padding = UDim.new(0, 2)

				local y = 0
       		 	for i, v in pairs(Section:GetChildren()) do
            		if (not v:IsA("UIListLayout") and not v:IsA("UIPadding")) then
               			 	y = y + v.AbsoluteSize.Y + 2;
            			end
        			end
        		Section.Size = UDim2.new(0, 438, 0, y)

				function SectionUI:Resize()
        		local y = 0
       		 	for i, v in pairs(Section:GetChildren()) do
            		if (not v:IsA("UIListLayout") and not v:IsA("UIPadding")) then
               			 	y = y + v.AbsoluteSize.Y + 2;
            			end
        			end
        		Section.Size = UDim2.new(0, 438, 0, y)
    			end	

				SectionUI:Resize()

				function SectionUI.Label(name)
					local LabelHolder = Instance.new("Frame")
					local Label = Instance.new("TextLabel")

					LabelHolder.Name = "LabelHolder"
					LabelHolder.Parent = Section
					LabelHolder.BackgroundColor3 = Color3.fromRGB(44, 44, 44)
					LabelHolder.BackgroundTransparency = 1.000
					LabelHolder.BorderSizePixel = 0
					LabelHolder.LayoutOrder = 3
					LabelHolder.Position = UDim2.new(0.00570776267, 0, 0.220588237, 0)
					LabelHolder.Size = UDim2.new(0, 432, 0, 30)

					Label.Name = "Label"
					Label.Parent = LabelHolder
					Label.AnchorPoint = Vector2.new(0, 0.00999999978)
					Label.BackgroundColor3 = Color3.fromRGB(55, 55, 55)
					Label.BorderColor3 = Color3.fromRGB(58, 58, 58)
					Label.Position = UDim2.new(0.00499999989, 0, 0.0700000003, 0)
					Label.Size = UDim2.new(0.987999976, 1, 0.829999983, 1)
					Label.Font = Enum.Font.SourceSans
					Label.LineHeight = 1.1
					Label.Text = name
					Label.TextColor3 = Color3.fromRGB(194, 194, 194)
					Label.TextSize = 20.000
					SectionUI:Resize()
				end

				function SectionUI.Button(name,callback)
					local ButtonHolder = Instance.new("Frame")
					local Button = Instance.new("TextButton")
					local Circle = Instance.new("ImageLabel")

					ButtonHolder.Name = "ButtonHolder"
					ButtonHolder.Parent = Section
					ButtonHolder.BackgroundColor3 = Color3.fromRGB(44, 44, 44)
					ButtonHolder.BorderSizePixel = 0
					ButtonHolder.LayoutOrder = 3
					ButtonHolder.Position = UDim2.new(0.008, 0,0.221, 0)
					ButtonHolder.Size = UDim2.new(0, 432, 0, 30)

					Button.Name = "Button"
					Button.Parent = ButtonHolder
					Button.AnchorPoint = Vector2.new(0, 0.01)
					Button.BackgroundColor3 = Color3.fromRGB(52, 52, 52)
					Button.BorderSizePixel = 0
					Button.ClipsDescendants = true
					Button.Position = UDim2.new(0.004, 0,0.08, 0)
					Button.Size = UDim2.new(0.989, 1,0.83, 1)
					Button.AutoButtonColor = false
					Button.Text = name
					Button.Font = Enum.Font.SourceSans
					Button.TextColor3 = Color3.fromRGB(166, 166, 166)
					Button.TextSize = 20.000

					Circle.Name = "Circle"
					Circle.Parent = game:GetService("CoreGui")
					Circle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					Circle.BackgroundTransparency = 1.000
					Circle.ZIndex = 10
					Circle.Image = "http://www.roblox.com/asset/?id=33112574"
					Circle.ImageColor3 = Color3.fromRGB(126, 126, 126)
					Circle.ImageTransparency = 0.700

					function CircleClick(Button, X, Y)
						coroutine.resume(coroutine.create(function()
						local Circle = game:GetService("CoreGui"):WaitForChild("Circle"):Clone()
						Circle.Parent = Button
						local NewX = X - Circle.AbsolutePosition.X
						local NewY = Y - Circle.AbsolutePosition.Y
						Circle.Position = UDim2.new(0, NewX, 0, NewY)
									
						local Size = 0
						if Button.AbsoluteSize.X > Button.AbsoluteSize.Y then
							Size = Button.AbsoluteSize.X*1.5
						elseif Button.AbsoluteSize.X < Button.AbsoluteSize.Y then
							Size = Button.AbsoluteSize.Y*1.5
						elseif Button.AbsoluteSize.X == Button.AbsoluteSize.Y then
							Size = Button.AbsoluteSize.X*1.5
						end
									
						local Time = 0.5
						Circle:TweenSizeAndPosition(UDim2.new(0, Size, 0, Size), UDim2.new(0.5, -Size/2, 0.5, -Size/2), "Out", "Quad", Time, false, nil)
							for i=1,10 do
								Circle.ImageTransparency = Circle.ImageTransparency + 0.03
									wait(Time/10)
								end
							Circle:Destroy()
						end))
					end
							
					local Mouse = game.Players.LocalPlayer:GetMouse()
					Button.MouseButton1Click:Connect(function()
						callback()
						CircleClick(Button,Mouse.X,Mouse.Y)
					end)
					SectionUI:Resize()
				end

				function SectionUI.KeyBind(name,callback)
					local KeybindHolder = Instance.new("Frame")
					local KeyBindText = Instance.new("TextLabel")
					local UIPadding = Instance.new("UIPadding")
					local KeybindButton = Instance.new("TextButton")

					KeybindHolder.Name = "KeybindHolder"
					KeybindHolder.Parent = Section
					KeybindHolder.BackgroundColor3 = Color3.fromRGB(44, 44, 44)
					KeybindHolder.BorderSizePixel = 0
					KeybindHolder.LayoutOrder = 3
					KeybindHolder.Position = UDim2.new(0.00570776267, 0, 0.220588237, 0)
					KeybindHolder.Size = UDim2.new(0, 432, 0, 30)

					KeyBindText.Name = "KeyBindText"
					KeyBindText.Parent = KeybindHolder
					KeyBindText.Active = true
					KeyBindText.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					KeyBindText.BackgroundTransparency = 1.000
					KeyBindText.BorderSizePixel = 0
					KeyBindText.Size = UDim2.new(0, 431, 0, 30)
					KeyBindText.Font = Enum.Font.SourceSans
					KeyBindText.Text = name
					KeyBindText.TextColor3 = Color3.fromRGB(198, 198, 198)
					KeyBindText.TextSize = 18.000
					KeyBindText.TextXAlignment = Enum.TextXAlignment.Left

					UIPadding.Parent = KeyBindText
					UIPadding.PaddingBottom = UDim.new(0, 3)
					UIPadding.PaddingLeft = UDim.new(0, 5)

					KeybindButton.Name = "KeybindButton"
					KeybindButton.Parent = KeybindHolder
					KeybindButton.BackgroundColor3 = Color3.fromRGB(52, 52, 52)
					KeybindButton.BorderSizePixel = 0
					KeybindButton.Position = UDim2.new(0.810000002, 0, 0.100000001, 0)
					KeybindButton.Size = UDim2.new(0, 79, 0, 24)
					KeybindButton.AutoButtonColor = false
					KeybindButton.Font = Enum.Font.SourceSans
					KeybindButton.Text = ""
					KeybindButton.TextColor3 = Color3.fromRGB(166, 166, 166)
					KeybindButton.TextSize = 15.000

					local userInputService = game:GetService("UserInputService")
					local waitingForKeyPress, currentKey
					KeybindButton.Text = "Set Bind"
						
					KeybindButton.MouseButton1Click:Connect(function()
						KeybindButton.Text = "..."
						waitingForKeyPress = true
					end)
						
					local Blacklisted = {
						[Enum.KeyCode.Space] = "Space";
						[Enum.KeyCode.RightShift] = "RightShift";
						[Enum.KeyCode.F1] = "F1";
						[Enum.KeyCode.F2] = "F2";
						[Enum.KeyCode.F3] = "F3";
						[Enum.KeyCode.F4] = "F4";
						[Enum.KeyCode.F5] = "F5";
						[Enum.KeyCode.F6] = "F6";
						[Enum.KeyCode.F7] = "F7";
						[Enum.KeyCode.F8] = "F8";
						[Enum.KeyCode.F9] = "F9";
						[Enum.KeyCode.F10] = "F10";
						[Enum.KeyCode.F11] = "F11";
						[Enum.KeyCode.F12] = "F12";
						[Enum.KeyCode.Escape] = "Escape";
						[Enum.KeyCode.CapsLock] = "CapsLock";
						[Enum.KeyCode.Print] = "Print";
						[Enum.KeyCode.Tab] = "Tab";
						[Enum.KeyCode.NumLock] = "NumLock";
						[Enum.KeyCode.PageDown] = "PageDown";
						[Enum.KeyCode.PageUp] = "PageUp";
						[Enum.KeyCode.Home] = "Home";
						[Enum.KeyCode.End] = "End";
						[Enum.KeyCode.Delete] = "Delete";
						[Enum.KeyCode.Insert] = "Insert";
						[Enum.KeyCode.Backquote] = "Backquote";
						[Enum.KeyCode.Pause] = "Pause";
						[Enum.KeyCode.ScrollLock] = "ScrollLock";
						[Enum.KeyCode.Up] = "Up";
						[Enum.KeyCode.Right] = "Right";
						[Enum.KeyCode.Left] = "Left";
						[Enum.KeyCode.Down] = "Down";
						[Enum.KeyCode.W] = "W";
						[Enum.KeyCode.A] = "A";
						[Enum.KeyCode.S] = "S";
						[Enum.KeyCode.D] = "D";
					}
						
					userInputService.InputBegan:Connect(function(Input)
						local keyName = string.split(tostring(Input.KeyCode), ".")[3]
						local BlacklistedKeys = Blacklisted[Input.KeyCode]
						if waitingForKeyPress and keyName ~= "Unknown" and keyName ~= BlacklistedKeys then
						   	KeybindButton.Text = keyName
						    currentKey = Input.KeyCode
						    waitingForKeyPress = false
						end
						if not waitingForKeyPress and currentKey and Input.KeyCode == currentKey then
							callback()
						end
					end)
					SectionUI:Resize()
				end

				function SectionUI.Toggle(name,callback)
					local ToggleHolder = Instance.new("Frame")
					local ToggleText = Instance.new("TextLabel")
					local UIPadding = Instance.new("UIPadding")
					local ToggleButton = Instance.new("TextButton")

					ToggleHolder.Name = "ToggleHolder"
					ToggleHolder.Parent = Section
					ToggleHolder.BackgroundColor3 = Color3.fromRGB(44, 44, 44)
					ToggleHolder.BorderSizePixel = 0
					ToggleHolder.LayoutOrder = 3
					ToggleHolder.Position = UDim2.new(0.00570776267, 0, 0.220588237, 0)
					ToggleHolder.Size = UDim2.new(0, 432, 0, 30)

					ToggleText.Name = "ToggleText"
					ToggleText.Parent = ToggleHolder
					ToggleText.Active = true
					ToggleText.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					ToggleText.BackgroundTransparency = 1.000
					ToggleText.BorderSizePixel = 0
					ToggleText.Size = UDim2.new(0, 431, 0, 30)
					ToggleText.Font = Enum.Font.SourceSans
					ToggleText.Text = name
					ToggleText.TextColor3 = Color3.fromRGB(198, 198, 198)
					ToggleText.TextSize = 18.000
					ToggleText.TextXAlignment = Enum.TextXAlignment.Left

					UIPadding.Parent = ToggleText
					UIPadding.PaddingBottom = UDim.new(0, 3)
					UIPadding.PaddingLeft = UDim.new(0, 5)

					ToggleButton.Name = "ToggleButton"
					ToggleButton.Parent = ToggleHolder
					ToggleButton.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
					ToggleButton.BorderColor3 = Color3.fromRGB(40, 40, 40)
					ToggleButton.Position = UDim2.new(0.935000002, 0, 0.100000001, 0)
					ToggleButton.Size = UDim2.new(0, 24, 0, 24)
					ToggleButton.AutoButtonColor = false
					ToggleButton.Font = Enum.Font.SourceSans
					ToggleButton.Text = "X"
					ToggleButton.TextColor3 = Color3.fromRGB(197, 197, 197)
					ToggleButton.TextSize = 25.000
					ToggleButton.TextTransparency = 1.000

					local Toggled = false;
						
					local tweenInfo = TweenInfo.new(.15,Enum.EasingStyle.Linear,Enum.EasingDirection.InOut,0,false,0)
						
					ToggleButton.MouseButton1Click:Connect(function()
						Toggled = not Toggled
						callback(Toggled)
						local Transparency = Toggled and 0 or 1
						game:GetService("TweenService"):Create(ToggleButton,tweenInfo,{TextTransparency = Transparency}):Play()
					end)
					SectionUI:Resize()
				end

				function SectionUI.Slider(name,min,max,default,callback)
					local SliderHolder = Instance.new("Frame")
					local Slider = Instance.new("TextButton")
					local Fill = Instance.new("Frame")
					local UIGradient = Instance.new("UIGradient")
					local ValueSlider = Instance.new("TextLabel")
					local UIPadding = Instance.new("UIPadding")
					local SliderText = Instance.new("TextLabel")
					local UIPadding_2 = Instance.new("UIPadding")
					local SetSlider = Instance.new("TextBox")

					SliderHolder.Name = "SliderHolder"
					SliderHolder.Parent = Section
					SliderHolder.BackgroundColor3 = Color3.fromRGB(44, 44, 44)
					SliderHolder.BorderSizePixel = 0
					SliderHolder.LayoutOrder = 3
					SliderHolder.Position = UDim2.new(0.00570776267, 0, 0.455882341, 0)
					SliderHolder.Size = UDim2.new(0, 432, 0, 40)

					Slider.Name = "Slider"
					Slider.Parent = SliderHolder
					Slider.BackgroundColor3 = Color3.fromRGB(79, 79, 79)
					Slider.BorderSizePixel = 0
					Slider.Position = UDim2.new(0.0189999994, 0, 0.680000007, 0)
					Slider.Size = UDim2.new(0, 415, 0, 4)
					Slider.AutoButtonColor = false
					Slider.Font = Enum.Font.SourceSans
					Slider.Text = ""
					Slider.TextColor3 = Color3.fromRGB(0, 0, 0)
					Slider.TextSize = 14.000

					Fill.Name = "Fill"
					Fill.Parent = Slider
					Fill.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					Fill.BorderSizePixel = 0
					Fill.LayoutOrder = 3
					Fill.Size = UDim2.new(0, 0, 0, 4)

					UIGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(32, 157, 53)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(80, 162, 44))}
					UIGradient.Parent = Fill

					ValueSlider.Name = "ValueSlider"
					ValueSlider.Parent = Slider
					ValueSlider.Active = true
					ValueSlider.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					ValueSlider.BackgroundTransparency = 1.000
					ValueSlider.BorderSizePixel = 0
					ValueSlider.Position = UDim2.new(-0.0186192524, 0, -6.80000305, 0)
					ValueSlider.Size = UDim2.new(0, 431, 0, 22)
					ValueSlider.Font = Enum.Font.SourceSans
					ValueSlider.Text = "Minimum/Maximum"
					ValueSlider.TextColor3 = Color3.fromRGB(198, 198, 198)
					ValueSlider.TextSize = 14.000

					UIPadding.Parent = ValueSlider
					UIPadding.PaddingBottom = UDim.new(0, 4)

					SliderText.Name = "SliderText"
					SliderText.Parent = SliderHolder
					SliderText.Active = true
					SliderText.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					SliderText.BackgroundTransparency = 1.000
					SliderText.BorderSizePixel = 0
					SliderText.Position = UDim2.new(0.018999977, 0, 0, 0)
					SliderText.Size = UDim2.new(0, 415, 0, 22)
					SliderText.Font = Enum.Font.SourceSans
					SliderText.Text = name
					SliderText.TextColor3 = Color3.fromRGB(198, 198, 198)
					SliderText.TextSize = 16.000
					SliderText.TextXAlignment = Enum.TextXAlignment.Left

					UIPadding_2.Parent = SliderText
					UIPadding_2.PaddingBottom = UDim.new(0, 2)

					SetSlider.Name = "SetSlider"
					SetSlider.Parent = SliderHolder
					SetSlider.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
					SetSlider.BackgroundTransparency = 1.000
					SetSlider.BorderColor3 = Color3.fromRGB(58, 58, 58)
					SetSlider.Position = UDim2.new(0.858524144, 0, 0.0500000007, 0)
					SetSlider.Size = UDim2.new(0, 51, 0, 16)
					SetSlider.Font = Enum.Font.SourceSans
					SetSlider.PlaceholderColor3 = Color3.fromRGB(178, 178, 178)
					SetSlider.PlaceholderText = "Slider Int"
					SetSlider.Text = ""
					SetSlider.TextColor3 = Color3.fromRGB(178, 178, 178)
					SetSlider.TextSize = 14.000
					SetSlider.TextXAlignment = Enum.TextXAlignment.Right

					local Connection;
					local RunService = game:GetService("RunService");
					local UIS = game:GetService("UserInputService");
						
					local tweenInfo = TweenInfo.new(.05,Enum.EasingStyle.Linear,Enum.EasingDirection.InOut,0,false,0)
						
					local function Fade(Object,Number)
						game:GetService("TweenService"):Create(Object,tweenInfo,{TextTransparency = tonumber(Number)}):Play()
					end
						
					UIS.InputEnded:Connect(function(Input)
						if Input.UserInputType == Enum.UserInputType.MouseButton1 then
							if (Connection) then
								Connection:Disconnect();
								Connection = nil;
								Fade(ValueSlider,1)
							end;
						end;
					end);
						
					local Vals = {
						["Minimum"] = min,
						["Maximum"] = max
					}
						
					ValueSlider.Text = Vals.Minimum .. "/" .. Vals.Maximum
						
					Slider.MouseButton1Down:Connect(function()
						if (Connection) then
							Connection:Disconnect();
						end;
							
						Connection = RunService.Stepped:Connect(function()
							local Mouse = UIS:GetMouseLocation();
							local Percentage = math.clamp((Mouse.X - Slider.AbsolutePosition.X)/(Slider.AbsoluteSize.X),0,1)
							local ValueToNumber = Vals.Minimum + (Vals.Maximum - Vals.Minimum)*Percentage
							
							ValueToNumber = math.floor(ValueToNumber)
							
							ValueSlider.Text = ValueToNumber .. "/" .. Vals.Maximum
							
							game:GetService("TweenService"):Create(Fill,tweenInfo,{Size = UDim2.new(Percentage,0,0,4)}):Play()
							Fade(ValueSlider,0)
							callback(tonumber(ValueToNumber))
							SetSlider.Text = ValueToNumber
						end);
					end);
					
					local function SetValue(value)
						local percent = 1 - ((Vals.Maximum - value)/(Vals.Maximum - Vals.Minimum))
						local Number = value
						
						Number = math.floor(Number)
					
						game:GetService("TweenService"):Create(Fill,tweenInfo,{Size = UDim2.new(percent,0,0,4)}):Play()
						ValueSlider.Text = Number .. "/" .. Vals.Maximum
					end

					SetValue(default or Vals.Minimum)
					
					SetSlider.Changed:Connect(function()
						pcall(function()
							local Value = tonumber(SetSlider.Text)
							if Value >= Vals.Minimum and Value <= Vals.Maximum then
									SetValue(tonumber(SetSlider.Text))
									callback(tonumber(SetSlider.Text))
								end
							end)
						end)
					
					SetSlider.FocusLost:Connect(function()
						SetSlider.Text = tonumber(SetSlider.Text)
					end)
					SectionUI:Resize()
				end
				function SectionUI.Dropdown(name,list,callback)
					local DropFrame = Instance.new("Frame")
					local Dropdown = Instance.new("Frame")
					local DropdownText = Instance.new("TextLabel")
					local UIPadding = Instance.new("UIPadding")
					local ToggleButton = Instance.new("ImageButton")
					local DropdownObjects = Instance.new("Frame")
					local UIPadding_2 = Instance.new("UIPadding")
					local UIListLayout = Instance.new("UIListLayout")

					DropFrame.Name = "DropFrame"
					DropFrame.Parent = Section
					DropFrame.BackgroundColor3 = Color3.fromRGB(44, 44, 44)
					DropFrame.BorderSizePixel = 0
					DropFrame.LayoutOrder = 3
					DropFrame.Position = UDim2.new(0.00570776267, 0, 0.519999981, 0)
					DropFrame.Size = UDim2.new(0, 432, 0, 30)
					DropFrame.ZIndex = 6

					Dropdown.Name = "Dropdown"
					Dropdown.Parent = DropFrame
					Dropdown.BackgroundColor3 = Color3.fromRGB(44, 44, 44)
					Dropdown.BackgroundTransparency = 0.200
					Dropdown.BorderSizePixel = 0
					Dropdown.LayoutOrder = 3
					Dropdown.Position = UDim2.new(0.00111346773, 0, 0, 0)
					Dropdown.Size = UDim2.new(0, 432, 0, 30)
					Dropdown.ZIndex = 6

					DropdownText.Name = "DropdownText"
					DropdownText.Parent = Dropdown
					DropdownText.Active = true
					DropdownText.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					DropdownText.BackgroundTransparency = 1.000
					DropdownText.BorderSizePixel = 0
					DropdownText.Position = UDim2.new(0.00337645644, 0, 0, 0)
					DropdownText.Size = UDim2.new(0, 431, 0, 30)
					DropdownText.ZIndex = 6
					DropdownText.Font = Enum.Font.SourceSans
					DropdownText.Text = name
					DropdownText.TextColor3 = Color3.fromRGB(198, 198, 198)
					DropdownText.TextSize = 18.000
					DropdownText.TextXAlignment = Enum.TextXAlignment.Left

					UIPadding.Parent = DropdownText
					UIPadding.PaddingBottom = UDim.new(0, 3)
					UIPadding.PaddingLeft = UDim.new(0, 5)

					ToggleButton.Name = "ToggleButton"
					ToggleButton.Parent = Dropdown
					ToggleButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					ToggleButton.BackgroundTransparency = 1.000
					ToggleButton.BorderSizePixel = 0
					ToggleButton.Position = UDim2.new(0.944999993, 0, 0.219999999, 0)
					ToggleButton.Rotation = 90.000
					ToggleButton.Size = UDim2.new(0, 15, 0, 15)
					ToggleButton.ZIndex = 6
					ToggleButton.Image = "http://www.roblox.com/asset/?id=4888315295"
					ToggleButton.ImageColor3 = Color3.fromRGB(80, 80, 80)
					ToggleButton.SliceCenter = Rect.new(100, 100, 100, 100)

					DropdownObjects.Name = "DropdownObjects"
					DropdownObjects.BackgroundTransparency = 1
					DropdownObjects.Parent = Dropdown
					DropdownObjects.BackgroundColor3 = Color3.fromRGB(47, 47, 47)
					DropdownObjects.BorderSizePixel = 0
					DropdownObjects.ClipsDescendants = true
					DropdownObjects.Position = UDim2.new(-0.002, 0,0, 0)
					DropdownObjects.Size = UDim2.new(0, 432, 0, 30)
					DropdownObjects.ZIndex = 5

					UIPadding_2.Parent = DropdownObjects
					UIPadding_2.PaddingTop = UDim.new(0, 32)

					UIListLayout.Parent = DropdownObjects
					UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
					UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
					UIListLayout.Padding = UDim.new(0, 1)

					local Toggled = false

					local tweenInfo = TweenInfo.new(.15,Enum.EasingStyle.Linear,Enum.EasingDirection.InOut,0,false,0)
						
					DropdownText.Text = name
					for _,v in pairs(list) do
						local Button = Instance.new("TextButton")
						Button.Name = "Button"
						Button.Parent = DropdownObjects
						Button.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
						Button.BorderColor3 = Color3.fromRGB(44, 44, 44)
						Button.BorderSizePixel = 2
						Button.Text = v
						Button.ZIndex = 5
						Button.Position = UDim2.new(0.269, 0, 1, 0)
						Button.Size = UDim2.new(0, 430, 0, 30)
						Button.AutoButtonColor = false
						Button.Font = Enum.Font.SourceSans
						Button.TextColor3 = Color3.fromRGB(148, 148, 148)
						Button.TextSize = 20.000
								
						Button.MouseButton1Click:Connect(function()
							callback(Button.Text)
							DropdownText.Text = v
							Toggled = false
							DropdownObjects:TweenSize(UDim2.new(0, 432,0, 30),"In","Linear",.25,true)
							game:GetService("TweenService"):Create(ToggleButton,tweenInfo,{Rotation = 90}):Play()
						end)
					end
						
					ToggleButton.MouseButton1Click:Connect(function()
						Toggled = not Toggled
						local TotalY = 0;
						for i,v in next, DropdownObjects:GetChildren() do
							if (v:IsA("TextButton")) then
								TotalY = TotalY + v.AbsoluteSize.Y + 2;
							end
						end
							
						local RotationAmount = Toggled and 0 or 90
						local ToggleDirection = Toggled and "Out" or "In"
						local GetSize = Toggled and UDim2.new(0,432,0,TotalY + 50) or UDim2.new(0, 432,0, 30)
						DropdownObjects:TweenSize(GetSize,ToggleDirection,"Linear",.25,true)
						game:GetService("TweenService"):Create(ToggleButton,tweenInfo,{Rotation = RotationAmount}):Play()
					end)
					SectionUI:Resize()
				end

				function SectionUI.Box(name,callback)
					local BoxHolder = Instance.new("Frame")
					local BoxHolder_2 = Instance.new("TextLabel")
					local UIPadding = Instance.new("UIPadding")
					local Box = Instance.new("TextBox")
					local UIPadding_2 = Instance.new("UIPadding")

					BoxHolder.Name = "BoxHolder"
					BoxHolder.Parent = Section
					BoxHolder.BackgroundColor3 = Color3.fromRGB(44, 44, 44)
					BoxHolder.BorderSizePixel = 0
					BoxHolder.LayoutOrder = 3
					BoxHolder.Position = UDim2.new(0.00228310493, 0, 1, 0)
					BoxHolder.Size = UDim2.new(0, 431, 0, 30)

					BoxHolder_2.Name = "BoxHolder"
					BoxHolder_2.Parent = BoxHolder
					BoxHolder_2.Active = true
					BoxHolder_2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
					BoxHolder_2.BackgroundTransparency = 1.000
					BoxHolder_2.BorderSizePixel = 0
					BoxHolder_2.Size = UDim2.new(0, 428, 0, 30)
					BoxHolder_2.Font = Enum.Font.SourceSans
					BoxHolder_2.Text = name
					BoxHolder_2.TextColor3 = Color3.fromRGB(198, 198, 198)
					BoxHolder_2.TextSize = 18.000
					BoxHolder_2.TextXAlignment = Enum.TextXAlignment.Left

					UIPadding.Parent = BoxHolder_2
					UIPadding.PaddingBottom = UDim.new(0, 3)
					UIPadding.PaddingLeft = UDim.new(0, 5)

					Box.Name = "Box"
					Box.Parent = BoxHolder
					Box.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
					Box.BorderColor3 = Color3.fromRGB(52, 52, 52)
					Box.Position = UDim2.new(0.770, 0,0.135, 0)
					Box.Size = UDim2.new(0, 95, 0, 22)
					Box.Font = Enum.Font.SourceSans
					Box.PlaceholderText = "Value"
					Box.Text = ""
					Box.TextColor3 = Color3.fromRGB(0, 0, 0)
					Box.TextSize = 14.000
					Box.TextXAlignment = Enum.TextXAlignment.Left
					Box.ClipsDescendants = true

					UIPadding_2.Parent = Box
					UIPadding_2.PaddingBottom = UDim.new(0, 1)
					UIPadding_2.PaddingLeft = UDim.new(0, 3)

					Box.FocusLost:Connect(function(Enter)
						if Enter then
							if Box.Text ~= nil or Box.Text ~= "" then
								callback(Box.Text)
							end
						end
					end)

					SectionUI:Resize()
				end				
				return SectionUI
			end
			return SideTabUI
		end
		return UITabs
	end
	return UI
end

function universal(lib)
    
    uni = lib
    
    
    local Example = uni.WindowTab('Example Window')
    
    local Exampletab = Example.SideTab("Example Tab")
    
    local ExampleSection = Exampletab.Section("ExampleSection")

    
    ExampleSection.Toggle("Toggle", function(a)
        accAimbot = a
    end)
    
   ExampleSection.Toggle("Toggle", function(a)
        triggerBot = a
   end)

    ExampleSection.Slider("Slider",1,10,2,function(a)
	    smooth = a
    end)
    
    ExampleSection.Dropdown("DropDown", {"Select", "Select2"}, function(a)
        targetPrt = a
    end)
    
    ExampleSection.Toggle("Toggle", function(a)
        FFA = a
    end)
    
end


    local Main = library.new("Example")
    universal(Main)
