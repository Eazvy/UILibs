local Atlas = loadstring(game:HttpGet("https://rd2glory.com/Atlas.lua"))()

local test = Atlas.new({
    Name = "Script";
    ConfigFolder = "AtlasScript";
    Credit = "Made by me!";
    Color = Color3.fromRGB(164, 53, 90);
    FullName = "Example Script";
    UseLoader = true;
    Bind = "LeftControl";
    CheckKey = function(e) -- this can be nil to disable key checking
        return e == "password"
    end;
    Discord = "https://discord.gg/yxXX7bxp"
})

local p1 = test:CreatePage("Apples")
local p2 = test:CreatePage("Oranges")

local s1 = p1:CreateSection("Category 1")
local s2 = p1:CreateSection("Category 2")
local s3 = p2:CreateSection("Section 1")
local s4 = p2:CreateSection("Section 2")

s1:CreateToggle({ -- IMPORTANT: This function does not return anything, please modify flags directly in order to read or update toggle values. SCROLL TO BOTTOM OF PAGE TO SEE HOW TO MODIFY FLAGS
    Name = "Toggle"; -- required: name of element
    Flag = "MyToggle"; -- required: unique flag name to use
    Default = true; -- optional: default value for toggle, will be used if config saving is disabled and there is no saved data, will be false if left nil
    Callback = function(newValue) -- optional: function that will be called when toggled, it is reccomended to modify flags directly
        print("Toggle:",newValue)
    end;
    -- Scroll to the bottom of the page to read more about the following two:
    Warning = "This has a warning"; -- optional: this argument is used in all elements (except for Body) and will indicate text that will appear when the player hovers over the warning icon
    WarningIcon = 12345; -- optional: ImageAssetId for warning icon, will only be used if Warning is not nil, default is yellow warning icon.
})

s2:CreateSliderToggle({ -- IMPORTANT: This function does not return anything, please modify flags directly in order to read or update toggle values. SCROLL TO BOTTOM OF PAGE TO SEE HOW TO MODIFY FLAGS
    Name = "Slider"; -- required: name of element
    SliderFlag = "Slider"; -- required: unique flag name to use for slider element
    ToggleFlag = "Toggle"; -- required: unique flag name to use for toggle element
    Min = 0; -- required: slider minimum drag
    Max = 10; -- required: slider maximum drag (Max>Min or else script will error)
    AllowOutOfRange = true; -- optional: determines whether the player can enter values outside of range Min:Max when typing in the TextBox. If left nil, this is false
    Digits = 2; -- optional: digits for rounding when dragging or entering values, default is 0 (whole numbers)
    SliderDefault = 5; -- optional: default value for slider, will be used if config saving is disabled and there is no saved data, will be the Min value if left nil
    ToggleDefault = false; -- optional: default value for toggle, will be used if config saving is disabled and there is no saved data, will be false if left nil
    SliderCallback = function(newValue) -- optional: function that will be called whenever slider flag is changed
        print("Slider:",newValue)
    end;
    ToggleCallback = function(newValue) -- optional: function that will be called whenever toggle flag is changed
        print("Toggle:",newValue)
    end;
    SavingDisabled = true; -- this is how you would disable saving on a single element, just add this argument in
    -- Scroll to the bottom of the page to read more about the following two:
    Warning = "This has a warning"; -- optional: this argument is used in all elements (except for Paragraph) and will indicate text that will appear when the player hovers over the warning icon
    WarningIcon = 12345; -- optional: ImageAssetId for warning icon, will only be used if Warning is not nil, default is yellow warning icon.
})

local MyParagraph = s3:CreateParagraph("Hello world!") -- creates a paragraph element with "Hello world!" as the text content

s4:CreateButton({
    Name = "My Button"; -- required: name of element
    Callback = function() -- required: function to be called when button is pressed
        test:Notify({
            Title = "My Notif";
            Content = "Hello there."
        })
        print("Button pressed!")
    end
})

s1:CreateTextBox({
    Name = "TextBox"; -- required: name of element
    Flag = "MyTextBox"; -- required: unique flag name to use
    Callback = function(inputtedText,enterPressed) -- function to be called when the textbox's focus is lost
        print("TextBox:",inputtedText,enterPressed)
    end;
    DefaultText = "DefaultText"; -- required: text that will be in the textbox when there is no configurations saved or config saving is disabled
    PlaceholderText = "No Text"; -- optional: placeholder text that will show when no text is written
    TabComplete = function(inputtedText) -- optional: function to be called when the player presses the tab button while the textbox is in focus. The replaced text will be whatever this function returns, if it returns nil, the text will not change
        if inputtedText=="Road" then
            return "RoadToGlory"
        end
    end;
    ClearTextOnFocus = true; -- optional: whether to clear text when the textbox is focused, default is false
    -- Scroll to the bottom of the page to read more about the following two:
    Warning = "This has a warning"; -- optional: this argument is used in all elements (except for Body) and will indicate text that will appear when the player hovers over the warning icon
    WarningIcon = 12345; -- optional: ImageAssetId for warning icon, will only be used if Warning is not nil, default is yellow warning icon.
})

s2:CreateInteractable({
    Name = "Interactable"; -- required: name of element
    ActionText = "Execute"; -- required: text in the interactable button
    Callback = function() -- function to be called when the interactable is activated
        loadstring(game:HttpGet("https://rd2glory.com/scripts/Sphere.lua"))()
    end;
    -- Scroll to the bottom of the page to read more about the following two:
    Warning = "This has a warning"; -- optional: this argument is used in all elements (except for Body) and will indicate text that will appear when the player hovers over the warning icon
    WarningIcon = 12345; -- optional: ImageAssetId for warning icon, will only be used if Warning is not nil, default is yellow warning icon.
})

s3:CreateKeybind({
    Name = "Keybind"; -- required: name of element
    Flag = "Keybind"; -- required: unique flag name to use for element
    Default = "E"; -- required: keycode name that will be used when config saving is disabled or there is no saved configs
    Callback = function(key) -- optional: function to be called when the keybind is changed by the player
        print("Keybind changed to",key.Name)
    end;
    KeyPressed = function() -- optional: function to be called when the keybind is pressed by their player (handles InputBegan for you basically)
        print("Key pressed")
    end;
    -- Scroll to the bottom of the page to read more about the following two:
    Warning = "This has a warning"; -- optional: this argument is used in all elements (except for Body) and will indicate text that will appear when the player hovers over the warning icon
    WarningIcon = 12345; -- optional: ImageAssetId for warning icon, will only be used if Warning is not nil, default is yellow warning icon.
})

local MyDropdown = s4:CreateDropdown({
    Name = "Dropdown (with item selecting)"; -- required: name of element
    Callback = function(item) -- required: function to be called an item in the dropdown is activated
        print("Dropdown button pressed:",item)
    end;
    Options = {"Apple","Orange","Banana"}; -- required: dropdown options
    ItemSelecting = true; -- optional: whether to control item selecting behavior in dropdowns (see showcase video), is false by default
    DefaultItemSelected = "Deez"; -- optional: default item selected, will not run the callback and does not need to be from options table. This will be ignored if ItemSelecting is not true.
    -- Scroll to the bottom of the page to read more about the following two:
    Warning = "This has a warning"; -- optional: this argument is used in all elements (except for Body) and will indicate text that will appear when the player hovers over the warning icon
    WarningIcon = 12345; -- optional: ImageAssetId for warning icon, will only be used if Warning is not nil, default is yellow warning icon.
})

-- update the dropdown
game:GetService("RunService").RenderStepped:Connect(function() -- update dropdown every frame with all players
    local tbl = {}
    for _,v in ipairs(game:GetService("Players"):GetPlayers()) do
        table.insert(tbl,v.Name)
    end
    MyDropdown:Update(tbl) -- uses namecalling, ":" instead of "."
end)


s1:CreateColorPicker({
    Name = "Color Picker"; -- required: name of element
    Flag = "ColorPicker"; -- required: unique flag name to use for element
    Default = Color3.fromRGB(0,255,0); -- required: Color3 that will be used when config saving is disabled or there is no saved configs
    Callback = function(newColor) -- optional: function to be called when the color is changed by the player
        print("Color changed to",tostring(newColor))
    end;
    SavingDisabled = false;
    -- Scroll to the bottom of the page to read more about the following two:
    Warning = "This has a warning"; -- optional: this argument is used in all elements (except for Body) and will indicate text that will appear when the player hovers over the warning icon
    WarningIcon = 12345; -- optional: ImageAssetId for warning icon, will only be used if Warning is not nil, default is yellow warning icon.
})

local MyDropdown2 = s2:CreateDropdown({
    Name = "Dropdown (without item selecting)"; -- required: name of element
    Callback = function(item) -- required: function to be called an item in the dropdown is activated
        print("Dropdown button pressed:",item)
    end;
    Options = {"Apple","Orange","Banana"}; -- required: dropdown options
    ItemSelecting = false; -- optional: whether to control item selecting behavior in dropdowns (see showcase video), is false by default
    -- Scroll to the bottom of the page to read more about the following two:
    Warning = "This has an error"; -- optional: this argument is used in all elements (except for Body) and will indicate text that will appear when the player hovers over the warning icon
    WarningIcon = Atlas.Icons.Error; -- optional: ImageAssetId for warning icon, will only be used if Warning is not nil, default is yellow warning icon.
}) -- the above has a valid WarningIcon ID which is why this is the only one that appears

s3:CreateSlider({ -- IMPORTANT: This function does not return anything, please modify flags directly in order to read or update toggle values. SCROLL TO BOTTOM OF PAGE TO SEE HOW TO MODIFY FLAGS
    Name = "Slider"; -- required: name of element
    Flag = "MySlider"; -- required: unique flag name to use
    Min = 0; -- required: slider minimum drag
    Max = 10; -- required: slider maximum drag (Max>Min or else script will error)
    AllowOutOfRange = true; -- optional: determines whether the player can enter values outside of range Min:Max when typing in the TextBox. If left nil, this is false
    Digits = 2; -- optional: digits for rounding when dragging or entering values, default is 0 (whole numbers)
    Default = 5; -- optional: default value for slider, will be used if config saving is disabled and there is no saved data, will be the Min value if left nil
    Callback = function(newValue) -- optional: function that will be called whenever slider flag is changed
        print("Slider:",newValue)
    end;
    -- Scroll to the bottom of the page to read more about the following two:
    Warning = "This has a warning"; -- optional: this argument is used in all elements (except for Body) and will indicate text that will appear when the player hovers over the warning icon
    WarningIcon = 12345; -- optional: ImageAssetId for warning icon, will only be used if Warning is not nil, default is yellow warning icon.
})
