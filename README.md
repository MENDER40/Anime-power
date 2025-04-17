-- Icon personalizado
local ScreenGui = Instance.new("ScreenGui")
local ImageButton = Instance.new("ImageButton")
local UICorner = Instance.new("UICorner")

-- Propriedades da GUI
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Enabled = true -- Garante que a GUI está ativada

ImageButton.Parent = ScreenGui
ImageButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ImageButton.BorderSizePixel = 0
ImageButton.Position = UDim2.new(0.005, 0, 0.010, 0)
ImageButton.Size = UDim2.new(0, 50, 0, 50) -- Tamanho aumentado para facilitar a visualização
ImageButton.Image = "rbxassetid://139166819013498" -- ID do ícone

UICorner.Parent = ImageButton

-- Função para tornar o botão arrastável
local UIS = game:GetService("UserInputService")
local dragging, dragInput, startPos, startMousePos
local hasMoved = false

ImageButton.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        hasMoved = false
        startPos = ImageButton.Position
        startMousePos = UIS:GetMouseLocation()

        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

ImageButton.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

UIS.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = UIS:GetMouseLocation() - startMousePos
        if math.abs(delta.X) > 5 or math.abs(delta.Y) > 5 then 
            hasMoved = true
        end
        ImageButton.Position = UDim2.new(
            startPos.X.Scale, startPos.X.Offset + delta.X,
            startPos.Y.Scale, startPos.Y.Offset + delta.Y
        )
    end
end)

ImageButton.MouseButton1Down:Connect(function()
    task.wait(0.1)
    if not hasMoved then
        game:GetService("VirtualInputManager"):SendKeyEvent(true, Enum.KeyCode.LeftControl, false, game)
    end
end)

-- Carregar Fluent Library
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

if not Fluent then
    warn("Erro ao carregar Fluent Library")
    return
end

local MarketplaceService = game:GetService("MarketplaceService")
local PlaceId = game.PlaceId
local ProductInfo = MarketplaceService:GetProductInfo(PlaceId)
local GameName = ProductInfo.Name

Fluent:Notify({ 
    Title = "Script executado com sucesso", 
    Content = "Você está usando Mender_hub",
    Duration = 4 
})

local Window = Fluent:CreateWindow({
    Title = "Mender_hub",
    SubTitle = "-- " .. GameName,
    TabWidth = 102,
    Size = UDim2.fromOffset(450, 320),
    Acrylic = false,
    Theme = "Amethyst",
    MinimizeKey = Enum.KeyCode.LeftControl
})

local Tabs = {
    Info = Window:AddTab({ Title = "Info", Icon = "scroll" }),
    Farm = Window:AddTab({ Title = "Farm", Icon = "rbxassetid://18831424669" }),
    Defense = Window:AddTab({ Title = "Defense", Icon = "scroll" }),
    Eggs = Window:AddTab({ Title = "Hatch", Icon = "egg" }),
    Dungeon = Window:AddTab({ Title = "Dungeon", Icon ="" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" }),
}

Tabs.Info:AddParagraph({
    Title = "This script is updated daily",
    Content = "Correções de bugs"
})


local AutoClick= Tabs.Farm:AddToggle("AutoClick", {Title = "AUTO CLICK", Default = false})
AutoClick:OnChanged(function()
    while AutoClick.Value do
    local args = {
    [1] = "attack"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))

wait(0)
           end
end)

--JOIN DEFENSE
local autodefense= Tabs.Defense:AddToggle("autodefense", {Title = "Auto Join defense", Default = false})

autodefense:OnChanged(function()
    while autodefense.Value do
--remote
local args = {
    [1] = "joinDefense"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))

        wait(0.9)
    end
end)
--JOIN DEFENSE

--START DEFENSE
local StartDefense= Tabs.Main:AddToggle("StartDefense", {Title = "Start defense", Default = false})

StartDefense:OnChanged(function()
    while StartDefense.Value do
local args = {
    [1] = "startDefense",
    [2] = {
        ["privacy"] = "public",
        ["difficult"] = "easy"
    }
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))

wait(2)
    end
end)
--START DEFENSE 

--EGGS
local AutoClick= Tabs.Eggs:AddToggle("AutoClick", {Title = "shinobi world", Default = false})
AutoClick:OnChanged(function()
    while AutoClick.Value do
    local args = {
    [1] = "rollChampion",
    [2] = "one",
    [3] = "shinobi world"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(0)
           end
end)



local AutoClick= Tabs.Eggs:AddToggle("AutoClick", {Title = "boar tavern", Default = false})
AutoClick:OnChanged(function()
    while AutoClick.Value do
    local args = {
    [1] = "rollChampion",
    [2] = "one",
    [3] = "boar tavern"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(0)
           end
end)
--EGGS

--DUNGEON
local Insane= Tabs.Dungeon:AddToggle("Insane", {Title = "Auto Join insane", Default = false})

Insane:OnChanged(function()
    while Insane.Value do
--remote
local args = {
    [1] = "joinDungeon",
    [2] = "dungeon insane"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))

wait(2)
    end
end)
--DUNGEON

--ANTAFK
local Toggle = Tabs.Settings:AddToggle("AntiAFK", { Title = "Anti AFK", Default = true})

Toggle:OnChanged(function(state)
    _G.antiAFK = state

    if _G.antiAFK then
        task.spawn(function()
            while _G.antiAFK do
                game:GetService("Players").LocalPlayer.Idled:Connect(function()
                    game:GetService("VirtualUser"):CaptureController()
                    game:GetService("VirtualUser"):ClickButton2(Vector2.new())
                end)
                task.wait(1)
            end
        end)
    end
end)
--ANTAFK
