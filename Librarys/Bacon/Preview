local lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/bacon"))()
local version, changelog = lib:GetInfo()
local window = lib:CreateWindow("BaconLib v"..version)
local label = lib:CreateLabel(window, "Main")
local textBox = lib:CreateTextBox(window, Enum.Font.Legacy, "Text", "Hello, World!")

local button = lib:CreateButton(window, "Print Text", function()
    print(textBox.Text)
end)

local toggled = false
local toggle = lib:CreateToggle(window, "Spam Warn 'Hello'", false, function(toggleState)
    toggled = not toggled
    while toggled and game:GetService('RunService').Heartbeat:Wait() do
        warn("Hello")
    end
end)

local drop = lib:CreateDropdown(window, "Dropdown")
lib:NewDropdownButton(window, drop, "Print 'LOL'", function()
   print("LOL")
end)

lib:NewDropdownButton(window, drop, "Print 'YES'", function()
   print("YES")
end)

lib:NewDropdownButton(window, drop, "Warn 'XD'", function()
   warn("XD")
end)

local slider = lib:CreateSlider(window, "Print Value", 0, 100, 50, function(value)
    print(value)
end)

local keybind = lib:CreateKeyBind(window, "Print Key", "z", function(key)
    print(key)
end)
