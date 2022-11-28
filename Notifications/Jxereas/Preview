local Notification = loadstring(game:HttpGet("https://raw.githubusercontent.com/Jxereas/UI-Libraries/main/notification_gui_library.lua", true))()

Notification.new("error", "Error Heading", "Error body message.") -- Args(<string> Type, <string> Heading, <string> Body, <boolean?> AutoRemoveNotif, <number?> AutoRemoveTime, <function?> OnCloseFunction)
Notification.new("success", "Success Heading", "Success body message.") -- Args(<string> Type, <string> Heading, <string> Body, <boolean?> AutoRemoveNotif, <number?> AutoRemoveTime, <function?> OnCloseFunction)
Notification.new("info", "Information Heading", "Information body message.") -- Args(<string> Type, <string> Heading, <string> Body, <boolean?> AutoRemoveNotif, <number?> AutoRemoveTime, <function?> OnCloseFunction)
Notification.new("warning", "Warning Heading", "Warning body message.") -- Args(<string> Type, <string> Heading, <string> Body, <boolean?> AutoRemoveNotif, <number?> AutoRemoveTime, <function?> OnCloseFunction)
Notification.new("message", "Message Heading", "Message body message.") -- Args(<string> Type, <string> Heading, <string> Body, <boolean?> AutoRemoveNotif, <number?> AutoRemoveTime, <function?> OnCloseFunction)

local notif = Notification.new("success", "Success", "Success body message.")
notif:changeHeading("New Heading") -- Args(<string> NewHeading)
notif:changeBody("New Body") -- Args(<string> NewBody)
notif:deleteTimeout(3) -- Args(<number> DeleteWaitTime)
notif:delete()
