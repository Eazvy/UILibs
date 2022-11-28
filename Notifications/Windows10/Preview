local MessageBox = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/NotificationGUI/main/source.lua"))()


--[[
   MessageBoxIcons:
      • Question
      • Error
      • Warning

   MessageBoxButtons:
      • YesNo
      • OKCancel
      • OK
--]]
-- AnchorPoint is 0.5,0.5
MessageBox.Show({Position = UDim2.new(0.5,0,0.5,0), Text = "Notification UI", Description = "Windows 10 MessageBox\nMade by : xHeptc\n \nDo you like this?", MessageBoxIcon = "Question", MessageBoxButtons = "YesNo", Result = function(res)
   if (res == "Yes") then
       MessageBox.Show({MessageBoxButtons = "OK", Description = "Wow, you said Yes! Thank you", Text = "YAYYY!"})
   elseif (res == "No") then
       MessageBox.Show({MessageBoxButtons = "OK", Description = "Ahh, sorry to dissapoint, I'll try better next time!", Text = "Nooooo"})
   end
end})
