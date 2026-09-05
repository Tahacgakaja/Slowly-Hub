-- SLOWLY SENSI V6.11 | BOTÃO FLUTUANTE COM LOGO SLOWLY XITER

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local Workspace = game:GetService("Workspace")
local CoreGui = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")
local StarterGui = game:GetService("StarterGui")

local LocalPlayer = Players.LocalPlayer
local Camera = Workspace.CurrentCamera

local RAW_ID = 134390937848624
local DISCORD_LINK = "https://discord.gg/m6vmPpz4z8"

-- Aviso no chat ao injetar
task.spawn(function()
    pcall(function()
        StarterGui:SetCore("ChatMakeSystemMessage", {
            Text = "[SLOWLY SENSI]: Entre no nosso Discord: " .. DISCORD_LINK,
            Color = Color3.fromRGB(235, 0, 0),
            Font = Enum.Font.SourceSansBold,
            TextSize = 16
        })
    end)
end)

local Config = {
    AimbotEnabled = true,
    Smoothness = 0,
    AimPart = "Head",
    WallCheck = false,
    TeamCheck = false,
    
    FOVVisible = true,
    FOVRadius = 180,
    FOVColor = Color3.fromRGB(235, 0, 0),
    
    ESPEnabled = true,
    BoxESP = true,
    NameESP = true,
    HealthESP = true,
    SkeletonESP = true,
    ESPTeamCheck = false,
    ESPColor = Color3.fromRGB(255, 255, 255),
    
    HideFloatingBtn = false,
    ThemeColor = Color3.fromRGB(235, 0, 0)
}

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "SlowlySensiUI_ExactMatch"
ScreenGui.ResetOnSpawn = false
if syn and syn.protect_gui then syn.protect_gui(ScreenGui) end
ScreenGui.Parent = CoreGui:FindFirstChild("RobloxGui") or CoreGui

local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 310, 0, 275)
MainFrame.Position = UDim2.new(0.05, 0, 0.25, 0)
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 10)
UICorner.Parent = MainFrame

local OpenBtn = Instance.new("ImageButton")
OpenBtn.Name = "FloatingOpenBtn"
OpenBtn.Size = UDim2.new(0, 45, 0, 45)
OpenBtn.Position = UDim2.new(0.85, 0, 0.15, 0)
OpenBtn.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
OpenBtn.BackgroundTransparency = 0
OpenBtn.BorderSizePixel = 0
OpenBtn.ScaleType = Enum.ScaleType.Fit
OpenBtn.Visible = true
OpenBtn.Active = true
OpenBtn.Draggable = true
OpenBtn.Parent = ScreenGui

local OpenBtnCorner = Instance.new("UICorner")
OpenBtnCorner.CornerRadius = UDim.new(1, 0)
OpenBtnCorner.Parent = OpenBtn

local OpenBtnStroke = Instance.new("UIStroke")
OpenBtnStroke.Thickness = 2.5
OpenBtnStroke.Color = Config.ThemeColor
OpenBtnStroke.Parent = OpenBtn

OpenBtn.Image = "rbxassetid://" .. tostring(RAW_ID)

local TitleBar = Instance.new("Frame")
TitleBar.Size = UDim2.new(1, 0, 0, 30)
TitleBar.BackgroundColor3 = Config.ThemeColor
TitleBar.BorderSizePixel = 0
TitleBar.Parent = MainFrame

local TitleCorner = Instance.new("UICorner")
TitleCorner.CornerRadius = UDim.new(0, 10)
TitleCorner.Parent = TitleBar

local TitleFill = Instance.new("Frame")
TitleFill.Size = UDim2.new(1, 0, 0, 10)
TitleFill.Position = UDim2.new(0, 0, 1, -10)
TitleFill.BackgroundColor3 = Config.ThemeColor
TitleFill.BorderSizePixel = 0
TitleFill.Parent = TitleBar

local TitleLabel = Instance.new("TextLabel")
TitleLabel.Size = UDim2.new(0.8, 0, 1, 0)
TitleLabel.Position = UDim2.new(0.04, 0, 0, 0)
TitleLabel.BackgroundTransparency = 1
TitleLabel.Text = "Slowly Sensi 1.108.X"
TitleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TitleLabel.TextXAlignment = Enum.TextXAlignment.Left
TitleLabel.Font = Enum.Font.SourceSansBold
TitleLabel.TextSize = 14
TitleLabel.Parent = TitleBar

local CloseBtn = Instance.new("TextButton")
CloseBtn.Size = UDim2.new(0, 25, 0, 25)
CloseBtn.Position = UDim2.new(1, -28, 0, 2.5)
CloseBtn.BackgroundTransparency = 1
CloseBtn.Text = "✕"
CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseBtn.Font = Enum.Font.SourceSansBold
CloseBtn.TextSize = 16
CloseBtn.Parent = TitleBar

local function ToggleMainFrame()
    local isOpen = MainFrame.Visible
    if not isOpen then
        MainFrame.Visible = true
        MainFrame.Size = UDim2.new(0, 0, 0, 0)
        MainFrame.BackgroundTransparency = 1
        local tweenInfo = TweenInfo.new(0.25, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
        TweenService:Create(MainFrame, tweenInfo, { Size = UDim2.new(0, 310, 0, 275), BackgroundTransparency = 0 }):Play()
    else
        local tweenInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.In)
        local tw = TweenService:Create(MainFrame, tweenInfo, { Size = UDim2.new(0, 0, 0, 0), BackgroundTransparency = 1 })
        tw:Play()
        tw.Completed:Connect(function()
            MainFrame.Visible = false
            MainFrame.Size = UDim2.new(0, 310, 0, 275)
            MainFrame.BackgroundTransparency = 0
        end)
    end
end

CloseBtn.MouseButton1Click:Connect(ToggleMainFrame)
OpenBtn.MouseButton1Click:Connect(ToggleMainFrame)

local TabBar = Instance.new("Frame")
TabBar.Size = UDim2.new(1, -12, 0, 24)
TabBar.Position = UDim2.new(0, 6, 0, 36)
TabBar.BackgroundTransparency = 1
TabBar.Parent = MainFrame

local Pages = {}
local TabButtons = {}

local function CreateTab(name, pos, selected)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.23, 0, 1, 0)
    btn.Position = pos
    btn.BackgroundColor3 = selected and Config.ThemeColor or Color3.fromRGB(30, 30, 30)
    btn.Text = name
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Font = Enum.Font.SourceSansBold
    btn.TextSize = 12
    btn.Parent = TabBar

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 4)
    corner.Parent = btn

    local page = Instance.new("ScrollingFrame")
    page.Size = UDim2.new(1, -12, 1, -68)
    page.Position = UDim2.new(0, 6, 0, 64)
    page.BackgroundTransparency = 1
    page.ScrollBarThickness = 2
    page.Visible = selected
    page.CanvasSize = UDim2.new(0, 0, 0, 0)
    page.Parent = MainFrame

    local layout = Instance.new("UIListLayout")
    layout.Parent = page
    layout.SortOrder = Enum.SortOrder.LayoutOrder
    layout.Padding = UDim.new(0, 5)
    
    layout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
        page.CanvasSize = UDim2.new(0, 0, 0, layout.AbsoluteContentSize.Y + 6)
    end)

    Pages[name] = {Btn = btn, Page = page}
    table.insert(TabButtons, {Btn = btn, Name = name})
    return page
end

local AimPage = CreateTab("Aimbot", UDim2.new(0, 0, 0, 0), true)
local EspPage = CreateTab("Esp", UDim2.new(0.25, 0, 0, 0), false)
local MiscPage = CreateTab("Misc", UDim2.new(0.50, 0, 0, 0), false)
local InfoPage = CreateTab("Info", UDim2.new(0.75, 0, 0, 0), false)

local function SwitchTab(targetName)
    for name, tab in pairs(Pages) do
        local isTarget = (name == targetName)
        tab.Page.Visible = isTarget
        tab.Btn.BackgroundColor3 = isTarget and Config.ThemeColor or Color3.fromRGB(30, 30, 30)
    end
end

Pages["Aimbot"].Btn.MouseButton1Click:Connect(function() SwitchTab("Aimbot") end)
Pages["Esp"].Btn.MouseButton1Click:Connect(function() SwitchTab("Esp") end)
Pages["Misc"].Btn.MouseButton1Click:Connect(function() SwitchTab("Misc") end)
Pages["Info"].Btn.MouseButton1Click:Connect(function() SwitchTab("Info") end)

local ToggleButtonsList = {}
local SliderFillsList = {}
local DropdownButtonsList = {}
local LinesList = {}

local function UpdateThemeColor(newColor)
    Config.ThemeColor = newColor
    Config.FOVColor = newColor
    TitleBar.BackgroundColor3 = newColor
    TitleFill.BackgroundColor3 = newColor
    OpenBtnStroke.Color = newColor
    
    for _, tabData in ipairs(TabButtons) do
        if Pages[tabData.Name].Page.Visible then
            tabData.Btn.BackgroundColor3 = newColor
        else
            tabData.Btn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
        end
    end
    
    for _, item in ipairs(ToggleButtonsList) do
        if item.GetState() then
            item.Btn.BackgroundColor3 = newColor
        end
    end
    
    for _, fill in ipairs(SliderFillsList) do
        fill.BackgroundColor3 = newColor
    end
    
    for _, dropBtn in ipairs(DropdownButtonsList) do
        dropBtn.BackgroundColor3 = newColor
    end

    for _, line in ipairs(LinesList) do
        line.BackgroundColor3 = newColor
    end
end

local function AddToggle(parent, text, default, callback)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, 0, 0, 24)
    frame.BackgroundTransparency = 1
    frame.Parent = parent

    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0, 16, 0, 16)
    btn.Position = UDim2.new(0, 2, 0.15, 0)
    btn.BackgroundColor3 = default and Config.ThemeColor or Color3.fromRGB(35, 35, 35)
    btn.Text = default and "✓" or ""
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Font = Enum.Font.SourceSansBold
    btn.TextSize = 12
    btn.Parent = frame

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 3)
    corner.Parent = btn

    local lbl = Instance.new("TextLabel")
    lbl.Size = UDim2.new(0.85, 0, 1, 0)
    lbl.Position = UDim2.new(0, 26, 0, 0)
    lbl.BackgroundTransparency = 1
    lbl.Text = text
    lbl.TextColor3 = Color3.fromRGB(220, 220, 220)
    lbl.Font = Enum.Font.SourceSans
    lbl.TextXAlignment = Enum.TextXAlignment.Left
    lbl.TextSize = 13
    lbl.Parent = frame

    local line = Instance.new("Frame")
    line.Size = UDim2.new(1, 0, 0, 1)
    line.Position = UDim2.new(0, 0, 1, -1)
    line.BackgroundColor3 = Config.ThemeColor
    line.BorderSizePixel = 0
    line.Parent = frame
    table.insert(LinesList, line)

    local state = default
    table.insert(ToggleButtonsList, {Btn = btn, GetState = function() return state end})

    btn.MouseButton1Click:Connect(function()
        state = not state
        btn.BackgroundColor3 = state and Config.ThemeColor or Color3.fromRGB(35, 35, 35)
        btn.Text = state and "✓" or ""
        callback(state)
    end)
end

local function AddSlider(parent, labelText, min, max, default, callback)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, 0, 0, 28)
    frame.BackgroundTransparency = 1
    frame.Parent = parent

    local bg = Instance.new("Frame")
    bg.Size = UDim2.new(0.65, 0, 0, 18)
    bg.Position = UDim2.new(0, 2, 0, 2)
    bg.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    bg.BorderSizePixel = 0
    bg.Parent = frame

    local fill = Instance.new("Frame")
    fill.Size = UDim2.new(0, 8, 1, 0)
    fill.Position = UDim2.new((default - min)/(max - min), -4, 0, 0)
    fill.BackgroundColor3 = Config.ThemeColor
    fill.BorderSizePixel = 0
    fill.Parent = bg
    table.insert(SliderFillsList, fill)

    local valLbl = Instance.new("TextLabel")
    valLbl.Size = UDim2.new(1, 0, 1, 0)
    valLbl.BackgroundTransparency = 1
    valLbl.Text = tostring(default)
    valLbl.TextColor3 = Color3.fromRGB(220, 220, 220)
    valLbl.Font = Enum.Font.SourceSans
    valLbl.TextSize = 12
    valLbl.Parent = bg

    local nameLbl = Instance.new("TextLabel")
    nameLbl.Size = UDim2.new(0.3, 0, 1, 0)
    nameLbl.Position = UDim2.new(0.68, 0, 0, 0)
    nameLbl.BackgroundTransparency = 1
    nameLbl.Text = labelText
    nameLbl.TextColor3 = Color3.fromRGB(220, 220, 220)
    nameLbl.Font = Enum.Font.SourceSans
    nameLbl.TextXAlignment = Enum.TextXAlignment.Left
    nameLbl.TextSize = 12
    nameLbl.Parent = frame

    local line = Instance.new("Frame")
    line.Size = UDim2.new(1, 0, 0, 1)
    line.Position = UDim2.new(0, 0, 1, -1)
    line.BackgroundColor3 = Config.ThemeColor
    line.BorderSizePixel = 0
    line.Parent = frame
    table.insert(LinesList, line)

    local dragging = false
    local function Update(input)
        local pos = math.clamp((input.Position.X - bg.AbsolutePosition.X) / bg.AbsoluteSize.X, 0, 1)
        local val = math.floor(min + (max - min) * pos)
        fill.Position = UDim2.new(pos, -4, 0, 0)
        valLbl.Text = tostring(val)
        callback(val)
    end

    bg.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            Update(input)
        end
    end)
    UserInputService.InputChanged:Connect(function(input)
        if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
            Update(input)
        end
    end)
    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = false
        end
    end)
end

local function AddTargetSelector(parent)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, 0, 0, 26)
    frame.BackgroundTransparency = 1
    frame.Parent = parent

    local targetDisplay = Instance.new("TextLabel")
    targetDisplay.Size = UDim2.new(0.5, 0, 1, 0)
    targetDisplay.Position = UDim2.new(0, 2, 0, 0)
    targetDisplay.BackgroundTransparency = 1
    targetDisplay.Text = "Cabeça"
    targetDisplay.TextColor3 = Color3.fromRGB(220, 220, 220)
    targetDisplay.Font = Enum.Font.SourceSans
    targetDisplay.TextXAlignment = Enum.TextXAlignment.Left
    targetDisplay.TextSize = 13
    targetDisplay.Parent = frame

    local dropdownBtn = Instance.new("TextButton")
    dropdownBtn.Size = UDim2.new(0, 22, 0, 18)
    dropdownBtn.Position = UDim2.new(0.52, 0, 0.15, 0)
    dropdownBtn.BackgroundColor3 = Config.ThemeColor
    dropdownBtn.Text = "▼"
    dropdownBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    dropdownBtn.Font = Enum.Font.SourceSansBold
    dropdownBtn.TextSize = 10
    dropdownBtn.Parent = frame
    table.insert(DropdownButtonsList, dropdownBtn)

    local btnCorner = Instance.new("UICorner")
    btnCorner.CornerRadius = UDim.new(0, 3)
    btnCorner.Parent = dropdownBtn

    local targetLabel = Instance.new("TextLabel")
    targetLabel.Size = UDim2.new(0.35, 0, 1, 0)
    targetLabel.Position = UDim2.new(0.62, 0, 0, 0)
    targetLabel.BackgroundTransparency = 1
    targetLabel.Text = "Target"
    targetLabel.TextColor3 = Color3.fromRGB(220, 220, 220)
    targetLabel.Font = Enum.Font.SourceSans
    targetLabel.TextXAlignment = Enum.TextXAlignment.Left
    targetLabel.TextSize = 13
    targetLabel.Parent = frame

    local line = Instance.new("Frame")
    line.Size = UDim2.new(1, 0, 0, 1)
    line.Position = UDim2.new(0, 0, 1, -1)
    line.BackgroundColor3 = Config.ThemeColor
    line.BorderSizePixel = 0
    line.Parent = frame
    table.insert(LinesList, line)

    local targets = {
        {Name = "Cabeça", Part = "Head"},
        {Name = "Torso", Part = "Torso"},
        {Name = "HumanoidRoot", Part = "HumanoidRootPart"}
    }
    local currentIndex = 1

    dropdownBtn.MouseButton1Click:Connect(function()
        currentIndex = currentIndex + 1
        if currentIndex > #targets then currentIndex = 1 end
        targetDisplay.Text = targets[currentIndex].Name
        Config.AimPart = targets[currentIndex].Part
    end)
end

local function AddThemeSelector(parent)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, 0, 0, 26)
    frame.BackgroundTransparency = 1
    frame.Parent = parent

    local nameLbl = Instance.new("TextLabel")
    nameLbl.Size = UDim2.new(0.5, 0, 1, 0)
    nameLbl.Position = UDim2.new(0, 2, 0, 0)
    nameLbl.BackgroundTransparency = 1
    nameLbl.Text = "Cor do Tema"
    nameLbl.TextColor3 = Color3.fromRGB(220, 220, 220)
    nameLbl.Font = Enum.Font.SourceSans
    nameLbl.TextXAlignment = Enum.TextXAlignment.Left
    nameLbl.TextSize = 13
    nameLbl.Parent = frame

    local colors = {
        {Name = "Vermelho", Color = Color3.fromRGB(235, 0, 0)},
        {Name = "Azul", Color = Color3.fromRGB(0, 120, 255)},
        {Name = "Verde", Color = Color3.fromRGB(0, 235, 80)},
        {Name = "Roxo", Color = Color3.fromRGB(160, 0, 255)},
        {Name = "Amarelo", Color = Color3.fromRGB(255, 200, 0)},
        {Name = "Rosa", Color = Color3.fromRGB(255, 0, 150)}
    }
    local colorIndex = 1

    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.4, 0, 0.8, 0)
    btn.Position = UDim2.new(0.58, 0, 0.1, 0)
    btn.BackgroundColor3 = colors[1].Color
    btn.Text = colors[1].Name
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Font = Enum.Font.SourceSansBold
    btn.TextSize = 12
    btn.Parent = frame

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 4)
    corner.Parent = btn

    btn.MouseButton1Click:Connect(function()
        colorIndex = colorIndex + 1
        if colorIndex > #colors then colorIndex = 1 end
        local selected = colors[colorIndex]
        btn.BackgroundColor3 = selected.Color
        btn.Text = selected.Name
        UpdateThemeColor(selected.Color)
    end)
end

AddToggle(AimPage, "Ativar Aimbot", Config.AimbotEnabled, function(v) Config.AimbotEnabled = v end)
AddToggle(AimPage, "Exibir Circulo do FOV", Config.FOVVisible, function(v) Config.FOVVisible = v end)
AddSlider(AimPage, "Smoothness", 0, 10, Config.Smoothness, function(v) Config.Smoothness = v end)
AddSlider(AimPage, "Regular FOV", 30, 500, Config.FOVRadius, function(v) Config.FOVRadius = v end)
AddTargetSelector(AimPage)
AddToggle(AimPage, "Wall Check", Config.WallCheck, function(v) Config.WallCheck = v end)
AddToggle(AimPage, "Team Check", Config.TeamCheck, function(v) Config.TeamCheck = v end)

AddToggle(EspPage, "Ativar ESP Master", Config.ESPEnabled, function(v) Config.ESPEnabled = v end)
AddToggle(EspPage, "Box ESP (Caixa 2D)", Config.BoxESP, function(v) Config.BoxESP = v end)
AddToggle(EspPage, "Name ESP", Config.NameESP, function(v) Config.NameESP = v end)
AddToggle(EspPage, "Health Bar (Verde)", Config.HealthESP, function(v) Config.HealthESP = v end)
AddToggle(EspPage, "Skeleton ESP (Esqueleto)", Config.SkeletonESP, function(v) Config.SkeletonESP = v end)

AddToggle(MiscPage, "Ocultar Botão Flutuante", Config.HideFloatingBtn, function(v)
    Config.HideFloatingBtn = v
    OpenBtn.BackgroundTransparency = v and 1 or 0
    OpenBtn.ImageTransparency = v and 1 or 0
    OpenBtnStroke.Transparency = v and 1 or 0
end)
AddThemeSelector(MiscPage)

local InfoText = Instance.new("TextLabel")
InfoText.Size = UDim2.new(1, 0, 0, 60)
InfoText.BackgroundTransparency = 1
InfoText.Text = "Slowly Sensi V6.11\nDesenvolvido por Slowly Scripts\n\nStatus: Indetectavel"
InfoText.TextColor3 = Color3.fromRGB(200, 200, 200)
InfoText.Font = Enum.Font.SourceSans
InfoText.TextSize = 13
InfoText.TextXAlignment = Enum.TextXAlignment.Left
InfoText.Parent = InfoPage

local CopyDiscordBtn = Instance.new("TextButton")
CopyDiscordBtn.Size = UDim2.new(1, 0, 0, 32)
CopyDiscordBtn.BackgroundColor3 = Config.ThemeColor
CopyDiscordBtn.Text = "Copiar Link do Discord"
CopyDiscordBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CopyDiscordBtn.Font = Enum.Font.SourceSansBold
CopyDiscordBtn.TextSize = 13
CopyDiscordBtn.Parent = InfoPage

local BtnCorner = Instance.new("UICorner")
BtnCorner.CornerRadius = UDim.new(0, 4)
BtnCorner.Parent = CopyDiscordBtn

CopyDiscordBtn.MouseButton1Click:Connect(function()
    if setclipboard then
        setclipboard(DISCORD_LINK)
        CopyDiscordBtn.Text = "Link Copiado!"
        task.wait(2)
        CopyDiscordBtn.Text = "Copiar Link do Discord"
    else
        CopyDiscordBtn.Text = "Executor sem suporte a setclipboard"
        task.wait(2)
        CopyDiscordBtn.Text = "Copiar Link do Discord"
    end
end)

local FOVCircle = Drawing.new("Circle")
FOVCircle.Thickness = 1.5
FOVCircle.NumSides = 60
FOVCircle.Filled = false

local function IsVisible(targetPart)
    if not Config.WallCheck then return true end
    local origin = Camera.CFrame.Position
    local destination = targetPart.Position
    local ignoreList = {LocalPlayer.Character, targetPart.Parent}
    local parts = Camera:GetPartsObscuringTarget({origin, destination}, ignoreList)
    return #parts == 0
end

local function GetTargetPart()
    local target = nil
    local shortestDist = Config.FOVRadius
    local viewportCenter = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2)

    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= LocalPlayer then
            if not Config.TeamCheck or (p.Team ~= LocalPlayer.Team) then
                local char = p.Character
                if char and char:FindFirstChild("Humanoid") and char.Humanoid.Health > 0 then
                    local aimPart = char:FindFirstChild(Config.AimPart) 
                    if not aimPart and Config.AimPart == "Torso" then
                        aimPart = char:FindFirstChild("UpperTorso") or char:FindFirstChild("HumanoidRootPart")
                    end

                    if aimPart and IsVisible(aimPart) then
                        local screenPos, onScreen = Camera:WorldToViewportPoint(aimPart.Position)
                        if onScreen then
                            local dist = (Vector2.new(screenPos.X, screenPos.Y) - viewportCenter).Magnitude
                            if dist < shortestDist then
                                shortestDist = dist
                                target = aimPart
                            end
                        end
                    end
                end
            end
        end
    end
    return target
end

local ESPObjects = {}

local function CreateESP(player)
    local drawings = {
        Box = Drawing.new("Square"),
        Name = Drawing.new("Text"),
        HealthOutline = Drawing.new("Square"),
        HealthBar = Drawing.new("Square"),
        Skeleton = {}
    }

    drawings.Box.Thickness = 1.5
    drawings.Box.Filled = false
    drawings.Box.Color = Config.ESPColor

    drawings.Name.Size = 13
    drawings.Name.Center = true
    drawings.Name.Outline = true
    drawings.Name.Color = Color3.fromRGB(255, 255, 255)

    drawings.HealthOutline.Thickness = 1
    drawings.HealthOutline.Filled = true
    drawings.HealthOutline.Color = Color3.fromRGB(0, 0, 0)

    drawings.HealthBar.Thickness = 1
    drawings.HealthBar.Filled = true
    drawings.HealthBar.Color = Color3.fromRGB(0, 255, 0)

    for i = 1, 15 do
        local line = Drawing.new("Line")
        line.Thickness = 1.5
        line.Color = Color3.fromRGB(255, 255, 255)
        table.insert(drawings.Skeleton, line)
    end

    ESPObjects[player] = drawings
end

local function RemoveESP(player)
    if ESPObjects[player] then
        for _, obj in pairs(ESPObjects[player]) do
            if type(obj) == "table" then
                for _, line in pairs(obj) do line:Remove() end
            else
                obj:Remove()
            end
        end
        ESPObjects[player] = nil
    end
end

for _, p in ipairs(Players:GetPlayers()) do if p ~= LocalPlayer then CreateESP(p) end end
Players.PlayerAdded:Connect(CreateESP)
Players.PlayerRemoving:Connect(RemoveESP)

local R15Bones = {
    {"Head", "UpperTorso"}, {"UpperTorso", "LowerTorso"},
    {"UpperTorso", "LeftUpperArm"}, {"LeftUpperArm", "LeftLowerArm"}, {"LeftLowerArm", "LeftHand"},
    {"UpperTorso", "RightUpperArm"}, {"RightUpperArm", "RightLowerArm"}, {"RightLowerArm", "RightHand"},
    {"LowerTorso", "LeftUpperLeg"}, {"LeftUpperLeg", "LeftLowerLeg"}, {"LeftLowerLeg", "LeftFoot"},
    {"LowerTorso", "RightUpperLeg"}, {"RightUpperLeg", "RightLowerLeg"}, {"RightLowerLeg", "RightFoot"}
}

local R6Bones = {
    {"Head", "Torso"}, {"Torso", "Left Arm"}, {"Torso", "Right Arm"},
    {"Torso", "Left Leg"}, {"Torso", "Right Leg"}
}

RunService.RenderStepped:Connect(function()
    local center = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2)
    FOVCircle.Position = center
    FOVCircle.Radius = Config.FOVRadius
    FOVCircle.Visible = Config.FOVVisible and Config.AimbotEnabled
    FOVCircle.Color = Config.FOVColor

    if Config.AimbotEnabled then
        local targetPart = GetTargetPart()
        if targetPart then
            if Config.Smoothness == 0 then
                Camera.CFrame = CFrame.new(Camera.CFrame.Position, targetPart.Position)
            else
                local targetCFrame = CFrame.new(Camera.CFrame.Position, targetPart.Position)
                local lerpFactor = math.clamp(1 / (Config.Smoothness * 2), 0.02, 0.9)
                Camera.CFrame = Camera.CFrame:Lerp(targetCFrame, lerpFactor)
            end
        end
    end

    for player, drawings in pairs(ESPObjects) do
        local char = player.Character
        local isTeam = (player.Team == LocalPlayer.Team)
        local shouldShow = Config.ESPEnabled and char and char:FindFirstChild("Humanoid") and char.Humanoid.Health > 0 and (not Config.ESPTeamCheck or not isTeam)

        if shouldShow then
            local root = char:FindFirstChild("HumanoidRootPart") or char:FindFirstChild("Torso")
            local head = char:FindFirstChild("Head")

            if root and head then
                local rootPos, onScreen = Camera:WorldToViewportPoint(root.Position)
                local headPos = Camera:WorldToViewportPoint(head.Position + Vector3.new(0, 0.5, 0))
                local legPos = Camera:WorldToViewportPoint(root.Position - Vector3.new(0, 3, 0))

                if onScreen then
                    local boxHeight = math.abs(headPos.Y - legPos.Y)
                    local boxWidth = boxHeight * 0.6
                    local boxPos = Vector2.new(rootPos.X - boxWidth / 2, rootPos.Y - boxHeight / 2)

                    drawings.Box.Size = Vector2.new(boxWidth, boxHeight)
                    drawings.Box.Position = boxPos
                    drawings.Box.Visible = Config.BoxESP

                    drawings.Name.Text = player.Name
                    drawings.Name.Position = Vector2.new(rootPos.X, boxPos.Y - 16)
                    drawings.Name.Visible = Config.NameESP

                    if Config.HealthESP then
                        local hum = char.Humanoid
                        local healthPercent = math.clamp(hum.Health / hum.MaxHealth, 0, 1)
                        local barWidth = 3
                        local barHeight = boxHeight * healthPercent

                        drawings.HealthOutline.Size = Vector2.new(barWidth + 2, boxHeight + 2)
                        drawings.HealthOutline.Position = Vector2.new(boxPos.X - 6, boxPos.Y - 1)
                        drawings.HealthOutline.Visible = true

                        drawings.HealthBar.Size = Vector2.new(barWidth, barHeight)
                        drawings.HealthBar.Position = Vector2.new(boxPos.X - 5, boxPos.Y + (boxHeight - barHeight))
                        drawings.HealthBar.Visible = true
                    else
                        drawings.HealthOutline.Visible = false
                        drawings.HealthBar.Visible = false
                    end

                    if Config.SkeletonESP then
                        local bonesToUse = char:FindFirstChild("UpperTorso") and R15Bones or R6Bones
                        local lineIndex = 1

                        for _, pair in ipairs(bonesToUse) do
                            local partA = char:FindFirstChild(pair[1])
                            local partB = char:FindFirstChild(pair[2])

                            if partA and partB and lineIndex <= #drawings.Skeleton then
                                local posA, visA = Camera:WorldToViewportPoint(partA.Position)
                                local posB, visB = Camera:WorldToViewportPoint(partB.Position)

                                if visA and visB then
                                    local line = drawings.Skeleton[lineIndex]
                                    line.From = Vector2.new(posA.X, posA.Y)
                                    line.To = Vector2.new(posB.X, posB.Y)
                                    line.Visible = true
                                    lineIndex = lineIndex + 1
                                end
                            end
                        end
                        for i = lineIndex, #drawings.Skeleton do drawings.Skeleton[i].Visible = false end
                    else
                        for _, line in ipairs(drawings.Skeleton) do line.Visible = false end
                    end
                else
                    drawings.Box.Visible = false
                    drawings.Name.Visible = false
                    drawings.HealthOutline.Visible = false
                    drawings.HealthBar.Visible = false
                    for _, line in ipairs(drawings.Skeleton) do line.Visible = false end
                end
            end
        else
            drawings.Box.Visible = false
            drawings.Name.Visible = false
            drawings.HealthOutline.Visible = false
            drawings.HealthBar.Visible = false
            for _, line in ipairs(drawings.Skeleton) do line.Visible = false end
        end
    end
end)
