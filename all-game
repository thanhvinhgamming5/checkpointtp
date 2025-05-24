local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer

local teleportLoop = false
local teleportDelay = 1
local selectedCheckpoint = nil
local checkpoints = {}

-- Tạo GUI
local gui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
gui.Name = "CheckpointGui"
gui.ResetOnSpawn = false

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 320, 0, 400)
frame.Position = UDim2.new(0, 100, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
frame.BorderSizePixel = 0
frame.Active = true
frame.Draggable = true
frame.Parent = gui

local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0, 30)
title.BackgroundTransparency = 1
title.Text = "Checkpoint Teleport GUI"
title.TextColor3 = Color3.new(1, 1, 1)
title.Font = Enum.Font.SourceSansBold
title.TextSize = 22

-- Nút lưu checkpoint
for i = 1, 4 do
    local saveBtn = Instance.new("TextButton", frame)
    saveBtn.Size = UDim2.new(0.5, -15, 0, 35)
    saveBtn.Position = UDim2.new(0, 10, 0, 40 + (i - 1) * 45)
    saveBtn.BackgroundColor3 = Color3.fromRGB(60, 120, 200)
    saveBtn.TextColor3 = Color3.new(1, 1, 1)
    saveBtn.Text = "📌 Lưu Checkpoint " .. i
    saveBtn.Font = Enum.Font.SourceSansBold
    saveBtn.TextSize = 18

    saveBtn.MouseButton1Click:Connect(function()
        local char = LocalPlayer.Character
        if char and char:FindFirstChild("HumanoidRootPart") then
            checkpoints[i] = char.HumanoidRootPart.Position
            print("Đã lưu vị trí vào Checkpoint", i)
        end
    end)

    local tpBtn = Instance.new("TextButton", frame)
    tpBtn.Size = UDim2.new(0.5, -15, 0, 35)
    tpBtn.Position = UDim2.new(0.5, 5, 0, 40 + (i - 1) * 45)
    tpBtn.BackgroundColor3 = Color3.fromRGB(60, 200, 100)
    tpBtn.TextColor3 = Color3.new(1, 1, 1)
    tpBtn.Text = "🚀 Đến Checkpoint " .. i
    tpBtn.Font = Enum.Font.SourceSansBold
    tpBtn.TextSize = 18

    tpBtn.MouseButton1Click:Connect(function()
        if checkpoints[i] then
            selectedCheckpoint = i
            local char = LocalPlayer.Character
            if char and char:FindFirstChild("HumanoidRootPart") then
                char.HumanoidRootPart.CFrame = CFrame.new(checkpoints[i] + Vector3.new(0, 3, 0))
                print("Dịch chuyển đến Checkpoint", i)
            end
        else
            warn("Checkpoint " .. i .. " chưa được lưu!")
        end
    end)
end

-- Toggle Loop
local loopBtn = Instance.new("TextButton", frame)
loopBtn.Size = UDim2.new(0.5, -15, 0, 40)
loopBtn.Position = UDim2.new(0, 10, 1, -90)
loopBtn.BackgroundColor3 = Color3.fromRGB(255, 170, 0)
loopBtn.TextColor3 = Color3.new(1, 1, 1)
loopBtn.Text = "🔁 Bật Loop"
loopBtn.Font = Enum.Font.SourceSansBold
loopBtn.TextSize = 18
loopBtn.Parent = frame

loopBtn.MouseButton1Click:Connect(function()
    teleportLoop = not teleportLoop
    loopBtn.Text = teleportLoop and "⛔ Tắt Loop" or "🔁 Bật Loop"
    loopBtn.BackgroundColor3 = teleportLoop and Color3.fromRGB(200, 50, 50) or Color3.fromRGB(255, 170, 0)
end)

-- Delay chỉnh
local delayBox = Instance.new("TextBox", frame)
delayBox.Size = UDim2.new(0.5, -15, 0, 40)
delayBox.Position = UDim2.new(0.5, 5, 1, -90)
delayBox.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
delayBox.PlaceholderText = "Thời gian lặp (giây)"
delayBox.Text = tostring(teleportDelay)
delayBox.TextColor3 = Color3.new(1, 1, 1)
delayBox.Font = Enum.Font.SourceSans
delayBox.TextSize = 18
delayBox.ClearTextOnFocus = false

delayBox.FocusLost:Connect(function()
    local value = tonumber(delayBox.Text)
    if value and value >= 0.1 then
        teleportDelay = value
    else
        delayBox.Text = tostring(teleportDelay)
    end
end)

-- Nút đóng GUI
local closeBtn = Instance.new("TextButton", frame)
closeBtn.Size = UDim2.new(1, -20, 0, 30)
closeBtn.Position = UDim2.new(0, 10, 1, -40)
closeBtn.BackgroundColor3 = Color3.fromRGB(180, 50, 50)
closeBtn.TextColor3 = Color3.new(1, 1, 1)
closeBtn.Text = "❌ Đóng GUI"
closeBtn.Font = Enum.Font.SourceSansBold
closeBtn.TextSize = 18

closeBtn.MouseButton1Click:Connect(function()
    teleportLoop = false
    gui:Destroy()
end)

-- Vòng lặp dịch chuyển
task.spawn(function()
    while true do
        task.wait(teleportDelay)
        if teleportLoop and selectedCheckpoint and checkpoints[selectedCheckpoint] then
            local char = LocalPlayer.Character
            if char and char:FindFirstChild("HumanoidRootPart") then
                char.HumanoidRootPart.CFrame = CFrame.new(checkpoints[selectedCheckpoint] + Vector3.new(0, 3, 0))
            end
        end
    end
end)


-- Điều chỉnh thời gian
local timeBox = Instance.new("TextBox", frame)
timeBox.Size = UDim2.new(1, -20, 0, 35)
timeBox.Position = UDim2.new(0, 10, 0, 160)
timeBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
timeBox.PlaceholderText = "⏱️ Thời gian lặp (giây)"
timeBox.TextColor3 = Color3.new(1,1,1)
timeBox.Font = Enum.Font.SourceSans
timeBox.TextSize = 16

-- Nút Tắt GUI
local closeBtn = Instance.new("TextButton", frame)
closeBtn.Size = UDim2.new(0, 30, 0, 30)
closeBtn.Position = UDim2.new(1, -35, 0, 5)
closeBtn.BackgroundColor3 = Color3.fromRGB(180, 60, 60)
closeBtn.Text = "X"
closeBtn.TextColor3 = Color3.new(1,1,1)
closeBtn.Font = Enum.Font.SourceSansBold
closeBtn.TextSize = 16

-- Logic
saveBtn.MouseButton1Click:Connect(function()
	if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
		savedCFrame = LocalPlayer.Character.HumanoidRootPart.CFrame
		print("[✅] Checkpoint đã lưu.")
	end
end)

teleportBtn.MouseButton1Click:Connect(function()
	if savedCFrame and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
		LocalPlayer.Character.HumanoidRootPart.CFrame = savedCFrame
	end
end)

loopBtn.MouseButton1Click:Connect(function()
	looping = not looping
	loopBtn.Text = looping and "🔁 Vòng lặp: BẬT" or "🔁 Vòng lặp: TẮT"
end)

timeBox.FocusLost:Connect(function()
	local val = tonumber(timeBox.Text)
	if val and val > 0 then
		interval = val
		timeBox.Text = ""
	end
end)

closeBtn.MouseButton1Click:Connect(function()
	gui:Destroy()
	print("[🛑] Đã tắt GUI checkpoint.")
end)

-- Vòng lặp dịch chuyển
task.spawn(function()
	while true do
		if looping and savedCFrame and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
			LocalPlayer.Character.HumanoidRootPart.CFrame = savedCFrame
		end
		task.wait(interval)
	end
end)
