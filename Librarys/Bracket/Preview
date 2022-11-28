local Bracket = loadstring(game:HttpGet("https://raw.githubusercontent.com/AlexR32/Bracket/main/BracketV32.lua"))()
Bracket:Notification() Bracket:Notification2()

local Window = Bracket:Window({Name = "Window",Enabled = true,Color = Color3.new(1,0.5,0.25),Size = UDim2.new(0,496,0,496),Position = UDim2.new(0.5,-248,0.5,-248)}) do
	--Window:ChangeName("Window")
	--Window:ChangeSize(UDim2.new(0,496,0,496))
	--Window:ChangePosition(UDim2.new(0.5,-248,0.5,-248))
	--Window:ChangeColor(Color3.new(1,0.5,0.25))
	--Window:Toggle(true)
	--Window.Background -- ImageLabel
	local Tab = Window:Tab({Name = "Tab"}) do
		--Tab:ChangeName("Tab")

		--Side might be "Left", "Right" or nil for auto side choose
		--if callback nil then it will be replaced with print function
		Tab:Divider({Text = "Divider",Side = "Left"})

		local Label = Tab:Label({Text = "Label",Side = "Left"})
		--Label:ChangeText("Label")

		local Button = Tab:Button({Name = "Button",Side = "Left",Callback = function()end})
		--Button:ChangeName("Button")
		--Button:ChangeCallback(function()end)
		--Button:ToolTip("ToolTip")

		local Toggle = Tab:Toggle({Name = "Toggle",Side = "Left",Value = false,Callback = function(Bool)end})
		--Toggle:ChangeName("Toggle")
		--Toggle:ChangeValue(true)
		--Toggle:ChangeCallback(function(Bool)end)
		--Toggle:ToolTip("ToolTip")
		--Toggle:Keybind({Key = "NONE",Mouse = false,Blacklist = {"W","A","S","D","Slash","Tab","Backspace","Escape","Space","Delete","Unknown","Backquote"},Callback = function(Bool,Key)end})

		local Slider = Tab:Slider({Name = "Slider",Side = "Left",Min = 0,Max = 100,Value = 50,Precise = 2,Unit = "",Callback = function(Number)end})
		--Slider:ChangeName("Slider")
		--Slider:ChangeValue(50)
		--Slider:ChangeCallback(function(Number)end)
		--Slider:ToolTip("ToolTip")

		local Textbox = Tab:Textbox({Name = "Textbox",Side = "Left",Text = "Text",Placeholder = "Placeholder",NumberOnly = false,Callback = function(String)end})
		--Textbox:ChangeName("Textbox")
		--Textbox:ChangeText("Text")
		--Textbox:ChangePlaceholder("Placeholder")
		--Textbox:ChangeCallback(function(String)end)
		--Textbox:ToolTip("ToolTip")

		local Keybind = Tab:Keybind({Name = "Keybind",Side = "Left",Key = "NONE",Mouse = false,Blacklist = {"W","A","S","D","Slash","Tab","Backspace","Escape","Space","Delete","Unknown","Backquote"},Callback = function(Bool,Key)end})
		--Keybind:ChangeName("Keybind")
		--Keybind:ChangeCallback(function(Bool,Key)end)
		--Keybind:ToolTip("ToolTip")
		
		local BodyParts = {"Head"}
		local Dropdown = Tab:Dropdown({Name = "Dropdown",Side = "Left",Default = BodyParts,List = {
			{
				Name = "Head",
				Mode = "Toggle",
				Value = false,
				Callback = function(Selected)
					BodyParts = Selected
					print(BodyParts)
				end
			},
			{
				Name = "HumanoidRootPart",
				Mode = "Toggle",
				Value = false,
				Callback = function(Selected)
					BodyParts = Selected
					print(BodyParts)
				end
			}
		}})
		--Dropdown:Clear()
		--Dropdown:AddOption("Option")
		--Dropdown:RemoveOption("Option")
		--Dropdown:SelectOption("Option")
		--Dropdown:ChangeName("Dropdown")
		--Dropdown:ToolTip("ToolTip")

		local Colorpicker = Tab:Colorpicker({Name = "Colorpicker",Side = "Left",Color = Color3.new(1,0,0),Callback = function(Color,Table)end})
		--Colorpicker:ChangeName("Colorpicker")
		--Colorpicker:ChangeCallback(function(Color3)end)
		--Colorpicker:ChangeValue(Color3.new(1,0,0))
		--Colorpicker:ToolTip("ToolTip")

		local Section = Tab:Section({Name = "Section",Side = "Right"}) do
			--Same Elements as in tab but without side option
			Section:Divider()
			Section:Label()
			Section:Button()
			Section:Toggle()
			Section:Slider()
			Section:Textbox()
			Section:Keybind()
			Section:Dropdown()
			Section:Colorpicker()
		end
	end
end
