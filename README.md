local replicatedStorage = game:GetService("ReplicatedStorage")
local createSpringEvent = replicatedStorage:WaitForChild("CreateSpring")

createSpringEvent.OnServerEvent:Connect(function(player)
    -- Tạo một lò xo dạng coil
    local spring = Instance.new("Part")
    spring.Size = Vector3.new(1, 1, 1)
    spring.Shape = Enum.PartType.Ball
    spring.BrickColor = BrickColor.new("Bright red")
    spring.Material = Enum.Material.SmoothPlastic
    spring.Anchored = true
    spring.CanCollide = false
    spring.Parent = workspace

    -- Sử dụng Mesh để tạo coil
    local mesh = Instance.new("SpecialMesh")
    mesh.MeshType = Enum.MeshType.FileMesh
    mesh.MeshId = "rbxassetid://1051557"
    mesh.Scale = Vector3.new(3, 3, 3)
    mesh.Parent = spring

    -- Đặt vị trí của coil (tại vị trí người chơi)
    local character = player.Character or player.CharacterAdded:Wait()
    spring.Position = character.HumanoidRootPart.Position + Vector3.new(0, 5, 0)

    -- Hiệu ứng lò xo nhảy lên xuống
    local function animateSpring()
        local tweenService = game:GetService("TweenService")
        local info = TweenInfo.new(1, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut, -1, true)
        local goal = {Position = spring.Position + Vector3.new(0, 2, 0)}
        local tween = tweenService:Create(spring, info, goal)
        tween:Play()
    end

    animateSpring()
end)
