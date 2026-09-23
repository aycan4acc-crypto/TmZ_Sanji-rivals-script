-- TmZ_Sanji | Rivals Loader
-- Key: 6767

local Players    = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local plr        = Players.LocalPlayer
local playerGui  = plr:WaitForChild("PlayerGui")

local CORRECT_KEY = "6767"
local SCRIPT_URL  = "https://raw.githubusercontent.com/aycan4acc-crypto/TmZ_Sanji-rivals-script/main/my%20Script.txt"

-- ── GUI ───────────────────────────────────────────────────────────────────────
local gui = Instance.new("ScreenGui")
gui.Name = "TmZ_KeySystem"
gui.ResetOnSpawn = false
gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
gui.Parent = playerGui

local blur = Instance.new("Frame")
blur.Size = UDim2.new(1,0,1,0)
blur.BackgroundColor3 = Color3.fromRGB(0,0,0)
blur.BackgroundTransparency = 0.4
blur.BorderSizePixel = 0
blur.Parent = gui

local win = Instance.new("Frame")
win.Size = UDim2.new(0,320,0,220)
win.Position = UDim2.new(0.5,-160,0.5,-110)
win.BackgroundColor3 = Color3.fromRGB(8,8,14)
win.BorderSizePixel = 0
win.Parent = gui
Instance.new("UICorner",win).CornerRadius = UDim.new(0,12)

local stroke = Instance.new("UIStroke")
stroke.Color = Color3.fromRGB(180,30,30)
stroke.Thickness = 1.5
stroke.Parent = win

-- Header
local header = Instance.new("Frame")
header.Size = UDim2.new(1,0,0,55)
header.BackgroundColor3 = Color3.fromRGB(14,14,22)
header.BorderSizePixel = 0
header.Parent = win
Instance.new("UICorner",header).CornerRadius = UDim.new(0,12)

local headerLine = Instance.new("Frame")
headerLine.Size = UDim2.new(1,0,0,2)
headerLine.Position = UDim2.new(0,0,1,-2)
headerLine.BackgroundColor3 = Color3.fromRGB(220,30,30)
headerLine.BorderSizePixel = 0
headerLine.Parent = header

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1,0,0.55,0)
title.Position = UDim2.new(0,14,0.08,0)
title.BackgroundTransparency = 1
title.Text = "TmZ_Sanji"
title.TextColor3 = Color3.fromRGB(220,30,30)
title.Font = Enum.Font.GothamBold
title.TextSize = 18
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = header

local sub = Instance.new("TextLabel")
sub.Size = UDim2.new(1,0,0.35,0)
sub.Position = UDim2.new(0,14,0.62,0)
sub.BackgroundTransparency = 1
sub.Text = "Rivals Script • Key System"
sub.TextColor3 = Color3.fromRGB(100,100,130)
sub.Font = Enum.Font.Gotham
sub.TextSize = 10
sub.TextXAlignment = Enum.TextXAlignment.Left
sub.Parent = header

-- Key Label
local keyLabel = Instance.new("TextLabel")
keyLabel.Size = UDim2.new(1,-28,0,20)
keyLabel.Position = UDim2.new(0,14,0,70)
keyLabel.BackgroundTransparency = 1
keyLabel.Text = "Key eingeben:"
keyLabel.TextColor3 = Color3.fromRGB(180,180,200)
keyLabel.Font = Enum.Font.GothamBold
keyLabel.TextSize = 12
keyLabel.TextXAlignment = Enum.TextXAlignment.Left
keyLabel.Parent = win

-- Input Box
local inputBox = Instance.new("TextBox")
inputBox.Size = UDim2.new(1,-28,0,38)
inputBox.Position = UDim2.new(0,14,0,95)
inputBox.BackgroundColor3 = Color3.fromRGB(16,16,26)
inputBox.BorderSizePixel = 0
inputBox.Text = ""
inputBox.PlaceholderText = "Key hier eingeben..."
inputBox.TextColor3 = Color3.fromRGB(255,255,255)
inputBox.PlaceholderColor3 = Color3.fromRGB(80,80,100)
inputBox.Font = Enum.Font.GothamBold
inputBox.TextSize = 14
inputBox.ClearTextOnFocus = false
inputBox.Parent = win
Instance.new("UICorner",inputBox).CornerRadius = UDim.new(0,8)

local inputStroke = Instance.new("UIStroke")
inputStroke.Color = Color3.fromRGB(50,50,75)
inputStroke.Thickness = 1.5
inputStroke.Parent = inputBox

-- Status Label
local statusLabel = Instance.new("TextLabel")
statusLabel.Size = UDim2.new(1,-28,0,16)
statusLabel.Position = UDim2.new(0,14,0,138)
statusLabel.BackgroundTransparency = 1
statusLabel.Text = ""
statusLabel.TextColor3 = Color3.fromRGB(220,30,30)
statusLabel.Font = Enum.Font.Gotham
statusLabel.TextSize = 11
statusLabel.TextXAlignment = Enum.TextXAlignment.Left
statusLabel.Parent = win

-- Confirm Button
local btn = Instance.new("TextButton")
btn.Size = UDim2.new(1,-28,0,36)
btn.Position = UDim2.new(0,14,0,160)
btn.BackgroundColor3 = Color3.fromRGB(220,30,30)
btn.Text = "BESTÄTIGEN"
btn.TextColor3 = Color3.new(1,1,1)
btn.Font = Enum.Font.GothamBold
btn.TextSize = 13
btn.BorderSizePixel = 0
btn.Parent = win
Instance.new("UICorner",btn).CornerRadius = UDim.new(0,8)

-- ── LOGIK ─────────────────────────────────────────────────────────────────────
local function wrongKey()
    statusLabel.Text = "❌ Falscher Key!"
    statusLabel.TextColor3 = Color3.fromRGB(220,30,30)
    inputStroke.Color = Color3.fromRGB(220,30,30)
    inputBox.Text = ""
    task.delay(1.5, function()
        inputStroke.Color = Color3.fromRGB(50,50,75)
        statusLabel.Text = ""
    end)
end

local function correctKey()
    statusLabel.Text = "✔ Key korrekt — lade Script..."
    statusLabel.TextColor3 = Color3.fromRGB(40,220,80)
    inputStroke.Color = Color3.fromRGB(40,220,80)
    btn.BackgroundColor3 = Color3.fromRGB(30,160,60)
    task.delay(1, function()
        gui:Destroy()
        local ok, err = pcall(function()
            loadstring(game:HttpGet(SCRIPT_URL))()
        end)
        if not ok then
            warn("[TmZ_Sanji] Script konnte nicht geladen werden: "..tostring(err))
        end
    end)
end

btn.MouseButton1Click:Connect(function()
    local entered = inputBox.Text
    if entered == CORRECT_KEY then
        correctKey()
    else
        wrongKey()
    end
end)

inputBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        if inputBox.Text == CORRECT_KEY then
            correctKey()
        else
            wrongKey()
        end
    end
end)
