-- Tùy chỉnh tốc độ acid trong game
local acid = workspace:FindFirstChild("Acid") -- Tìm đối tượng Acid
if acid then
    local speed = 5 -- Tốc độ ban đầu của acid

    -- Hàm điều chỉnh tốc độ acid
    local function adjustAcidSpeed(newSpeed)
        speed = newSpeed
        print("Tốc độ acid đã được thay đổi thành:", speed)
    end

    -- Acid di chuyển với tốc độ hiện tại
    game:GetService("RunService").Heartbeat:Connect(function()
        if acid and acid:IsA("Part") then
            acid.Position = acid.Position + Vector3.new(0, speed * 0.01, 0)
        end
    end)

    -- Tạo GUI để điều chỉnh tốc độ acid
    local player = game.Players.LocalPlayer
    local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
    local frame = Instance.new("Frame", screenGui)
    frame.Size = UDim2.new(0, 200, 0, 100)
    frame.Position = UDim2.new(0.5, -100, 0.1, 0)
    frame.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)

    local textLabel = Instance.new("TextLabel", frame)
    textLabel.Size = UDim2.new(1, 0, 0.5, 0)
    textLabel.Text = "Tốc độ Acid: " .. speed
    textLabel.TextColor3 = Color3.new(1, 1, 1)
    textLabel.BackgroundTransparency = 1

    local textBox = Instance.new("TextBox", frame)
    textBox.Size = UDim2.new(1, 0, 0.5, 0)
    textBox.Position = UDim2.new(0, 0, 0.5, 0)
    textBox.PlaceholderText = "Nhập tốc độ mới"
    textBox.Text = ""

    textBox.FocusLost:Connect(function(enterPressed)
        if enterPressed then
            local newSpeed = tonumber(textBox.Text)
            if newSpeed then
                adjustAcidSpeed(newSpeed)
                textLabel.Text = "Tốc độ Acid: " .. speed
                textBox.Text = ""
            else
                textBox.Text = "Không hợp lệ!"
            end
        end
    end)
end
