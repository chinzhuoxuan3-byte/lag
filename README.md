-- LocalUltraCrashSpawner.lua (LocalScript)
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")

local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local hrp = character:WaitForChild("HumanoidRootPart")

local COUNT = 1000000          -- 每帧 100 万
local LIFETIME = 4
local OFFSET = Vector3.new(0, 5, 0)

RunService.Heartbeat:Connect(function()
    for i = 1, COUNT do
        local sphere = Instance.new("Part")
        sphere.Shape = Enum.PartType.Ball
        sphere.Size = Vector3.new(1, 1, 1)
        sphere.Anchored = false
        sphere.CanCollide = true

        sphere.Position = hrp.Position + OFFSET
        sphere.Velocity = Vector3.new(0, 50, 0)

        sphere.Parent = workspace
        game:GetService("Debris"):AddItem(sphere, LIFETIME)
    end
end)
