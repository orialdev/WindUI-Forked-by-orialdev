# WindUI (Forked)

A powerful and modern Roblox UI library featuring tabs, sections, key systems, configuration saving, and theming.

---

## Installation

Load the library into your script:

```lua
local WindUI = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/orialdev/WindUI-Forked-by-orialdev/refs/heads/main/WindUI%20Forked"
))()
```

---

## Key System

WindUI includes a built-in **Key System** with support for popular whitelisting services.
If a `Folder` is defined in the window configuration, keys are automatically saved and loaded.

### Supported Services

* `platoboost`
* `pandadevelopment`
* `luarmor`

```lua
KeySystem = {
    Title = "Project Alpha",
    Key = {"AdminKey1", "TestKey2"}, -- Table of keys or a single string
    SaveKey = true, -- Saves to WindUI/FolderName/Key.key
    API = {
        {
            Type = "platoboost",
            ServiceId = "your_id",
            Secret = "your_secret"
        }
    }
}
```

---

## Window Creation

The main container for your interface.

```lua
local Window = WindUI:CreateWindow({
    Title = "sexy hub",
    Icon = "door-open", -- lucide icon
    Author = "by orialdev",
    Folder = "MySuperHub",
    
    -- ↓ This all is Optional. You can remove it.
    Size = UDim2.fromOffset(580, 460),
    MinSize = Vector2.new(560, 350),
    MaxSize = Vector2.new(850, 560),
    Transparent = true,
    Theme = "Dark",
    Resizable = true,
    SideBarWidth = 200,
    BackgroundImageTransparency = 0.42,
    HideSearchBar = true,
    ScrollBarEnabled = false,
    
    -- ↓ Optional. You can remove it.
    --[[ You can set 'rbxassetid://' or video to Background.
        'rbxassetid://':
            Background = "rbxassetid://", -- rbxassetid
        Video:
            Background = "video:YOUR-RAW-LINK-TO-VIDEO.webm", -- video 
    --]]
    
    -- ↓ Optional. You can remove it.
    User = {
        Enabled = true,
        Anonymous = true,
        Callback = function()
            print("clicked")
        end,
    },
    
    --       remove this all, 
    -- !  ↓  if you DON'T need the key system
    KeySystem = { 
        -- ↓ Optional. You can remove it.
        Key = { "1234", "5678" },
        
        Note = "Example Key System.",
        
        -- ↓ Optional. You can remove it.
        Thumbnail = {
            Image = "rbxassetid://",
            Title = "Thumbnail",
        },
        
        -- ↓ Optional. You can remove it.
        URL = "YOUR LINK TO GET KEY (Discord, Linkvertise, Pastebin, etc.)",
        
        -- ↓ Optional. You can remove it.
        SaveKey = false, -- automatically save and load the key.
        
        -- ↓ Optional. You can remove it.
        -- API = {} ← Services. Read about it below ↓
    },
})
```

---

## Tabs & Navigation

Tabs organize your UI into pages in the sidebar.

```lua
local Tab = Window:Tab({
    Title = "General",
    Icon = "house",
    Visible = true
})
```

### Tab Methods

```lua
Tab:SetBadge("New")
Tab:Lock()
Tab:Unlock()
Tab:Select()
Tab:ScrollToTheElement(1)
```

---

## Organization Containers

### Section

A collapsible container for grouping elements.

```lua
local Section = Tab:Section({
    Title = "Movement",
    Opened = true
})
```

### MultiSection

Tabbed sub-navigation inside a section.

```lua
local Multi = Tab:MultiSection({
    Title = "Visuals",
    Sections = {"World", "Players", "Self"}
})

Multi.World:Button({
    Title = "Fullbright"
})
```

### Group

Arranges elements horizontally in a grid.

```lua
local Group = Tab:Group()

Group:Button({ Title = "Button 1" })
Group:Button({ Title = "Button 2" })
```

---

## UI Components

### Button

```lua
Tab:Button({
    Title = "Reset Character",
    Desc = "Force kills your character",
    Icon = "rotate-ccw",
    Callback = function()
        -- code here
    end
})
```

### Toggle

```lua
Tab:Toggle({
    Title = "Auto Farm",
    Value = false,
    Flag = "AutoFarmToggle",
    Callback = function(state)
        print(state)
    end
})
```

### Slider

```lua
Tab:Slider({
    Title = "WalkSpeed",
    Value = { Min = 16, Max = 150, Default = 16 },
    Step = 1,
    IsTooltip = true,
    Flag = "WalkspeedSlider",
    Callback = function(value)
        -- code here
    end
})
```

### Dropdown

```lua
Tab:Dropdown({
    Title = "Aimbot Target",
    Values = {"Head", "Torso", "Random"},
    Multi = false,
    Value = "Head",
    Callback = function(selected)
        -- code here
    end
})
```

---

## Keybinds & Advanced Input

### Keybind

```lua
Tab:Keybind({
    Title = "UI Toggle",
    Value = "RightShift",
    Callback = function()
        Window:Toggle()
    end
})
```

### ToggleKeybind

```lua
Tab:ToggleKeybind({
    Title = "Auto Parry",
    Value = false,
    Key = "V",
    Callback = function(state)
        print(state)
    end
})
```

### ButtonKeybind

```lua
local action = Tab:ButtonKeybind({
    Title = "Emergency Logout",
    Desc = "Instantly leave the game",
    Icon = "log-out",
    Key = "L",
    Callback = function(sourceKey)
        print("Action fired via " .. sourceKey)
    end
})

action:SetKey("M")
```

---

## Utility Features

| Feature       | Usage                                                         |
| ------------- | ------------------------------------------------------------- |
| Notification  | `WindUI:Notify({Title = "Notice", Content = "Script Ready"})` |
| Popup         | `WindUI:Popup({Title = "Alert", Content = "Message"})`        |
| Dialog        | `Window:Dialog({Title = "Quit", Content = "Are you sure?"})`  |
| Colorpicker   | `Tab:Colorpicker({Title = "Chams Color"})`                    |
| Input         | `Tab:Input({Title = "Search"})`                               |
| Code Block    | `Tab:Code({Code = "-- Code Here"})`                           |
| Image         | `Tab:Image({Image = "rbxassetid://123"})`                     |
| Paragraph     | `Tab:Paragraph({Title = "Rules", Desc = "Do not use..."})`    |
| Divider/Space | `Tab:Divider()` / `Tab:Space(10)`                             |

---

## Theme System

Themes can be changed live at runtime.

```lua
WindUI:SetTheme("Dark")
WindUI:SetTheme("Light")
WindUI:SetTheme("Midnight")
WindUI:SetTheme("MonokaiPro")
WindUI:SetTheme("Rainbow") -- Animated gradients
```

---

## Configuration Manager

Automatically save and load UI state using component flags.

```lua
-- Save configuration
Window.ConfigManager:Config("settings"):Save()

-- Load configuration
Window.ConfigManager:Config("settings"):Load()
```

---

## Icons

This library uses **Lucide Icons**.
Browse icons at **[https://lucide.dev](https://lucide.dev)** and use their lowercase, hyphenated names:

```
mouse-pointer
shield-check
trash-2
```
