local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/7yhx/kwargs_Ui_Library/main/source.lua"))()


local Players = game:GetService("Players")
local Workspace = game:GetService("Workspace")

-- Função para criar o círculo e causar dano
local function createDamageCircle(radius, damage)
    local part = Instance.new("Part")
    part.Shape = Enum.PartType.Ball
    part.Size = Vector3.new(radius*2, radius*2, radius*2)
    part.Anchored = true
    part.CanCollide = false
    part.Transparency = 0.5
    part.Color = Color3.fromRGB(255, 0, 0)
    part.Parent = Workspace
    part.Position = Vector3.new(0, 10, 0) -- Ajuste a posição conforme necessário

    -- Função para causar dano aos jogadores
    local function applyDamage()
        for _, player in pairs(Players:GetPlayers()) do
            if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                local distance = (part.Position - player.Character.HumanoidRootPart.Position).magnitude
                if distance <= radius then
                    player.Character.Humanoid:TakeDamage(damage)
                end
            end
        end
    end

    -- Loop para aplicar dano periodicamente
    while true do
        applyDamage()
        wait(1) -- Aplica dano a cada 1 segundo
    end
end

-- Criar um círculo de dano com raio de 10 studs e dano de 10 pontos por segundo
createDamageCircle(10, 10)
