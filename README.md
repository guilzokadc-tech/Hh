-- Este é um exemplo genérico de como mostrar um botão quando uma ferramenta é equipada.
-- Deve ser colocado dentro de um LocalScript em StarterPlayerScripts ou dentro de uma ScreenGui.

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local playerGui = player:WaitForChild("PlayerGui")

-- Criando a Interface via Script (Geralmente é feito manualmente no Explorer)
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ExemploUI"
screenGui.Parent = playerGui

local shootButton = Instance.new("TextButton")
shootButton.Size = UDim2.new(0, 100, 0, 50)
shootButton.Position = UDim2.new(1, -120, 0.5, -25) -- Lado direito da tela
shootButton.Text = "SHOOT"
shootButton.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
shootButton.Visible = false -- Começa invisível
shootButton.Parent = screenGui

-- Função para verificar se o jogador está segurando uma ferramenta (ex: "Gun")
local function monitorarFerramenta()
    player.Character.ChildAdded:Connect(function(child)
        if child:IsA("Tool") then
            -- Aqui você verificaria o nome, ex: if child.Name == "Gun" then
            shootButton.Visible = true
        end
    end)

    player.Character.ChildRemoved:Connect(function(child)
        if child:IsA("Tool") then
            shootButton.Visible = false
        end
    end)
end

-- Iniciar monitoramento
if player.Character then
    monitorarFerramenta()
end

player.CharacterAdded:Connect(function(char)
    character = char
    monitorarFerramenta()
end)

-- Lógica do Clique (Apenas para demonstração)
shootButton.MouseButton1Click:Connect(function()
    print("Botão pressionado! Aqui você colocaria a lógica de disparo do seu próprio jogo.")
end)
