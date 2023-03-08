-- // Library Tables
local library = {}
local utility = {}
local obelus = {
	connections = {}
}
-- // Variables
local uis = game:GetService("UserInputService")
local cre = game:GetService("CoreGui")
-- // Indexing
library.__index = library
-- // Functions
do
	function utility:Create(createInfo)
		local createInfo = createInfo or {}
		--
		if createInfo.Type then
			local instance = Instance.new(createInfo.Type)
			--
			if createInfo.Properties and typeof(createInfo.Properties) == "table" then
				for property, value in pairs(createInfo.Properties) do
					instance[property] = value
				end
			end
			--
			return instance
		end
	end
	--
	function utility:Connection(connectionInfo)
		local connectionInfo = connectionInfo or {}
		--
		if connectionInfo.Type then
			local connection = connectionInfo.Type:Connect(connectionInfo.Callback or function() end)
			--
			obelus.connections[#obelus.connections] = connection
			--
			return connection
		end
	end
	--
	function utility:RemoveConnection(connectionInfo)
		local connectionInfo = connectionInfo or {}
		--
		if connectionInfo.Connection then
			local found = table.find(obelus.connections, connectionInfo.Connection)
			--
			if found then
				connectionInfo.Connection:Disconnect()
				--
				table.remove(obelus.connections, found)
			end
		end
	end
end
-- // Ui Functions
do
	function library:Window(windowInfo)
		-- // Variables
		local info = windowInfo or {}
		local window = {Pages = {}, Dragging = false, Delta = UDim2.new(), Delta2 = Vector3.new()}
		-- // Utilisation
		local screen = utility:Create({Type = "ScreenGui", Properties = {
			Parent = cre,
			DisplayOrder = 8888,
			IgnoreGuiInset = true,
			Name = "obleus",
			ZIndexBehavior = "Global",
			ResetOnSpawn = false
		}})

        game:GetService("UserInputService").InputBegan:Connect(function(k,g)
            if not g then 
                if k.KeyCode == Enum.KeyCode.RightShift then 
                    screen.Enabled = not screen.Enabled 
                end
            end
        end)
		--
		local main = utility:Create({Type = "Frame", Properties = {
			AnchorPoint = Vector2.new(0.5, 0.5),
			BackgroundColor3 = Color3.fromRGB(51, 51, 51),
			BorderColor3 = Color3.fromRGB(0, 0, 0),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Parent = screen,
			Position = UDim2.new(0.5, 0, 0.5, 0),
			Size = UDim2.new(0, 516, 0, 563)
		}})
		--
		local frame = utility:Create({Type = "Frame", Properties = {
			AnchorPoint = Vector2.new(0.5, 0.5),
			BackgroundColor3 = Color3.fromRGB(12, 12, 12),
			BorderSizePixel = 0,
			Parent = main,
			Position = UDim2.new(0.5, 0, 0.5, 0),
			Size = UDim2.new(1, -2, 1, -2),
		}})

		--
		local draggingButton = utility:Create({Type = "TextButton", Properties = {
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Parent = frame,
			Position = UDim2.new(0, 0, 0, 0),
			Size = UDim2.new(1, 0, 0, 24),
			Text = ""
		}})
		--
		local title = utility:Create({Type = "TextLabel", Properties = {
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Parent = frame,
			Position = UDim2.new(0, 9, 0, 6),
			Size = UDim2.new(1, -16, 0, 15),
			Font = "Code",
			RichText = true,
			Text = info.Name or info.name or "obleus",
			TextColor3 = Color3.fromRGB(142, 142, 142),
			TextStrokeTransparency = 0.5,
			TextSize = 13,
			TextXAlignment = "Left"
		}})
		--
		local accent = utility:Create({Type = "Frame", Properties = {
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Parent = frame,
			Position = UDim2.new(0, 8, 0, 22),
			Size = UDim2.new(1, -16, 0, 2)
		}})
		--
		local accentFirst = utility:Create({Type = "Frame", Properties = {
			BackgroundColor3 = Color3.fromRGB(170, 85, 235),
			BorderSizePixel = 0,
			Parent = accent,
			Position = UDim2.new(0, 0, 0, 0),
			Size = UDim2.new(1, 0, 0, 1)
		}})
		--
		local accentSecond = utility:Create({Type = "Frame", Properties = {
			BackgroundColor3 = Color3.fromRGB(101, 51, 141),
			BorderSizePixel = 0,
			Parent = accent,
			Position = UDim2.new(0, 0, 0, 1),
			Size = UDim2.new(1, 0, 0, 1)
		}})
		--
		local tabs = utility:Create({Type = "Frame", Properties = {
			BackgroundColor3 = Color3.fromRGB(1, 1, 1),
			BorderSizePixel = 0,
			Parent = frame,
			Position = UDim2.new(0, 8, 0, 29),
			Size = UDim2.new(1, -16, 0, 30)
		}})
		--
		local tabsInline = utility:Create({Type = "Frame", Properties = {
			BackgroundColor3 = Color3.fromRGB(1, 1, 1),
			BorderSizePixel = 0,
			Parent = tabs,
			Position = UDim2.new(0, 0, 0, 0),
			Size = UDim2.new(1, -1, 1, 0)
		}})
		--
		utility:Create({Type = "UIListLayout", Properties = {
			Padding = UDim.new(0, 0),
			Parent = tabsInline,
			FillDirection = "Horizontal"
		}})
		--
		local pagesHolder = utility:Create({Type = "Frame", Properties = {
			BackgroundColor3 = Color3.fromRGB(51, 51, 51),
			BorderColor3 = Color3.fromRGB(0, 0, 0),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Parent = frame,
			Position = UDim2.new(0, 8, 0, 65),
			Size = UDim2.new(1, -16, 1, -76)
		}})
		--
		local pagesFrame = utility:Create({Type = "Frame", Properties = {
			BackgroundColor3 = Color3.fromRGB(13, 13, 13),
			BorderSizePixel = 0,
			Parent = pagesHolder,
			Position = UDim2.new(0, 1, 0, 1),
			Size = UDim2.new(1, -2, 1, -2)
		}})
		--
		local pagesFolder = utility:Create({Type = "Folder", Properties = {
			Parent = pagesFrame
		}})
		-- // Functions / Connections
		local connection = utility:Connection({Type = draggingButton.InputBegan, Callback = function(Input)
			if not window.Dragging and Input.UserInputType == Enum.UserInputType.MouseButton1 then
				window.Dragging = true
				window.Delta = main.Position
				window.Delta2 = Input.Position
			end
		end})
		--
		local connection2 = utility:Connection({Type = uis.InputEnded, Callback = function(Input)
			if window.Dragging and Input.UserInputType == Enum.UserInputType.MouseButton1 then
				window.Dragging = false
				window.Delta = UDim2.new()
				window.Delta2 = Vector3.new()
			end
		end})
		--
		local connection3 = utility:Connection({Type = uis.InputChanged, Callback = function(Input)
			if window.Dragging then
				local Delta = Input.Position - window.Delta2
				main.Position = UDim2.new(window.Delta.X.Scale, window.Delta.X.Offset + Delta.X, window.Delta.Y.Scale, window.Delta.Y.Offset + Delta.Y)
			end
		end})
		-- // Nested Functions
		function window:RefreshTabs()
			for index, page in pairs(window.Pages) do
				page.Tab.Size = UDim2.new(1 / (#window.Pages), 0, 1, 0)
			end
		end
		--
		function window:Page(pageInfo)
			-- // Variables
			local info = pageInfo or {}
			local page = {Open = false}
			-- // Utilisation
			local tab = utility:Create({Type = "Frame", Properties = {
				BackgroundTransparency = 1,
				BorderSizePixel = 0,
				Parent = tabsInline,
				Size = UDim2.new(1, 0, 1, 0)
			}})
			--
			local tabButton = utility:Create({Type = "TextButton", Properties = {
				BackgroundTransparency = 1,
				BorderSizePixel = 0,
				Parent = tab,
				Position = UDim2.new(0, 0, 0, 0),
				Size = UDim2.new(1, 0, 1, 0)
			}})
			--
			local tabInline = utility:Create({Type = "Frame", Properties = {
				BackgroundColor3 = Color3.fromRGB(41, 41, 41),
				BorderSizePixel = 0,
				Parent = tab,
				Position = UDim2.new(0, 1, 0, 1),
				Size = UDim2.new(1, -1, 1, -2)
			}})
			--
			local tabInlineGradient = utility:Create({Type = "Frame", Properties = {
				BackgroundColor3 = Color3.fromRGB(41, 41, 41),
				BorderSizePixel = 0,
				Parent = tabInline,
				Position = UDim2.new(0, 1, 0, 1),
				Size = UDim2.new(1, -2, 1, -2)
			}})
			--
			local tabGradient = utility:Create({Type = "UIGradient", Properties = {
				Color = ColorSequence.new({ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 255, 255)), ColorSequenceKeypoint.new(1, Color3.fromRGB(100, 100, 100))}),
				Rotation = 90,
				Parent = tabInlineGradient
			}})
			--
			local tabTitle = utility:Create({Type = "TextLabel", Properties = {
				AnchorPoint = Vector2.new(0, 0.5),
				BackgroundTransparency = 1,
				BorderSizePixel = 0,
				Parent = tabInlineGradient,
				Position = UDim2.new(0, 4, 0.5, 0),
				Size = UDim2.new(1, -8, 0, 15),
				Font = "Code",
				RichText = true,
				Text = info.Name or info.name or "tab",
				TextColor3 = Color3.fromRGB(142, 142, 142),
				TextStrokeTransparency = 0.5,
				TextSize = 13,
				TextXAlignment = "Center"
			}})
			--
			local pageHolder = utility:Create({Type = "Frame", Properties = {
				BackgroundTransparency = 1,
				BorderSizePixel = 0,
				Parent = pagesFolder,
				Position = UDim2.new(0, 10, 0, 10),
				Size = UDim2.new(1, -20, 1, -20),
				Visible = false
			}})
			--
			local leftHolder = utility:Create({Type = "Frame", Properties = {
				BackgroundTransparency = 1,
				BorderSizePixel = 0,
				Parent = pageHolder,
				Position = UDim2.new(0, 0, 0 ,0),
				Size = UDim2.new(0.5, -5, 1, 0)
			}})
			--
			local rightHolder = utility:Create({Type = "Frame", Properties = {
				AnchorPoint = Vector2.new(1, 0),
				BackgroundTransparency = 1,
				BorderSizePixel = 0,
				Parent = pageHolder,
				Position = UDim2.new(1, 0, 0 ,0),
				Size = UDim2.new(0.5, -5, 1, 0)
			}})
			-- // Functions / Connections
			utility:Connection({Type = tabButton.MouseButton1Down, Callback = function()
				if not page.open then
					for index, other_page in pairs(window.Pages) do
						if other_page ~= page then
							other_page:Turn(false)
						end
					end
				end
				--
				page:Turn(true)
			end})
			-- // Nested Functions
			function page:Turn(state)
				tabTitle.TextColor3 = state and Color3.fromRGB(170, 85, 235) or Color3.fromRGB(142, 142, 142)
				tabGradient.Color = state and ColorSequence.new({ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 255, 255)), ColorSequenceKeypoint.new(1, Color3.fromRGB(155, 155, 155))}) or ColorSequence.new({ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 255, 255)), ColorSequenceKeypoint.new(1, Color3.fromRGB(100, 100, 100))})
				--
				page.PageHolder.Visible = state
				page.Open = state
			end
			--
			function page:Section(sectionInfo)
				-- // Variables
				local info = sectionInfo or {}
				local section = {}
				-- // Utilisation
				local sectionMain = utility:Create({Type = "Frame", Properties = {
					BackgroundColor3 = Color3.fromRGB(45, 45, 45),
					BorderColor3 = Color3.fromRGB(13, 13, 13),
					BorderMode = "Inset",
					BorderSizePixel = 1,
					Parent = page[((info.Side and info.Side:lower() == "right") or (info.side and info.side:lower() == "right")) and "Right" or "Left"],
					Position = UDim2.new(0, 0, 0, 0),
					Size = UDim2.new(1, 0, 0, (info.Size or info.size or 200) + 4)
				}})
				--
				local sectionFrame = utility:Create({Type = "Frame", Properties = {
					BackgroundColor3 = Color3.fromRGB(19, 19, 19),
					BorderSizePixel = 0,
					Parent = sectionMain,
					Position = UDim2.new(0, 1, 0, 1),
					Size = UDim2.new(1, -2, 1, -2)
				}})
				--
				local sectionTitle = utility:Create({Type = "TextLabel", Properties = {
					AnchorPoint = Vector2.new(0, 0.5),
					BackgroundTransparency = 1,
					BorderSizePixel = 0,
					Parent = sectionMain,
					Position = UDim2.new(0, 13, 0, 0),
					Size = UDim2.new(1, -26, 0, 15),
					Font = "Code",
					RichText = true,
					Text = info.Name or info.name or "new section",
					TextColor3 = Color3.fromRGB(205, 205, 205),
					TextStrokeTransparency = 0.5,
					TextSize = 13,
					TextXAlignment = "Left",
					ZIndex = 2
				}})
				--
				local sectionTitleLine = utility:Create({Type = "Frame", Properties = {
					BackgroundColor3 = Color3.fromRGB(19, 19, 19),
					BorderSizePixel = 0,
					Parent = sectionMain,
					Position = UDim2.new(0, 9, 0, 0),
					Size = UDim2.new(0, sectionTitle.TextBounds.X + 6, 0, 1)
				}})
				--
				local sectionScrolling = utility:Create({Type = "Frame", Properties = {
					BackgroundTransparency = 1,
					BorderSizePixel = 0,
					Parent = sectionMain,
					Position = UDim2.new(0, 1, 0, 1),
					Size = UDim2.new(1, -2, 1, -2),
					Visible = false
				}})
				--
				local sectionScrollingBar = utility:Create({Type = "Frame", Properties = {
					AnchorPoint = Vector2.new(1, 0),
					BackgroundColor3 = Color3.fromRGB(45, 45, 45),
					BorderSizePixel = 0,
					Parent = sectionScrolling,
					Position = UDim2.new(1, 0, 0, 0),
					Size = UDim2.new(0, 5, 1, 0),
					ZIndex = 3
				}})
				--
				local sectionScrollingGradient = utility:Create({Type = "ImageLabel", Properties = {
					AnchorPoint = Vector2.new(0, 1),
					BackgroundTransparency = 1,
					BorderSizePixel = 0,
					Parent = sectionScrolling,
					Position = UDim2.new(0, 0, 1, 0),
					Size = UDim2.new(1, 0, 0, 20),
					ZIndex = 2,
					Image = "rbxassetid://7783533907",
					ImageTransparency = 0,
					ImageColor3 = Color3.fromRGB(19, 19, 19),
					ScaleType = "Stretch"
				}})
				--
				local sectionContentHolder = utility:Create({Type = "ScrollingFrame", Properties = {
					BackgroundTransparency = 1,
					BorderSizePixel = 0,
					Parent = sectionFrame,
					Position = UDim2.new(0, 0, 0, 0),
					Size = UDim2.new(1, 0, 1, 0),
					ZIndex = 4,
					AutomaticCanvasSize = "Y",
					BottomImage = "rbxassetid://7783554086",
					CanvasSize = UDim2.new(0, 0, 0, 0),
					MidImage = "rbxassetid://7783554086",
					ScrollBarImageColor3 = Color3.fromRGB(65, 65, 65),
					ScrollBarThickness = 4,
					TopImage = "rbxassetid://7783554086",
					VerticalScrollBarInset = "ScrollBar"
				}})
				--
				utility:Create({Type = "UIListLayout", Properties = {
					Padding = UDim.new(0, 5),
					Parent = sectionContentHolder,
					FillDirection = "Vertical"
				}})
				--
				local sectionInline = utility:Create({Type = "Frame", Properties = {
					BackgroundColor3 = Color3.fromRGB(19, 19, 19),
					BorderSizePixel = 0,
					Parent = sectionContentHolder,
					Position = UDim2.new(0, 1, 0, 1),
					Size = UDim2.new(1, 0, 0, 10)
				}})
				-- // Functions / Connections
				-- // Nested Functions
				function section:Update()
					if sectionContentHolder.AbsoluteCanvasSize.Y > ((info.Size or info.size or 200) + 4) then
						sectionScrolling.Visible = true
					else
						sectionScrolling.Visible = false
					end
				end
				--
				function section:Label(labelInfo)
					-- // Variables
					local info = labelInfo or {}
					local label = {}
					-- // Utilisation
					local contentHolder = utility:Create({Type = "Frame", Properties = {
						BackgroundTransparency = 1,
						BorderSizePixel = 0,
						Parent = sectionContentHolder,
						Size = UDim2.new(1, 0, 0, 14)
					}})
					--
					local labelTitle = utility:Create({Type = "TextLabel", Properties = {
						AnchorPoint = Vector2.new(0, 0),
						BackgroundTransparency = 1,
						BorderSizePixel = 0,
						Parent = contentHolder,
						Size = UDim2.new(1, -(info.Offset or 36), 1, 0),
						Position = UDim2.new(0, info.Offset or 36, 0, 0),
						Font = "Code",
						RichText = true,
						Text = info.Name or info.name or info.Text or info.text or "new label",
						TextColor3 = Color3.fromRGB(180, 180, 180),
						TextStrokeTransparency = 0.5,
						TextSize = 13,
						TextXAlignment = "Left"
					}})
					-- // Functions / Connections
					-- // Nested Functions
					function label:Remove()
						contentHolder:Remove()
						label = nil
						--
						section:Update()
					end
					-- // Returning + Other
					section:Update()
					--
					return label
				end
				--
				function section:Toggle(toggleInfo)
					-- // Variables
					local info = toggleInfo or {}
					local toggle = {
						state = (info.Default or info.default or info.Def or info.def or false),
						callback = (info.Callback or info.callback or function() end)
					}
					-- // Utilisation
					local contentHolder = utility:Create({Type = "Frame", Properties = {
						BackgroundTransparency = 1,
						BorderSizePixel = 0,
						Parent = sectionContentHolder,
						Size = UDim2.new(1, 0, 0, 14)
					}})
					--
					local toggleButton = utility:Create({Type = "TextButton", Properties = {
						BackgroundTransparency = 1,
						BorderSizePixel = 0,
						Parent = contentHolder,
						Position = UDim2.new(0, 0, 0, 0),
						Size = UDim2.new(1, 0, 1, 0),
						Text = ""
					}})
					--
					local toggleTitle = utility:Create({Type = "TextLabel", Properties = {
						AnchorPoint = Vector2.new(0, 0),
						BackgroundTransparency = 1,
						BorderSizePixel = 0,
						Parent = contentHolder,
						Size = UDim2.new(1, -36, 1, 0),
						Position = UDim2.new(0, 36, 0, 0),
						Font = "Code",
						RichText = true,
						Text = info.Name or info.name or info.Text or info.text or "new toggle",
						TextColor3 = Color3.fromRGB(180, 180, 180),
						TextStrokeTransparency = 0.5,
						TextSize = 13,
						TextXAlignment = "Left"
					}})
					--
					local toggleFrame = utility:Create({Type = "Frame", Properties = {
						BackgroundColor3 = Color3.fromRGB(1, 1, 1),
						BorderSizePixel = 0,
						Parent = contentHolder,
						Position = UDim2.new(0, 16, 0, 2),
						Size = UDim2.new(0, 10, 0, 10)
					}})
					--
					local toggleInlineGradient = utility:Create({Type = "Frame", Properties = {
						BackgroundColor3 = toggle.state and Color3.fromRGB(170, 85, 235) or Color3.fromRGB(63, 63, 63),
						BorderSizePixel = 0,
						Parent = toggleFrame,
						Position = UDim2.new(0, 1, 0, 1),
						Size = UDim2.new(1, -2, 1, -2)
					}})
					--
					local toggleGradient = utility:Create({Type = "UIGradient", Properties = {
						Color = ColorSequence.new({ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 255, 255)), ColorSequenceKeypoint.new(1, Color3.fromRGB(125, 125, 125))}),
						Rotation = 90,
						Parent = toggleInlineGradient
					}})
					-- // Functions / Connections
					local connection = utility:Connection({Type = toggleButton.MouseButton1Down, Callback = function()
						toggle.state = not toggle.state
						toggleInlineGradient.BackgroundColor3 = toggle.state and Color3.fromRGB(170, 85, 235) or Color3.fromRGB(63, 63, 63)
						toggle.callback(toggle.state)
					end})
					-- // Nested Functions
					function toggle:Remove()
						contentHolder:Remove()
						toggle = nil
						--
						utility:RemoveConnection({Connection = connection})
						connection = nil
						--
						section:Update()
					end
					--
					function toggle:Get()
						return toggle.state
					end
					--
					function toggle:Set(value)
						if typeof(value) == "boolean" then
							toggle.state = value
						end
					end
					-- // Returning + Other
					section:Update()
					--
					return toggle
				end
				--
				function section:Button(buttonInfo)
					-- // Variables
					local info = buttonInfo or {}
					local button = {
						callback = (info.Callback or info.callback or function() end)
					}
					-- // Utilisation
					local contentHolder = utility:Create({Type = "Frame", Properties = {
						BackgroundTransparency = 1,
						BorderSizePixel = 0,
						Parent = sectionContentHolder,
						Size = UDim2.new(1, 0, 0, 20)
					}})
					--
					local buttonButton = utility:Create({Type = "TextButton", Properties = {
						BackgroundTransparency = 1,
						BorderSizePixel = 0,
						Parent = contentHolder,
						Position = UDim2.new(0, 0, 0, 0),
						Size = UDim2.new(1, 0, 1, 0),
						Text = ""
					}})
					--
					local buttonFrame = utility:Create({Type = "Frame", Properties = {
						BackgroundColor3 = Color3.fromRGB(45, 45, 45),
						BorderColor3 = Color3.fromRGB(1, 1, 1),
						BorderMode = "Inset",
						BorderSizePixel = 1,
						Parent = contentHolder,
						Position = UDim2.new(0, 16, 0, 0),
						Size = UDim2.new(1, -32, 1, 0)
					}})
					--
					local buttonInline = utility:Create({Type = "Frame", Properties = {
						BackgroundColor3 = Color3.fromRGB(25, 25, 25),
						BorderSizePixel = 0,
						Parent = buttonFrame,
						Position = UDim2.new(0, 1, 0, 1),
						Size = UDim2.new(1, -2, 1, -2)
					}})
					--
					local buttonTitle = utility:Create({Type = "TextLabel", Properties = {
						BackgroundTransparency = 1,
						BorderSizePixel = 0,
						Parent = contentHolder,
						Size = UDim2.new(1, -32, 1, 0),
						Position = UDim2.new(0, 16, 0, 0),
						Font = "Code",
						RichText = true,
						Text = info.Name or info.name or info.Text or info.text or "new button",
						TextColor3 = Color3.fromRGB(180, 180, 180),
						TextStrokeTransparency = 0.5,
						TextSize = 13,
						TextXAlignment = "Center"
					}})
					--
					-- // Functions / Connections
					local connection = utility:Connection({Type = buttonButton.MouseButton1Down, Callback = function()
						button.callback()
					end})
					-- // Nested Functions
					function button:Remove()
						contentHolder:Remove()
						button = nil
						--
						utility:RemoveConnection({Connection = connection})
						connection = nil
						--
						section:Update()
					end
					-- // Returning + Other
					section:Update()
					--
					return button
				end
				--
				function section:Slider(sliderInfo)
					-- // Variables
					local info = sliderInfo or {}
					local slider = {
						state = (info.Default or info.default or info.Def or info.def or 0),
						min = (info.Minimum or info.minimum or info.Min or info.min or 0),
						max = (info.Maximum or info.maximum or info.Max or info.max or 10),
						decimals = (1 / (info.Decimals or info.decimals or info.Tick or info.tick or 0.25)),
						suffix = (info.Suffix or info.suffix or info.Ending or info.ending or ""),
						callback = (info.Callback or info.callback or function() end),
						holding = false
					}
					-- // Utilisation
					local contentHolder = utility:Create({Type = "Frame", Properties = {
						BackgroundTransparency = 1,
						BorderSizePixel = 0,
						Parent = sectionContentHolder,
						Size = UDim2.new(1, 0, 0, (info.Name or info.name or info.Text or info.text) and 24 or 10)
					}})
					--
					local sliderButton = utility:Create({Type = "TextButton", Properties = {
						BackgroundTransparency = 1,
						BorderSizePixel = 0,
						Parent = contentHolder,
						Position = UDim2.new(0, 0, 0, 0),
						Size = UDim2.new(1, 0, 1, 0),
						Text = ""
					}})
					--
					if (info.Name or info.name or info.Text or info.text) then
						local sliderTitle = utility:Create({Type = "TextLabel", Properties = {
							AnchorPoint = Vector2.new(0, 0),
							BackgroundTransparency = 1,
							BorderSizePixel = 0,
							Parent = contentHolder,
							Size = UDim2.new(1, -16, 0, 14),
							Position = UDim2.new(0, 16, 0, 0),
							Font = "Code",
							RichText = true,
							Text = (info.Name or info.name or info.Text or info.text),
							TextColor3 = Color3.fromRGB(180, 180, 180),
							TextStrokeTransparency = 0.5,
							TextSize = 13,
							TextXAlignment = "Left"
						}})
					end
					--
					local sliderFrame = utility:Create({Type = "Frame", Properties = {
						BackgroundColor3 = Color3.fromRGB(1, 1, 1),
						BorderSizePixel = 0,
						Parent = contentHolder,
						Position = UDim2.new(0, 16, 0, (info.Name or info.name or info.Text or info.text) and 14 or 0),
						Size = UDim2.new(1, -32, 0, 10)
					}})
					--
					local sliderInlineGradient = utility:Create({Type = "Frame", Properties = {
						BackgroundColor3 = Color3.fromRGB(63, 63, 63),
						BorderSizePixel = 0,
						Parent = sliderFrame,
						Position = UDim2.new(0, 1, 0, 1),
						Size = UDim2.new(1, -2, 1, -2)
					}})
					--
					local sliderGradient = utility:Create({Type = "UIGradient", Properties = {
						Color = ColorSequence.new({ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 255, 255)), ColorSequenceKeypoint.new(1, Color3.fromRGB(125, 125, 125))}),
						Rotation = 90,
						Parent = sliderInlineGradient
					}})
					--
					local sliderSlideHolder = utility:Create({Type = "Frame", Properties = {
						BackgroundTransparency = 1,
						BorderSizePixel = 0,
						Parent = sliderFrame,
						Position = UDim2.new(0, 1, 0, 1),
						Size = UDim2.new(1, -2, 1, -2)
					}})
					--
					local sliderSlide = utility:Create({Type = "Frame", Properties = {
						BackgroundColor3 = Color3.fromRGB(170, 85, 235),
						BorderSizePixel = 0,
						Parent = sliderSlideHolder,
						Position = UDim2.new(0, 0, 0, 0),
						Size = UDim2.new(0.5, 0, 1, 0)
					}})
					--
					local sliderGradient = utility:Create({Type = "UIGradient", Properties = {
						Color = ColorSequence.new({ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 255, 255)), ColorSequenceKeypoint.new(1, Color3.fromRGB(125, 125, 125))}),
						Rotation = 90,
						Parent = sliderSlide
					}})
					--
					local sliderValue = utility:Create({Type = "TextLabel", Properties = {
						AnchorPoint = Vector2.new(0.5, 0.25),
						BackgroundTransparency = 1,
						BorderSizePixel = 0,
						Parent = sliderSlide,
						Size = UDim2.new(0, 10, 0, 14),
						Position = UDim2.new(1, 0, 0.5, 0),
						Font = "Code",
						RichText = true,
						Text = tostring(slider.state) .. tostring(slider.suffix),
						TextColor3 = Color3.fromRGB(180, 180, 180),
						TextStrokeTransparency = 0.5,
						TextSize = 13,
						TextXAlignment = "Left"
					}})
					-- // Functions / Connections
					local connection = utility:Connection({Type = sliderButton.MouseButton1Down, Callback = function()
						slider.holding = true
						slider:Refresh()
					end})
					--
					local connection2 = utility:Connection({Type = uis.InputEnded, Callback = function()
						slider.holding = false
					end})
					--
					local connection3 = utility:Connection({Type = uis.InputChanged, Callback = function()
						if slider.holding then
							slider:Refresh()
						end
					end})
					-- // Nested Functions
					function slider:Remove()
						contentHolder:Remove()
						slider = nil
						--
						utility:RemoveConnection({Connection = connection})
						connection = nil
						utility:RemoveConnection({Connection = connection2})
						connection2 = nil
						utility:RemoveConnection({Connection = connection3})
						connection3 = nil
						--
						section:Update()
					end
					--
					function slider:Get()
						return slider.state
					end
					--
					function slider:Set(value)
						slider.state = math.clamp(math.round(value * slider.decimals) / slider.decimals, slider.min, slider.max)
						sliderSlide.Size = UDim2.new(1 - ((slider.max - slider.state) / (slider.max - slider.min)), 0, 1, 0)
						sliderValue.Text = tostring(slider.state) .. tostring(slider.suffix)
						pcall(slider.callback, slider.state)
					end
					--
					function slider:Refresh()
						if slider.holding then
							local mouseLocation = uis:GetMouseLocation()
							slider:Set(math.clamp(math.floor((slider.min + (slider.max - slider.min) * (math.clamp(mouseLocation.X - sliderSlide.AbsolutePosition.X, 0, sliderSlideHolder.AbsoluteSize.X) / sliderSlideHolder.AbsoluteSize.X)) * slider.decimals) / slider.decimals, slider.min, slider.max))
						end
					end
					-- // Returning + Other
					section:Update()
					slider:Set(slider.state)
					--
					return slider
				end
				-- // Returning + Other
				return section
			end
			-- // Returning + Other
			page.Tab = tab
			page.PageHolder = pageHolder
			page.Left = leftHolder
			page.Right = rightHolder
			--
			window.Pages[#window.Pages + 1] = page
			window:RefreshTabs()
			--
			return page
		end
		-- // Returning
		return window
	end
end
-- // Main
local window = library:Window({name = "<font color=\"#AA55EB\">elixer.sol</font> | Jul 7 2021"})
--
local aimbot = window:Page({Name = "aimbot"})
local antiaim = window:Page({Name = "antiaim"})
local visuals = window:Page({Name = "visuals"})
local misc = window:Page({Name = "misc"})
local config = window:Page({Name = "config"})
local skins = window:Page({Name = "skins"})
--
local aimbot_section = aimbot:Section({Name = "players", size = 300})
local aimbot_section2 = aimbot:Section({Name = "colored models", Side = "Right"})
--
local label = aimbot_section:Label({Name = "label hello random"})
local label2 = aimbot_section:Label({Name = "with none", Offset = 16})
local toggle = aimbot_section:Toggle({Name = "random toggle", Default = true, Callback = function(val) warn(val) end})
local slider = aimbot_section:Slider({Default = 10, Minimum = -10, Maximum = 30, Decimals = 10, Suffix = "%", Callback = function(val) warn(val) end})
local button = aimbot_section:Button({Name = "random button", Callback = function() warn("clicked") end})
local slider = aimbot_section:Slider({Name = "random slider", Callback = function(val) warn(val) end})
local slider = aimbot_section:Slider({Name = "random slider", Default = 10, Minimum = -10, Maximum = 30, Decimals = 10, Suffix = "%", Callback = function(val) warn(val) end})
local label = aimbot_section:Label({Name = "label hello random"})
local label2 = aimbot_section:Label({Name = "with none", Offset = 16})
local toggle = aimbot_section:Toggle({Name = "random toggle", Default = true, Callback = function(val) warn(val) end})
local slider = aimbot_section:Slider({Default = 10, Minimum = -10, Maximum = 30, Decimals = 10, Suffix = "%", Callback = function(val) warn(val) end})
local button = aimbot_section:Button({Name = "random button", Callback = function() warn("clicked") end})
local slider = aimbot_section:Slider({Name = "random slider", Callback = function(val) warn(val) end})
local slider = aimbot_section:Slider({Name = "random slider", Default = 10, Minimum = -10, Maximum = 30, Decimals = 10, Suffix = "%", Callback = function(val) warn(val) end})
--
aimbot:Turn(true)
-- // Returning
return library, utility, obelus
