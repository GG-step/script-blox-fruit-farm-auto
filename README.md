local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local runService = game:GetService("RunService")

local function findTarget()
    local closestTarget = nil
    local shortestDistance = math.huge

    for _, obj in pairs(workspace:GetChildren()) do
        if obj:IsA("Model") and obj:FindFirstChild("Humanoid") and obj.Name ~= character.Name then
            local distance = (obj.HumanoidRootPart.Position - character.HumanoidRootPart.Position).Magnitude
            if distance < shortestDistance then
                closestTarget = obj
                shortestDistance = distance
            end
        end
    end
    return closestTarget
end

-- Função para atacar o mob
local function attackMob(mob)
    local humanoid = mob:FindFirstChild("Humanoid")
    if humanoid then
        -- Substitua este código pela mecânica de dano do seu jogo
        humanoid:TakeDamage(10)  -- Exemplo de dano
    end
end

-- Função principal para mover e atacar
local function autoFarm()
    while true do
        local target = findTarget()
        if target then
            -- Mover para o mob
            character:MoveTo(target.HumanoidRootPart.Position)
            wait(1)  -- Espera para chegar perto
            attackMob(target)  -- Atacar o mob
        end
        wait(0.5)  -- Intervalo entre as verificações
    end
end

-- Iniciar o auto farm
autoFarm()
