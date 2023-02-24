--[[    KINETIC UI

    Author : Blissful#4492
    Finish Date : 26/2/22
    Documentation : https://blissful.gitbook.io/kinetic/
    GitRepo : https://github.com/Blissful4992/Kinetic

]]--

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/Kinetic"))()

local Overrides = {
    Background = Color3.fromRGB(23, 30, 51),
    Section_Background = Color3.fromRGB(18, 23, 38),

    Dark_Borders = Color3.fromRGB(18, 23, 38),
    Light_Borders = Color3.fromRGB(255, 255, 255),

    Text_Color = Color3.fromRGB(235, 235, 235),

    Accent = Color3.fromRGB(255, 81, 0),
    Dark_Accent = Color3.fromRGB(140, 45, 0),
}

local Window = Library.NewWindow({
    Text = "Test UI",

    WindowSize = Vector2.new(550, 450),     -- Initial Size of the Window
    WindowPosition = Vector2.new(400, 200), -- Initial Position of the Window

    ThemeOverrides = Overrides,
    Scalable = true, -- Default : True
    
    -- WindowSizeCallback will fire everytime the user changes the size of the UI, 
    -- you can use this to save the size into a config system for example
    WindowSizeCallback = function(new)
        print("You changed the window size to: " .. new.X .. ", " .. new.Y)
    end,

    -- WindowPositionCallback will fire everytime the user moves/drags the UI to a new position, 
    -- you can use this to save the position into a config system for example
    WindowPositionCallback = function(new)
        print("You moved the window to: " .. new.X .. ", " .. new.Y)
    end,

    -- CloseCallback will fire when the user presses the close button on the UI (Top Right)
    CloseCallback = function()
        print("You closed the script !")
    end
})

local Page = Window.NewPage({Text = "Page 1"})

local Section = Page.NewSection({Text = "Section 1"})

local Button = Section.NewButton({
    Text = "Click Me", 
    Callback = function()
        print("I got clicked !")
    end, 
    Description = "This can be used as a one time feature !"
})

local Toggle = Section.NewToggle({
    Text = "Toggle Me",
    Callback = function(bool)
        print(bool)
    end, 
    Default = true,
    Description = "This turns ON and OFF when you click it !"
})

local TextBox = Section.NewTextBox({
    Text = "Type", 
    PlaceHolderText = "Type !",
    Callback = function(text)
        print("New Input: " .. text)
    end, 

    Default = "Green",
    Description = "Type anything in this box !",

    OnlyNumeric = true,         -- Only Allow Numeric Output (Numbers)
    -- OnlyAlphabetic = true    -- Only Allow Alphabetic Output (Letters)
})

local Slider = Section.NewSlider({
    Text = "Slide Me",
    Callback = function(value)
        print("You slid to: " .. value)
    end,
    Default = 50,
    Min = 1, Max = 100,
    Decimals = 0, -- Number of decimal numbers to show after the period/comma
    Suffix = "m",
    Description = "You can slide me with your mouse to change the value !"
})

local Dropdown = Section.NewDropdown({
    Text = "Select Me", 
    Callback = function(option)
        print("You selected: " .. option)
    end, 
    Options = { -- Spoiler : Won't be in order
        "Red",
        "Green",
        "Blue"
    }, 
    Default = 2, -- Index of the default option (e.g. "Green")
    Description = "You can select a single item from this list !"
})

local Keybind = Section.NewKeybind({
    Text = "Press Me", 
    Callback = function()
        print("You pressed the right key !")
    end, 
    KeyCallback = function(new)
        print("You changed the key to: " .. string.sub(tostring(new), 14, #tostring(new)))
    end, 
    Default = Enum.KeyCode.X,
    Description = "Press the key to activate this !",
})

local Picker = Section.NewColorPicker({
    Text = "Pick Me", 
    Callback = function(color)
        print("You picked the new color: " .. color.R .. ", " .. color.G .. ", " .. color.B)
    end, 
    Default = Color3.fromRGB(0, 50, 0),
    Description = "Pick a new color from this little frame !"
})

local Chipset = Section.NewChipset({
    Text = "Select Me", 
    Callback = function(tbl)
        print("New Options:")
        for i,v in pairs(tbl) do
            print("    " .. tostring(i) .. ": " .. tostring(v))
        end
    end, 
    Options = {
        Switch1 = true,
        Switch2 = false,
        Switch3 = true
    }, 
    Description = "Select individual options from this little dropdown !"
})

local PlayerTbl = {}
local PlayerList = Section.NewPlayerChipset({
    Text = "Player List", 
    Callback = function(tbl) 
        PlayerTbl = tbl
    end, 
    Description = "Select individual players from this auto-updating list of players !"
})

for i = 1, 5 do
    Window.NewNotification({
        Title = "Ring-Ring",
        Body = "Hello, your pizza delivery is here ! That'll be a total of 5.50 $ ...",
        Time = math.random(2, 10)
    })
    task.wait(0.2)
end
