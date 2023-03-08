local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/laagginq/ui-libraries/main/ven/src.lua"))()
local window = Library:Window("Test")
local tab1 = window:Tab("Tab 1")
local tab2 = window:Tab("Tab 2")
tab1:Button("Hello",function()
    print("World!")    
end)

tab1:Toggle("Toggle1",function(v)
    print("Toggle 1 set to: "..v)    
end)

tab1:Slider("Slider1",1,10,5,function(v)
    print("Slider 1 set to: "..v)    
end)

tab1:Slider("Dropdown",{"1","2","3","4","5"},function(v)
    print(v)    
end)

tab1:Textbox("Textbox",true,function(v)
    print(v)    
end)
