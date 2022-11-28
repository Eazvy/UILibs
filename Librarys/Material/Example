-- Example made by twink marie
local Material = loadstring(game:HttpGet("https://raw.githubusercontent.com/Kinlei/MaterialLua/master/Module.lua"))()

local X = Material.Load({
    Title = "ChibuHub",
    Style = 3,
    SizeX = 500,
    SizeY = 350,
    Theme = "Light",
    ColorOverrides = {
        MainFrame = Color3.fromRGB(235,235,235)
    }
})

local Y = X.New({
    Title = "1"
})

local Z = X.New({
    Title = "2"
})

local A = Y.Button({
    Text = "Kill All",
    Callback = function()
        print("hello")
    end,
    Menu = {
        Information = function(self)
            X.Banner({
                Text = "This function can get you banned in up-to-date servers; use at your own risk."
            })
        end
    }
})

local B = Y.Toggle({
    Text = "I'm a switch",
    Callback = function(Value)
        print(Value)
    end,
    Enabled = false
})

local C = Y.Slider({
    Text = "Slip and... you get the idea",
    Callback = function(Value)
        print(Value)
    end,
    Min = 200,
    Max = 400,
    Def = 300
})

local D = Y.Dropdown({
    Text = "Dropping care package",
    Callback = function(Value)
        print(Value)
    end,
    Options = {
        "Floor 1",
        "Floor 2",
        "Floor 3",
        "Floor 4",
        "Floor 5"
    },
    Menu = {
        Information = function(self)
            X.Banner({
                Text = "Test alert!"
            })
        end
    }
})

local E = Y.ChipSet({
    Text = "Chipping away",
    Callback = function(ChipSet)
        table.foreach(ChipSet, function(Option, Value)
            print(Option, Value)
        end)
    end,
    Options = {
        ESP = true,
        TeamCheck = false,
        UselessBool = {
            Enabled = true,
            Menu = {
                Information = function(self)
                    X.Banner({
                        Text = "This bool has absolutely no purpose whatsoever."
                    })
                end
            }
        }
    }
})

local F = Y.DataTable({
    Text = "Chipping away",
    Callback = function(ChipSet)
        table.foreach(ChipSet, function(Option, Value)
            print(Option, Value)
        end)
    end,
    Options = {
        ESP2 = true,
        TeamCheck2 = false,
        UselessBool2 = {
            Enabled = true,
            Menu = {
                Information = function(self)
                    X.Banner({
                        Text = "This bool ALSO has absolutely no purpose. Sorry."
                    })
                end
            }
        }
    }
})

local G = Y.ColorPicker({
    Text = "ESP Colour",
    Default = Color3.fromRGB(0,255,110),
    Callback = function(Value)
        print("RGB:", Value.R * 255, Value.G * 255, Value.B * 255)
    end,
    Menu = {
        Information = function(self)
            X.Banner({
                Text = "This changes the color of your ESP."
            })
        end
    }
})

local H = Y.TextField({
    Text = "Country",
    Callback = function(Value)
        print(Value)
    end,
    Menu = {
        GB = function(self)
            self.SetText("GB")
        end,
        JP = function(self)
            self.SetText("JP")
        end,
        KO = function(self)
            self.SetText("KO")
        end
    }
})
