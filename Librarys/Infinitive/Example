--Lib
local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/Hosvile/Refinement/main/InfinitiveUI",true))()

--Create Window
--Lib:CreateWindow(name,DefTab,WinSize,function)
local Win = Lib:CreateWindow("ah",1,nil,nil)

for i = 1, 16 do

--Create Tab
local Tab,name = Win:CreateTab("Tab "..tostring(i),function() warn(i) end)

Tab:CreateButton("Infinite yield",function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source",true))()
	end)

Tab:CreateButton("Console",function()
	game:GetService("StarterGui"):SetCore("DevConsoleVisible",true)
	end)

for i = 1, i do


--Returns UI
--Tab:CreateButton(name,function)
	
Tab:CreateButton("Button "..i,function()
	print(i,name)
	end)


--Returns bool,UI
--Tab:CreateToggle(name,default,function)
	
Tab:CreateToggle("Toggle "..i,false,function(t)
	print(i,name,t)
	end)


--Returns value,UI
--Tab:CreateSlider(name,min,max,default,function)

local max = math.random(500,5000)
Tab:CreateSlider("Slider "..i,50,max,max/math.random(2,6),function(v)
	print(i,name,v)
	end)


--Returns two userdata,UI
--Tab:CreateDropdown(name,{table,string},visible,function)

Tab:CreateDropdown("Dropdown "..i, {{
	"Named", {}},"hello","he","ah","eh","yw"
},false,function(c,f)
	print(i,name,c,f)
	end)


--Returns TextBox for FocusLost or Stretchability
local Textbox = Tab:CreateTextbox("TextBox "..i,"FFlag")

Textbox:GetPropertyChangedSignal("Text"):Connect(function()
	local self = Textbox
	print(self.Text)
	end)


end
end
