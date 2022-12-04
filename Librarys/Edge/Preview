getgenv().color_schemes = {
	white_blue = { -- Original
		dark_color = Color3.fromRGB(0, 78, 152),
		dark_hover_color = Color3.fromRGB(0, 65, 125),
		background_color = Color3.fromRGB(235, 235, 235),
		section_background_color = Color3.fromRGB(192, 192, 192),
		misc_elements_color = Color3.fromRGB(235, 235, 235),
		elements_color = Color3.fromRGB(58, 110, 165),
		elements_hover_color = Color3.fromRGB(49, 94, 139),
		enabled_color = Color3.fromRGB(255, 103, 0),
		enabled_hover_color = Color3.fromRGB(221, 88, 0),
		scroll_bar_color = Color3.fromRGB(0, 0, 0)
	},
	
	custom = { -- Your color scheme
		dark_color = Color3.fromRGB(0, 78, 152),
		dark_hover_color = Color3.fromRGB(0, 65, 125),
		background_color = Color3.fromRGB(235, 235, 235),
		section_background_color = Color3.fromRGB(192, 192, 192),
		misc_elements_color = Color3.fromRGB(235, 235, 235),
		elements_color = Color3.fromRGB(58, 110, 165),
		elements_hover_color = Color3.fromRGB(49, 94, 139),
		enabled_color = Color3.fromRGB(255, 103, 0),
		enabled_hover_color = Color3.fromRGB(221, 88, 0),
		scroll_bar_color = Color3.fromRGB(0, 0, 0)
	}
}

getgenv().color_scheme = getgenv().color_schemes.custom


local window = loadstring(game:HttpGet("https://raw.githubusercontent.com/deadmopose/Edge-ui-library/main/script.lua"))()

local tab = window.new_tab("Main")

local section = tab.new_section("Player")

section.new_button("button", function()
	-- Something
end)

section.new_toggle("toggle", function(state)
	-- Something
end)

section.new_text_box("text_box", function(text)
	-- Something
end)

section.new_key_bind("key_bind", "A", function(key)
	-- Something
end)

section.new_slider("key_bind", 1, 100, function(value)
	-- Something
end)

section.new_dropdown("dropdown", {1, 2, 3}, function(value)
	-- Something
end)

section.new_dropdown2("dropdown2", {1, 2, 3}, function(value)
	-- Something
end)

local function get_table()
    return {1, 2, 3}
end

section.new_dropdown("dropdown", get_table, function(value) -- Put function that returns a table instead of a table
	-- Something
end)

