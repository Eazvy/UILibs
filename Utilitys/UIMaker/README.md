# Instance maker module
Made by SALFIIN#2470

# Importing the module into ur library
so we need to just make loadstring to the module source

```lua
local Module = loadstring(game:HttpGet("https://github.com/slf0Dev/my-ui-library-making-utility/raw/main/InstanceMaker.lua"))();
```

# Functions
there is only one function named "Instance", it creates instance that you need.
how to use it?

```lua
local Module = loadstring(game:HttpGet("https://github.com/slf0Dev/my-ui-library-making-utility/raw/main/InstanceMaker.lua"))(); -- this is our loadstring to module that we got on 1st step

local Frame = Module.Instance(instance : string ,properties : table) -- returns an created instance
```

# Special

you can add UICorner to the instance you created in 1 line,
just add an "CornerRadius" property and set the radius you need.

# Example
there is an example:

```lua
local Module = loadstring(game:HttpGet("https://github.com/slf0Dev/my-ui-library-making-utility/raw/main/InstanceMaker.lua"))();

local Screengui = Module.Instance("ScreenGui" ,{
  Parent = game.CoreGui;
  Name = "Example"
})

local CornerFrame = Module.Instance("Frame",{
  Parent = Screengui;
  Name = "CornerFrame";
  BackgroundColor3 = Color3.fromRGB(0,255,0);
  BackgroundTransparency = 0;
  CornerRadius = UDim.new(0,100);
  Position = UDim2.new(0.45,0,0.5,0);
  Size = UDim2.new(0,50,0,50)
})

local SimpleFrame = Module.Instance("Frame",{
  Parent = Screengui;
  Name = "SimpleFrame";
  BackgroundColor3 = Color3.fromRGB(0,0,255);
  BackgroundTransparency = 0;
  Position = UDim2.new(0.5,0,0.5,0);
  Size = UDim2.new(0,50,0,50)
})
```


