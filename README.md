-- Flee the Facility Script: Teleport, ESP e AutoHack

function teleportToComputer()
    for _, comp in pairs(workspace:GetDescendants()) do
        if comp.Name == "ComputerTable" and comp:FindFirstChild("Hackable") then
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = comp.CFrame + Vector3.new(0, 3, 0)
            wait(1.5)
        end
    end
end

function createESP(object, color)
    local box = Instance.new("BoxHandleAdornment", object)
    box.Size = object.Size
    box.Color3 = color
    box.AlwaysOnTop = true
    box.ZIndex = 10
    box.Adornee = object
    box.Transparency = 0.5
end

function applyESP()
    for _, comp in pairs(workspace:GetDescendants()) do
        if comp.Name == "ComputerTable" then
            createESP(comp, Color3.fromRGB(0, 255, 0))
        end
    end

    for _, player in pairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            local isBeast = player.Backpack:FindFirstChild("BeastPowers") ~= nil
            local color = isBeast and Color3.fromRGB(255, 0, 0) or Color3.fromRGB(0, 255, 0)
            createESP(player.Character.HumanoidRootPart, color)
        end
    end
end

function autoHack()
    for _, comp in pairs(workspace:GetDescendants()) do
        if comp.Name == "ComputerTable" and comp:FindFirstChild("Hackable") then
            fireproximityprompt(comp.Hackable)
            wait(1.5)
        end
    end
end

-- Executar tudo:
applyESP()
teleportToComputer()
autoHack()
