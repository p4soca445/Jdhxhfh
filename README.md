-- Espera o jogo carregar completamente
repeat wait() until game:IsLoaded()

-- Variáveis principais
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
local humanoid = character:FindFirstChildOfClass("Humanoid")
local head = character:WaitForChild("Head")

-- Criação do botão na tela
local ScreenGui = Instance.new("ScreenGui")
local LaserButton = Instance.new("TextButton")

ScreenGui.Parent = game.CoreGui
LaserButton.Parent = ScreenGui
LaserButton.Size = UDim2.new(0, 200, 0, 50)
LaserButton.Position = UDim2.new(0.4, 0, 0.85, 0)  -- Ajuste a posição do botão na tela
LaserButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
LaserButton.TextSize = 20
LaserButton.Text = "Lançar Raio Laser"
LaserButton.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Função para lançar o raio laser dos olhos
local function shootLaser()
    -- Criação do laser
    local laser = Instance.new("Part")
    laser.Size = Vector3.new(0.2, 0.2, 10)  -- Ajuste o tamanho do laser
    laser.Position = head.Position + Vector3.new(0, 1, 0)  -- Posição inicial do laser (saindo dos olhos)
    laser.Anchored = true
    laser.CanCollide = false
    laser.BrickColor = BrickColor.new("Bright red")  -- Cor do laser
    laser.Material = Enum.Material.SmoothPlastic
    laser.Parent = workspace
    
    -- Movimento do laser
    local direction = head.CFrame.LookVector * 50  -- Direção do laser (olhando para frente)
    laser.CFrame = CFrame.new(laser.Position, laser.Position + direction)
    
    -- Criar uma parte de efeito de brilho
    local laserGlow = Instance.new("PointLight")
    laserGlow.Parent = laser
    laserGlow.Range = 15
    laserGlow.Brightness = 5
    
    -- Destroi o laser após 1 segundo
    game:GetService("Debris"):AddItem(laser, 1)
end

-- Ao clicar no botão, dispara o laser
LaserButton.MouseButton1Click:Connect(shootLaser)

-- Mensagem de confirmação
game.StarterGui:SetCore("SendNotification", {
    Title = "Raio Laser Ativado!";
    Text = "Clique no botão para lançar raios laser dos seus olhos.";
    Duration = 5;
})
