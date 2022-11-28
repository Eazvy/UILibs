_G.CustomTheme = {
	Tab_Color = Color3.fromRGB(255, 255, 255),
    Tab_Text_Color = Color3.fromRGB(0, 0, 0),
    Description_Color = Color3.fromRGB(255, 255, 255),
    Description_Text_Color = Color3.fromRGB(0, 0, 0),
    Container_Color = Color3.fromRGB(255, 255, 255),
    Container_Text_Color = Color3.fromRGB(0, 0, 0),
    Button_Text_Color = Color3.fromRGB(0, 0, 0),
    Toggle_Box_Color = Color3.fromRGB(243, 243, 243),
    Toggle_Inner_Color = Color3.fromRGB(94, 255, 180),
    Toggle_Text_Color = Color3.fromRGB(0, 0, 0),
    Toggle_Border_Color = Color3.fromRGB(225, 225, 225),
    Slider_Bar_Color = Color3.fromRGB(243, 243, 243),
    Slider_Inner_Color = Color3.fromRGB(94, 255, 180),
    Slider_Text_Color = Color3.fromRGB(0, 0, 0),
	Slider_Border_Color = Color3.fromRGB(255, 255, 255),
    Dropdown_Text_Color = Color3.fromRGB(0, 0, 0),
    Dropdown_Option_BorderSize = 1,
    Dropdown_Option_BorderColor = Color3.fromRGB(235, 235, 235),
    Dropdown_Option_Color = Color3.fromRGB(255, 255, 255),
    Dropdown_Option_Text_Color = Color3.fromRGB(0, 0, 0)
}

local Library = loadstring(game:HttpGet("https://pastebin.com/raw/2xDTKdpV", true))()

local AimbotTab = Library:CreateTab("Aimbot", "This is where you modify the Aimbot")

AimbotTab:CreateTextbox("Whitelist Player", function(arg) --arg is what the text is inside the textbox
    print("Whitelisted: " .. arg)
end)

AimbotTab:CreateButton("Inf Jump", function() --you dont need "arg" for a button
    print("Inf Jump is now permanently on.")
end)


AimbotTab:CreateSlider("Fov Radius", 0, 600, function(arg) --the (arg) is the sliders value
    print("Fov Radius is set to:", arg)
end)

AimbotTab:CreateDropDown("Aimbot Part", {"Head", "Torso"}, function(arg) --the (arg) is the option you choose 
    if arg == "Head" then
        print("HEahshoot")
    elseif arg == "Torso" then
        print("trrrrso")
    end
end)

AimbotTab:CreateToggle("Enable Aimbot", function(arg) --the (arg) is if the checkbox is toggled or not
    if arg then
        print("Aimbot is now : Enabled")
    else
        print("Aimbot is now : Disabled")
    end
end)
