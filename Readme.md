Sorry for the inexperience of the script, but I haven't learned to run permanent hud in roblox yet, byfron works very well :),

first script:

	local plr = game:GetService"Players".LocalPlayer
	local m = plr:GetMouse()
	m.KeyDown:connect(function(k)
		if k == "v" then
			game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Jumping")
			wait()
			game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Seated")
		end
	end)

second script:

local player = game.Players.LocalPlayer
local userInputService = game:GetService("UserInputService")

userInputService.InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.F then
        local character = player.Character
        if character then
            local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
            local camera = workspace.CurrentCamera
            local forwardVector = camera.CFrame.LookVector
            humanoidRootPart.CFrame = CFrame.new(humanoidRootPart.Position + forwardVector * 30)
        end
    end
end)




last script:

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

local gui = Instance.new("ScreenGui")
local label = Instance.new("TextLabel")
label.Size = UDim2.new(0, 200, 0, 50)
label.Position = UDim2.new(0, 10, 0, 10)
label.Text = ""
label.TextColor3 = Color3.new(1, 0, 0) 
label.FontSize = Enum.FontSize.Size24
label.Parent = gui
gui.Parent = player:WaitForChild("PlayerGui")

local function updateGUI()
    while true do
        if humanoid.Health <= 0 or humanoid.RootPart.Velocity.Y < -115 then
            label.Text = "bruh u will die"
        elseif humanoid.RootPart.Velocity.Y > -115 and humanoid.RootPart.Velocity.Y < 0 then
            label.Text = "nah u live"
           label.TextColor3 = Color3.new(2, 0, 0)
        else
            label.Text = ""
        end
        wait(1) 
    end
end

updateGUI()

gui.AncestryChanged:Connect(function()
    if not gui:IsDescendantOf(player:FindFirstChild("PlayerGui")) then
        gui:Destroy()
    end
end)
