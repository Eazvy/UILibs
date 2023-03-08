repeat
    wait()
until game:IsLoaded()

local library
do
    local folder = "specter"

    local services = setmetatable({}, {
        __index = function(_, service)
            if service == "InputService" then
                return game:GetService("UserInputService")
            end

            return game:GetService(service)
        end
    })

    local utility = {}

    function utility.randomstring(length)
        local str = ""
        local chars = string.split("abcdefghijklmnopqrstuvwxyz1234567890", "")

        for i = 1, length do
            local i = math.random(1, #chars)

            if not tonumber(chars[i]) then
                local uppercase = math.random(1, 2) == 2 and true or false
                str = str .. (uppercase and chars[i]:upper() or chars[i])
            else
                str = str .. chars[i]
            end
        end

        return str
    end

    function utility.create(class, properties)
        local obj = Instance.new(class)

        local forced = {
            AutoButtonColor = false
        }

        for prop, v in next, properties do
            obj[prop] = v
        end

        for prop, v in next, forced do
            pcall(function()
                obj[prop] = v
            end)
        end

        obj.Name = utility.randomstring(16)

        return obj
    end

    function utility.dragify(object, speed)
        local start, objectPosition, dragging

        speed = speed or 0

        object.InputBegan:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseButton1 then
                dragging = true
                start = input.Position
                objectPosition = object.Position
            end
        end)

        object.InputEnded:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseButton1 then
                dragging = false
            end
        end)

        services.InputService.InputChanged:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseMovement and dragging then
                utility.tween(object, { speed }, { Position = UDim2.new(objectPosition.X.Scale, objectPosition.X.Offset + (input.Position - start).X, objectPosition.Y.Scale, objectPosition.Y.Offset + (input.Position - start).Y) })
            end
        end)
    end

    function utility.getrgb(color)
        local r = math.floor(color.r * 255)
        local g = math.floor(color.g * 255)
        local b = math.floor(color.b * 255)

        return r, g, b
    end

    function utility.getcenter(sizeX, sizeY)
        return UDim2.new(0.5, -(sizeX / 2), 0.5, -(sizeY / 2))
    end

    function utility.table(tbl)
        tbl = tbl or {}

        local newtbl = {}

        for i, v in next, tbl do
            if type(i) == "string" then
                newtbl[i:lower()] = v
            end
        end

        return setmetatable({}, {
            __newindex = function(_, k, v)
                rawset(newtbl, k:lower(), v)
            end,

            __index = function(_, k)
                return newtbl[k:lower()]
            end
        })
    end

    function utility.tween(obj, info, properties, callback)
        local anim = services.TweenService:Create(obj, TweenInfo.new(unpack(info)), properties)
        anim:Play()

        if callback then
            anim.Completed:Connect(callback)
        end

        return anim
    end

    function utility.makevisible(obj, bool)
        if bool == false then
            local tween

            if not obj.ClassName:find("UI") then
                if obj.ClassName:find("Text") then
                    tween = utility.tween(obj, { 0.2 }, { BackgroundTransparency = obj.BackgroundTransparency + 1, TextTransparency = obj.TextTransparency + 1, TextStrokeTransparency = obj.TextStrokeTransparency + 1 })
                elseif obj.ClassName:find("Image") then
                    tween = utility.tween(obj, { 0.2 }, { BackgroundTransparency = obj.BackgroundTransparency + 1, ImageTransparency = obj.ImageTransparency + 1 })
                elseif obj.ClassName:find("Scrolling") then
                    tween = utility.tween(obj, { 0.2 }, { BackgroundTransparency = obj.BackgroundTransparency + 1, ScrollBarImageTransparency = obj.ScrollBarImageTransparency + 1 })
                else
                    tween = utility.tween(obj, { 0.2 }, { BackgroundTransparency = obj.BackgroundTransparency + 1 })
                end
            end

            tween.Completed:Connect(function()
                obj.Visible = false
            end)

            for _, descendant in next, obj:GetDescendants() do
                if not descendant.ClassName:find("UI") then
                    if descendant.ClassName:find("Text") then
                        utility.tween(descendant, { 0.2 }, { BackgroundTransparency = descendant.BackgroundTransparency + 1, TextTransparency = descendant.TextTransparency + 1, TextStrokeTransparency = descendant.TextStrokeTransparency + 1 })
                    elseif descendant.ClassName:find("Image") then
                        utility.tween(descendant, { 0.2 }, { BackgroundTransparency = descendant.BackgroundTransparency + 1, ImageTransparency = descendant.ImageTransparency + 1 })
                    elseif descendant.ClassName:find("Scrolling") then
                        utility.tween(descendant, { 0.2 }, { BackgroundTransparency = descendant.BackgroundTransparency + 1, ScrollBarImageTransparency = descendant.ScrollBarImageTransparency + 1 })
                    else
                        utility.tween(descendant, { 0.2 }, { BackgroundTransparency = descendant.BackgroundTransparency + 1 })
                    end
                end
            end

            return tween
        elseif bool == true then
            local tween

            if not obj.ClassName:find("UI") then
                obj.Visible = true

                if obj.ClassName:find("Text") then
                    tween = utility.tween(obj, { 0.2 }, { BackgroundTransparency = obj.BackgroundTransparency - 1, TextTransparency = obj.TextTransparency - 1, TextStrokeTransparency = obj.TextStrokeTransparency - 1 })
                elseif obj.ClassName:find("Image") then
                    tween = utility.tween(obj, { 0.2 }, { BackgroundTransparency = obj.BackgroundTransparency - 1, ImageTransparency = obj.ImageTransparency - 1 })
                elseif obj.ClassName:find("Scrolling") then
                    tween = utility.tween(obj, { 0.2 }, { BackgroundTransparency = obj.BackgroundTransparency - 1, ScrollBarImageTransparency = obj.ScrollBarImageTransparency - 1 })
                else
                    tween = utility.tween(obj, { 0.2 }, { BackgroundTransparency = obj.BackgroundTransparency - 1 })
                end
            end

            for _, descendant in next, obj:GetDescendants() do
                if not descendant.ClassName:find("UI") then
                    if descendant.ClassName:find("Text") then
                        utility.tween(descendant, { 0.2 }, { BackgroundTransparency = descendant.BackgroundTransparency - 1, TextTransparency = descendant.TextTransparency - 1, TextStrokeTransparency = descendant.TextStrokeTransparency - 1 })
                    elseif descendant.ClassName:find("Image") then
                        utility.tween(descendant, { 0.2 }, { BackgroundTransparency = descendant.BackgroundTransparency - 1, ImageTransparency = descendant.ImageTransparency - 1 })
                    elseif descendant.ClassName:find("Scrolling") then
                        utility.tween(descendant, { 0.2 }, { BackgroundTransparency = descendant.BackgroundTransparency - 1, ScrollBarImageTransparency = descendant.ScrollBarImageTransparency - 1 })
                    else
                        utility.tween(descendant, { 0.2 }, { BackgroundTransparency = descendant.BackgroundTransparency - 1 })
                    end
                end
            end

            return tween
        end
    end

    function utility.updatescrolling(scrolling, list)
        return list:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
            scrolling.CanvasSize = UDim2.new(0, 0, 0, list.AbsoluteContentSize.Y)
        end)
    end

    function utility.changecolor(color, amount)
        local r, g, b = utility.getrgb(color)
        r = math.clamp(r + amount, 0, 255)
        g = math.clamp(g + amount, 0, 255)
        b = math.clamp(b + amount, 0, 255)

        return Color3.fromRGB(r, g, b)
    end

    function utility.gradient(colors)
        local colortbl = {}

        for i, color in next, colors do
            table.insert(colortbl, ColorSequenceKeypoint.new((i - 1) / (#colors - 1), color))
        end

        return ColorSequence.new(colortbl)
    end

    library = utility.table {
        flags = {},
        toggled = true,
        accent = Color3.fromRGB(162, 109, 184),
        outline = { Color3.fromRGB(121, 66, 254), Color3.fromRGB(223, 57, 137) },
        keybind = Enum.KeyCode.RightShift
    }

    local accentobjects = { gradient = {}, bg = {}, text = {} }

    function library:ChangeAccent(accent)
        library.accent = accent

        for obj, color in next, accentobjects.gradient do
            obj.Color = color(accent)
        end

        for _, obj in next, accentobjects.bg do
            obj.BackgroundColor3 = accent
        end

        for _, obj in next, accentobjects.text do
            obj.TextColor3 = accent
        end
    end

    local outlineobjs = {}

    function library:ChangeOutline(colors)
        for _, obj in next, outlineobjs do
            obj.Color = utility.gradient(colors)
        end
    end

    local gui = utility.create("ScreenGui", {})

    local flags = {}

    function library:SaveConfig(name, universal)
        local configtbl = {}
        local placeid = universal and "universal" or game.PlaceId

        for flag, _ in next, flags do
            local value = library.flags[flag]
            if typeof(value) == "EnumItem" then
                configtbl[flag] = tostring(value)
            elseif typeof(value) == "Color3" then
                configtbl[flag] = { math.floor(value.R * 255), math.floor(value.G * 255), math.floor(value.B * 255) }
            else
                configtbl[flag] = value
            end
        end

        local config = services.HttpService:JSONEncode(configtbl)
        local folderpath = string.format("%s//%s", folder, placeid)

        if not isfolder(folderpath) then
            makefolder(folderpath)
        end

        local filepath = string.format("%s//%s.json", folderpath, name)
        writefile(filepath, config)
    end

    function library:DeleteConfig(name, universal)
        local placeid = universal and "universal" or game.PlaceId

        local folderpath = string.format("%s//%s", folder, placeid)

        if isfolder(folderpath) then
            local folderpath = string.format("%s//%s", folder, placeid)
            local filepath = string.format("%s//%s.json", folderpath, name)

            delfile(filepath)
        end
    end

    function library:LoadConfig(name)
        local placeidfolder = string.format("%s//%s", folder, game.PlaceId)
        local placeidfile = string.format("%s//%s.json", placeidfolder, name)

        local filepath
        do
            if isfolder(placeidfolder) and isfile(placeidfile) then
                filepath = placeidfile
            else
                filepath = string.format("%s//universal//%s.json", folder, name)
            end
        end

        local file = readfile(filepath)
        local config = services.HttpService:JSONDecode(file)

        for flag, v in next, config do
            local func = flags[flag]
            func(v)
        end
    end

    function library:ListConfigs(universal)
        local configs = {}
        local placeidfolder = string.format("%s//%s", folder, game.PlaceId)
        local universalfolder = folder .. "//universal"

        for _, config in next, (isfolder(placeidfolder) and listfiles(placeidfolder) or {}) do
            local name = config:gsub(placeidfolder .. "\\", ""):gsub(".json", "")
            table.insert(configs, name)
        end

        if universal and isfolder(universalfolder) then
            for _, config in next, (isfolder(placeidfolder) and listfiles(placeidfolder) or {}) do
                configs[config:gsub(universalfolder .. "\\", "")] = readfile(config)
            end
        end
        return configs
    end

    function library:Watermark(options)
        local text = table.concat(options, " <font color=\"#D2D2D2\">|</font> ")

        local watermarksize = services.TextService:GetTextSize(text:gsub("<font color=\"#D2D2D2\">", ""):gsub("</font>", ""), 14, Enum.Font.Code, Vector2.new(1000, 1000)).X + 16

        local watermark = utility.create("TextLabel", {
            ZIndex = 2,
            Size = UDim2.new(0, watermarksize, 0, 20),
            BorderColor3 = Color3.fromRGB(50, 50, 50),
            Position = UDim2.new(0, 10, 0, 10),
            BorderSizePixel = 0,
            BackgroundColor3 = Color3.fromRGB(30, 30, 30),
            FontSize = Enum.FontSize.Size14,
            TextStrokeTransparency = 0,
            TextSize = 14,
            RichText = true,
            TextColor3 = library.accent,
            Text = text,
            Font = Enum.Font.Code,
            Parent = gui
        })

        table.insert(accentobjects.text, watermark)

        utility.create("UIPadding", {
            PaddingBottom = UDim.new(0, 2),
            Parent = watermark
        })

        local outline = utility.create("Frame", {
            Size = UDim2.new(1, 2, 1, 4),
            BorderColor3 = Color3.fromRGB(45, 45, 45),
            Position = UDim2.new(0, -1, 0, -1),
            BorderSizePixel = 0,
            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
            Parent = watermark
        })

        utility.create("Frame", {
            ZIndex = 0,
            Size = UDim2.new(1, 2, 1, 2),
            Position = UDim2.new(0, -1, 0, -1),
            BorderSizePixel = 0,
            BackgroundColor3 = Color3.fromRGB(45, 45, 45),
            Parent = outline
        })

        local outlinegradient = utility.create("UIGradient", {
            Rotation = 45,
            Color = utility.gradient(library.outline),
            Parent = outline
        })

        table.insert(outlineobjs, outlinegradient)

        local watermarktypes = utility.table()

        function watermarktypes:Update(options)
            local text = table.concat(options, " <font color=\"#D2D2D2\">|</font> ")
            local watermarksize = services.TextService:GetTextSize(text:gsub("<font color=\"#D2D2D2\">", ""):gsub("</font>", ""), 14, Enum.Font.Code, Vector2.new(1000, 1000)).X + 16

            watermark.Size = UDim2.new(0, watermarksize, 0, 20)
            watermark.Text = text
        end

        local toggling = false
        local toggled = true

        function watermarktypes:Toggle()
            if not toggling then
                toggling = true

                toggled = not toggled
                local tween = utility.makevisible(watermark, toggled)
                tween.Completed:Wait()

                toggling = false
            end
        end

        return watermarktypes
    end

    function library:New(options)
        options = utility.table(options)
        local name = options.name
        local accent = options.accent or library.accent
        local outlinecolor = options.outline or { accent, utility.changecolor(accent, -100) }
        local sizeX = options.sizeX or 550
        local sizeY = options.sizeY or 350

        library.accent = accent
        library.outline = outlinecolor

        local holder = utility.create("Frame", {
            Size = UDim2.new(0, sizeX, 0, 24),
            BackgroundTransparency = 1,
            Position = utility.getcenter(sizeX, sizeY),
            Parent = gui
        })

        local toggling = false

        function library:Toggle()
            if not toggling then
                toggling = true

                library.toggled = not library.toggled
                local tween = utility.makevisible(holder, library.toggled)
                tween.Completed:Wait()

                toggling = false
            end
        end

        utility.dragify(holder)

        local title = utility.create("TextLabel", {
            ZIndex = 5,
            Size = UDim2.new(0, 0, 1, -2),
            BorderColor3 = Color3.fromRGB(50, 50, 50),
            BackgroundTransparency = 1,
            Position = UDim2.new(0, 12, 0, 0),
            BackgroundColor3 = Color3.fromRGB(30, 30, 30),
            FontSize = Enum.FontSize.Size14,
            TextStrokeTransparency = 0,
            TextSize = 14,
            TextColor3 = library.accent,
            Text = name,
            Font = Enum.Font.Code,
            TextXAlignment = Enum.TextXAlignment.Left,
            Parent = holder
        })

        table.insert(accentobjects.text, title)

        local main = utility.create("Frame", {
            ZIndex = 2,
            Size = UDim2.new(1, 0, 0, sizeY),
            BorderColor3 = Color3.fromRGB(27, 42, 53),
            BorderSizePixel = 0,
            BackgroundColor3 = Color3.fromRGB(30, 30, 30),
            Parent = holder
        })

        local outline = utility.create("Frame", {
            Size = UDim2.new(1, 2, 1, 2),
            BorderColor3 = Color3.fromRGB(45, 45, 45),
            Position = UDim2.new(0, -1, 0, -1),
            BorderSizePixel = 0,
            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
            Parent = main
        })

        local outlinegradient = utility.create("UIGradient", {
            Rotation = 45,
            Color = utility.gradient(library.outline),
            Parent = outline
        })

        table.insert(outlineobjs, outlinegradient)

        local border = utility.create("Frame", {
            ZIndex = 0,
            Size = UDim2.new(1, 2, 1, 2),
            Position = UDim2.new(0, -1, 0, -1),
            BorderSizePixel = 0,
            BackgroundColor3 = Color3.fromRGB(45, 45, 45),
            Parent = outline
        })

        local tabs = utility.create("Frame", {
            ZIndex = 4,
            Size = UDim2.new(1, -16, 1, -30),
            BorderColor3 = Color3.fromRGB(50, 50, 50),
            Position = UDim2.new(0, 8, 0, 22),
            BorderSizePixel = 0,
            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
            Parent = main
        })

        utility.create("UIGradient", {
            Rotation = 90,
            Color = ColorSequence.new(Color3.fromRGB(25, 25, 25), Color3.fromRGB(20, 20, 20)),
            Parent = tabs
        })

        utility.create("Frame", {
            ZIndex = 3,
            Size = UDim2.new(1, 2, 1, 2),
            Position = UDim2.new(0, -1, 0, -1),
            BorderSizePixel = 0,
            BackgroundColor3 = Color3.fromRGB(20, 20, 20),
            Parent = tabs
        })

        local tabtoggles = utility.create("Frame", {
            Size = UDim2.new(0, 395, 0, 22),
            BackgroundTransparency = 1,
            Position = UDim2.new(0, 6, 0, 6),
            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
            Parent = tabs
        })

        utility.create("UIListLayout", {
            FillDirection = Enum.FillDirection.Horizontal,
            SortOrder = Enum.SortOrder.LayoutOrder,
            Padding = UDim.new(0, 4),
            Parent = tabtoggles
        })

        local tabframes = utility.create("Frame", {
            ZIndex = 5,
            Size = UDim2.new(1, -12, 1, -35),
            BorderColor3 = Color3.fromRGB(50, 50, 50),
            Position = UDim2.new(0, 6, 0, 29),
            BackgroundColor3 = Color3.fromRGB(30, 30, 30),
            Parent = tabs
        })

        local tabholder = utility.create("Frame", {
            Size = UDim2.new(1, -16, 1, -16),
            BackgroundTransparency = 1,
            Position = UDim2.new(0, 8, 0, 8),
            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
            Parent = tabframes
        })

        local windowtypes = utility.table()

        local pagetoggles = {}

        local switchingtabs = false

        local firsttab
        local currenttab

        function windowtypes:Page(options)
            options = utility.table(options)
            local name = options.name

            local first = #tabtoggles:GetChildren() == 1

            local togglesizeX = math.clamp(services.TextService:GetTextSize(name, 14, Enum.Font.Code, Vector2.new(1000, 1000)).X, 25, math.huge)

            local tabtoggle = utility.create("TextButton", {
                Size = UDim2.new(0, togglesizeX + 18, 1, 0),
                BackgroundTransparency = 1,
                FontSize = Enum.FontSize.Size14,
                TextSize = 14,
                Parent = tabtoggles
            })

            local antiborder = utility.create("Frame", {
                ZIndex = 6,
                Visible = first,
                Size = UDim2.new(1, 0, 0, 1),
                Position = UDim2.new(0, 0, 1, 0),
                BorderSizePixel = 0,
                BackgroundColor3 = Color3.fromRGB(30, 30, 30),
                Parent = tabtoggle
            })

            local selectedglow = utility.create("Frame", {
                ZIndex = 6,
                Size = UDim2.new(1, 0, 0, 1),
                Visible = first,
                BorderColor3 = Color3.fromRGB(50, 50, 50),
                BorderSizePixel = 0,
                BackgroundColor3 = library.accent,
                Parent = tabtoggle
            })

            table.insert(accentobjects.bg, selectedglow)

            utility.create("Frame", {
                ZIndex = 7,
                Size = UDim2.new(1, 0, 0, 1),
                Position = UDim2.new(0, 0, 1, 0),
                BorderSizePixel = 0,
                BackgroundColor3 = Color3.fromRGB(30, 30, 30),
                Parent = selectedglow
            })

            local titleholder = utility.create("Frame", {
                ZIndex = 6,
                Size = UDim2.new(1, 0, 1, first and -1 or -4),
                BorderColor3 = Color3.fromRGB(50, 50, 50),
                Position = UDim2.new(0, 0, 0, first and 1 or 4),
                BorderSizePixel = 0,
                BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                Parent = tabtoggle
            })

            local title = utility.create("TextLabel", {
                ZIndex = 7,
                Size = UDim2.new(1, 0, 1, 0),
                BackgroundTransparency = 1,
                FontSize = Enum.FontSize.Size14,
                TextStrokeTransparency = 0,
                TextSize = 14,
                TextColor3 = first and library.accent or Color3.fromRGB(110, 110, 110),
                Text = name,
                Font = Enum.Font.Code,
                Parent = titleholder
            })

            if first then
                table.insert(accentobjects.text, title)
            end

            local tabglowgradient = utility.create("UIGradient", {
                Rotation = 90,
                Color = first and utility.gradient { utility.changecolor(library.accent, -30), Color3.fromRGB(30, 30, 30) } or utility.gradient { Color3.fromRGB(22, 22, 22), Color3.fromRGB(22, 22, 22) },
                Offset = Vector2.new(0, -0.55),
                Parent = titleholder
            })

            if first then
                accentobjects.gradient[tabglowgradient] = function(color)
                    return utility.gradient { utility.changecolor(color, -30), Color3.fromRGB(30, 30, 30) }
                end
            end

            local tabtoggleborder = utility.create("Frame", {
                ZIndex = 5,
                Size = UDim2.new(1, 2, 1, 2),
                Position = UDim2.new(0, -1, 0, -1),
                BorderSizePixel = 0,
                BackgroundColor3 = Color3.fromRGB(50, 50, 50),
                Parent = title
            })

            pagetoggles[tabtoggle] = {}
            pagetoggles[tabtoggle] = function()
                utility.tween(antiborder, { 0.2 }, { BackgroundTransparency = 1 }, function()
                    antiborder.Visible = false
                end)

                utility.tween(selectedglow, { 0.2 }, { BackgroundTransparency = 1 }, function()
                    selectedglow.Visible = false
                end)

                utility.tween(titleholder, { 0.2 }, { Size = UDim2.new(1, 0, 1, -4), Position = UDim2.new(0, 0, 0, 4) })

                utility.tween(title, { 0.2 }, { TextColor3 = Color3.fromRGB(110, 110, 110) })
                if table.find(accentobjects.text, title) then
                    table.remove(accentobjects.text, table.find(accentobjects.text, title))
                end

                tabglowgradient.Color = utility.gradient { Color3.fromRGB(22, 22, 22), Color3.fromRGB(22, 22, 22) }

                if accentobjects.gradient[tabglowgradient] then
                    accentobjects.gradient[tabglowgradient] = function() end
                end
            end

            local tab = utility.create("Frame", {
                Size = UDim2.new(1, 0, 1, 0),
                BackgroundTransparency = first and 1 or 2,
                Visible = first,
                Parent = tabholder
            })

            if first then
                currenttab = tab
                firsttab = tab
            end

            tab.DescendantAdded:Connect(function(descendant)
                if tab ~= currenttab then
                    task.wait()
                    if not descendant.ClassName:find("UI") then
                        if descendant.ClassName:find("Text") then
                            descendant.TextTransparency = descendant.TextTransparency + 1
                            descendant.TextStrokeTransparency = descendant.TextStrokeTransparency + 1
                        end

                        if descendant.ClassName:find("Scrolling") then
                            descendant.ScrollBarImageTransparency = descendant.ScrollBarImageTransparency + 1
                        end

                        descendant.BackgroundTransparency = descendant.BackgroundTransparency + 1
                    end
                end
            end)

            local column1 = utility.create("ScrollingFrame", {
                Size = UDim2.new(0.5, -5, 1, 0),
                BackgroundTransparency = 1,
                Active = true,
                BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                AutomaticCanvasSize = Enum.AutomaticSize.Y,
                CanvasSize = UDim2.new(0, 0, 0, 123),
                ScrollBarImageColor3 = Color3.fromRGB(0, 0, 0),
                ScrollBarThickness = 0,
                Parent = tab
            })

            local column1list = utility.create("UIListLayout", {
                SortOrder = Enum.SortOrder.LayoutOrder,
                Padding = UDim.new(0, 10),
                Parent = column1
            })

            utility.updatescrolling(column1, column1list)

            local column2 = utility.create("ScrollingFrame", {
                Size = UDim2.new(0.5, -5, 1, 0),
                BackgroundTransparency = 1,
                Position = UDim2.new(0.5, 7, 0, 0),
                Active = true,
                BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                AutomaticCanvasSize = Enum.AutomaticSize.Y,
                CanvasSize = UDim2.new(0, 0, 0, 0),
                ScrollBarImageColor3 = Color3.fromRGB(0, 0, 0),
                ScrollBarThickness = 0,
                Parent = tab
            })

            local column2list = utility.create("UIListLayout", {
                SortOrder = Enum.SortOrder.LayoutOrder,
                Padding = UDim.new(0, 10),
                Parent = column2
            })

            utility.updatescrolling(column2, column2list)

            local function opentab()
                if not switchingtabs then
                    switchingtabs = true

                    currenttab = tab

                    for toggle, close in next, pagetoggles do
                        if toggle ~= tabtoggle then
                            close()
                        end
                    end

                    for _, obj in next, tabholder:GetChildren() do
                        if obj ~= tab and obj.BackgroundTransparency <= 1 then
                            utility.makevisible(obj, false)
                        end
                    end

                    antiborder.Visible = true
                    utility.tween(antiborder, { 0.2 }, { BackgroundTransparency = 0 })

                    selectedglow.Visible = true
                    utility.tween(selectedglow, { 0.2 }, { BackgroundTransparency = 0 })

                    utility.tween(titleholder, { 0.2 }, { Size = UDim2.new(1, 0, 1, -1), Position = UDim2.new(0, 0, 0, 1) })

                    utility.tween(title, { 0.2 }, { TextColor3 = library.accent })

                    table.insert(accentobjects.text, title)

                    tabglowgradient.Color = utility.gradient { utility.changecolor(library.accent, -30), Color3.fromRGB(30, 30, 30) }

                    accentobjects.gradient[tabglowgradient] = function(color)
                        return utility.gradient { utility.changecolor(color, -30), Color3.fromRGB(30, 30, 30) }
                    end

                    tab.Visible = true
                    if tab.BackgroundTransparency > 1 then
                        task.wait(0.2)

                        local tween = utility.makevisible(tab, true)
                        tween.Completed:Wait()
                    end

                    switchingtabs = false
                end
            end

            tabtoggle.MouseButton1Click:Connect(opentab)

            local pagetypes = utility.table()

            function pagetypes:Section(options)
                options = utility.table(options)
                local name = options.name
                local side = options.side or "left"
                local max = options.max or math.huge
                local column = (side:lower() == "left" and column1) or (side:lower() == "right" and column2)

                local sectionholder = utility.create("Frame", {
                    Size = UDim2.new(1, -1, 0, 28),
                    BackgroundTransparency = 1,
                    BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                    Parent = column
                })

                local section = utility.create("Frame", {
                    ZIndex = 6,
                    Size = UDim2.new(1, -2, 1, -2),
                    BorderColor3 = Color3.fromRGB(50, 50, 50),
                    Position = UDim2.new(0, 1, 0, 1),
                    BackgroundColor3 = Color3.fromRGB(22, 22, 22),
                    Parent = sectionholder
                })

                local title = utility.create("TextLabel", {
                    ZIndex = 8,
                    Size = UDim2.new(0, 0, 0, 14),
                    BorderColor3 = Color3.fromRGB(50, 50, 50),
                    BackgroundTransparency = 1,
                    Position = UDim2.new(0, 6, 0, 3),
                    BackgroundColor3 = Color3.fromRGB(30, 30, 30),
                    FontSize = Enum.FontSize.Size14,
                    TextStrokeTransparency = 0,
                    TextSize = 14,
                    TextColor3 = library.accent,
                    Text = name,
                    Font = Enum.Font.Code,
                    TextXAlignment = Enum.TextXAlignment.Left,
                    Parent = section
                })

                table.insert(accentobjects.text, title)

                local glow = utility.create("Frame", {
                    ZIndex = 8,
                    Size = UDim2.new(1, 0, 0, 1),
                    BorderColor3 = Color3.fromRGB(50, 50, 50),
                    BorderSizePixel = 0,
                    BackgroundColor3 = library.accent,
                    Parent = section
                })

                table.insert(accentobjects.bg, glow)

                utility.create("Frame", {
                    ZIndex = 9,
                    Size = UDim2.new(1, 0, 0, 1),
                    Position = UDim2.new(0, 0, 1, 0),
                    BorderSizePixel = 0,
                    BackgroundColor3 = Color3.fromRGB(30, 30, 30),
                    Parent = glow
                })

                local fade = utility.create("Frame", {
                    ZIndex = 7,
                    Size = UDim2.new(1, 0, 0, 20),
                    BorderSizePixel = 0,
                    BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                    Parent = glow
                })

                local fadegradient = utility.create("UIGradient", {
                    Rotation = 90,
                    Color = utility.gradient { utility.changecolor(library.accent, -30), Color3.fromRGB(22, 22, 22) },
                    Offset = Vector2.new(0, -0.55),
                    Parent = fade
                })

                accentobjects.gradient[fadegradient] = function(color)
                    return utility.gradient { utility.changecolor(color, -30), Color3.fromRGB(22, 22, 22) }
                end

                local sectioncontent = utility.create("ScrollingFrame", {
                    ZIndex = 7,
                    Size = UDim2.new(1, -7, 1, -26),
                    BorderColor3 = Color3.fromRGB(27, 42, 53),
                    BackgroundTransparency = 1,
                    Position = UDim2.new(0, 6, 0, 20),
                    Active = true,
                    BorderSizePixel = 0,
                    BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                    CanvasSize = UDim2.new(0, 0, 0, 1),
                    ScrollBarThickness = 2,
                    Parent = section
                })

                local sectionlist = utility.create("UIListLayout", {
                    SortOrder = Enum.SortOrder.LayoutOrder,
                    Padding = UDim.new(0, 2),
                    Parent = sectioncontent
                })

                utility.updatescrolling(sectioncontent, sectionlist)

                local sectiontypes = utility.table()

                function sectiontypes:Label(options)
                    options = utility.table(options)
                    local name = options.name

                    utility.create("TextLabel", {
                        ZIndex = 8,
                        Size = UDim2.new(1, 0, 0, 13),
                        BorderColor3 = Color3.fromRGB(50, 50, 50),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 6, 0, 3),
                        BackgroundColor3 = Color3.fromRGB(30, 30, 30),
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        TextSize = 13,
                        TextColor3 = Color3.fromRGB(210, 210, 210),
                        Text = name,
                        Font = Enum.Font.Code,
                        TextXAlignment = Enum.TextXAlignment.Left,
                        Parent = sectioncontent
                    })

                    if #sectioncontent:GetChildren() - 1 <= max then
                        sectionholder.Size = UDim2.new(1, -1, 0, sectionlist.AbsoluteContentSize.Y + 28)
                    end
                end

                function sectiontypes:Button(options)
                    options = utility.table(options)
                    local name = options.name
                    local callback = options.callback

                    local buttonholder = utility.create("Frame", {
                        Size = UDim2.new(1, -5, 0, 17),
                        BackgroundTransparency = 1,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = sectioncontent
                    })

                    local button = utility.create("TextButton", {
                        ZIndex = 10,
                        Size = UDim2.new(1, -4, 1, -4),
                        BorderColor3 = Color3.fromRGB(40, 40, 40),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 2, 0, 2),
                        BackgroundColor3 = Color3.fromRGB(25, 25, 25),
                        AutoButtonColor = false,
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        TextSize = 13,
                        TextColor3 = Color3.fromRGB(210, 210, 210),
                        Text = name,
                        Font = Enum.Font.Code,
                        Parent = buttonholder
                    })

                    local bg = utility.create("Frame", {
                        ZIndex = 9,
                        Size = UDim2.new(1, 0, 1, 0),
                        BorderColor3 = Color3.fromRGB(40, 40, 40),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = button
                    })

                    local bggradient = utility.create("UIGradient", {
                        Rotation = 90,
                        Color = utility.gradient { Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25) },
                        Parent = bg
                    })

                    local grayborder = utility.create("Frame", {
                        ZIndex = 8,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                        Parent = button
                    })

                    local blackborder = utility.create("Frame", {
                        ZIndex = 7,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                        Parent = grayborder
                    })

                    button.MouseButton1Click:Connect(callback)

                    button.InputBegan:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseButton1 then
                            bggradient.Color = utility.gradient { Color3.fromRGB(45, 45, 45), Color3.fromRGB(35, 35, 35) }
                        end
                    end)

                    button.InputEnded:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseButton1 then
                            bggradient.Color = utility.gradient { Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25) }
                        end
                    end)

                    if #sectioncontent:GetChildren() - 1 <= max then
                        sectionholder.Size = UDim2.new(1, -1, 0, sectionlist.AbsoluteContentSize.Y + 28)
                    end
                end

                function sectiontypes:Toggle(options)
                    options = utility.table(options)
                    local name = options.name
                    local default = options.default
                    local flag = options.pointer
                    local callback = options.callback or function() end

                    local toggleholder = utility.create("TextButton", {
                        Size = UDim2.new(1, -5, 0, 14),
                        BackgroundTransparency = 1,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextSize = 14,
                        TextColor3 = Color3.fromRGB(0, 0, 0),
                        Font = Enum.Font.SourceSans,
                        Parent = sectioncontent
                    })

                    local togglething = utility.create("TextButton", {
                        ZIndex = 9,
                        Size = UDim2.new(1, 0, 0, 14),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        BackgroundTransparency = 1,
                        TextTransparency = 1,
                        Parent = toggleholder
                    })

                    local icon = utility.create("Frame", {
                        ZIndex = 9,
                        Size = UDim2.new(0, 10, 0, 10),
                        BorderColor3 = Color3.fromRGB(40, 40, 40),
                        Position = UDim2.new(0, 2, 0, 2),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = toggleholder
                    })

                    local grayborder = utility.create("Frame", {
                        ZIndex = 8,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                        Parent = icon
                    })

                    utility.create("Frame", {
                        ZIndex = 7,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                        Parent = grayborder
                    })

                    local icongradient = utility.create("UIGradient", {
                        Rotation = 90,
                        Color = utility.gradient { Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25) },
                        Parent = icon
                    })

                    local enablediconholder = utility.create("Frame", {
                        ZIndex = 10,
                        Size = UDim2.new(1, 0, 1, 0),
                        BackgroundTransparency = 1,
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = icon
                    })

                    local enabledicongradient = utility.create("UIGradient", {
                        Rotation = 90,
                        Color = utility.gradient { library.accent, Color3.fromRGB(25, 25, 25) },
                        Parent = enablediconholder
                    })

                    accentobjects.gradient[enabledicongradient] = function(color)
                        return utility.gradient { color, Color3.fromRGB(25, 25, 25) }
                    end

                    local title = utility.create("TextLabel", {
                        ZIndex = 7,
                        Size = UDim2.new(0, 0, 0, 14),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 20, 0, 0),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        TextSize = 13,
                        TextColor3 = Color3.fromRGB(180, 180, 180),
                        Text = name,
                        Font = Enum.Font.Code,
                        TextXAlignment = Enum.TextXAlignment.Left,
                        Parent = toggleholder
                    })

                    local toggled = false

                    if flag then
                        library.flags[flag] = toggled
                    end

                    local function toggle()
                        if not switchingtabs then
                            toggled = not toggled

                            if flag then
                                library.flags[flag] = toggled
                            end

                            callback(toggled)

                            local enabledtransparency = toggled and 0 or 1
                            utility.tween(enablediconholder, { 0.2 }, { Transparency = enabledtransparency })

                            local textcolor = toggled and library.accent or Color3.fromRGB(180, 180, 180)
                            utility.tween(title, { 0.2 }, { TextColor3 = textcolor })

                            if toggled then
                                table.insert(accentobjects.text, title)
                            elseif table.find(accentobjects.text, title) then
                                table.remove(accentobjects.text, table.find(accentobjects.text, title))
                            end
                        end
                    end

                    togglething.MouseButton1Click:Connect(toggle)

                    local function set(bool)
                        if type(bool) == "boolean" and toggled ~= bool then
                            toggle()
                        end
                    end

                    if default then
                        set(default)
                    end

                    if flag then
                        flags[flag] = set
                    end

                    local toggletypes = utility.table()

                    function toggletypes:Toggle(bool)
                        set(bool)
                    end

                    function toggletypes:Colorpicker(newoptions)
                        newoptions = utility.table(newoptions)
                        local name = newoptions.name
                        local default = newoptions.default or Color3.fromRGB(255, 255, 255)
                        local colorpickertype = newoptions.mode
                        local toggleflag = colorpickertype and colorpickertype:lower() == "toggle" and newoptions.togglepointer
                        local togglecallback = colorpickertype and colorpickertype:lower() == "toggle" and newoptions.togglecallback or function() end
                        local flag = newoptions.pointer
                        local callback = newoptions.callback or function() end

                        local colorpickerframe = utility.create("Frame", {
                            ZIndex = 9,
                            Size = UDim2.new(1, -70, 0, 148),
                            Position = UDim2.new(1, -168, 0, 18),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                            Visible = false,
                            Parent = toggleholder
                        })

                        colorpickerframe.DescendantAdded:Connect(function(descendant)
                            if not opened then
                                task.wait()
                                if not descendant.ClassName:find("UI") then
                                    if descendant.ClassName:find("Text") then
                                        descendant.TextTransparency = descendant.TextTransparency + 1
                                        descendant.TextStrokeTransparency = descendant.TextStrokeTransparency + 1
                                    end

                                    if descendant.ClassName:find("Image") then
                                        descendant.ImageTransparency = descendant.ImageTransparency + 1
                                    end

                                    descendant.BackgroundTransparency = descendant.BackgroundTransparency + 1
                                end
                            end
                        end)

                        local bggradient = utility.create("UIGradient", {
                            Rotation = 90,
                            Color = utility.gradient { Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25) },
                            Parent = colorpickerframe
                        })

                        local grayborder = utility.create("Frame", {
                            ZIndex = 8,
                            Size = UDim2.new(1, 2, 1, 2),
                            Position = UDim2.new(0, -1, 0, -1),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                            Parent = colorpickerframe
                        })

                        local blackborder = utility.create("Frame", {
                            ZIndex = 7,
                            Size = UDim2.new(1, 2, 1, 2),
                            Position = UDim2.new(0, -1, 0, -1),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                            Parent = grayborder
                        })

                        local saturationframe = utility.create("ImageLabel", {
                            ZIndex = 12,
                            Size = UDim2.new(0, 128, 0, 100),
                            BorderColor3 = Color3.fromRGB(50, 50, 50),
                            Position = UDim2.new(0, 6, 0, 6),
                            BorderSizePixel = 0,
                            BackgroundColor3 = default,
                            Image = "http://www.roblox.com/asset/?id=8630797271",
                            Parent = colorpickerframe
                        })

                        local grayborder = utility.create("Frame", {
                            ZIndex = 11,
                            Size = UDim2.new(1, 2, 1, 2),
                            Position = UDim2.new(0, -1, 0, -1),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                            Parent = saturationframe
                        })

                        utility.create("Frame", {
                            ZIndex = 10,
                            Size = UDim2.new(1, 2, 1, 2),
                            Position = UDim2.new(0, -1, 0, -1),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                            Parent = grayborder
                        })

                        local saturationpicker = utility.create("Frame", {
                            ZIndex = 13,
                            Size = UDim2.new(0, 2, 0, 2),
                            BorderColor3 = Color3.fromRGB(10, 10, 10),
                            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                            Parent = saturationframe
                        })

                        local hueframe = utility.create("ImageLabel", {
                            ZIndex = 12,
                            Size = UDim2.new(0, 14, 0, 100),
                            Position = UDim2.new(1, -20, 0, 6),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(255, 193, 49),
                            ScaleType = Enum.ScaleType.Crop,
                            Image = "http://www.roblox.com/asset/?id=8630799159",
                            Parent = colorpickerframe
                        })

                        local grayborder = utility.create("Frame", {
                            ZIndex = 11,
                            Size = UDim2.new(1, 2, 1, 2),
                            Position = UDim2.new(0, -1, 0, -1),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                            Parent = hueframe
                        })

                        utility.create("Frame", {
                            ZIndex = 10,
                            Size = UDim2.new(1, 2, 1, 2),
                            Position = UDim2.new(0, -1, 0, -1),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                            Parent = grayborder
                        })

                        local huepicker = utility.create("Frame", {
                            ZIndex = 13,
                            Size = UDim2.new(1, 0, 0, 1),
                            BorderColor3 = Color3.fromRGB(10, 10, 10),
                            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                            Parent = hueframe
                        })

                        local boxholder = utility.create("Frame", {
                            Size = UDim2.new(1, -8, 0, 17),
                            ClipsDescendants = true,
                            Position = UDim2.new(0, 4, 0, 110),
                            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                            Parent = colorpickerframe
                        })

                        local box = utility.create("TextBox", {
                            ZIndex = 13,
                            Size = UDim2.new(1, -4, 1, -4),
                            BackgroundTransparency = 1,
                            Position = UDim2.new(0, 2, 0, 2),
                            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                            FontSize = Enum.FontSize.Size14,
                            TextStrokeTransparency = 0,
                            TextSize = 13,
                            TextColor3 = Color3.fromRGB(210, 210, 210),
                            Text = table.concat({ utility.getrgb(default) }, ", "),
                            PlaceholderText = "R, G, B",
                            Font = Enum.Font.Code,
                            Parent = boxholder
                        })

                        local grayborder = utility.create("Frame", {
                            ZIndex = 11,
                            Size = UDim2.new(1, 2, 1, 2),
                            Position = UDim2.new(0, -1, 0, -1),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                            Parent = box
                        })

                        utility.create("Frame", {
                            ZIndex = 10,
                            Size = UDim2.new(1, 2, 1, 2),
                            Position = UDim2.new(0, -1, 0, -1),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                            Parent = grayborder
                        })

                        local bg = utility.create("Frame", {
                            ZIndex = 12,
                            Size = UDim2.new(1, 0, 1, 0),
                            BorderColor3 = Color3.fromRGB(40, 40, 40),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                            Parent = box
                        })

                        utility.create("UIGradient", {
                            Rotation = 90,
                            Color = utility.gradient { Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25) },
                            Parent = bg
                        })

                        local rainbowtoggleholder = utility.create("TextButton", {
                            Size = UDim2.new(1, -8, 0, 14),
                            BackgroundTransparency = 1,
                            Position = UDim2.new(0, 4, 0, 130),
                            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                            FontSize = Enum.FontSize.Size14,
                            TextSize = 14,
                            TextColor3 = Color3.fromRGB(0, 0, 0),
                            Font = Enum.Font.SourceSans,
                            Parent = colorpickerframe
                        })

                        local toggleicon = utility.create("Frame", {
                            ZIndex = 12,
                            Size = UDim2.new(0, 10, 0, 10),
                            BorderColor3 = Color3.fromRGB(40, 40, 40),
                            Position = UDim2.new(0, 2, 0, 2),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                            Parent = rainbowtoggleholder
                        })

                        local enablediconholder = utility.create("Frame", {
                            ZIndex = 13,
                            Size = UDim2.new(1, 0, 1, 0),
                            BackgroundTransparency = 1,
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                            Parent = toggleicon
                        })

                        local enabledicongradient = utility.create("UIGradient", {
                            Rotation = 90,
                            Color = utility.gradient { library.accent, Color3.fromRGB(25, 25, 25) },
                            Parent = enablediconholder
                        })

                        accentobjects.gradient[enabledicongradient] = function(color)
                            return utility.gradient { color, Color3.fromRGB(25, 25, 25) }
                        end

                        local grayborder = utility.create("Frame", {
                            ZIndex = 11,
                            Size = UDim2.new(1, 2, 1, 2),
                            Position = UDim2.new(0, -1, 0, -1),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                            Parent = toggleicon
                        })

                        utility.create("Frame", {
                            ZIndex = 10,
                            Size = UDim2.new(1, 2, 1, 2),
                            Position = UDim2.new(0, -1, 0, -1),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                            Parent = grayborder
                        })

                        utility.create("UIGradient", {
                            Rotation = 90,
                            Color = utility.gradient { Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25) },
                            Parent = toggleicon
                        })

                        local rainbowtxt = utility.create("TextLabel", {
                            ZIndex = 10,
                            Size = UDim2.new(0, 0, 1, 0),
                            BackgroundTransparency = 1,
                            Position = UDim2.new(0, 20, 0, 0),
                            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                            FontSize = Enum.FontSize.Size14,
                            TextStrokeTransparency = 0,
                            TextSize = 13,
                            TextColor3 = Color3.fromRGB(180, 180, 180),
                            Text = "Rainbow",
                            Font = Enum.Font.Code,
                            TextXAlignment = Enum.TextXAlignment.Left,
                            Parent = rainbowtoggleholder
                        })

                        local colorpicker = utility.create("TextButton", {
                            Size = UDim2.new(1, 0, 0, 14),
                            BackgroundTransparency = 1,
                            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                            FontSize = Enum.FontSize.Size14,
                            TextSize = 14,
                            TextColor3 = Color3.fromRGB(0, 0, 0),
                            Font = Enum.Font.SourceSans,
                            Parent = toggleholder
                        })

                        local icon = utility.create("TextButton", {
                            ZIndex = 9,
                            Size = UDim2.new(0, 18, 0, 10),
                            BorderColor3 = Color3.fromRGB(40, 40, 40),
                            Position = UDim2.new(1, -20, 0, 2),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                            Parent = colorpicker,
                            Text = ""
                        })

                        local grayborder = utility.create("Frame", {
                            ZIndex = 8,
                            Size = UDim2.new(1, 2, 1, 2),
                            Position = UDim2.new(0, -1, 0, -1),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                            Parent = icon
                        })

                        utility.create("Frame", {
                            ZIndex = 7,
                            Size = UDim2.new(1, 2, 1, 2),
                            Position = UDim2.new(0, -1, 0, -1),
                            BorderSizePixel = 0,
                            BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                            Parent = grayborder
                        })

                        local icongradient = utility.create("UIGradient", {
                            Rotation = 90,
                            Color = utility.gradient { default, utility.changecolor(default, -200) },
                            Parent = icon
                        })

                        if #sectioncontent:GetChildren() - 1 <= max then
                            sectionholder.Size = UDim2.new(1, -1, 0, sectionlist.AbsoluteContentSize.Y + 28)
                        end

                        local colorpickertypes = utility.table()

                        local opened = false
                        local opening = false

                        local function opencolorpicker()
                            if not opening then
                                opening = true

                                opened = not opened

                                if opened then
                                    utility.tween(toggleholder, { 0.2 }, { Size = UDim2.new(1, -5, 0, 168) })
                                end

                                local tween = utility.makevisible(colorpickerframe, opened)

                                tween.Completed:Wait()

                                if not opened then
                                    local tween = utility.tween(toggleholder, { 0.2 }, { Size = UDim2.new(1, -5, 0, 16) })
                                    tween.Completed:Wait()
                                end

                                opening = false
                            end
                        end

                        icon.MouseButton1Click:Connect(opencolorpicker)

                        local hue, sat, val = default:ToHSV()

                        local slidinghue = false
                        local slidingsaturation = false

                        local hsv = Color3.fromHSV(hue, sat, val)

                        if flag then
                            library.flags[flag] = default
                        end

                        local function updatehue(input)
                            local sizeY = 1 - math.clamp((input.Position.Y - hueframe.AbsolutePosition.Y) / hueframe.AbsoluteSize.Y, 0, 1)
                            local posY = math.clamp(((input.Position.Y - hueframe.AbsolutePosition.Y) / hueframe.AbsoluteSize.Y) * hueframe.AbsoluteSize.Y, 0, hueframe.AbsoluteSize.Y - 2)
                            huepicker.Position = UDim2.new(0, 0, 0, posY)

                            hue = sizeY
                            hsv = Color3.fromHSV(sizeY, sat, val)

                            box.Text = math.clamp(math.floor((hsv.R * 255) + 0.5), 0, 255) .. ", " .. math.clamp(math.floor((hsv.B * 255) + 0.5), 0, 255) .. ", " .. math.clamp(math.floor((hsv.G * 255) + 0.5), 0, 255)

                            saturationframe.BackgroundColor3 = hsv
                            icon.BackgroundColor3 = hsv

                            if flag then
                                library.flags[flag] = Color3.fromRGB(hsv.r * 255, hsv.g * 255, hsv.b * 255)
                            end

                            callback(Color3.fromRGB(hsv.r * 255, hsv.g * 255, hsv.b * 255))
                        end

                        hueframe.InputBegan:Connect(function(input)
                            if input.UserInputType == Enum.UserInputType.MouseButton1 then
                                slidinghue = true
                                updatehue(input)
                            end
                        end)

                        hueframe.InputEnded:Connect(function(input)
                            if input.UserInputType == Enum.UserInputType.MouseButton1 then
                                slidinghue = false
                            end
                        end)

                        services.InputService.InputChanged:Connect(function(input)
                            if input.UserInputType == Enum.UserInputType.MouseMovement then
                                if slidinghue then
                                    updatehue(input)
                                end
                            end
                        end)

                        local function updatesatval(input)
                            local sizeX = math.clamp((input.Position.X - saturationframe.AbsolutePosition.X) / saturationframe.AbsoluteSize.X, 0, 1)
                            local sizeY = 1 - math.clamp((input.Position.Y - saturationframe.AbsolutePosition.Y) / saturationframe.AbsoluteSize.Y, 0, 1)
                            local posY = math.clamp(((input.Position.Y - saturationframe.AbsolutePosition.Y) / saturationframe.AbsoluteSize.Y) * saturationframe.AbsoluteSize.Y, 0, saturationframe.AbsoluteSize.Y - 4)
                            local posX = math.clamp(((input.Position.X - saturationframe.AbsolutePosition.X) / saturationframe.AbsoluteSize.X) * saturationframe.AbsoluteSize.X, 0, saturationframe.AbsoluteSize.X - 4)

                            saturationpicker.Position = UDim2.new(0, posX, 0, posY)

                            sat = sizeX
                            val = sizeY
                            hsv = Color3.fromHSV(hue, sizeX, sizeY)

                            box.Text = math.clamp(math.floor((hsv.R * 255) + 0.5), 0, 255) .. ", " .. math.clamp(math.floor((hsv.B * 255) + 0.5), 0, 255) .. ", " .. math.clamp(math.floor((hsv.G * 255) + 0.5), 0, 255)

                            saturationframe.BackgroundColor3 = hsv
                            icon.BackgroundColor3 = hsv

                            if flag then
                                library.flags[flag] = Color3.fromRGB(hsv.r * 255, hsv.g * 255, hsv.b * 255)
                            end

                            callback(Color3.fromRGB(hsv.r * 255, hsv.g * 255, hsv.b * 255))
                        end

                        saturationframe.InputBegan:Connect(function(input)
                            if input.UserInputType == Enum.UserInputType.MouseButton1 then
                                slidingsaturation = true
                                updatesatval(input)
                            end
                        end)

                        saturationframe.InputEnded:Connect(function(input)
                            if input.UserInputType == Enum.UserInputType.MouseButton1 then
                                slidingsaturation = false
                            end
                        end)

                        services.InputService.InputChanged:Connect(function(input)
                            if input.UserInputType == Enum.UserInputType.MouseMovement then
                                if slidingsaturation then
                                    updatesatval(input)
                                end
                            end
                        end)

                        local function set(color)
                            if type(color) == "table" then
                                color = Color3.fromRGB(unpack(color))
                            end

                            hue, sat, val = color:ToHSV()
                            hsv = Color3.fromHSV(hue, sat, val)

                            saturationframe.BackgroundColor3 = hsv
                            icon.BackgroundColor3 = hsv
                            saturationpicker.Position = UDim2.new(0, (math.clamp(sat * saturationframe.AbsoluteSize.X, 0, saturationframe.AbsoluteSize.X - 4)), 0, (math.clamp((1 - val) * saturationframe.AbsoluteSize.Y, 0, saturationframe.AbsoluteSize.Y - 4)))
                            huepicker.Position = UDim2.new(0, 0, 0, math.clamp((1 - hue) * saturationframe.AbsoluteSize.Y, 0, saturationframe.AbsoluteSize.Y - 4))

                            box.Text = math.clamp(math.floor((hsv.R * 255) + 0.5), 0, 255) .. ", " .. math.clamp(math.floor((hsv.B * 255) + 0.5), 0, 255) .. ", " .. math.clamp(math.floor((hsv.G * 255) + 0.5), 0, 255)

                            if flag then
                                library.flags[flag] = Color3.fromRGB(hsv.r * 255, hsv.g * 255, hsv.b * 255)
                            end

                            callback(Color3.fromRGB(hsv.r * 255, hsv.g * 255, hsv.b * 255))
                        end

                        local toggled = false

                        local function toggle()
                            if not switchingtabs then
                                toggled = not toggled

                                if toggled then
                                    task.spawn(function()
                                        while toggled do
                                            for i = 0, 1, 0.0015 do
                                                if not toggled then
                                                    return
                                                end

                                                local color = Color3.fromHSV(i, 1, 1)
                                                set(color)

                                                task.wait()
                                            end
                                        end
                                    end)
                                end

                                local enabledtransparency = toggled and 0 or 1
                                utility.tween(enablediconholder, { 0.2 }, { BackgroundTransparency = enabledtransparency })

                                local textcolor = toggled and library.accent or Color3.fromRGB(180, 180, 180)
                                utility.tween(rainbowtxt, { 0.2 }, { TextColor3 = textcolor })

                                if toggled then
                                    table.insert(accentobjects.text, title)
                                elseif table.find(accentobjects.text, title) then
                                    table.remove(accentobjects.text, table.find(accentobjects.text, title))
                                end
                            end
                        end

                        rainbowtoggleholder.MouseButton1Click:Connect(toggle)

                        box.FocusLost:Connect(function()
                            local _, amount = box.Text:gsub(", ", "")

                            if amount == 2 then
                                local values = box.Text:split(", ")
                                local r, g, b = math.clamp(values[1], 0, 255), math.clamp(values[2], 0, 255), math.clamp(values[3], 0, 255)
                                set(Color3.fromRGB(r, g, b))
                            else
                                rgb.Text = math.floor((hsv.r * 255) + 0.5) .. ", " .. math.floor((hsv.g * 255) + 0.5) .. ", " .. math.floor((hsv.b * 255) + 0.5)
                            end
                        end)

                        if default then
                            set(default)
                        end

                        if flag then
                            flags[flag] = set
                        end

                        local colorpickertypes = utility.table()

                        function colorpickertypes:Set(color)
                            set(color)
                        end
                    end

                    if #sectioncontent:GetChildren() - 1 <= max then
                        sectionholder.Size = UDim2.new(1, -1, 0, sectionlist.AbsoluteContentSize.Y + 28)
                    end

                    return toggletypes
                end

                function sectiontypes:Box(options)
                    options = utility.table(options)
                    local name = options.name
                    local placeholder = options.placeholder or ""
                    local default = options.default
                    local boxtype = options.type or "string"
                    local flag = options.pointer
                    local callback = options.callback or function() end

                    local boxholder = utility.create("Frame", {
                        Size = UDim2.new(1, -5, 0, 32),
                        ClipsDescendants = true,
                        BorderColor3 = Color3.fromRGB(27, 42, 53),
                        BackgroundTransparency = 1,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = sectioncontent
                    })

                    utility.create("TextLabel", {
                        ZIndex = 7,
                        Size = UDim2.new(0, 0, 0, 13),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 1, 0, 0),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        TextSize = 13,
                        TextColor3 = Color3.fromRGB(210, 210, 210),
                        Text = name,
                        Font = Enum.Font.Code,
                        TextXAlignment = Enum.TextXAlignment.Left,
                        Parent = boxholder
                    })

                    local box = utility.create("TextBox", {
                        ZIndex = 10,
                        Size = UDim2.new(1, -4, 0, 13),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 2, 0, 17),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        PlaceholderColor3 = Color3.fromRGB(120, 120, 120),
                        TextSize = 13,
                        TextColor3 = Color3.fromRGB(210, 210, 210),
                        Text = "",
                        PlaceholderText = placeholder,
                        Font = Enum.Font.Code,
                        Parent = boxholder
                    })

                    local bg = utility.create("Frame", {
                        ZIndex = 9,
                        Size = UDim2.new(1, 0, 1, 0),
                        BorderColor3 = Color3.fromRGB(40, 40, 40),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = box
                    })

                    local bggradient = utility.create("UIGradient", {
                        Rotation = 90,
                        Color = ColorSequence.new(Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25)),
                        Parent = bg
                    })

                    local grayborder = utility.create("Frame", {
                        ZIndex = 8,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                        Parent = box
                    })

                    local blackborder = utility.create("Frame", {
                        ZIndex = 7,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                        Parent = grayborder
                    })

                    if #sectioncontent:GetChildren() - 1 <= max then
                        sectionholder.Size = UDim2.new(1, -1, 0, sectionlist.AbsoluteContentSize.Y + 28)
                    end

                    if flag then
                        library.flags[flag] = default or ""
                    end

                    local function set(str)
                        if boxtype:lower() == "number" then
                            str = str:gsub("%D+", "")
                        end

                        box.Text = str

                        if flag then
                            library.flags[flag] = str
                        end

                        callback(str)
                    end

                    if default then
                        set(default)
                    end

                    if boxtype:lower() == "number" then
                        box:GetPropertyChangedSignal("Text"):Connect(function()
                            box.Text = box.Text:gsub("%D+", "")
                        end)
                    end

                    box.FocusLost:Connect(function()
                        set(box.Text)
                    end)

                    if flag then
                        flags[flag] = set
                    end

                    local boxtypes = utility.table()

                    function boxtypes:Set(str)
                        set(str)
                    end

                    return boxtypes
                end

                function sectiontypes:Slider(options)
                    options = utility.table(options)
                    local name = options.name
                    local min = options.minimum or 0
                    local slidermax = options.maximum or 100
                    local valuetext = options.value or "[value]/" .. slidermax
                    local increment = options.decimals or 0.5
                    local default = options.default and math.clamp(options.default, min, slidermax) or min
                    local flag = options.pointer
                    local callback = options.callback or function() end

                    local sliderholder = utility.create("Frame", {
                        Size = UDim2.new(1, -5, 0, 28),
                        BackgroundTransparency = 1,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = sectioncontent
                    })

                    local slider = utility.create("Frame", {
                        ZIndex = 10,
                        Size = UDim2.new(1, -4, 0, 9),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 2, 1, -11),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = sliderholder
                    })

                    local grayborder = utility.create("Frame", {
                        ZIndex = 8,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                        Parent = slider
                    })

                    utility.create("Frame", {
                        ZIndex = 7,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                        Parent = grayborder
                    })

                    local bg = utility.create("Frame", {
                        ZIndex = 9,
                        Size = UDim2.new(1, 0, 1, 0),
                        BorderColor3 = Color3.fromRGB(40, 40, 40),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = slider
                    })

                    utility.create("UIGradient", {
                        Rotation = 90,
                        Color = ColorSequence.new(Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25)),
                        Parent = bg
                    })

                    local fill = utility.create("Frame", {
                        ZIndex = 11,
                        Size = UDim2.new((default - min) / (slidermax - min), 0, 1, 0),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = slider
                    })

                    local fillgradient = utility.create("UIGradient", {
                        Rotation = 90,
                        Color = utility.gradient { library.accent, Color3.fromRGB(25, 25, 25) },
                        Parent = fill
                    })

                    accentobjects.gradient[fillgradient] = function(color)
                        return utility.gradient { color, Color3.fromRGB(25, 25, 25) }
                    end

                    local valuelabel = utility.create("TextLabel", {
                        ZIndex = 12,
                        Size = UDim2.new(1, 0, 1, 0),
                        BackgroundTransparency = 1,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        TextSize = 13,
                        TextColor3 = Color3.fromRGB(210, 210, 210),
                        Text = valuetext:gsub("%[value%]", tostring(default)),
                        Font = Enum.Font.Code,
                        Parent = slider
                    })

                    utility.create("TextLabel", {
                        ZIndex = 7,
                        Size = UDim2.new(0, 0, 0, 13),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 1, 0, 0),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        TextSize = 13,
                        TextColor3 = Color3.fromRGB(210, 210, 210),
                        Text = name,
                        Font = Enum.Font.Code,
                        TextXAlignment = Enum.TextXAlignment.Left,
                        Parent = sliderholder
                    })

                    if #sectioncontent:GetChildren() - 1 <= max then
                        sectionholder.Size = UDim2.new(1, -1, 0, sectionlist.AbsoluteContentSize.Y + 28)
                    end

                    local sliding = false

                    local function slide(input)
                        local sizeX = math.clamp((input.Position.X - slider.AbsolutePosition.X) / slider.AbsoluteSize.X, 0, 1)
                        local newincrement = (slidermax / ((slidermax - min) / (increment * 4)))
                        local newsizeX = math.floor(sizeX * (((slidermax - min) / newincrement) * 4)) / (((slidermax - min) / newincrement) * 4)

                        utility.tween(fill, { newincrement / 80 }, { Size = UDim2.new(newsizeX, 0, 1, 0) })

                        local value = math.floor((newsizeX * (slidermax - min) + min) * 20) / 20
                        valuelabel.Text = valuetext:gsub("%[value%]", tostring(value))

                        if flag then
                            library.flags[flag] = value
                        end

                        callback(value)
                    end

                    slider.InputBegan:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseButton1 then
                            sliding = true
                            slide(input)
                        end
                    end)

                    slider.InputEnded:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseButton1 then
                            sliding = false
                        end
                    end)

                    services.InputService.InputChanged:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseMovement then
                            if sliding then
                                slide(input)
                            end
                        end
                    end)

                    local function set(value)
                        value = math.clamp(value, min, slidermax)

                        local sizeX = ((value - min)) / (slidermax - min)
                        local newincrement = (slidermax / ((slidermax - min) / (increment * 4)))

                        local newsizeX = math.floor(sizeX * (((slidermax - min) / newincrement) * 4)) / (((slidermax - min) / newincrement) * 4)
                        value = math.floor((newsizeX * (slidermax - min) + min) * 20) / 20

                        fill.Size = UDim2.new(newsizeX, 0, 1, 0)
                        valuelabel.Text = valuetext:gsub("%[value%]", tostring(value))

                        if flag then
                            library.flags[flag] = value
                        end

                        callback(value)
                    end

                    if default then
                        set(default)
                    end

                    if flag then
                        flags[flag] = set
                    end

                    local slidertypes = utility.table()

                    function slidertypes:Set(value)
                        set(value)
                    end

                    return slidertypes
                end

                function sectiontypes:Dropdown(options)
                    options = utility.table(options)
                    local name = options.name
                    local content = options["options"]
                    local maxoptions = options.maximum and (options.maximum > 1 and options.maximum)
                    local default = options.default or maxoptions and {}
                    local flag = options.pointer
                    local callback = options.callback or function() end

                    if maxoptions then
                        for i, def in next, default do
                            if not table.find(content, def) then
                                table.remove(default, i)
                            end
                        end
                    else
                        if not table.find(content, default) then
                            default = nil
                        end
                    end

                    local defaulttext = default and ((type(default) == "table" and table.concat(default, ", ")) or default)

                    local opened = false

                    local dropdownholder = utility.create("Frame", {
                        Size = UDim2.new(1, -5, 0, 32),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 0, 0, 0),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = sectioncontent
                    })

                    local dropdown = utility.create("TextButton", {
                        ZIndex = 10,
                        Size = UDim2.new(1, -4, 0, 13),
                        BorderColor3 = Color3.fromRGB(40, 40, 40),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 2, 0, 17),
                        BackgroundColor3 = Color3.fromRGB(25, 25, 25),
                        AutoButtonColor = false,
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        TextSize = 13,
                        TextColor3 = default and (defaulttext ~= "" and Color3.fromRGB(210, 210, 210) or Color3.fromRGB(120, 120, 120)) or Color3.fromRGB(120, 120, 120),
                        Text = default and (defaulttext ~= "" and defaulttext or "NONE") or "NONE",
                        Font = Enum.Font.Code,
                        TextXAlignment = Enum.TextXAlignment.Left,
                        Parent = dropdownholder
                    })

                    local bg = utility.create("Frame", {
                        ZIndex = 9,
                        Size = UDim2.new(1, 6, 1, 0),
                        BorderColor3 = Color3.fromRGB(40, 40, 40),
                        Position = UDim2.new(0, -6, 0, 0),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = dropdown
                    })

                    local bggradient = utility.create("UIGradient", {
                        Rotation = 90,
                        Color = ColorSequence.new(Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25)),
                        Parent = bg
                    })

                    local textpadding = utility.create("UIPadding", {
                        PaddingLeft = UDim.new(0, 6),
                        Parent = dropdown
                    })

                    local grayborder = utility.create("Frame", {
                        ZIndex = 8,
                        Size = UDim2.new(1, 8, 1, 2),
                        Position = UDim2.new(0, -7, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                        Parent = dropdown
                    })

                    utility.create("Frame", {
                        ZIndex = 7,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                        Parent = grayborder
                    })

                    local icon = utility.create("TextLabel", {
                        ZIndex = 11,
                        Size = UDim2.new(0, 13, 1, 0),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(1, -13, 0, 0),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size12,
                        TextStrokeTransparency = 0,
                        TextSize = 12,
                        TextColor3 = Color3.fromRGB(210, 210, 210),
                        Text = "+",
                        Font = Enum.Font.Gotham,
                        Parent = dropdown
                    })

                    utility.create("TextLabel", {
                        ZIndex = 7,
                        Size = UDim2.new(0, 0, 0, 13),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 1, 0, 0),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        TextSize = 13,
                        TextColor3 = Color3.fromRGB(210, 210, 210),
                        Text = name,
                        Font = Enum.Font.Code,
                        TextXAlignment = Enum.TextXAlignment.Left,
                        Parent = dropdownholder
                    })

                    local contentframe = utility.create("Frame", {
                        ZIndex = 9,
                        Size = UDim2.new(1, -4, 1, -38),
                        Position = UDim2.new(0, 2, 0, 36),
                        BorderSizePixel = 0,
                        Visible = false,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = dropdownholder
                    })

                    local opened = false
                    contentframe.DescendantAdded:Connect(function(descendant)
                        if not opened then
                            task.wait()
                            if not descendant.ClassName:find("UI") then
                                if descendant.ClassName:find("Text") then
                                    descendant.TextTransparency = descendant.TextTransparency + 1
                                    descendant.TextStrokeTransparency = descendant.TextStrokeTransparency + 1
                                end

                                descendant.BackgroundTransparency = descendant.BackgroundTransparency + 1
                            end
                        end
                    end)

                    local contentframegradient = utility.create("UIGradient", {
                        Rotation = 90,
                        Color = ColorSequence.new(Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25)),
                        Parent = contentframe
                    })

                    local grayborder = utility.create("Frame", {
                        ZIndex = 8,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                        Parent = contentframe
                    })

                    utility.create("Frame", {
                        ZIndex = 7,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                        Parent = grayborder
                    })

                    local dropdowncontent = utility.create("Frame", {
                        Size = UDim2.new(1, -2, 1, -2),
                        Position = UDim2.new(0, 1, 0, 1),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = contentframe
                    })

                    local dropdowncontentlist = utility.create("UIListLayout", {
                        SortOrder = Enum.SortOrder.LayoutOrder,
                        Padding = UDim.new(0, 2),
                        Parent = dropdowncontent
                    })

                    local option = utility.create("TextButton", {
                        ZIndex = 12,
                        Size = UDim2.new(1, 0, 0, 16),
                        BorderColor3 = Color3.fromRGB(50, 50, 50),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 2, 0, 2),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(22, 22, 22),
                        AutoButtonColor = false,
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        TextSize = 13,
                        TextColor3 = Color3.fromRGB(150, 150, 150),
                        Text = "",
                        Font = Enum.Font.Code,
                        TextXAlignment = Enum.TextXAlignment.Left
                    })

                    utility.create("UIPadding", {
                        PaddingLeft = UDim.new(0, 10),
                        Parent = option
                    })

                    if #sectioncontent:GetChildren() - 1 <= max then
                        sectionholder.Size = UDim2.new(1, -1, 0, sectionlist.AbsoluteContentSize.Y + 28)
                    end

                    local opening = false

                    local function opendropdown()
                        if not opening then
                            opening = true

                            opened = not opened

                            utility.tween(icon, { 0.2 }, { TextTransparency = 1, TextStrokeTransparency = 1 }, function()
                                icon.Text = opened and "-" or "+"
                            end)

                            if opened then
                                utility.tween(dropdownholder, { 0.2 }, { Size = UDim2.new(1, -5, 0, dropdowncontentlist.AbsoluteContentSize.Y + 40) })
                            end

                            local tween = utility.makevisible(contentframe, opened)

                            tween.Completed:Wait()

                            if not opened then
                                local tween = utility.tween(dropdownholder, { 0.2 }, { Size = UDim2.new(1, -5, 0, 32) })
                                tween.Completed:Wait()
                            end

                            utility.tween(icon, { 0.2 }, { TextTransparency = 0, TextStrokeTransparency = 0 })

                            opening = false
                        end
                    end

                    dropdown.MouseButton1Click:Connect(opendropdown)

                    local chosen = maxoptions and {}
                    local choseninstances = {}
                    local optioninstances = {}

                    if flag then
                        library.flags[flag] = default
                    end

                    for _, opt in next, content do
                        if not maxoptions then
                            local optionbtn = option:Clone()
                            optionbtn.Parent = dropdowncontent
                            optionbtn.Text = opt

                            optioninstances[opt] = optionbtn

                            if default == opt then
                                chosen = opt
                                optionbtn.BackgroundTransparency = 0
                                optionbtn.TextColor3 = Color3.fromRGB(210, 210, 210)
                            end

                            optionbtn.MouseButton1Click:Connect(function()
                                if chosen ~= opt then
                                    for _, optbtn in next, dropdowncontent:GetChildren() do
                                        if optbtn ~= optionbtn and optbtn:IsA("TextButton") then
                                            utility.tween(optbtn, { 0.2 }, { BackgroundTransparency = 1, TextColor3 = Color3.fromRGB(150, 150, 150) })
                                        end
                                    end

                                    utility.tween(optionbtn, { 0.2 }, { BackgroundTransparency = 0, TextColor3 = Color3.fromRGB(210, 210, 210) })

                                    local tween = utility.tween(dropdown, { 0.2 }, { TextTransparency = 1, TextStrokeTransparency = 1 }, function()
                                        dropdown.Text = opt
                                    end)

                                    chosen = opt

                                    tween.Completed:Wait()

                                    utility.tween(dropdown, { 0.2 }, { TextTransparency = 0, TextStrokeTransparency = 0, TextColor3 = Color3.fromRGB(210, 210, 210) })

                                    if flag then
                                        library.flags[flag] = opt
                                    end

                                    callback(opt)
                                else
                                    utility.tween(optionbtn, { 0.2 }, { BackgroundTransparency = 1, TextColor3 = Color3.fromRGB(150, 150, 150) })

                                    local tween = utility.tween(dropdown, { 0.2 }, { TextTransparency = 1, TextStrokeTransparency = 1 }, function()
                                        dropdown.Text = "NONE"
                                    end)

                                    tween.Completed:Wait()

                                    utility.tween(dropdown, { 0.2 }, { TextTransparency = 0, TextStrokeTransparency = 0, TextColor3 = Color3.fromRGB(150, 150, 150) })
                                    chosen = nil

                                    if flag then
                                        library.flags[flag] = nil
                                    end

                                    callback(nil)
                                end
                            end)
                        else
                            local optionbtn = option:Clone()
                            optionbtn.Parent = dropdowncontent
                            optionbtn.Text = opt

                            optioninstances[opt] = optionbtn

                            if table.find(default, opt) then
                                chosen = opt
                                optionbtn.BackgroundTransparency = 0
                                optionbtn.TextColor3 = Color3.fromRGB(210, 210, 210)
                            end

                            optionbtn.MouseButton1Click:Connect(function()
                                if not table.find(chosen, opt) then
                                    if #chosen >= maxoptions then
                                        table.remove(chosen, 1)
                                        utility.tween(choseninstances[1], { 0.2 }, { BackgroundTransparency = 1, TextColor3 = Color3.fromRGB(150, 150, 150) })
                                        table.remove(choseninstances, 1)
                                    end

                                    utility.tween(optionbtn, { 0.2 }, { BackgroundTransparency = 0, TextColor3 = Color3.fromRGB(210, 210, 210) })

                                    table.insert(chosen, opt)
                                    table.insert(choseninstances, optionbtn)

                                    local tween = utility.tween(dropdown, { 0.2 }, { TextTransparency = 1, TextStrokeTransparency = 1 }, function()
                                        dropdown.Text = table.concat(chosen, ", ")
                                    end)

                                    tween.Completed:Wait()

                                    utility.tween(dropdown, { 0.2 }, { TextTransparency = 0, TextStrokeTransparency = 0, TextColor3 = Color3.fromRGB(210, 210, 210) })

                                    if flag then
                                        library.flags[flag] = chosen
                                    end

                                    callback(chosen)
                                else
                                    utility.tween(optionbtn, { 0.2 }, { BackgroundTransparency = 1, TextColor3 = Color3.fromRGB(150, 150, 150) })

                                    table.remove(chosen, table.find(chosen, opt))
                                    table.remove(choseninstances, table.find(choseninstances, optionbtn))

                                    local tween = utility.tween(dropdown, { 0.2 }, { TextTransparency = 1, TextStrokeTransparency = 1 }, function()
                                        dropdown.Text = table.concat(chosen, ", ") ~= "" and table.concat(chosen, ", ") or "NONE"
                                    end)

                                    tween.Completed:Wait()

                                    utility.tween(dropdown, { 0.2 }, { TextTransparency = 0, TextStrokeTransparency = 0, TextColor3 = table.concat(chosen, ", ") ~= "" and Color3.fromRGB(210, 210, 210) or Color3.fromRGB(150, 150, 150) })

                                    if flag then
                                        library.flags[flag] = chosen
                                    end

                                    callback(chosen)
                                end
                            end)
                        end
                    end

                    local function set(opt)
                        if not maxoptions then
                            if optioninstances[opt] then
                                for _, optbtn in next, dropdowncontent:GetChildren() do
                                    if optbtn ~= optioninstances[opt] and optbtn:IsA("TextButton") then
                                        utility.tween(optbtn, { 0.2 }, { BackgroundTransparency = 1, TextColor3 = Color3.fromRGB(150, 150, 150) })
                                    end
                                end

                                utility.tween(optioninstances[opt], { 0.2 }, { BackgroundTransparency = 0, TextColor3 = Color3.fromRGB(210, 210, 210) })

                                local tween = utility.tween(dropdown, { 0.2 }, { TextTransparency = 1, TextStrokeTransparency = 1 }, function()
                                    dropdown.Text = opt
                                end)

                                chosen = opt

                                tween.Completed:Wait()

                                utility.tween(dropdown, { 0.2 }, { TextTransparency = 0, TextStrokeTransparency = 0, TextColor3 = Color3.fromRGB(210, 210, 210) })

                                if flag then
                                    library.flags[flag] = opt
                                end

                                callback(opt)
                            else
                                for _, optbtn in next, dropdowncontent:GetChildren() do
                                    if optbtn:IsA("TextButton") then
                                        utility.tween(optbtn, { 0.2 }, { BackgroundTransparency = 1, TextColor3 = Color3.fromRGB(150, 150, 150) })
                                    end
                                end

                                local tween = utility.tween(dropdown, { 0.2 }, { TextTransparency = 1, TextStrokeTransparency = 1 }, function()
                                    dropdown.Text = "NONE"
                                end)

                                tween.Completed:Wait()

                                utility.tween(dropdown, { 0.2 }, { TextTransparency = 0, TextStrokeTransparency = 0, TextColor3 = Color3.fromRGB(150, 150, 150) })
                                chosen = nil

                                if flag then
                                    library.flags[flag] = nil
                                end

                                callback(nil)
                            end
                        else
                            table.clear(chosen)
                            table.clear(choseninstances)

                            if not opt then
                                local tween = utility.tween(dropdown, { 0.2 }, { TextTransparency = 1, TextStrokeTransparency = 1 }, function()
                                    dropdown.Text = table.concat(chosen, ", ") ~= "" and table.concat(chosen, ", ") or "NONE"
                                end)

                                tween.Completed:Wait()

                                utility.tween(dropdown, { 0.2 }, { TextTransparency = 0, TextStrokeTransparency = 0, TextColor3 = table.concat(chosen, ", ") ~= "" and Color3.fromRGB(210, 210, 210) or Color3.fromRGB(150, 150, 150) })

                                if flag then
                                    library.flags[flag] = chosen
                                end

                                callback(chosen)
                            else
                                for _, opti in next, opt do
                                    if optioninstances[opti] then
                                        if #chosen >= maxoptions then
                                            table.remove(chosen, 1)
                                            utility.tween(choseninstances[1], { 0.2 }, { BackgroundTransparency = 1, TextColor3 = Color3.fromRGB(150, 150, 150) })
                                            table.remove(choseninstances, 1)
                                        end

                                        utility.tween(optioninstances[opti], { 0.2 }, { BackgroundTransparency = 0, TextColor3 = Color3.fromRGB(210, 210, 210) })

                                        if not table.find(chosen, opti) then
                                            table.insert(chosen, opti)
                                        end

                                        if not table.find(choseninstances, opti) then
                                            table.insert(choseninstances, optioninstances[opti])
                                        end

                                        local tween = utility.tween(dropdown, { 0.2 }, { TextTransparency = 1, TextStrokeTransparency = 1 }, function()
                                            dropdown.Text = table.concat(chosen, ", ")
                                        end)

                                        tween.Completed:Wait()

                                        utility.tween(dropdown, { 0.2 }, { TextTransparency = 0, TextStrokeTransparency = 0, TextColor3 = Color3.fromRGB(210, 210, 210) })

                                        if flag then
                                            library.flags[flag] = chosen
                                        end

                                        callback(chosen)
                                    end
                                end
                            end
                        end
                    end

                    if flag then
                        flags[flag] = set
                    end

                    local dropdowntypes = utility.table()

                    function dropdowntypes:Set(option)
                        set(option)
                    end

                    function dropdowntypes:Refresh(content)
                        if maxoptions then
                            table.clear(chosen)
                        end

                        table.clear(choseninstances)
                        table.clear(optioninstances)

                        for _, optbtn in next, dropdowncontent:GetChildren() do
                            if optbtn:IsA("TextButton") then
                                optbtn:Destroy()
                            end
                        end

                        set()

                        for _, opt in next, content do
                            if not maxoptions then
                                local optionbtn = option:Clone()
                                optionbtn.Parent = dropdowncontent
                                optionbtn.BackgroundTransparency = 2
                                optionbtn.Text = opt
                                optionbtn.TextTransparency = 1
                                optionbtn.TextStrokeTransparency = 1

                                optioninstances[opt] = optionbtn

                                optionbtn.MouseButton1Click:Connect(function()
                                    if chosen ~= opt then
                                        for _, optbtn in next, dropdowncontent:GetChildren() do
                                            if optbtn ~= optionbtn and optbtn:IsA("TextButton") then
                                                utility.tween(optbtn, { 0.2 }, { BackgroundTransparency = 1, TextColor3 = Color3.fromRGB(150, 150, 150) })
                                            end
                                        end

                                        utility.tween(optionbtn, { 0.2 }, { BackgroundTransparency = 0, TextColor3 = Color3.fromRGB(210, 210, 210) })

                                        local tween = utility.tween(dropdown, { 0.2 }, { TextTransparency = 1, TextStrokeTransparency = 1 }, function()
                                            dropdown.Text = opt
                                        end)

                                        chosen = opt

                                        tween.Completed:Wait()

                                        utility.tween(dropdown, { 0.2 }, { TextTransparency = 0, TextStrokeTransparency = 0, TextColor3 = Color3.fromRGB(210, 210, 210) })

                                        if flag then
                                            library.flags[flag] = opt
                                        end

                                        callback(opt)
                                    else
                                        utility.tween(optionbtn, { 0.2 }, { BackgroundTransparency = 1, TextColor3 = Color3.fromRGB(150, 150, 150) })

                                        local tween = utility.tween(dropdown, { 0.2 }, { TextTransparency = 1, TextStrokeTransparency = 1 }, function()
                                            dropdown.Text = "NONE"
                                        end)

                                        tween.Completed:Wait()

                                        utility.tween(dropdown, { 0.2 }, { TextTransparency = 0, TextStrokeTransparency = 0, TextColor3 = Color3.fromRGB(150, 150, 150) })
                                        chosen = nil

                                        if flag then
                                            library.flags[flag] = nil
                                        end

                                        callback(nil)
                                    end
                                end)
                            else
                                local optionbtn = option:Clone()
                                optionbtn.Parent = dropdowncontent
                                optionbtn.Text = opt

                                optioninstances[opt] = optionbtn

                                if table.find(default, opt) then
                                    chosen = opt
                                    optionbtn.BackgroundTransparency = 0
                                    optionbtn.TextColor3 = Color3.fromRGB(210, 210, 210)
                                end

                                optionbtn.MouseButton1Click:Connect(function()
                                    if not table.find(chosen, opt) then
                                        if #chosen >= maxoptions then
                                            table.remove(chosen, 1)
                                            utility.tween(choseninstances[1], { 0.2 }, { BackgroundTransparency = 1, TextColor3 = Color3.fromRGB(150, 150, 150) })
                                            table.remove(choseninstances, 1)
                                        end

                                        utility.tween(optionbtn, { 0.2 }, { BackgroundTransparency = 0, TextColor3 = Color3.fromRGB(210, 210, 210) })

                                        table.insert(chosen, opt)
                                        table.insert(choseninstances, optionbtn)

                                        local tween = utility.tween(dropdown, { 0.2 }, { TextTransparency = 1, TextStrokeTransparency = 1 }, function()
                                            dropdown.Text = table.concat(chosen, ", ")
                                        end)

                                        tween.Completed:Wait()

                                        utility.tween(dropdown, { 0.2 }, { TextTransparency = 0, TextStrokeTransparency = 0, TextColor3 = Color3.fromRGB(210, 210, 210) })

                                        if flag then
                                            library.flags[flag] = chosen
                                        end

                                        callback(chosen)
                                    else
                                        utility.tween(optionbtn, { 0.2 }, { BackgroundTransparency = 1, TextColor3 = Color3.fromRGB(150, 150, 150) })

                                        table.remove(chosen, table.find(chosen, opt))
                                        table.remove(choseninstances, table.find(choseninstances, optionbtn))

                                        local tween = utility.tween(dropdown, { 0.2 }, { TextTransparency = 1, TextStrokeTransparency = 1 }, function()
                                            dropdown.Text = table.concat(chosen, ", ") ~= "" and table.concat(chosen, ", ") or "NONE"
                                        end)

                                        tween.Completed:Wait()

                                        utility.tween(dropdown, { 0.2 }, { TextTransparency = 0, TextStrokeTransparency = 0, TextColor3 = table.concat(chosen, ", ") ~= "" and Color3.fromRGB(210, 210, 210) or Color3.fromRGB(150, 150, 150) })

                                        if flag then
                                            library.flags[flag] = chosen
                                        end

                                        callback(chosen)
                                    end
                                end)
                            end
                        end
                    end

                    return dropdowntypes
                end

                function sectiontypes:Multibox(options)
                    local newoptions = {}
                    for i, v in next, options do
                        newoptions[i:lower()] = v
                    end

                    newoptions.maximum = newoptions.maximum or math.huge
                    return sectiontypes:Dropdown(newoptions)
                end

                function sectiontypes:Keybind(options)
                    options = utility.table(options)
                    local name = options.name
                    local keybindtype = options.mode
                    local default = options.default
                    local toggledefault = keybindtype and keybindtype:lower() == "toggle" and options.toggledefault
                    local toggleflag = keybindtype and keybindtype:lower() == "toggle" and options.togglepointer
                    local togglecallback = keybindtype and keybindtype:lower() == "toggle" and options.togglecallback or function() end
                    local holdflag = keybindtype and keybindtype:lower() == "hold" and options.holdflag
                    local holdcallback = keybindtype and keybindtype:lower() == "hold" and options.holdcallback or function() end
                    local blacklist = options.blacklist or {}
                    local flag = options.pointer
                    local callback = options.callback or function() end

                    table.insert(blacklist, Enum.UserInputType.Focus)

                    local keybindholder = utility.create("TextButton", {
                        Size = UDim2.new(1, -5, 0, 14),
                        BackgroundTransparency = 1,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextSize = 14,
                        TextColor3 = Color3.fromRGB(0, 0, 0),
                        Font = Enum.Font.SourceSans,
                        Parent = sectioncontent
                    })

                    local icon, grayborder, enablediconholder
                    do
                        if keybindtype and keybindtype:lower() == "toggle" then
                            icon = utility.create("Frame", {
                                ZIndex = 9,
                                Size = UDim2.new(0, 10, 0, 10),
                                BorderColor3 = Color3.fromRGB(40, 40, 40),
                                Position = UDim2.new(0, 2, 0, 2),
                                BorderSizePixel = 0,
                                BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                                Parent = keybindholder
                            })

                            grayborder = utility.create("Frame", {
                                ZIndex = 8,
                                Size = UDim2.new(1, 2, 1, 2),
                                Position = UDim2.new(0, -1, 0, -1),
                                BorderSizePixel = 0,
                                BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                                Parent = icon
                            })

                            utility.create("UIGradient", {
                                Rotation = 90,
                                Color = ColorSequence.new(Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25)),
                                Parent = icon
                            })

                            utility.create("Frame", {
                                ZIndex = 7,
                                Size = UDim2.new(1, 2, 1, 2),
                                Position = UDim2.new(0, -1, 0, -1),
                                BorderSizePixel = 0,
                                BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                                Parent = grayborder
                            })

                            enablediconholder = utility.create("Frame", {
                                ZIndex = 10,
                                Size = UDim2.new(1, 0, 1, 0),
                                BackgroundTransparency = 1,
                                BorderSizePixel = 0,
                                BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                                Parent = icon
                            })

                            local enabledicongradient = utility.create("UIGradient", {
                                Rotation = 90,
                                Color = utility.gradient { library.accent, Color3.fromRGB(25, 25, 25) },
                                Parent = enablediconholder
                            })

                            accentobjects.gradient[enabledicongradient] = function(color)
                                return utility.gradient { color, Color3.fromRGB(25, 25, 25) }
                            end
                        end
                    end

                    local title = utility.create("TextLabel", {
                        ZIndex = 7,
                        Size = UDim2.new(0, 0, 1, 0),
                        BackgroundTransparency = 1,
                        Position = keybindtype and keybindtype:lower() == "toggle" and UDim2.new(0, 20, 0, 0) or UDim2.new(0, 1, 0, 0),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        TextSize = 13,
                        TextColor3 = (keybindtype and keybindtype:lower() == "toggle" and Color3.fromRGB(180, 180, 180)) or Color3.fromRGB(210, 210, 210),
                        Text = name,
                        Font = Enum.Font.Code,
                        TextXAlignment = Enum.TextXAlignment.Left,
                        Parent = keybindholder
                    })

                    local keytext = utility.create(keybindtype and keybindtype:lower() == "toggle" and "TextButton" or "TextLabel", {
                        ZIndex = 7,
                        Size = keybindtype and keybindtype:lower() == "toggle" and UDim2.new(0, 45, 1, 0) or UDim2.new(0, 0, 1, 0),
                        BackgroundTransparency = 1,
                        Position = keybindtype and keybindtype:lower() == "toggle" and UDim2.new(1, -45, 0, 0) or UDim2.new(1, 0, 0, 0),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        TextColor3 = Color3.fromRGB(150, 150, 150),
                        Text = "[NONE]",
                        Font = Enum.Font.Code,
                        TextXAlignment = Enum.TextXAlignment.Right,
                        Parent = keybindholder
                    })

                    utility.create("UIPadding", {
                        PaddingBottom = UDim.new(0, 1),
                        Parent = keytext
                    })

                    if #sectioncontent:GetChildren() - 1 <= max then
                        sectionholder.Size = UDim2.new(1, -1, 0, sectionlist.AbsoluteContentSize.Y + 28)
                    end

                    local keys = {
                        [Enum.KeyCode.LeftShift] = "L-SHIFT",
                        [Enum.KeyCode.RightShift] = "R-SHIFT",
                        [Enum.KeyCode.LeftControl] = "L-CTRL",
                        [Enum.KeyCode.RightControl] = "R-CTRL",
                        [Enum.KeyCode.LeftAlt] = "L-ALT",
                        [Enum.KeyCode.RightAlt] = "R-ALT",
                        [Enum.KeyCode.CapsLock] = "CAPSLOCK",
                        [Enum.KeyCode.One] = "1",
                        [Enum.KeyCode.Two] = "2",
                        [Enum.KeyCode.Three] = "3",
                        [Enum.KeyCode.Four] = "4",
                        [Enum.KeyCode.Five] = "5",
                        [Enum.KeyCode.Six] = "6",
                        [Enum.KeyCode.Seven] = "7",
                        [Enum.KeyCode.Eight] = "8",
                        [Enum.KeyCode.Nine] = "9",
                        [Enum.KeyCode.Zero] = "0",
                        [Enum.KeyCode.KeypadOne] = "NUM-1",
                        [Enum.KeyCode.KeypadTwo] = "NUM-2",
                        [Enum.KeyCode.KeypadThree] = "NUM-3",
                        [Enum.KeyCode.KeypadFour] = "NUM-4",
                        [Enum.KeyCode.KeypadFive] = "NUM-5",
                        [Enum.KeyCode.KeypadSix] = "NUM-6",
                        [Enum.KeyCode.KeypadSeven] = "NUM-7",
                        [Enum.KeyCode.KeypadEight] = "NUM-8",
                        [Enum.KeyCode.KeypadNine] = "NUM-9",
                        [Enum.KeyCode.KeypadZero] = "NUM-0",
                        [Enum.KeyCode.Minus] = "-",
                        [Enum.KeyCode.Equals] = "=",
                        [Enum.KeyCode.Tilde] = "~",
                        [Enum.KeyCode.LeftBracket] = "[",
                        [Enum.KeyCode.RightBracket] = "]",
                        [Enum.KeyCode.RightParenthesis] = ")",
                        [Enum.KeyCode.LeftParenthesis] = "(",
                        [Enum.KeyCode.Semicolon] = ",",
                        [Enum.KeyCode.Quote] = "'",
                        [Enum.KeyCode.BackSlash] = "\\",
                        [Enum.KeyCode.Comma] = ",",
                        [Enum.KeyCode.Period] = ".",
                        [Enum.KeyCode.Slash] = "/",
                        [Enum.KeyCode.Asterisk] = "*",
                        [Enum.KeyCode.Plus] = "+",
                        [Enum.KeyCode.Period] = ".",
                        [Enum.KeyCode.Backquote] = "`",
                        [Enum.UserInputType.MouseButton1] = "MOUSE-1",
                        [Enum.UserInputType.MouseButton2] = "MOUSE-2",
                        [Enum.UserInputType.MouseButton3] = "MOUSE-3"
                    }

                    local keychosen
                    local isbinding = false

                    local function startbinding()
                        isbinding = true
                        keytext.Text = "[...]"
                        keytext.TextColor3 = Color3.fromRGB(210, 210, 210)

                        local binding
                        binding = services.InputService.InputBegan:Connect(function(input)
                            local key = keys[input.KeyCode] or keys[input.UserInputType]
                            keytext.Text = "[" .. (key or tostring(input.KeyCode):gsub("Enum.KeyCode.", "")) .. "]"
                            keytext.TextColor3 = Color3.fromRGB(180, 180, 180)
                            keytext.Size = UDim2.new(0, keytext.TextBounds.X, 1, 0)
                            keytext.Position = UDim2.new(1, -keytext.TextBounds.X, 0, 0)

                            if input.UserInputType == Enum.UserInputType.Keyboard then
                                task.wait()
                                if not table.find(blacklist, input.KeyCode) then
                                    keychosen = input.KeyCode

                                    if flag then
                                        library.flags[flag] = input.KeyCode
                                    end

                                    binding:Disconnect()
                                else
                                    keychosen = nil
                                    keytext.TextColor3 = Color3.fromRGB(180, 180, 180)
                                    keytext.Text = "NONE"

                                    if flag then
                                        library.flags[flag] = nil
                                    end

                                    binding:Disconnect()
                                end
                            else
                                if not table.find(blacklist, input.UserInputType) then
                                    keychosen = input.UserInputType

                                    if flag then
                                        library.flags[flag] = input.UserInputType
                                    end

                                    binding:Disconnect()
                                else
                                    keychosen = nil
                                    keytext.TextColor3 = Color3.fromRGB(180, 180, 180)
                                    keytext.Text = "[NONE]"

                                    keytext.Size = UDim2.new(0, keytext.TextBounds.X, 1, 0)
                                    keytext.Position = UDim2.new(1, -keytext.TextBounds.X, 0, 0)

                                    if flag then
                                        library.flags[flag] = nil
                                    end

                                    binding:Disconnect()
                                end
                            end
                        end)
                    end

                    if not keybindtype or keybindtype:lower() == "hold" then
                        keybindholder.MouseButton1Click:Connect(startbinding)
                    else
                        keytext.MouseButton1Click:Connect(startbinding)
                    end

                    local keybindtypes = utility.table()

                    if keybindtype and keybindtype:lower() == "toggle" then
                        local toggled = false

                        if toggleflag then
                            library.flags[toggleflag] = toggled
                        end

                        local function toggle()
                            if not switchingtabs then
                                toggled = not toggled

                                if toggleflag then
                                    library.flags[toggleflag] = toggled
                                end

                                togglecallback(toggled)

                                local enabledtransparency = toggled and 0 or 1
                                utility.tween(enablediconholder, { 0.2 }, { Transparency = enabledtransparency })

                                local textcolor = toggled and library.accent or Color3.fromRGB(180, 180, 180)
                                utility.tween(title, { 0.2 }, { TextColor3 = textcolor })

                                if toggled then
                                    table.insert(accentobjects.text, title)
                                elseif table.find(accentobjects.text, title) then
                                    table.remove(accentobjects.text, table.find(accentobjects.text, title))
                                end
                            end
                        end

                        keybindholder.MouseButton1Click:Connect(toggle)

                        local function set(bool)
                            if type(bool) == "boolean" and toggled ~= bool then
                                toggle()
                            end
                        end

                        function keybindtypes:Toggle(bool)
                            set(bool)
                        end

                        if toggledefault then
                            set(toggledefault)
                        end

                        if toggleflag then
                            flags[toggleflag] = set
                        end

                        services.InputService.InputBegan:Connect(function(input)
                            if input.UserInputType == Enum.UserInputType.Keyboard then
                                if input.KeyCode == keychosen then
                                    toggle()
                                    callback(keychosen)
                                end
                            else
                                if input.UserInputType == keychosen then
                                    toggle()
                                    callback(keychosen)
                                end
                            end
                        end)
                    end

                    if keybindtype and keybindtype:lower() == "hold" then
                        services.InputService.InputBegan:Connect(function(input)
                            if input.UserInputType == Enum.UserInputType.Keyboard then
                                if input.KeyCode == keychosen then
                                    if holdflag then
                                        library.flags[holdflag] = true
                                    end

                                    callback(keychosen)
                                    holdcallback(true)
                                end
                            else
                                if input.UserInputType == keychosen then
                                    if holdflag then
                                        library.flags[holdflag] = true
                                    end

                                    callback(keychosen)
                                    holdcallback(true)
                                end
                            end
                        end)

                        services.InputService.InputEnded:Connect(function(input)
                            if input.UserInputType == Enum.UserInputType.Keyboard then
                                if input.KeyCode == keychosen then
                                    if holdflag then
                                        library.flags[holdflag] = true
                                    end

                                    holdcallback(false)
                                end
                            else
                                if input.UserInputType == keychosen then
                                    if holdflag then
                                        library.flags[holdflag] = true
                                    end

                                    holdcallback(false)
                                end
                            end
                        end)
                    end

                    if not keybindtype then
                        services.InputService.InputBegan:Connect(function(input)
                            if input.UserInputType == Enum.UserInputType.Keyboard then
                                if input.KeyCode == keychosen then
                                    callback(keychosen)
                                end
                            else
                                if input.UserInputType == keychosen then
                                    callback(keychosen)
                                end
                            end
                        end)
                    end

                    local function setkey(newkey)
                        if tostring(newkey):find("Enum.KeyCode.") then
                            newkey = Enum.KeyCode[tostring(newkey):gsub("Enum.KeyCode.", "")]
                        else
                            newkey = Enum.UserInputType[tostring(newkey):gsub("Enum.UserInputType.", "")]
                        end

                        if not table.find(blacklist, newkey) then
                            local key = keys[newkey]
                            local text = "[" .. (keys[newkey] or tostring(newkey):gsub("Enum.KeyCode.", "")) .. "]"
                            local sizeX = services.TextService:GetTextSize(text, 8, Enum.Font.Code, Vector2.new(1000, 1000)).X

                            keytext.Text = text
                            keytext.Size = UDim2.new(0, sizeX, 1, 0)
                            keytext.Position = UDim2.new(1, -sizeX, 0, 0)

                            keytext.TextColor3 = Color3.fromRGB(180, 180, 180)

                            keychosen = newkey

                            if flag then
                                library.flags[flag] = newkey
                            end

                            callback(newkey, true)
                        else
                            keychosen = nil
                            keytext.TextColor3 = Color3.fromRGB(180, 180, 180)
                            keytext.Text = "[NONE]"
                            keytext.Size = UDim2.new(0, keytext.TextBounds.X, 1, 0)
                            keytext.Position = UDim2.new(1, -keytext.TextBounds.X, 0, 0)

                            if flag then
                                library.flags[flag] = nil
                            end

                            callback(newkey, true)
                        end
                    end

                    if default then
                        task.wait()
                        setkey(default)
                    end

                    if flag then
                        flags[flag] = setkey
                    end

                    function keybindtypes:Set(newkey)
                        setkey(newkey)
                    end

                    return keybindtypes
                end

                function sectiontypes:ColorPicker(options)
                    options = utility.table(options)
                    local name = options.name
                    local default = options.default or Color3.fromRGB(255, 255, 255)
                    local colorpickertype = options.mode
                    local toggleflag = colorpickertype and colorpickertype:lower() == "toggle" and options.togglepointer
                    local togglecallback = colorpickertype and colorpickertype:lower() == "toggle" and options.togglecallback or function() end
                    local flag = options.pointer
                    local callback = options.callback or function() end

                    local colorpickerholder = utility.create("Frame", {
                        Size = UDim2.new(1, -5, 0, 14),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 0, 0, 0),
                        Parent = sectioncontent
                    })

                    local enabledcpiconholder
                    do
                        if colorpickertype and colorpickertype:lower() == "toggle" then
                            local togglecpicon = utility.create("Frame", {
                                ZIndex = 9,
                                Size = UDim2.new(0, 10, 0, 10),
                                BorderColor3 = Color3.fromRGB(40, 40, 40),
                                Position = UDim2.new(0, 2, 0, 2),
                                BorderSizePixel = 0,
                                BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                                Parent = colorpickerholder
                            })

                            local grayborder = utility.create("Frame", {
                                ZIndex = 8,
                                Size = UDim2.new(1, 2, 1, 2),
                                Position = UDim2.new(0, -1, 0, -1),
                                BorderSizePixel = 0,
                                BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                                Parent = togglecpicon
                            })

                            utility.create("UIGradient", {
                                Rotation = 90,
                                Color = ColorSequence.new(Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25)),
                                Parent = togglecpicon
                            })

                            utility.create("Frame", {
                                ZIndex = 7,
                                Size = UDim2.new(1, 2, 1, 2),
                                Position = UDim2.new(0, -1, 0, -1),
                                BorderSizePixel = 0,
                                BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                                Parent = grayborder
                            })

                            enabledcpiconholder = utility.create("Frame", {
                                ZIndex = 10,
                                Size = UDim2.new(1, 0, 1, 0),
                                BackgroundTransparency = 1,
                                BorderSizePixel = 0,
                                BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                                Parent = togglecpicon
                            })

                            local enabledicongradient = utility.create("UIGradient", {
                                Rotation = 90,
                                Color = utility.gradient { library.accent, Color3.fromRGB(25, 25, 25) },
                                Parent = enabledcpiconholder
                            })

                            accentobjects.gradient[enabledicongradient] = function(color)
                                return utility.gradient { color, Color3.fromRGB(25, 25, 25) }
                            end
                        end
                    end

                    local colorpickerframe = utility.create("Frame", {
                        ZIndex = 9,
                        Size = UDim2.new(1, -70, 0, 148),
                        Position = UDim2.new(1, -168, 0, 18),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Visible = false,
                        Parent = colorpickerholder
                    })

                    colorpickerframe.DescendantAdded:Connect(function(descendant)
                        if not opened then
                            task.wait()
                            if not descendant.ClassName:find("UI") then
                                if descendant.ClassName:find("Text") then
                                    descendant.TextTransparency = descendant.TextTransparency + 1
                                    descendant.TextStrokeTransparency = descendant.TextStrokeTransparency + 1
                                end

                                if descendant.ClassName:find("Image") then
                                    descendant.ImageTransparency = descendant.ImageTransparency + 1
                                end

                                descendant.BackgroundTransparency = descendant.BackgroundTransparency + 1
                            end
                        end
                    end)

                    local bggradient = utility.create("UIGradient", {
                        Rotation = 90,
                        Color = utility.gradient { Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25) },
                        Parent = colorpickerframe
                    })

                    local grayborder = utility.create("Frame", {
                        ZIndex = 8,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                        Parent = colorpickerframe
                    })

                    local blackborder = utility.create("Frame", {
                        ZIndex = 7,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                        Parent = grayborder
                    })

                    local saturationframe = utility.create("ImageLabel", {
                        ZIndex = 12,
                        Size = UDim2.new(0, 128, 0, 100),
                        BorderColor3 = Color3.fromRGB(50, 50, 50),
                        Position = UDim2.new(0, 6, 0, 6),
                        BorderSizePixel = 0,
                        BackgroundColor3 = default,
                        Image = "http://www.roblox.com/asset/?id=8630797271",
                        Parent = colorpickerframe
                    })

                    local grayborder = utility.create("Frame", {
                        ZIndex = 11,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                        Parent = saturationframe
                    })

                    utility.create("Frame", {
                        ZIndex = 10,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                        Parent = grayborder
                    })

                    local saturationpicker = utility.create("Frame", {
                        ZIndex = 13,
                        Size = UDim2.new(0, 2, 0, 2),
                        BorderColor3 = Color3.fromRGB(10, 10, 10),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = saturationframe
                    })

                    local hueframe = utility.create("ImageLabel", {
                        ZIndex = 12,
                        Size = UDim2.new(0, 14, 0, 100),
                        Position = UDim2.new(1, -20, 0, 6),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 193, 49),
                        ScaleType = Enum.ScaleType.Crop,
                        Image = "http://www.roblox.com/asset/?id=8630799159",
                        Parent = colorpickerframe
                    })

                    local grayborder = utility.create("Frame", {
                        ZIndex = 11,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                        Parent = hueframe
                    })

                    utility.create("Frame", {
                        ZIndex = 10,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                        Parent = grayborder
                    })

                    local huepicker = utility.create("Frame", {
                        ZIndex = 13,
                        Size = UDim2.new(1, 0, 0, 1),
                        BorderColor3 = Color3.fromRGB(10, 10, 10),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = hueframe
                    })

                    local boxholder = utility.create("Frame", {
                        Size = UDim2.new(1, -8, 0, 17),
                        ClipsDescendants = true,
                        Position = UDim2.new(0, 4, 0, 110),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = colorpickerframe
                    })

                    local box = utility.create("TextBox", {
                        ZIndex = 13,
                        Size = UDim2.new(1, -4, 1, -4),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 2, 0, 2),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        TextSize = 13,
                        TextColor3 = Color3.fromRGB(210, 210, 210),
                        Text = table.concat({ utility.getrgb(default) }, ", "),
                        PlaceholderText = "R, G, B",
                        Font = Enum.Font.Code,
                        Parent = boxholder
                    })

                    local grayborder = utility.create("Frame", {
                        ZIndex = 11,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                        Parent = box
                    })

                    utility.create("Frame", {
                        ZIndex = 10,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                        Parent = grayborder
                    })

                    local bg = utility.create("Frame", {
                        ZIndex = 12,
                        Size = UDim2.new(1, 0, 1, 0),
                        BorderColor3 = Color3.fromRGB(40, 40, 40),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = box
                    })

                    utility.create("UIGradient", {
                        Rotation = 90,
                        Color = utility.gradient { Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25) },
                        Parent = bg
                    })

                    local toggleholder = utility.create("TextButton", {
                        Size = UDim2.new(1, -8, 0, 14),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 4, 0, 130),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextSize = 14,
                        TextColor3 = Color3.fromRGB(0, 0, 0),
                        Font = Enum.Font.SourceSans,
                        Parent = colorpickerframe
                    })

                    local toggleicon = utility.create("Frame", {
                        ZIndex = 12,
                        Size = UDim2.new(0, 10, 0, 10),
                        BorderColor3 = Color3.fromRGB(40, 40, 40),
                        Position = UDim2.new(0, 2, 0, 2),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = toggleholder
                    })

                    local enablediconholder = utility.create("Frame", {
                        ZIndex = 13,
                        Size = UDim2.new(1, 0, 1, 0),
                        BackgroundTransparency = 1,
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = toggleicon
                    })

                    local enabledicongradient = utility.create("UIGradient", {
                        Rotation = 90,
                        Color = utility.gradient { library.accent, Color3.fromRGB(25, 25, 25) },
                        Parent = enablediconholder
                    })

                    accentobjects.gradient[enabledicongradient] = function(color)
                        return utility.gradient { color, Color3.fromRGB(25, 25, 25) }
                    end

                    local grayborder = utility.create("Frame", {
                        ZIndex = 11,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                        Parent = toggleicon
                    })

                    utility.create("Frame", {
                        ZIndex = 10,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                        Parent = grayborder
                    })

                    utility.create("UIGradient", {
                        Rotation = 90,
                        Color = utility.gradient { Color3.fromRGB(35, 35, 35), Color3.fromRGB(25, 25, 25) },
                        Parent = toggleicon
                    })

                    local rainbowtxt = utility.create("TextLabel", {
                        ZIndex = 10,
                        Size = UDim2.new(0, 0, 1, 0),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 20, 0, 0),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        TextSize = 13,
                        TextColor3 = Color3.fromRGB(180, 180, 180),
                        Text = "Rainbow",
                        Font = Enum.Font.Code,
                        TextXAlignment = Enum.TextXAlignment.Left,
                        Parent = toggleholder
                    })

                    local colorpicker = utility.create("TextButton", {
                        Size = UDim2.new(1, 0, 0, 14),
                        BackgroundTransparency = 1,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextSize = 14,
                        TextColor3 = Color3.fromRGB(0, 0, 0),
                        Font = Enum.Font.SourceSans,
                        Parent = colorpickerholder
                    })

                    local icon = utility.create(colorpickertype and colorpickertype:lower() == "toggle" and "TextButton" or "Frame", {
                        ZIndex = 9,
                        Size = UDim2.new(0, 18, 0, 10),
                        BorderColor3 = Color3.fromRGB(40, 40, 40),
                        Position = UDim2.new(1, -20, 0, 2),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        Parent = colorpicker
                    })

                    if colorpickertype and colorpickertype:lower() == "toggle" then
                        icon.Text = ""
                    end

                    local grayborder = utility.create("Frame", {
                        ZIndex = 8,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(40, 40, 40),
                        Parent = icon
                    })

                    utility.create("Frame", {
                        ZIndex = 7,
                        Size = UDim2.new(1, 2, 1, 2),
                        Position = UDim2.new(0, -1, 0, -1),
                        BorderSizePixel = 0,
                        BackgroundColor3 = Color3.fromRGB(10, 10, 10),
                        Parent = grayborder
                    })

                    local icongradient = utility.create("UIGradient", {
                        Rotation = 90,
                        Color = utility.gradient { default, utility.changecolor(default, -200) },
                        Parent = icon
                    })

                    local title = utility.create("TextLabel", {
                        ZIndex = 7,
                        Size = UDim2.new(0, 0, 0, 14),
                        BackgroundTransparency = 1,
                        Position = colorpickertype and colorpickertype:lower() == "toggle" and UDim2.new(0, 20, 0, 0) or UDim2.new(0, 1, 0, 0),
                        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                        FontSize = Enum.FontSize.Size14,
                        TextStrokeTransparency = 0,
                        TextSize = 13,
                        TextColor3 = Color3.fromRGB(210, 210, 210),
                        Text = name,
                        Font = Enum.Font.Code,
                        TextXAlignment = Enum.TextXAlignment.Left,
                        Parent = colorpicker
                    })

                    if #sectioncontent:GetChildren() - 1 <= max then
                        sectionholder.Size = UDim2.new(1, -1, 0, sectionlist.AbsoluteContentSize.Y + 28)
                    end

                    local colorpickertypes = utility.table()

                    if colorpickertype and colorpickertype:lower() == "toggle" then
                        local toggled = false

                        if toggleflag then
                            library.flags[toggleflag] = toggled
                        end

                        local function toggle()
                            if not switchingtabs then
                                toggled = not toggled

                                if toggleflag then
                                    library.flags[toggleflag] = toggled
                                end

                                togglecallback(toggled)

                                local enabledtransparency = toggled and 0 or 1
                                utility.tween(enabledcpiconholder, { 0.2 }, { BackgroundTransparency = enabledtransparency })

                                local textcolor = toggled and library.accent or Color3.fromRGB(180, 180, 180)
                                utility.tween(title, { 0.2 }, { TextColor3 = textcolor })

                                if toggled then
                                    table.insert(accentobjects.text, title)
                                elseif table.find(accentobjects.text, title) then
                                    table.remove(accentobjects.text, table.find(accentobjects.text, title))
                                end
                            end
                        end

                        colorpicker.MouseButton1Click:Connect(toggle)

                        local function set(bool)
                            if type(bool) == "boolean" and toggled ~= bool then
                                toggle()
                            end
                        end

                        function colorpickertypes:Toggle(bool)
                            set(bool)
                        end

                        if toggledefault then
                            set(toggledefault)
                        end

                        if toggleflag then
                            flags[toggleflag] = set
                        end
                    end

                    local opened = false
                    local opening = false

                    local function opencolorpicker()
                        if not opening then
                            opening = true

                            opened = not opened

                            if opened then
                                utility.tween(colorpickerholder, { 0.2 }, { Size = UDim2.new(1, -5, 0, 168) })
                            end

                            local tween = utility.makevisible(colorpickerframe, opened)

                            tween.Completed:Wait()

                            if not opened then
                                local tween = utility.tween(colorpickerholder, { 0.2 }, { Size = UDim2.new(1, -5, 0, 16) })
                                tween.Completed:Wait()
                            end

                            opening = false
                        end
                    end

                    if colorpickertype and colorpickertype:lower() == "toggle" then
                        icon.MouseButton1Click:Connect(opencolorpicker)
                    else
                        colorpicker.MouseButton1Click:Connect(opencolorpicker)
                    end

                    local hue, sat, val = default:ToHSV()

                    local slidinghue = false
                    local slidingsaturation = false

                    local hsv = Color3.fromHSV(hue, sat, val)

                    if flag then
                        library.flags[flag] = default
                    end

                    local function updatehue(input)
                        local sizeY = 1 - math.clamp((input.Position.Y - hueframe.AbsolutePosition.Y) / hueframe.AbsoluteSize.Y, 0, 1)
                        local posY = math.clamp(((input.Position.Y - hueframe.AbsolutePosition.Y) / hueframe.AbsoluteSize.Y) * hueframe.AbsoluteSize.Y, 0, hueframe.AbsoluteSize.Y - 2)
                        huepicker.Position = UDim2.new(0, 0, 0, posY)

                        hue = sizeY
                        hsv = Color3.fromHSV(sizeY, sat, val)

                        box.Text = math.clamp(math.floor((hsv.R * 255) + 0.5), 0, 255) .. ", " .. math.clamp(math.floor((hsv.B * 255) + 0.5), 0, 255) .. ", " .. math.clamp(math.floor((hsv.G * 255) + 0.5), 0, 255)

                        saturationframe.BackgroundColor3 = hsv
                        icon.BackgroundColor3 = hsv

                        if flag then
                            library.flags[flag] = Color3.fromRGB(hsv.r * 255, hsv.g * 255, hsv.b * 255)
                        end

                        callback(Color3.fromRGB(hsv.r * 255, hsv.g * 255, hsv.b * 255))
                    end

                    hueframe.InputBegan:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseButton1 then
                            slidinghue = true
                            updatehue(input)
                        end
                    end)

                    hueframe.InputEnded:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseButton1 then
                            slidinghue = false
                        end
                    end)

                    services.InputService.InputChanged:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseMovement then
                            if slidinghue then
                                updatehue(input)
                            end
                        end
                    end)

                    local function updatesatval(input)
                        local sizeX = math.clamp((input.Position.X - saturationframe.AbsolutePosition.X) / saturationframe.AbsoluteSize.X, 0, 1)
                        local sizeY = 1 - math.clamp((input.Position.Y - saturationframe.AbsolutePosition.Y) / saturationframe.AbsoluteSize.Y, 0, 1)
                        local posY = math.clamp(((input.Position.Y - saturationframe.AbsolutePosition.Y) / saturationframe.AbsoluteSize.Y) * saturationframe.AbsoluteSize.Y, 0, saturationframe.AbsoluteSize.Y - 4)
                        local posX = math.clamp(((input.Position.X - saturationframe.AbsolutePosition.X) / saturationframe.AbsoluteSize.X) * saturationframe.AbsoluteSize.X, 0, saturationframe.AbsoluteSize.X - 4)

                        saturationpicker.Position = UDim2.new(0, posX, 0, posY)

                        sat = sizeX
                        val = sizeY
                        hsv = Color3.fromHSV(hue, sizeX, sizeY)

                        box.Text = math.clamp(math.floor((hsv.R * 255) + 0.5), 0, 255) .. ", " .. math.clamp(math.floor((hsv.B * 255) + 0.5), 0, 255) .. ", " .. math.clamp(math.floor((hsv.G * 255) + 0.5), 0, 255)

                        saturationframe.BackgroundColor3 = hsv
                        icon.BackgroundColor3 = hsv

                        if flag then
                            library.flags[flag] = Color3.fromRGB(hsv.r * 255, hsv.g * 255, hsv.b * 255)
                        end

                        callback(Color3.fromRGB(hsv.r * 255, hsv.g * 255, hsv.b * 255))
                    end

                    saturationframe.InputBegan:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseButton1 then
                            slidingsaturation = true
                            updatesatval(input)
                        end
                    end)

                    saturationframe.InputEnded:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseButton1 then
                            slidingsaturation = false
                        end
                    end)

                    services.InputService.InputChanged:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseMovement then
                            if slidingsaturation then
                                updatesatval(input)
                            end
                        end
                    end)

                    local function set(color)
                        if type(color) == "table" then
                            color = Color3.fromRGB(unpack(color))
                        end

                        hue, sat, val = color:ToHSV()
                        hsv = Color3.fromHSV(hue, sat, val)

                        saturationframe.BackgroundColor3 = hsv
                        icon.BackgroundColor3 = hsv
                        saturationpicker.Position = UDim2.new(0, (math.clamp(sat * saturationframe.AbsoluteSize.X, 0, saturationframe.AbsoluteSize.X - 4)), 0, (math.clamp((1 - val) * saturationframe.AbsoluteSize.Y, 0, saturationframe.AbsoluteSize.Y - 4)))
                        huepicker.Position = UDim2.new(0, 0, 0, math.clamp((1 - hue) * saturationframe.AbsoluteSize.Y, 0, saturationframe.AbsoluteSize.Y - 4))

                        box.Text = math.clamp(math.floor((hsv.R * 255) + 0.5), 0, 255) .. ", " .. math.clamp(math.floor((hsv.B * 255) + 0.5), 0, 255) .. ", " .. math.clamp(math.floor((hsv.G * 255) + 0.5), 0, 255)

                        if flag then
                            library.flags[flag] = Color3.fromRGB(hsv.r * 255, hsv.g * 255, hsv.b * 255)
                        end

                        callback(Color3.fromRGB(hsv.r * 255, hsv.g * 255, hsv.b * 255))
                    end

                    local toggled = false

                    local function toggle()
                        if not switchingtabs then
                            toggled = not toggled

                            if toggled then
                                task.spawn(function()
                                    while toggled do
                                        for i = 0, 1, 0.0015 do
                                            if not toggled then
                                                return
                                            end

                                            local color = Color3.fromHSV(i, 1, 1)
                                            set(color)

                                            task.wait()
                                        end
                                    end
                                end)
                            end

                            local enabledtransparency = toggled and 0 or 1
                            utility.tween(enablediconholder, { 0.2 }, { BackgroundTransparency = enabledtransparency })

                            local textcolor = toggled and library.accent or Color3.fromRGB(180, 180, 180)
                            utility.tween(rainbowtxt, { 0.2 }, { TextColor3 = textcolor })

                            if toggled then
                                table.insert(accentobjects.text, title)
                            elseif table.find(accentobjects.text, title) then
                                table.remove(accentobjects.text, table.find(accentobjects.text, title))
                            end
                        end
                    end

                    toggleholder.MouseButton1Click:Connect(toggle)

                    box.FocusLost:Connect(function()
                        local _, amount = box.Text:gsub(", ", "")

                        if amount == 2 then
                            local values = box.Text:split(", ")
                            local r, g, b = math.clamp(values[1], 0, 255), math.clamp(values[2], 0, 255), math.clamp(values[3], 0, 255)
                            set(Color3.fromRGB(r, g, b))
                        else
                            rgb.Text = math.floor((hsv.r * 255) + 0.5) .. ", " .. math.floor((hsv.g * 255) + 0.5) .. ", " .. math.floor((hsv.b * 255) + 0.5)
                        end
                    end)

                    if default then
                        set(default)
                    end

                    if flag then
                        flags[flag] = set
                    end

                    local colorpickertypes = utility.table()

                    function colorpickertypes:Set(color)
                        set(color)
                    end
                end

                return sectiontypes
            end

            return pagetypes
        end

        return windowtypes
    end

    function library:Initialize()
        if gethui then
            gui.Parent = gethui()
        elseif syn and syn.protect_gui then
            syn.protect_gui(gui)
            gui.Parent = services.CoreGui
        end
    end

    function library:Init()
        library:Initialize()
    end
end









local ScriptProperties = {
    ScriptName = "specter.lua",
    ScriptSizeOne = 700,
    ScriptSizeTwo = 500,
    ScriptAccent = Color3.fromRGB(121, 66, 254),


    Perms = { 246220626, 2415886442, 2284385613, 2415886442 },
    Owners = { "tenaki", "happy", "xiba" },
    Admins = { "aiden", "mertcan", "linux" },

    UserPanel = {
        Status = "member"
    }
}




local Library = library

local Window = Library:New({ Name = ScriptProperties.ScriptName, Accent = Color3.fromRGB(133, 87, 242) })
--
local Pred = 0.14
local Pos = 0
local mouse = game.Players.LocalPlayer:GetMouse()
local Player = game:GetService("Players").LocalPlayer
local runService = game:service("RunService")
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-- pages , sections --


local Pages = {
    Aiming = Window:Page({ Name = "Main" }),
    Rage = Window:Page({ Name = "Rage" }),
    Visuals = Window:Page({ Name = "Visuals" }),
    Misc = Window:Page({ Name = "Miscellaneous" }),
    ConfigSec = Window:Page({ Name = "Configurations" })
}

local Sections = {
    Aiming = {
        TargetAim = {
            Main = Pages.Aiming:Section({ Name = "Bullet Prioritise", Side = "Right", Max = 3 }),
            Settings = Pages.Aiming:Section({ Name = "Bullet Prioritise Settings", Side = "Right", Max = 3 })
        },
        Aimbot = {
            Main = Pages.Aiming:Section({ Name = "Aiming", Side = "Left", Max = 3 }),
            Settings = Pages.Aiming:Section({ Name = "Aiming Settings", Side = "Left", Max = 4 })
        },
        MouseStuff = Pages.Aiming:Section({ Name = "Mouse Position", Side = "Right", Max = 2 })
    },
    Visuals = {
        MainVisuals = Pages.Visuals:Section({ Name = "Esp", Side = "Left", Max = 5 }),
        WorldVisuals = Pages.Visuals:Section({ Name = "World Settings", Side = "Right" }),
        PlayerChams = Pages.Visuals:Section({ Name = "Client Visuals", Side = "Left", Max = 2 }),
        BulletTracers = Pages.Visuals:Section({ Name = "Bullet Tracers", Side = "Right", Max = 2 })
    },
    RageSector = {
        AntiAim = Pages.Rage:Section({ Name = "Anti Aim", Side = "Left", Max = 5 }),
        TargetStrafe = Pages.Rage:Section({ Name = "Target Strafe", Side = "Right" }),
        AntiHit = Pages.Rage:Section({ Name = "Anti Hit", Side = "Left" }),
        FakeLag = Pages.Rage:Section({ Name = "Fake Lag", Side = "Right", Max = 2 })
    },
    MiscSector = {
        Fly = Pages.Misc:Section({ Name = "Float", Side = "Left" }),
        CharMain = Pages.Misc:Section({ Name = "Limits", Side = "Right" }),
        SpeedMain = Pages.Misc:Section({ Name = "Movement", Side = "Left" }),
        Fun = Pages.Misc:Section({ Name = "Spammer", Side = "Right", Max = 4 })


    },
    Configuations = {
        Configs = Pages.ConfigSec:Section({ Name = "Configuration", Side = "Left" }),
        Discord = Pages.ConfigSec:Section({ Name = "Discord", Side = "Right" }),
        ScriptStuff = Pages.ConfigSec:Section({ Name = "Utilities", Side = "Right" })
    }
}

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-- cheat settings table --


local BulletTracers = false
local AimingSettings = {
    Aimbot = {
        NotificationMode = false,
        Keybind = Enum.KeyCode.Q,
        Hitbox = "Head",
        HitAirshots = false,
        CameraMode = false,
        MouseMode = false,
        AutoPredct = false,
        PredictionAmount = 0.165,
        Smoothing = false,
        Smoothness = 0.015
    },
    TargetAim = {
        Enabled = true,
        UseFOV = true,
        ShowFOV = false,
        FOV = 60,
        FOVFilled = false,
        Selected = false,
        WallCheck = false,
        PingPred1 = false,
        PingPred2 = false,
        CrewCheck = false,
        ShowHitbox = false,
        AirShotMode = true,
        RandomHitbox = false,
        GrabbedCheck = false,
        KnockedCheck = false,
        FOVThickness = 2,
        FovTransparency = 1,
        NotificationMode = false,
        UseNearestDistance = false,
        Hitboxes = "Head",
        FOVColor = Color3.new(0.603921, 0.011764, 1)
    },
    MousePosSector = {
        Filled = false,
        Thickness = 1,
        Size = 10,
        DOTColor = Color3.fromRGB(0, 71, 212),
        Enabled = false
    }
}

local RageSettings = {
    AntiAim = {
        Enabled = false,
        VelocityBreaker = false,
        VBV = 500,
        VBF = 100,
        Confusion = false
    },

    LegitAntiHit = {
        Enabled = false,
        Multiplier = 0.25
    },
    FakeLag = {
        Enabled = false,
        Multiplier = 0.10,
        Visulize = false,
        ViulizationTransparency = 1,
        ViulizationColor = Color3.fromRGB(255, 0, 0)


    },
    TargetStrafe = {
        Enabled = false,
        AntiAimMode = false,
        AntiAimType = "Default",
        Distance = 2,
        Speed = 0.5,
        Color = Color3.fromRGB(255, 255, 255)
    }
}


local MiscSettings = {
    TrashTalk = {
        Enabled = false
    },
    NoJumpCd = {
        Enabled = false
    },
    NoRecoil = {
        Enabled = false
    },
    Speed = {
        Enabled = false,
        Motion = true,
        BHop = false,
        Amount = 1
    },
    Fly = {
        Enabled = false,
        Normal = true,
        Height = 35,
        MoveOnly = false,
        Amount = 1
    },
    Strafe = {
        Enabled = false
    },
    NoSlowdown = {
        Enabled = false
    }
}

local parts = {
    "Head",
    "UpperTorso",
    "RightUpperArm",
    "RightLowerArm",
    "RightUpperArm",
    "LeftUpperArm",
    "LeftLowerArm",
    "LeftFoot",
    "RightFoot",
    "LowerTorso",
    "LeftHand",
    "RightHand",
    "RightUpperLeg",
    "LeftUpperLeg",
    "LeftLowerLeg",
    "RightLowerLeg"
}


local VisualsExtra = {
    WorldVisuals = {
        MapLightingEnabled = false,
        MapBrightness = 0.6,
        MapContrast = 0.2,
        MapTintColor = Color3.fromRGB(0, 0, 153)
    },
    WeaponEffects = {
        Enabled = false,
        Color = Color3.fromRGB(255, 0, 0),
        Material = "ForceField"
    },
    ClientVisuals = {
        SelfChams = false,
        SelfChamsMaterial = "ForceField",
        SelfChamsColor = Color3.fromRGB(255, 0, 0),
        BaseSkin = "Plastic"
    }
}

local ConfigurationTab = {

    Configs = {


    },

    Discord = {
        AutoJoin = false

    },

    UIPreferances = {


    }
}

----- strafe ---
local Yung = loadstring(game:HttpGet("https://pastebin.com/raw/kwQeFKTi"))()
local Circle = Yung:New3DCircle()
Circle.Visible = RageSettings.TargetStrafe.Enabled
Circle.ZIndex = 1
Circle.Transparency = 1
Circle.Color = RageSettings.TargetStrafe.Color
Circle.Thickness = 1
Circle.Radius = RageSettings.TargetStrafe.Distance
local delta = 0
local duration = RageSettings.TargetStrafe.Speed
local d32_ui_color3 = Color3.fromRGB(255, 255, 255)





--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-- aimbot --

local CC = game:GetService "Workspace".CurrentCamera
local LocalMouse = game.Players.LocalPlayer:GetMouse()
local Locking = false

function x(tt, tx, cc)
    game.StarterGui:SetCore(
        "SendNotification",
        {
        Title = tt,
        Text = tx,
        Duration = cc
    }
    )
end

local UserInputService = game:GetService("UserInputService")

UserInputService.InputBegan:Connect(
    function(keygo, ok)
    if (not ok) then
        if (keygo.KeyCode == AimingSettings.Aimbot.Keybind) then
            Locking = not Locking
            if Locking and getgenv().mousemoverel then
                Plr = getClosestPlayerToCursor()
                PlrP = getclosest()
                if AimingSettings.Aimbot.NotificationMode then
                end
            elseif not Locking then
                if AimingSettings.Aimbot.NotificationMode then
                end
            end
        end
    end
end
)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-- functions --

function getClosestPlayerToCursor()
    local closestPlayer
    local shortestDistance = AimingSettings.TargetAim.FOV

    for i, v in pairs(game.Players:GetPlayers()) do
        if v ~= game.Players.LocalPlayer and v.Character and v.Character:FindFirstChild("Humanoid") and
            v.Character.Humanoid.Health ~= 0 and
            v.Character:FindFirstChild(AimingSettings.Aimbot.Hitbox)
        then
            local pos = CC:WorldToViewportPoint(v.Character.PrimaryPart.Position)
            local magnitude = (Vector2.new(pos.X, pos.Y) - Vector2.new(LocalMouse.X, LocalMouse.Y)).magnitude
            if magnitude < shortestDistance then
                closestPlayer = v
                shortestDistance = magnitude
            end
        end
    end
    return closestPlayer
end

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-- mouse / camera mode --

game:GetService("RunService").RenderStepped:Connect(
    function()
    if Plr == nil then
        return
    elseif not Plr.Character then
        return
    end
    if not Plr.Character:FindFirstChild(AimingSettings.Aimbot.Hitbox) then
        return
    end
    if Locking and AimingSettings.Aimbot.MouseMode then
        local goal =
        CC:WorldToScreenPoint(
            Plr.Character[AimingSettings.Aimbot.Hitbox].Position +
            (Plr.Character[AimingSettings.Aimbot.Hitbox].Velocity * AimingSettings.Aimbot.PredictionAmount)
        )
        mousemoverel(goal.X - LocalMouse.X, goal.Y - LocalMouse.Y)
    else wait()
    end

    if Locking and AimingSettings.Aimbot.CameraMode and not AimingSettings.Aimbot.Smoothing then
        workspace.CurrentCamera.CFrame = CFrame.new(
            workspace.CurrentCamera.CFrame.Position,
            Plr.Character[AimingSettings.Aimbot.Hitbox].Position +
            Plr.Character[AimingSettings.Aimbot.Hitbox].Velocity * AimingSettings.Aimbot.PredictionAmount
        )
    elseif Locking and AimingSettings.Aimbot.CameraMode and AimingSettings.Aimbot.Smoothing then
        local Main =
        CFrame.new(
            workspace.CurrentCamera.CFrame.p,
            Plr.Character[AimingSettings.Aimbot.Hitbox].Position +
            Plr.Character[AimingSettings.Aimbot.Hitbox].Velocity * AimingSettings.Aimbot.PredictionAmount
        )
        workspace.CurrentCamera.CFrame = workspace.CurrentCamera.CFrame:Lerp(
            Main,
            AimingSettings.Aimbot.Smoothness,
            Enum.EasingStyle.Elastic,
            Enum.EasingDirection.InOut
        )
    else wait()
    end
    --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    -- airshot function --

    if AimingSettings.Aimbot.MouseMode == false then
        if AimingSettings.Aimbot.HitAirshots == true then
            if Plr ~= nil and Plr.Character.Humanoid.Jump == true and
                Plr.Character.Humanoid.FloorMaterial == Enum.Material.Air
            then
                AimingSettings.Aimbot.Hitbox = "RightFoot"
            else
                AimingSettings.Aimbot.Hitbox = "LowerTorso"
            end
        end
    end
end
)




--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-- global toggles --


local Toggles = {
    TargetAim = {

        MainToggle = Sections.Aiming.TargetAim.Main:Keybind(
            {
            Name = "Enabled",
            Callback = function(key) end,
            Default = key,
            Pointer = "1",
            Mode = "Toggle",
            toggleflag = "1.1",
            togglecallback = function(state)
                AimingSettings.TargetAim.Enabled = state
            end
        }
        ),

        HitboxesToggle = Sections.Aiming.TargetAim.Main:Dropdown(
            {
            Name = "Hitbox",
            Options = { "Head", "UpperTorso", "HumanoidRootPart" },
            Default = "Head",
            Pointer = "2",
            callback = function(state)
                AimingSettings.TargetAim.Hitboxes = state
            end
        }
        ),


        UseNearestDistance = Sections.Aiming.TargetAim.Main:Toggle(
            {
            Name = "Distance Based",
            Default = false,
            Pointer = "3",
            callback = function(state)
                AimingSettings.TargetAim.UseNearestDistance = state
            end
        }
        ),
        CrewCheckToggle = Sections.Aiming.TargetAim.Main:Toggle(
            {
            Name = "Prioritise Team",
            Default = false,
            Pointer = "4",
            callback = function(state)
                AimingSettings.TargetAim.CrewCheck = state
            end
        }
        ),

        WallCheckToggle = Sections.Aiming.TargetAim.Main:Toggle(
            {
            Name = "Visibility Check",
            Default = false,
            Pointer = "5",
            callback = function(state)
                AimingSettings.TargetAim.WallCheck = state
            end
        }
        ),


        ShowFOVToggle = Sections.Aiming.TargetAim.Settings:Toggle(
            {
            Name = "Draw Fov",
            Default = false,
            Pointer = "6",
            callback = function(state)
                AimingSettings.TargetAim.ShowFOV = state
            end
        }
        ),

        FOVSlider = Sections.Aiming.TargetAim.Settings:Slider(
            {
            Name = "Bullet Radius Size",
            Minimum = 1,
            Maximum = 10,
            Default = 1,
            Decimals = 0.1,
            Pointer = "7",
            callback = function(state)
                AimingSettings.TargetAim.FOV = state ^ 3
            end
        }
        )

    },
    Aimbot = {
        EnableTog = Sections.Aiming.Aimbot.Main:Toggle(
            {
            Name = "Enabled",
            Default = false,
            Pointer = "8",
            callback = function(e)
                AimingSettings.Aimbot.CameraMode = e
            end
        }
        ),
        SmoothingToggle = Sections.Aiming.Aimbot.Main:Toggle(
            {
            Name = "Smoothing",
            Default = false,
            Pointer = "9",
            callback = function(state)
                AimingSettings.Aimbot.Smoothing = state
            end
        }
        ),

        HitboxesDropdown = Sections.Aiming.Aimbot.Main:Dropdown(
            {
            Name = "Hitbox",
            Options = { "Head", "UpperTorso", "HumanoidRootPart" },
            Default = "Head",
            Pointer = "10",
            callback = function(state)
                AimingSettings.Aimbot.Hitbox = state
            end
        }
        ),

        TeamCheckToggle = Sections.Aiming.Aimbot.Main:Toggle(
            {
            Name = "Visibility Check",
            Default = false,
            Pointer = "11",
            callback = function()
            end
        }
        ),


        Revaluation = Sections.Aiming.Aimbot.Main:Toggle(
            {
            Name = "Revaluate Hitspand",
            Default = false,
            Pointer = "12",
            callback = function(state)
                AimingSettings.Aimbot.HitAirshots = state
            end
        }
        ),



        PingDropDown = Sections.Aiming.Aimbot.Settings:Dropdown(
            {
            Name = "Aiming Type",
            Options = { "Ping Based", "Custom" },
            Default = "Ping Based",
            Pointer = "13",
            callback = function(state)
                AimingSettings.Aimbot.AutoPredct = state
            end
        }
        ),
        TypeDropdown = Sections.Aiming.Aimbot.Settings:Dropdown(
            {
            Name = "Aiming Tracing",
            Options = { "Camera", "nil" },
            Default = "nil",
            Pointer = "14",
            callback = function(state)

            end
        }
        ),

        SmoothingSlider = Sections.Aiming.Aimbot.Settings:Slider(
            {
            Name = "Smoothing Amount",
            Minimum = 1,
            Maximum = 10,
            Default = 10,
            Decimals = 0.000000000000000001,
            Pointer = "15",
            callback = function(state)
                AimingSettings.Aimbot.Smoothness = state / 50
            end
        }
        ),
        PredictionAmount = Sections.Aiming.Aimbot.Settings:Slider(
            {
            Name = "Prediction Amount",
            Minimum = 1,
            Maximum = 10,
            Default = 10,
            Decimals = 0.000000000000000001,
            Pointer = "16",
            callback = function(state)
                AimingSettings.Aimbot.Prediction = state / 50
            end
        }
        ),

        RageStuff = {

            AntiAimToggle = Sections.RageSector.AntiAim:Toggle(
                {
                Name = "Enabled",
                Default = false,
                Pointer = "17",
                callback = function(state)
                    RageSettings.AntiAim.Enabled = state
                end
            }
            ),
            DesyncToggle = Sections.RageSector.AntiAim:Toggle(
                {
                Name = "Confusion",
                Default = false,
                Pointer = "18",
                callback = function(state)
                    RageSettings.AntiAim.VelocityBreaker = state
                end
            }
            ),
            DesyncVelocitySlider = Sections.RageSector.AntiAim:Slider(
                {
                Name = "Velocity Speed",
                Minimum = 1,
                Maximum = 500,
                Default = 10,
                Decimals = 0.000000000000001,
                Pointer = "19",
                callback = function(state)
                    RageSettings.AntiAim.VBV = state
                end
            }
            ),
            DesyncFrameSlider = Sections.RageSector.AntiAim:Slider(
                {
                Name = "Spin Speed",
                Minimum = 1,
                Maximum = 100,
                Default = 10,
                Decimals = 0.000000000000001,
                Pointer = "20",
                callback = function(state)
                    RageSettings.AntiAim.VBF = state
                end
            }
            ),
            AntiHitToggle = Sections.RageSector.AntiHit:Toggle(
                {
                Name = "Enabled",
                Default = false,
                Pointer = "21",
                callback = function(state)
                    RageSettings.LegitAntiHit.Enabled = state
                end
            }
            ),
            AntiHitSlider = Sections.RageSector.AntiHit:Slider(
                {
                Name = "Multiplier",
                Minimum = 1,
                Maximum = 10,
                Default = 1,
                Decimals = 0.000000000000001,
                Pointer = "22",
                callback = function(state)
                    RageSettings.LegitAntiHit.Multiplier = state / 10
                end
            }
            )
        },

        FakeLagShit = {
            FakeLagT = Sections.RageSector.FakeLag:Toggle(
                {
                Name = "Enabled",
                Default = false,
                Pointer = "23",
                callback = function(state)

                end
            }
            ),


            FakeLagSlid = Sections.RageSector.FakeLag:Slider(
                {
                Name = "Multiplier",
                Minimum = 1,
                Maximum = 10,
                Default = 1,
                Decimals = 0.000000000000001,
                Pointer = "24",
                callback = function(state)
                    RageSettings.FakeLag.Multiplier = state / 30
                end
            }
            ),

            FakeLagBodyCham = Sections.RageSector.FakeLag:Toggle(
                {
                Name = "Body Cham",
                Default = false,
                Pointer = "25",
                callback = function(state)
                    fakelag = state
                end
            }
            ),

        },
    },

    MiscStuff1 = {
        FlyToggle = Sections.MiscSector.Fly:Toggle(
            {
            Name = "Enabled",
            Default = false,
            Pointer = "26",
            callback = function(state)
                MiscSettings.Fly.Enabled = state
            end
        }
        ),
        FlyHightSlider = Sections.MiscSector.Fly:Slider(
            {
            Name = "Height",
            Minimum = 1,
            Maximum = 100,
            Default = 10,
            Decimals = 0.000000000000001,
            Pointer = "27",
            callback = function(state)
                MiscSettings.Fly.Height = state
            end
        }
        ),
        FlyAmount = Sections.MiscSector.Fly:Slider(
            {
            Name = "Multiplier",
            Minimum = 1,
            Maximum = 10,
            Default = 5,
            Decimals = 0.000000000000001,
            Pointer = "28",
            callback = function(state)
                MiscSettings.Fly.Amount = state
            end
        }
        )

    },


    MiscStuff2 = {
        NoJumpCdToggle = Sections.MiscSector.CharMain:Toggle(
            {
            Name = "Blacklisted",
            Default = false,
            Pointer = "29",
            callback = function(state)
                MiscSettings.NoJumpCd.Enabled = state
                MiscSettings.NoSlowdown.Enabled = state
            end
        }
        ),
        CooldownDropdown = Sections.MiscSector.CharMain:Dropdown(
            {
            Name = "Type",
            Options = { "Jump", "Slowdown" },
            Default = "Jump",
            Pointer = "30",
            callback = function()
            end
        }
        ),
    },

    MovementShit = {
        SpeedToggle = Sections.MiscSector.SpeedMain:Toggle(
            {
            Name = "Enabled",
            Default = false,
            Pointer = "31",
            callback = function(state)
                MiscSettings.Speed.Enabled = state
            end
        }
        ),

        BhopToggle = Sections.MiscSector.SpeedMain:Toggle(
            {
            Name = "Bunny Hop",
            Default = false,
            Pointer = "32",
            callback = function(state)
                MiscSettings.Speed.BHop = state
            end
        }
        ),
        SpeedMultipler = Sections.MiscSector.SpeedMain:Slider(
            {
            Name = "Multiplier",
            Minimum = 1,
            Maximum = 10,
            Default = 1,
            Decimals = 0.000000000000001,
            Pointer = "32",
            callback = function(state)
                MiscSettings.Speed.Amount = state
            end
        }
        ),
        TrashTalk = Sections.MiscSector.Fun:Toggle(
            {
            Name = "Enabled",
            Default = false,
            Pointer = "33",
            callback = function(state)
                MiscSettings.TrashTalk.Enabled = state
            end
        }
        ),
        TrashTalkDropdown = Sections.MiscSector.Fun:Dropdown(
            {
            Name = "Type",
            Options = { "Main" },
            Default = "Main",
            Pointer = "34",
            callback = function(state)
            end
        }
        )
    }
}

local StrafeSection = {
    TargetStrafe = Sections.RageSector.TargetStrafe:Toggle(
        {
        Name = "Enabled",
        Default = false,
        Pointer = "35",
        callback = function(state)
            RageSettings.TargetStrafe.Enabled = state
        end
    }
    ),



    StrafeSlider = Sections.RageSector.TargetStrafe:Slider(
        {
        Name = "Range",
        Minimum = 1,
        Maximum = 100,
        Default = 50,
        Decimals = 0.000000000000001,
        Pointer = "36",
        callback = function(state)
            RageSettings.TargetStrafe.Distance = state
        end
    }
    ),

    SpeedStrafe = Sections.RageSector.TargetStrafe:Slider(
        {
        Name = "Speed",
        Minimum = 1,
        Maximum = 100,
        Default = 50,
        Decimals = 0.000000000000001,
        Pointer = "37",
        callback = function(state)
            RageSettings.TargetStrafe.Speed = state / 50
        end
    }
    ),

    StrafeRage = Sections.RageSector.TargetStrafe:Toggle(
        {
        Name = "Rage Bot",
        Default = false,
        Pointer = "37",
        callback = function(state)
            RageSettings.TargetStrafe.AntiAimMode = state
        end
    }
    ),


    StrafeMode = Sections.RageSector.TargetStrafe:Dropdown(
        {
        Name = "Type",
        Options = { "Flinger", "Default" },
        Default = "Default",
        Pointer = "38",
        callback = function(state)
            RageSettings.TargetStrafe.AntiAimType = state
        end
    }
    )
}


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-- mouse toggles --

local MousePositionToggles = {
    MouseEnabled = Sections.Aiming.MouseStuff:Toggle(
        {
        Name = "Enabled",
        Default = false,
        Pointer = "39",
        callback = function(state)
            AimingSettings.MousePosSector.Enabled = state
        end
    }
    ),


    MouseSizeSlider = Sections.Aiming.MouseStuff:Slider(
        {
        Name = "Pos Radius",
        Minimum = 1,
        Maximum = 50,
        Default = 1,
        Decimals = 0.1,
        Pointer = "40",
        callback = function(state)
            AimingSettings.MousePosSector.Size = state
        end
    }
    )
}

Toggles.TargetAim.ShowFOVToggle:Colorpicker(
    {
    Name = "Fov Color",
    Info = "Field Of View Rgb",
    Alpha = 0.5,
    Default = Color3.fromRGB(133, 87, 242),
    Pointer = "41",
    callback = function(shit)
        AimingSettings.TargetAim.FOVColor = shit
    end
}
)
StrafeSection.TargetStrafe:Colorpicker(
    {
    Name = "Mouse Color",
    Info = "Mouse Color",
    Alpha = 0.5,
    Default = Color3.fromRGB(133, 87, 242),
    Pointer = "42",
    callback = function(shit)
        Circle.Color = shit
    end
}
)

MousePositionToggles.MouseEnabled:Colorpicker(
    {
    Name = "Mouse Color",
    Info = "Mouse Color",
    Alpha = 0.5,
    Default = Color3.fromRGB(133, 87, 242),
    Pointer = "43",
    callback = function(shit)
        AimingSettings.MousePosSector.DOTColor = shit
    end
}
)




local AllahStorage = { Instance = {} }

local GetService =
setmetatable(
    {},
    {
    __index = function(self, key)
        return game:GetService(key)
    end
}
)

local Camera = workspace.CurrentCamera
local WorldToScreen = Camera.WorldToScreenPoint
local WorldToViewportPoint = Camera.WorldToViewportPoint
local GetPartsObscuringTarget = Camera.GetPartsObscuringTarget

local RunService = GetService.RunService
local Players = GetService.Players
local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local CurrentCamera = workspace.CurrentCamera
local UserInputService = GetService.UserInputService
local Unpack = table.unpack
local GuiInset = GetService.GuiService:GetGuiInset()
local Insert = table.insert
local Network = GetService.NetworkClient
local StarterGui = GetService.StarterGui
local tweenService = GetService.TweenService
local ReplicatedStorage = GetService.ReplicatedStorage
local http = GetService.HttpService
local lighting = GetService.Lighting



function Find(Data)
    getgenv().Target = nil
    for i, v in next, Players:GetPlayers() do
        if v.Name ~= LocalPlayer.Name and v.Name:lower():match("^" .. NoSpace(Data):lower()) then
            getgenv().Target = v.Name
        end
    end

    return getgenv().Target
end

function IsNetwork(GetPlayer)
    return GetPlayer and GetPlayer.Character and GetPlayer.Character:FindFirstChild("HumanoidRootPart") ~= nil and
        GetPlayer.Character:FindFirstChild("Humanoid") ~= nil and
        GetPlayer.Character:FindFirstChild("Head") ~= nil and
        true or
        false
end

function Knocked(GetPlayer)
    if IsNetwork(GetPlayer) then
        return GetPlayer.Character.BodyEffects["K.O"].Value and true or false
    end
    return false
end

function Grabbing(GetPlayer)
    if IsNetwork(GetPlayer) then
        return GetPlayer.Character:FindFirstChild("GRABBING_CONSTRAINT") and true or false
    end
    return false
end

function Alive(Player)
    if Player and Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") ~= nil and
        Player.Character:FindFirstChild("Humanoid") ~= nil and
        Player.Character:FindFirstChild("Head") ~= nil
    then
        return true
    end
    return false
end

function CameraCheck(GetPosition, IgnoredList)
    if IsNetwork(LocalPlayer) then
        return #CurrentCamera:GetPartsObscuringTarget({ LocalPlayer.Character.Head.Position, GetPosition }, IgnoredList) ==
            0 and
            true or
            false
    end
end

function WallCheck(OriginPart, Part)
    if IsNetwork(LocalPlayer) then
        local IgnoreList = { CurrentCamera, LocalPlayer.Character, OriginPart.Parent }
        local Parts =
        CurrentCamera:GetPartsObscuringTarget(
            {
                OriginPart.Position,
                Part.Position
            },
            IgnoreList
        )

        for i, v in pairs(Parts) do
            if v.Transparency >= 0.3 then
                AllahStorage.Instance[#AllahStorage.Instance + 1] = v
            end

            if v.Material == Enum.Material.Glass then
                AllahStorage.Instance[#AllahStorage.Instance + 1] = v
            end
        end

        return #Parts == 0
    end
    return true
end

function NilBody()
    if Alive(LocalPlayer) then
        for i, v in pairs(LocalPlayer.Character:GetChildren()) do
            if v:IsA("BasePart") or v:IsA("Part") or v:IsA("MeshPart") then
                if v.Name ~= "HumanoidRootPart" then
                    v:Destroy()
                end
            end
        end
    end
end

function NearestDistance()
    local Target = nil
    local Distance = math.huge
    for i, v in next, Players:GetPlayers() do
        if v ~= LocalPlayer and Alive(LocalPlayer) and Alive(v) then
            local DistanceFromPlayer =
            (v.Character.HumanoidRootPart.Position - LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
            if Distance > DistanceFromPlayer then
                if (not AimingSettings.TargetAim.CrewCheck or
                    v:FindFirstChild("DataFolder") and v.DataFolder.Information:FindFirstChild("Crew") and
                    not tonumber(v.DataFolder.Information.Crew.Value) ==
                    tonumber(LocalPlayer.DataFolder.Information.Crew.Value)) and
                    (not AimingSettings.TargetAim.WallCheck or
                        WallCheck(v.Character.HumanoidRootPart, LocalPlayer.Character.HumanoidRootPart))
                then
                    Target = v
                    Distance = DistanceFromPlayer
                end
            end
        end
    end

    return Target, Distance
end

function NearestMouse()
    local Target = nil
    local Distance = AimingSettings.TargetAim.FOV
    for i, v in next, Players:GetPlayers() do
        if v ~= LocalPlayer and Alive(LocalPlayer) and Alive(v) then
            local RootPosition, RootVisible = CurrentCamera:WorldToViewportPoint(v.Character.HumanoidRootPart.Position)
            local DistanceFromMouse =
            (Vector2.new(RootPosition.X, RootPosition.Y) - Vector2.new(Mouse.X, Mouse.Y)).Magnitude
            if RootVisible and Distance > DistanceFromMouse then
                if (not AimingSettings.TargetAim.CrewCheck or
                    v:FindFirstChild("DataFolder") and v.DataFolder.Information:FindFirstChild("Crew") and
                    not tonumber(v.DataFolder.Information.Crew.Value) ==
                    tonumber(LocalPlayer.DataFolder.Information.Crew.Value)) and
                    (not AimingSettings.TargetAim.WallCheck or
                        WallCheck(v.Character.HumanoidRootPart, LocalPlayer.Character.HumanoidRootPart))
                then
                    Target = v
                    Distance = DistanceFromMouse
                end
            end
        end
    end

    return Target, Distance
end

function NearestType(Type)
    if Type == "Distance" then
        return NearestDistance()
    elseif Type == "Mouse" then
        return NearestMouse()
    end
end

function ChanceTable(Table)
    local Chance = 0
    for i, v in pairs(Table) do
        Chance = Chance + v
    end
    Chance = math.random(0, Chance)
    for i, v in pairs(Table) do
        Chance = Chance - v
        if Chance <= 0 then
            return i
        end
    end
end

function RandomTable(Table)
    local Values = 0
    for i, v in pairs(Table) do
        Values = i
    end

    return Table[math.random(1, Values)]
end

local function getMousePosition()
    return Vector2.new(mouse.X, mouse.Y)
end

local mouse = game.Players.LocalPlayer:GetMouse()





local WorldToViewportPoint = CurrentCamera.worldToViewportPoint

local fov_circle = Drawing.new("Circle")
fov_circle.Thickness = 1
fov_circle.NumSides = 100
fov_circle.Radius = 180
fov_circle.Filled = false
fov_circle.Visible = false
fov_circle.ZIndex = 999
fov_circle.Transparency = AimingSettings.TargetAim.FovTransparency
fov_circle.Color = Color3.fromRGB(54, 57, 241)


local outline = Drawing.new("Circle")
outline.Thickness = 0.3
outline.NumSides = 100
outline.Radius = fov_circle.Radius
outline.Filled = false
outline.Visible = false
outline.ZIndex = 999
outline.Color = Color3.fromRGB(1, 1, 1)

local mouse_box = Drawing.new("Square")
mouse_box.Visible = false
mouse_box.ZIndex = 999
mouse_box.Color = Color3.fromRGB(54, 57, 241)
mouse_box.Thickness = 20
mouse_box.Size = Vector2.new(20, 20)
mouse_box.Filled = true

local Plr = nil

local pingvalue = game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValueString()
local split = string.split(pingvalue, "(")
local ping = tonumber(split[1])

local mt = getrawmetatable(game)
local old = mt.__namecall
setreadonly(mt, false)
mt.__namecall = newcclosure(
    function(...) --// LPH JIT
    local args = { ... }
    if AimingSettings.TargetAim.Enabled and Plr ~= game.Players.LocalPlayer and Plr ~= nil and
        (not AimingSettings.TargetAim.UseFOV or AimingSettings.TargetAim.FOV > Pos) and
        getnamecallmethod() == "FireServer" and
        args[2] == "UpdateMousePos"
    then
        if AimingSettings.TargetAim.AirShotMode == true then
            if Plr ~= nil and Plr.Character.Humanoid.Jump == true and
                Plr.Character.Humanoid.FloorMaterial == Enum.Material.Air
            then
                -- "RightFoot"
                args[3] = Plr.Character["RightFoot"].Position + (Plr.Character["RightFoot"].Velocity * Pred)
                return old(unpack(args))
            else
                -- "LowerTorso"
                args[3] = Plr.Character[AimingSettings.TargetAim.Hitboxes].Position +
                    (Plr.Character[AimingSettings.TargetAim.Hitboxes].Velocity * Pred)
                return old(unpack(args))
            end
        else
            args[3] = Plr.Character[AimingSettings.TargetAim.Hitboxes].Position +
                (Plr.Character[AimingSettings.TargetAim.Hitboxes].Velocity * Pred)
            return old(unpack(args))
        end

        --[[
args[3] =
Plr.Character[AimingSettings.TargetAim.Hitboxes].Position +
(Plr.Character[AimingSettings.TargetAim.Hitboxes].Velocity * Pred)

]]
    end

    return old(...)
end
)

-- ac

loadstring(
    game:HttpGet(
    "https://pastebin.com/raw/UrQGK0p7"
    )
)()


local a;
a = hookfunction(wait, function(b) if b == 1.5 and MiscSettings.NoJumpCd.Enabled then return a() end return a(b) end)





local EspVisuals = {

    BoxesToggle = Sections.Visuals.MainVisuals:Toggle(
        {
        Name = "Boxes",
        Default = false,
        Pointer = "44",
        callback = function(bi)
        end
    }
    ),

    NameToggle = Sections.Visuals.MainVisuals:Toggle(
        {
        Name = "Names",
        Default = false,
        Pointer = "45",
        callback = function(bi)
        end
    }
    ),
    TracersToggle = Sections.Visuals.MainVisuals:Toggle(
        {
        Name = "Tracers",
        Default = false,
        Pointer = "46",
        callback = function(bi)
        end
    }
    ),
    SkelotonToggle = Sections.Visuals.MainVisuals:Toggle(
        {
        Name = "Skeletons",
        Default = false,
        Pointer = "47",
        callback = function(bi)
        end
    }
    ),



    DistanceTog = Sections.Visuals.MainVisuals:Toggle(
        {
        Name = "Distance",
        Default = false,
        Pointer = "48",
        callback = function(bi)

        end
    }
    ),

    HealthInfo = Sections.Visuals.MainVisuals:Toggle(
        {
        Name = "Health Info",
        Default = false,
        Pointer = "49",
        callback = function(bi)

        end
    }
    ),

    GunInfo = Sections.Visuals.MainVisuals:Toggle(
        {
        Name = "Weapon Info",
        Default = false,
        Pointer = "50",
        callback = function(bi)
        end
    }
    ),




    ChamsTog = Sections.Visuals.PlayerChams:Toggle(
        {
        Name = "Body Cham",
        Default = false,
        Pointer = "51",
        callback = function(state)
            VisualsExtra.ClientVisuals.SelfChams = state
        end
    }
    ),

    ChamDrop = Sections.Visuals.PlayerChams:Dropdown(
        {
        Name = "Body Material",
        Options = { "ForceField", "Glass" },
        Default = "ForceField",
        Pointer = "52",
        callback = function(state)
            VisualsExtra.ClientVisuals.SelfChamsMaterial = state
        end
    }
    ),
    GunTog = Sections.Visuals.PlayerChams:Toggle(
        {
        Name = "Gun Cham",
        Default = false,
        Pointer = "53",
        callback = function(state)
            VisualsExtra.WeaponEffects.Enabled = state
        end
    }
    ),
    GunDrop = Sections.Visuals.PlayerChams:Dropdown(
        {
        Name = "Gun Material",
        Options = { "ForceField", "Glass" },
        Default = "ForceField",
        Pointer = "54",
        callback = function(state)
            VisualsExtra.WeaponEffects.Material = state
        end
    }
    ),

    BulletTracersToggle = Sections.Visuals.BulletTracers:Toggle(
        {
        Name = "Enabled",
        Default = false,
        Pointer = "55",
        callback = function(bi)
            BulletTracers = bi
        end
    }
    ),



    MapLightingToggle = Sections.Visuals.WorldVisuals:Toggle(
        {
        Name = "Map Lighting",
        Default = false,
        Pointer = "56",
        callback = function(bi)
            VisualsExtra.WorldVisuals.MapLightingEnabled = bi
        end
    }
    ), -- add more shit soon
    MapBrightness = Sections.Visuals.WorldVisuals:Slider(
        {
        Name = "Map Brightness",
        Minimum = 0,
        Maximum = 100,
        Default = 1,

        Decimals = 0.1,
        Pointer = "57",
        callback = function(E)
            VisualsExtra.WorldVisuals.MapBrightness = E / 50
        end
    }
    ),
    MapContrast = Sections.Visuals.WorldVisuals:Slider(
        {
        Name = "Map Contrast",
        Minimum = 0,
        Maximum = 100,
        Default = 1,

        Decimals = 0.1,
        Pointer = "58",
        callback = function(E)
            VisualsExtra.WorldVisuals.MapContrast = E / 50
        end
    }
    )



}
EspVisuals.BulletTracersToggle:Colorpicker(
    {
    Name = "Bullet Tracers",
    Info = "Bullet Tracers",
    Alpha = 0.5,
    Default = Color3.fromRGB(255, 0, 0),
    Pointer = "59",
    callback = function(bi)
        bullet_tracer_color = bi
    end
}
)


EspVisuals.MapLightingToggle:Colorpicker(
    {
    Name = "Lighting Color",
    Info = "World Color",
    Alpha = 0.5,
    Default = Color3.fromRGB(255, 255, 255),
    Pointer = "60",
    callback = function(shit)
        VisualsExtra.WorldVisuals.MapTintColor = shit
    end
}
)

EspVisuals.BoxesToggle:Colorpicker(
    {
    Name = "Esp Color",
    Info = "Esp Color",
    Alpha = 0.5,
    Default = Color3.fromRGB(137, 207, 240),
    Pointer = "61",
    callback = function(shit)
        ESPColor = shit

    end
}
)



EspVisuals.ChamsTog:Colorpicker(
    {
    Name = "Self Chams Color",
    Info = "Self Chams Color",
    Alpha = 0.5,
    Default = Color3.fromRGB(133, 87, 242),
    Pointer = "62",
    callback = function(bi)
        VisualsExtra.ClientVisuals.SelfChamsColor = bi
    end
}
)

EspVisuals.GunTog:Colorpicker(
    {
    Name = "Gun Color",
    Info = "Gun Color",
    Alpha = 0.5,
    Default = Color3.fromRGB(255, 0, 0),
    Pointer = "63",
    callback = function(bi)
        VisualsExtra.WeaponEffects.Color = bi
    end
}
)


local watermark = library:Watermark {}

task.spawn(function()
    local frames = 0

    game:GetService "RunService".RenderStepped:Connect(function()
        frames = frames + 1
    end)

    watermark:Update { "specter.lua", ScriptProperties.UserPanel.Status, frames .. " FPS", string.format("%s:%s %s", tonumber(os.date("%I")), os.date("%M"), os.date("%p")) }

    while task.wait(1) do
        watermark:Update { "specter.lua", ScriptProperties.UserPanel.Status, frames .. " FPS", string.format("%s:%s %s", tonumber(os.date("%I")), os.date("%M"), os.date("%p")) }
        frames = 0
    end
end)

local currentconfig = ""
local configname = ""

ConfigStuff = {


    configdropdown = Sections.Configuations.Configs:Dropdown { Name = "Main", Options = Library:ListConfigs(), Callback = function(option)
        currentconfig = option
    end },



    Sections.Configuations.Configs:Box { Name = "", Callback = function(text)
        configname = text
    end },

    Sections.Configuations.Configs:Button { Name = "Save", Callback = function()
        Library:SaveConfig(configname)
        ConfigStuff.configdropdown:Refresh(Library:ListConfigs())
    end }
    ,

    Sections.Configuations.Configs:Button { Name = "Load", Callback = function()
        Library:LoadConfig(currentconfig)
    end },
    Sections.Configuations.Configs:Button { Name = "Delete", Callback = function()
        Library:DeleteConfig(currentconfig)
        ConfigStuff.configdropdown:Refresh(Library:ListConfigs())
    end }


}



SettingsSection = {
    UiToggle = Sections.Configuations.ScriptStuff:Keybind { Name = "Keybind", Default = Enum.KeyCode.RightShift, Blacklist = { Enum.UserInputType.MouseButton1 }, Flag = "CurrentBind", Callback = function(key, fromsetting)
        if not fromsetting then
            library:Toggle()
        end
    end },

    WaterMarkToggle = Sections.Configuations.ScriptStuff:Keybind { Name = "Watermark", Default = Enum.KeyCode.RightShift, Blacklist = { Enum.UserInputType.MouseButton1 }, Flag = "CurrentToggle", Callback = function(key, fromsetting)
        if not fromsetting then
            watermark:Toggle()
        end
    end }

}




Discord = {


    AutoJoin = Sections.Configuations.Discord:Toggle(
        {
        Name = "Auto Join",
        Default = false,
        Pointer = "64",
        callback = function(e)
            ConfigurationTab.Discord.AutoJoin = e

        end
    }
    ),

    DiscordCopyInv = Sections.Configuations.Discord:Button { Name = "Copy Invite", Callback = function()
        setclipboard("https://discord.gg/BaUbkH7BVr")
    end }

}


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-- fakelag --



--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-- rage --


function getclosest()

    local mouse = game.Players.localPlayer:GetMouse()
    local x, y = mouse.X, mouse.Y
    local closestPlayer = nil
    local shortestDistance = math.huge
    for i, v in pairs(game:GetService("Players"):GetPlayers()) do
        if v ~= lp and v.Character and v.Character:FindFirstChild("Humanoid") and v.Character.Humanoid.Health ~= 0 and v.Character:FindFirstChild("HumanoidRootPart") and v.Character:FindFirstChild("Head") then
            local pos = game:GetService("Workspace").CurrentCamera:WorldToViewportPoint(v.Character.HumanoidRootPart.Position)
            local magnitude = (Vector2.new(pos.X, pos.Y) - Vector2.new(x, y)).magnitude
            if magnitude < shortestDistance and v.Character.Humanoid.Health > 0 then
                closestPlayer = v
                shortestDistance = magnitude
            end
        end
    end
    return closestPlayer
end

game:GetService("RunService").Stepped:Connect(
    function(a, b)
    if PlrP ~= nil and RageSettings.TargetStrafe.Enabled and Locking then
        delta = (delta + b / RageSettings.TargetStrafe.Speed) % 1
        Circle.Visible = true
        Circle.Position = PlrP.Character.HumanoidRootPart.Position
        Circle.Color = RageSettings.TargetStrafe.Color
        Circle.Radius = RageSettings.TargetStrafe.Distance
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.Angles(0, 2 * math.pi * delta, 0) * CFrame.new(0, 0, Circle.Radius) + PlrP.Character.HumanoidRootPart.Position

        if RageSettings.TargetStrafe.AntiAimMode then
            if RageSettings.TargetStrafe.AntiAimType == 'Flinger' then
                game.Players.LocalPlayer.Character.HumanoidRootPart.Velocity = Vector3.new(math.random(-500, 500), math.random(-400, 400), math.random(-1000, 1000))
                wait()
                game.Players.LocalPlayer.Character.HumanoidRootPart.Velocity = Vector3.new(math.random(-500, 500), math.random(-400, 400), math.random(-1000, 1000))
            else
                game.Players.LocalPlayer.Character.HumanoidRootPart.Velocity = Vector3.new(math.random(100, 6000), math.random(100, 6000), math.random(100, 6000))
                wait()
                game.Players.LocalPlayer.Character.HumanoidRootPart.Velocity = Vector3.new(-math.random(100, 6000), -math.random(100, 6000), -math.random(100, 6000))
            end
        end
    else
        Circle.Visible = false
    end
end)
game:GetService("RunService").Stepped:Connect(
    function(a, b)
    Plr = NearestMouse()

    fov_circle.Filled = AimingSettings.TargetAim.FOVFilled
    fov_circle.Thickness = AimingSettings.TargetAim.FOVThickness
    fov_circle.Radius = AimingSettings.TargetAim.FOV
    outline.Radius = AimingSettings.TargetAim.FOV
    fov_circle.Visible = AimingSettings.TargetAim.ShowFOV
    outline.Visible = AimingSettings.TargetAim.ShowFOV
    fov_circle.Color = AimingSettings.TargetAim.FOVColor
    outline.Position = getMousePosition() + Vector2.new(0, 36)
    fov_circle.Position = getMousePosition() + Vector2.new(0, 36)
    fov_circle.Transparency = AimingSettings.TargetAim.FovTransparency
    mouse_box.Thickness = AimingSettings.MousePosSector.Thickness -- thickness slider
    mouse_box.Size = Vector2.new(AimingSettings.MousePosSector.Size, AimingSettings.MousePosSector.Size) -- size slider

    if AimingSettings.MousePosSector.Enabled and NearestMouse() ~= nil then
        mouse_box.Color = AimingSettings.MousePosSector.DOTColor -- add colorpicker
        mouse_box.Visible = ((NearestMouse() and true) or false)
        mouse_box.Position = ((NearestMouse().Character[AimingSettings.TargetAim.Hitboxes].Position and
            Vector2.new(
                WorldToViewportPoint(Camera, Plr.Character[AimingSettings.TargetAim.Hitboxes].Position).X,
                WorldToViewportPoint(Camera, NearestMouse().Character[AimingSettings.TargetAim.Hitboxes].Position).Y
            )) or
            Vector2.new(-9000, -9000))
    end



    if RageSettings.LegitAntiHit.Enabled then
        if RageSettings.LegitAntiHit.Enabled then
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame +
                -game.Players.LocalPlayer.Character.Humanoid.MoveDirection * RageSettings.LegitAntiHit.Multiplier
        end
    end

    --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    -- auto predict to ping --

    pingvalue = game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValueString()
    split = string.split(pingvalue, "(")
    ping = tonumber(split[1])


    if AimingSettings.TargetAim.PingPred1 == true then
        if ping < 130 then
            Pred = 0.151
        elseif ping < 125 then
            Pred = 0.149
        elseif ping < 110 then
            Pred = 0.146
        elseif ping < 105 then
            Pred = 0.138
        elseif ping < 90 then
            Pred = 0.136
        elseif ping < 80 then
            Pred = 0.134379
        elseif ping < 70 then
            Pred = 0.129762
        elseif ping < 60 then
            Pred = 0.1248976
        elseif ping < 50 then
            Pred = 0.1245
        elseif ping < 40 then
            Pred = 0.13232
        end
    end





    if RageSettings.AntiAim.Enabled == true then
        game.Players.LocalPlayer.Character.Head.CanCollide = false
        game.Players.LocalPlayer.Character.UpperTorso.CanCollide = false
        game.Players.LocalPlayer.Character.LowerTorso.CanCollide = false
        game.Players.LocalPlayer.Character.HumanoidRootPart.CanCollide = false
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame *
            CFrame.new(math.random(1, 2) == 1 and 2 or -2, 0, 0)
    else
        game.Players.LocalPlayer.Character.Head.CanCollide = true
        game.Players.LocalPlayer.Character.UpperTorso.CanCollide = true
        game.Players.LocalPlayer.Character.LowerTorso.CanCollide = true
        game.Players.LocalPlayer.Character.HumanoidRootPart.CanCollide = true
    end

    if RageSettings.AntiAim.VelocityBreaker then
        game.Players.LocalPlayer.Character.HumanoidRootPart.Velocity = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector * RageSettings.AntiAim.VBV
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame *
            CFrame.Angles(0, math.rad(RageSettings.AntiAim.VBF), 0)
    end

    if MiscSettings.TrashTalk.Enabled == true then
        local A_1 = {
            "specter.lua > u",
            "sonned?",
            "sad life",
            "u shall quit "
        }
        local A_2 = "All"
        local Event = game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest
        Event:FireServer(A_1[math.random(7)], A_2)
    end

    if MiscSettings.Speed.Enabled and not MiscSettings.Fly.Enabled then
        if LocalPlayer.Character.Humanoid.MoveDirection.Magnitude > 0 then
            if MiscSettings.Speed.Motion then
                LocalPlayer.Character:TranslateBy(
                    LocalPlayer.Character.Humanoid.MoveDirection * MiscSettings.Speed.Amount / 1.5
                )
            end
            if MiscSettings.Speed.BHop and
                LocalPlayer.Character.Humanoid:GetState() ~= Enum.HumanoidStateType.Freefall
            then
                LocalPlayer.Character.Humanoid:ChangeState("Jumping")
            end
        end
    end

    if MiscSettings.Fly.Enabled and
        (not MiscSettings.Fly.MoveOnly or LocalPlayer.Character.Humanoid.MoveDirection.Magnitude > 0)
    then
        if MiscSettings.Fly.Normal then
            local AngleX, AngleY, AngleZ = LocalPlayer.Character.HumanoidRootPart.CFrame:ToEulerAnglesYXZ()
            LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(
                LocalPlayer.Character.HumanoidRootPart.CFrame.X,
                MiscSettings.Fly.Height + 24,
                LocalPlayer.Character.HumanoidRootPart.CFrame.Z
            ) * CFrame.Angles(AngleX, AngleY, AngleZ)
            LocalPlayer.Character.Humanoid:ChangeState("Freefall")
            LocalPlayer.Character:TranslateBy(
                LocalPlayer.Character.Humanoid.MoveDirection * MiscSettings.Fly.Amount / 1.5
            )
        end
    end

    if MiscSettings.Strafe.Enabled then
        if LocalPlayer.Character.Humanoid.MoveDirection.Magnitude > 0 and
            LocalPlayer.Character.Humanoid:GetState() == Enum.HumanoidStateType.Freefall
        then
            LocalPlayer.Character:TranslateBy(LocalPlayer.Character.Humanoid.MoveDirection / 3.1)
        end
    end
end
)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-- map visuals --
local MapLightingJmp = Instance.new("ColorCorrectionEffect")

game:GetService("RunService").RenderStepped:Connect(
    function()
    if MapLightingJmp.Enabled ~= VisualsExtra.WorldVisuals.MapLightingEnabled then
        MapLightingJmp.Enabled = VisualsExtra.WorldVisuals.MapLightingEnabled
    end

    if MapLightingJmp.Brightness ~= VisualsExtra.WorldVisuals.MapBrightness then
        MapLightingJmp.Brightness = VisualsExtra.WorldVisuals.MapBrightness
    end

    if MapLightingJmp.Contrast ~= VisualsExtra.WorldVisuals.MapContrast then
        MapLightingJmp.Contrast = VisualsExtra.WorldVisuals.MapContrast
    end

    if MapLightingJmp.TintColor ~= VisualsExtra.WorldVisuals.MapTintColor then
        MapLightingJmp.TintColor = VisualsExtra.WorldVisuals.MapTintColor
    end

    if MapLightingJmp.Parent ~= game:GetService("Lighting") then
        MapLightingJmp.Parent = game:GetService("Lighting")
    end

    -- wsg


    if VisualsExtra.ClientVisuals.SelfChams then
        for i, v in pairs(parts) do
            game.Players.LocalPlayer.Character[v].Material = VisualsExtra.ClientVisuals.SelfChamsMaterial
            game.Players.LocalPlayer.Character[v].Color = VisualsExtra.ClientVisuals.SelfChamsColor
        end
    end

    if VisualsExtra.ClientVisuals.SelfChams == false then
        for i, v in pairs(parts) do
            game.Players.LocalPlayer.Character[v].Material = VisualsExtra.ClientVisuals.BaseSkin
        end
    end

    local tool = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool")
    if tool and tool:FindFirstChild 'Default' then

        if VisualsExtra.WeaponEffects.Enabled == true then
            Game.GetService(game, "Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Default.Material = VisualsExtra.WeaponEffects.Material
            Game.GetService(game, "Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Default.Color = VisualsExtra.WeaponEffects.Color
        else
            if tool and tool:FindFirstChild 'Default' then
                if VisualsExtra.WeaponEffects.Enabled == false then
                    Game.GetService(game, "Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Default.Material = Enum.Material.Glass
                end
            end
        end
    end
end

)
---------------------------------------------------------------------------------------------------------------------------------------------

-- no slowdown  --



-- Bullet Tracers
bullet_tracer_color = Color3.fromRGB(255, 255, 255)
function GetGun()
    if game.Players.LocalPlayer.Character then
        for i, v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
            if v:FindFirstChild 'Ammo' then
                return v
            end
        end
    end
    return nil
end

BulletTracers = false
local Services = {
    Players = game:GetService("Players"),
    UserInputService = game:GetService("UserInputService"),
    RunService = game:GetService("RunService"),
}

local Local = {
    Player = Services.Players.LocalPlayer,
    Mouse = Services.Players.LocalPlayer:GetMouse(),
}
local Other = {
    Camera = workspace.CurrentCamera,
    BeamPart = Instance.new("Part", workspace)
}

Other.BeamPart.Name = "BeamPart"
Other.BeamPart.Transparency = 1
local Settings = {
    StartColor = MainAccentColor,
    EndColor = MainAccentColor,
    StartWidth = 3,
    EndWidth = 3,
    ShowImpactPoint = false,
    ImpactTransparency = 0.5,
    ImpactColor = Color3.new(1, 1, 1),
    Time = 1,
}
game:GetService "RunService".Heartbeat:Connect(function()

end)
local funcs = {}
Local.Mouse.TargetFilter = Other.BeamPart
function funcs:Beam(v1, v2)
    v2 = Vector3.new(v2.X - 0.1, v2.Y + 0.2, v2.Z)
    local colorSequence = ColorSequence.new({
        ColorSequenceKeypoint.new(0, bullet_tracer_color),
        ColorSequenceKeypoint.new(1, bullet_tracer_color),
    })
    local Part = Instance.new("Part", Other.BeamPart)
    Part.Size = Vector3.new(0, 0, 0)
    Part.Massless = true
    Part.Transparency = 1
    Part.CanCollide = false
    Part.Position = v1
    Part.Anchored = true
    local Attachment = Instance.new("Attachment", Part)
    local Part2 = Instance.new("Part", Other.BeamPart)
    Part2.Size = Vector3.new(0, 0, 0)
    Part2.Transparency = 0
    Part2.CanCollide = false
    Part2.Position = v2
    Part2.Anchored = true
    Part2.Material = Enum.Material.ForceField
    Part2.Color = Settings.ImpactColor
    Part2.Massless = true
    local Attachment2 = Instance.new("Attachment", Part2)
    local Beam = Instance.new("Beam", Part)
    Beam.FaceCamera = true
    Beam.Color = colorSequence
    Beam.Attachment0 = Attachment
    Beam.Attachment1 = Attachment2
    Beam.LightEmission = 6
    Beam.LightInfluence = 1
    Beam.Width0 = Settings.StartWidth
    Beam.Width1 = Settings.EndWidth
    Beam.Texture = "http://www.roblox.com/asset/?id=9150663556"
    Beam.TextureSpeed = 2
    Beam.TextureLength = 1
    delay(Settings.Time, function()
        Part:Destroy()
        Part2:Destroy()
    end)
end

spawn(function()
    while task.wait(0.5) do
        gun = GetGun()
        if gun then
            LastAmmo = gun.Ammo.Value
            gun.Ammo:GetPropertyChangedSignal("Value"):Connect(function()
                if BulletTracers and gun.Ammo.Value < LastAmmo then
                    LastAmmo = gun.Ammo.Value
                    funcs:Beam(gun.Handle.Position, Local.Mouse.hit.p)
                end
            end)
        end
    end
end)



Library:ChangeAccent(Color3.fromRGB(133, 87, 242))
Library:ChangeOutline { Color3.fromRGB(121, 66, 254), Color3.fromRGB(223, 57, 137) }

Library:Initialize()
