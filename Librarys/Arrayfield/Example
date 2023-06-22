local Rayfield = loadstring(game:HttpGet('https://raw.githubusercontent.com/UI-Interface/CustomFIeld/main/RayField.lua'))()
local Window = Rayfield:CreateWindow({
   Name = "Arrayfield Example Window",
   LoadingTitle = "Arrayfield Interface Suite",
   LoadingSubtitle = "by Arrays",
   ConfigurationSaving = {
      Enabled = true,
      FolderName = nil, -- Create a custom folder for your hub/game
      FileName = "Arrayfield"
   },
   Discord = {
      Enabled = false,
      Invite = "sirius", -- The Discord invite code, do not include discord.gg/
      RememberJoins = true -- Set this to false to make them join the discord every time they load it up
   },
   KeySystem = true, -- Set this to true to use our key system
   KeySettings = {
      Title = "Arrayfield",
      Subtitle = "Key System",
      Note = "Join the discord (discord.gg/sirius)",
      FileName = "SiriusKey",
      SaveKey = false,
      GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
      Key = "Hello"
   }
})
local Tab = Window:CreateTab("Tab Example", 4483362458) -- Title, Image
local Tab2 = Window:CreateTab("Tab Example 2") -- Title, Image
local Section = Tab:CreateSection("Section Example",false) -- The 2nd argument is to tell if its only a Title and doesnt contain element
local Button = Tab:CreateButton({
   Name = "Button Example",
   Info = "Button info/Description.", -- Speaks for itself, Remove if none.
   Interact = 'Changable',
   Callback = function()
   print('Pressed')
   end,
})
local Toggle = Tab:CreateToggle({
   Name = "Toggle Example",
   Info = "Toggle info/Description.", -- Speaks for itself, Remove if none.
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
      print(Value)
   end,
})
local ColorPicker = Tab:CreateColorPicker({
	Name = "Color Picker",
	Info = 'info or description',
	Color = Color3.fromRGB(2,255,255),
	Flag = "ColorPicker1", 
	Callback = function(Value)
		print(Value)
	end
})
local Slider = Tab:CreateSlider({
   Name = "Slider Example",
   Info = "Button info/Description.",
   Range = {0, 100},
   Increment = 10,
   Suffix = "Bananas",
   CurrentValue = 10,
   Flag = "Slider1", 
   Callback = function(Value)
      print(Value)
   end,
})
local Section2 = Tab:CreateSection("Inputs Examples",true)
Tab:CreateInput({
   Name = "Numbers Only",
   Info = "Input info/Description.",
   PlaceholderText = "Amount",
   NumbersOnly = true,
   OnEnter = true,
   RemoveTextAfterFocusLost = true,
   Callback = function(Text)
      print(Text)
   end,
})
Tab:CreateInput({
   Name = "11 Characters Limit",
   Info = "Input info/Description.",
   PlaceholderText = "Text",
   CharacterLimit = 15,
   RemoveTextAfterFocusLost = true,
   Callback = function(Text)
      print(Text)
   end,
})
Tab:CreateInput({
   Name = "No RemoveTextAfterFocusLost",
   Info = "Input info/Description.",
   PlaceholderText = "Input",
   RemoveTextAfterFocusLost = false,
   Callback = function(Text)
      print(Text)
   end,
})
local Section3= Tab:CreateSection("Dropdown Examples",true)
local MultiSelectionDropdown = Tab:CreateDropdown({
   Name = "Multi Selection",
   Options = {"Option 1","Option 2",'Option 3'},
   CurrentOption = {"Option 1","Option 3"} ,
   MultiSelection = true,
   Flag = "Dropdown1",
   Callback = function(Option)
    print(Option)
   end,
})
local SingleSelection = Tab:CreateDropdown({
   Name = "Single Selection",
   Options = {"Option 1","Option 2"},
   CurrentOption = "Option 1",
   MultiSelection = false,
   Flag = "Dropdown2", 
   Callback = function(Option)
    print(Option)
   end,
})
local Label = Tab:CreateLabel("Thanks for using Arrayfield, there were alot of issues but here we are!",Section)
local Paragraph = Tab:CreateParagraph({Title = "Paragraph Example", Content = "Paragraph Example"},Section)
local Sets = Tab:CreateSection('Set Functions',false)
local SButton
SButton = Tab:CreateButton({
   Name = "Button Example",
   Interact = 'Interact',
   SectionParent = Sets,
   Callback = function()
    SButton:Set(nil,'New Interaction')
   end
})
 Tab:CreateButton({
   Name = "Dropdown Set",
   Interact = 'Interact',
   SectionParent = Sets,
   Callback = function()
   SingleSelection:Set('Option 1')
   end
})

local LockTesting = Tab:CreateSection('Lockdown Section',false)
local ToLock = {}
Tab:CreateToggle({
   Name = "Lockdown",
   SectionParent = LockTesting,
   Info = "Toggle info/Description.", -- Speaks for itself, Remove if none.
   CurrentValue = false,
   Callback = function(Value)
    if Value then
     for _,v in ToLock do
     v:Lock('Locked')
     end
     else
      for _,v in ToLock do
          v:Unlock('Locked')
       end
    end
   end,
})
 ToLock.Button = Tab:CreateButton({
   SectionParent = LockTesting,
   Name = "Button Example",
   Info = "Button info/Description.", -- Speaks for itself, Remove if none.
   Interact = 'Interact',
   Callback = function()
   print('Pressed')
   end,
})
ToLock.Toggle = Tab:CreateToggle({
   SectionParent = LockTesting,
   Name = "Toggle Example",
   Info = "Toggle info/Description.", -- Speaks for itself, Remove if none.
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
      print(Value)
   end,
})
ToLock.ColorPicker = Tab:CreateColorPicker({
	Name = "Color Picker",
	Info = 'info or description',
	SectionParent = LockTesting,
	Color = Color3.fromRGB(2,255,255),
	Flag = "ColorPicker1", 
	Callback = function(Value)
		print(Value)
	end
})
ToLock.Slider = Tab:CreateSlider({
   SectionParent = LockTesting,
   Name = "Slider Example",
   Info = "Button info/Description.",
   Range = {0, 100},
   Increment = 10,
   Suffix = "Bananas",
   CurrentValue = 10,
   Flag = "Slider1", 
   Callback = function(Value)
      print(Value)
   end,
})
