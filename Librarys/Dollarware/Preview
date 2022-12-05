-- Dollarware example script

-- Snag the ui loader function thingy (loadstring the link, but dont call it)
local uiLoader = loadstring(game:HttpGet('https://raw.githubusercontent.com/topitbopit/dollarware/main/library.lua'))
-- Because of the way the library loads, settings are handled on the loadstring call
local ui = uiLoader({
    rounding = false, -- Whether certain features get rounded 
    theme = 'cherry', -- The theme. Available themes are: cherry, orange, lemon, lime, raspberry, blueberry, grape, watermelon
    smoothDragging = false -- Smooth dragging
})

ui.autoDisableToggles = true -- All toggles will automatically be disabled when the ui is destroyed (window is closed)
-- so you don't have to manually handle everything. This defaults to true!

-- Make a window, which houses all the stuff for the gui
-- Technically multiple windows can be made, but there is no (and likely wont ever be) official support for them
-- since its a lot of work for such a minute use
local window = ui.newWindow({
    text = 'Dollarware demo', -- Title of window 
    resize = true, -- Ability to resize
    size = Vector2.new(550, 376), -- Window size, accepts UDim2s and Vector2s
    position = nil -- Custom position, defaults to roughly the bottom right corner
})

local menu = window:addMenu({
    text = 'menu 1' -- Title of menu
})
do 
    -- Menus have sections which house all the controls    
    local section = menu:addSection({
        text = 'section 1', -- Title of section
        side = 'auto', -- Side of the menu that the section is placed on. Defaults to 'auto', but can be 'left' or 'right'
        showMinButton = true, -- Ability to minimize this section. Defaults to true
    })
    
    do 
        section:addLabel({
            text = 'text' -- Self explanatory
        })
        
        local toggle = section:addToggle({
            text = 'toggle', 
            state = false -- Starting state of the toggle - doesn't automatically call the callback
        })
        
        toggle:bindToEvent('onToggle', function(newState) -- Call a function when toggled
            ui.notify({
                title = 'toggle',
                message = 'Toggle was toggled to ' .. tostring(newState),
                duration = 3
            })
        end)
        
        section:addButton({
            text = 'button (small)', 
            style = 'small' -- style of the button, can be 'large' or 'small'
        }):bindToEvent('onClick', function() -- Call a function when clicked
            ui.notify({
                title = 'button',
                message = 'The button got clicked!',
                duration = 3
            })
        end)
        
        section:addButton({
            text = 'button (large)', 
            style = 'large' -- style of the button, can be 'large' or 'small'
        }, function() -- you don't have to always use bindToEvent, just passing a callback normally works fine
            ui.notify({
                title = 'button',
                message = 'The large button got clicked!',
                duration = 3
            })
        end):setTooltip('this is a large button')
        
        local hotkey = section:addHotkey({
            text = 'hotkey'
        })
        hotkey:setHotkey(Enum.KeyCode.G)
        hotkey:setTooltip('This is a hotkey linked to the toggle!')
        hotkey:linkToControl(toggle)
    end
    
    local section = menu:addSection({
        text = 'section 2',
        side = 'right',
        showMinButton = false
    })
    do 
        section:addSlider({
            text = 'slider',
            min = 1,
            max = 150,
            step = 0.01,
            val = 50
        }, function(newValue) 
            print(newValue)
        end):setTooltip('Heres a slider!')
        
        section:addColorPicker({
            text = 'color picker',
            color = Color3.fromRGB(255, 0, 0)
        }, function(newColor) 
            print(newColor)
        end)
        
        section:addTextbox({
            text = 'textbox'
        }):bindToEvent('onFocusLost', function(text) 
            ui.notify({
                title = 'textbox',
                message = text,
                duration = 4
            })
        end)
    end
    
end

window:addMenu({
    text = 'menu 2'
})
