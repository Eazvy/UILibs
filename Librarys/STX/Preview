local Console =  loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/STX"))()
local ConsoleLog = Console:Window({
    Title = "[STX_Console] TEXT TITLE",
    Position = UDim2.new(0.5, 0, 0.5, 0),
    DragSpeed = 12
})
local Player = game.Players.LocalPlayer
local Char = Player.Character
local Humanoid = Char.Humanoid
local WaitDelay = 0.5
local StillWaiting = false
Humanoid:GetPropertyChangedSignal("Jump"):Connect(function()
    if StillWaiting == false then
        StillWaiting = true
        ConsoleLog:Prompt({
            Title = "HumanoidSignalJumped",
            TypesWeHave = {
                "default",
                "success",
                "fail",
                "warning",
                "nofitication"
            },
            Type = "default"
        })
        wait(WaitDelay)
        StillWaiting = false
    end
end)
ConsoleLog:Prompt({
    Title = "Your Text Here",
    TypesWeHave = {
        "default",
        "success",
        "fail",
        "warning",
        "nofitication"
    },
    Type = "default"
})
wait(1)
ConsoleLog:Prompt({
    Title = "Your Text Here",
    TypesWeHave = {
        "default",
        "success",
        "fail",
        "warning",
        "nofitication"
    },
    Type = "success"
})
wait(1)
ConsoleLog:Prompt({
    Title = "Your Text Here",
    TypesWeHave = {
        "default",
        "success",
        "fail",
        "warning",
        "nofitication"
    },
    Type = "fail"
})
wait(1)
ConsoleLog:Prompt({
    Title = "Your Text Here",
    TypesWeHave = {
        "default",
        "success",
        "fail",
        "warning",
        "nofitication"
    },
    Type = "warning"
})
wait(1)
ConsoleLog:Prompt({
    Title = "Your Text Here",
    TypesWeHave = {
        "default",
        "success",
        "fail",
        "warning",
        "nofitication"
    },
    Type = "nofitication"
})
