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
    Info = Window:AddTab({ Title = "Info", Icon = "rbxassetid://77473995449278" }),
    Farm = Window:AddTab({ Title = "Farm", Icon = "rbxassetid://140251526987992" }),
    Player = Window:AddTab({ Title = "Player", Icon ="rbxassetid://131528850280887" }),
    Upgrades = Window:AddTab({ Title = "Upgrades", Icon ="rbxassetid://77669617316317"}),
    Defense = Window:AddTab({ Title = "Defense", Icon = "rbxassetid://140251526987" }),
    Eggs = Window:AddTab({ Title = "Hatch", Icon = "rbxassetid://74532559013474" }),
    Dungeon = Window:AddTab({ Title = "Dungeon", Icon ="rbxassetid://101216544797779" }),
    Raid = Window:AddTab({ Title = "Raid", Icon ="rbxassetid://140251526987992" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "rbxassetid://105210425187745" }),
}

Tabs.Info:AddParagraph({
    Title = "This script is updated daily",
    Content = "Correções de bugs"
})

--PLAYER
local AutoClick= Tabs.Player:AddToggle("AutoClick", {Title = "AUTO CLICK", Default = false})
AutoClick:OnChanged(function()
    while AutoClick.Value do
    local args = {
    [1] = "attack"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))

wait(0)
           end
end)

local Rank= Tabs.Player:AddToggle("Rank", {Title = "Rank Up", Default = false})
Rank:OnChanged(function()
    local args = {
    [1] = "rankup"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
    while Rank.Value do
wait(10)
           end
end) 

local Ability= Tabs.Player:AddToggle("Ability", {Title = "Use ability", Default = false})
Ability:OnChanged(function()
    while Ability.Value do
    local args = {
    [1] = "useAbility"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(1)
           end
end)

local AutoClick= Tabs.Player:AddToggle("AutoClick", {Title = "auto spin Roleta", Default = false})
AutoClick:OnChanged(function()
    while AutoClick.Value do
local args = {
    [1] = "spinWheel"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(15)
           end
end)

local Quest= Tabs.Player:AddToggle("Quest", {Title = "upgrade grimoire 1", Default = false})
Quest:OnChanged(function()
    while Quest.Value do
local args = {
    [1] = "setQuest",
    [2] = "gemsQuest"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(60)
           end
end)
--PLAYER

--UPGRADES
local Grimoire= Tabs.Upgrades:AddToggle("Grimoire", {Title = "upgrade grimoire 1", Default = false})
Grimoire:OnChanged(function()
    while Grimoire.Value do
local args = {
    [1] = "upgradeGrimoire",
    [2] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(2)
           end
end)

local Damage= Tabs.Upgrades:AddToggle ("Damage", {Titlr = "Upgrade Damage", Default = false}) 
Damage:OnChanged(function()
    while Damage.Value do
local args = {
    [1] = "buyUpgrade",
    [2] = "damageBoost"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(2)
  end
    end)
--UPGRADES

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
local StartDefense= Tabs.Defense:AddToggle("StartDefense", {Title = "Start defense", Default = false})

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

local AutoClick= Tabs.Eggs:AddToggle("AutoClick", {Title = "namek", Default = false})
AutoClick:OnChanged(function()
    while AutoClick.Value do
    local args = {
    [1] = "rollChampion",
    [2] = "one",
    [3] = "namek"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))

wait(0)
           end
end)

local AutoClick= Tabs.Eggs:AddToggle("AutoClick", {Title = "sky lands", Default = false})
AutoClick:OnChanged(function()
    while AutoClick.Value do
    local args = {
    [1] = "rollChampion",
    [2] = "one",
    [3] = "sky lands"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))

wait(0)
           end
end)

local AutoClick= Tabs.Eggs:AddToggle("AutoClick", {Title = "shadows city", Default = false})
AutoClick:OnChanged(function()
    while AutoClick.Value do
    local args = {
    [1] = "rollChampion",
    [2] = "one",
    [3] = "shadows city"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))

wait(0)
           end
end)

local AutoClick= Tabs.Eggs:AddToggle("AutoClick", {Title = "cursed school", Default = false})
AutoClick:OnChanged(function()
    while AutoClick.Value do
    local args = {
    [1] = "rollChampion",
    [2] = "one",
    [3] = "cursed school"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(0)
           end
end)

local AutoClick= Tabs.Eggs:AddToggle("AutoClick", {Title = "skull island", Default = false})
AutoClick:OnChanged(function()
    while AutoClick.Value do
    local args = {
    [1] = "rollChampion",
    [2] = "one",
    [3] = "skull island"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(0)
           end
end)

local AutoClick= Tabs.Eggs:AddToggle("AutoClick", {Title = "fortified city", Default = false})
AutoClick:OnChanged(function()
    while AutoClick.Value do
    local args = {
    [1] = "rollChampion",
    [2] = "one",
    [3] = "fortified city"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(0)
           end
end)

--EGGS

--DUNGEON
local easy= Tabs.Dungeon:AddToggle("easy", {Title = "Auto Join easy", Default = false})

easy:OnChanged(function()
    while easy.Value do
local args = {
    [1] = "joinDungeon",
    [2] = "dungeon easy"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(2)
    end
end)

local Medium= Tabs.Dungeon:AddToggle("Medium", {Title = "Auto Join insane", Default = false})

Medium:OnChanged(function() 
    while Medium.Value do
local args = {
    [1] = "joinDungeon",
    [2] = "dungeon medium"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(2)
  end
    end)

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

--RAID
local Jraid= Tabs.Raid:AddToggle("Insane", {Title = "Auto Join Raid", Default = false})

Jraid:OnChanged(function()
    while Jraid.Value do
--remote
local args = {
    [1] = "joinRaid"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(4)
    end
end)
local Jraid= Tabs.Raid:AddToggle("Insane", {Title = "Auto arise", Default = false})

Jraid:OnChanged(function()
    while Jraid.Value do
--remote
local args = {
    [1] = "arise"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(1) 
end
end)



--RAID

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






local args = {
    [1] = "joinDungeon",
    [2] = "dungeon medium"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))



local args = {
    [1] = "setQuest",
    [2] = "gemsQuest"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))











--AUTO SPIN
    Spin:AddButton({
    Title = "Spin sword",
    Callback = function()
local args = {
    [1] = "rollSwords",
    [2] = "one"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))

print("roletado")
    end
})
--AUTO SPIN

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
