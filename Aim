-- Thats is the fucking pollolock bitch
-- Owner: BlackPollo

-- Show "By BlackPollo" neon splash before anything else
local players = game:GetService("Players")
local localPlayer = players.LocalPlayer
local splashGui = Instance.new("ScreenGui")
splashGui.Name = "PolloLockSplash"
splashGui.IgnoreGuiInset = true
splashGui.ResetOnSpawn = false
splashGui.Parent = localPlayer:WaitForChild("PlayerGui")

local neonColor = Color3.fromRGB(0,255,255)

local splashLabel = Instance.new("TextLabel", splashGui)
splashLabel.Size = UDim2.new(0.5, 0, 0, 60)
splashLabel.Position = UDim2.new(0.25, 0, 0.44, 0)
splashLabel.BackgroundTransparency = 1
splashLabel.Text = "By BlackPollo"
splashLabel.TextColor3 = neonColor
splashLabel.Font = Enum.Font.GothamSemibold
splashLabel.TextSize = 40
splashLabel.TextStrokeTransparency = 0.2
splashLabel.ZIndex = 100

-- Neon color cycling effect for the splash
local runService = game:GetService("RunService")
local splashAlive = true
local splashConn
splashConn = runService.RenderStepped:Connect(function()
    if splashAlive then
        local t = tick()*2
        splashLabel.TextColor3 = Color3.fromHSV((t%5)/5,1,1)
    else
        splashConn:Disconnect()
    end
end)

task.wait(3)
splashAlive = false
splashGui:Destroy()

-- Initial settings
local fovSize = 100
local neonTextColor = Color3.fromRGB(0,255,255)
local aimlockKey = Enum.KeyCode.E

local colorPresets = {
    {name="Rainbow", func=function() local t=tick()*2 return Color3.fromHSV((t%5)/5,1,1) end},
    {name="Cyan",    func=function() return Color3.fromRGB(0,255,255) end},
    {name="Pink",    func=function() return Color3.fromRGB(255,0,120) end},
    {name="Green",   func=function() return Color3.fromRGB(0,255,0) end},
    {name="Orange",  func=function() return Color3.fromRGB(255,140,0) end},
    {name="White",   func=function() return Color3.fromRGB(255,255,255) end},
    {name="Blue",    func=function() return Color3.fromRGB(80,140,255) end},
    {name="Yellow",  func=function() return Color3.fromRGB(255,255,0) end},
}
local colorPresetIndex = 1

local function getCurrentColor()
    return colorPresets[colorPresetIndex].func()
end

local uis = game:GetService("UserInputService")
local localPlayer = players.LocalPlayer
local camera = workspace.CurrentCamera

local aimlockEnabled = false
local target = nil

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "PolloLockUI"
screenGui.IgnoreGuiInset = true
screenGui.ResetOnSpawn = false
screenGui.Parent = localPlayer:WaitForChild("PlayerGui")

local notice = Instance.new("TextLabel", screenGui)
notice.Size = UDim2.new(0.5, 0, 0, 35)
notice.Position = UDim2.new(0.25, 0, 0.04, 0)
notice.BackgroundTransparency = 0.3
notice.BackgroundColor3 = Color3.fromRGB(25,25,25)
notice.Text = "To activate aimlock, click or hold on the FOV"
notice.TextColor3 = neonTextColor
notice.Font = Enum.Font.GothamSemibold
notice.TextSize = 17
notice.TextStrokeTransparency = 0.3
notice.ZIndex = 10
notice.Visible = true
game:GetService("Debris"):AddItem(notice, 6)

local fovCircle = Instance.new("TextButton", screenGui)
fovCircle.AnchorPoint = Vector2.new(0.5, 0.5)
fovCircle.Size = UDim2.new(0, fovSize * 2, 0, fovSize * 2)
fovCircle.Position = UDim2.new(0.5, 0, 0.5, 0)
fovCircle.BackgroundTransparency = 0.7
fovCircle.BorderSizePixel = 0
fovCircle.Name = "FOVCircle"
fovCircle.Text = ""

local uiStroke = Instance.new("UIStroke", fovCircle)
uiStroke.Thickness = 2
uiStroke.Transparency = 0.2

local uicorner = Instance.new("UICorner", fovCircle)
uicorner.CornerRadius = UDim.new(1, 0)

local title = Instance.new("TextLabel", screenGui)
title.Text = "PolloLock"
title.Size = UDim2.new(0, 120, 0, 15)
title.Position = UDim2.new(0.5, -60, 0.5, fovSize + 10)
title.BackgroundTransparency = 1
title.TextColor3 = neonTextColor
title.Font = Enum.Font.GothamSemibold
title.TextSize = 12
title.TextStrokeTransparency = 0.5
title.ZIndex = 3

local resetBtn = Instance.new("TextButton", screenGui)
resetBtn.Size = UDim2.new(0, 100, 0, 25)
resetBtn.Position = UDim2.new(0.5, -50, 0.5, fovSize + 40)
resetBtn.BackgroundColor3 = neonTextColor
resetBtn.TextColor3 = Color3.new(0,0,0)
resetBtn.Text = "Reset FOV"
resetBtn.Font = Enum.Font.GothamSemibold
resetBtn.TextSize = 14
resetBtn.BackgroundTransparency = 0.2
resetBtn.AutoButtonColor = true
resetBtn.ZIndex = 4

-- FOV Size Customization UI
local fovSizeLabel = Instance.new("TextLabel", screenGui)
fovSizeLabel.Size = UDim2.new(0, 120, 0, 22)
fovSizeLabel.Position = UDim2.new(0.5, -60, 0.5, fovSize + 68)
fovSizeLabel.BackgroundTransparency = 0.4
fovSizeLabel.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
fovSizeLabel.Text = "FOV Size: " .. tostring(fovSize)
fovSizeLabel.TextColor3 = neonTextColor
fovSizeLabel.Font = Enum.Font.GothamSemibold
fovSizeLabel.TextSize = 14
fovSizeLabel.TextStrokeTransparency = 0.3
fovSizeLabel.ZIndex = 5

local fovMinusBtn = Instance.new("TextButton", screenGui)
fovMinusBtn.Size = UDim2.new(0, 32, 0, 22)
fovMinusBtn.Position = UDim2.new(0.5, -60-36, 0.5, fovSize + 68)
fovMinusBtn.BackgroundColor3 = neonTextColor
fovMinusBtn.TextColor3 = Color3.new(0,0,0)
fovMinusBtn.Text = "-"
fovMinusBtn.Font = Enum.Font.GothamSemibold
fovMinusBtn.TextSize = 18
fovMinusBtn.BackgroundTransparency = 0.17
fovMinusBtn.AutoButtonColor = true
fovMinusBtn.ZIndex = 6

local fovPlusBtn = Instance.new("TextButton", screenGui)
fovPlusBtn.Size = UDim2.new(0, 32, 0, 22)
fovPlusBtn.Position = UDim2.new(0.5, 60+4, 0.5, fovSize + 68)
fovPlusBtn.BackgroundColor3 = neonTextColor
fovPlusBtn.TextColor3 = Color3.new(0,0,0)
fovPlusBtn.Text = "+"
fovPlusBtn.Font = Enum.Font.GothamSemibold
fovPlusBtn.TextSize = 18
fovPlusBtn.BackgroundTransparency = 0.17
fovPlusBtn.AutoButtonColor = true
fovPlusBtn.ZIndex = 6

local toggleUIBtn = Instance.new("TextButton", screenGui)
toggleUIBtn.Size = UDim2.new(0, 42, 0, 22)
toggleUIBtn.Position = UDim2.new(0.5, 60, 0.5, fovSize + 10)
toggleUIBtn.BackgroundColor3 = neonTextColor
toggleUIBtn.TextColor3 = Color3.new(0,0,0)
toggleUIBtn.Text = "UI"
toggleUIBtn.Font = Enum.Font.GothamSemibold
toggleUIBtn.TextSize = 13
toggleUIBtn.BackgroundTransparency = 0.16
toggleUIBtn.AutoButtonColor = true
toggleUIBtn.ZIndex = 5

local colorBtn = Instance.new("TextButton", screenGui)
colorBtn.Size = UDim2.new(0, 120, 0, 38)
colorBtn.Position = UDim2.new(0, 25, 0.5, 40)
colorBtn.AnchorPoint = Vector2.new(0, 0)
colorBtn.BackgroundColor3 = neonTextColor
colorBtn.TextColor3 = Color3.new(0,0,0)
colorBtn.Text = "Color changer"
colorBtn.Font = Enum.Font.GothamSemibold
colorBtn.TextSize = 16
colorBtn.BackgroundTransparency = 0.12
colorBtn.AutoButtonColor = true
colorBtn.ZIndex = 6
local colorBtnStroke = Instance.new("UIStroke", colorBtn)
colorBtnStroke.Color = neonTextColor
colorBtnStroke.Thickness = 3
colorBtnStroke.Transparency = 0.1

-- ESP Button and variables
local espEnabled = false
local espFolder = Instance.new("Folder", screenGui)
espFolder.Name = "PolloLockESP"
local espBtn = Instance.new("TextButton", screenGui)
espBtn.Size = UDim2.new(0, 80, 0, 25)
espBtn.Position = UDim2.new(0.5, -40, 0.5, fovSize + 100)
espBtn.BackgroundColor3 = neonTextColor
espBtn.TextColor3 = Color3.new(0,0,0)
espBtn.Text = "ESP: OFF"
espBtn.Font = Enum.Font.GothamSemibold
espBtn.TextSize = 14
espBtn.BackgroundTransparency = 0.22
espBtn.AutoButtonColor = true
espBtn.ZIndex = 6
espBtn.Visible = true

local function updateESPBtnPos()
    local pos = fovCircle.Position
    espBtn.Position = UDim2.new(
        pos.X.Scale, pos.X.Offset - 40,
        pos.Y.Scale, pos.Y.Offset + fovSize + 100
    )
end
local function updateESPBtnColor(c)
    espBtn.BackgroundColor3 = c
end

espBtn.MouseButton1Click:Connect(function()
    espEnabled = not espEnabled
    espBtn.Text = espEnabled and "ESP: ON" or "ESP: OFF"
    if not espEnabled then
        for _,v in ipairs(espFolder:GetChildren()) do
            v:Destroy()
        end
    end
end)

local colorDragging = false
local colorDragStart, colorBtnStartPos

local function beginColorDrag(input)
    colorDragging = true
    colorDragStart = input.Position
    colorBtnStartPos = colorBtn.Position
    input.Changed:Connect(function()
        if input.UserInputState == Enum.UserInputState.End then
            colorDragging = false
        end
    end)
end

colorBtn.MouseButton1Down:Connect(function(input)
    beginColorDrag(input)
end)

colorBtn.TouchLongPress:Connect(function(input)
    beginColorDrag(input)
end)

colorBtn.InputChanged:Connect(function(input)
    if colorDragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local delta = input.Position - colorDragStart
        colorBtn.Position = colorBtnStartPos + UDim2.new(0, delta.X, 0, delta.Y)
    end
end)

local function isInFOV(pos)
    local screenPos, onScreen = camera:WorldToViewportPoint(pos)
    if not onScreen then return false end
    local center = Vector2.new(
        fovCircle.AbsolutePosition.X + fovCircle.AbsoluteSize.X/2,
        fovCircle.AbsolutePosition.Y + fovCircle.AbsoluteSize.Y/2
    )
    local dist = (Vector2.new(screenPos.X, screenPos.Y) - center).Magnitude
    return dist <= fovSize
end

local function wallCheck(target)
    if not target or not target.Character or not target.Character:FindFirstChild("Head") then return false end
    local origin = camera.CFrame.Position
    local head = target.Character.Head.Position
    local direction = head - origin
    local rayParams = RaycastParams.new()
    rayParams.FilterType = Enum.RaycastFilterType.Blacklist
    rayParams.FilterDescendantsInstances = {localPlayer.Character, camera}
    rayParams.IgnoreWater = true

    local result = workspace:Raycast(origin, direction, rayParams)
    if result then
        if not result.Instance:IsDescendantOf(target.Character) then
            return false
        end
    end
    return true
end

local function getClosestTarget()
    local closest, shortest = nil, math.huge
    for _,plr in ipairs(players:GetPlayers()) do
        if plr ~= localPlayer 
           and plr.Character 
           and plr.Character:FindFirstChild("Head") 
           and plr.Character:FindFirstChild("Humanoid") 
           and plr.Character.Humanoid.Health > 0 then
            local head = plr.Character.Head
            if isInFOV(head.Position) and wallCheck(plr) then
                local screenPos = camera:WorldToViewportPoint(head.Position)
                local center = Vector2.new(
                    fovCircle.AbsolutePosition.X + fovCircle.AbsoluteSize.X/2,
                    fovCircle.AbsolutePosition.Y + fovCircle.AbsoluteSize.Y/2
                )
                local dist = (Vector2.new(screenPos.X, screenPos.Y) - center).Magnitude
                if dist < shortest then
                    shortest = dist
                    closest = plr
                end
            end
        end
    end
    return closest
end

local function aimAt(target)
    if not target or not target.Character or not target.Character:FindFirstChild("Head") then return end
    local head = target.Character.Head
    camera.CFrame = CFrame.new(camera.CFrame.Position, head.Position)
end

colorBtn.MouseButton1Click:Connect(function()
    colorPresetIndex = colorPresetIndex % #colorPresets + 1
    local preset = colorPresets[colorPresetIndex]
    colorBtn.Text = "Color: " .. preset.name
end)
colorBtn.TouchTap:Connect(function()
    colorPresetIndex = colorPresetIndex % #colorPresets + 1
    local preset = colorPresets[colorPresetIndex]
    colorBtn.Text = "Color: " .. preset.name
end)

-- FOV Size Customization Logic
local function updateFovUI()
    fovCircle.Size = UDim2.new(0, fovSize * 2, 0, fovSize * 2)
    title.Position = UDim2.new(0.5, -60, 0.5, fovSize + 10)
    resetBtn.Position = UDim2.new(0.5, -50, 0.5, fovSize + 40)
    toggleUIBtn.Position = UDim2.new(0.5, 60, 0.5, fovSize + 10)
    espBtn.Position = UDim2.new(0.5, -40, 0.5, fovSize + 100)
    fovSizeLabel.Position = UDim2.new(0.5, -60, 0.5, fovSize + 68)
    fovMinusBtn.Position = UDim2.new(0.5, -60-36, 0.5, fovSize + 68)
    fovPlusBtn.Position = UDim2.new(0.5, 60+4, 0.5, fovSize + 68)
    fovSizeLabel.Text = "FOV Size: " .. tostring(fovSize)
end

fovMinusBtn.MouseButton1Click:Connect(function()
    fovSize = math.max(20, fovSize - 10)
    updateFovUI()
end)

fovPlusBtn.MouseButton1Click:Connect(function()
    fovSize = math.min(500, fovSize + 10)
    updateFovUI()
end)

local function updateUIPositions()
    updateFovUI()
end

resetBtn.MouseButton1Click:Connect(function()
    fovCircle.Position = UDim2.new(0.5, 0, 0.5, 0)
    fovSize = 100
    updateFovUI()
end)

runService.RenderStepped:Connect(function()
    local c = getCurrentColor()
    fovCircle.BackgroundColor3 = c
    uiStroke.Color = c
    resetBtn.BackgroundColor3 = c
    toggleUIBtn.BackgroundColor3 = c
    colorBtn.BackgroundColor3 = c
    colorBtnStroke.Color = c
    updateESPBtnColor(c)
    fovMinusBtn.BackgroundColor3 = c
    fovPlusBtn.BackgroundColor3 = c
    fovSizeLabel.TextColor3 = c

    -- ESP for all players except yourself (ESP does NOT use wallCheck)
    if espEnabled then
        for _,v in ipairs(espFolder:GetChildren()) do
            v:Destroy()
        end
        for _,plr in ipairs(players:GetPlayers()) do
            if plr ~= localPlayer 
                and plr.Character 
                and plr.Character:FindFirstChild("Head") 
                and plr.Character:FindFirstChild("Humanoid") 
                and plr.Character.Humanoid.Health > 0 then
                local head = plr.Character.Head
                local headScreen, onScreen = camera:WorldToViewportPoint(head.Position)
                if onScreen then
                    local nameLbl = Instance.new("TextLabel", espFolder)
                    nameLbl.Size = UDim2.new(0, 100, 0, 18)
                    nameLbl.Position = UDim2.new(0, headScreen.X - 50, 0, headScreen.Y - 30)
                    nameLbl.BackgroundTransparency = 1
                    nameLbl.Text = plr.Name
                    nameLbl.TextColor3 = c
                    nameLbl.Font = Enum.Font.Gotham
                    nameLbl.TextSize = 14
                    nameLbl.TextStrokeTransparency = 0.2
                    nameLbl.ZIndex = 99

                    local tracer = Instance.new("Frame", espFolder)
                    tracer.BackgroundTransparency = 1
                    tracer.Size = UDim2.new(1,0,1,0)
                    tracer.ZIndex = 98

                    local cx, cy = camera.ViewportSize.X/2, camera.ViewportSize.Y/2
                    local dx, dy = headScreen.X - cx, headScreen.Y - cy
                    local dist = math.sqrt(dx*dx + dy*dy)
                    local angle = math.deg(math.atan2(dy, dx))
                    
                    local line = Instance.new("Frame", tracer)
                    line.BackgroundColor3 = c
                    line.BorderSizePixel = 0
                    line.AnchorPoint = Vector2.new(0, 0.5)
                    line.Position = UDim2.new(0, cx, 0, cy)
                    line.Size = UDim2.new(0, dist, 0, 2)
                    line.Rotation = angle
                    line.ZIndex = 98
                    line.BackgroundTransparency = 0.2
                end
            end
        end
    else
        for _,v in ipairs(espFolder:GetChildren()) do
            v:Destroy()
        end
    end

    if aimlockEnabled then
        target = getClosestTarget()
        if target then
            aimAt(target)
            title.Text = "PolloLock: " .. target.Name
            title.TextColor3 = Color3.fromRGB(255,0,100)
        else
            title.Text = "PolloLock (No target)"
            title.TextColor3 = c
        end
    else
        title.Text = "PolloLock"
        title.TextColor3 = c
    end
end)

local function isPointInFOVScreen(pt)
    local center = Vector2.new(
        fovCircle.AbsolutePosition.X + fovCircle.AbsoluteSize.X/2,
        fovCircle.AbsolutePosition.Y + fovCircle.AbsoluteSize.Y/2
    )
    local dist = (pt - center).Magnitude
    return dist <= fovSize
end

local function toggleAimlock()
    aimlockEnabled = not aimlockEnabled
end

fovCircle.MouseButton1Click:Connect(toggleAimlock)
fovCircle.TouchTap:Connect(toggleAimlock)

uis.InputBegan:Connect(function(input, processed)
    if processed then return end
    if not screenGui.Enabled then return end

    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        local loc
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            loc = uis:GetMouseLocation()
        elseif input.UserInputType == Enum.UserInputType.Touch then
            loc = input.Position
        end
        if loc then
            if isPointInFOVScreen(Vector2.new(loc.X, loc.Y)) then
                toggleAimlock()
            end
        end
    end
end)

toggleUIBtn.MouseButton1Click:Connect(function()
    local visible = not resetBtn.Visible
    resetBtn.Visible = visible
    colorBtn.Visible = visible
    espBtn.Visible = visible
    fovSizeLabel.Visible = visible
    fovMinusBtn.Visible = visible
    fovPlusBtn.Visible = visible
end)
