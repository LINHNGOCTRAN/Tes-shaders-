-- BeautifulShader.lua
-- Roblox Lighting Visual Shader System

local Shader = {}

local Lighting = game:GetService("Lighting")

function Shader:Enable()
	
	-- Global Lighting
	Lighting.Brightness = 3
	Lighting.ClockTime = 14
	Lighting.EnvironmentDiffuseScale = 1
	Lighting.EnvironmentSpecularScale = 1
	
	-- Atmosphere
	local atmosphere = Instance.new("Atmosphere")
	atmosphere.Density = 0.35
	atmosphere.Offset = 0
	atmosphere.Color = Color3.fromRGB(199, 199, 255)
	atmosphere.Decay = Color3.fromRGB(106, 112, 125)
	atmosphere.Parent = Lighting

	-- Bloom Effect
	local bloom = Instance.new("BloomEffect")
	bloom.Intensity = 0.8
	bloom.Size = 56
	bloom.Threshold = 1
	bloom.Parent = Lighting

	-- Color Correction
	local color = Instance.new("ColorCorrectionEffect")
	color.Brightness = 0.05
	color.Contrast = 0.2
	color.Saturation = 0.15
	color.TintColor = Color3.fromRGB(255, 244, 214)
	color.Parent = Lighting

	-- Sun Rays
	local sun = Instance.new("SunRaysEffect")
	sun.Intensity = 0.15
	sun.Spread = 1
	sun.Parent = Lighting

	-- Depth of Field
	local dof = Instance.new("DepthOfFieldEffect")
	dof.FarIntensity = 0.1
	dof.FocusDistance = 50
	dof.InFocusRadius = 20
	dof.NearIntensity = 0.2
	dof.Parent = Lighting

end

return Shader
