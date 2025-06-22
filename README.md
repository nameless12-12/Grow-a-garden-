local gardenArea = workspace:WaitForChild("GardenArea")
local plantTemplate = game.ServerStorage:WaitForChild("Plant")

local plantsToSpawn = 20
local spawnInterval = 2
local maxActivePlants = 50

local function getRandomPosition(area)
	local size = area.Size
	local cf = area.CFrame

	local offset = Vector3.new(
		math.random(-size.X/2, size.X/2),
		0,
		math.random(-size.Z/2, size.Z/2)
	)

	local position = (cf.Position + offset)
	position = Vector3.new(position.X, cf.Position.Y + size.Y/2, position.Z)

	return position
end

local function spawnPlant()
	if #gardenArea:GetChildren() >= maxActivePlants then
		return
	end

	local newPlant = plantTemplate:Clone()
	newPlant.CFrame = CFrame.new(getRandomPosition(gardenArea))
	newPlant.Parent = gardenArea
end

spawn(function()
	for i = 1, plantsToSpawn do
		spawnPlant()
		wait(spawnInterval)
	end
end)
