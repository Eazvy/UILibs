-- credits due: bracket lib - keybind & tooltip function, cripware - slider math, xaxaxaxaxaxaxaxaxa making the ui

local library, patches = {
    version = "1.0",
    configuration = {
        frames = {
            MainBackFrameColor = Color3.fromRGB(138, 138, 138), -- the very back border's color
            BorderColor = Color3.fromRGB(50, 50, 50), -- the outline border color of every element (element = toggle, textbox, etc)
            InlineBorderColor = Color3.fromRGB(10, 10, 10), -- the inline border color of every frame in the ui
        },
        
        elements = {
            BorderColor = Color3.fromRGB(50, 50, 50), -- the outline border color of every element (element = toggle, textbox, etc)
            InlineBorderColor = Color3.fromRGB(10, 10, 10), -- the inline border color of every element (element = toggle, textbox, etc)
        },
    
        text = {
            Color = Color3.fromRGB(255, 255, 255), -- the color of the everything in the ui that has the TextColor3 property
            Font = "Code", -- the font of everything in the ui that has the Font property
        },
    
        miscellaneous = {
            BackgroundGlowColor = Color3.fromRGB(255, 255, 255), -- the color of the back ground glow of the ui 
            TabHighlightColor = Color3.fromRGB(30, 30, 30), -- The BackGroundColor3 of tab and sub-tabs/sections when you click them
            
            DisplayFpsAndPing = true, -- displays your fps and ping in the top right corner of the ui 
            UIToggleKey = Enum.KeyCode.RightAlt, -- the key to toggle the ui's Visible property on/true and off/false
        },
    },
}, {};

if library.version ~= "1.0" then 
    setclipboard("https://pastebin.com/raw/yWynU0Wq")
    return messagebox("You are using an outdated version of the ciazware ui library, the github repository for the ui library has been copied to your clipboard", "ciazware ui library", 0)
end

local configuration = library.configuration;

local frames = configuration.frames;
local FrameBorderColor, FrameInlineBorderColor, MainBackFrameColor = frames.BorderColor, frames.InlineBorderColor, frames.MainBackFrameColor;

local elements = configuration.elements;
local ElementBorderColor, ElementsInlineBorderColor = elements.BorderColor, elements.InlineBorderColor;

local text = configuration.text;
local TextColor, TextFont = text.Color, text.Font;

local miscellaneous = configuration.miscellaneous;
local BackgroundGlowColor, TabHighlightColor, DisplayFpsAndPing, UIToggleKey = miscellaneous.BackgroundGlowColor, miscellaneous.TabHighlightColor, miscellaneous.DisplayFpsAndPing, miscellaneous.UIToggleKey;

-- init 
local IsLoaded, Loaded, GetService = game.IsLoaded, game.Loaded, game.GetService;
if not IsLoaded(game) then 
    Loaded.Wait(Loaded)
end

local assert = function(case)
    if not case then 
        return error(debug.traceback());
    end
end

local Service = setmetatable({}, {
    __index = function(self, Index)
        assert((Index or GetService(game, Index)));
        
        return GetService(game, Index)
    end
}); local workspace, TweenService, TextService, UserInputService, RunService = Service.Workspace, Service.TweenService, Service.TextService, Service.UserInputService, Service.RunService;

local lower, upper = string.lower, string.upper;
local find, len, format, split = string.find, string.len, string.format, string.split;
local resume, create = coroutine.resume, coroutine.create;

local Vector3, Vector2, Rect = Vector3.new, Vector2.new, Rect.new;
local NewInstance, Color3FromRGB, UDim2, UDim = Instance.new, Color3.fromRGB, UDim2.new, UDim.new;

local Connect, Camera, Mouse = Loaded.Connect, workspace.CurrentCamera, Service.Players.LocalPlayer.GetMouse(Service.Players.LocalPlayer);
local GetDescendants, GetChildren, IsA = game.GetDescendants, game.GetChildren, game.IsA;

local PropertiesTable = {["TextButton"] = "BackgroundColor3", ["Frame"] = "BackgroundTransparency", ["UIStroke"] = "Transparency"}; --{["Frame"] = "BackgroundTransparency", ["TextLabel"] = "TextTransparency", ["UIStroke"] = "Transparency"};
local BlacklistedKeyNames = {"W", "A", "S", "D", "Slash", "Tab", "Backspace", "Escape", "Space", "Delete", "Unknown", "Backquote"};

local protect_gui = function(Gui, Parent)
    if syn then
        syn.protect_gui(Gui)
        Gui.Parent = Parent
    elseif gethui then
        Gui.Parent = gethui()
    else
        Gui.Parent = Parent
    end
end -- thanks regularid

-- script functions
function patches.FixTextSize(Object, FixSize)
    assert((Object or typeof(Object) == "Instance"));
    assert((FixSize or type(FixSize) == "number"));
    
    local TextSize = TextService.GetTextSize(TextService, 
        Object.Text, Object.TextSize, Object.Font, Vector2(Camera.ViewportSize.X, Object.AbsoluteSize.Y)
    ).X

    Object.Size = UDim2(0, TextSize + FixSize, 0, Object.Size.Y.Offset)
end

function patches.FadeObject(Object, Speed, Value, Custom)
    assert((Object or typeof(Object) == "Instance"));
    assert((Speed or type(Speed) == "number"));
    assert((Value));
    
    local Property = ((Custom == false and PropertiesTable[Object.ClassName]) or (Custom == true and "BackgroundColor3"))
    
    local TweenServiceInfo = TweenService.Create(TweenService, Object, TweenInfo.new(Speed, Enum.EasingStyle.Sine, Enum.EasingDirection.Out), {
        [Property] = Value,
    }); TweenServiceInfo.Play(TweenServiceInfo);
end


function library.new(Name)
    assert((Name or type(Name) == "string"));
    
    local IsToolTipActive = false 
    local ActiveToolTip, ActiveTab, MenuOpen = nil, nil, true
    
    local function UpdateToolTipPosition() 
        if IsToolTipActive == true and ActiveToolTip ~= nil then 
            ActiveToolTip.Position = UDim2(0, UserInputService.GetMouseLocation(UserInputService).X - ActiveToolTip.AbsoluteSize.Y - ActiveToolTip.AbsoluteSize.X, 0, UserInputService.GetMouseLocation(UserInputService).Y - 10)
        end
    end
    
    local ScreenGui = NewInstance("ScreenGui")    
    ScreenGui.ZIndexBehavior = "Global"
    protect_gui(ScreenGui, game.GetService(game, "CoreGui"))

    local BackFrame = NewInstance("Frame")
    BackFrame.Name = "BackFrame"
    BackFrame.BackgroundColor3 = Color3FromRGB(20, 20, 20)
    BackFrame.BorderColor3 = Color3FromRGB(20, 20, 20)
    BackFrame.BorderSizePixel = 2
    BackFrame.Position = UDim2(0.0981308445, 0, 0.0834355801, 0)
    BackFrame.Size = UDim2(0, 550, 0, 600)
    BackFrame.Draggable = true 
    BackFrame.Selectable = true 
    BackFrame.Active = true
    BackFrame.Parent = ScreenGui
    
    local BackFrame_UIStroke = NewInstance("UIStroke")
    BackFrame_UIStroke.Name = "BackFrame_UIStroke"
    BackFrame_UIStroke.ApplyStrokeMode = "Border"
    BackFrame_UIStroke.Color = MainBackFrameColor
    BackFrame_UIStroke.LineJoinMode = "Miter"
    BackFrame_UIStroke.Thickness = 1 
    BackFrame_UIStroke.Transparency = 0 
    BackFrame_UIStroke.Enabled = true 
    BackFrame_UIStroke.Parent = BackFrame
    
    local MainFrame = NewInstance("Frame")
    MainFrame.Name = "MainFrame"
    MainFrame.BackgroundColor3 = Color3FromRGB(20, 20, 20)
    MainFrame.BorderColor3 = FrameBorderColor
    MainFrame.BorderSizePixel = 2
    MainFrame.Position = UDim2(0.0199490078, 0, 0.0434355661, 0)
    MainFrame.Size = UDim2(0, 528, 0, 564)
    MainFrame.Parent = BackFrame
    
    local MainFrame_UIStroke = NewInstance("UIStroke")
    MainFrame_UIStroke.Name = "MainFrame_UIStroke"
    MainFrame_UIStroke.ApplyStrokeMode = "Border"
    MainFrame_UIStroke.Color = FrameInlineBorderColor
    MainFrame_UIStroke.LineJoinMode = "Miter"
    MainFrame_UIStroke.Thickness = 1 
    MainFrame_UIStroke.Transparency = 0 
    MainFrame_UIStroke.Enabled = true 
    MainFrame_UIStroke.Parent = MainFrame
    
    local SectionsFrame = NewInstance("Frame")
    SectionsFrame.Name = "SectionsFrame"
    SectionsFrame.BackgroundColor3 = Color3FromRGB(255, 255, 255)
    SectionsFrame.BackgroundTransparency = 1.000
    SectionsFrame.Position = UDim2(0.024999965, 0, 0.0514184386, 35)
    SectionsFrame.Size = UDim2(0, 504, 0, 488)
    SectionsFrame.Parent = MainFrame
    
    local TabsHolderFrame = NewInstance("Frame")
    TabsHolderFrame.Name = "TabsHolderFrame"
    TabsHolderFrame.BackgroundColor3 = Color3FromRGB(20, 20, 20)
    TabsHolderFrame.BorderColor3 = FrameBorderColor
    TabsHolderFrame.BorderSizePixel = 2
    TabsHolderFrame.Position = UDim2(0.0250000004, 0, 0.0209999997, 0)
    TabsHolderFrame.Size = UDim2(0, 503, 0, 42)
    TabsHolderFrame.Parent = MainFrame
    
    local TabsHolderFrame_UIStroke = NewInstance("UIStroke")
    TabsHolderFrame_UIStroke.Name = "TabsHolderFrame_UIStroke"
    TabsHolderFrame_UIStroke.ApplyStrokeMode = "Border"
    TabsHolderFrame_UIStroke.Color = FrameInlineBorderColor
    TabsHolderFrame_UIStroke.LineJoinMode = "Miter"
    TabsHolderFrame_UIStroke.Thickness = 1 
    TabsHolderFrame_UIStroke.Transparency = 0 
    TabsHolderFrame_UIStroke.Enabled = true 
    TabsHolderFrame_UIStroke.Parent = TabsHolderFrame
    
    local TabsFrame = NewInstance("Frame") 
    TabsFrame.Name = "TabsFrame"
    TabsFrame.BackgroundColor3 = Color3FromRGB(255, 255, 255)
    TabsFrame.BackgroundTransparency = 1.000
    TabsFrame.Position = UDim2(0.0177865606, 0, 0.261904955, 0)
    TabsFrame.Size = UDim2(0, 488, 0, 25)
    TabsFrame.Parent = TabsHolderFrame
    
    local TabsFrame_UIListLayout = NewInstance("UIListLayout")
    TabsFrame_UIListLayout.Name = "TabsFrame_UIListLayout"
    TabsFrame_UIListLayout.FillDirection = Enum.FillDirection.Horizontal
    TabsFrame_UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
    TabsFrame_UIListLayout.Padding = UDim(0, 10)
    TabsFrame_UIListLayout.Parent = TabsFrame
    
    local Shadow = NewInstance("ImageLabel")
    Shadow.Name = "Shadow"
    Shadow.AnchorPoint = Vector2(0.5, 0.5)
    Shadow.BackgroundColor3 = Color3FromRGB(255, 255, 255)
    Shadow.BackgroundTransparency = 1.000
    Shadow.Position = UDim2(0.5, 0, 0.5, 0)
    Shadow.Size = UDim2(1, 45, 1, 45)
    Shadow.ZIndex = 0
    Shadow.Image = "rbxassetid://2654849154"
    Shadow.ImageRectOffset = Vector2(2, 2)
    Shadow.ImageRectSize = Vector2(252, 252)
    Shadow.ImageTransparency = 0.400
    Shadow.ScaleType = Enum.ScaleType.Slice
    Shadow.SliceCenter = Rect(64, 64, 192, 192)
    Shadow.SliceScale = 0.310
    Shadow.ImageColor3 = BackgroundGlowColor
    Shadow.Parent = BackFrame
    
    local NameLabel = NewInstance("TextLabel")
    NameLabel.Name = "NameLabel"
    NameLabel.BackgroundColor3 = Color3FromRGB(255, 255, 255)
    NameLabel.BackgroundTransparency = 1.000
    NameLabel.Position = UDim2(0.0181818176, 0, 0, 0)
    NameLabel.Size = UDim2(0, 188, 0, 26)
    NameLabel.Font = TextFont
    NameLabel.LineHeight = 0.740
    NameLabel.Text = Name
    NameLabel.TextColor3 = TextColor
    NameLabel.TextSize = 14.000
    NameLabel.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
    NameLabel.Parent = BackFrame
    
    patches.FixTextSize(NameLabel, -2)
    
    local FpsAndPingLabel = NewInstance("TextLabel")
    FpsAndPingLabel.Name = "FpsAndPingLabel"
    FpsAndPingLabel.BackgroundColor3 = Color3FromRGB(255, 255, 255)
    FpsAndPingLabel.BackgroundTransparency = 1.000
    FpsAndPingLabel.Position = UDim2(0.73636359, 0, 0, 0)
    FpsAndPingLabel.Size = UDim2(0, 133, 0, 26)
    FpsAndPingLabel.Font = Enum.Font.Code
    FpsAndPingLabel.LineHeight = 0.740
    FpsAndPingLabel.Text = ""
    FpsAndPingLabel.TextColor3 = Color3FromRGB(255, 255, 255)
    FpsAndPingLabel.TextSize = 14.000
    FpsAndPingLabel.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
    FpsAndPingLabel.Visible = DisplayFpsAndPing
    FpsAndPingLabel.Parent = BackFrame
    
    local FpsAndPingLoop, FpsAmount, PingAmount = nil, 0, 0
    FpsAndPingLoop = Connect(RunService.Heartbeat, function(Step)
        FpsAmount = (1 / Step);
    end)
    
    resume(create(function() -- put it on a new thread
        while task.wait(1) do 
            FpsAndPingLabel.Text = format("fps - %d, ping - %d", FpsAmount, tonumber(string.split(Service.Stats.Network.ServerStatsItem["Data Ping"].GetValueString(Service.Stats.Network.ServerStatsItem["Data Ping"]), ".")[1]));
            patches.FixTextSize(FpsAndPingLabel, -4)
        end
    end))
    
    Connect(UserInputService.InputBegan, function(Key)
        if UserInputService.GetFocusedTextBox(UserInputService) then return end 
        
        if Key and Key.KeyCode == UIToggleKey then 
            MenuOpen = not MenuOpen
            
            BackFrame.Visible = MenuOpen 
            MainFrame.Visible = MenuOpen
        end
    end)
    
    local internalfunctions = {}
    
    function internalfunctions.HandleToolTip(Object, Text)    
        assert((Object or typeof(Object) == "Instance"));
        assert((Text or type(Text) == "string"));
        
        local ToolTip = NewInstance("TextLabel")
        ToolTip.Name = "ToolTip"
        ToolTip.BackgroundColor3 = Color3FromRGB(20, 20, 20)
        ToolTip.BorderColor3 = ElementBorderColor
        ToolTip.BorderSizePixel = 2
        ToolTip.Position = UDim2(0.490150571, 0, 0.63190186, 0)
        ToolTip.Size = UDim2(0, 123, 0, 17)
        ToolTip.Font = TextFont
        ToolTip.Text = Text
        ToolTip.TextColor3 = TextColor
        ToolTip.TextSize = 14.000
        ToolTip.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
        ToolTip.Visible = false 
        ToolTip.Parent = ScreenGui
        
        local ToolTip_UIStroke = NewInstance("UIStroke")
        ToolTip_UIStroke.Name = "ToolTip_UIStroke"
        ToolTip_UIStroke.ApplyStrokeMode = "Border"
        ToolTip_UIStroke.Color = ElementsInlineBorderColor
        ToolTip_UIStroke.LineJoinMode = "Miter"
        ToolTip_UIStroke.Thickness = 1 
        ToolTip_UIStroke.Transparency = 0 
        ToolTip_UIStroke.Enabled = true 
        ToolTip_UIStroke.Parent = ToolTip
        
        patches.FixTextSize(ToolTip, 5)
        
        local function OnToolTipMouseEnter()
            ToolTip.Visible = true 
            
            IsToolTipActive = true 
            ActiveToolTip = ToolTip
            
            RunService.BindToRenderStep(RunService, "ciazware_tooltip_loop", 1, UpdateToolTipPosition)
        end; Connect(Object.MouseEnter, OnToolTipMouseEnter);
        
        local function OnToolTipMouseLeave()
            ToolTip.Visible = false
            
            IsToolTipActive = false
            ActiveToolTip = nil 
            
            RunService.UnbindFromRenderStep(RunService, "ciazware_tooltip_loop")
        end; Connect(Object.MouseLeave, OnToolTipMouseLeave);
    end

    local tabs = {}
    
    function tabs.AddTab(Name)
        assert((Name or type(Name) == "string"));
        
        local TabButton = NewInstance("TextButton")
        TabButton.Name = Name
        TabButton.BackgroundColor3 = Color3FromRGB(20, 20, 20)
        TabButton.BorderColor3 = ElementBorderColor
        TabButton.BorderSizePixel = 2
        TabButton.Position = UDim2(0.830841064, 0, 1.10017526, 0)
        TabButton.Size = UDim2(0, 53, 0, 23)
        TabButton.Font = TextFont
        TabButton.Text = Name
        TabButton.TextColor3 = TextColor
        TabButton.TextSize = 14.000
        TabButton.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
        TabButton.Parent = TabsFrame
        
        local TabButton_UIStroke = NewInstance("UIStroke")
        TabButton_UIStroke.Name = "TabButton_UIStroke"
        TabButton_UIStroke.ApplyStrokeMode = "Border"
        TabButton_UIStroke.Color = ElementsInlineBorderColor
        TabButton_UIStroke.LineJoinMode = "Miter"
        TabButton_UIStroke.Thickness = 1 
        TabButton_UIStroke.Transparency = 0 
        TabButton_UIStroke.Enabled = true 
        TabButton_UIStroke.Parent = TabButton
        
        patches.FixTextSize(TabButton, 5)
        
        local function OnTabButtonClick()
            for Index, Object in next, GetChildren(TabsFrame) do 
                if Object and IsA(Object, "TextButton") then 
                    Object.BackgroundColor3 = Color3FromRGB(20, 20, 20)
                end
            end
            
            task.wait()
            
            TabButton.BackgroundColor3 = TabHighlightColor
            
            for Index, Object in next, GetChildren(SectionsFrame) do 
                Object.Visible = (find(split(Object.Name, "_")[2], Name) and true or false)
            end
        end; Connect(TabButton.MouseButton1Click, OnTabButtonClick);
        
        local sections = {}
        
        function sections.AddSection()
            local SectionFrame = NewInstance("Frame")
            SectionFrame.Name = format("SectionFrame_%s", TabButton.Name)
            SectionFrame.BackgroundColor3 = Color3FromRGB(20, 20, 20)
            SectionFrame.BorderColor3 = FrameBorderColor
            SectionFrame.BorderSizePixel = 2
            SectionFrame.Position = UDim2(-0.00169626868, 0, -0.0684931427, 35)
            SectionFrame.Size = UDim2(0, 503, 0, 486)
            SectionFrame.Visible = false 
            SectionFrame.Parent = SectionsFrame
            
            local SectionFrame_UIStroke = NewInstance("UIStroke")
            SectionFrame_UIStroke.Name = "SectionFrame_UIStroke"
            SectionFrame_UIStroke.ApplyStrokeMode = "Border"
            SectionFrame_UIStroke.Color = FrameInlineBorderColor
            SectionFrame_UIStroke.LineJoinMode = "Miter"
            SectionFrame_UIStroke.Thickness = 1 
            SectionFrame_UIStroke.Transparency = 0 
            SectionFrame_UIStroke.Enabled = true 
            SectionFrame_UIStroke.Parent = SectionFrame
            
            local SectionTabsHolderFrame = NewInstance("Frame")
            SectionTabsHolderFrame.Name = "SectionTabsHolderFrame"
            SectionTabsHolderFrame.BackgroundColor3 = Color3FromRGB(20, 20, 20)
            SectionTabsHolderFrame.BorderColor3 = FrameBorderColor
            SectionTabsHolderFrame.BorderSizePixel = 2
            SectionTabsHolderFrame.Position = UDim2(0.0357852876, 0, 0.0308641978, 0)
            SectionTabsHolderFrame.Size = UDim2(0, 466, 0, 42)
            SectionTabsHolderFrame.Parent = SectionFrame
            
            local SectionTabsFrame_UIStroke = NewInstance("UIStroke")
            SectionTabsFrame_UIStroke.Name = "SectionTabsFrame_UIStroke"
            SectionTabsFrame_UIStroke.ApplyStrokeMode = "Border"
            SectionTabsFrame_UIStroke.Color = FrameInlineBorderColor
            SectionTabsFrame_UIStroke.LineJoinMode = "Miter"
            SectionTabsFrame_UIStroke.Thickness = 1 
            SectionTabsFrame_UIStroke.Transparency = 0 
            SectionTabsFrame_UIStroke.Enabled = true 
            SectionTabsFrame_UIStroke.Parent = SectionTabsHolderFrame
            
            local SectionTabsFrame = NewInstance("Frame")
            SectionTabsFrame.Name = "SectionTabsFrame"
            SectionTabsFrame.BackgroundColor3 = Color3FromRGB(255, 255, 255)
            SectionTabsFrame.BackgroundTransparency = 1.000
            SectionTabsFrame.Position = UDim2(0.0201459229, 0, 0.261523664, -1)
            SectionTabsFrame.Size = UDim2(0, 448, 0, 25)
            SectionTabsFrame.Parent = SectionTabsHolderFrame
            
            local SectionTabsFrame_UIListLayout = NewInstance("UIListLayout")
            SectionTabsFrame_UIListLayout.Name = "SectionTabsFrame_UIListLayout"
            SectionTabsFrame_UIListLayout.FillDirection = Enum.FillDirection.Horizontal
            SectionTabsFrame_UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
            SectionTabsFrame_UIListLayout.Padding = UDim(0, 10)
            SectionTabsFrame_UIListLayout.Parent = SectionTabsFrame
            
            local SubSectionsFrame = NewInstance("Frame")
            SubSectionsFrame.Name = "SubSectionsFrame"
            SubSectionsFrame.BackgroundColor3 = Color3FromRGB(20, 20, 20)
            SubSectionsFrame.BackgroundTransparency = 1.000
            SubSectionsFrame.BorderColor3 = FrameBorderColor
            SubSectionsFrame.BorderSizePixel = 2
            SubSectionsFrame.Position = UDim2(0.0357852876, 0, 0.146090537, 0)
            SubSectionsFrame.Size = UDim2(0, 466, 0, 403)
            SubSectionsFrame.Parent = SectionFrame
            
            local subsections = {}
            
            function subsections.AddSubSection(Name)
                assert((Name or type(Name) == "string"));
                
                local SectionTabButton = NewInstance("TextButton")
                SectionTabButton.Name = format("SectionTabButton_%s", TabButton.Name)
                SectionTabButton.BackgroundColor3 = Color3FromRGB(20, 20, 20)
                SectionTabButton.BorderColor3 = ElementBorderColor
                SectionTabButton.BorderSizePixel = 2
                SectionTabButton.Position = UDim2(0.830841064, 0, 1.10017526, 0)
                SectionTabButton.Size = UDim2(0, 53, 0, 23)
                SectionTabButton.Font = TextFont
                SectionTabButton.Text = Name
                SectionTabButton.TextColor3 = TextColor
                SectionTabButton.TextSize = 14.000
                SectionTabButton.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
                SectionTabButton.Parent = SectionTabsFrame
                
                local SectionTabButton_UIStroke = NewInstance("UIStroke")
                SectionTabButton_UIStroke.Name = "SectionTabButton_UIStroke"
                SectionTabButton_UIStroke.ApplyStrokeMode = "Border"
                SectionTabButton_UIStroke.Color = ElementsInlineBorderColor
                SectionTabButton_UIStroke.LineJoinMode = "Miter"
                SectionTabButton_UIStroke.Thickness = 1 
                SectionTabButton_UIStroke.Transparency = 0 
                SectionTabButton_UIStroke.Enabled = true 
                SectionTabButton_UIStroke.Parent = SectionTabButton
                
                patches.FixTextSize(SectionTabButton, 5)
                
                local function OnSectionTabButtonClick()
                    for Index, Object in next, GetChildren(SectionTabsFrame) do 
                        if Object and IsA(Object, "TextButton") then 
                            Object.BackgroundColor3 = Color3FromRGB(20, 20, 20)
                        end
                    end
                    
                    task.wait()
                    
                    SectionTabButton.BackgroundColor3 = TabHighlightColor
                    
                    for Index, Object in next, GetChildren(SubSectionsFrame) do 
                        Object.Visible = (find(Object.Name, --[[split(Object.Name, "_")[2],]] Name) and true or false)
                    end
                end; Connect(SectionTabButton.MouseButton1Click, OnSectionTabButtonClick);
                
                local SubSection = NewInstance("Frame")
                SubSection.Name = Name--format("SubSection_%s", TabButton.Name)
                SubSection.BackgroundColor3 = Color3FromRGB(20, 20, 20)
                SubSection.BorderColor3 = FrameBorderColor
                SubSection.BorderSizePixel = 2
                SubSection.Position = UDim2(-0.00069539994, 0, -0.000311452895, 0)
                SubSection.Size = UDim2(0, 466, 0, 403)
                SubSection.Visible = false 
                SubSection.Parent = SubSectionsFrame

                local SubSection_UIStroke = NewInstance("UIStroke")
                SubSection_UIStroke.Name = "SubSection_UIStroke"
                SubSection_UIStroke.ApplyStrokeMode = "Border"
                SubSection_UIStroke.Color = FrameInlineBorderColor
                SubSection_UIStroke.LineJoinMode = "Miter"
                SubSection_UIStroke.Thickness = 1 
                SubSection_UIStroke.Transparency = 0 
                SubSection_UIStroke.Enabled = true 
                SubSection_UIStroke.Parent = SubSection
                
                local SubSection_LeftSideFrame = NewInstance("Frame")
                SubSection_LeftSideFrame.Name = "SubSection_LeftSideFrame"
                SubSection_LeftSideFrame.BackgroundColor3 = Color3FromRGB(255, 255, 255)
                SubSection_LeftSideFrame.BackgroundTransparency = 1.000
                SubSection_LeftSideFrame.BorderSizePixel = 0
                SubSection_LeftSideFrame.Size = UDim2(0, 234, 0, 403)
                SubSection_LeftSideFrame.Parent = SubSection
                
                local LeftSideFrame_LabelsFrame = NewInstance("Frame")
                LeftSideFrame_LabelsFrame.Name = "LeftSideFrame_LabelsFrame"
                LeftSideFrame_LabelsFrame.BackgroundColor3 = Color3FromRGB(255, 255, 255)
                LeftSideFrame_LabelsFrame.BackgroundTransparency = 1.000
                LeftSideFrame_LabelsFrame.Size = UDim2(0, 115, 0, 403)
                LeftSideFrame_LabelsFrame.Parent = SubSection_LeftSideFrame
                
                local LeftLabelsFrame_UIListLayout = NewInstance("UIListLayout")
                LeftLabelsFrame_UIListLayout.Name = "LabelsFrame_UIListLayout"
                LeftLabelsFrame_UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
                LeftLabelsFrame_UIListLayout.Padding = UDim(0, 1)
                LeftLabelsFrame_UIListLayout.Parent = LeftSideFrame_LabelsFrame
                
                local LeftSideFrame_InteractablesFrame = NewInstance("Frame")
                LeftSideFrame_InteractablesFrame.Name = "LeftSideFrame_InteractablesFrame"
                LeftSideFrame_InteractablesFrame.BackgroundColor3 = Color3FromRGB(255, 255, 255)
                LeftSideFrame_InteractablesFrame.BackgroundTransparency = 1.000
                LeftSideFrame_InteractablesFrame.Position = UDim2(0.0415044278, 0, 0.0198511165, 0)
                LeftSideFrame_InteractablesFrame.Size = UDim2(0, 216, 0, 395)
                LeftSideFrame_InteractablesFrame.Parent = SubSection_LeftSideFrame
                
                local LeftInteractablesFrame_UIListLayout = NewInstance("UIListLayout")
                LeftInteractablesFrame_UIListLayout.Name = "LeftInteractablesFrame_UIListLayout"
                LeftInteractablesFrame_UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Right
                LeftInteractablesFrame_UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
                LeftInteractablesFrame_UIListLayout.Padding = UDim(0, 20)
                LeftInteractablesFrame_UIListLayout.Parent = LeftSideFrame_InteractablesFrame
                
                local SubSection_MiddleSpliterFrame = NewInstance("Frame")
                SubSection_MiddleSpliterFrame.Name = "SubSection_MiddleSpliterFrame"
                SubSection_MiddleSpliterFrame.BackgroundColor3 = FrameBorderColor
                SubSection_MiddleSpliterFrame.BorderSizePixel = 0
                SubSection_MiddleSpliterFrame.Position = UDim2(0.502145886, 0, 0, 0)
                SubSection_MiddleSpliterFrame.Size = UDim2(0, 1, 0, 403)
                SubSection_MiddleSpliterFrame.Parent = SubSection

                local MiddleSpliterFrame_UIStroke = NewInstance("UIStroke")
                MiddleSpliterFrame_UIStroke.Name = "MiddleSpliterFrame_UIStroke"
                MiddleSpliterFrame_UIStroke.ApplyStrokeMode = "Border"
                MiddleSpliterFrame_UIStroke.Color = FrameInlineBorderColor
                MiddleSpliterFrame_UIStroke.LineJoinMode = "Miter"
                MiddleSpliterFrame_UIStroke.Thickness = 1 
                MiddleSpliterFrame_UIStroke.Transparency = 0 
                MiddleSpliterFrame_UIStroke.Enabled = true 
                MiddleSpliterFrame_UIStroke.Parent = SubSection_MiddleSpliterFrame
                
                local SubSection_RightSideFrame = NewInstance("Frame")
                SubSection_RightSideFrame.Name = "SubSection_RightSideFrame"
                SubSection_RightSideFrame.BackgroundColor3 = Color3FromRGB(255, 255, 255)
                SubSection_RightSideFrame.BackgroundTransparency = 1.000
                SubSection_RightSideFrame.Position = UDim2(0.5, 0, 0, 0)
                SubSection_RightSideFrame.Size = UDim2(0, 233, 0, 403)
                SubSection_RightSideFrame.Parent = SubSection
                
                local RightSideFrame_LabelsFrame = NewInstance("Frame")
                RightSideFrame_LabelsFrame.Name = "RightSideFrame_LabelsFrame"
                RightSideFrame_LabelsFrame.BackgroundColor3 = Color3FromRGB(255, 255, 255)
                RightSideFrame_LabelsFrame.BackgroundTransparency = 1.000
                RightSideFrame_LabelsFrame.Size = UDim2(0, 115, 0, 403)
                RightSideFrame_LabelsFrame.Parent = SubSection_RightSideFrame
                
                local RightLabelsFrame_UIListLayout = NewInstance("UIListLayout")
                RightLabelsFrame_UIListLayout.Name = "RightLabelsFrame_UIListLayout"
                RightLabelsFrame_UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
                RightLabelsFrame_UIListLayout.Padding = UDim(0, 1)
                RightLabelsFrame_UIListLayout.Parent = RightSideFrame_LabelsFrame
                
                local RightSideFrame_InteractablesFrame = NewInstance("Frame")
                RightSideFrame_InteractablesFrame.Name = "RightSideFrame_InteractablesFrame"
                RightSideFrame_InteractablesFrame.BackgroundColor3 = Color3FromRGB(255, 255, 255)
                RightSideFrame_InteractablesFrame.BackgroundTransparency = 1.000
                RightSideFrame_InteractablesFrame.Position = UDim2(0.0415044278, 0, 0.0198511165, 0)
                RightSideFrame_InteractablesFrame.Size = UDim2(0, 216, 0, 395)
                RightSideFrame_InteractablesFrame.Parent = SubSection_RightSideFrame
                
                local RightInteractablesFrame_UIListLayout = NewInstance("UIListLayout")
                RightInteractablesFrame_UIListLayout.Name = "RightInteractablesFrame_UIListLayout"
                RightInteractablesFrame_UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Right
                RightInteractablesFrame_UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
                RightInteractablesFrame_UIListLayout.Padding = UDim(0, 20)
                RightInteractablesFrame_UIListLayout.Parent = RightSideFrame_InteractablesFrame
                
                local elements = {}
                
                function elements.AddToggle(Name, Callback, Side)
                    assert((Name or type(Name) == "string"));
                    assert((Callback or type(Callback) == "function"));
                    assert((Side or type(Side) == "string" or (find(lower(Side), "left") or find(lower(Side), "right"))));
                    
                    local Toggled = false
                    
                    local ToggleLabel = NewInstance("TextLabel")
                    ToggleLabel.Name = "ToggleLabel"
                    ToggleLabel.BackgroundColor3 = Color3FromRGB(255, 255, 255)
                    ToggleLabel.BackgroundTransparency = 1.000
                    ToggleLabel.Size = UDim2(0, 71, 0, 36)
                    ToggleLabel.Font = TextFont
                    ToggleLabel.Text = Name
                    ToggleLabel.TextColor3 = TextColor
                    ToggleLabel.TextSize = 14.000
                    ToggleLabel.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
                    ToggleLabel.Parent = ((find(lower(Side), "left") and LeftSideFrame_LabelsFrame) or (find(lower(Side), "right") and RightSideFrame_LabelsFrame));
                    
                    local ToggleButton = NewInstance("TextButton")
                    ToggleButton.Name = "ToggleButton"
                    ToggleButton.BackgroundColor3 = Color3FromRGB(20, 20, 20)
                    ToggleButton.BorderColor3 = ElementBorderColor
                    ToggleButton.BorderSizePixel = 2
                    ToggleButton.Size = UDim2(0, 39, 0, 19)
                    ToggleButton.Font = TextFont
                    ToggleButton.Text = ""
                    ToggleButton.TextColor3 = TextColor
                    ToggleButton.TextSize = 14.000
                    ToggleButton.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
                    ToggleButton.Parent = ((find(lower(Side), "left") and LeftSideFrame_InteractablesFrame) or (find(lower(Side), "right") and RightSideFrame_InteractablesFrame));
                    
                    local ToggleButton_UIStroke = NewInstance("UIStroke")
                    ToggleButton_UIStroke.Name = "ToggleButton_UIStroke"
                    ToggleButton_UIStroke.ApplyStrokeMode = "Border"
                    ToggleButton_UIStroke.Color = ElementsInlineBorderColor
                    ToggleButton_UIStroke.LineJoinMode = "Miter"
                    ToggleButton_UIStroke.Thickness = 1 
                    ToggleButton_UIStroke.Transparency = 0 
                    ToggleButton_UIStroke.Enabled = true 
                    ToggleButton_UIStroke.Parent = ToggleButton
                    
                    local function OnToggleButtonClick()
                        Toggled = not Toggled
                        
                        patches.FadeObject(ToggleButton, 0.5, ((Toggled == true and ToggleButton.BorderColor3) or (Toggled == false and Color3FromRGB(20, 20, 20))), false);
                        ToggleButton_UIStroke.Enabled = not Toggled 
                        
                        Callback(Toggled)
                    end; Connect(ToggleButton.MouseButton1Click, OnToggleButtonClick)
                    
                    patches.FixTextSize(ToggleLabel, 20)
                    
                    local subelements = {}
                    
                    function subelements.AddToolTip(Text)
                        assert((Text or type(Text) == "string"))
                        internalfunctions.HandleToolTip(ToggleLabel, Text) 
                    end
                    
                    return subelements
                end
                
                function elements.AddTextBox(Name, Callback, Side)
                    assert((Name or type(Name) == "string"));
                    assert((Callback or type(Callback) == "function"));
                    assert((Side or type(Side) == "string" or (find(lower(Side), "left") or find(lower(Side), "right"))));
                    
                    local TextBoxLabel = NewInstance("TextLabel")
                    TextBoxLabel.Name = "TextBoxLabel"
                    TextBoxLabel.BackgroundColor3 = Color3FromRGB(255, 255, 255)
                    TextBoxLabel.BackgroundTransparency = 1.000
                    TextBoxLabel.Size = UDim2(0, 71, 0, 36)
                    TextBoxLabel.Font = TextFont
                    TextBoxLabel.Text = Name
                    TextBoxLabel.TextColor3 = TextColor
                    TextBoxLabel.TextSize = 14.000
                    TextBoxLabel.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
                    TextBoxLabel.Parent = ((find(lower(Side), "left") and LeftSideFrame_LabelsFrame) or (find(lower(Side), "right") and RightSideFrame_LabelsFrame));
                    
                    patches.FixTextSize(TextBoxLabel, 20)
                    
                    local TextBox = NewInstance("TextBox")
                    TextBox.BackgroundColor3 = Color3FromRGB(20, 20, 20)
                    TextBox.BorderColor3 = ElementBorderColor
                    TextBox.BorderSizePixel = 2
                    TextBox.Position = UDim2(0.116974272, 0, 0.0936708897, 0)
                    TextBox.Size = UDim2(0, 67, 0, 19)
                    TextBox.Font = TextFont
                    TextBox.Text = ""
                    TextBox.TextColor3 = TextColor
                    TextBox.TextSize = 14.000
                    TextBox.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
                    TextBox.Parent = ((find(lower(Side), "left") and LeftSideFrame_InteractablesFrame) or (find(lower(Side), "right") and RightSideFrame_InteractablesFrame));
                    
                    local TextBox_UIStroke = NewInstance("UIStroke")
                    TextBox_UIStroke.Name = "TextBox_UIStroke"
                    TextBox_UIStroke.ApplyStrokeMode = "Border"
                    TextBox_UIStroke.Color = ElementsInlineBorderColor
                    TextBox_UIStroke.LineJoinMode = "Miter"
                    TextBox_UIStroke.Thickness = 1 
                    TextBox_UIStroke.Transparency = 0 
                    TextBox_UIStroke.Enabled = true 
                    TextBox_UIStroke.Parent = TextBox
                    
                    local function OnTextBoxFocusLost()
                        if len(TextBox.Text) > 0 then 
                            Callback(TextBox.Text)
                        end
                    end; Connect(TextBox.FocusLost, OnTextBoxFocusLost);
                    
                    local subelements = {}
                    
                    function subelements.AddToolTip(Text)
                        assert((Text or type(Text) == "string"))
                        internalfunctions.HandleToolTip(TextBoxLabel, Text) 
                    end
                    
                    return subelements
                end
                
                function elements.AddDropdown(Name, Options, Callback, Side)
                    assert((Name or type(Name) == "string"));
                    assert((Options or type(Options) == "table" or #Options == 0));
                    assert((Callback or type(Callback) == "function"));
                    assert((Side or type(Side) == "string" or (find(lower(Side), "left") or find(lower(Side), "right"))));
                    
                    local DropdownOpen = false
                    
                    local DropdownLabel = NewInstance("TextLabel")
                    DropdownLabel.Name = "DropdownLabel"
                    DropdownLabel.BackgroundColor3 = Color3FromRGB(255, 255, 255)
                    DropdownLabel.BackgroundTransparency = 1.000
                    DropdownLabel.Position = UDim2(0, 0, 0.17866005, 0)
                    DropdownLabel.Size = UDim2(0, 78, 0, 36)
                    DropdownLabel.Font = TextFont
                    DropdownLabel.Text = Name
                    DropdownLabel.TextColor3 = TextColor
                    DropdownLabel.TextSize = 14.000
                    DropdownLabel.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
                    DropdownLabel.Parent = ((find(lower(Side), "left") and LeftSideFrame_LabelsFrame) or (find(lower(Side), "right") and RightSideFrame_LabelsFrame));
                    
                    local DropdownButton = NewInstance("TextButton")
                    DropdownButton.Name = "DropdownButton"
                    DropdownButton.BackgroundColor3 = Color3FromRGB(20, 20, 20)
                    DropdownButton.BorderColor3 = ElementBorderColor
                    DropdownButton.BorderSizePixel = 2
                    DropdownButton.Position = UDim2(0.681921244, 0, 0.187341779, 0)
                    DropdownButton.Size = UDim2(0, 68, 0, 19)
                    DropdownButton.Font = TextFont
                    DropdownButton.Text = ""
                    DropdownButton.TextColor3 = TextColor
                    DropdownButton.TextSize = 14.000
                    DropdownButton.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
                    DropdownButton.Parent = ((find(lower(Side), "left") and LeftSideFrame_InteractablesFrame) or (find(lower(Side), "right") and RightSideFrame_InteractablesFrame));
                    
                    local DropdownButton_UIStroke = NewInstance("UIStroke")
                    DropdownButton_UIStroke.Name = "TextBox_UIStroke"
                    DropdownButton_UIStroke.ApplyStrokeMode = "Border"
                    DropdownButton_UIStroke.Color = ElementsInlineBorderColor
                    DropdownButton_UIStroke.LineJoinMode = "Miter"
                    DropdownButton_UIStroke.Thickness = 1 
                    DropdownButton_UIStroke.Transparency = 0 
                    DropdownButton_UIStroke.Enabled = true 
                    DropdownButton_UIStroke.Parent = DropdownButton
                    
                    local DropdownButton_OptionsFrame = NewInstance("Frame")
                    DropdownButton_OptionsFrame.Name = "DropdownButton_OptionsFrame"
                    DropdownButton_OptionsFrame.BackgroundColor3 = Color3FromRGB(20, 20, 20)
                    DropdownButton_OptionsFrame.BorderColor3 = ElementBorderColor
                    DropdownButton_OptionsFrame.BorderSizePixel = 2
                    DropdownButton_OptionsFrame.Position = UDim2(-0.0103678983, 0, 1.36842108, 0)
                    DropdownButton_OptionsFrame.Size = UDim2(0, 68, 0, 100)
                    DropdownButton_OptionsFrame.Visible = false
                    DropdownButton_OptionsFrame.ZIndex = 7
                    DropdownButton_OptionsFrame.Parent = DropdownButton
                    
                    local OptionsFrame_UIListLayout = NewInstance("UIListLayout")
                    OptionsFrame_UIListLayout.Name = "OptionsFrame_UIListLayout"
                    OptionsFrame_UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
                    OptionsFrame_UIListLayout.Parent = DropdownButton_OptionsFrame
                    
                    Connect(OptionsFrame_UIListLayout.GetPropertyChangedSignal(OptionsFrame_UIListLayout, "AbsoluteContentSize"), function()
                        DropdownButton_OptionsFrame.Size = UDim2(0, 68, 0, OptionsFrame_UIListLayout.AbsoluteContentSize.Y)
                    end)
                    
                    local OptionsFrame_UIStroke = NewInstance("UIStroke")
                    OptionsFrame_UIStroke.Name = "OptionsFrame_UIStroke"
                    OptionsFrame_UIStroke.ApplyStrokeMode = "Border"
                    OptionsFrame_UIStroke.Color = ElementsInlineBorderColor
                    OptionsFrame_UIStroke.LineJoinMode = "Miter"
                    OptionsFrame_UIStroke.Thickness = 1 
                    OptionsFrame_UIStroke.Transparency = 0 
                    OptionsFrame_UIStroke.Enabled = true 
                    OptionsFrame_UIStroke.Parent = DropdownButton_OptionsFrame
                    
                    local function OnDropdownButtonClick()
                        DropdownOpen = not DropdownOpen
                        
                        DropdownButton_OptionsFrame.BackgroundTransparency = ((DropdownOpen == true and 1) or (DropdownOpen == false and 0));
                        DropdownButton_OptionsFrame.Visible = DropdownOpen 
                        
                        patches.FadeObject(DropdownButton_OptionsFrame, 0.3, ((DropdownOpen == true and 0) or (DropdownOpen == false and 1)), false);
                        patches.FadeObject(OptionsFrame_UIStroke, 0.3, ((DropdownOpen == true and 0) or (DropdownOpen == false and 1)), false);
                    end; Connect(DropdownButton.MouseButton1Click, OnDropdownButtonClick);
                    
                    patches.FixTextSize(DropdownLabel, 20)
                    
                    table.foreachi(Options, function(Index, Option)
                        local OptionsFrame_Option = NewInstance("TextButton")
                        OptionsFrame_Option.Name = "OptionsFrame_Option"
                        OptionsFrame_Option.BackgroundColor3 = Color3FromRGB(20, 20, 20)
                        OptionsFrame_Option.BorderColor3 = FrameBorderColor
                        OptionsFrame_Option.BorderSizePixel = 0
                        OptionsFrame_Option.Size = UDim2(0, 68, 0, 22)
                        OptionsFrame_Option.ZIndex = 7
                        OptionsFrame_Option.Font = TextFont
                        OptionsFrame_Option.Text = Option
                        OptionsFrame_Option.TextColor3 = TextColor
                        OptionsFrame_Option.TextSize = 14.000
                        OptionsFrame_Option.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
                        OptionsFrame_Option.TextTransparency = 0
                        OptionsFrame_Option.Parent = DropdownButton_OptionsFrame 
                        
                        local function OnOptionButtonClick()
                            DropdownButton.Text = Option 
                            Callback(Option)
                            
                            patches.FadeObject(DropdownButton_OptionsFrame, 0.3, ((DropdownOpen == true and 1) or (DropdownOpen == false and 0)), false);
                            patches.FadeObject(OptionsFrame_UIStroke, 0.3, ((DropdownOpen == true and 1) or (DropdownOpen == false and 0)), false)
                            
                            delay(0.3, function()
                                DropdownButton_OptionsFrame.Visible = false 
                            end)
                        end; Connect(OptionsFrame_Option.MouseButton1Click, OnOptionButtonClick)
                    end)
                    
                    local subelements = {}
                    
                    function subelements.AddToolTip(Text)
                        assert((Text or type(Text) == "string"));
                        internalfunctions.HandleToolTip(DropdownLabel, Text) 
                    end
                    
                    return subelements
                end
                
                function elements.AddSlider(Name, Callback, Side, ...)
                    assert((Name or type(Name) == "string"));
                    assert((Callback or type(Callback) == "function"));
                    assert((Side or type(Side) == "string" or (find(lower(Side), "left") or find(lower(Side), "right"))));
                    assert((... or type(...) == "table"));
                    
                    local SettingsTable = (({...})[1]);
                    local Minimum, Maximum, Default = SettingsTable.Minimum, SettingsTable.Maximum, SettingsTable.Default;
                    table.foreach(SettingsTable, function(Index, Value)
                        assert((Value or type(Value) == "number"));
                    end)
                    
                    local Value, MoveConnection, ReleaseConnection = 0, false, nil

                    local SliderLabel = NewInstance("TextLabel")
                    SliderLabel.Name = "SliderLabel"
                    SliderLabel.BackgroundColor3 = Color3FromRGB(255, 255, 255)
                    SliderLabel.BackgroundTransparency = 1.000
                    SliderLabel.Size = UDim2(0, 71, 0, 36)
                    SliderLabel.Font = TextFont
                    SliderLabel.Text = Name
                    SliderLabel.TextColor3 = TextColor
                    SliderLabel.TextSize = 14.000
                    SliderLabel.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
                    SliderLabel.LineHeight = 0.4
                    SliderLabel.Parent = ((find(lower(Side), "left") and LeftSideFrame_LabelsFrame) or (find(lower(Side), "right") and RightSideFrame_LabelsFrame));
                    
                    local SliderButton = NewInstance("TextButton")
                    SliderButton.Name = "SliderButton"
                    SliderButton.BackgroundColor3 = Color3FromRGB(20, 20, 20)
                    SliderButton.BorderColor3 = ElementBorderColor
                    SliderButton.BorderSizePixel = 2
                    SliderButton.Position = UDim2(0.578703701, 0, 0.281012654, 0)
                    SliderButton.Size = UDim2(0, 91, 0, 19)
                    SliderButton.ZIndex = 2
                    SliderButton.Font = TextFont
                    SliderButton.Text = ""
                    SliderButton.TextColor3 = TextColor
                    SliderButton.TextSize = 14.000
                    SliderButton.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
                    SliderButton.Parent = ((find(lower(Side), "left") and LeftSideFrame_InteractablesFrame) or (find(lower(Side), "right") and RightSideFrame_InteractablesFrame));
                    
                    local SliderButton_UIStroke = NewInstance("UIStroke")
                    SliderButton_UIStroke.Name = "SliderButton_UIStroke"
                    SliderButton_UIStroke.ApplyStrokeMode = "Border"
                    SliderButton_UIStroke.Color = ElementsInlineBorderColor
                    SliderButton_UIStroke.LineJoinMode = "Miter"
                    SliderButton_UIStroke.Thickness = 1 
                    SliderButton_UIStroke.Transparency = 0 
                    SliderButton_UIStroke.Enabled = true 
                    SliderButton_UIStroke.Parent = SliderButton
                    
                    local SliderFrame = Instance.new("Frame")
                    SliderFrame.Name = "SliderFrame"
                    SliderFrame.BackgroundColor3 = Color3FromRGB(30, 30, 30)
                    SliderFrame.BorderSizePixel = 0
                    SliderFrame.Size = UDim2(0, 91, 0, 19)
                    SliderFrame.Visible = true 
                    SliderFrame.ZIndex = 3
                    SliderFrame.Parent = SliderButton
                    
                    local SliderFrame_SliderLabel = NewInstance("TextLabel")
                    SliderFrame_SliderLabel.Name = "SliderFrame_SliderLabel"
                    SliderFrame_SliderLabel.BackgroundColor3 = Color3FromRGB(255, 255, 255)
                    SliderFrame_SliderLabel.BackgroundTransparency = 1.000
                    SliderFrame_SliderLabel.Position = UDim2(0.109890111, 0, 0, 0)
                    SliderFrame_SliderLabel.Size = UDim2(0, 71, 0, 19)
                    SliderFrame_SliderLabel.ZIndex = 5
                    SliderFrame_SliderLabel.Font = TextFont
                    SliderFrame_SliderLabel.Text = format("%d / %d", Default, Maximum)
                    SliderFrame_SliderLabel.TextColor3 = TextColor
                    SliderFrame_SliderLabel.TextSize = 14.000
                    SliderFrame_SliderLabel.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
                    SliderFrame_SliderLabel.Parent = SliderButton
                    
                    local function OnSliderButtonDown()
                        local function UpdateSliderData()
                            local SliderPosition = UDim2(0, math.clamp((Mouse.X - SliderFrame.AbsolutePosition.X), 0, SliderButton.Size.X.Offset), 1, 0)
                            SliderFrame.Size = SliderPosition
                            
                            Value = math.floor((((Maximum - Minimum) / SliderButton.Size.X.Offset) * SliderFrame.AbsoluteSize.X) + Minimum)
                            SliderFrame_SliderLabel.Text = format("%d / %d", Value, Maximum)
                            
                            Callback(Value)
                        end
                        
                        MoveConnection = Connect(Mouse.Move, UpdateSliderData);
                        ReleaseConnection = Connect(UserInputService.InputEnded, function(Key)
                            if Key and Key.UserInputType == Enum.UserInputType.MouseButton1 then 
                                UpdateSliderData()
                                
                                MoveConnection.Disconnect(MoveConnection);
                                ReleaseConnection.Disconnect(ReleaseConnection);
                            end
                        end)
                    end; Connect(SliderButton.MouseButton1Down, OnSliderButtonDown);
                    
                    local subelements = {}
                    
                    function subelements.AddToolTip(Text)
                        assert((Text or type(Text) == "string"))
                        internalfunctions.HandleToolTip(SliderLabel, Text) 
                    end
                    
                    return subelements
                end
                
                function elements.AddKeybind(Name, Callback, Side)
                    assert((Name or type(Name) == "string"));
                    assert((Callback or type(Callback) == "function"));
                    assert((Side or type(Side) == "string" or (find(lower(Side), "left") or find(lower(Side), "right"))));
                    
                    local WaitingForKeybind, SelectedKey, Toggled = false, nil, false
                    
                    local KeybindLabel = NewInstance("TextLabel")
                    KeybindLabel.Name = "KeybindLabel"
                    KeybindLabel.BackgroundColor3 = Color3FromRGB(255, 255, 255)
                    KeybindLabel.BackgroundTransparency = 1.000
                    KeybindLabel.Size = UDim2(0, 71, 0, 36)
                    KeybindLabel.Font = TextFont
                    KeybindLabel.Text = Name
                    KeybindLabel.TextColor3 = TextColor
                    KeybindLabel.TextSize = 14.000
                    KeybindLabel.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
                    KeybindLabel.LineHeight = -1
                    KeybindLabel.Parent = ((find(lower(Side), "left") and LeftSideFrame_LabelsFrame) or (find(lower(Side), "right") and RightSideFrame_LabelsFrame));
                    
                    patches.FixTextSize(KeybindLabel, 25)
                    
                    local KeybindButton = NewInstance("TextButton")
                    KeybindButton.Name = "KeybindButton"
                    KeybindButton.BackgroundColor3 = Color3FromRGB(20, 20, 20)
                    KeybindButton.BorderColor3 = ElementBorderColor
                    KeybindButton.BorderSizePixel = 2
                    KeybindButton.Size = UDim2(0, 28, 0, 19)
                    KeybindButton.Font = TextFont
                    KeybindButton.Text = "[]"
                    KeybindButton.TextColor3 = TextColor
                    KeybindButton.TextSize = 14.000
                    KeybindButton.TextStrokeColor3 = Color3FromRGB(255, 255, 255)
                    KeybindButton.Parent = ((find(lower(Side), "left") and LeftSideFrame_InteractablesFrame) or (find(lower(Side), "right") and RightSideFrame_InteractablesFrame));
                    
                    local KeybindButton_UIStroke = NewInstance("UIStroke")
                    KeybindButton_UIStroke.Name = "KeybindButton_UIStroke"
                    KeybindButton_UIStroke.ApplyStrokeMode = "Border"
                    KeybindButton_UIStroke.Color = ElementsInlineBorderColor
                    KeybindButton_UIStroke.LineJoinMode = "Miter"
                    KeybindButton_UIStroke.Thickness = 1 
                    KeybindButton_UIStroke.Transparency = 0 
                    KeybindButton_UIStroke.Enabled = true 
                    KeybindButton_UIStroke.Parent = KeybindButton
                    
                    local function OnKeybindButtonClick()
                        KeybindButton.Text = "[...]"
                        patches.FixTextSize(KeybindButton, 5)
                        WaitingForKeybind = true 
                    end; Connect(KeybindButton.MouseButton1Click, OnKeybindButtonClick)
                    
                    local InputBeganConnection = nil 
                    InputBeganConnection = Connect(UserInputService.InputBegan, function(Key)
                        if (Key.UserInputType == Enum.UserInputType.Keyboard or Key.UserInputType) then 
                            Key = ((Key.UserInputType == Enum.UserInputType.Keyboard and Key.KeyCode) or Key.UserInputType)
                            local KeyName = Key.Name
                            
                            if WaitingForKeybind == true then 
                                if not table.find(BlacklistedKeyNames, KeyName) then 
                                    KeybindButton.Text = format("[%s]", lower(KeyName))
                                    SelectedKey = KeyName
                                    
                                    patches.FixTextSize(KeybindButton, 5)
                                else 
                                    KeybindButton.Text = format("[%s]", "blacklisted keycode")
                                    SelectedKey = "blacklisted keycode"
                                    
                                    patches.FixTextSize(KeybindButton, 5)
                                end
                                
                                WaitingForKeybind = false 
                            elseif WaitingForKeybind == false then 
                                if KeyName == SelectedKey then 
                                    Toggled = not Toggled
                                    Callback(KeyName)
                                end
                            end
                        end
                    end)
                    
                    local subelements = {}
                    
                    function subelements.AddToolTip(Text)
                        assert((Text or type(Text) == "string"))
                        internalfunctions.HandleToolTip(KeybindLabel, Text) 
                    end
                    
                    return subelements
                end
                
                return elements
            end
            
            return subsections
        end
        
        return sections
    end
    
    return tabs
end


library.configuration = {
   version = "1.3",
   frames = {
       MainBackFrameColor = Color3.fromRGB(138, 138, 138),
       BorderColor = Color3.fromRGB(50, 50, 50),
       InlineBorderColor = Color3.fromRGB(10, 10, 10),
   },

   elements = {
       BorderColor = Color3.fromRGB(50, 50, 50),
       InlineBorderColor = Color3.fromRGB(10, 10, 10),
   },
 
   text = {
       Color = Color3.fromRGB(255, 255, 255),
       Font = "Code",
   },
 
   miscellaneous = {
       BackgroundGlowColor = Color3.fromRGB(255, 255, 255),
       TabHighlightColor = Color3.fromRGB(30, 30, 30),
       
       DisplayFpsAndPing = true,
       UIToggleKey = Enum.KeyCode.RightAlt,
   },
};

local UI = library.new("METAWARE **TESTING_GAME**");
local UI_TAB = UI.AddTab("Test Tab")
local UI_SECTION = UI_TAB.AddSection();

local UI_SUBSECTION = UI_SECTION.AddSubSection("Test SUBSECTION");
local UI_TOGGLE = UI_SUBSECTION.AddToggle("toggle", function(state)
   print(tostring(state));
end, "Left")
local UI_TOGGLE_TOOLTIP = UI_TOGGLE.AddToolTip("test!")
