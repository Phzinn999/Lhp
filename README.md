-- Interface do Script
local ScreenGui = Instance.new("ScreenGui")
local MinimizeButton = Instance.new("TextButton")
local gui = script.Parent -- A janela da interface que você quer mover
local dragging = false
local dragInput, mousePos, framePos

local function update(input)
    local delta = input.Position - mousePos
    gui.Position = UDim2.new(framePos.X.Scale, framePos.X.Offset + delta.X, framePos.Y.Scale, framePos.Y.Offset + delta.Y)
end

gui.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        mousePos = input.Position
        framePos = gui.Position

        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

gui.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

game:GetService("UserInputService").InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        update(input)
    end
end)

local ScrollingFrame = Instance.new("ScrollingFrame")
local Title = Instance.new("TextLabel")
local ESPButton = Instance.new("TextButton")
local SpeedHackButton = Instance.new("TextButton")
local CollectRareItemsButton = Instance.new("TextButton")
local SpeedSlider = Instance.new("TextBox")
local InstantKillButton = Instance.new("TextButton")

-- Propriedades da Interface
ScreenGui.Parent = game.CoreGui

MinimizeButton.Parent = ScreenGui
MinimizeButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
MinimizeButton.Position = UDim2.new(0.05, 0, 0.05, 0)
MinimizeButton.Size = UDim2.new(0, 50, 0, 50)
MinimizeButton.Font = Enum.Font.SourceSans
MinimizeButton.Text = "O"
MinimizeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizeButton.TextSize = 24

ScrollingFrame.Parent = ScreenGui
ScrollingFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
ScrollingFrame.Position = UDim2.new(0.1, 0, 0.1, 0)
ScrollingFrame.Size = UDim2.new(0, 300, 0, 400)
ScrollingFrame.CanvasSize = UDim2.new(0, 0, 1.5, 0) -- Ajuste o valor conforme necessário
ScrollingFrame.ScrollBarThickness = 10
ScrollingFrame.Visible = false

Title.Parent = ScrollingFrame
Title.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
Title.Size = UDim2.new(1, 0, 0, 50)
Title.Font = Enum.Font.SourceSans
Title.Text = "Script Menu"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 24

ESPButton.Parent = ScrollingFrame
ESPButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
ESPButton.Position = UDim2.new(0, 0, 0.2, 0)
ESPButton.Size = UDim2.new(1, 0, 0, 50)
ESPButton.Font = Enum.Font.SourceSans
ESPButton.Text = "ESP (Ver Jogadores)"
ESPButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ESPButton.TextSize = 20

SpeedHackButton.Parent = ScrollingFrame
SpeedHackButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
SpeedHackButton.Position = UDim2.new(0, 0, 0.35, 0)
SpeedHackButton.Size = UDim2.new(1, 0, 0, 50)
SpeedHackButton.Font = Enum.Font.SourceSans
SpeedHackButton.Text = "Speed Hack"
SpeedHackButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SpeedHackButton.TextSize = 20

SpeedSlider.Parent = ScrollingFrame
SpeedSlider.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
SpeedSlider.Position = UDim2.new(0, 0, 0.45, 0)
SpeedSlider.Size = UDim2.new(1, 0, 0, 50)
SpeedSlider.Font = Enum.Font.SourceSans
SpeedSlider.Text = "Digite a Velocidade"
SpeedSlider.TextColor3 = Color3.fromRGB(255, 255, 255)
SpeedSlider.TextSize = 20

CollectRareItemsButton.Parent = ScrollingFrame
CollectRareItemsButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
CollectRareItemsButton.Position = UDim2.new(0, 0, 0.6, 0)
CollectRareItemsButton.Size = UDim2.new(1, 0, 0, 50)
CollectRareItemsButton.Font = Enum.Font.SourceSans
CollectRareItemsButton.Text = "Coletar Itens Raros"
CollectRareItemsButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CollectRareItemsButton.TextSize = 20

InstantKillButton.Parent = ScrollingFrame
InstantKillButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
InstantKillButton.Position = UDim2.new(0, 0, 0.75, 0)
InstantKillButton.Size = UDim2.new(1, 0, 0, 50)
InstantKillButton.Font = Enum.Font.SourceSans
InstantKillButton.Text = "Morte Instantânea"
InstantKillButton.TextColor3 = Color3.fromRGB(255, 255, 255)
InstantKillButton.TextSize = 20

-- Função para minimizar e maximizar a interface
MinimizeButton.MouseButton1Click:Connect(function()
    ScrollingFrame.Visible = not ScrollingFrame.Visible
    MinimizeButton.Text = ScrollingFrame.Visible and "-" or "O"
end)

-- Funções dos Botões
ESPButton.MouseButton1Click:Connect(function()
    local assassinName = "NomeDoAssassino" -- Substitua pelo nome real do assassino
    for _, player in pairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer then
            local esp = Instance.new("BillboardGui", player.Character.Head)
            esp.Size = UDim2.new(3, 0, 3, 0) -- Aumentado para cobrir o corpo inteiro
            esp.AlwaysOnTop = true
            local frame = Instance.new("Frame", esp)
            frame.Size = UDim2.new(1, 0, 1, 0)
            frame.BackgroundTransparency = 0.5
            if player.Name == assassinName then
                frame.BackgroundColor3 = Color3.fromRGB(255, 0, 0) -- Vermelho para o assassino
            else
                frame.BackgroundColor3 = Color3.fromRGB(0, 255, 0) -- Verde para jogadores normais
            end
        end
    end
end)

SpeedHackButton.MouseButton1Click:Connect(function()
    local speed = tonumber(SpeedSlider.Text)
    if speed then
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = speed
    else
        print("Por favor, insira um valor numérico válido.")
    end
end)

CollectRareItemsButton.MouseButton1Click:Connect(function()
    for _, item in pairs(game.Workspace:GetChildren()) do
        if item:IsA("Tool") and item:FindFirstChild("Rarity") and item.Rarity.Value == "Rare" then
            item.Handle.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
        end
    end
end)

InstantKillButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    if player.Backpack:FindFirstChild("Knife") then
        player.Backpack.Knife.Activated:Connect(function()
            local target = player:GetMouse().Target.Parent
            if target and target:FindFirstChild("Humanoid") then
                target.Humanoid.Health = 0
            end
        end)
    else
        print("Faca não encontrada no inventário.")
    end
end)

-- Função para tornar o jogador imortal
game.Players.LocalPlayer.CharacterAdded:Connect(function(character)
    local humanoid = character:WaitForChild("Humanoid")
    humanoid:GetPropertyChangedSignal("Health"):Connect(function()
        if humanoid.Health < humanoid.MaxHealth then
            humanoid.Health = humanoid.MaxHealth
        end
    end)
end)

-- Script para manter a posição de rolagem
local lastCanvasPosition = ScrollingFrame.CanvasPosition
ScrollingFrame.Changed:Connect(function(property)
    if property == "CanvasPosition" then
        lastCanvasPosition = ScrollingFrame.CanvasPosition
    end
end)

ScrollingFrame:GetPropertyChangedSignal("Visible"):Connect(function()
    if ScrollingFrame.Visible then
        ScrollingFrame.CanvasPosition = lastCanvasPosition
    end
end)

