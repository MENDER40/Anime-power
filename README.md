# Anime-power

local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local MarketplaceService = game:GetService("MarketplaceService")
local PlaceId = game.PlaceId
local ProductInfo = MarketplaceService:GetProductInfo(PlaceId)
local GameName = ProductInfo.Name

Fluent:Notify({ Title = "Script executado com sucesso", Content = "Você está usando Mender_hub" })

local Window = Fluent:CreateWindow({
    Title = "Mender_hub",
    SubTitle = "-- " .. GameName,
    TabWidth = 102,
    Size = UDim2.fromOffset(450, 320),
    Acrylic = false,
    Theme = "Acrylic",
    MinimizeKey = Enum.KeyCode.LeftControl
})

local Tabs = {
    Main= Window:AddTab({ Title = "| Farm", Icon = "rbxassetid://18831424669" })
}

Window:SelectTab(1)

local autodefense= Tabs.Main:AddToggle("autodefense", {Title = "Auto Join defense", Default = false})

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

local AutoClick= Tabs.Main:AddToggle("AutoClick", {Title = "Auto Click", Default = false})

AutoClick:OnChanged(function()
    while AutoClick.Value do
--remote
local args = {
    [1] = "attack"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
wait(0.2)
    end
end)

local AutoClick= Tabs.Main:AddToggle("AutoClick", {Title = "Auto Join insane", Default = false})

AutoClick:OnChanged(function()
    while AutoClick.Value do
--remote
local args = {
    [1] = "joinDungeon",
    [2] = "dungeon insane"
}

game:GetService("ReplicatedStorage"):WaitForChild("Shared"):WaitForChild("events"):WaitForChild("RemoteEvent"):FireServer(unpack(args))

wait(2)
    end
end)

local AutoClick= Tabs.Main:AddToggle("AutoClick", {Title = "Goo defense", Default = false})

AutoClick:OnChanged(function()
    while AutoClick.Value do
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

local MainTab = Window:AddTab({ Title = "TELEPORT" })

MainTab:AddButton({
    Title = "HALLOWEEN EVENT",
    Callback = function()
        print("✓!")
    end
})
