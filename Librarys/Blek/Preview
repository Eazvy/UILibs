local BlekLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/laderite/bleklib/main/library.lua"))()

local win = BlekLib:Create({
    Name = "Blek Library",
    StartupSound = {
        Toggle = false,
        SoundID = "rbxassetid://6958727243",
        TimePosition = 1
    }
})

local maintab = win:Tab('Main')
local charactertab = win:Tab('Character')
local uitab = win:Tab('UI')

uitab:Button('Destroy GUI', function()
    win:Exit()
end)


maintab:Toggle('Aimbot', function(v)
    aimbot = v
end)

maintab:Textbox('FOV', function(v)
    fov = v
end)

maintab:Slider('FOV', 30, function(v) -- default, 10 -- min, 300 -- max, function(a)
    print(a)
end)

maintab:Label('This is a label')


