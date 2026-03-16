-- BeautifulShader.lua
-- Roblox Lighting Visual Shader System (Phiên bản cải thiện)

local Shader = {}
local Lighting = game:GetService("Lighting")

-- Bảng lưu trữ các effect để có thể xóa sau
local effects = {}

function Shader:Enable()
	-- Xác minh Lighting service
	if not Lighting then
		warn("❌ Không thể lấy Lighting service!")
		return false
	end

	-- Đóng gói trong pcall để xử lý lỗi
	local success, err = pcall(function()
		-- Global Lighting (Giảm Brightness từ 3 xuống 2)
		Lighting.Brightness = 2
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
		table.insert(effects, atmosphere)

		-- Bloom Effect (Giảm Size từ 56 xuống 25)
		local bloom = Instance.new("BloomEffect")
		bloom.Intensity = 0.8
		bloom.Size = 25
		bloom.Threshold = 1
		bloom.Parent = Lighting
		table.insert(effects, bloom)

		-- Color Correction
		local color = Instance.new("ColorCorrectionEffect")
		color.Brightness = 0.05
		color.Contrast = 0.2
		color.Saturation = 0.15
		color.TintColor = Color3.fromRGB(255, 244, 214)
		color.Parent = Lighting
		table.insert(effects, color)

		-- Sun Rays
		local sun = Instance.new("SunRaysEffect")
		sun.Intensity = 0.15
		sun.Spread = 1
		sun.Parent = Lighting
		table.insert(effects, sun)

		-- Depth of Field
		local dof = Instance.new("DepthOfFieldEffect")
		dof.FarIntensity = 0.1
		dof.FocusDistance = 50
		dof.InFocusRadius = 20
		dof.NearIntensity = 0.2
		dof.Parent = Lighting
		table.insert(effects, dof)
		
		print("✅ Shader kích hoạt thành công!")
	end)
	
	if not success then
		warn("❌ Lỗi kích hoạt shader:", err)
		return false
	end
	
	return true
end

function Shader:Disable()
	-- Xóa tất cả effects
	for _, effect in ipairs(effects) do
		if effect and effect.Parent then
			effect:Destroy()
		end
	end
	effects = {}
	print("✅ Shader đã tắt!")
end

-- **QUAN TRỌNG: GỌI HÀM NÀY!**
Shader:Enable()

return Shader
