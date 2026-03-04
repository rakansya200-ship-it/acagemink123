local a=loadstring;local b=[[

local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")

local LocalPlayer = Players.LocalPlayer
local Character
local Humanoid
local RootPart
local InfiniteJumpEnabled = true

-- Configuration Variables
local JUMP_POWER = 75
local JUMP_COOLDOWN = 0.1
local LastJumpTime = 0

-- UI Creation
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "ACAGEMINK123_UI"
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

if gethui then
    ScreenGui.Parent = gethui()
elseif syn and syn.protect_gui then
    syn.protect_gui(ScreenGui)
    ScreenGui.Parent = game.CoreGui
else
    ScreenGui.Parent = game.CoreGui
end

-- Main Frame
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 350, 0, 400)
MainFrame.Position = UDim2.new(0.5, -175, 0.5, -200)
MainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
MainFrame.BackgroundTransparency = 0.1
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

-- Shadow Effect
local Shadow = Instance.new("ImageLabel")
Shadow.Name = "Shadow"
Shadow.Size = UDim2.new(1, 10, 1, 10)
Shadow.Position = UDim2.new(0, -5, 0, -5)
Shadow.BackgroundTransparency = 1
Shadow.Image = "rbxassetid://1316045217"
Shadow.ImageColor3 = Color3.fromRGB(0, 0, 0)
Shadow.ImageTransparency = 0.8
Shadow.ScaleType = Enum.ScaleType.Slice
Shadow.SliceCenter = Rect.new(10, 10, 118, 118)
Shadow.Parent = MainFrame

-- Title Bar
local TitleBar = Instance.new("Frame")
TitleBar.Name = "TitleBar"
TitleBar.Size = UDim2.new(1, 0, 0, 40)
TitleBar.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
TitleBar.BorderSizePixel = 0
TitleBar.Parent = MainFrame

local Title = Instance.new("TextLabel")
Title.Name = "Title"
Title.Size = UDim2.new(1, 0, 1, 0)
Title.BackgroundTransparency = 1
Title.Text = "🦘 ACAGEMINK123 INFINITE JUMP"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 18
Title.Font = Enum.Font.GothamBold
Title.Parent = TitleBar

-- Close Button
local CloseButton = Instance.new("TextButton")
CloseButton.Name = "CloseButton"
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -35, 0, 5)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 60, 60)
CloseButton.BorderSizePixel = 0
CloseButton.Text = "X"
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.TextSize = 16
CloseButton.Font = Enum.Font.GothamBold
CloseButton.Parent = TitleBar

CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- Status Indicator
local StatusFrame = Instance.new("Frame")
StatusFrame.Name = "StatusFrame"
StatusFrame.Size = UDim2.new(1, -40, 0, 50)
StatusFrame.Position = UDim2.new(0, 20, 0, 50)
StatusFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
StatusFrame.BorderSizePixel = 0
StatusFrame.Parent = MainFrame

local StatusLabel = Instance.new("TextLabel")
StatusLabel.Name = "StatusLabel"
StatusLabel.Size = UDim2.new(0, 100, 1, 0)
StatusLabel.BackgroundTransparency = 1
StatusLabel.Text = "STATUS:"
StatusLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
StatusLabel.TextSize = 14
StatusLabel.Font = Enum.Font.Gotham
StatusLabel.TextXAlignment = Enum.TextXAlignment.Left
StatusLabel.Parent = StatusFrame

local StatusValue = Instance.new("TextLabel")
StatusValue.Name = "StatusValue"
StatusValue.Size = UDim2.new(0, 150, 1, 0)
StatusValue.Position = UDim2.new(0, 110, 0, 0)
StatusValue.BackgroundTransparency = 1
StatusValue.Text = InfiniteJumpEnabled and "ENABLED 🟢" or "DISABLED 🔴"
StatusValue.TextColor3 = InfiniteJumpEnabled and Color3.fromRGB(0, 255, 0) or Color3.fromRGB(255, 50, 50)
StatusValue.TextSize = 14
StatusValue.Font = Enum.Font.GothamBold
StatusValue.TextXAlignment = Enum.TextXAlignment.Left
StatusValue.Parent = StatusFrame

-- Toggle Button
local ToggleButton = Instance.new("TextButton")
ToggleButton.Name = "ToggleButton"
ToggleButton.Size = UDim2.new(1, -40, 0, 40)
ToggleButton.Position = UDim2.new(0, 20, 0, 110)
ToggleButton.BackgroundColor3 = InfiniteJumpEnabled and Color3.fromRGB(50, 200, 50) or Color3.fromRGB(200, 50, 50)
ToggleButton.BorderSizePixel = 0
ToggleButton.Text = InfiniteJumpEnabled and "DISABLE INFINITE JUMP" or "ENABLE INFINITE JUMP"
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.TextSize = 16
ToggleButton.Font = Enum.Font.GothamBold
ToggleButton.Parent = MainFrame

-- Settings Section
local SettingsLabel = Instance.new("TextLabel")
SettingsLabel.Name = "SettingsLabel"
SettingsLabel.Size = UDim2.new(1, -40, 0, 30)
SettingsLabel.Position = UDim2.new(0, 20, 0, 170)
SettingsLabel.BackgroundTransparency = 1
SettingsLabel.Text = "SETTINGS"
SettingsLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
SettingsLabel.TextSize = 18
SettingsLabel.Font = Enum.Font.GothamBold
SettingsLabel.Parent = MainFrame

-- Jump Power Slider
local JumpPowerFrame = Instance.new("Frame")
JumpPowerFrame.Name = "JumpPowerFrame"
JumpPowerFrame.Size = UDim2.new(1, -40, 0, 60)
JumpPowerFrame.Position = UDim2.new(0, 20, 0, 210)
JumpPowerFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
JumpPowerFrame.BorderSizePixel = 0
JumpPowerFrame.Parent = MainFrame

local JumpPowerLabel = Instance.new("TextLabel")
JumpPowerLabel.Name = "JumpPowerLabel"
JumpPowerLabel.Size = UDim2.new(1, 0, 0, 20)
JumpPowerLabel.BackgroundTransparency = 1
JumpPowerLabel.Text = "JUMP POWER: " .. JUMP_POWER
JumpPowerLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
JumpPowerLabel.TextSize = 14
JumpPowerLabel.Font = Enum.Font.Gotham
JumpPowerLabel.Parent = JumpPowerFrame

local JumpPowerSlider = Instance.new("Frame")
JumpPowerSlider.Name = "JumpPowerSlider"
JumpPowerSlider.Size = UDim2.new(1, -20, 0, 10)
JumpPowerSlider.Position = UDim2.new(0, 10, 0, 30)
JumpPowerSlider.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
JumpPowerSlider.BorderSizePixel = 0
JumpPowerSlider.Parent = JumpPowerFrame

local JumpPowerFill = Instance.new("Frame")
JumpPowerFill.Name = "JumpPowerFill"
JumpPowerFill.Size = UDim2.new((JUMP_POWER - 20) / 180, 0, 1, 0)
JumpPowerFill.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
JumpPowerFill.BorderSizePixel = 0
JumpPowerFill.Parent = JumpPowerSlider

local JumpPowerMin = Instance.new("TextLabel")
JumpPowerMin.Name = "JumpPowerMin"
JumpPowerMin.Size = UDim2.new(0, 30, 0, 20)
JumpPowerMin.Position = UDim2.new(0, 0, 1, 0)
JumpPowerMin.BackgroundTransparency = 1
JumpPowerMin.Text = "20"
JumpPowerMin.TextColor3 = Color3.fromRGB(150, 150, 150)
JumpPowerMin.TextSize = 12
JumpPowerMin.Font = Enum.Font.Gotham
JumpPowerMin.Parent = JumpPowerSlider

local JumpPowerMax = Instance.new("TextLabel")
JumpPowerMax.Name = "JumpPowerMax"
JumpPowerMax.Size = UDim2.new(0, 30, 0, 20)
JumpPowerMax.Position = UDim2.new(1, -30, 1, 0)
JumpPowerMax.BackgroundTransparency = 1
JumpPowerMax.Text = "200"
JumpPowerMax.TextColor3 = Color3.fromRGB(150, 150, 150)
JumpPowerMax.TextSize = 12
JumpPowerMax.Font = Enum.Font.Gotham
JumpPowerMax.Parent = JumpPowerSlider

-- Cooldown Slider
local CooldownFrame = Instance.new("Frame")
CooldownFrame.Name = "CooldownFrame"
CooldownFrame.Size = UDim2.new(1, -40, 0, 60)
CooldownFrame.Position = UDim2.new(0, 20, 0, 280)
CooldownFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
CooldownFrame.BorderSizePixel = 0
CooldownFrame.Parent = MainFrame

local CooldownLabel = Instance.new("TextLabel")
CooldownLabel.Name = "CooldownLabel"
CooldownLabel.Size = UDim2.new(1, 0, 0, 20)
CooldownLabel.BackgroundTransparency = 1
CooldownLabel.Text = "COOLDOWN: " .. JUMP_COOLDOWN .. "s"
CooldownLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
CooldownLabel.TextSize = 14
CooldownLabel.Font = Enum.Font.Gotham
CooldownLabel.Parent = CooldownFrame

local CooldownSlider = Instance.new("Frame")
CooldownSlider.Name = "CooldownSlider"
CooldownSlider.Size = UDim2.new(1, -20, 0, 10)
CooldownSlider.Position = UDim2.new(0, 10, 0, 30)
CooldownSlider.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
CooldownSlider.BorderSizePixel = 0
CooldownSlider.Parent = CooldownFrame

local CooldownFill = Instance.new("Frame")
CooldownFill.Name = "CooldownFill"
CooldownFill.Size = UDim2.new((0.5 - JUMP_COOLDOWN) / 0.45, 0, 1, 0)
CooldownFill.BackgroundColor3 = Color3.fromRGB(255, 150, 0)
CooldownFill.BorderSizePixel = 0
CooldownFill.Parent = CooldownSlider

local CooldownMin = Instance.new("TextLabel")
CooldownMin.Name = "CooldownMin"
CooldownMin.Size = UDim2.new(0, 30, 0, 20)
CooldownMin.Position = UDim2.new(0, 0, 1, 0)
CooldownMin.BackgroundTransparency = 1
CooldownMin.Text = "0.05"
CooldownMin.TextColor3 = Color3.fromRGB(150, 150, 150)
CooldownMin.TextSize = 12
CooldownMin.Font = Enum.Font.Gotham
CooldownMin.Parent = CooldownSlider

local CooldownMax = Instance.new("TextLabel")
CooldownMax.Name = "CooldownMax"
CooldownMax.Size = UDim2.new(0, 30, 0, 20)
CooldownMax.Position = UDim2.new(1, -30, 1, 0)
CooldownMax.BackgroundTransparency = 1
CooldownMax.Text = "0.5"
CooldownMax.TextColor3 = Color3.fromRGB(150, 150, 150)
CooldownMax.TextSize = 12
CooldownMax.Font = Enum.Font.Gotham
CooldownMax.Parent = CooldownSlider

-- Footer
local Footer = Instance.new("TextLabel")
Footer.Name = "Footer"
Footer.Size = UDim2.new(1, 0, 0, 30)
Footer.Position = UDim2.new(0, 0, 1, -30)
Footer.BackgroundTransparency = 1
Footer.Text = "Press F to toggle | Made by ACAGEMINK123"
Footer.TextColor3 = Color3.fromRGB(150, 150, 150)
Footer.TextSize = 12
Footer.Font = Enum.Font.Gotham
Footer.Parent = MainFrame

-- Slider Interaction Functions
local function updateJumpPower(value)
    JUMP_POWER = math.floor(value)
    JumpPowerLabel.Text = "JUMP POWER: " .. JUMP_POWER
    JumpPowerFill.Size = UDim2.new((JUMP_POWER - 20) / 180, 0, 1, 0)
end

local function updateCooldown(value)
    JUMP_COOLDOWN = math.round(value * 100) / 100
    CooldownLabel.Text = "COOLDOWN: " .. JUMP_COOLDOWN .. "s"
    CooldownFill.Size = UDim2.new((0.5 - JUMP_COOLDOWN) / 0.45, 0, 1, 0)
end

-- Slider Drag Logic
local function createSliderDrag(sliderFrame, fillFrame, minValue, maxValue, currentValue, callback)
    local dragging = false
    
    local function updateFromMouse()
        if not dragging then return end
        
        local mouse = game:GetService("Players").LocalPlayer:GetMouse()
        local relativeX = math.clamp((mouse.X - sliderFrame.AbsolutePosition.X) / sliderFrame.AbsoluteSize.X, 0, 1)
        local value = minValue + (maxValue - minValue) * relativeX
        
        if sliderFrame.Name == "CooldownSlider" then
            value = maxValue - (maxValue - minValue) * relativeX
        end
        
        callback(value)
    end
    
    sliderFrame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            updateFromMouse()
        end
    end)
    
    sliderFrame.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = false
        end
    end)
    
    game:GetService("UserInputService").InputChanged:Connect(function(input)
        if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
            updateFromMouse()
        end
    end)
end

-- Initialize Sliders
createSliderDrag(JumpPowerSlider, JumpPowerFill, 20, 200, JUMP_POWER, updateJumpPower)
createSliderDrag(CooldownSlider, CooldownFill, 0.05, 0.5, JUMP_COOLDOWN, updateCooldown)

-- Infinite Jump Function
local function OnJumpRequest()
    if not InfiniteJumpEnabled then return end
    
    local CurrentTime = tick()
    if CurrentTime - LastJumpTime < JUMP_COOLDOWN then return end
    
    LastJumpTime = CurrentTime
    
    if Character and Humanoid and RootPart then
        -- Method 1: JumpPower (Universal)
        Humanoid.JumpPower = JUMP_POWER
        
        -- Method 2: Velocity Boost (Anti Anti-Cheat)
        if RootPart then
            RootPart.Velocity = Vector3.new(RootPart.Velocity.X, JUMP_POWER, RootPart.Velocity.Z)
        end
        
        -- Method 3: Jump State Force
        Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
    end
end

-- Setup Character
local function SetupCharacter(NewCharacter)
    Character = NewCharacter
    Humanoid = NewCharacter:WaitForChild("Humanoid")
    RootPart = NewCharacter:WaitForChild("HumanoidRootPart")
    
    -- Reset JumpPower
    Humanoid.JumpPower = 50
    Humanoid.JumpHeight = 10
    
    -- Anti Jump Reset
    local JumpHeightConnection
    JumpHeightConnection = RunService.Heartbeat:Connect(function()
        if Character ~= NewCharacter or not Character.Parent then
            JumpHeightConnection:Disconnect()
            return
        end
        
        -- Force JumpPower terus
        Humanoid.JumpPower = JUMP_POWER
        Humanoid.JumpHeight = JUMP_POWER / 5
    end)
end

-- Character Respawn Handler
if LocalPlayer.Character then
    SetupCharacter(LocalPlayer.Character)
end

LocalPlayer.CharacterAdded:Connect(SetupCharacter)

-- Infinite Jump Input
UserInputService.JumpRequest:Connect(OnJumpRequest)

-- Toggle Button Function
ToggleButton.MouseButton1Click:Connect(function()
    InfiniteJumpEnabled = not InfiniteJumpEnabled
    
    -- Update UI
    StatusValue.Text = InfiniteJumpEnabled and "ENABLED 🟢" or "DISABLED 🔴"
    StatusValue.TextColor3 = InfiniteJumpEnabled and Color3.fromRGB(0, 255, 0) or Color3.fromRGB(255, 50, 50)
    ToggleButton.Text = InfiniteJumpEnabled and "DISABLE INFINITE JUMP" or "ENABLE INFINITE JUMP"
    ToggleButton.BackgroundColor3 = InfiniteJumpEnabled and Color3.fromRGB(50, 200, 50) or Color3.fromRGB(200, 50, 50)
    
    -- Notification
    game.StarterGui:SetCore("SendNotification", {
        Title = "🦘 ACAGEMINK123";
        Text = "Infinite Jump " .. (InfiniteJumpEnabled and "ENABLED" or "DISABLED");
        Duration = 2;
    })
end)

-- Toggle dengan F Key
UserInputService.InputBegan:Connect(function(Input, GameProcessed)
    if GameProcessed then return end
    
    if Input.KeyCode == Enum.KeyCode.F then
        InfiniteJumpEnabled = not InfiniteJumpEnabled
        
        -- Update UI
        StatusValue.Text = InfiniteJumpEnabled and "ENABLED 🟢" or "DISABLED 🔴"
        StatusValue.TextColor3 = InfiniteJumpEnabled and Color3.fromRGB(0, 255, 0) or Color3.fromRGB(255, 50, 50)
        ToggleButton.Text = InfiniteJumpEnabled and "DISABLE INFINITE JUMP" or "ENABLE INFINITE JUMP"
        ToggleButton.BackgroundColor3 = InfiniteJumpEnabled and Color3.fromRGB(50, 200, 50) or Color3.fromRGB(200, 50, 50)
        
        print("🦘 ACAGEMINK123 Infinite Jump:", InfiniteJumpEnabled and "ON" or "OFF")
        
        game.StarterGui:SetCore("SendNotification", {
            Title = "🦘 ACAGEMINK123";
            Text = "Infinite Jump " .. (InfiniteJumpEnabled and "ON!" or "OFF!");
            Duration = 2;
        })
    end
end)

-- Animation untuk UI
local function animateUI()
    local tweenInfo = TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    
    -- Button hover effects
    local buttons = {ToggleButton, CloseButton}
    
    for _, button in pairs(buttons) do
        local originalColor = button.BackgroundColor3
        
        button.MouseEnter:Connect(function()
            local tween = TweenService:Create(button, tweenInfo, {BackgroundColor3 = Color3.fromRGB(
                math.min(originalColor.R * 255 + 20, 255),
                math.min(originalColor.G * 255 + 20, 255),
                math.min(originalColor.B * 255 + 20, 255)
            ) / 255})
            tween:Play()
        end)
        
        button.MouseLeave:Connect(function()
            local tween = TweenService:Create(button, tweenInfo, {BackgroundColor3 = originalColor})
            tween:Play()
        end)
    end
end

animateUI()

]]a(b)()
