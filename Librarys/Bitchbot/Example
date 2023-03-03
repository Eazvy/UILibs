local menu
local MenuName = isfile("bitchbot/menuname.txt") and readfile("bitchbot/menuname.txt") or nil
local loadstart = tick()

local function map(X, A, B, C, D)
	return (X - A) / (B - A) * (D - C) + C
end

do
	local notes = {}
	local function DrawingObject(t, col)
		local d = Drawing.new(t)

		d.Visible = true
		d.Transparency = 1
		d.Color = col

		return d
	end

	local function Rectangle(sizex, sizey, fill, col)
		local s = DrawingObject("Square", col)

		s.Filled = fill
		s.Thickness = 1
		s.Position = Vector2.new()
		s.Size = Vector2.new(sizex, sizey)

		return s
	end

	local function Text(text)
		local s = DrawingObject("Text", Color3.new(1, 1, 1))

		s.Text = text
		s.Size = 13
		s.Center = false
		s.Outline = true
		s.Position = Vector2.new()
		s.Font = 2

		return s
	end

	function CreateNotification(t, customcolor) -- TODO i want some kind of prioritized message to the notification list, like a warning or something. warnings have icons too maybe? idk??
		local gap = 25
		local width = 18

		local alpha = 255
		local time = 0
		local estep = 0
		local eestep = 0.02

		local insety = 0

		local Note = {

			enabled = true,

			targetPos = Vector2.new(50, 33),

			size = Vector2.new(200, width),

			drawings = {
				outline = Rectangle(202, width + 2, false, Color3.new(0, 0, 0)),
				fade = Rectangle(202, width + 2, false, Color3.new(0, 0, 0)),
			},

			Remove = function(self, d)
				if d.Position.x < d.Size.x then
					for k, drawing in pairs(self.drawings) do
						drawing:Remove()
						drawing = false
					end
					self.enabled = false
				end
			end,

			Update = function(self, num, listLength, dt)
				local pos = self.targetPos

				local indexOffset = (listLength - num) * gap
				if insety < indexOffset then
					insety -= (insety - indexOffset) * 0.2
				else
					insety = indexOffset
				end
				local size = self.size

				local tpos = Vector2.new(pos.x - size.x / time - map(alpha, 0, 255, size.x, 0), pos.y + insety)
				self.pos = tpos

				local locRect = {
					x = math.ceil(tpos.x),
					y = math.ceil(tpos.y),
					w = math.floor(size.x - map(255 - alpha, 0, 255, 0, 70)),
					h = size.y,
				}
				--pos.set(-size.x / fc - map(alpha, 0, 255, size.x, 0), pos.y)

				local fade = math.min(time * 12, alpha)
				fade = fade > 255 and 255 or fade < 0 and 0 or fade

				if self.enabled then
					local linenum = 1
					for i, drawing in pairs(self.drawings) do
						drawing.Transparency = fade / 255

						if type(i) == "number" then
							drawing.Position = Vector2.new(locRect.x + 1, locRect.y + i)
							drawing.Size = Vector2.new(locRect.w - 2, 1)
						elseif i == "text" then
							drawing.Position = tpos + Vector2.new(6, 2)
						elseif i == "outline" then
							drawing.Position = Vector2.new(locRect.x, locRect.y)
							drawing.Size = Vector2.new(locRect.w, locRect.h)
						elseif i == "fade" then
							drawing.Position = Vector2.new(locRect.x - 1, locRect.y - 1)
							drawing.Size = Vector2.new(locRect.w + 2, locRect.h + 2)
							local t = (200 - fade) / 255 / 3
							drawing.Transparency = t < 0.4 and 0.4 or t
						elseif i:find("line") then
							drawing.Position = Vector2.new(locRect.x + linenum, locRect.y + 1)
							if menu then
								local mencol = customcolor or (
										Color3.fromRGB(127, 72, 163)
									)
								local color = linenum == 1 and mencol or Color3.fromRGB(mencol.R * 255 - 40, mencol.G * 255 - 40, mencol.B * 255 - 40) -- super shit
								if drawing.Color ~= color then
									drawing.Color = color
								end
							end
							linenum += 1
						end
					end

					time += estep * dt * 128 -- TODO need to do the duration
					estep += eestep * dt * 64
				end
			end,

			Fade = function(self, num, len, dt)
				if self.pos.x > self.targetPos.x - 0.2 * len or self.fading then
					if not self.fading then
						estep = 0
					end
					self.fading = true
					alpha -= estep / 4 * len * dt * 50
					eestep += 0.01 * dt * 100
				end
				if alpha <= 0 then
					self:Remove(self.drawings[1])
				end
			end,
		}

		for i = 1, Note.size.y - 2 do
			local c = 0.28 - i / 80
			Note.drawings[i] = Rectangle(200, 1, true, Color3.new(c, c, c))
		end
		local color =  Color3.fromRGB(127, 72, 163)

		Note.drawings.text = Text(t)
		if Note.drawings.text.TextBounds.x + 7 > Note.size.x then -- expand the note size to fit if it's less than the default size
			Note.size = Vector2.new(Note.drawings.text.TextBounds.x + 7, Note.size.y)
		end
		Note.drawings.line = Rectangle(1, Note.size.y - 2, true, color)
		Note.drawings.line1 = Rectangle(1, Note.size.y - 2, true, color)

		notes[#notes + 1] = Note
	end

	renderStepped = game.RunService.RenderStepped:Connect(function(dt)
		Camera = workspace.CurrentCamera
		local smallest = math.huge
		for k = 1, #notes do
			local v = notes[k]
			if v and v.enabled then
				smallest = k < smallest and k or smallest
			else
				table.remove(notes, k)
			end
		end
		local length = #notes
		for k = 1, #notes do
			local note = notes[k]
			note:Update(k, length, dt)
			if k <= math.ceil(length / 10) or note.fading then
				note:Fade(k, length, dt)
			end
		end
	end)
	--ANCHOR how to create notification
	--CreateNotification("Loading...")
end

--!SECTION

local menuWidth, menuHeight = 500, 600
menu = { -- this is for menu stuffs n shi
	w = menuWidth,
	h = menuHeight,
	x = 0,
	y = 0,
	columns = {
		width = (menuWidth - 40) / 2,
		left = 17,
		right = (menuWidth - 20) / 2 + 13,
	},
	activetab = 1,
	open = true,
	fadestart = 0,
	fading = false,
	mousedown = false,
	postable = {},
	options = {},
	clrs = {
		norm = {},
		dark = {},
		togz = {},
	},
	mc = { 127, 72, 163 },
	watermark = {},
	connections = {},
	list = {},
	unloaded = false,
	copied_clr = nil,
	game = "uni",
	tabnames = {}, -- its used to change the tab num to the string (did it like this so its dynamic if u add or remove tabs or whatever :D)
	friends = {},
	priority = {},
	muted = {},
	spectating = false,
	stat_menu = false,
	load_time = 0,
	log_multi = nil,
	mgrouptabz = {},
	backspaceheld = false,
	backspacetime = -1,
	backspaceflags = 0,
	selectall = false,
	modkeys = {
		alt = {
			direction = nil,
		},
		shift = {
			direction = nil,
		},
	},
	modkeydown = function(self, key, direction)
		local keydata = self.modkeys[key]
		return keydata.direction and keydata.direction == direction or false
	end,
	keybinds = {},
	values = {}
}

local function round(num, numDecimalPlaces)
	local mult = 10 ^ (numDecimalPlaces or 0)
	return math.floor(num * mult + 0.5) / mult
end

local function average(t)
	local sum = 0
	for _, v in pairs(t) do -- Get the sum of all numbers in t
		sum = sum + v
	end
	return sum / #t
end

local function clamp(a, lowerNum, higher) -- DONT REMOVE this clamp is better then roblox's because it doesnt error when its not lower or heigher
	if a > higher then
		return higher
	elseif a < lowerNum then
		return lowerNum
	else
		return a
	end
end

local function CreateThread(func, ...) -- improved... yay.
	local thread = coroutine.create(func)
	coroutine.resume(thread, ...)
	return thread
end

local function MultiThreadList(obj, ...)
	local n = #obj
	if n > 0 then
		for i = 1, n do
			local t = obj[i]
			if type(t) == "table" then
				local d = #t
				assert(d ~= 0, "table inserted was not an array or was empty")
				assert(d < 3, ("invalid number of arguments (%d)"):format(d))
				local thetype = type(t[1])
				assert(
					thetype == "function",
					("invalid argument #1: expected 'function', got '%s'"):format(tostring(thetype))
				)

				CreateThread(t[1], unpack(t[2]))
			else
				CreateThread(t, ...)
			end
		end
	else
		for i, v in pairs(obj) do
			CreateThread(v, ...)
		end
	end
end

local DeepRestoreTableFunctions, DeepCleanupTable

DeepRestoreTableFunctions = function(tbl)
	for k, v in next, tbl do
		if type(v) == "function" and is_synapse_function(v) then
			for k1, v1 in next, getupvalues(v) do
				if type(v1) == "function" and islclosure(v1) and not is_synapse_function(v1) then
					tbl[k] = v1
				end
			end
		end

		if type(v) == "table" then
			DeepRestoreTableFunctions(v)
		end
	end
end

DeepCleanupTable = function(tbl)
	local numTable = #tbl
	local isTableArray = numTable > 0
	if isTableArray then
		for i = 1, numTable do
			local entry = tbl[i]
			local entryType = type(entry)

			if entryType == "table" then
				DeepCleanupTable(tbl)
			end

			tbl[i] = nil
			entry = nil
			entryType = nil
		end
	else
		for k, v in next, tbl do
			if type(v) == "table" then
				DeepCleanupTable(tbl)
			end
		end

		tbl[k] = nil
	end

	numTable = nil
	isTableArray = nil
end

local event = {}

local allevent = {}

function event.new(eventname, eventtable, requirename) -- fyi you can put in a table of choice to make the table you want an "event" pretty cool its like doing & in c lol!
	if eventname then
		assert(
			allevent[eventname] == nil,
			("the event '%s' already exists in the event table"):format(eventname)
		)
	end
	local newevent = eventtable or {}
	local funcs = {}
	local disconnectlist = {}
	function newevent:fire(...)
		allevent[eventname].fire(...)
	end
	function newevent:connect(func)
		funcs[#funcs + 1] = func
		local disconnected = false
		local function disconnect()
			if not disconnected then
				disconnected = true
				disconnectlist[func] = true
			end
		end
		return disconnect
	end

	local function fire(...)
		local n = #funcs
		local j = 0
		for i = 1, n do
			local func = funcs[i]
			if disconnectlist[func] then
				disconnectlist[func] = nil
			else
				j = j + 1
				funcs[j] = func
			end
		end
		for i = j + 1, n do
			funcs[i] = nil
		end
		for i = 1, j do
			CreateThread(function(...)
				pcall(funcs[i], ...)
			end, ...)
		end
	end

	if eventname then
		allevent[eventname] = {
			event = newevent,
			fire = fire,
		}
	end

	return newevent, fire
end

local function FireEvent(eventname, ...)
	if allevent[eventname] then
		return allevent[eventname].fire(...)
	else
		--warn(("Event %s does not exist!"):format(eventname))
	end
end

local function GetEvent(eventname)
	return allevent[eventname]
end

local BBOT_IMAGES = {}
MultiThreadList({
	function()
		BBOT_IMAGES[1] = game:HttpGet("https://i.imgur.com/9NMuFcQ.png")
	end,
	function()
		BBOT_IMAGES[2] = game:HttpGet("https://i.imgur.com/jG3NjxN.png")
	end,
	function()
		BBOT_IMAGES[3] = game:HttpGet("https://i.imgur.com/2Ty4u2O.png")
	end,
	function()
		BBOT_IMAGES[4] = game:HttpGet("https://i.imgur.com/kNGuTlj.png")
	end,
	function()
		BBOT_IMAGES[5] = game:HttpGet("https://i.imgur.com/OZUR3EY.png")
	end,
	function()
		BBOT_IMAGES[6] = game:HttpGet("https://i.imgur.com/3HGuyVa.png")
	end,
})

-- MULTITHREAD DAT LOADING SO FAST!!!!
local loaded = {}
do
	local function Loopy_Image_Checky()
		for i = 1, 6 do
			local v = BBOT_IMAGES[i]
			if v == nil then
				return true
			elseif not loaded[i] then
				loaded[i] = true
			end
		end
		return false
	end
	while Loopy_Image_Checky() do
		wait(0)
	end
end

loadstart = tick()

-- nate i miss u D:
-- im back
local NETWORK = game:service("NetworkClient")
local NETWORK_SETTINGS = settings().Network
NETWORK:SetOutgoingKBPSLimit(0)

setfpscap(maxfps or 144)

if not isfolder("bitchbot") then
	makefolder("bitchbot")
	if not isfile("bitchbot/relations.bb") then
		writefile("bitchbot/relations.bb", "bb:{{friends:}{priority:}")
	end
else
	if not isfile("bitchbot/relations.bb") then
		writefile("bitchbot/relations.bb", "bb:{{friends:}{priority:}")
	end
	writefile("bitchbot/debuglog.bb", "")
end

if not isfolder("bitchbot/" .. menu.game) then
	makefolder("bitchbot/" .. menu.game)
end

local configs = {}

local function GetConfigs()
	local result = {}
	local directory = "bitchbot\\" .. menu.game
	for k, v in pairs(listfiles(directory)) do
		local clipped = v:sub(#directory + 2)
		if clipped:sub(#clipped - 2) == ".bb" then
			clipped = clipped:sub(0, #clipped - 3)
			result[k] = clipped
			configs[k] = v
		end
	end
	if #result <= 0 then
		writefile("bitchbot/" .. menu.game .. "/Default.bb", "")
	end
	return result
end

local Players = game:GetService("Players")
local stats = game:GetService("Stats")

local function UnpackRelations()
	local str = isfile("bitchbot/relations.bb") and readfile("bitchbot/relations.bb") or nil
	local final = {
		friends = {},
		priority = {},
	}
	if str then
		if str:find("bb:{{") then
			writefile("bitchbot/relations.bb", "friends:\npriority:")
			return
		end

		local friends, frend = str:find("friends:")
		local priority, priend = str:find("\npriority:")
		local friendslist = str:sub(frend + 1, priority - 1)
		local prioritylist = str:sub(priend + 1)
		for i in friendslist:gmatch("[^,]+") do
			if not table.find(final.friends, i) then
				table.insert(final.friends, i)
			end
		end
		for i in prioritylist:gmatch("[^,]+") do
			if not table.find(final.priority, i) then
				table.insert(final.priority, i)
			end
		end
	end
	if not menu then
		repeat
			game.RunService.Heartbeat:Wait()
		until menu
	end
	menu.friends = final.friends
	if not table.find(menu.friends, Players.LocalPlayer.Name) then
		table.insert(menu.friends, Players.LocalPlayer.Name)
	end
	menu.priority = final.priority
end

local function WriteRelations()
	local str = "friends:"

	for k, v in next, menu.friends do
		local playerobj
		local userid
		local pass, ret = pcall(function()
			playerobj = Players[v]
		end)

		if not pass then
			local newpass, newret = pcall(function()
				userid = v
			end)
		end

		if userid then
			str ..= tostring(userid) .. ","
		else
			str ..= tostring(playerobj.Name) .. ","
		end
	end

	str ..= "\npriority:"

	for k, v in next, menu.priority do
		local playerobj
		local userid
		local pass, ret = pcall(function()
			playerobj = Players[v]
		end)

		if not pass then
			local newpass, newret = pcall(function()
				userid = v
			end)
		end

		if userid then
			str ..= tostring(userid) .. ","
		else
			str ..= tostring(playerobj.Name) .. ","
		end
	end

	writefile("bitchbot/relations.bb", str)
end
CreateThread(function()
	if (not menu or not menu.GetVal) then
		repeat
			game.RunService.Heartbeat:Wait()
		until (menu and menu.GetVal)
	end
	wait(2)
	UnpackRelations()
	WriteRelations()
end)

local LOCAL_PLAYER = Players.LocalPlayer
local LOCAL_MOUSE = LOCAL_PLAYER:GetMouse()
local TEAMS = game:GetService("Teams")
local INPUT_SERVICE = game:GetService("UserInputService")
local GAME_SETTINGS = UserSettings():GetService("UserGameSettings")
local CACHED_VEC3 = Vector3.new()
local Camera = workspace.CurrentCamera
local SCREEN_SIZE = Camera.ViewportSize
local ButtonPressed = event.new("bb_buttonpressed")
local TogglePressed = event.new("bb_togglepressed")
local MouseMoved = event.new("bb_mousemoved")

menu.x = math.floor((SCREEN_SIZE.x / 2) - (menu.w / 2))
menu.y = math.floor((SCREEN_SIZE.y / 2) - (menu.h / 2))

local Lerp = function(delta, from, to) -- wtf why were these globals thats so exploitable!
	if (delta > 1) then
		return to
	end
	if (delta < 0) then
		return from
	end
	return from + (to - from) * delta
end

local ColorRange = function(value, ranges) -- ty tony for dis function u a homie
	if value <= ranges[1].start then
		return ranges[1].color
	end
	if value >= ranges[#ranges].start then
		return ranges[#ranges].color
	end

	local selected = #ranges
	for i = 1, #ranges - 1 do
		if value < ranges[i + 1].start then
			selected = i
			break
		end
	end
	local minColor = ranges[selected]
	local maxColor = ranges[selected + 1]
	local lerpValue = (value - minColor.start) / (maxColor.start - minColor.start)
	return Color3.new(
		Lerp(lerpValue, minColor.color.r, maxColor.color.r),
		Lerp(lerpValue, minColor.color.g, maxColor.color.g),
		Lerp(lerpValue, minColor.color.b, maxColor.color.b)
	)
end

local bVector2 = {}
do -- vector functions
	function bVector2:getRotate(Vec, Rads)
		local vec = Vec.Unit
		--x2 = cos β x1 − sin β y1
		--y2 = sin β x1 + cos β y1
		local sin = math.sin(Rads)
		local cos = math.cos(Rads)
		local x = (cos * vec.x) - (sin * vec.y)
		local y = (sin * vec.x) + (cos * vec.y)

		return Vector2.new(x, y).Unit * Vec.Magnitude
	end
end
local bColor = {}
do -- color functions
	function bColor:Mult(col, mult)
		return Color3.new(col.R * mult, col.G * mult, col.B * mult)
	end
	function bColor:Add(col, num)
		return Color3.new(col.R + num, col.G + num, col.B + num)
	end
end
local function string_cut(s1, num)
	return num == 0 and s1 or string.sub(s1, 1, num)
end

local textBoxLetters = {
	"A",
	"B",
	"C",
	"D",
	"E",
	"F",
	"G",
	"H",
	"I",
	"J",
	"K",
	"L",
	"M",
	"N",
	"O",
	"P",
	"Q",
	"R",
	"S",
	"T",
	"U",
	"V",
	"W",
	"X",
	"Y",
	"Z",
}

local keyNames = {
	One = "1",
	Two = "2",
	Three = "3",
	Four = "4",
	Five = "5",
	Six = "6",
	Seven = "7",
	Eight = "8",
	Nine = "9",
	Zero = "0",
	LeftBracket = "[",
	RightBracket = "]",
	Semicolon = ";",
	BackSlash = "\\",
	Slash = "/",
	Minus = "-",
	Equals = "=",
	Return = "Enter",
	Backquote = "`",
	CapsLock = "Caps",
	LeftShift = "LShift",
	RightShift = "RShift",
	LeftControl = "LCtrl",
	RightControl = "RCtrl",
	LeftAlt = "LAlt",
	RightAlt = "RAlt",
	Backspace = "Back",
	Plus = "+",
	Multiply = "x",
	PageUp = "PgUp",
	PageDown = "PgDown",
	Delete = "Del",
	Insert = "Ins",
	NumLock = "NumL",
	Comma = ",",
	Period = ".",
}
local colemak = {
	E = "F",
	R = "P",
	T = "G",
	Y = "J",
	U = "L",
	I = "U",
	O = "Y",
	P = ";",
	S = "R",
	D = "S",
	F = "T",
	G = "D",
	J = "N",
	K = "E",
	L = "I",
	[";"] = "O",
	N = "K",
}

local keymodifiernames = {
	["`"] = "~",
	["1"] = "!",
	["2"] = "@",
	["3"] = "#",
	["4"] = "$",
	["5"] = "%",
	["6"] = "^",
	["7"] = "&",
	["8"] = "*",
	["9"] = "(",
	["0"] = ")",
	["-"] = "_",
	["="] = "+",
	["["] = "{",
	["]"] = "}",
	["\\"] = "|",
	[";"] = ":",
	["'"] = '"',
	[","] = "<",
	["."] = ".",
	["/"] = "?",
}

local function KeyEnumToName(key) -- did this all in a function cuz why not
	if key == nil then
		return "None"
	end
	local _key = tostring(key) .. "."
	local _key = _key:gsub("%.", ",")
	local keyname = nil
	local looptime = 0
	for w in _key:gmatch("(.-),") do
		looptime = looptime + 1
		if looptime == 3 then
			keyname = w
		end
	end
	if string.match(keyname, "Keypad") then
		keyname = string.gsub(keyname, "Keypad", "")
	end

	if keyname == "Unknown" or key.Value == 27 then
		return "None"
	end

	if keyNames[keyname] then
		keyname = keyNames[keyname]
	end
	if Nate then
		return colemak[keyname] or keyname
	else
		return keyname
	end
end

local invalidfilekeys = {
	["\\"] = true,
	["/"] = true,
	[":"] = true,
	["*"] = true,
	["?"] = true,
	['"'] = true,
	["<"] = true,
	[">"] = true,
	["|"] = true,
}

local function KeyModifierToName(key, filename)
	if keymodifiernames[key] ~= nil then
		if filename then
			if invalidfilekeys[keymodifiernames[key]] then
				return ""
			else
				return keymodifiernames[key]
			end
		else
			return keymodifiernames[key]
		end
	else
		return ""
	end
end

local allrender = {}

local RGB = Color3.fromRGB
local Draw = {}

do
	function Draw:UnRender()
		for k, v in pairs(allrender) do
			for k1, v1 in pairs(v) do
				--warn(k1, v1)
				-- ANCHOR WHAT THE FUCK IS GOING ON WITH THIS WHY IS THIS ERRORING BECAUSE OF NUMBER
				if v1 and type(v1) ~= "number" and v1.__OBJECT_EXISTS then
					v1:Remove()
				else
					--rconsolewarn(tostring(k),tostring(v),tostring(k1),tostring(v1)) -- idfk why but this shit doesn't print anything out. might as well have it commented out though -nata april 1 21
				end
			end
		end
	end

	function Draw:OutlinedRect(visible, pos_x, pos_y, width, height, clr, tablename)
		local temptable = Drawing.new("Square")
		temptable.Visible = visible
		temptable.Position = Vector2.new(pos_x, pos_y)
		temptable.Size = Vector2.new(width, height)
		temptable.Color = RGB(clr[1], clr[2], clr[3])
		temptable.Filled = false
		temptable.Thickness = 0
		temptable.Transparency = clr[4] / 255
		table.insert(tablename, temptable)
		if not table.find(allrender, tablename) then
			table.insert(allrender, tablename)
		end
	end

	function Draw:FilledRect(visible, pos_x, pos_y, width, height, clr, tablename)
		local temptable = Drawing.new("Square")
		temptable.Visible = visible
		temptable.Position = Vector2.new(pos_x, pos_y)
		temptable.Size = Vector2.new(width, height)
		temptable.Color = RGB(clr[1], clr[2], clr[3])
		temptable.Filled = true
		temptable.Thickness = 0
		temptable.Transparency = clr[4] / 255
		table.insert(tablename, temptable)
		if not table.find(allrender, tablename) then
			table.insert(allrender, tablename)
		end
	end

	function Draw:Line(visible, thickness, start_x, start_y, end_x, end_y, clr, tablename)
		temptable = Drawing.new("Line")
		temptable.Visible = visible
		temptable.Thickness = thickness
		temptable.From = Vector2.new(start_x, start_y)
		temptable.To = Vector2.new(end_x, end_y)
		temptable.Color = RGB(clr[1], clr[2], clr[3])
		temptable.Transparency = clr[4] / 255
		table.insert(tablename, temptable)
		if not table.find(allrender, tablename) then
			table.insert(allrender, tablename)
		end
	end

	function Draw:Image(visible, imagedata, pos_x, pos_y, width, height, transparency, tablename)
		local temptable = Drawing.new("Image")
		temptable.Visible = visible
		temptable.Position = Vector2.new(pos_x, pos_y)
		temptable.Size = Vector2.new(width, height)
		temptable.Transparency = transparency
		temptable.Data = imagedata or placeholderImage
		table.insert(tablename, temptable)
		if not table.find(allrender, tablename) then
			table.insert(allrender, tablename)
		end
	end

	function Draw:Text(text, font, visible, pos_x, pos_y, size, centered, clr, tablename)
		local temptable = Drawing.new("Text")
		temptable.Text = text
		temptable.Visible = visible
		temptable.Position = Vector2.new(pos_x, pos_y)
		temptable.Size = size
		temptable.Center = centered
		temptable.Color = RGB(clr[1], clr[2], clr[3])
		temptable.Transparency = clr[4] / 255
		temptable.Outline = false
		temptable.Font = font
		table.insert(tablename, temptable)
		if not table.find(allrender, tablename) then
			table.insert(allrender, tablename)
		end
	end

	function Draw:OutlinedText(text, font, visible, pos_x, pos_y, size, centered, clr, clr2, tablename)
		local temptable = Drawing.new("Text")
		temptable.Text = text
		temptable.Visible = visible
		temptable.Position = Vector2.new(pos_x, pos_y)
		temptable.Size = size
		temptable.Center = centered
		temptable.Color = RGB(clr[1], clr[2], clr[3])
		temptable.Transparency = clr[4] / 255
		temptable.Outline = true
		temptable.OutlineColor = RGB(clr2[1], clr2[2], clr2[3])
		temptable.Font = font
		if not table.find(allrender, tablename) then
			table.insert(allrender, tablename)
		end
		if tablename then
			table.insert(tablename, temptable)
		end
		return temptable
	end

	function Draw:Triangle(visible, filled, pa, pb, pc, clr, tablename)
		clr = clr or { 255, 255, 255, 1 }
		local temptable = Drawing.new("Triangle")
		temptable.Visible = visible
		temptable.Transparency = clr[4] or 1
		temptable.Color = RGB(clr[1], clr[2], clr[3])
		temptable.Thickness = 4.1
		if pa and pb and pc then
			temptable.PointA = Vector2.new(pa[1], pa[2])
			temptable.PointB = Vector2.new(pb[1], pb[2])
			temptable.PointC = Vector2.new(pc[1], pc[2])
		end
		temptable.Filled = filled
		table.insert(tablename, temptable)
		if tablename and not table.find(allrender, tablename) then
			table.insert(allrender, tablename)
		end
	end

	function Draw:Circle(visible, pos_x, pos_y, size, thickness, sides, clr, tablename)
		local temptable = Drawing.new("Circle")
		temptable.Position = Vector2.new(pos_x, pos_y)
		temptable.Visible = visible
		temptable.Radius = size
		temptable.Thickness = thickness
		temptable.NumSides = sides
		temptable.Transparency = clr[4]
		temptable.Filled = false
		temptable.Color = RGB(clr[1], clr[2], clr[3])
		table.insert(tablename, temptable)
		if not table.find(allrender, tablename) then
			table.insert(allrender, tablename)
		end
	end

	function Draw:FilledCircle(visible, pos_x, pos_y, size, thickness, sides, clr, tablename)
		local temptable = Drawing.new("Circle")
		temptable.Position = Vector2.new(pos_x, pos_y)
		temptable.Visible = visible
		temptable.Radius = size
		temptable.Thickness = thickness
		temptable.NumSides = sides
		temptable.Transparency = clr[4]
		temptable.Filled = true
		temptable.Color = RGB(clr[1], clr[2], clr[3])
		table.insert(tablename, temptable)
		if not table.find(allrender, tablename) then
			table.insert(allrender, tablename)
		end
	end

	--ANCHOR MENU ELEMENTS

	function Draw:MenuOutlinedRect(visible, pos_x, pos_y, width, height, clr, tablename)
		Draw:OutlinedRect(visible, pos_x + menu.x, pos_y + menu.y, width, height, clr, tablename)
		table.insert(menu.postable, { tablename[#tablename], pos_x, pos_y })

		if menu.log_multi ~= nil then
			table.insert(menu.mgrouptabz[menu.log_multi[1]][menu.log_multi[2]], tablename[#tablename])
		end
	end

	function Draw:MenuFilledRect(visible, pos_x, pos_y, width, height, clr, tablename)
		Draw:FilledRect(visible, pos_x + menu.x, pos_y + menu.y, width, height, clr, tablename)
		table.insert(menu.postable, { tablename[#tablename], pos_x, pos_y })

		if menu.log_multi ~= nil then
			table.insert(menu.mgrouptabz[menu.log_multi[1]][menu.log_multi[2]], tablename[#tablename])
		end
	end

	function Draw:MenuImage(visible, imagedata, pos_x, pos_y, width, height, transparency, tablename)
		Draw:Image(visible, imagedata, pos_x + menu.x, pos_y + menu.y, width, height, transparency, tablename)
		table.insert(menu.postable, { tablename[#tablename], pos_x, pos_y })

		if menu.log_multi ~= nil then
			table.insert(menu.mgrouptabz[menu.log_multi[1]][menu.log_multi[2]], tablename[#tablename])
		end
	end

	function Draw:MenuBigText(text, visible, centered, pos_x, pos_y, tablename)
		local text = Draw:OutlinedText(
			text,
			2,
			visible,
			pos_x + menu.x,
			pos_y + menu.y,
			13,
			centered,
			{ 255, 255, 255, 255 },
			{ 0, 0, 0 },
			tablename
		)
		table.insert(menu.postable, { tablename[#tablename], pos_x, pos_y })

		if menu.log_multi ~= nil then
			table.insert(menu.mgrouptabz[menu.log_multi[1]][menu.log_multi[2]], tablename[#tablename])
		end

		return text
	end

	function Draw:CoolBox(name, x, y, width, height, tab)
		Draw:MenuOutlinedRect(true, x, y, width, height, { 0, 0, 0, 255 }, tab)
		Draw:MenuOutlinedRect(true, x + 1, y + 1, width - 2, height - 2, { 20, 20, 20, 255 }, tab)
		Draw:MenuOutlinedRect(true, x + 2, y + 2, width - 3, 1, { 127, 72, 163, 255 }, tab)
		table.insert(menu.clrs.norm, tab[#tab])
		Draw:MenuOutlinedRect(true, x + 2, y + 3, width - 3, 1, { 87, 32, 123, 255 }, tab)
		table.insert(menu.clrs.dark, tab[#tab])
		Draw:MenuOutlinedRect(true, x + 2, y + 4, width - 3, 1, { 20, 20, 20, 255 }, tab)

		for i = 0, 7 do
			Draw:MenuFilledRect(true, x + 2, y + 5 + (i * 2), width - 4, 2, { 45, 45, 45, 255 }, tab)
			tab[#tab].Color = ColorRange(
				i,
				{ [1] = { start = 0, color = RGB(45, 45, 45) }, [2] = { start = 7, color = RGB(35, 35, 35) } }
			)
		end

		Draw:MenuBigText(name, true, false, x + 6, y + 5, tab)
	end

	function Draw:CoolMultiBox(names, x, y, width, height, tab)
		Draw:MenuOutlinedRect(true, x, y, width, height, { 0, 0, 0, 255 }, tab)
		Draw:MenuOutlinedRect(true, x + 1, y + 1, width - 2, height - 2, { 20, 20, 20, 255 }, tab)
		Draw:MenuOutlinedRect(true, x + 2, y + 2, width - 3, 1, { 127, 72, 163, 255 }, tab)
		table.insert(menu.clrs.norm, tab[#tab])
		Draw:MenuOutlinedRect(true, x + 2, y + 3, width - 3, 1, { 87, 32, 123, 255 }, tab)
		table.insert(menu.clrs.dark, tab[#tab])
		Draw:MenuOutlinedRect(true, x + 2, y + 4, width - 3, 1, { 20, 20, 20, 255 }, tab)

		--{35, 35, 35, 255}

		Draw:MenuFilledRect(true, x + 2, y + 5, width - 4, 18, { 30, 30, 30, 255 }, tab)
		Draw:MenuFilledRect(true, x + 2, y + 21, width - 4, 2, { 20, 20, 20, 255 }, tab)

		local selected = {}
		for i = 0, 8 do
			Draw:MenuFilledRect(true, x + 2, y + 5 + (i * 2), width - 159, 2, { 45, 45, 45, 255 }, tab)
			tab[#tab].Color = ColorRange(
				i,
				{ [1] = { start = 0, color = RGB(50, 50, 50) }, [2] = { start = 8, color = RGB(35, 35, 35) } }
			)
			table.insert(selected, { postable = #menu.postable, drawn = tab[#tab] })
		end

		local length = 2
		local selected_pos = {}
		local click_pos = {}
		local nametext = {}
		for i, v in ipairs(names) do
			Draw:MenuBigText(v, true, false, x + 4 + length, y + 5, tab)
			if i == 1 then
				tab[#tab].Color = RGB(255, 255, 255)
			else
				tab[#tab].Color = RGB(170, 170, 170)
			end
			table.insert(nametext, tab[#tab])

			Draw:MenuFilledRect(true, x + length + tab[#tab].TextBounds.X + 8, y + 5, 2, 16, { 20, 20, 20, 255 }, tab)
			table.insert(selected_pos, { pos = x + length, length = tab[#tab - 1].TextBounds.X + 8 })
			table.insert(click_pos, {
				x = x + length,
				y = y + 5,
				width = tab[#tab - 1].TextBounds.X + 8,
				height = 18,
				name = v,
				num = i,
			})
			length += tab[#tab - 1].TextBounds.X + 10
		end

		local settab = 1
		for k, v in pairs(selected) do
			menu.postable[v.postable][2] = selected_pos[settab].pos
			v.drawn.Size = Vector2.new(selected_pos[settab].length, 2)
		end

		return { bar = selected, barpos = selected_pos, click_pos = click_pos, nametext = nametext }

		--Draw:MenuBigText(str, true, false, x + 6, y + 5, tab)
	end

	function Draw:Toggle(name, value, unsafe, x, y, tab)
		Draw:MenuOutlinedRect(true, x, y, 12, 12, { 30, 30, 30, 255 }, tab)
		Draw:MenuOutlinedRect(true, x + 1, y + 1, 10, 10, { 0, 0, 0, 255 }, tab)

		local temptable = {}
		for i = 0, 3 do
			Draw:MenuFilledRect(true, x + 2, y + 2 + (i * 2), 8, 2, { 0, 0, 0, 255 }, tab)
			table.insert(temptable, tab[#tab])
			if value then
				tab[#tab].Color = ColorRange(i, {
					[1] = { start = 0, color = RGB(menu.mc[1], menu.mc[2], menu.mc[3]) },
					[2] = { start = 3, color = RGB(menu.mc[1] - 40, menu.mc[2] - 40, menu.mc[3] - 40) },
				})
			else
				tab[#tab].Color = ColorRange(i, {
					[1] = { start = 0, color = RGB(50, 50, 50) },
					[2] = { start = 3, color = RGB(30, 30, 30) },
				})
			end
		end

		Draw:MenuBigText(name, true, false, x + 16, y - 1, tab)
		if unsafe == true then
			tab[#tab].Color = RGB(90, 90, 90)
		end
		table.insert(temptable, tab[#tab])
		return temptable
	end

	function Draw:Keybind(key, x, y, tab)
		local temptable = {}
		Draw:MenuFilledRect(true, x, y, 44, 16, { 25, 25, 25, 255 }, tab)
		Draw:MenuBigText(KeyEnumToName(key), true, true, x + 22, y + 1, tab)
		table.insert(temptable, tab[#tab])
		Draw:MenuOutlinedRect(true, x, y, 44, 16, { 30, 30, 30, 255 }, tab)
		table.insert(temptable, tab[#tab])
		Draw:MenuOutlinedRect(true, x + 1, y + 1, 42, 14, { 0, 0, 0, 255 }, tab)

		return temptable
	end

	function Draw:ColorPicker(color, x, y, tab)
		local temptable = {}

		Draw:MenuOutlinedRect(true, x, y, 28, 14, { 30, 30, 30, 255 }, tab)
		Draw:MenuOutlinedRect(true, x + 1, y + 1, 26, 12, { 0, 0, 0, 255 }, tab)

		Draw:MenuFilledRect(true, x + 2, y + 2, 24, 10, { color[1], color[2], color[3], 255 }, tab)
		table.insert(temptable, tab[#tab])
		Draw:MenuOutlinedRect(true, x + 2, y + 2, 24, 10, { color[1] - 40, color[2] - 40, color[3] - 40, 255 }, tab)
		table.insert(temptable, tab[#tab])
		Draw:MenuOutlinedRect(true, x + 3, y + 3, 22, 8, { color[1] - 40, color[2] - 40, color[3] - 40, 255 }, tab)
		table.insert(temptable, tab[#tab])

		return temptable
	end

	function Draw:Slider(name, stradd, value, minvalue, maxvalue, customvals, rounded, x, y, length, tab)
		Draw:MenuBigText(name, true, false, x, y - 3, tab)

		for i = 0, 3 do
			Draw:MenuFilledRect(true, x + 2, y + 14 + (i * 2), length - 4, 2, { 0, 0, 0, 255 }, tab)
			tab[#tab].Color = ColorRange(
				i,
				{ [1] = { start = 0, color = RGB(50, 50, 50) }, [2] = { start = 3, color = RGB(30, 30, 30) } }
			)
		end

		local temptable = {}
		for i = 0, 3 do
			Draw:MenuFilledRect(
				true,
				x + 2,
				y + 14 + (i * 2),
				(length - 4) * ((value - minvalue) / (maxvalue - minvalue)),
				2,
				{ 0, 0, 0, 255 },
				tab
			)
			table.insert(temptable, tab[#tab])
			tab[#tab].Color = ColorRange(i, {
				[1] = { start = 0, color = RGB(menu.mc[1], menu.mc[2], menu.mc[3]) },
				[2] = { start = 3, color = RGB(menu.mc[1] - 40, menu.mc[2] - 40, menu.mc[3] - 40) },
			})
		end
		Draw:MenuOutlinedRect(true, x, y + 12, length, 12, { 30, 30, 30, 255 }, tab)
		Draw:MenuOutlinedRect(true, x + 1, y + 13, length - 2, 10, { 0, 0, 0, 255 }, tab)

		local textstr = ""

		if stradd == nil then
			stradd = ""
		end

		local decplaces = rounded and string.rep("0", math.log(1 / rounded) / math.log(10)) or 1
		if rounded and value == math.floor(value * decplaces) then
			textstr = tostring(value) .. "." .. decplaces .. stradd
		else
			textstr = tostring(value) .. stradd
		end

		Draw:MenuBigText(customvals[value] or textstr, true, true, x + (length * 0.5), y + 11, tab)
		table.insert(temptable, tab[#tab])
		table.insert(temptable, stradd)
		return temptable
	end

	function Draw:Dropbox(name, value, values, x, y, length, tab)
		local temptable = {}
		Draw:MenuBigText(name, true, false, x, y - 3, tab)

		for i = 0, 7 do
			Draw:MenuFilledRect(true, x + 2, y + 14 + (i * 2), length - 4, 2, { 0, 0, 0, 255 }, tab)
			tab[#tab].Color = ColorRange(
				i,
				{ [1] = { start = 0, color = RGB(50, 50, 50) }, [2] = { start = 7, color = RGB(35, 35, 35) } }
			)
		end

		Draw:MenuOutlinedRect(true, x, y + 12, length, 22, { 30, 30, 30, 255 }, tab)
		Draw:MenuOutlinedRect(true, x + 1, y + 13, length - 2, 20, { 0, 0, 0, 255 }, tab)

		Draw:MenuBigText(tostring(values[value]), true, false, x + 6, y + 16, tab)
		table.insert(temptable, tab[#tab])

		Draw:MenuBigText("-", true, false, x - 17 + length, y + 16, tab)
		table.insert(temptable, tab[#tab])

		return temptable
	end

	function Draw:Combobox(name, values, x, y, length, tab)
		local temptable = {}
		Draw:MenuBigText(name, true, false, x, y - 3, tab)

		for i = 0, 7 do
			Draw:MenuFilledRect(true, x + 2, y + 14 + (i * 2), length - 4, 2, { 0, 0, 0, 255 }, tab)
			tab[#tab].Color = ColorRange(
				i,
				{ [1] = { start = 0, color = RGB(50, 50, 50) }, [2] = { start = 7, color = RGB(35, 35, 35) } }
			)
		end

		Draw:MenuOutlinedRect(true, x, y + 12, length, 22, { 30, 30, 30, 255 }, tab)
		Draw:MenuOutlinedRect(true, x + 1, y + 13, length - 2, 20, { 0, 0, 0, 255 }, tab)
		local textthing = ""
		for k, v in pairs(values) do
			if v[2] then
				if textthing == "" then
					textthing = v[1]
				else
					textthing ..= ", " .. v[1]
				end
			end
		end
		if string.len(textthing) > 25 then
			textthing = string_cut(textthing, 25)
		end
		textthing = textthing ~= "" and textthing or "None"
		Draw:MenuBigText(textthing, true, false, x + 6, y + 16, tab)
		table.insert(temptable, tab[#tab])

		Draw:MenuBigText("...", true, false, x - 27 + length, y + 16, tab)
		table.insert(temptable, tab[#tab])

		return temptable
	end

	function Draw:Button(name, x, y, length, tab)
		local temptable = {}

		for i = 0, 8 do
			Draw:MenuFilledRect(true, x + 2, y + 2 + (i * 2), length - 4, 2, { 0, 0, 0, 255 }, tab)
			tab[#tab].Color = ColorRange(
				i,
				{ [1] = { start = 0, color = RGB(50, 50, 50) }, [2] = { start = 8, color = RGB(35, 35, 35) } }
			)
			table.insert(temptable, tab[#tab])
		end

		Draw:MenuOutlinedRect(true, x, y, length, 22, { 30, 30, 30, 255 }, tab)
		Draw:MenuOutlinedRect(true, x + 1, y + 1, length - 2, 20, { 0, 0, 0, 255 }, tab)
		temptable.text = Draw:MenuBigText(name, true, true, x + math.floor(length * 0.5), y + 4, tab)

		return temptable
	end

	function Draw:List(name, x, y, length, maxamount, columns, tab)
		local temptable = { uparrow = {}, downarrow = {}, liststuff = { rows = {}, words = {} } }

		for i, v in ipairs(name) do
			Draw:MenuBigText(
				v,
				true,
				false,
				(math.floor(length / columns) * i) - math.floor(length / columns) + 30,
				y - 3,
				tab
			)
		end

		Draw:MenuOutlinedRect(true, x, y + 12, length, 22 * maxamount + 4, { 30, 30, 30, 255 }, tab)
		Draw:MenuOutlinedRect(true, x + 1, y + 13, length - 2, 22 * maxamount + 2, { 0, 0, 0, 255 }, tab)

		Draw:MenuFilledRect(true, x + length - 7, y + 16, 1, 1, { menu.mc[1], menu.mc[2], menu.mc[3], 255 }, tab)
		table.insert(temptable.uparrow, tab[#tab])
		table.insert(menu.clrs.norm, tab[#tab])
		Draw:MenuFilledRect(true, x + length - 8, y + 17, 3, 1, { menu.mc[1], menu.mc[2], menu.mc[3], 255 }, tab)
		table.insert(temptable.uparrow, tab[#tab])
		table.insert(menu.clrs.norm, tab[#tab])
		Draw:MenuFilledRect(true, x + length - 9, y + 18, 5, 1, { menu.mc[1], menu.mc[2], menu.mc[3], 255 }, tab)
		table.insert(temptable.uparrow, tab[#tab])
		table.insert(menu.clrs.norm, tab[#tab])

		Draw:MenuFilledRect(
			true,
			x + length - 7,
			y + 16 + (22 * maxamount + 4) - 9,
			1,
			1,
			{ menu.mc[1], menu.mc[2], menu.mc[3], 255 },
			tab
		)
		table.insert(temptable.downarrow, tab[#tab])
		table.insert(menu.clrs.norm, tab[#tab])
		Draw:MenuFilledRect(
			true,
			x + length - 8,
			y + 16 + (22 * maxamount + 4) - 10,
			3,
			1,
			{ menu.mc[1], menu.mc[2], menu.mc[3], 255 },
			tab
		)
		table.insert(temptable.downarrow, tab[#tab])
		table.insert(menu.clrs.norm, tab[#tab])
		Draw:MenuFilledRect(
			true,
			x + length - 9,
			y + 16 + (22 * maxamount + 4) - 11,
			5,
			1,
			{ menu.mc[1], menu.mc[2], menu.mc[3], 255 },
			tab
		)
		table.insert(temptable.downarrow, tab[#tab])
		table.insert(menu.clrs.norm, tab[#tab])

		for i = 1, maxamount do
			temptable.liststuff.rows[i] = {}
			if i ~= maxamount then
				Draw:MenuOutlinedRect(true, x + 4, (y + 13) + (22 * i), length - 8, 2, { 20, 20, 20, 255 }, tab)
				table.insert(temptable.liststuff.rows[i], tab[#tab])
			end

			if columns ~= nil then
				for i1 = 1, columns - 1 do
					Draw:MenuOutlinedRect(
						true,
						x + math.floor(length / columns) * i1,
						(y + 13) + (22 * i) - 18,
						2,
						16,
						{ 20, 20, 20, 255 },
						tab
					)
					table.insert(temptable.liststuff.rows[i], tab[#tab])
				end
			end

			temptable.liststuff.words[i] = {}
			if columns ~= nil then
				for i1 = 1, columns do
					Draw:MenuBigText(
						"",
						true,
						false,
						(x + math.floor(length / columns) * i1) - math.floor(length / columns) + 5,
						(y + 13) + (22 * i) - 16,
						tab
					)
					table.insert(temptable.liststuff.words[i], tab[#tab])
				end
			else
				Draw:MenuBigText("", true, false, x + 5, (y + 13) + (22 * i) - 16, tab)
				table.insert(temptable.liststuff.words[i], tab[#tab])
			end
		end

		return temptable
	end

	function Draw:ImageWithText(size, image, text, x, y, tab)
		local temptable = {}
		Draw:MenuOutlinedRect(true, x, y, size + 4, size + 4, { 30, 30, 30, 255 }, tab)
		Draw:MenuOutlinedRect(true, x + 1, y + 1, size + 2, size + 2, { 0, 0, 0, 255 }, tab)
		Draw:MenuFilledRect(true, x + 2, y + 2, size, size, { 40, 40, 40, 255 }, tab)

		Draw:MenuBigText(text, true, false, x + size + 8, y, tab)
		table.insert(temptable, tab[#tab])

		Draw:MenuImage(true, BBOT_IMAGES[5], x + 2, y + 2, size, size, 1, tab)
		table.insert(temptable, tab[#tab])

		return temptable
	end

	function Draw:TextBox(name, text, x, y, length, tab)
		for i = 0, 8 do
			Draw:MenuFilledRect(true, x + 2, y + 2 + (i * 2), length - 4, 2, { 0, 0, 0, 255 }, tab)
			tab[#tab].Color = ColorRange(
				i,
				{ [1] = { start = 0, color = RGB(50, 50, 50) }, [2] = { start = 8, color = RGB(35, 35, 35) } }
			)
		end

		Draw:MenuOutlinedRect(true, x, y, length, 22, { 30, 30, 30, 255 }, tab)
		Draw:MenuOutlinedRect(true, x + 1, y + 1, length - 2, 20, { 0, 0, 0, 255 }, tab)
		Draw:MenuBigText(text, true, false, x + 6, y + 4, tab)

		return tab[#tab]
	end
end

-- finish

local loadingthing = Draw:OutlinedText(
	"Loading...",
	2,
	true,
	math.floor(SCREEN_SIZE.x / 16),
	math.floor(SCREEN_SIZE.y / 16),
	13,
	true,
	{ 255, 50, 200, 255 },
	{ 0, 0, 0 }
)

function menu.Initialize(menutable)
	local bbmenu = {} -- this one is for the rendering n shi
	do
		Draw:MenuOutlinedRect(true, 0, 0, menu.w, menu.h, { 0, 0, 0, 255 }, bbmenu) -- first gradent or whatever
		Draw:MenuOutlinedRect(true, 1, 1, menu.w - 2, menu.h - 2, { 20, 20, 20, 255 }, bbmenu)
		Draw:MenuOutlinedRect(true, 2, 2, menu.w - 3, 1, { 127, 72, 163, 255 }, bbmenu)
		table.insert(menu.clrs.norm, bbmenu[#bbmenu])
		Draw:MenuOutlinedRect(true, 2, 3, menu.w - 3, 1, { 87, 32, 123, 255 }, bbmenu)
		table.insert(menu.clrs.dark, bbmenu[#bbmenu])
		Draw:MenuOutlinedRect(true, 2, 4, menu.w - 3, 1, { 20, 20, 20, 255 }, bbmenu)

		for i = 0, 19 do
			Draw:MenuFilledRect(true, 2, 5 + i, menu.w - 4, 1, { 20, 20, 20, 255 }, bbmenu)
			bbmenu[6 + i].Color = ColorRange(
				i,
				{ [1] = { start = 0, color = RGB(50, 50, 50) }, [2] = { start = 20, color = RGB(35, 35, 35) } }
			)
		end
		Draw:MenuFilledRect(true, 2, 25, menu.w - 4, menu.h - 27, { 35, 35, 35, 255 }, bbmenu)

		Draw:MenuBigText(MenuName or "Bitch Bot", true, false, 6, 6, bbmenu)

		Draw:MenuOutlinedRect(true, 8, 22, menu.w - 16, menu.h - 30, { 0, 0, 0, 255 }, bbmenu) -- all this shit does the 2nd gradent
		Draw:MenuOutlinedRect(true, 9, 23, menu.w - 18, menu.h - 32, { 20, 20, 20, 255 }, bbmenu)
		Draw:MenuOutlinedRect(true, 10, 24, menu.w - 19, 1, { 127, 72, 163, 255 }, bbmenu)
		table.insert(menu.clrs.norm, bbmenu[#bbmenu])
		Draw:MenuOutlinedRect(true, 10, 25, menu.w - 19, 1, { 87, 32, 123, 255 }, bbmenu)
		table.insert(menu.clrs.dark, bbmenu[#bbmenu])
		Draw:MenuOutlinedRect(true, 10, 26, menu.w - 19, 1, { 20, 20, 20, 255 }, bbmenu)

		for i = 0, 14 do
			Draw:MenuFilledRect(true, 10, 27 + (i * 2), menu.w - 20, 2, { 45, 45, 45, 255 }, bbmenu)
			bbmenu[#bbmenu].Color = ColorRange(
				i,
				{ [1] = { start = 0, color = RGB(50, 50, 50) }, [2] = { start = 15, color = RGB(35, 35, 35) } }
			)
		end
		Draw:MenuFilledRect(true, 10, 57, menu.w - 20, menu.h - 67, { 35, 35, 35, 255 }, bbmenu)
	end
	-- ok now the cool part :D
	--ANCHOR menu stuffz

	local tabz = {}
	for i = 1, #menutable do
		tabz[i] = {}
	end

	local tabs = {} -- i like tabby catz 🐱🐱🐱

	menu.multigroups = {}

	for k, v in pairs(menutable) do
		Draw:MenuFilledRect(
			true,
			10 + ((k - 1) * ((menu.w - 20) / #menutable)),
			27,
			((menu.w - 20) / #menutable),
			32,
			{ 30, 30, 30, 255 },
			bbmenu
		)
		Draw:MenuOutlinedRect(
			true,
			10 + ((k - 1) * ((menu.w - 20) / #menutable)),
			27,
			((menu.w - 20) / #menutable),
			32,
			{ 20, 20, 20, 255 },
			bbmenu
		)
		Draw:MenuBigText(
			v.name,
			true,
			true,
			math.floor(10 + ((k - 1) * ((menu.w - 20) / #menutable)) + (((menu.w - 20) / #menutable) * 0.5)),
			35,
			bbmenu
		)
		table.insert(tabs, { bbmenu[#bbmenu - 2], bbmenu[#bbmenu - 1], bbmenu[#bbmenu] })
		table.insert(menu.tabnames, v.name)

		menu.options[v.name] = {}
		menu.multigroups[v.name] = {}
		menu.mgrouptabz[v.name] = {}

		local y_offies = { left = 66, right = 66 }
		if v.content ~= nil then
			for k1, v1 in pairs(v.content) do
				if v1.autopos ~= nil then
					v1.width = menu.columns.width
					if v1.autopos == "left" then
						v1.x = menu.columns.left
						v1.y = y_offies.left
					elseif v1.autopos == "right" then
						v1.x = menu.columns.right
						v1.y = y_offies.right
					end
				end

				local groups = {}

				if type(v1.name) == "table" then
					groups = v1.name
				else
					table.insert(groups, v1.name)
				end

				local y_pos = 24

				for g_ind, g_name in ipairs(groups) do
					menu.options[v.name][g_name] = {}
					if type(v1.name) == "table" then
						menu.mgrouptabz[v.name][g_name] = {}
						menu.log_multi = { v.name, g_name }
					end

					local content = nil
					if type(v1.name) == "table" then
						y_pos = 28
						content = v1[g_ind].content
					else
						y_pos = 24
						content = v1.content
					end

					if content ~= nil then
						for k2, v2 in pairs(content) do
							if v2.type == "toggle" then
								menu.options[v.name][g_name][v2.name] = {}
								local unsafe = false
								if v2.unsafe then
									unsafe = true
								end
								menu.options[v.name][g_name][v2.name][4] = Draw:Toggle(v2.name, v2.value, unsafe, v1.x + 8, v1.y + y_pos, tabz[k])
								menu.options[v.name][g_name][v2.name][1] = v2.value
								menu.options[v.name][g_name][v2.name][7] = v2.value
								menu.options[v.name][g_name][v2.name][2] = v2.type
								menu.options[v.name][g_name][v2.name][3] = { v1.x + 7, v1.y + y_pos - 1 }
								menu.options[v.name][g_name][v2.name][6] = unsafe
								menu.options[v.name][g_name][v2.name].tooltip = v2.tooltip or nil
								if v2.extra ~= nil then
									if v2.extra.type == "keybind" then
										menu.options[v.name][g_name][v2.name][5] = {}
										menu.options[v.name][g_name][v2.name][5][4] = Draw:Keybind(
											v2.extra.key,
											v1.x + v1.width - 52,
											y_pos + v1.y - 2,
											tabz[k]
										)
										menu.options[v.name][g_name][v2.name][5][1] = v2.extra.key
										menu.options[v.name][g_name][v2.name][5][2] = v2.extra.type
										menu.options[v.name][g_name][v2.name][5][3] = { v1.x + v1.width - 52, y_pos + v1.y - 2 }
										menu.options[v.name][g_name][v2.name][5][5] = false
										menu.options[v.name][g_name][v2.name][5].toggletype = v2.extra.toggletype == nil and 1 or v2.extra.toggletype
										menu.options[v.name][g_name][v2.name][5].relvalue = false
										local event = event.new(("%s %s %s"):format(v.name, g_name, v2.name))
										event:connect(function(newval) 
											if menu:GetVal("Visuals", "Keybinds" ,"Log Keybinds") then 
												CreateNotification(("%s %s %s has been set to %s"):format(v.name, g_name, v2.name, newval and "true" or "false")) 
											end 
										end)
										menu.options[v.name][g_name][v2.name][5].event = event
										menu.options[v.name][g_name][v2.name][5].bind = table.insert(menu.keybinds, {
												menu.options[v.name][g_name][v2.name],
												tostring(v2.name),
												tostring(g_name),
												tostring(v.name),
											})
									elseif v2.extra.type == "single colorpicker" then
										menu.options[v.name][g_name][v2.name][5] = {}
										menu.options[v.name][g_name][v2.name][5][4] = Draw:ColorPicker(
											v2.extra.color,
											v1.x + v1.width - 38,
											y_pos + v1.y - 1,
											tabz[k]
										)
										menu.options[v.name][g_name][v2.name][5][1] = v2.extra.color
										menu.options[v.name][g_name][v2.name][5][2] = v2.extra.type
										menu.options[v.name][g_name][v2.name][5][3] = { v1.x + v1.width - 38, y_pos + v1.y - 1 }
										menu.options[v.name][g_name][v2.name][5][5] = false
										menu.options[v.name][g_name][v2.name][5][6] = v2.extra.name
									elseif v2.extra.type == "double colorpicker" then
										menu.options[v.name][g_name][v2.name][5] = {}
										menu.options[v.name][g_name][v2.name][5][1] = {}
										menu.options[v.name][g_name][v2.name][5][1][1] = {}
										menu.options[v.name][g_name][v2.name][5][1][2] = {}
										menu.options[v.name][g_name][v2.name][5][2] = v2.extra.type
										for i = 1, 2 do
											menu.options[v.name][g_name][v2.name][5][1][i][4] = Draw:ColorPicker(
												v2.extra.color[i],
												v1.x + v1.width - 38 - ((i - 1) * 34),
												y_pos + v1.y - 1,
												tabz[k]
											)
											menu.options[v.name][g_name][v2.name][5][1][i][1] = v2.extra.color[i]
											menu.options[v.name][g_name][v2.name][5][1][i][3] = { v1.x + v1.width - 38 - ((i - 1) * 34), y_pos + v1.y - 1 }
											menu.options[v.name][g_name][v2.name][5][1][i][5] = false
											menu.options[v.name][g_name][v2.name][5][1][i][6] = v2.extra.name[i]
										end
									end
								end
								y_pos += 18
							elseif v2.type == "slider" then
								menu.options[v.name][g_name][v2.name] = {}
								menu.options[v.name][g_name][v2.name][4] = Draw:Slider(
									v2.name,
									v2.stradd,
									v2.value,
									v2.minvalue,
									v2.maxvalue,
									v2.custom or {},
									v2.decimal,
									v1.x + 8,
									v1.y + y_pos,
									v1.width - 16,
									tabz[k]
								)
								menu.options[v.name][g_name][v2.name][1] = v2.value
								menu.options[v.name][g_name][v2.name][2] = v2.type
								menu.options[v.name][g_name][v2.name][3] = { v1.x + 7, v1.y + y_pos - 1, v1.width - 16 }
								menu.options[v.name][g_name][v2.name][5] = false
								menu.options[v.name][g_name][v2.name][6] = { v2.minvalue, v2.maxvalue }
								menu.options[v.name][g_name][v2.name][7] = { v1.x + 7 + v1.width - 38, v1.y + y_pos - 1 }
								menu.options[v.name][g_name][v2.name].decimal = v2.decimal == nil and nil or v2.decimal
								menu.options[v.name][g_name][v2.name].stepsize = v2.stepsize
								menu.options[v.name][g_name][v2.name].custom = v2.custom or {}

								y_pos += 30
							elseif v2.type == "dropbox" then
								menu.options[v.name][g_name][v2.name] = {}
								menu.options[v.name][g_name][v2.name][1] = v2.value
								menu.options[v.name][g_name][v2.name][2] = v2.type
								menu.options[v.name][g_name][v2.name][5] = false
								menu.options[v.name][g_name][v2.name][6] = v2.values

								if v2.x == nil then
									menu.options[v.name][g_name][v2.name][3] = { v1.x + 7, v1.y + y_pos - 1, v1.width - 16 }
									menu.options[v.name][g_name][v2.name][4] = Draw:Dropbox(
										v2.name,
										v2.value,
										v2.values,
										v1.x + 8,
										v1.y + y_pos,
										v1.width - 16,
										tabz[k]
									)
									y_pos += 40
								else
									menu.options[v.name][g_name][v2.name][3] = { v2.x + 7, v2.y - 1, v2.w }
									menu.options[v.name][g_name][v2.name][4] = Draw:Dropbox(v2.name, v2.value, v2.values, v2.x + 8, v2.y, v2.w, tabz[k])
								end
							elseif v2.type == "combobox" then
								menu.options[v.name][g_name][v2.name] = {}
								menu.options[v.name][g_name][v2.name][4] = Draw:Combobox(
										v2.name,
										v2.values,
										v1.x + 8,
										v1.y + y_pos,
										v1.width - 16,
										tabz[k]
									)
								menu.options[v.name][g_name][v2.name][1] = v2.values
								menu.options[v.name][g_name][v2.name][2] = v2.type
								menu.options[v.name][g_name][v2.name][3] = { v1.x + 7, v1.y + y_pos - 1, v1.width - 16 }
								menu.options[v.name][g_name][v2.name][5] = false
								y_pos += 40
							elseif v2.type == "button" then
								menu.options[v.name][g_name][v2.name] = {}
								menu.options[v.name][g_name][v2.name][1] = false
								menu.options[v.name][g_name][v2.name][2] = v2.type
								menu.options[v.name][g_name][v2.name].name = v2.name
								menu.options[v.name][g_name][v2.name].groupbox = g_name
								menu.options[v.name][g_name][v2.name].tab = v.name -- why is it all v, v1, v2 so ugly
								menu.options[v.name][g_name][v2.name].doubleclick = v2.doubleclick

								if v2.x == nil then
									menu.options[v.name][g_name][v2.name][3] = { v1.x + 7, v1.y + y_pos - 1, v1.width - 16 }
									menu.options[v.name][g_name][v2.name][4] = Draw:Button(v2.name, v1.x + 8, v1.y + y_pos, v1.width - 16, tabz[k])
									y_pos += 28
								else
									menu.options[v.name][g_name][v2.name][3] = { v2.x + 7, v2.y - 1, v2.w }
									menu.options[v.name][g_name][v2.name][4] = Draw:Button(v2.name, v2.x + 8, v2.y, v2.w, tabz[k])
								end
							elseif v2.type == "textbox" then
								menu.options[v.name][g_name][v2.name] = {}
								menu.options[v.name][g_name][v2.name][4] = Draw:TextBox(v2.name, v2.text, v1.x + 8, v1.y + y_pos, v1.width - 16, tabz[k])
								menu.options[v.name][g_name][v2.name][1] = v2.text
								menu.options[v.name][g_name][v2.name][2] = v2.type
								menu.options[v.name][g_name][v2.name][3] = { v1.x + 7, v1.y + y_pos - 1, v1.width - 16 }
								menu.options[v.name][g_name][v2.name][5] = false
								menu.options[v.name][g_name][v2.name][6] = v2.file and true or false
								y_pos += 28
							elseif v2.type == "list" then
								menu.options[v.name][g_name][v2.name] = {}
								menu.options[v.name][g_name][v2.name][4] = Draw:List(
									v2.multiname,
									v1.x + 8,
									v1.y + y_pos,
									v1.width - 16,
									v2.size,
									v2.columns,
									tabz[k]
								)
								menu.options[v.name][g_name][v2.name][1] = nil
								menu.options[v.name][g_name][v2.name][2] = v2.type
								menu.options[v.name][g_name][v2.name][3] = 1
								menu.options[v.name][g_name][v2.name][5] = {}
								menu.options[v.name][g_name][v2.name][6] = v2.size
								menu.options[v.name][g_name][v2.name][7] = v2.columns
								menu.options[v.name][g_name][v2.name][8] = { v1.x + 8, v1.y + y_pos, v1.width - 16 }
								y_pos += 22 + (22 * v2.size)
							elseif v2.type == "image" then
								menu.options[v.name][g_name][v2.name] = {}
								menu.options[v.name][g_name][v2.name][1] = Draw:ImageWithText(v2.size, nil, v2.text, v1.x + 8, v1.y + y_pos, tabz[k])
								menu.options[v.name][g_name][v2.name][2] = v2.type
							end
						end
					end

					menu.log_multi = nil
				end

				y_pos += 2

				if type(v1.name) ~= "table" then
					if v1.autopos == nil then
						Draw:CoolBox(v1.name, v1.x, v1.y, v1.width, v1.height, tabz[k])
					else
						if v1.autofill then
							y_pos = (menu.h - 17) - v1.y
						elseif v1.size ~= nil then
							y_pos = v1.size
						end
						Draw:CoolBox(v1.name, v1.x, v1.y, v1.width, y_pos, tabz[k])
						y_offies[v1.autopos] += y_pos + 6
					end
				else
					if v1.autofill then
						y_pos = (menu.h - 17) - v1.y
						y_offies[v1.autopos] += y_pos + 6
					elseif v1.size ~= nil then
						y_pos = v1.size
						y_offies[v1.autopos] += y_pos + 6
					end

					local drawn

					if v1.autopos == nil then
						drawn = Draw:CoolMultiBox(v1.name, v1.x, v1.y, v1.width, v1.height, tabz[k])
					else
						drawn = Draw:CoolMultiBox(v1.name, v1.x, v1.y, v1.width, y_pos, tabz[k])
					end

					local group_vals = {}

					for _i, _v in ipairs(v1.name) do
						if _i == 1 then
							group_vals[_v] = true
						else
							group_vals[_v] = false
						end
					end
					table.insert(menu.multigroups[v.name], { vals = group_vals, drawn = drawn })
				end
			end
		end
	end

	menu.list.addval = function(list, option)
		table.insert(list[5], option)
	end

	menu.list.removeval = function(list, optionnum)
		if list[1] == optionnum then
			list[1] = nil
		end
		table.remove(list[5], optionnum)
	end

	menu.list.removeall = function(list)
		list[5] = {}
		for k, v in pairs(list[4].liststuff) do
			for i, v1 in ipairs(v) do
				for i1, v2 in ipairs(v1) do
					v2.Visible = false
				end
			end
		end
	end

	menu.list.setval = function(list, value)
		list[1] = value
	end

	Draw:MenuOutlinedRect(true, 10, 59, menu.w - 20, menu.h - 69, { 20, 20, 20, 255 }, bbmenu)

	Draw:MenuOutlinedRect(true, 11, 58, ((menu.w - 20) / #menutable) - 2, 2, { 35, 35, 35, 255 }, bbmenu)
	local barguy = { bbmenu[#bbmenu], menu.postable[#menu.postable] }

	local function setActiveTab(slot)
		barguy[1].Position = Vector2.new(
			(menu.x + 11 + ((((menu.w - 20) / #menutable) - 2) * (slot - 1))) + ((slot - 1) * 2),
			menu.y + 58
		)
		barguy[2][2] = (11 + ((((menu.w - 20) / #menutable) - 2) * (slot - 1))) + ((slot - 1) * 2)
		barguy[2][3] = 58

		for k, v in pairs(tabs) do
			if k == slot then
				v[1].Visible = false
				v[3].Color = RGB(255, 255, 255)
			else
				v[3].Color = RGB(170, 170, 170)
				v[1].Visible = true
			end
		end

		for k, v in pairs(tabz) do
			if k == slot then
				for k1, v1 in pairs(v) do
					v1.Visible = true
				end
			else
				for k1, v1 in pairs(v) do
					v1.Visible = false
				end
			end
		end

		for k, v in pairs(menu.multigroups) do
			if menu.tabnames[menu.activetab] == k then
				for k1, v1 in pairs(v) do
					for k2, v2 in pairs(v1.vals) do
						for k3, v3 in pairs(menu.mgrouptabz[k][k2]) do
							v3.Visible = v2
						end
					end
				end
			end
		end
	end

	setActiveTab(menu.activetab)

	local plusminus = {}

	Draw:OutlinedText("_", 1, false, 10, 10, 14, false, { 225, 225, 225, 255 }, { 20, 20, 20 }, plusminus)
	Draw:OutlinedText("+", 1, false, 10, 10, 14, false, { 225, 225, 225, 255 }, { 20, 20, 20 }, plusminus)

	local function set_plusminus(value, x, y)
		for i, v in ipairs(plusminus) do
			if value == 0 then
				v.Visible = false
			else
				v.Visible = true
			end
		end

		if value ~= 0 then
			plusminus[1].Position = Vector2.new(x + 3 + menu.x, y - 5 + menu.y)
			plusminus[2].Position = Vector2.new(x + 13 + menu.x, y - 1 + menu.y)

			if value == 1 then
				for i, v in ipairs(plusminus) do
					v.Color = RGB(225, 225, 225)
					v.OutlineColor = RGB(20, 20, 20)
				end
			else
				for i, v in ipairs(plusminus) do
					if i + 1 == value then
						v.Color = RGB(menu.mc[1], menu.mc[2], menu.mc[3])
					else
						v.Color = RGB(255, 255, 255)
					end
					v.OutlineColor = RGB(0, 0, 0)
				end
			end
		end
	end

	set_plusminus(0, 20, 20)

	--DROP BOX THINGY
	local dropboxthingy = {}
	local dropboxtexty = {}

	Draw:OutlinedRect(false, 20, 20, 100, 22, { 20, 20, 20, 255 }, dropboxthingy)
	Draw:OutlinedRect(false, 21, 21, 98, 20, { 0, 0, 0, 255 }, dropboxthingy)
	Draw:FilledRect(false, 22, 22, 96, 18, { 45, 45, 45, 255 }, dropboxthingy)

	for i = 1, 30 do
		Draw:OutlinedText("", 2, false, 20, 20, 13, false, { 255, 255, 255, 255 }, { 0, 0, 0 }, dropboxtexty)
	end

	local function set_dropboxthingy(visible, x, y, length, value, values)
		for k, v in pairs(dropboxthingy) do
			v.Visible = visible
		end

		dropboxthingy[1].Position = Vector2.new(x, y)
		dropboxthingy[2].Position = Vector2.new(x + 1, y + 1)
		dropboxthingy[3].Position = Vector2.new(x + 2, y + 22)

		dropboxthingy[1].Size = Vector2.new(length, 21 * (#values + 1) + 3)
		dropboxthingy[2].Size = Vector2.new(length - 2, (21 * (#values + 1)) + 1)
		dropboxthingy[3].Size = Vector2.new(length - 4, (21 * #values) + 1 - 1)

		if visible then
			for i = 1, #values do
				dropboxtexty[i].Position = Vector2.new(x + 6, y + 26 + ((i - 1) * 21))
				dropboxtexty[i].Visible = true
				dropboxtexty[i].Text = values[i]
				if i == value then
					dropboxtexty[i].Color = RGB(menu.mc[1], menu.mc[2], menu.mc[3])
				else
					dropboxtexty[i].Color = RGB(255, 255, 255)
				end
			end
		else
			for k, v in pairs(dropboxtexty) do
				v.Visible = false
			end
		end
	end

	local function set_comboboxthingy(visible, x, y, length, values)
		for k, v in pairs(dropboxthingy) do
			v.Visible = visible
		end

		dropboxthingy[1].Position = Vector2.new(x, y)
		dropboxthingy[2].Position = Vector2.new(x + 1, y + 1)
		dropboxthingy[3].Position = Vector2.new(x + 2, y + 22)

		dropboxthingy[1].Size = Vector2.new(length, 22 * (#values + 1) + 2)
		dropboxthingy[2].Size = Vector2.new(length - 2, (22 * (#values + 1)))
		dropboxthingy[3].Size = Vector2.new(length - 4, (22 * #values))

		if visible then
			for i = 1, #values do
				dropboxtexty[i].Position = Vector2.new(x + 6, y + 26 + ((i - 1) * 22))
				dropboxtexty[i].Visible = true
				dropboxtexty[i].Text = values[i][1]
				if values[i][2] then
					dropboxtexty[i].Color = RGB(menu.mc[1], menu.mc[2], menu.mc[3])
				else
					dropboxtexty[i].Color = RGB(255, 255, 255)
				end
			end
		else
			for k, v in pairs(dropboxtexty) do
				v.Visible = false
			end
		end
	end

	set_dropboxthingy(false, 400, 200, 160, 1, { "HI q", "HI q", "HI q" })

	--MODE SELECT THING
	local modeselect = {}

	Draw:OutlinedRect(false, 20, 20, 100, 22, { 20, 20, 20, 255 }, modeselect)
	Draw:OutlinedRect(false, 21, 21, 98, 20, { 0, 0, 0, 255 }, modeselect)
	Draw:FilledRect(false, 22, 22, 96, 18, { 45, 45, 45, 255 }, modeselect)

	local modeselecttext = { "Hold", "Toggle", "Hold Off", "Always" }
	for i = 1, 4 do
		Draw:OutlinedText(
			modeselecttext[i],
			2,
			false,
			20,
			20,
			13,
			false,
			{ 255, 255, 255, 255 },
			{ 0, 0, 0 },
			modeselect
		)
	end

	local function set_modeselect(visible, x, y, value)
		for k, v in pairs(modeselect) do
			v.Visible = visible
		end

		if visible then
			modeselect[1].Position = Vector2.new(x, y)
			modeselect[2].Position = Vector2.new(x + 1, y + 1)
			modeselect[3].Position = Vector2.new(x + 2, y + 2)

			modeselect[1].Size = Vector2.new(70, 22 * 4 - 1)
			modeselect[2].Size = Vector2.new(70 - 2, 22 * 4 - 3)
			modeselect[3].Size = Vector2.new(70 - 4, 22 * 4 - 5)

			for i = 1, 4 do
				modeselect[i + 3].Position = Vector2.new(x + 6, y + 4 + ((i - 1) * 21))
				if value == i then
					modeselect[i + 3].Color = RGB(menu.mc[1], menu.mc[2], menu.mc[3])
				else
					modeselect[i + 3].Color = RGB(255, 255, 255)
				end
			end
		end
	end

	set_modeselect(false, 200, 400, 1)

	--COLOR PICKER
	local cp = {
		x = 400,
		y = 40,
		w = 280,
		h = 211,
		alpha = false,
		dragging_m = false,
		dragging_r = false,
		dragging_b = false,
		hsv = {
			h = 0,
			s = 0,
			v = 0,
			a = 0,
		},
		postable = {},
		drawings = {},
	}

	local function ColorpickerOutline(visible, pos_x, pos_y, width, height, clr, tablename) -- doing all this shit to make it easier for me to make this beat look nice and shit ya fell dog :dog_head:
		Draw:OutlinedRect(visible, pos_x + cp.x, pos_y + cp.y, width, height, clr, tablename)
		table.insert(cp.postable, { tablename[#tablename], pos_x, pos_y })
	end

	local function ColorpickerRect(visible, pos_x, pos_y, width, height, clr, tablename)
		Draw:FilledRect(visible, pos_x + cp.x, pos_y + cp.y, width, height, clr, tablename)
		table.insert(cp.postable, { tablename[#tablename], pos_x, pos_y })
	end

	local function ColorpickerImage(visible, imagedata, pos_x, pos_y, width, height, transparency, tablename)
		Draw:Image(visible, imagedata, pos_x, pos_y, width, height, transparency, tablename)
		table.insert(cp.postable, { tablename[#tablename], pos_x, pos_y })
	end

	local function ColorpickerText(text, visible, centered, pos_x, pos_y, tablename)
		Draw:OutlinedText(
			text,
			2,
			visible,
			pos_x + cp.x,
			pos_y + cp.y,
			13,
			centered,
			{ 255, 255, 255, 255 },
			{ 0, 0, 0 },
			tablename
		)
		table.insert(cp.postable, { tablename[#tablename], pos_x, pos_y })
	end

	ColorpickerRect(false, 1, 1, cp.w, cp.h, { 35, 35, 35, 255 }, cp.drawings)
	ColorpickerOutline(false, 1, 1, cp.w, cp.h, { 0, 0, 0, 255 }, cp.drawings)
	ColorpickerOutline(false, 2, 2, cp.w - 2, cp.h - 2, { 20, 20, 20, 255 }, cp.drawings)
	ColorpickerOutline(false, 3, 3, cp.w - 3, 1, { 127, 72, 163, 255 }, cp.drawings)
	table.insert(menu.clrs.norm, cp.drawings[#cp.drawings])
	ColorpickerOutline(false, 3, 4, cp.w - 3, 1, { 87, 32, 123, 255 }, cp.drawings)
	table.insert(menu.clrs.dark, cp.drawings[#cp.drawings])
	ColorpickerOutline(false, 3, 5, cp.w - 3, 1, { 20, 20, 20, 255 }, cp.drawings)
	ColorpickerText("color picker :D", false, false, 7, 6, cp.drawings)

	ColorpickerText("x", false, false, 268, 4, cp.drawings)

	ColorpickerOutline(false, 10, 23, 160, 160, { 30, 30, 30, 255 }, cp.drawings)
	ColorpickerOutline(false, 11, 24, 158, 158, { 0, 0, 0, 255 }, cp.drawings)
	ColorpickerRect(false, 12, 25, 156, 156, { 0, 0, 0, 255 }, cp.drawings)
	local maincolor = cp.drawings[#cp.drawings]
	ColorpickerImage(false, BBOT_IMAGES[1], 12, 25, 156, 156, 1, cp.drawings)

	--https://i.imgur.com/jG3NjxN.png
	local alphabar = {}
	ColorpickerOutline(false, 10, 189, 160, 14, { 30, 30, 30, 255 }, cp.drawings)
	table.insert(alphabar, cp.drawings[#cp.drawings])
	ColorpickerOutline(false, 11, 190, 158, 12, { 0, 0, 0, 255 }, cp.drawings)
	table.insert(alphabar, cp.drawings[#cp.drawings])
	ColorpickerImage(false, BBOT_IMAGES[2], 12, 191, 159, 10, 1, cp.drawings)
	table.insert(alphabar, cp.drawings[#cp.drawings])

	ColorpickerOutline(false, 176, 23, 14, 160, { 30, 30, 30, 255 }, cp.drawings)
	ColorpickerOutline(false, 177, 24, 12, 158, { 0, 0, 0, 255 }, cp.drawings)
	--https://i.imgur.com/2Ty4u2O.png
	ColorpickerImage(false, BBOT_IMAGES[3], 178, 25, 10, 156, 1, cp.drawings)

	ColorpickerText("New Color", false, false, 198, 23, cp.drawings)
	ColorpickerOutline(false, 197, 37, 75, 40, { 30, 30, 30, 255 }, cp.drawings)
	ColorpickerOutline(false, 198, 38, 73, 38, { 0, 0, 0, 255 }, cp.drawings)
	ColorpickerImage(false, BBOT_IMAGES[4], 199, 39, 71, 36, 1, cp.drawings)

	ColorpickerRect(false, 199, 39, 71, 36, { 255, 0, 0, 255 }, cp.drawings)
	local newcolor = cp.drawings[#cp.drawings]

	ColorpickerText("copy", false, true, 198 + 36, 41, cp.drawings)
	ColorpickerText("paste", false, true, 198 + 37, 56, cp.drawings)
	local newcopy = { cp.drawings[#cp.drawings - 1], cp.drawings[#cp.drawings] }

	ColorpickerText("Old Color", false, false, 198, 77, cp.drawings)
	ColorpickerOutline(false, 197, 91, 75, 40, { 30, 30, 30, 255 }, cp.drawings)
	ColorpickerOutline(false, 198, 92, 73, 38, { 0, 0, 0, 255 }, cp.drawings)
	ColorpickerImage(false, BBOT_IMAGES[4], 199, 93, 71, 36, 1, cp.drawings)

	ColorpickerRect(false, 199, 93, 71, 36, { 255, 0, 0, 255 }, cp.drawings)
	local oldcolor = cp.drawings[#cp.drawings]

	ColorpickerText("copy", false, true, 198 + 36, 103, cp.drawings)
	local oldcopy = { cp.drawings[#cp.drawings] }

	--ColorpickerRect(false, 197, cp.h - 25, 75, 20, {30, 30, 30, 255}, cp.drawings)
	ColorpickerText("[ Apply ]", false, true, 235, cp.h - 23, cp.drawings)
	local applytext = cp.drawings[#cp.drawings]

	local function set_newcolor(r, g, b, a)
		newcolor.Color = RGB(r, g, b)
		if a ~= nil then
			newcolor.Transparency = a / 255
		else
			newcolor.Transparency = 1
		end
	end

	local function set_oldcolor(r, g, b, a)
		oldcolor.Color = RGB(r, g, b)
		if a ~= nil then
			oldcolor.Transparency = a / 255
		else
			oldcolor.Transparency = 1
		end
	end
	-- all this color picker shit is disgusting, why can't it be in it's own fucking scope. these are all global
	local dragbar_r = {}
	Draw:OutlinedRect(true, 30, 30, 16, 5, { 0, 0, 0, 255 }, cp.drawings)
	table.insert(dragbar_r, cp.drawings[#cp.drawings])
	Draw:OutlinedRect(true, 31, 31, 14, 3, { 255, 255, 255, 255 }, cp.drawings)
	table.insert(dragbar_r, cp.drawings[#cp.drawings])

	local dragbar_b = {}
	Draw:OutlinedRect(true, 30, 30, 5, 16, { 0, 0, 0, 255 }, cp.drawings)
	table.insert(dragbar_b, cp.drawings[#cp.drawings])
	table.insert(alphabar, cp.drawings[#cp.drawings])
	Draw:OutlinedRect(true, 31, 31, 3, 14, { 255, 255, 255, 255 }, cp.drawings)
	table.insert(dragbar_b, cp.drawings[#cp.drawings])
	table.insert(alphabar, cp.drawings[#cp.drawings])

	local dragbar_m = {}
	Draw:OutlinedRect(true, 30, 30, 5, 5, { 0, 0, 0, 255 }, cp.drawings)
	table.insert(dragbar_m, cp.drawings[#cp.drawings])
	Draw:OutlinedRect(true, 31, 31, 3, 3, { 255, 255, 255, 255 }, cp.drawings)
	table.insert(dragbar_m, cp.drawings[#cp.drawings])

	local function set_dragbar_r(x, y)
		dragbar_r[1].Position = Vector2.new(x, y)
		dragbar_r[2].Position = Vector2.new(x + 1, y + 1)
	end

	local function set_dragbar_b(x, y)
		dragbar_b[1].Position = Vector2.new(x, y)
		dragbar_b[2].Position = Vector2.new(x + 1, y + 1)
	end

	local function set_dragbar_m(x, y)
		dragbar_m[1].Position = Vector2.new(x, y)
		dragbar_m[2].Position = Vector2.new(x + 1, y + 1)
	end

	local function set_colorpicker(visible, color, value, alpha, text, x, y)
		for k, v in pairs(cp.drawings) do
			v.Visible = visible
		end

		if visible then
			cp.x = clamp(x, 0, SCREEN_SIZE.x - cp.w)
			cp.y = clamp(y, 0, SCREEN_SIZE.y - cp.h)
			for k, v in pairs(cp.postable) do
				v[1].Position = Vector2.new(cp.x + v[2], cp.y + v[3])
			end

			local tempclr = RGB(color[1], color[2], color[3])
			local h, s, v = tempclr:ToHSV()
			cp.hsv.h = h
			cp.hsv.s = s
			cp.hsv.v = v

			set_dragbar_r(cp.x + 175, cp.y + 23 + math.floor((1 - h) * 156))
			set_dragbar_m(cp.x + 9 + math.floor(s * 156), cp.y + 23 + math.floor((1 - v) * 156))
			if not alpha then
				set_newcolor(color[1], color[2], color[3])
				set_oldcolor(color[1], color[2], color[3])
				cp.alpha = false
				for k, v in pairs(alphabar) do
					v.Visible = false
				end
				cp.h = 191
				for i = 1, 2 do
					cp.drawings[i].Size = Vector2.new(cp.w, cp.h)
				end
				cp.drawings[3].Size = Vector2.new(cp.w - 2, cp.h - 2)
			else
				cp.hsv.a = color[4]
				cp.alpha = true
				set_newcolor(color[1], color[2], color[3], color[4])
				set_oldcolor(color[1], color[2], color[3], color[4])
				cp.h = 211
				for i = 1, 2 do
					cp.drawings[i].Size = Vector2.new(cp.w, cp.h)
				end
				cp.drawings[3].Size = Vector2.new(cp.w - 2, cp.h - 2)
				set_dragbar_b(cp.x + 12 + math.floor(156 * (color[4] / 255)), cp.y + 188)
			end

			applytext.Position = Vector2.new(235 + cp.x, cp.y + cp.h - 23)
			maincolor.Color = Color3.fromHSV(h, 1, 1)
			cp.drawings[7].Text = text
		end
	end

	set_colorpicker(false, { 255, 0, 0 }, nil, false, "", 0, 0)

	--TOOL TIP
	local tooltip = {
		x = 0,
		y = 0,
		time = 0,
		active = false,
		text = "This does this and that i guess\npooping 24/7",
		drawings = {},
		postable = {},
	}

	local function ttOutline(visible, pos_x, pos_y, width, height, clr, tablename)
		Draw:OutlinedRect(visible, pos_x + tooltip.x, pos_y + tooltip.y, width, height, clr, tablename)
		table.insert(tooltip.postable, { tablename[#tablename], pos_x, pos_y })
	end

	local function ttRect(visible, pos_x, pos_y, width, height, clr, tablename)
		Draw:FilledRect(visible, pos_x + tooltip.x, pos_y + tooltip.y, width, height, clr, tablename)
		table.insert(tooltip.postable, { tablename[#tablename], pos_x, pos_y })
	end

	local function ttText(text, visible, centered, pos_x, pos_y, tablename)
		Draw:OutlinedText(
			text,
			2,
			visible,
			pos_x + tooltip.x,
			pos_y + tooltip.y,
			13,
			centered,
			{ 255, 255, 255, 255 },
			{ 0, 0, 0 },
			tablename
		)
		table.insert(tooltip.postable, { tablename[#tablename], pos_x, pos_y })
	end

	ttRect(
		false,
		tooltip.x + 1,
		tooltip.y + 1,
		1,
		28,
		{ menu.mc[1], menu.mc[2], menu.mc[3], 255 },
		tooltip.drawings
	)
	ttRect(
		false,
		tooltip.x + 2,
		tooltip.y + 1,
		1,
		28,
		{ menu.mc[1] - 40, menu.mc[2] - 40, menu.mc[3] - 40, 255 },
		tooltip.drawings
	)
	ttOutline(false, tooltip.x, tooltip.y, 4, 30, { 20, 20, 20, 255 }, tooltip.drawings)
	ttRect(false, tooltip.x + 4, tooltip.y, 100, 30, { 40, 40, 40, 255 }, tooltip.drawings)
	ttOutline(false, tooltip.x - 1, tooltip.y - 1, 102, 32, { 0, 0, 0, 255 }, tooltip.drawings)
	ttOutline(false, tooltip.x + 3, tooltip.y, 102, 30, { 20, 20, 20, 255 }, tooltip.drawings)
	ttText(tooltip.text, false, false, tooltip.x + 7, tooltip.y + 1, tooltip.drawings)

	local function set_tooltip(x, y, text, visible, dt)
		dt = dt or 0
		x = x or tooltip.x
		y = y or tooltip.y
		tooltip.x = x
		tooltip.y = y
		if tooltip.time < 1 and visible then
			if tooltip.time < -2 then
				tooltip.time = -2
			end
			tooltip.time += dt
		else
			tooltip.time -= dt
			if tooltip.time < -1 then
				tooltip.time = -1
			end
		end
		if tooltip.time > 1 then
			tooltip.time = 1
		end
		for k, v in ipairs(tooltip.drawings) do
			v.Visible = tooltip.time > 0
		end

		tooltip.active = visible
		if text then
			tooltip.drawings[7].Text = text
		end
		for k, v in pairs(tooltip.postable) do
			v[1].Position = Vector2.new(x + v[2], y + v[3])
			v[1].Transparency = (0.3 + tooltip.time) ^ 3 - 1
			if not menu.open then
				v[1].Transparency = 0
			end
		end
		tooltip.drawings[1].Color = RGB(menu.mc[1], menu.mc[2], menu.mc[3])
		tooltip.drawings[2].Color = RGB(menu.mc[1] - 40, menu.mc[2] - 40, menu.mc[3] - 40)

		local tb = tooltip.drawings[7].TextBounds

		tooltip.drawings[1].Size = Vector2.new(1, tb.Y + 3)
		tooltip.drawings[2].Size = Vector2.new(1, tb.Y + 3)
		tooltip.drawings[3].Size = Vector2.new(4, tb.Y + 5)
		tooltip.drawings[4].Size = Vector2.new(tb.X + 6, tb.Y + 5)
		tooltip.drawings[5].Size = Vector2.new(tb.X + 12, tb.Y + 7)
		tooltip.drawings[6].Size = Vector2.new(tb.X + 7, tb.Y + 5)
	end

	set_tooltip(500, 500, "", false)

	-- mouse shiz
	local bbmouse = {}
	local mousie = {
		x = 100,
		y = 240,
	}
	Draw:Triangle(
		true,
		true,
		{ mousie.x, mousie.y },
		{ mousie.x, mousie.y + 15 },
		{ mousie.x + 10, mousie.y + 10 },
		{ 127, 72, 163, 255 },
		bbmouse
	)
	table.insert(menu.clrs.norm, bbmouse[#bbmouse])
	Draw:Triangle(
		true,
		false,
		{ mousie.x, mousie.y },
		{ mousie.x, mousie.y + 15 },
		{ mousie.x + 10, mousie.y + 10 },
		{ 0, 0, 0, 255 },
		bbmouse
	)
	local lastMousePos = Vector2.new()
	function menu:set_mouse_pos(x, y)
		FireEvent("bb_mousemoved", lastMousePos ~= Vector2.new(x, y))
		for k = 1, #bbmouse do
			local v = bbmouse[k]
			v.PointA = Vector2.new(x, y + 36)
			v.PointB = Vector2.new(x, y + 36 + 15)
			v.PointC = Vector2.new(x + 10, y + 46)
		end
		lastMousePos = Vector2.new(x, y)
	end

	function menu:set_menu_clr(r, g, b)
		menu.watermark.rect[1].Color = RGB(r - 40, g - 40, b - 40)
		menu.watermark.rect[2].Color = RGB(r, g, b)

		for k, v in pairs(menu.clrs.norm) do
			v.Color = RGB(r, g, b)
		end
		for k, v in pairs(menu.clrs.dark) do
			v.Color = RGB(r - 40, g - 40, b - 40)
		end
		local menucolor = { r, g, b }
		for k, v in pairs(menu.options) do
			for k1, v1 in pairs(v) do
				for k2, v2 in pairs(v1) do
					if v2[2] == "toggle" then
						if not v2[1] then
							for i = 0, 3 do
								v2[4][i + 1].Color = ColorRange(i, {
									[1] = { start = 0, color = RGB(50, 50, 50) },
									[2] = { start = 3, color = RGB(30, 30, 30) },
								})
							end
						else
							for i = 0, 3 do
								v2[4][i + 1].Color = ColorRange(i, {
									[1] = { start = 0, color = RGB(menucolor[1], menucolor[2], menucolor[3]) },
									[2] = {
										start = 3,
										color = RGB(menucolor[1] - 40, menucolor[2] - 40, menucolor[3] - 40),
									},
								})
							end
						end
					elseif v2[2] == "slider" then
						for i = 0, 3 do
							v2[4][i + 1].Color = ColorRange(i, {
								[1] = { start = 0, color = RGB(menucolor[1], menucolor[2], menucolor[3]) },
								[2] = {
									start = 3,
									color = RGB(menucolor[1] - 40, menucolor[2] - 40, menucolor[3] - 40),
								},
							})
						end
					end
				end
			end
		end
	end

	local function UpdateConfigs()
		local configthing = menu.options["Settings"]["Configuration"]["Configs"]

		configthing[6] = GetConfigs()
		if configthing[1] > #configthing[6] then
			configthing[1] = #configthing[6]
		end
		configthing[4][1].Text = configthing[6][configthing[1]]
	end

	menu.keybind_open = nil

	menu.dropbox_open = nil

	menu.colorpicker_open = false

	menu.textboxopen = nil

	function menu:InputBeganMenu(key) --ANCHOR menu input
		if key.KeyCode == Enum.KeyCode.RightShift and not loadingthing.Visible then
			cp.dragging_m = false
			cp.dragging_r = false
			cp.dragging_b = false

			UpdateConfigs()
			if menu.open and not menu.fading then
				for k = 1, #menu.options do
					local v = menu.options[k]
					for k1, v1 in pairs(v) do
						for k2, v2 in pairs(v1) do
							if v2[2] == "slider" and v2[5] then
								v2[5] = false
							elseif v2[2] == "dropbox" and v2[5] then
								v2[5] = false
							elseif v2[2] == "combobox" and v2[5] then
								v2[5] = false
							elseif v2[2] == "toggle" then
								if v2[5] ~= nil then
									if v2[5][2] == "keybind" and v2[5][5] then
										v2[5][4][2].Color = RGB(30, 30, 30)
										v2[5][5] = false
									elseif v2[5][2] == "single colorpicker" and v2[5][5] then
										v2[5][5] = false
									end
								end
							elseif v2[2] == "button" then
								if v2[1] then
									for i = 0, 8 do
										v2[4][i + 1].Color = ColorRange(i, {
											[1] = { start = 0, color = RGB(50, 50, 50) },
											[2] = { start = 8, color = RGB(35, 35, 35) },
										})
									end
									v2[1] = false
								end
							end
						end
					end
				end
				menu.keybind_open = nil
				set_modeselect(false, 20, 20, 1)
				menu.dropbox_open = nil
				set_dropboxthingy(false, 400, 200, 160, 1, { "HI q", "HI q", "HI q" })
				menu.colorpicker_open = nil
				set_tooltip(nil, nil, nil, false)
				set_colorpicker(false, { 255, 0, 0 }, nil, false, "hahaha", 400, 200)
			end
			if not menu.fading then
				menu.fading = true
				menu.fadestart = tick()
			end
		end

		if menu == nil then
			return
		end

		if menu.textboxopen then
			if key.KeyCode == Enum.KeyCode.RightShift or key.KeyCode == Enum.KeyCode.Return then
				for k, v in pairs(menu.options) do
					for k1, v1 in pairs(v) do
						for k2, v2 in pairs(v1) do
							if v2[2] == "textbox" then
								if v2[5] then
									v2[5] = false
									v2[4].Color = RGB(255, 255, 255)
									menu.textboxopen = false
									v2[4].Text = v2[1]
								end
							end
						end
					end
				end
			end
		end

		if menu.open and not menu.fading then
			for k, v in pairs(menu.options) do
				for k1, v1 in pairs(v) do
					for k2, v2 in pairs(v1) do
						if v2[2] == "toggle" then
							if v2[5] ~= nil then
								if v2[5][2] == "keybind" and v2[5][5] and key.KeyCode.Value ~= 0 then
									v2[5][4][2].Color = RGB(30, 30, 30)
									v2[5][4][1].Text = KeyEnumToName(key.KeyCode)
									if KeyEnumToName(key.KeyCode) == "None" then
										v2[5][1] = nil
									else
										v2[5][1] = key.KeyCode
									end
									v2[5][5] = false
								end
							end
						elseif v2[2] == "textbox" then --ANCHOR TEXTBOXES
							if v2[5] then
								if not INPUT_SERVICE:IsKeyDown(Enum.KeyCode.LeftControl) then
									if string.len(v2[1]) <= 28 then
										if table.find(textBoxLetters, KeyEnumToName(key.KeyCode)) then
											if INPUT_SERVICE:IsKeyDown(Enum.KeyCode.LeftShift) then
												v2[1] ..= string.upper(KeyEnumToName(key.KeyCode))
											else
												v2[1] ..= string.lower(KeyEnumToName(key.KeyCode))
											end
										elseif KeyEnumToName(key.KeyCode) == "Space" then
											v2[1] ..= " "
										elseif keymodifiernames[KeyEnumToName(key.KeyCode)] ~= nil then
											if INPUT_SERVICE:IsKeyDown(Enum.KeyCode.LeftShift) then
												v2[1] ..= KeyModifierToName(KeyEnumToName(key.KeyCode), v2[6])
											else
												v2[1] ..= KeyEnumToName(key.KeyCode)
											end
										elseif KeyEnumToName(key.KeyCode) == "Back" and v2[1] ~= "" then
											v2[1] = string.sub(v2[1], 0, #v2[1] - 1)
										end
									end
									v2[4].Text = v2[1] .. "|"
								end
							end
						end
					end
				end
			end
		end
	end

	function menu:InputBeganKeybinds(key) -- this is super shit because once we add mouse we need to change all this shit to be the contextaction stuff
		if INPUT_SERVICE:GetFocusedTextBox() or menu.textboxopen then
			return
		end
		for i = 1, #self.keybinds do
			local value = self.keybinds[i][1]
			if key.KeyCode == value[5][1] then
				value[5].lastvalue = value[5].relvalue
				if value[5].toggletype == 2 then
					value[5].relvalue = not value[5].relvalue
				elseif value[5].toggletype == 1 then
					value[5].relvalue = true
				elseif value[5].toggletype == 3 then
					value[5].relvalue = false
				end
			elseif value[5].toggletype == 4 then
				value[5].relvalue = true
			end
			if value[5].lastvalue ~= value[5].relvalue then
				value[5].event:fire(value[5].relvalue)
			end
		end
	end

	function menu:InputEndedKeybinds(key)
		for i = 1, #self.keybinds do
			local value = self.keybinds[i][1]
			value[5].lastvalue = value[5].relvalue
			if key.KeyCode == value[5][1] then
				if value[5].toggletype == 1 then
					value[5].relvalue = false
				elseif value[5].toggletype == 3 then
					value[5].relvalue = true
				end
			end
			if value[5].lastvalue ~= value[5].relvalue then
				value[5].event:fire(value[5].relvalue)
			end
		end
	end

	function menu:SetMenuPos(x, y)
		for k, v in pairs(menu.postable) do
			if v[1].Visible then
				v[1].Position = Vector2.new(x + v[2], y + v[3])
			end
		end
	end

	function menu:MouseInArea(x, y, width, height)
		return LOCAL_MOUSE.x > x and LOCAL_MOUSE.x < x + width and LOCAL_MOUSE.y > 36 + y and LOCAL_MOUSE.y < 36 + y + height
	end

	function menu:MouseInMenu(x, y, width, height)
		return LOCAL_MOUSE.x > menu.x + x and LOCAL_MOUSE.x < menu.x + x + width and LOCAL_MOUSE.y > menu.y - 36 + y and LOCAL_MOUSE.y < menu.y - 36 + y + height
	end

	function menu:MouseInColorPicker(x, y, width, height)
		return LOCAL_MOUSE.x > cp.x + x and LOCAL_MOUSE.x < cp.x + x + width and LOCAL_MOUSE.y > cp.y - 36 + y and LOCAL_MOUSE.y < cp.y - 36 + y + height
	end

	local keyz = {}
	for k, v in pairs(Enum.KeyCode:GetEnumItems()) do
		keyz[v.Value] = v
	end

	function menu:GetVal(tab, groupbox, name, ...)
		local args = { ... }

		local option = menu.options[tab][groupbox][name]

		if args[1] == nil then
			if option[2] == "toggle" then
				local lastval = option[7]
				option[7] = option[1]
				return option[1], lastval
			elseif option[2] ~= "combobox" then
				return option[1]
			else
				local temptable = {}
				for k, v in ipairs(option[1]) do
					table.insert(temptable, v[2])
				end
				return temptable
			end
		else
			if args[1] == "keybind" or args[1] == "color" then
				if args[2] then
					return RGB(option[5][1][1], option[5][1][2], option[5][1][3])
				else
					return option[5][1]
				end
			elseif args[1] == "color1" then
				if args[2] then
					return RGB(option[5][1][1][1][1], option[5][1][1][1][2], option[5][1][1][1][3])
				else
					return option[5][1][1][1]
				end
			elseif args[1] == "color2" then
				if args[2] then
					return RGB(option[5][1][2][1][1], option[5][1][2][1][2], option[5][1][2][1][3])
				else
					return option[5][1][2][1]
				end
			end
		end
	end

	function menu:GetKey(tab, groupbox, name)
		local option = self.options[tab][groupbox][name][5]
		if self:GetVal(tab, groupbox, name) then
			if option.toggletype ~= 0 then
				if option.lastvalue == nil then
					option.lastvalue = option.relvalue
				end
				return option.relvalue, option.lastvalue, option.event
			else
				return false
			end
		end
	end

	function menu:SetKey(tab, groupbox, name, val)
		val = val or false
		local option = menu.options[tab][groupbox][name][5]
		if option.toggletype ~= 0 then
			option.lastvalue = option.relvalue
			option.relvalue = val
			if option.lastvalue ~= option.relvalue then
				option.event:fire(option.relvalue)
			end
		end
	end

	local menuElementTypes = { "toggle", "slider", "dropbox", "textbox" }
	local doubleclickDelay = 4
	local buttonsInQue = {}

	local function SaveCurSettings() --ANCHOR figgies
		local figgy = "BitchBot v2\nmade with <3 by nata and bitch\n\n" -- screw zarzel XD (and json and classy)

		for k, v in next, menuElementTypes do
			figgy ..= v .. "s {\n"
			for k1, v1 in pairs(menu.options) do
				for k2, v2 in pairs(v1) do
					for k3, v3 in pairs(v2) do
						if v3[2] == tostring(v) and k3 ~= "Configs" and k3 ~= "Player Status" and k3 ~= "ConfigName"
						then
							figgy ..= k1 .. "|" .. k2 .. "|" .. k3 .. "|" .. tostring(v3[1]) .. "\n"
						end
					end
				end
			end
			figgy = figgy .. "}\n"
		end
		figgy = figgy .. "comboboxes {\n"
		for k, v in pairs(menu.options) do
			for k1, v1 in pairs(v) do
				for k2, v2 in pairs(v1) do
					if v2[2] == "combobox" then
						local boolz = ""
						for k3, v3 in pairs(v2[1]) do
							boolz = boolz .. tostring(v3[2]) .. ", "
						end
						figgy = figgy .. k .. "|" .. k1 .. "|" .. k2 .. "|" .. boolz .. "\n"
					end
				end
			end
		end
		figgy = figgy .. "}\n"
		figgy = figgy .. "keybinds {\n"
		for k, v in pairs(menu.options) do
			for k1, v1 in pairs(v) do
				for k2, v2 in pairs(v1) do
					if v2[2] == "toggle" then
						if v2[5] ~= nil then
							if v2[5][2] == "keybind" then
								local toggletype = "|" .. tostring(v2[5].toggletype)

								if v2[5][1] == nil then
									figgy = figgy
										.. k
										.. "|"
										.. k1
										.. "|"
										.. k2
										.. "|nil"
										.. "|"
										.. tostring(v2[5].toggletype)
										.. "\n"
								else
									figgy = figgy
										.. k
										.. "|"
										.. k1
										.. "|"
										.. k2
										.. "|"
										.. tostring(v2[5][1].Value)
										.. "|"
										.. tostring(v2[5].toggletype)
										.. "\n"
								end
							end
						end
					end
				end
			end
		end
		figgy = figgy .. "}\n"
		figgy = figgy .. "colorpickers {\n"
		for k, v in pairs(menu.options) do
			for k1, v1 in pairs(v) do
				for k2, v2 in pairs(v1) do
					if v2[2] == "toggle" then
						if v2[5] ~= nil then
							if v2[5][2] == "single colorpicker" then
								local clrz = ""
								for k3, v3 in pairs(v2[5][1]) do
									clrz = clrz .. tostring(v3) .. ", "
								end
								figgy = figgy .. k .. "|" .. k1 .. "|" .. k2 .. "|" .. clrz .. "\n"
							end
						end
					end
				end
			end
		end
		figgy = figgy .. "}\n"
		figgy = figgy .. "double colorpickers {\n"
		for k, v in pairs(menu.options) do
			for k1, v1 in pairs(v) do
				for k2, v2 in pairs(v1) do
					if v2[2] == "toggle" then
						if v2[5] ~= nil then
							if v2[5][2] == "double colorpicker" then
								local clrz1 = ""
								for k3, v3 in pairs(v2[5][1][1][1]) do
									clrz1 = clrz1 .. tostring(v3) .. ", "
								end
								local clrz2 = ""
								for k3, v3 in pairs(v2[5][1][2][1]) do
									clrz2 = clrz2 .. tostring(v3) .. ", "
								end
								figgy = figgy .. k .. "|" .. k1 .. "|" .. k2 .. "|" .. clrz1 .. "|" .. clrz2 .. "\n"
							end
						end
					end
				end
			end
		end
		figgy = figgy .. "}\n"

		return figgy
	end

	local function LoadConfig(loadedcfg)
		local lines = {}

		for s in loadedcfg:gmatch("[^\r\n]+") do
			table.insert(lines, s)
		end

		if lines[1] == "BitchBot v2" then
			local start = nil
			for i, v in next, lines do
				if v == "toggles {" then
					start = i
					break
				end
			end
			local end_ = nil
			for i, v in next, lines do
				if i > start and v == "}" then
					end_ = i
					break
				end
			end
			for i = 1, end_ - start - 1 do
				local tt = string.split(lines[i + start], "|")

				if menu.options[tt[1]] ~= nil and menu.options[tt[1]][tt[2]] ~= nil and menu.options[tt[1]][tt[2]][tt[3]] ~= nil
				then
					if tt[4] == "true" then
						menu.options[tt[1]][tt[2]][tt[3]][1] = true
					else
						menu.options[tt[1]][tt[2]][tt[3]][1] = false
					end
				end
			end

			local start = nil
			for i, v in next, lines do
				if v == "sliders {" then
					start = i
					break
				end
			end
			local end_ = nil
			for i, v in next, lines do
				if i > start and v == "}" then
					end_ = i
					break
				end
			end
			for i = 1, end_ - start - 1 do
				local tt = string.split(lines[i + start], "|")
				if menu.options[tt[1]] ~= nil and menu.options[tt[1]][tt[2]] ~= nil and menu.options[tt[1]][tt[2]][tt[3]] ~= nil
				then
					menu.options[tt[1]][tt[2]][tt[3]][1] = tonumber(tt[4])
				end
			end

			local start = nil
			for i, v in next, lines do
				if v == "dropboxs {" then
					start = i
					break
				end
			end
			local end_ = nil
			for i, v in next, lines do
				if i > start and v == "}" then
					end_ = i
					break
				end
			end
			for i = 1, end_ - start - 1 do
				local tt = string.split(lines[i + start], "|")

				if menu.options[tt[1]] ~= nil and menu.options[tt[1]][tt[2]] ~= nil and menu.options[tt[1]][tt[2]][tt[3]] ~= nil
				then
					local num = tonumber(tt[4])
					if num > #menu.options[tt[1]][tt[2]][tt[3]][6] then
						num = #menu.options[tt[1]][tt[2]][tt[3]][6]
					elseif num < 0 then
						num = 1
					end
					menu.options[tt[1]][tt[2]][tt[3]][1] = num
				end
			end

			local start = nil
			for i, v in next, lines do
				if v == "textboxs {" then
					start = i
					break
				end
			end
			if start ~= nil then
				local end_ = nil
				for i, v in next, lines do
					if i > start and v == "}" then
						end_ = i
						break
					end
				end
				for i = 1, end_ - start - 1 do
					local tt = string.split(lines[i + start], "|")
					if menu.options[tt[1]] ~= nil and menu.options[tt[1]][tt[2]] ~= nil and menu.options[tt[1]][tt[2]][tt[3]] ~= nil
					then
						menu.options[tt[1]][tt[2]][tt[3]][1] = tostring(tt[4])
					end
				end
			end

			local start = nil
			for i, v in next, lines do
				if v == "comboboxes {" then
					start = i
					break
				end
			end
			local end_ = nil
			for i, v in next, lines do
				if i > start and v == "}" then
					end_ = i
					break
				end
			end
			for i = 1, end_ - start - 1 do
				local tt = string.split(lines[i + start], "|")
				if menu.options[tt[1]] ~= nil and menu.options[tt[1]][tt[2]] ~= nil and menu.options[tt[1]][tt[2]][tt[3]] ~= nil
				then
					local subs = string.split(tt[4], ",")

					for i, v in ipairs(subs) do
						local opt = string.gsub(v, " ", "")
						if opt == "true" then
							menu.options[tt[1]][tt[2]][tt[3]][1][i][2] = true
						else
							menu.options[tt[1]][tt[2]][tt[3]][1][i][2] = false
						end
						if i == #subs - 1 then
							break
						end
					end
				end
			end

			local start = nil
			for i, v in next, lines do
				if v == "keybinds {" then
					start = i
					break
				end
			end
			local end_ = nil
			for i, v in next, lines do
				if i > start and v == "}" then
					end_ = i
					break
				end
			end
			for i = 1, end_ - start - 1 do
				local tt = string.split(lines[i + start], "|")
				if menu.options[tt[1]] ~= nil and menu.options[tt[1]][tt[2]] ~= nil and menu.options[tt[1]][tt[2]][tt[3]] ~= nil and menu.options[tt[1]][tt[2]][tt[3]][5] ~= nil
				then
					if tt[5] ~= nil then
						local toggletype = clamp(tonumber(tt[5]), 1, 4)
						if menu.options[tt[1]][tt[2]][tt[3]][5].toggletype ~= 0 then
							menu.options[tt[1]][tt[2]][tt[3]][5].toggletype = toggletype
						end
					end

					if tt[4] == "nil" then
						menu.options[tt[1]][tt[2]][tt[3]][5][1] = nil
					else
						menu.options[tt[1]][tt[2]][tt[3]][5][1] = keyz[tonumber(tt[4])]
					end
				end
			end

			local start = nil
			for i, v in next, lines do
				if v == "colorpickers {" then
					start = i
					break
				end
			end
			local end_ = nil
			for i, v in next, lines do
				if i > start and v == "}" then
					end_ = i
					break
				end
			end
			for i = 1, end_ - start - 1 do
				local tt = string.split(lines[i + start], "|")
				if menu.options[tt[1]] ~= nil and menu.options[tt[1]][tt[2]] ~= nil and menu.options[tt[1]][tt[2]][tt[3]] ~= nil
				then
					local subs = string.split(tt[4], ",")

					for i, v in ipairs(subs) do
						if menu.options[tt[1]][tt[2]][tt[3]][5][1][i] == nil then
							break
						end
						local opt = string.gsub(v, " ", "")
						menu.options[tt[1]][tt[2]][tt[3]][5][1][i] = tonumber(opt)
						if i == #subs - 1 then
							break
						end
					end
				end
			end

			local start = nil
			for i, v in next, lines do
				if v == "double colorpickers {" then
					start = i
					break
				end
			end
			local end_ = nil
			for i, v in next, lines do
				if i > start and v == "}" then
					end_ = i
					break
				end
			end
			for i = 1, end_ - start - 1 do
				local tt = string.split(lines[i + start], "|")
				if menu.options[tt[1]] ~= nil and menu.options[tt[1]][tt[2]] ~= nil and menu.options[tt[1]][tt[2]][tt[3]] ~= nil
				then
					local subs = { string.split(tt[4], ","), string.split(tt[5], ",") }

					for i, v in ipairs(subs) do
						for i1, v1 in ipairs(v) do
							if menu.options[tt[1]][tt[2]][tt[3]][5][1][i][1][i1] == nil then
								break
							end
							local opt = string.gsub(v1, " ", "")
							menu.options[tt[1]][tt[2]][tt[3]][5][1][i][1][i1] = tonumber(opt)
							if i1 == #v - 1 then
								break
							end
						end
					end
				end
			end

			for k, v in pairs(menu.options) do
				for k1, v1 in pairs(v) do
					for k2, v2 in pairs(v1) do
						if v2[2] == "toggle" then
							if not v2[1] then
								for i = 0, 3 do
									v2[4][i + 1].Color = ColorRange(i, {
										[1] = { start = 0, color = RGB(50, 50, 50) },
										[2] = { start = 3, color = RGB(30, 30, 30) },
									})
								end
							else
								for i = 0, 3 do
									v2[4][i + 1].Color = ColorRange(i, {
										[1] = { start = 0, color = RGB(menu.mc[1], menu.mc[2], menu.mc[3]) },
										[2] = {
											start = 3,
											color = RGB(menu.mc[1] - 40, menu.mc[2] - 40, menu.mc[3] - 40),
										},
									})
								end
							end
							if v2[5] ~= nil then
								if v2[5][2] == "keybind" then
									v2[5][4][2].Color = RGB(30, 30, 30)
									v2[5][4][1].Text = KeyEnumToName(v2[5][1])
								elseif v2[5][2] == "single colorpicker" then
									v2[5][4][1].Color = RGB(v2[5][1][1], v2[5][1][2], v2[5][1][3])
									for i = 2, 3 do
										v2[5][4][i].Color = RGB(v2[5][1][1] - 40, v2[5][1][2] - 40, v2[5][1][3] - 40)
									end
								elseif v2[5][2] == "double colorpicker" then
									for i, v3 in ipairs(v2[5][1]) do
										v3[4][1].Color = RGB(v3[1][1], v3[1][2], v3[1][3])
										for i1 = 2, 3 do
											v3[4][i1].Color = RGB(v3[1][1] - 40, v3[1][2] - 40, v3[1][3] - 40)
										end
									end
								end
							end
						elseif v2[2] == "slider" then
							if v2[1] < v2[6][1] then
								v2[1] = v2[6][1]
							elseif v2[1] > v2[6][2] then
								v2[1] = v2[6][2]
							end

							local decplaces = v2.decimal and string.rep("0", math.log(1 / v2.decimal) / math.log(10))
							if decplaces and math.abs(v2[1]) < v2.decimal then
								v2[1] = 0
							end
							v2[4][5].Text = v2.custom[v2[1]] or (v2[1] == math.floor(v2[1]) and v2.decimal) and tostring(v2[1]) .. "." .. decplaces .. v2[4][6] or tostring(v2[1]) .. v2[4][6]
							-- v2[4][5].Text = tostring(v2[1]).. v2[4][6]

							for i = 1, 4 do
								v2[4][i].Size = Vector2.new((v2[3][3] - 4) * ((v2[1] - v2[6][1]) / (v2[6][2] - v2[6][1])), 2)
							end
						elseif v2[2] == "dropbox" then
							if v2[6][v2[1]] == nil then
								v2[1] = 1
							end
							v2[4][1].Text = v2[6][v2[1]]
						elseif v2[2] == "combobox" then
							local textthing = ""
							for k3, v3 in pairs(v2[1]) do
								if v3[2] then
									if textthing == "" then
										textthing = v3[1]
									else
										textthing = textthing .. ", " .. v3[1]
									end
								end
							end
							textthing = textthing ~= "" and textthing or "None"
							if string.len(textthing) > 25 then
								textthing = string_cut(textthing, 25)
							end
							v2[4][1].Text = textthing
						elseif v2[2] == "textbox" then
							v2[4].Text = v2[1]
						end
					end
				end
			end
		end
	end

	function menu.saveconfig()
		local figgy = SaveCurSettings()
		writefile(
			"bitchbot/"
				.. menu.game
				.. "/"
				.. menu.options["Settings"]["Configuration"]["ConfigName"][1]
				.. ".bb",
			figgy
		)
		CreateNotification('Saved "' .. menu.options["Settings"]["Configuration"]["ConfigName"][1] .. '.bb"!')
		UpdateConfigs()
	end
	
	function menu.loadconfig()
		local configname = "bitchbot/"
			.. menu.game
			.. "/"
			.. menu.options["Settings"]["Configuration"]["ConfigName"][1]
			.. ".bb"
		if not isfile(configname) then
			CreateNotification(
				'"'
					.. menu.options["Settings"]["Configuration"]["ConfigName"][1]
					.. '.bb" is not a valid config.'
			)
			return
		end
	
		local curcfg = SaveCurSettings()
		local loadedcfg = readfile(configname)
	
		if pcall(LoadConfig, loadedcfg) then
			CreateNotification('Loaded "' .. menu.options["Settings"]["Configuration"]["ConfigName"][1] .. '.bb"!')
		else
			LoadConfig(curcfg)
			CreateNotification(
				'There was an issue loading "'
					.. menu.options["Settings"]["Configuration"]["ConfigName"][1]
					.. '.bb"'
			)
		end
	end

	local function buttonpressed(bp)
		if bp.doubleclick then
			if buttonsInQue[bp] and tick() - buttonsInQue[bp] < doubleclickDelay then
				buttonsInQue[bp] = 0
			else
				for button, time in next, buttonsInQue do
					buttonsInQue[button] = 0
				end
				buttonsInQue[bp] = tick()
				return
			end
		end
		FireEvent("bb_buttonpressed", bp.tab, bp.groupbox, bp.name)
		--ButtonPressed:Fire(bp.tab, bp.groupbox, bp.name)
		if bp == menu.options["Settings"]["Cheat Settings"]["Unload Cheat"] then
			menu.fading = true
			wait()
			menu:unload()
		elseif bp == menu.options["Settings"]["Cheat Settings"]["Set Clipboard Game ID"] then
			setclipboard(game.JobId)
		elseif bp == menu.options["Settings"]["Configuration"]["Save Config"] then
			menu.saveconfig()
		elseif bp == menu.options["Settings"]["Configuration"]["Delete Config"] then
			delfile(
				"bitchbot/"
					.. menu.game
					.. "/"
					.. menu.options["Settings"]["Configuration"]["ConfigName"][1]
					.. ".bb"
			)
			CreateNotification('Deleted "' .. menu.options["Settings"]["Configuration"]["ConfigName"][1] .. '.bb"!')
			UpdateConfigs()
		elseif bp == menu.options["Settings"]["Configuration"]["Load Config"] then
			menu.loadconfig()
		elseif bp == menu.options["Visuals"]["Highlight Chams"]["Print Values"] then
			local hl = menu:GetVal("Visuals", "Highlight Chams", "Enable")
			local hlcf = Color3.fromRGB(unpack(menu:GetVal("Visuals", "Highlight Chams", "Enable", "color1")))
			local hlco = Color3.fromRGB(unpack(menu:GetVal("Visuals", "Highlight Chams", "Enable", "color2")))
			local hltype = menu:GetVal("Visuals", "Highlight Chams", "Highlight Type")
			print(hl)
			print(hltype - 1)
			print(menu.options["Visuals"]["Highlight Chams"]["Enable"][5][1][1][6])
			print(hlcf)
			print(menu.options["Visuals"]["Highlight Chams"]["Enable"][5][1][2][6])
			print(hlco)
		end
	end

	local function mousebutton2downfunc()
		if menu.colorpicker_open or menu.dropbox_open then
			return
		end

		for k, v in pairs(menu.options) do
			if menu.tabnames[menu.activetab] == k then
				for k1, v1 in pairs(v) do
					local pass = true
					for k3, v3 in pairs(menu.multigroups) do
						if k == k3 then
							for k4, v4 in pairs(v3) do
								for k5, v5 in pairs(v4.vals) do
									if k1 == k5 then
										pass = v5
									end
								end
							end
						end
					end

					if pass then
						for k2, v2 in pairs(v1) do --ANCHOR more menu bs
							if v2[2] == "toggle" then
								if v2[5] ~= nil then
									if v2[5][2] == "keybind" then
										if menu:MouseInMenu(v2[5][3][1], v2[5][3][2], 44, 16) then
											if menu.keybind_open ~= v2 and v2[5].toggletype ~= 0 then
												menu.keybind_open = v2
												set_modeselect(
													true,
													v2[5][3][1] + menu.x,
													v2[5][3][2] + 16 + menu.y,
													v2[5].toggletype
												)
											else
												menu.keybind_open = nil
												set_modeselect(false, 20, 20, 1)
											end
										end
									end
								end
							end
						end
					end
				end
			end
		end
	end

	local function mousebutton1downfunc() --ANCHOR menu mouse down func
		menu.dropbox_open = nil
		menu.textboxopen = false

		set_modeselect(false, 20, 20, 1)
		if menu.keybind_open then
			local key = menu.keybind_open
			local foundkey = false
			for i = 1, 4 do
				if menu:MouseInMenu(key[5][3][1], key[5][3][2] + 16 + ((i - 1) * 21), 70, 21) then
					foundkey = true
					menu.keybind_open[5].toggletype = i
					menu.keybind_open[5].relvalue = false
				end
			end
			menu.keybind_open = nil
			if foundkey then
				return
			end
		end

		for k, v in pairs(menu.options) do
			for k1, v1 in pairs(v) do
				for k2, v2 in pairs(v1) do
					if v2[2] == "dropbox" and v2[5] then
						if not menu:MouseInMenu(v2[3][1], v2[3][2], v2[3][3], 24 * (#v2[6] + 1) + 3) then
							set_dropboxthingy(false, 400, 200, 160, 1, { "HI q", "HI q", "HI q" })
							v2[5] = false
						else
							menu.dropbox_open = v2
						end
					end
					if v2[2] == "combobox" and v2[5] then
						if not menu:MouseInMenu(v2[3][1], v2[3][2], v2[3][3], 24 * (#v2[1] + 1) + 3) then
							set_dropboxthingy(false, 400, 200, 160, 1, { "HI q", "HI q", "HI q" })
							v2[5] = false
						else
							menu.dropbox_open = v2
						end
					end
					if v2[2] == "toggle" then
						if v2[5] ~= nil then
							if v2[5][2] == "keybind" then
								if v2[5][5] == true then
									v2[5][4][2].Color = RGB(30, 30, 30)
									v2[5][5] = false
								end
							elseif v2[5][2] == "single colorpicker" then
								if v2[5][5] == true then
									if not menu:MouseInColorPicker(0, 0, cp.w, cp.h) then
										set_colorpicker(false, { 255, 0, 0 }, nil, false, "hahaha", 400, 200)
										v2[5][5] = false
										menu.colorpicker_open = nil
										menu.colorpicker_open = nil
									end
								end
							elseif v2[5][2] == "double colorpicker" then
								for k3, v3 in pairs(v2[5][1]) do
									if v3[5] == true then
										if not menu:MouseInColorPicker(0, 0, cp.w, cp.h) then
											set_colorpicker(false, { 255, 0, 0 }, nil, false, "hahaha", 400, 200)
											v3[5] = false
											menu.colorpicker_open = nil
											menu.colorpicker_open = nil
										end
									end
								end
							end
						end
					end
					if v2[2] == "textbox" and v2[5] then
						v2[4].Color = RGB(255, 255, 255)
						v2[5] = false
						v2[4].Text = v2[1]
					end
				end
			end
		end
		for i = 1, #menutable do
			if menu:MouseInMenu(
					10 + ((i - 1) * math.floor((menu.w - 20) / #menutable)),
					27,
					math.floor((menu.w - 20) / #menutable),
					32
				)
			then
				menu.activetab = i
				setActiveTab(menu.activetab)
				menu:SetMenuPos(menu.x, menu.y)
				set_tooltip(nil, nil, nil, false)
			end
		end
		if menu.colorpicker_open then
			if menu:MouseInColorPicker(197, cp.h - 25, 75, 20) then
				local tempclr = Color3.fromHSV(cp.hsv.h, cp.hsv.s, cp.hsv.v)
				menu.colorpicker_open[4][1].Color = tempclr
				for i = 2, 3 do
					menu.colorpicker_open[4][i].Color = RGB(
						math.floor(tempclr.R * 255) - 40,
						math.floor(tempclr.G * 255) - 40,
						math.floor(tempclr.B * 255) - 40
					)
				end
				if cp.alpha then
					menu.colorpicker_open[1] = {
						math.floor(tempclr.R * 255),
						math.floor(tempclr.G * 255),
						math.floor(tempclr.B * 255),
						cp.hsv.a,
					}
				else
					menu.colorpicker_open[1] = {
						math.floor(tempclr.R * 255),
						math.floor(tempclr.G * 255),
						math.floor(tempclr.B * 255),
					}
				end
				menu.colorpicker_open = nil
				menu.colorpicker_open = nil
				set_colorpicker(false, { 255, 0, 0 }, nil, false, "hahaha", 400, 200)
			end
			if menu:MouseInColorPicker(264, 2, 14, 14) then
				menu.colorpicker_open = nil
				menu.colorpicker_open = nil
				set_colorpicker(false, { 255, 0, 0 }, nil, false, "hahaha", 400, 200)
			end
			if menu:MouseInColorPicker(10, 23, 160, 160) then
				cp.dragging_m = true
			elseif menu:MouseInColorPicker(176, 23, 14, 160) then
				cp.dragging_r = true
			elseif menu:MouseInColorPicker(10, 189, 160, 14) and cp.alpha then
				cp.dragging_b = true
			end

			if menu:MouseInColorPicker(197, 37, 75, 20) then
				menu.copied_clr = newcolor.Color
			elseif menu:MouseInColorPicker(197, 57, 75, 20) then
				if menu.copied_clr ~= nil then
					local cpa = false
					local clrtable = { menu.copied_clr.R * 255, menu.copied_clr.G * 255, menu.copied_clr.B * 255 }
					if menu.colorpicker_open[1][4] ~= nil then
						cpa = true
						table.insert(clrtable, menu.colorpicker_open[1][4])
					end

					set_colorpicker(true, clrtable, menu.colorpicker_open, cpa, menu.colorpicker_open[6], cp.x, cp.y)
					local oldclr = menu.colorpicker_open[4][1].Color
					if menu.colorpicker_open[1][4] ~= nil then
						set_oldcolor(oldclr.R * 255, oldclr.G * 255, oldclr.B * 255, menu.colorpicker_open[1][4])
					else
						set_oldcolor(oldclr.R * 255, oldclr.G * 255, oldclr.B * 255)
					end
				end
			end

			if menu:MouseInColorPicker(197, 91, 75, 40) then
				menu.copied_clr = oldcolor.Color
			end
		else
			for k, v in pairs(menu.multigroups) do
				if menu.tabnames[menu.activetab] == k then
					for k1, v1 in pairs(v) do
						local c_pos = v1.drawn.click_pos
						--local selected = v1.drawn.bar
						local selected_pos = v1.drawn.barpos

						for k2, v2 in pairs(v1.drawn.click_pos) do
							if menu:MouseInMenu(v2.x, v2.y, v2.width, v2.height) then
								for _k, _v in pairs(v1.vals) do
									if _k == v2.name then
										v1.vals[_k] = true
									else
										v1.vals[_k] = false
									end
								end

								local settab = v2.num
								for _k, _v in pairs(v1.drawn.bar) do
									menu.postable[_v.postable][2] = selected_pos[settab].pos
									_v.drawn.Size = Vector2.new(selected_pos[settab].length, 2)
								end

								for i, v in pairs(v1.drawn.nametext) do
									if i == v2.num then
										v.Color = RGB(255, 255, 255)
									else
										v.Color = RGB(170, 170, 170)
									end
								end

								menu:set_menu_visibility(true)
								setActiveTab(menu.activetab)
								menu:SetMenuPos(menu.x, menu.y)
							end
						end
					end
				end
			end
			local newdropbox_open
			for k, v in pairs(menu.options) do
				if menu.tabnames[menu.activetab] == k then
					for k1, v1 in pairs(v) do
						local pass = true
						for k3, v3 in pairs(menu.multigroups) do
							if k == k3 then
								for k4, v4 in pairs(v3) do
									for k5, v5 in pairs(v4.vals) do
										if k1 == k5 then
											pass = v5
										end
									end
								end
							end
						end

						if pass then
							for k2, v2 in pairs(v1) do
								if v2[2] == "toggle" and not menu.dropbox_open then
									if menu:MouseInMenu(v2[3][1], v2[3][2], 30 + v2[4][5].TextBounds.x, 16) then
										if v2[6] then
											if menu:GetVal(
													"Settings",
													"Cheat Settings",
													"Allow Unsafe Features"
												) and v2[1] == false
											then
												v2[1] = true
											else
												v2[1] = false
											end
										else
											v2[1] = not v2[1]
										end
										if not v2[1] then
											for i = 0, 3 do
												v2[4][i + 1].Color = ColorRange(i, {
													[1] = { start = 0, color = RGB(50, 50, 50) },
													[2] = { start = 3, color = RGB(30, 30, 30) },
												})
											end
										else
											for i = 0, 3 do
												v2[4][i + 1].Color = ColorRange(i, {
													[1] = {
														start = 0,
														color = RGB(menu.mc[1], menu.mc[2], menu.mc[3]),
													},
													[2] = {
														start = 3,
														color = RGB(
															menu.mc[1] - 40,
															menu.mc[2] - 40,
															menu.mc[3] - 40
														),
													},
												})
											end
										end
										--TogglePressed:Fire(k1, k2, v2)
										FireEvent("bb_togglepressed", k1, k2, v2)
									end
									if v2[5] ~= nil then
										if v2[5][2] == "keybind" then
											if menu:MouseInMenu(v2[5][3][1], v2[5][3][2], 44, 16) then
												v2[5][4][2].Color = RGB(menu.mc[1], menu.mc[2], menu.mc[3])
												v2[5][5] = true
											end
										elseif v2[5][2] == "single colorpicker" then
											if menu:MouseInMenu(v2[5][3][1], v2[5][3][2], 28, 14) then
												v2[5][5] = true
												menu.colorpicker_open = v2[5]
												menu.colorpicker_open = v2[5]
												if v2[5][1][4] ~= nil then
													set_colorpicker(
														true,
														v2[5][1],
														v2[5],
														true,
														v2[5][6],
														LOCAL_MOUSE.x,
														LOCAL_MOUSE.y + 36
													)
												else
													set_colorpicker(
														true,
														v2[5][1],
														v2[5],
														false,
														v2[5][6],
														LOCAL_MOUSE.x,
														LOCAL_MOUSE.y + 36
													)
												end
											end
										elseif v2[5][2] == "double colorpicker" then
											for k3, v3 in pairs(v2[5][1]) do
												if menu:MouseInMenu(v3[3][1], v3[3][2], 28, 14) then
													v3[5] = true
													menu.colorpicker_open = v3
													menu.colorpicker_open = v3
													if v3[1][4] ~= nil then
														set_colorpicker(
															true,
															v3[1],
															v3,
															true,
															v3[6],
															LOCAL_MOUSE.x,
															LOCAL_MOUSE.y + 36
														)
													else
														set_colorpicker(
															true,
															v3[1],
															v3,
															false,
															v3[6],
															LOCAL_MOUSE.x,
															LOCAL_MOUSE.y + 36
														)
													end
												end
											end
										end
									end
								elseif v2[2] == "slider" and not menu.dropbox_open then
									if menu:MouseInMenu(v2[7][1], v2[7][2], 22, 13) then
										local stepval = 1
										if v2.stepsize then
											stepval = v2.stepsize
										end
										if menu:modkeydown("shift", "left") then
											stepval = 0.1
										end
										if menu:MouseInMenu(v2[7][1], v2[7][2], 11, 13) then
											v2[1] -= stepval
										elseif menu:MouseInMenu(v2[7][1] + 11, v2[7][2], 11, 13) then
											v2[1] += stepval
										end

										if v2[1] < v2[6][1] then
											v2[1] = v2[6][1]
										elseif v2[1] > v2[6][2] then
											v2[1] = v2[6][2]
										end
										local decplaces = v2.decimal and string.rep("0", math.log(1 / v2.decimal) / math.log(10))
										if decplaces and math.abs(v2[1]) < v2.decimal then
											v2[1] = 0
										end
										v2[4][5].Text = v2.custom[v2[1]] or (v2[1] == math.floor(v2[1]) and v2.decimal) and tostring(v2[1]) .. "." .. decplaces .. v2[4][6] or tostring(v2[1]) .. v2[4][6]

										for i = 1, 4 do
											v2[4][i].Size = Vector2.new(
												(v2[3][3] - 4) * ((v2[1] - v2[6][1]) / (v2[6][2] - v2[6][1])),
												2
											)
										end
									elseif menu:MouseInMenu(v2[3][1], v2[3][2], v2[3][3], 28) then
										v2[5] = true
									end
								elseif v2[2] == "dropbox" then
									if menu.dropbox_open then
										if v2 ~= menu.dropbox_open then
											continue
										end
									end
									if menu:MouseInMenu(v2[3][1], v2[3][2], v2[3][3], 36) then
										if not v2[5] then
											set_dropboxthingy(
												true,
												v2[3][1] + menu.x + 1,
												v2[3][2] + menu.y + 13,
												v2[3][3],
												v2[1],
												v2[6]
											)
											v2[5] = true
											newdropbox_open = v2
										else
											set_dropboxthingy(false, 400, 200, 160, 1, { "HI q", "HI q", "HI q" })
											v2[5] = false
											newdropbox_open = nil
										end
									elseif menu:MouseInMenu(v2[3][1], v2[3][2], v2[3][3], 24 * (#v2[6] + 1) + 3) and v2[5]
									then
										for i = 1, #v2[6] do
											if menu:MouseInMenu(
													v2[3][1],
													v2[3][2] + 36 + ((i - 1) * 21),
													v2[3][3],
													21
												)
											then
												v2[4][1].Text = v2[6][i]
												v2[1] = i
												set_dropboxthingy(false, 400, 200, 160, 1, { "HI q", "HI q", "HI q" })
												v2[5] = false
												newdropbox_open = nil
											end
										end

										if v2 == menu.options["Settings"]["Configuration"]["Configs"] then
											local textbox = menu.options["Settings"]["Configuration"]["ConfigName"]
											local relconfigs = GetConfigs()
											textbox[1] = relconfigs[menu.options["Settings"]["Configuration"]["Configs"][1]]
											textbox[4].Text = textbox[1]
										end
									end
								elseif v2[2] == "combobox" then
									if menu.dropbox_open then
										if v2 ~= menu.dropbox_open then
											continue
										end
									end
									if menu:MouseInMenu(v2[3][1], v2[3][2], v2[3][3], 36) then
										if not v2[5] then
											set_comboboxthingy(
												true,
												v2[3][1] + menu.x + 1,
												v2[3][2] + menu.y + 13,
												v2[3][3],
												v2[1],
												v2[6]
											)
											v2[5] = true
											newdropbox_open = v2
										else
											set_dropboxthingy(false, 400, 200, 160, 1, { "HI q", "HI q", "HI q" })
											v2[5] = false
											newdropbox_open = nil
										end
									elseif menu:MouseInMenu(v2[3][1], v2[3][2], v2[3][3], 24 * (#v2[1] + 1) + 3) and v2[5]
									then
										for i = 1, #v2[1] do
											if menu:MouseInMenu(
													v2[3][1],
													v2[3][2] + 36 + ((i - 1) * 22),
													v2[3][3],
													23
												)
											then
												v2[1][i][2] = not v2[1][i][2]
												local textthing = ""
												for k, v in pairs(v2[1]) do
													if v[2] then
														if textthing == "" then
															textthing = v[1]
														else
															textthing = textthing .. ", " .. v[1]
														end
													end
												end
												textthing = textthing ~= "" and textthing or "None"
												if string.len(textthing) > 25 then
													textthing = string_cut(textthing, 25)
												end
												v2[4][1].Text = textthing
												set_comboboxthingy(
													true,
													v2[3][1] + menu.x + 1,
													v2[3][2] + menu.y + 13,
													v2[3][3],
													v2[1],
													v2[6]
												)
											end
										end
									end
								elseif v2[2] == "button" and not menu.dropbox_open then
									if menu:MouseInMenu(v2[3][1], v2[3][2], v2[3][3], 22) then
										if not v2[1] then
											buttonpressed(v2)
											if k2 == "Unload Cheat" then
												return
											end
											for i = 0, 8 do
												v2[4][i + 1].Color = ColorRange(i, {
													[1] = { start = 0, color = RGB(35, 35, 35) },
													[2] = { start = 8, color = RGB(50, 50, 50) },
												})
											end
											v2[1] = true
										end
									end
								elseif v2[2] == "textbox" and not menu.dropbox_open then
									if menu:MouseInMenu(v2[3][1], v2[3][2], v2[3][3], 22) then
										if not v2[5] then
											menu.textboxopen = v2

											v2[4].Color = RGB(menu.mc[1], menu.mc[2], menu.mc[3])
											v2[5] = true
										end
									end
								elseif v2[2] == "list" then
									--[[
									menu.options[v.name][v1.name][v2.name] = {}
									menu.options[v.name][v1.name][v2.name][4] = Draw:List(v2.name, v1.x + 8, v1.y + y_pos, v1.width - 16, v2.size, v2.columns, tabz[k])
									menu.options[v.name][v1.name][v2.name][1] = nil
									menu.options[v.name][v1.name][v2.name][2] = v2.type
									menu.options[v.name][v1.name][v2.name][3] = 1
									menu.options[v.name][v1.name][v2.name][5] = {}
									menu.options[v.name][v1.name][v2.name][6] = v2.size
									menu.options[v.name][v1.name][v2.name][7] = v2.columns
									menu.options[v.name][v1.name][v2.name][8] = {v1.x + 8, v1.y + y_pos, v1.width - 16}
									]]
									--
									if #v2[5] > v2[6] then
										for i = 1, v2[6] do
											if menu:MouseInMenu(v2[8][1], v2[8][2] + (i * 22) - 5, v2[8][3], 22)
											then
												if v2[1] == tostring(v2[5][i + v2[3] - 1][1][1]) then
													v2[1] = nil
												else
													v2[1] = tostring(v2[5][i + v2[3] - 1][1][1])
												end
											end
										end
									else
										for i = 1, #v2[5] do
											if menu:MouseInMenu(v2[8][1], v2[8][2] + (i * 22) - 5, v2[8][3], 22)
											then
												if v2[1] == tostring(v2[5][i + v2[3] - 1][1][1]) then
													v2[1] = nil
												else
													v2[1] = tostring(v2[5][i + v2[3] - 1][1][1])
												end
											end
										end
									end
								end
							end
						end
					end
				end
			end
			menu.dropbox_open = newdropbox_open
		end
		for k, v in pairs(menu.options) do
			for k1, v1 in pairs(v) do
				for k2, v2 in pairs(v1) do
					if v2[2] == "toggle" then
						if v2[6] then
							if not menu:GetVal("Settings", "Cheat Settings", "Allow Unsafe Features") then
								v2[1] = false
								for i = 0, 3 do
									v2[4][i + 1].Color = ColorRange(i, {
										[1] = { start = 0, color = RGB(50, 50, 50) },
										[2] = { start = 3, color = RGB(30, 30, 30) },
									})
								end
							end
						end
					end
				end
			end
		end
		if menu.open then
			if menu.options["Settings"]["Cheat Settings"]["Menu Accent"][1] then
				local clr = menu.options["Settings"]["Cheat Settings"]["Menu Accent"][5][1]
				menu.mc = { clr[1], clr[2], clr[3] }
			else
				menu.mc = { 127, 72, 163 }
			end
			menu:set_menu_clr(menu.mc[1], menu.mc[2], menu.mc[3])

			local wme = menu:GetVal("Settings", "Cheat Settings", "Watermark")
			for k, v in pairs(menu.watermark.rect) do
				v.Visible = wme
			end
			menu.watermark.text[1].Visible = wme
		end
	end

	local function mousebutton1upfunc()
		cp.dragging_m = false
		cp.dragging_r = false
		cp.dragging_b = false
		for k, v in pairs(menu.options) do
			if menu.tabnames[menu.activetab] == k then
				for k1, v1 in pairs(v) do
					for k2, v2 in pairs(v1) do
						if v2[2] == "slider" and v2[5] then
							v2[5] = false
						end
						if v2[2] == "button" and v2[1] then
							for i = 0, 8 do
								v2[4][i + 1].Color = ColorRange(i, {
									[1] = { start = 0, color = RGB(50, 50, 50) },
									[2] = { start = 8, color = RGB(35, 35, 35) },
								})
							end
							v2[1] = false
						end
					end
				end
			end
		end
	end

	local clickspot_x, clickspot_y, original_menu_x, original_menu_y = 0, 0, 0, 0

	menu.connections.mwf = LOCAL_MOUSE.WheelForward:Connect(function()
		if menu.open then
			for k, v in pairs(menu.options) do
				if menu.tabnames[menu.activetab] == k then
					for k1, v1 in pairs(v) do
						for k2, v2 in pairs(v1) do
							if v2[2] == "list" then
								if v2[3] > 1 then
									v2[3] -= 1
								end
							end
						end
					end
				end
			end
		end
	end)

	menu.connections.mwb = LOCAL_MOUSE.WheelBackward:Connect(function()
		if menu.open then
			for k, v in pairs(menu.options) do
				if menu.tabnames[menu.activetab] == k then
					for k1, v1 in pairs(v) do
						for k2, v2 in pairs(v1) do
							if v2[2] == "list" then
								if v2[5][v2[3] + v2[6]] ~= nil then
									v2[3] += 1
								end
							end
						end
					end
				end
			end
		end
	end)

	function menu:set_menu_alphaparency(transparency)
		for k, v in pairs(bbmouse) do
			v.Transparency = transparency / 255
		end
		for k, v in pairs(bbmenu) do
			v.Transparency = transparency / 255
		end
		for k, v in pairs(tabz[menu.activetab]) do
			v.Transparency = transparency / 255
		end
	end

	function menu:set_menu_visibility(visible)
		for k, v in pairs(bbmouse) do
			v.Visible = visible
		end
		for k, v in pairs(bbmenu) do
			v.Visible = visible
		end
		for k, v in pairs(tabz[menu.activetab]) do
			v.Visible = visible
		end

		if visible then
			for k, v in pairs(menu.multigroups) do
				if menu.tabnames[menu.activetab] == k then
					for k1, v1 in pairs(v) do
						for k2, v2 in pairs(v1.vals) do
							for k3, v3 in pairs(menu.mgrouptabz[k][k2]) do
								v3.Visible = v2
							end
						end
					end
				end
			end
		end
	end

	menu:set_menu_alphaparency(0)
	menu:set_menu_visibility(false)
	menu.lastActive = true
	menu.open = false
	menu.windowactive = true
	menu.connections.mousemoved = MouseMoved:connect(function(b)
		menu.windowactive = iswindowactive() or b
	end)

	local function renderSteppedMenu(fdt)
		menu.dt = fdt
		if menu.unloaded then
			return
		end
		SCREEN_SIZE = Camera.ViewportSize
		-- i pasted the old menu working ingame shit from the old source nate pls fix ty
		-- this is the really shitty alive check that we've been using since day one
		-- removed it :DDD
		-- im keepin all of our comments they're fun to look at
		-- i wish it showed comment dates that would be cool
		-- nah that would suck fk u (comment made on 3/4/2021 3:35 pm est by bitch)

		if menu.lastActive ~= menu.windowactive then
			setfpscap(menu.windowactive and (maxfps or 144) or 15)
		end

		menu.lastActive = menu.windowactive
		for button, time in next, buttonsInQue do
			if time and tick() - time < doubleclickDelay then
				button[4].text.Color = RGB(menu.mc[1], menu.mc[2], menu.mc[3])
				button[4].text.Text = "Confirm?"
			else
				button[4].text.Color = Color3.new(1, 1, 1)
				button[4].text.Text = button.name
			end
		end
        INPUT_SERVICE.MouseBehavior = menu.open and Enum.MouseBehavior.Default or Enum.MouseBehavior.LockCenter
        --[[ if menu.open then
			if client.char.alive then
				INPUT_SERVICE.MouseBehavior = Enum.MouseBehavior.Default
			else
				INPUT_SERVICE.MouseIconEnabled = false
			end
		else
			if client.char.alive then
				INPUT_SERVICE.MouseBehavior = Enum.MouseBehavior.LockCenter
				INPUT_SERVICE.MouseIconEnabled = false
			else
				INPUT_SERVICE.MouseBehavior = Enum.MouseBehavior.Default
				INPUT_SERVICE.MouseIconEnabled = true
			end
		end ]]
		if menu.open then
			if menu.backspaceheld then
				local dt = tick() - menu.backspacetime
				if dt > 0.4 then
					menu.backspaceflags += 1
					if menu.backspaceflags % 5 == 0 then
						local textbox = menu.textboxopen
						textbox[1] = string.sub(textbox[1], 0, #textbox[1] - 1)
						textbox[4].Text = textbox[1] .. "|"
					end
				end
			end
		end
		if menu.fading then
			if menu.open then
				local timesincefade = tick() - menu.fadestart
				local fade_amount = 255 - math.floor((timesincefade * 10) * 255)
				set_plusminus(0, 20, 20)
				menu:set_menu_alphaparency(fade_amount)
				if fade_amount <= 0 then
					menu.open = false
					menu.fading = false
					menu:set_menu_alphaparency(0)
					menu:set_menu_visibility(false)
				else
					menu:set_menu_alphaparency(fade_amount)
				end
			else
				menu:set_menu_visibility(true)
				setActiveTab(menu.activetab)
				local timesincefade = tick() - menu.fadestart
				local fade_amount = math.floor((timesincefade * 10) * 255)
				menu.fadeamount = fade_amount
				menu:set_menu_alphaparency(fade_amount)
				if fade_amount >= 255 then
					menu.open = true
					menu.fading = false
					menu:set_menu_alphaparency(255)
				else
					menu:set_menu_alphaparency(fade_amount)
				end
			end
		end
		menu:set_mouse_pos(LOCAL_MOUSE.x, LOCAL_MOUSE.y)
		set_tooltip(nil, nil, nil, false, fdt)
		if menu.open or menu.fading then
			set_plusminus(0, 20, 20)
			for k, v in pairs(menu.options) do
				if menu.tabnames[menu.activetab] == k then
					for k1, v1 in pairs(v) do
						local pass = true
						for k3, v3 in pairs(menu.multigroups) do
							if k == k3 then
								for k4, v4 in pairs(v3) do
									for k5, v5 in pairs(v4.vals) do
										if k1 == k5 then
											pass = v5
										end
									end
								end
							end
						end

						if pass then
							for k2, v2 in pairs(v1) do
								if v2[2] == "toggle" then
									if not menu.dropbox_open and not menu.colorpicker_open then
										if menu.open and menu:MouseInMenu(v2[3][1], v2[3][2], 30 + v2[4][5].TextBounds.x, 16)
										then
											if v2.tooltip then
												set_tooltip(
													menu.x + v2[3][1],
													menu.y + v2[3][2] + 18,
													v2.tooltip,
													true,
													fdt * 2--[[this is really fucking stupid]]
												)
											end
										end
									end
								elseif v2[2] == "slider" then
									if v2[5] then
										local new_val = (v2[6][2] - v2[6][1])  * (
												(
													LOCAL_MOUSE.x
													- menu.x
													- v2[3][1]
												) / v2[3][3]
											)
										v2[1] = (
												not v2.decimal and math.floor(new_val) or math.floor(new_val / v2.decimal) * v2.decimal
											) + v2[6][1]
										if v2[1] < v2[6][1] then
											v2[1] = v2[6][1]
										elseif v2[1] > v2[6][2] then
											v2[1] = v2[6][2]
										end
										local decplaces = v2.decimal and string.rep("0", math.log(1 / v2.decimal) / math.log(10))
										if decplaces and math.abs(v2[1]) < v2.decimal then
											v2[1] = 0
										end

										v2[4][5].Text = v2.custom[v2[1]] or (v2[1] == math.floor(v2[1]) and v2.decimal) and tostring(v2[1]) .. "." .. decplaces .. v2[4][6] or tostring(v2[1]) .. v2[4][6]
										for i = 1, 4 do
											v2[4][i].Size = Vector2.new(
												(v2[3][3] - 4) * ((v2[1] - v2[6][1]) / (v2[6][2] - v2[6][1])),
												2
											)
										end
										set_plusminus(1, v2[7][1], v2[7][2])
									else
										if not menu.dropbox_open then
											if menu:MouseInMenu(v2[3][1], v2[3][2], v2[3][3], 28) then
												if menu:MouseInMenu(v2[7][1], v2[7][2], 22, 13) then
													if menu:MouseInMenu(v2[7][1], v2[7][2], 11, 13) then
														set_plusminus(2, v2[7][1], v2[7][2])
													elseif menu:MouseInMenu(v2[7][1] + 11, v2[7][2], 11, 13) then
														set_plusminus(3, v2[7][1], v2[7][2])
													end
												else
													set_plusminus(1, v2[7][1], v2[7][2])
												end
											end
										end
									end
								elseif v2[2] == "list" then
									for k3, v3 in pairs(v2[4].liststuff) do
										for i, v4 in ipairs(v3) do
											for i1, v5 in ipairs(v4) do
												v5.Visible = false
											end
										end
									end
									for i = 1, v2[6] do
										if v2[5][i + v2[3] - 1] ~= nil then
											for i1 = 1, v2[7] do
												v2[4].liststuff.words[i][i1].Text = v2[5][i + v2[3] - 1][i1][1]
												v2[4].liststuff.words[i][i1].Visible = true

												if v2[5][i + v2[3] - 1][i1][1] == v2[1] and i1 == 1 then
													if menu.options["Settings"]["Cheat Settings"]["Menu Accent"][1]
													then
														local clr = menu.options["Settings"]["Cheat Settings"]["Menu Accent"][5][1]
														v2[4].liststuff.words[i][i1].Color = RGB(clr[1], clr[2], clr[3])
													else
														v2[4].liststuff.words[i][i1].Color = RGB(menu.mc[1], menu.mc[2], menu.mc[3])
													end
												else
													v2[4].liststuff.words[i][i1].Color = v2[5][i + v2[3] - 1][i1][2]
												end
											end
											for k3, v3 in pairs(v2[4].liststuff.rows[i]) do
												v3.Visible = true
											end
										elseif v2[3] > 1 then
											v2[3] -= 1
										end
									end
									if v2[3] == 1 then
										for k3, v3 in pairs(v2[4].uparrow) do
											if v3.Visible then
												v3.Visible = false
											end
										end
									else
										for k3, v3 in pairs(v2[4].uparrow) do
											if not v3.Visible then
												v3.Visible = true
												menu:SetMenuPos(menu.x, menu.y)
											end
										end
									end
									if v2[5][v2[3] + v2[6]] == nil then
										for k3, v3 in pairs(v2[4].downarrow) do
											if v3.Visible then
												v3.Visible = false
											end
										end
									else
										for k3, v3 in pairs(v2[4].downarrow) do
											if not v3.Visible then
												v3.Visible = true
												menu:SetMenuPos(menu.x, menu.y)
											end
										end
									end
								end
							end
						end
					end
				end
			end
			menu.inmenu = LOCAL_MOUSE.x > menu.x and LOCAL_MOUSE.x < menu.x + menu.w and LOCAL_MOUSE.y > menu.y - 32 and LOCAL_MOUSE.y < menu.y + menu.h
			menu.inmiddlemenu = LOCAL_MOUSE.x > menu.x + 9 and LOCAL_MOUSE.x < menu.x + menu.w - 9 and LOCAL_MOUSE.y > menu.y - 9 and LOCAL_MOUSE.y < menu.y + menu.h - 47
			if (
					--[[(
						LOCAL_MOUSE.x > menu.x and LOCAL_MOUSE.x < menu.x + menu.w and LOCAL_MOUSE.y > menu.y - 32 and LOCAL_MOUSE.y < menu.y - 11
					)]]
					(
						menu.inmenu and 
						not menu.inmiddlemenu
					) or menu.dragging
				) and not menu.dontdrag
			then
				if menu.mousedown then
					if not menu.dragging then
						clickspot_x = LOCAL_MOUSE.x
						clickspot_y = LOCAL_MOUSE.y - 36 original_menu_X = menu.x original_menu_y = menu.y
						menu.dragging = true
					end
					menu.x = (original_menu_X - clickspot_x) + LOCAL_MOUSE.x
					menu.y = (original_menu_y - clickspot_y) + LOCAL_MOUSE.y - 36
					if menu.y < 0 then
						menu.y = 0
					end
					if menu.x < -menu.w / 4 * 3 then
						menu.x = -menu.w / 4 * 3
					end
					if menu.x + menu.w / 4 > SCREEN_SIZE.x then
						menu.x = SCREEN_SIZE.x - menu.w / 4
					end
					if menu.y > SCREEN_SIZE.y - 20 then
						menu.y = SCREEN_SIZE.y - 20
					end
					menu:SetMenuPos(menu.x, menu.y)
				else
					menu.dragging = false
				end
			elseif menu.mousedown then
				menu.dontdrag = true
			elseif not menu.mousedown then
				menu.dontdrag = false
			end
			if menu.colorpicker_open then
				if cp.dragging_m then
					set_dragbar_m(
						clamp(LOCAL_MOUSE.x, cp.x + 12, cp.x + 167) - 2,
						clamp(LOCAL_MOUSE.y + 36, cp.y + 25, cp.y + 180) - 2
					)

					cp.hsv.s = (clamp(LOCAL_MOUSE.x, cp.x + 12, cp.x + 167) - cp.x - 12) / 155
					cp.hsv.v = 1 - ((clamp(LOCAL_MOUSE.y + 36, cp.y + 23, cp.y + 178) - cp.y - 23) / 155)
					newcolor.Color = Color3.fromHSV(cp.hsv.h, cp.hsv.s, cp.hsv.v)
				elseif cp.dragging_r then
					set_dragbar_r(cp.x + 175, clamp(LOCAL_MOUSE.y + 36, cp.y + 23, cp.y + 178))

					maincolor.Color = Color3.fromHSV(
							1 - ((clamp(LOCAL_MOUSE.y + 36, cp.y + 23, cp.y + 178) - cp.y - 23) / 155),
							1,
							1
						)

					cp.hsv.h = 1 - ((clamp(LOCAL_MOUSE.y + 36, cp.y + 23, cp.y + 178) - cp.y - 23) / 155)
					newcolor.Color = Color3.fromHSV(cp.hsv.h, cp.hsv.s, cp.hsv.v)
				elseif cp.dragging_b then
					set_dragbar_b(clamp(LOCAL_MOUSE.x, cp.x + 10, cp.x + 168), cp.y + 188)
					newcolor.Transparency = (clamp(LOCAL_MOUSE.x, cp.x + 10, cp.x + 168) - cp.x - 10) / 158
					cp.hsv.a = math.floor(((clamp(LOCAL_MOUSE.x, cp.x + 10, cp.x + 168) - cp.x - 10) / 158) * 255)
				else
					local setvisnew = menu:MouseInColorPicker(197, 37, 75, 40)
					for i, v in ipairs(newcopy) do
						v.Visible = setvisnew
					end

					local setvisold = menu:MouseInColorPicker(197, 91, 75, 40)
					for i, v in ipairs(oldcopy) do
						v.Visible = setvisold
					end
				end
			end
		else
			menu.dragging = false
		end
	end

	menu.connections.inputstart = INPUT_SERVICE.InputBegan:Connect(function(input)
		if menu then
			if input.UserInputType == Enum.UserInputType.MouseButton1 then
				menu.mousedown = true
				if menu.open and not menu.fading then
					mousebutton1downfunc()
				end
			elseif input.UserInputType == Enum.UserInputType.MouseButton2 then
				if menu.open and not menu.fading then
					mousebutton2downfunc()
				end
			end

			if input.UserInputType == Enum.UserInputType.Keyboard then
				if input.KeyCode.Name:match("Shift") then
					local kcn = input.KeyCode.Name
					local direction = kcn:split("Shift")[1]
					menu.modkeys.shift.direction = direction:lower()
				end
				if input.KeyCode.Name:match("Alt") then
					local kcn = input.KeyCode.Name
					local direction = kcn:split("Alt")[1]
					menu.modkeys.alt.direction = direction:lower()
				end
			end
			if not menu then
				return
			end -- this fixed shit with unload
			menu:InputBeganMenu(input)
			menu:InputBeganKeybinds(input)
			if menu.open then
				if menu.tabnames[menu.activetab] == "Settings" then
					bbmenu[27].Text = menu:GetVal("Settings", "Cheat Settings", "Custom Menu Name") and menu:GetVal("Settings", "Cheat Settings", "MenuName") or "Bitch Bot"

					menu.watermark.text[1].Text = menu.options["Settings"]["Cheat Settings"]["MenuName"][1]
						.. menu.watermark.textString

					for i, v in ipairs(menu.watermark.rect) do
						local len = #menu.watermark.text[1].Text * 7 + 10
						if i == #menu.watermark.rect then
							len += 2
						end
						v.Size = Vector2.new(len, v.Size.y)
					end
				end
			end
			if input.KeyCode == Enum.KeyCode.Home then
				menu.stat_menu = not menu.stat_menu

				for k, v in pairs(graphs) do
					if k ~= "other" then
						for k1, v1 in pairs(v) do
							if k1 ~= "pos" then
								for k2, v2 in pairs(v1) do
									v2.Visible = menu.stat_menu
								end
							end
						end
					end
				end

				for k, v in pairs(graphs.other) do
					v.Visible = menu.stat_menu
				end
			end
		end
	end)

	menu.connections.inputended = INPUT_SERVICE.InputEnded:Connect(function(input)
		menu:InputEndedKeybinds(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 then
			menu.mousedown = false
			if menu.open and not menu.fading then
				mousebutton1upfunc()
			end
		end
		if input.UserInputType == Enum.UserInputType.Keyboard then
			if input.KeyCode.Name:match("Shift") then
				menu.modkeys.shift.direction = nil
			end
			if input.KeyCode.Name:match("Alt") then
				menu.modkeys.alt.direction = nil
			end
		end
	end)

	menu.connections.renderstepped = game.RunService.RenderStepped:Connect(renderSteppedMenu) -- fucking asshole 🖕🖕🖕

	function menu:unload()
		getgenv().v2 = nil
		self.unloaded = true

		for k, conn in next, self.connections do
			if not getrawmetatable(conn) then
				conn()
			else
				conn:Disconnect()
			end
			self.connections[k] = nil
		end

		game:service("ContextActionService"):UnbindAction("BB Keycheck")
		--[[ if self.game == "pf" then
			game:service("ContextActionService"):UnbindAction("BB PF check")
		elseif self.game == "uni" then
			game:service("ContextActionService"):UnbindAction("BB UNI check")
		end ]]

		local mt = getrawmetatable(game)

		setreadonly(mt, false)

		local oldmt = menu.oldmt

		if oldmt then
			for k, v in next, mt do
				if oldmt[k] then
					mt[k] = oldmt[k]
				end
			end
		else
			--TODO nate do this please
			-- remember to store any "game" metatable hooks PLEASE PLEASE because this will ensure it replaces the meta so that it UNLOADS properly
			--rconsoleerr("fatal error: no old game meta found! (UNLOAD PROBABLY WON'T WORK AS EXPECTED)")
		end

		setreadonly(mt, true)

		if menu.game == "pf" or menu.pfunload then
			menu:pfunload()
		end

		Draw:UnRender()
		CreateNotification = nil
		allrender = nil
		menu = nil
		Draw = nil
		self.unloaded = true
	end
end

local StatMenuRendered = event.new("StatMenuRendered")
menu.connections.heartbeatmenu = game.RunService.Heartbeat:Connect(function() --ANCHOR MENU HEARTBEAT
	if menu.y < 0 then
		menu.y = 0
		menu:SetMenuPos(menu.x, 0)
	end
	if menu.x < -menu.w / 4 * 3 then
		menu.x = -menu.w / 4 * 3
		menu:SetMenuPos(-menu.w / 4 * 3, menu.y)
	end
	if menu.x + menu.w / 4 > SCREEN_SIZE.x then
		menu.x = SCREEN_SIZE.x - menu.w / 4
		menu:SetMenuPos(SCREEN_SIZE.x - menu.w / 4, menu.y)
	end
	if menu.y > SCREEN_SIZE.y - 20 then
		menu.y = SCREEN_SIZE.y - 20
		menu:SetMenuPos(menu.x, SCREEN_SIZE.y - 20)
	end
	if menu.stat_menu == false then
		return
	end
end)

local function keycheck(actionName, inputState, inputObject)
	if actionName == "BB Keycheck" then
		if menu.open then
			if menu.textboxopen then
				if inputObject.KeyCode == Enum.KeyCode.Backspace then
					if menu.selectall then
						menu.textboxopen[1] = ""
						menu.textboxopen[4].Text = "|"
						menu.textboxopen[4].Color = RGB(unpack(menu.mc))
						menu.selectall = false
					end
					local on = inputState == Enum.UserInputState.Begin
					menu.backspaceheld = on
					menu.backspacetime = on and tick() or -1
					if not on then
						menu.backspaceflags = 0
					end
				end

				if inputObject.KeyCode ~= Enum.KeyCode.A and (not inputObject.KeyCode.Name:match("^Left") and not inputObject.KeyCode.Name:match("^Right")) and inputObject.KeyCode ~= Enum.KeyCode.RightShift
				then
					if menu.selectall then
						menu.textboxopen[4].Color = RGB(unpack(menu.mc))
						menu.selectall = false
					end
				end

				if inputObject.KeyCode == Enum.KeyCode.A then
					if inputState == Enum.UserInputState.Begin and INPUT_SERVICE:IsKeyDown(Enum.KeyCode.LeftControl)
					then
						menu.selectall = true
						local textbox = menu.textboxopen
						textbox[4].Color = RGB(menu.mc[3], menu.mc[2], menu.mc[1])
					end
				end

				return Enum.ContextActionResult.Sink
			end
		end

		return Enum.ContextActionResult.Pass
	end
end

game:service("ContextActionService"):BindAction("BB Keycheck", keycheck, false, Enum.UserInputType.Keyboard)

menu.Initialize({
	{ --ANCHOR stuffs
		name = "Legit",
		content = {
			{
				name = "Aim Assist",
				autopos = "left",
				content = {
					{
						type = "toggle",
						name = "Enabled",
						value = false,
						callback = function(bool)
					print(bool)	    
					end},
					{
						type = "slider",
						name = "Aimbot FOV",
						value = 20,
						minvalue = 0,
						maxvalue = 180,
						stradd = "°",
					},
					{
						type = "slider",
						name = "Smoothing",
						value = 20,
						minvalue = 0,
						maxvalue = 100,
						stradd = "%",
					},
					{
						type = "dropbox",
						name = "Smoothing Type",
						value = 2,
						values = { "Exponential", "Linear" },
					},
					{
						type = "slider",
						name = "Randomization",
						value = 5,
						minvalue = 0,
						maxvalue = 20,
						custom = { [0] = "Off" },
					},
					{
						type = "slider",
						name = "Deadzone FOV",
						value = 1,
						minvalue = 0,
						maxvalue = 50,
						stradd = "°",
						decimal = 0.1,
						custom = { [0] = "Off" },
					},
					{
						type = "dropbox",
						name = "Aimbot Key",
						value = 1,
						values = { "Mouse 1", "Mouse 2", "Always" },
					},
					{
						type = "dropbox",
						name = "Hitscan Priority",
						value = 1,
						values = { "Head", "Body", "Closest" },
					},
					{
						type = "combobox",
						name = "Hitscan Points",
						values = { { "Head", true }, { "Body", true }, { "Arms", false }, { "Legs", false } },
					},
					{
						type = "toggle",
						name = "Adjust for Bullet Drop",
						value = false,
					},
					{
						type = "toggle",
						name = "Target Prediction",
						value = false,
					},
					{
						type = "slider",
						name = "Enlarge Enemy Hitboxes",
						value = 0,
						minvalue = 0,
						maxvalue = 100,
						stradd = "%",
					},
				},
			},
			{
				name = "Trigger Bot",
				autopos = "right",
				content = {
					{
						type = "toggle",
						name = "Enabled",
						value = false,
						extra = {
							type = "keybind",
							key = Enum.KeyCode.M,
						},
					},
					{
						type = "combobox",
						name = "Trigger Bot Hitboxes",
						values = { { "Head", true }, { "Body", true }, { "Arms", false }, { "Legs", false } },
					},
					{
						type = "toggle",
						name = "Trigger When Aiming",
						value = false,
					},
					{
						type = "slider",
						name = "Aim Percentage",
						minvalue = 0,
						maxvalue = 100,
						value = 90,
						stradd = "%",
					},
					--[[
			{
				type = "toggle",
				name = "Magnet Triggerbot",
				value = false
			},
			{
				type = "slider",
				name = "Magnet FOV",
				value = 80,
				minvalue = 0,
				maxvalue = 180,
				stradd = "°"
			},
			{
				type = "slider",
				name = "Magnet Smoothing Factor",
				value = 20,
				minvalue = 0,
				maxvalue = 50,
				stradd = "%"
			},
			{
				type = "dropbox",
				name = "Magnet Priority",
				value = 1,
				values = {"Head", "Body"}
			},]]
				},
			},
			{
				name = "Bullet Redirection",
				autopos = "right",
				autofill = true,
				content = {
					{
						type = "toggle",
						name = "Silent Aim",
						value = false,
					},
					{
						type = "slider",
						name = "Silent Aim FOV",
						value = 5,
						minvalue = 0.1,
						maxvalue = 180,
						stradd = "°",
						decimal = 0.1,
					},
					{
						type = "slider",
						name = "Hit Chance",
						value = 30,
						minvalue = 0,
						maxvalue = 100,
						stradd = "%",
					},
					{
						type = "slider",
						name = "Accuracy",
						value = 90,
						minvalue = 0,
						maxvalue = 100,
						stradd = "%",
					},
					{
						type = "dropbox",
						name = "Hitscan Priority",
						value = 1,
						values = { "Head", "Body", "Closest" },
					},
					{
						type = "combobox",
						name = "Hitscan Points",
						values = { { "Head", true }, { "Body", true }, { "Arms", false }, { "Legs", false } },
					},
				},
			},
			{
				name = "Recoil Control",
				autopos = "left",
				autofill = true,
				content = {
					{
						type = "toggle",
						name = "Weapon RCS",
						value = false,
					},
					{
						type = "slider",
						name = "Recoil Control X",
						value = 10,
						minvalue = 0,
						maxvalue = 100,
						stradd = "%",
					},
					{
						type = "slider",
						name = "Recoil Control Y",
						value = 10,
						minvalue = 0,
						maxvalue = 100,
						stradd = "%",
					},
				},
			},
		},
	},
	{
		name = "Rage",
		content = {
			{
				name = "Aimbot",
				autopos = "left",
				content = {
					{
						type = "toggle",
						name = "Enabled",
						value = false,
						extra = {
							type = "keybind",
							toggletype = 4,
						},
						unsafe = true,
					},
					{
						type = "toggle",
						name = "Silent Aim",
						value = false,
					},
					{
						type = "toggle",
						name = "Rotate Viewmodel",
						value = false,
					},
					{
						type = "slider",
						name = "Aimbot FOV",
						value = 180,
						minvalue = 0,
						maxvalue = 181,
						stradd = "°",
						custom = { [181] = "Ignored" },
					},
					{
						type = "dropbox",
						name = "Auto Wall",
						value = 1,
						values = { "Off", "Standard", "Legacy" },
					},
					{
						type = "slider",
						name = "Autowall FPS (Standard)",
						value = 30,
						minvalue = 10,
						maxvalue = 30,
						stradd = "fps",
					},
					{
						type = "toggle",
						name = "Auto Shoot",
						value = false,
					},
					{
						type = "toggle",
						name = "Double Tap",
						value = false,
					},
					{
						type = "dropbox",
						name = "Hitscan Priority",
						value = 1,
						values = { "Head", "Body" },
					},
				},
			},
			{
				name = "Hack vs. Hack",
				autopos = "right",
				content = {
					--[[{
				type = "toggle",
				name = "Extend Penetration",
				value = false
			},]]
					-- {
					-- 	type = "slider",
					-- 	name = "Extra Penetration",
					-- 	value = 11,
					-- 	minvalue = 1,
					-- 	maxvalue = 20,
					-- 	stradd = " studs",
					-- 	tooltip = "does nothing",
					-- }, -- fuck u json
					{
						type = "toggle",
						name = "Autowall Hitscan",
						value = false,
						unsafe = true,
					},
					{
						type = "combobox",
						name = "Hitscan Points",
						values = {
							{ "Up", true },
							{ "Down", true },
							{ "Left", false },
							{ "Right", false },
							{ "Forward", true },
							{ "Backward", true },
							{ "Origin", true },
							{ "Towards", true },
						},
					},
					{
						type = "toggle",
						name = "Hitbox Shifting",
						value = false,
						tooltip = "Increases possible penetration with Autowall. The higher\nthe Hitbox Shift Distance the more likely it is to miss shots.\nWhen it misses it will try disable this.",
					},
					{
						type = "slider",
						name = "Hitbox Shift Distance",
						value = 16,
						minvalue = 1,
						maxvalue = 30,
						stradd = " studs",
					},
					{
						type = "toggle",
						name = "Force Player Stances",
						value = false,
					},
					{
						type = "dropbox",
						name = "Stance Choice",
						value = 1,
						values = { "Stand", "Crouch", "Prone" },
					},
					{
						type = "toggle", 
						name = "Backtracking",
						value = false,
					},
					{
						type = "slider",
						name = "Backtracking Time",
						value = 4000,
						minvalue = 0,
						maxvalue = 5000,
						stradd = " ms",
					},
					{
						type = "toggle",
						name = "Freestanding",
						value = false,
						extra = {
							type = "keybind",
						},
					},
				},
			},
			{
				name = { "Extra", "Settings" },
				autopos = "left",
				autofill = true,
				[1] = {
					content = {
						{
							type = "toggle",
							name = "Knife Bot",
							value = false,
							extra = {
								type = "keybind",
							},
							unsafe = true,
						},
						{
							type = "dropbox",
							name = "Knife Bot Type",
							value = 2,
							values = { "Assist", "Multi Aura", "Flight Aura" },
						},
						{
							type = "toggle",
							name = "Auto Peek",
							value = false,
							extra = {
								type = "keybind",
								toggletype = 1,
							},
							tooltip = "Hitscans from in front of your camera,\nif a target is found it will move you towards the point automatically",
						},
					},
				},
				[2] = {
					content = {
						{
							type = "toggle",
							name = "Aimbot Performance Mode",
							value = true,
							tooltip = "Lowers polling rate for targetting in Rage Aimbot.",
						},
						{
							type = "toggle",
							name = "Aimbot Damage Prediction",
							value = true,
							tooltip = "Predicts damage done to enemies as to prevent wasting ammo and time on certain players.\nHelps for users, and against players with high latency.",
						},
						{
							type = "slider",
							name = "Damage Prediction Limit",
							value = 100,
							minvalue = 0,
							maxvalue = 300,
							stradd = "hp",
						},
						{
							type = "slider",
							name = "Damage Prediction Time",
							value = 200,
							minvalue = 100,
							maxvalue = 500,
							stradd = "%",
						},
						{
							type = "slider",
							name = "Max Hitscan Points",
							value = 30,
							minvalue = 0,
							maxvalue = 300,
							stradd = " points",
						},
					},
				},
			},
			{
				name = { "Anti Aim", "Fake Lag" },
				autopos = "right",
				autofill = true,
				[1] = {
					content = {
						{
							type = "toggle",
							name = "Enabled",
							value = false,
							tooltip = "When this is enabled, your server-side yaw, pitch and stance are set to the values in this tab.",
						},
						{
							type = "dropbox",
							name = "Pitch",
							value = 4,
							values = {
								"Off",
								"Up",
								"Zero",
								"Down",
								"Upside Down",
								"Roll Forward",
								"Roll Backward",
								"Random",
								"Bob",
								"Glitch",
							},
						},
						{
							type = "dropbox",
							name = "Yaw",
							value = 2,
							values = { "Forward", "Backward", "Spin", "Random", "Glitch Spin", "Stutter Spin" },
						},
						{
							type = "slider",
							name = "Spin Rate",
							value = 10,
							minvalue = -100,
							maxvalue = 100,
							stradd = "°/s",
						},
						{
							type = "dropbox",
							name = "Force Stance",
							value = 4,
							values = { "Off", "Stand", "Crouch", "Prone" },
						},
						{
							type = "toggle",
							name = "Hide in Floor",
							value = true,
							tooltip = "Shifts your body slightly under the ground\nso as to hide it when Force Stance is set to Prone.",
						},
						{
							type = "toggle",
							name = "Lower Arms",
							value = false,
							tooltip = "Lowers your arms on the server.",
						},
						{
							type = "toggle",
							name = "Tilt Neck",
							value = false,
							tooltip = "Forces the replicated aiming state so that it appears as though your head is tilted.",
						},
					},
				},
				[2] = {
					content = {
						{
							type = "toggle",
							name = "Enabled",
							value = false,
						},
						{
							type = "slider",
							name = "Fake Lag Amount",
							value = 1,
							minvalue = 1,
							maxvalue = 1000,
							stradd = " kbps",
						},
						{
							type = "slider",
							name = "Fake Lag Distance",
							value = 1,
							minvalue = 1,
							maxvalue = 40,
							stradd = " studs",
						},
						{
							type = "toggle",
							name = "Manual Choke",
							extra = {
								type = "keybind",
							},
						},
						{
							type = "toggle",
							name = "Release Packets on Shoot",
							value = false,
						},
					},
				},
			},
		},
	},
	{
		name = "Visuals",
		content = {
			{
				name = { "Enemy ESP", "Team ESP", "Local" },
				autopos = "left",
				size = 330,
				[1] = {
					content = {
						{
							type = "toggle",
							name = "Enabled",
							value = true,
						},
						{
							type = "toggle",
							name = "Name",
							value = true,
							extra = {
								type = "single colorpicker",
								name = "Enemy Name",
								color = { 255, 255, 255, 200 },
							},
						},
						{
							type = "toggle",
							name = "Rank",
							value = false,
						},
						{
							type = "toggle",
							name = "Box",
							value = true,
							extra = {
								type = "single colorpicker",
								name = "Enemy Box",
								color = { 255, 0, 0, 150 },
							},
						},
						{
							type = "toggle",
							name = "Filled Box",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Enemy Filled Box",
								color = { 255, 0, 0, 90 },
							},
						},
						{
							type = "toggle",
							name = "Health Bar",
							value = true,
							extra = {
								type = "double colorpicker",
								name = { "Enemy Low Health", "Enemy Max Health" },
								color = { { 255, 0, 0 }, { 0, 255, 0 } },
							},
						},
						{
							type = "toggle",
							name = "Health Number",
							value = true,
							extra = {
								type = "single colorpicker",
								name = "Enemy Health Number",
								color = { 255, 255, 255, 255 },
							},
						},
						{
							type = "toggle",
							name = "Held Weapon",
							value = true,
							extra = {
								type = "single colorpicker",
								name = "Enemy Held Weapon",
								color = { 255, 255, 255, 200 },
							},
						},
						{
							type = "toggle",
							name = "Distance",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Enemy Distance",
								color = { 255, 255, 255, 200 },
							},
						},
						{
							type = "toggle",
							name = "Chams",
							value = true,
							extra = {
								type = "double colorpicker",
								name = { "Visible Enemy Chams", "Invisible Enemy Chams" },
								color = { { 255, 0, 0, 200 }, { 100, 0, 0, 100 } },
							},
						},
						{
							type = "toggle",
							name = "Skeleton",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Enemy skeleton",
								color = { 255, 255, 255, 120 },
							},
						},
						{
							type = "toggle",
							name = "Out of View",
							value = true,
							extra = {
								type = "single colorpicker",
								name = "Arrow Color",
								color = { 255, 255, 255, 255 },
							},
						},
						{
							type = "slider",
							name = "Arrow Distance",
							value = 50,
							minvalue = 10,
							maxvalue = 100,
							stradd = "%",
						},
						{
							type = "toggle",
							name = "Dynamic Arrow Size",
							value = true,
						},
						{
							type = "toggle",
							name = "Show Resolved Position",
							value = false,
						},
						{
							type = "toggle",
							name = "Show Backtracked Position",
							value = false,
						},
					},
				},
				[2] = {
					content = {
						{
							type = "toggle",
							name = "Enabled",
							value = false,
						},
						{
							type = "toggle",
							name = "Name",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Team Name",
								color = { 255, 255, 255, 200 },
							},
						},
						{
							type = "toggle",
							name = "Rank",
							value = false,
						},
						{
							type = "toggle",
							name = "Box",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Team Box",
								color = { 0, 255, 0, 150 },
							},
						},
						{
							type = "toggle",
							name = "Filled Box",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Team Filled Box",
								color = { 0, 255, 0, 90 },
							},
						},
						{
							type = "toggle",
							name = "Health Bar",
							value = false,
							extra = {
								type = "double colorpicker",
								name = { "Team Low Health", "Team Max Health" },
								color = { { 255, 0, 0 }, { 0, 255, 0 } },
							},
						},
						{
							type = "toggle",
							name = "Health Number",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Team Health Number",
								color = { 255, 255, 255, 255 },
							},
						},
						{
							type = "toggle",
							name = "Held Weapon",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Team Held Weapon",
								color = { 255, 255, 255, 200 },
							},
						},
						{
							type = "toggle",
							name = "Distance",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Team Distance",
								color = { 255, 255, 255, 200 },
							},
						},
						{
							type = "toggle",
							name = "Chams",
							value = false,
							extra = {
								type = "double colorpicker",
								name = { "Visible Team Chams", "Invisible Team Chams" },
								color = { { 0, 255, 0, 200 }, { 0, 100, 0, 100 } },
							},
						},
						{
							type = "toggle",
							name = "Skeleton",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Team skeleton",
								color = { 255, 255, 255, 120 },
							},
						},
					},
				},
				[3] = {
					content = {
						{
							type = "toggle",
							name = "Arm Chams",
							value = false,
							extra = {
								type = "double colorpicker",
								name = { "Sleeve Color", "Hand Color" },
								color = { { 106, 136, 213, 255 }, { 181, 179, 253, 255 } },
							},
						},
						{
							type = "dropbox",
							name = "Arm Material",
							value = 1,
							values = { "Plastic", "Ghost", "Neon", "Foil", "Glass" },
						},
						{
							type = "toggle",
							name = "Weapon Chams",
							value = false,
							extra = {
								type = "double colorpicker",
								name = { "Weapon Color", "Laser Color" },
								color = { { 106, 136, 213, 255 }, { 181, 179, 253, 255 } },
							},
						},
						{
							type = "dropbox",
							name = "Weapon Material",
							value = 1,
							values = { "Plastic", "Ghost", "Neon", "Foil", "Glass" },
						},
						{
							type = "toggle",
							name = "Animate Ghost Material",
							value = false,
							tooltip = "Toggles whether or not the 'Ghost' material will be animated or not.",
						},
						{
							type = "toggle",
							name = "Remove Weapon Skin",
							value = false,
							tooltip = "If a loaded weapon has a skin, it will remove it.",
						},
						{
							type = "toggle",
							name = "Third Person",
							value = false,
							extra = {
								type = "keybind",
								key = nil,
								toggletype = 2,
							},
						},
						{
							type = "slider",
							name = "Third Person Distance",
							value = 60,
							minvalue = 1,
							maxvalue = 150,
						},
						{
							type = "toggle",
							name = "Local Player Chams",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Local Player Chams",
								color = { 106, 136, 213, 255 },
							},
							tooltip = "Changes the color and material of the local third person body when it is on.",
						},
						{
							type = "dropbox",
							name = "Local Player Material",
							value = 1,
							values = { "Plastic", "Ghost", "Neon", "Foil", "Glass" },
						},
					},
				},
			},
			{
				name = "ESP Settings",
				autopos = "left",
				autofill = true,
				content = {
					{
						type = "slider",
						name = "Max HP Visibility Cap",
						value = 90,
						minvalue = 50,
						maxvalue = 100,
						stradd = "hp",
					},
					{
						type = "dropbox",
						name = "Text Case",
						value = 2,
						values = { "lowercase", "Normal", "UPPERCASE" },
					},
					{
						type = "slider",
						name = "Max Text Length",
						value = 0,
						minvalue = 0,
						maxvalue = 32,
						custom = { [0] = "Unlimited" },
					},
					{
						type = "toggle",
						name = "Highlight Aimbot Target",
						value = false,
						extra = {
							type = "single colorpicker",
							name = "Aimbot Target",
							color = { 255, 0, 0, 255 },
						},
					},
					{
						type = "toggle",
						name = "Highlight Friends",
						value = true,
						extra = {
							type = "single colorpicker",
							name = "Friended Players",
							color = { 0, 255, 255, 255 },
						},
					},
					{
						type = "toggle",
						name = "Highlight Priority",
						value = true,
						extra = {
							type = "single colorpicker",
							name = "Priority Players",
							color = { 255, 210, 0, 255 },
						},
					},
					-- {
					-- 	type = "slider",
					-- 	name = "Max Player Text",
					-- 	value = 0,
					-- 	minvalue = 0,
					-- 	maxvalue = 32,
					-- 	custom = {[0] = "None"},
					-- }
				},
			},
			{
				name = { "Camera Visuals", "Viewmodel" },
				autopos = "right",
				size = 240,
				[1] = {
					content = {
						{
							type = "slider",
							name = "Camera FOV",
							value = 85,
							minvalue = 60,
							maxvalue = 120,
							stradd = "°",
						},
						{
							type = "toggle",
							name = "No Camera Bob",
							value = false,
						},
						{
							type = "toggle",
							name = "No Scope Sway",
							value = false,
						},
						{
							type = "toggle",
							name = "Disable ADS FOV",
							value = false,
						},
						{
							type = "toggle",
							name = "No Scope Border",
							value = false,
						},
						{
							type = "toggle",
							name = "No Visual Suppression",
							value = false,
							tooltip = "Removes the suppression of enemies' bullets.",
						},
						{
							type = "toggle",
							name = "No Gun Bob or Sway",
							value = false,
							tooltip = "Removes the bob and sway of weapons when walking.\nThis does not remove the swing effect when moving your mouse.",
						},
						{
							type = "toggle",
							name = "Reduce Camera Recoil",
							value = false,
							tooltip = "Reduces camera recoil by X%. Does not affect visible weapon recoil or kick.",
						},
						{
							type = "slider",
							name = "Camera Recoil Reduction",
							value = 10,
							minvalue = 0,
							maxvalue = 100,
							stradd = "%",
						},
					},
				},
				[2] = {
					content = {
						{
							type = "toggle",
							name = "Enabled",
							value = false,
						},
						{
							type = "slider",
							name = "Offset X",
							value = 0,
							minvalue = -3,
							maxvalue = 3,
							decimal = 0.01,
							stradd = " studs",
						},
						{
							type = "slider",
							name = "Offset Y",
							value = 0,
							minvalue = -3,
							maxvalue = 3,
							decimal = 0.01,
							stradd = " studs",
						},
						{
							type = "slider",
							name = "Offset Z",
							value = 0,
							minvalue = -3,
							maxvalue = 3,
							decimal = 0.01,
							stradd = " studs",
						},
						{
							type = "slider",
							name = "Pitch",
							value = 0,
							minvalue = -180,
							maxvalue = 180,
							stradd = "°",
						},
						{
							type = "slider",
							name = "Yaw",
							value = 0,
							minvalue = -180,
							maxvalue = 180,
							stradd = "°",
						},
						{
							type = "slider",
							name = "Roll",
							value = 0,
							minvalue = -180,
							maxvalue = 180,
							stradd = "°",
						},
					},
				},
			},
			{
				name = { "World", "Misc", "Keybinds", "FOV" },

				autopos = "right",
				size = 144,
				[1] = {
					content = {
						{
							type = "toggle",
							name = "Ambience",
							value = false,
							extra = {
								type = "double colorpicker",
								name = { "Inside Ambience", "Outside Ambience" },
								color = { { 117, 76, 236 }, { 117, 76, 236 } },
							},
							tooltip = "Changes the map's ambient colors to the user defined colors.",
						},
						{
							type = "toggle",
							name = "Force Time",
							value = false,
							tooltip = "Forces the time to the time set by the user below.",
						},
						{
							type = "slider",
							name = "Custom Time",
							value = 0,
							minvalue = 0,
							maxvalue = 24,
							decimal = 0.1,
						},
						{
							type = "toggle",
							name = "Custom Saturation",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Saturation Tint",
								color = { 255, 255, 255 },
							},
							tooltip = "Adds custom saturation the image of the game.",
						},
						{
							type = "slider",
							name = "Saturation Density",
							value = 0,
							minvalue = 0,
							maxvalue = 100,
							stradd = "%",
						},
					},
				},
				[2] = {
					content = {
						{
							type = "toggle",
							name = "Crosshair Color",
							value = false,
							extra = {
								type = "double colorpicker",
								name = { "Inline", "Outline" },
								color = { { 127, 72, 163 }, { 25, 25, 25 } },
							},
						},
						{
							type = "toggle",
							name = "Laser Pointer",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Laser Pointer Color",
								color = { 255, 255, 255, 255 },
							},
						},
						{
							type = "toggle",
							name = "Ragdoll Chams",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Ragdoll Chams",
								color = { 106, 136, 213, 255 },
							},
						},
						{
							type = "dropbox",
							name = "Ragdoll Material",
							value = 1,
							values = { "Plastic", "Ghost", "Neon", "Foil", "Glass" },
						},
						{
							type = "toggle",
							name = "Bullet Tracers",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Bullet Tracers",
								color = { 201, 69, 54 },
							},
						},
					},
				},
				[3] = {
					content = {
						{
							type = "toggle",
							name = "Enabled",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Text Color",
								color = { 127, 72, 163, 255 },
							},
						},
						{
							type = "toggle",
							name = "Use List Sizes",
							value = false,
						},
						{
							type = "toggle",
							name = "Log Keybinds",
							value = false
						}
					},
				},
				[4] = {
					content = {
						{
							type = "toggle",
							name = "Enabled",
							value = false,
						},
						{
							type = "toggle",
							name = "Aim Assist",
							value = true,
							extra = {
								type = "single colorpicker",
								name = "Aim Assist FOV",
								color = { 127, 72, 163, 255 },
							},
						},
						{
							type = "toggle",
							name = "Aim Assist Deadzone",
							value = true,
							extra = {
								type = "single colorpicker",
								name = "Deadzone FOV",
								color = { 50, 50, 50, 255 },
							},
						},
						{
							type = "toggle",
							name = "Bullet Redirection",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Bullet Redirection FOV",
								color = { 163, 72, 127, 255 },
							},
						},
						{
							type = "toggle",
							name = "Ragebot",
							value = false,
							extra = {
								type = "single colorpicker",
								name = "Ragebot FOV",
								color = { 255, 210, 0, 255 },
							},
						},
					},
				},
			},
			{
				name = "Dropped ESP",
				autopos = "right",
				autofill = true,
				content = {
					{
						type = "toggle",
						name = "Weapon Names",
						value = false,
						extra = {
							type = "double colorpicker",
							name = { "Highlighted Weapons", "Weapon Names" },
							color = { { 255, 125, 255, 255 }, { 255, 255, 255, 255 } },
						},
						tooltip = "Displays dropped weapons as you get closer to them,\nHighlights the weapon you are holding in the second color.",
					},
					{
						type = "toggle",
						name = "Weapon Ammo",
						value = false,
						extra = {
							type = "single colorpicker",
							name = "Weapon Ammo",
							color = { 61, 168, 235, 150 },
						},
					},
					{
						type = "toggle",
						name = "Dropped Weapon Chams",
						value = false,
						extra = {
							type = "single colorpicker",
							name = "Dropped Weapon Color",
							color = { 3, 252, 161, 150 },
						},
					},
					{
						type = "toggle",
						name = "Grenade Warning",
						value = true,
						extra = {
							type = "single colorpicker",
							name = "Slider Color",
							color = { 68, 92, 227 },
						},
						tooltip = "Displays where grenades that will deal\ndamage to you will land and the damage they will deal.",
					},
					{
						type = "toggle",
						name = "Grenade ESP",
						value = false,
						extra = {
							type = "double colorpicker",
							name = { "Inner Color", "Outer Color" },
							color = { { 195, 163, 255 }, { 123, 69, 224 } },
						},
						tooltip = "Displays the full path of any grenade that will deal damage to you is thrown.",
					},
				},
			},
		},
	},
	{
		name = "Misc",
		content = {
			{
				name = { "Movement", "Tweaks" },
				autopos = "left",
				size = 250,
				[1] = {
					content = {
						{
							type = "toggle",
							name = "Fly",
							value = false,
							unsafe = true,
							tooltip = "Manipulates your velocity to make you fly.\nUse 60 speed or below to never get flagged.",
							extra = {
								type = "keybind",
								key = Enum.KeyCode.B,
								toggletype = 2,
							},
						},
						{
							type = "slider",
							name = "Fly Speed",
							value = 60,
							minvalue = 1,
							maxvalue = 400,
							stradd = " stud/s",
						},
						{
							type = "toggle",
							name = "Auto Jump",
							value = false,
							tooltip = "When you hold the spacebar, it will automatically jump repeatedly, ignoring jump delay.",
						},
						{
							type = "toggle",
							name = "Speed",
							value = false,
							unsafe = true,
							tooltip = "Manipulates your velocity to make you move faster, unlike fly it doesn't make you fly.\nUse 60 speed or below to never get flagged.",
							extra = {
								type = "keybind",
								toggletype = 4,
							},
						},
						{
							type = "dropbox",
							name = "Speed Type",
							value = 1,
							values = { "Always", "In Air", "On Hop" },
						},
						{
							type = "slider",
							name = "Speed Factor",
							value = 40,
							minvalue = 1,
							maxvalue = 400,
							stradd = " stud/s",
						},
						{
							type = "toggle",
							name = "Circle Strafe",
							value = false,
							extra = {
								type = "keybind",
							},
							tooltip = "When you hold this keybind, it will strafe in a perfect circle.\nSpeed of strafing is borrowed from Speed Factor.",
						},
						{
							type = "toggle",
							name = "Bypass Speed Checks",
							value = false,
							unsafe = true,
							tooltip = "Attempts to bypass maximum speed limit on the server.",
						},
					},
				},
				[2] = {
					content = {
						{
							type = "toggle",
							name = "Gravity Shift",
							value = false,
							tooltip = "Shifts movement gravity by X%. (Does not affect bullet acceleration.)",
						},
						{
							type = "slider",
							name = "Gravity Shift Percentage",
							value = -50,
							minvalue = -500,
							maxvalue = 500,
							stradd = "%",
						},
						{
							type = "toggle",
							name = "Jump Power",
							value = false,
							tooltip = "Shifts movement jump power by X%.",
						},
						{
							type = "slider",
							name = "Jump Power Percentage",
							value = 150,
							minvalue = 0,
							maxvalue = 1000,
							stradd = "%",
						},
						{
							type = "toggle",
							name = "Prevent Fall Damage",
							value = false,
						},
					},
				},
			},
			{
				name = "Weapon Modifications",
				autopos = "left",
				autofill = true,
				content = {
					{
						type = "toggle",
						name = "Enabled",
						value = false,
						tooltip = "Allows Bitch Bot to modify weapons.",
					},
					{
						type = "slider",
						name = "Fire Rate Scale",
						value = 150,
						minvalue = 50,
						maxvalue = 500,
						stradd = "%",
						tooltip = "Scales all weapons' firerate by X%.\n100% = Normal firerate",
					},
					{
						type = "slider",
						name = "Recoil Scale",
						value = 10,
						minvalue = 0,
						maxvalue = 100,
						stradd = "%",
						tooltip = "Scales all weapons' recoil by X%.\n0% = No recoil | 50% = Halved recoil",
					},
					{
						type = "toggle",
						name = "Remove Animations",
						value = true,
						tooltip = "Removes all animations from any gun.\nThis will also completely remove the equipping animations.",
					},
					{
						type = "toggle",
						name = "Instant Equip",
						value = true,
					},
					{
						type = "toggle",
						name = "Fully Automatic",
						value = true,
					},
					{
						type = "toggle",
						name = "Run and Gun",
						value = false,
						tooltip = "Makes it so that your weapon does not\nsway due to mouse movement, or turns over while sprinting.",
					},
				},
			},
			{
				name = { "Extra", "Exploits" },
				autopos = "right",
				autofill = true,
				[1] = {
					content = {
						{
							type = "toggle",
							name = "Ignore Friends",
							value = true,
							tooltip = "When turned on, bullets do not deal damage to friends,\nand Rage modules won't target friends.",
						},
						{
							type = "toggle",
							name = "Target Only Priority Players",
							value = false,
							tooltip = "When turned on, all modules except for Aim Assist that target players\nwill ignore anybody that isn't on the Priority list.",
						},
						{
							type = "toggle",
							name = "Suppress Only",
							value = false,
							tooltip = "When turned on, bullets do not deal damage.",
						},
						{
							type = "toggle",
							name = "Auto Respawn",
							value = false,
							tooltip = "Automatically respawns after deaths.",
						},
						{
							type = "toggle",
							name = "Auto Vote",
							value = false,
							tooltip = "When votekicks are started, Bitch Bot will automatically choose\nwhat choice to make depending on the options below.",
						},
						{
							type = "dropbox",
							name = "Vote Friends",
							value = 1,
							values = { "Off", "Yes", "No" },
						},
						{
							type = "dropbox",
							name = "Vote Priority",
							value = 1,
							values = { "Off", "Yes", "No" },
						},
						{
							type = "dropbox",
							name = "Default Vote",
							value = 1,
							values = { "Off", "Yes", "No" },
						},
						{
							type = "toggle",
							name = "Kill Sound",
							value = false,
						},
						{
							type = "textbox",
							name = "killsoundid",
							text = "6229978482",
							tooltip = "The Roblox sound ID or file inside of synapse\n workspace to play when Kill Sound is on.",
						},
						{
							type = "slider",
							name = "Kill Sound Volume",
							value = 20,
							minvalue = 0,
							maxvalue = 100,
							stradd = "%",
						},
						{
							type = "toggle",
							name = "Kill Say",
							value = false,
							tooltip = "Kill say messages, located in bitchbot/killsay.txt \n[name] is the target's name\n[weapon] is the weapon used\n[hitbox] says head or body depending on where you shot the player",
						},
						{
							type = "dropbox",
							name = "Chat Spam",
							value = 1,
							values = {
								"Off",
								"Original",
								"t0nymode",
								"Chinese Propaganda",
								"Emojis",
								"Deluxe",
								"Youtube Title",
								"Custom",
								"Custom Combination",
							},
							tooltip = "Spams chat, Custom options are located in the bitchbot/chatspam.txt",
						},
						{
							type = "toggle",
							name = "Chat Spam Repeat",
							value = false,
							tooltip = "Repeats the same Chat Spam message in chat.",
						},
						{
							type = "slider",
							name = "Chat Spam Delay",
							minvalue = 1,
							maxvalue = 10,
							value = 5,
							stradd = " seconds",
						},
						{
							type = "toggle",
							name = "Auto Martyrdom",
							value = false,
							tooltip = "Whenever you die to an enemy, this will drop a grenade\nat your death position. If Grenade Teleport is on, it will place the grenade at the enemy.",
						},
						{
							type = "toggle",
							name = "Break Windows",
							value = false,
							tooltip = "Breaks all windows in the map when you spawn."
						},
						{
							type = "button",
							name = "Join New Game",
							value = false,
							unsafe = false,
							doubleclick = true,
						},

					},
				},
				[2] = {
					content = {

						--[[{
					type = "toggle",
					name = "Super Invisibility",
					value = false,
					extra = {
						type = "keybind"
					}
				},]]
						{
							type = "button",
							name = "Crash Server",
							doubleclick = true,
							tooltip = "Attempts to overwhelm the server so that users are kicked for internet connection problems.\nRoblox may detect strange activity and automatically\nkick you for it before the server can crash.",
						},
						{
							type = "toggle",
							name = "Invisibility",
							extra = {
								type = "keybind",
								toggletype = 0,
							},
						},
						{
							type = "toggle",
							name = "Rapid Kill",
							value = false,
							extra = {
								type = "keybind",
								toggletype = 0,
							},
							tooltip = "Throws 3 grenades instantly on random enemies.",
						},
						{
							type = "toggle",
							name = "Auto Rapid Kill",
							value = false,
							tooltip = "Throws 3 grenades instantly on random enemies,\nthen respawns to do it again.\nWorks only when Rapid Kill is enabled.",
						},
						{
							type = "toggle",
							name = "Grenade Teleport",
							value = false,
							tooltip = "Sets any spawned grenade's position to the nearest enemy to your cursor and instantly explodes.",
						},
						{
							type = "toggle",
							name = "Crimwalk",
							value = false,
							extra = {
								type = "keybind",
							},
						},
						{
							type = "toggle",
							name = "Teleport",
							value = false,
							extra = {
								type = "keybind",
								toggletype = 0,
							},
							tooltip = "When key pressed you will teleport to the mouse position",
						},
						{
							type = "toggle",
							name = "Disable Crimwalk on Shot",
							value = true,
						},
						{
							type = "toggle",
							name = "Vertical Floor Clip",
							value = false,
							extra = {
								type = "keybind",
								toggletype = 0,
							},
							tooltip = "Teleports you 19 studs under the ground. Must be over glass or non-collidable parts to work. \nHold Alt to go up, and Shift to go forwards.",
						},
						{
							type = "toggle",
							name = "Fake Equip",
							value = false,
							unsafe = true,
						},
						{
							type = "dropbox",
							name = "Fake Slot",
							values = { "Primary", "Secondary", "Melee" },
							value = 1,
						},

						-- {
						-- 	type = "toggle",
						-- 	name = "Noclip",
						-- 	value = false,
						-- 	extra = {
						-- 		type = "keybind",
						-- 		key = nil
						-- 	},
						-- 	unsafe = true,
						-- 	tooltip = "Allows you to noclip through most parts of the map. Must be over glass or non-collidable parts to work."
						-- },
						-- {
						-- 	type = "toggle",
						-- 	name = "Fake Position",
						-- 	value = false,
						-- 	extra = {
						-- 		type = "keybind"
						-- 	},
						-- 	unsafe = true,
						-- 	tooltip = "Fakes your server-side position. Works best when stationary, and allows you to be unhittable."
						-- },
						{
							type = "toggle",
							name = "Lock Player Positions",
							value = false,
							extra = {
								type = "keybind",
							},
							tooltip = "Locks all other players' positions.",
						},
						{
							type = "toggle",
							name = "Skin Changer",
							value = false,
							tooltip = "While this is enabled, all custom skins will apply with the custom settings below.",
							extra = {
								type = "single colorpicker",
								name = "Weapon Skin Color",
								color = { 127, 72, 163, 255 },
							},
						},
						{
							type = "textbox",
							name = "skinchangerTexture",
							text = "6156783684",
						},
						{
							type = "slider",
							name = "Scale X",
							value = 10,
							minvalue = 1,
							maxvalue = 500,
							stradd = "%",
						},
						{
							type = "slider",
							name = "Scale Y",
							value = 10,
							minvalue = 1,
							maxvalue = 500,
							stradd = "%",
						},
						{
							type = "dropbox",
							name = "Skin Material",
							value = 1,
							values = { "Plastic", "Ghost", "Neon", "Foil", "Glass" },
						},
					},
				},
			},
		},
	},
	{
		name = "Settings",
		content = {
			
			{
				name = "Cheat Settings",
				x = menu.columns.left,
				y = menu.columns.right - 185,
				width = menu.columns.width,
				height = 182,
				content = {
					{
						type = "toggle",
						name = "Menu Accent",
						value = false,
						extra = {
							type = "single colorpicker",
							name = "Accent Color",
							color = { 127, 72, 163 },
						},
					},
					{
						type = "toggle",
						name = "Watermark",
						value = true,
					},
					{
						type = "toggle",
						name = "Custom Menu Name",
						value = MenuName and true or false,
					},
					{
						type = "textbox",
						name = "MenuName",
						text = MenuName or "Bitch Bot",
					},
					{
						type = "button",
						name = "Set Clipboard Game ID",
					},
					{
						type = "button",
						name = "Unload Cheat",
						doubleclick = true,
					},
					{
						type = "toggle",
						name = "Allow Unsafe Features",
						value = false,
					},
				},
			},
			{
				name = "Configuration",
				x = menu.columns.right,
				y = menu.columns.left + 50,
				width = menu.columns.width,
				height = 182,
				content = {
					{
						type = "textbox",
						name = "ConfigName",
						file = true,
						text = "",
					},
					{
						type = "dropbox",
						name = "Configs",
						value = 1,
						values = GetConfigs(),
					},
					{
						type = "button",
						name = "Load Config",
						doubleclick = true,
					},
					{
						type = "button",
						name = "Save Config",
						doubleclick = true,
					},
					{
						type = "button",
						name = "Delete Config",
						doubleclick = true,
					},
				},
			},
		},
	},
})



do
	local wm = menu.watermark
	wm.textString = " | " .. "user" .. " | " .. os.date("%b. %d, %Y")
	wm.pos = Vector2.new(50, 9)
	wm.text = {}
	local fulltext = menu.options["Settings"]["Cheat Settings"]["MenuName"][1] .. wm.textString
	wm.width = #fulltext * 7 + 10
	wm.height = 19
	wm.rect = {}

	Draw:FilledRect(
		false,
		wm.pos.x,
		wm.pos.y + 1,
		wm.width,
		2,
		{ menu.mc[1] - 40, menu.mc[2] - 40, menu.mc[3] - 40, 255 },
		wm.rect
	)
	Draw:FilledRect(false, wm.pos.x, wm.pos.y, wm.width, 2, { menu.mc[1], menu.mc[2], menu.mc[3], 255 }, wm.rect)
	Draw:FilledRect(false, wm.pos.x, wm.pos.y + 3, wm.width, wm.height - 5, { 50, 50, 50, 255 }, wm.rect)
	for i = 0, wm.height - 4 do
		Draw:FilledRect(
			false,
			wm.pos.x,
			wm.pos.y + 3 + i,
			wm.width,
			1,
			{ 50 - i * 1.7, 50 - i * 1.7, 50 - i * 1.7, 255 },
			wm.rect
		)
	end
	Draw:OutlinedRect(false, wm.pos.x, wm.pos.y, wm.width, wm.height, { 0, 0, 0, 255 }, wm.rect)
	Draw:OutlinedRect(false, wm.pos.x - 1, wm.pos.y - 1, wm.width + 2, wm.height + 2, { 0, 0, 0, 255 * 0.4 }, wm.rect)
	Draw:OutlinedText(
		fulltext,
		2,
		false,
		wm.pos.x + 5,
		wm.pos.y + 3,
		13,
		false,
		{ 255, 255, 255, 255 },
		{ 0, 0, 0, 255 },
		wm.text
	)
end

--ANCHOR watermak
for k, v in pairs(menu.watermark.rect) do
	v.Visible = true
end

menu.watermark.text[1].Visible = true

local textbox = menu.options["Settings"]["Configuration"]["ConfigName"]
local relconfigs = GetConfigs()
textbox[1] = relconfigs[menu.options["Settings"]["Configuration"]["Configs"][1]]
textbox[4].Text = textbox[1]

menu.load_time = math.floor((tick() - loadstart) * 1000)
CreateNotification(string.format("Done loading the " .. menu.game .. " cheat. (%d ms)", menu.load_time))
CreateNotification("Press DELETE to open and close the menu!")

loadingthing.Visible = false -- i do it this way because otherwise it would fuck up the Draw:UnRender function, it doesnt cause any lag sooooo
if not menu.open then
	menu.fading = true
	menu.fadestart = tick()
end

menu.Initialize = true -- let me freeeeee
-- not lettin u free asshole bitch
-- i meant the program memory, alan...............  fuckyouAlan_iHateYOU from v1
-- im changing all the var names that had typos by me back to what they were now because of this.... enjoy hieght....
-- wutw
