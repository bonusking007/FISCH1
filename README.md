local TweenService = game:GetService('TweenService')
local object = cre
local tweenInfo = TweenInfo.new(2.5)

while getfenv().RGB do
local r, g, b = math.random(), math.random(), math.random()
local goal = {Color = Color3.new(r, g, b)}

local tween = TweenService:Create(object, tweenInfo, goal)
tween:Play()
tween.Completed:Wait()
end

if game.CoreGui:FindFirstChild("ToggleUI") then
	game.CoreGui:FindFirstChild("ToggleUI"):Destroy()
end
local ToggleUI = Instance.new("ScreenGui")
local ToggleButton = Instance.new("TextButton")
local ToggleButtonHUI = Instance.new("UICorner")
ToggleUI.Name = "ToggleUI"
ToggleUI.Parent = game.CoreGui
ToggleUI.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

ToggleButton.Name = "ToggleButton"
ToggleButton.Parent = ToggleUI
ToggleButton.BackgroundColor3 = Color3.fromRGB(30,20,20)
ToggleButton.BackgroundTransparency = 0.1
ToggleButton.BorderSizePixel = 0
ToggleButton.Position = UDim2.new(0.120833337, 0, 0.0952890813, 0)
ToggleButton.Size = UDim2.new(0, 50, 0, 50)
ToggleButton.Font = Enum.Font.SourceSans
ToggleButton.Text = ""
ToggleButton.TextColor3 = Color3.fromRGB(0, 0, 0)
ToggleButton.TextSize = 14.000
ToggleButton.Draggable = true
ToggleButton.MouseButton1Click:Connect(function()
	game.CoreGui:FindFirstChild("Kenei").Enabled = not game.CoreGui:FindFirstChild("Kenei").Enabled
end)

coroutine.wrap(
	function()
	do
    local CoreGui = {}
    local CheckCoreGui = {}
    local CoreGui = game:GetService("CoreGui"):FindFirstChild("Kenei")
        if CoreGui then 
         CoreGui:Destroy() 
        elseif CoreGui then 
        local CheckCoreGui = not game.CoreGui:FindFirstChild("Kenei").Enabled
            if CheckCoreGui then
            CoreGui:Destroy()
            elseif not CoreGui and CheckCoreGuithen == nil then
                 local CoreGui = nil or {nil}
                 local CheckCoreGu = nil or {nil}
            end
        end
    end
end)();
-- // variables
local library = {}
local pages = {}
local sections = {}
local multisections = {}
local mssections = {}
local toggles = {}
local buttons = {}
local sliders = {}
local dropdowns = {}
local multiboxs = {}
local buttonboxs = {}
local textboxs = {}
local keybinds = {}
local colorpickers = {}
local configloaders = {}
local watermarks = {}
local loaders = {}
--
local utility = {}
--
local plrs = game:GetService("Players")
local cre = game:GetService("CoreGui")
local rs = game:GetService("RunService")
local ts = game:GetService("TweenService") 
local uis = game:GetService("UserInputService") 
local hs = game:GetService("HttpService")
local ws = game:GetService("Workspace")
local plr = plrs.LocalPlayer
local cam = ws.CurrentCamera
-- // indexes
library.__index = library
pages.__index = pages
sections.__index = sections
multisections.__index = multisections
mssections.__index = mssections
toggles.__index = toggles
buttons.__index = buttons
sliders.__index = sliders
dropdowns.__index = dropdowns
multiboxs.__index = multiboxs
buttonboxs.__index = buttonboxs
textboxs.__index = textboxs
keybinds.__index = keybinds
colorpickers.__index = colorpickers
configloaders.__index = configloaders
watermarks.__index = watermarks
loaders.__index = loaders
-- // functions
utility.new = function(instance,properties) 
	-- // instance
	local ins = Instance.new(instance)
	-- // properties setting
	for property,value in pairs(properties) do
		ins[property] = value
	end
	-- // return
	return ins
end
--
utility.dragify = function(ins,touse)
	local dragging
	local dragInput
	local dragStart
	local startPos
	--
	local function update(input)
		local delta = input.Position - dragStart
		touse:TweenPosition(UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y),Enum.EasingDirection.Out,Enum.EasingStyle.Quad,0.1,true)
	end
	--
	ins.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			dragging = true
			dragStart = input.Position
			startPos = touse.Position

			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
				end
			end)
		end
	end)
	--
	ins.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			dragInput = input
		end
	end)
	--
	uis.InputChanged:Connect(function(input)
		if input == dragInput and dragging then
			update(input)
		end
	end)
end
--
utility.round = function(n,d)
	return tonumber(string.format("%."..(d or 0).."f",n))
end
--
utility.zigzag = function(X)
	return math.acos(math.cos(X*math.pi))/math.pi
end
--
utility.capatalize = function(s)
	local l = ""
	for v in s:gmatch('%u') do
		l = l..v
	end
	return l
end
--
utility.splitenum = function(enum)
	local s = tostring(enum):split(".")
	return s[#s]
end
--
utility.from_hex = function(h)
	local r,g,b = string.match(h,"^#?(%w%w)(%w%w)(%w%w)$")
	return Color3.fromRGB(tonumber(r,16), tonumber(g,16), tonumber(b,16))
end
--
utility.to_hex = function(c)
	return string.format("#%02X%02X%02X",c.R *255,c.G *255,c.B *255)
end
--
utility.removespaces = function(s)
   return s:gsub(" ","")
end
-- // main
function library:new(props)
	-- // properties
	local textsize = props.textsize or props.TextSize or props.textSize or props.Textsize or 12
	local font = props.font or props.Font or "RobotoMono"
	local name = props.name or props.Name or props.UiName or props.Uiname or props.uiName or props.username or props.Username or props.UserName or props.userName or "new ui"
	local color = props.color or props.Color or props.mainColor or props.maincolor or props.MainColor or props.Maincolor or props.Accent or props.accent or Color3.fromRGB(225, 58, 81)
	-- // variables
	local window = {}
	-- // main
	local screen = utility.new(
		"ScreenGui",
		{
			Name = "Kenei",
			DisplayOrder = 9999,
			ResetOnSpawn = false,
			ZIndexBehavior = "Global",
			Parent = cre
		}
	)
	-- 1
	local outline = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundColor3 = color,
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderSizePixel = 1,
			Size = UDim2.new(0,541,0,341),
			Position = UDim2.new(0.5,0,0.5,0),
			Parent = screen
		}
	)
	-- 2
	local outline2 = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundColor3 = Color3.fromRGB(0, 0, 0),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderSizePixel = 1,
			Size = UDim2.new(1,-4,1,-4),
			Position = UDim2.new(0.5,0,0.5,0),
			Parent = outline
		}
	)
	-- 3
	local indent = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundColor3 = Color3.fromRGB(20, 20, 20),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0.5,0,0.5,0),
			Parent = outline2
		}
	)
	-- 4
	local main = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,1),
			BackgroundColor3 = Color3.fromRGB(20, 20, 20),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,-10,1,-25),
			Position = UDim2.new(0.5,0,1,-5),
			Parent = outline2
		}
	)
	--
	local title = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,20),
			Position = UDim2.new(0.5,0,0,0),
			Parent = outline2
		}
	)
	-- 5
	local outline3 = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0.5,0,0.5,0),
			Parent = main
		}
	)
	--
	local titletext = utility.new(
		"TextLabel",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-10,1,0),
			Position = UDim2.new(0.5,0,0,0),
			Font = font,
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextXAlignment = "Left",
			TextSize = textsize,
			TextStrokeTransparency = 0,
			Parent = title
		}
	)
	-- 6
	local holder = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-6,1,-6),
			Position = UDim2.new(0.5,0,0.5,0),
			Parent = main
		}
	)
	-- 7
	local holder = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-6,1,-6),
			Position = UDim2.new(0.5,0,0.5,0),
			Parent = main
		}
	)
	-- 8
	local tabs = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,1),
			BackgroundColor3 = Color3.fromRGB(20, 20, 20),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,-20),
			Position = UDim2.new(0.5,0,1,0),
			Parent = holder
		}
	)
	--
	local tabsbuttons = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,21),
			Position = UDim2.new(0.5,0,0,0),
			ZIndex = 2,
			Parent = holder
		}
	)
	-- 9
	local outline4 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(20, 20, 20),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Parent = tabs
		}
	)
	--
	utility.new(
		"UIListLayout",
		{
			FillDirection = "Horizontal",
			Padding = UDim.new(0,2),
			Parent = tabsbuttons
		}
	)
	--
	utility.dragify(title,outline)
	-- // window tbl
	window = {
		["screen"] = screen,
		["holder"] = holder,
		["labels"] = {},
		["tabs"] = outline4,
		["tabsbuttons"] = tabsbuttons,
		["outline"] = outline,
		["pages"] = {},
		["pointers"] = {},
		["dropdowns"] = {},
		["multiboxes"] = {},
		["buttonboxs"] = {},
		["colorpickers"] = {},
		["x"] = true,
		["y"] = true,
		["key"] = Enum.KeyCode.RightShift,
		["textsize"] = textsize,
		["font"] = font,
		["theme"] = {
			["accent"] = color
		},
		["themeitems"] = {
			["accent"] = {
				["BackgroundColor3"] = {},
				["BorderColor3"] = {},
				["TextColor3"] = {}
			}
		}
	}
	--
	table.insert(window.themeitems["accent"]["BackgroundColor3"],outline)
	--
	local toggled = true
	local cooldown = false
	local saved = UDim2.new(0,0,0,0)
	--
	uis.InputBegan:Connect(function(Input)
		if Input.UserInputType == Enum.UserInputType.Keyboard then
			if Input.KeyCode == window.key then
				if cooldown == false then
					if toggled then
						cooldown = true
						toggled = not toggled
						saved = outline.Position
						local xx,yy = 0,0
						local xxx,yyy = 0,0
						--
						if (outline.AbsolutePosition.X+(outline.AbsoluteSize.X/2)) < (cam.ViewportSize.X/2) then
							xx = -3
						else
							xx = 3
						end
						--
						if window.y then
							if (outline.AbsolutePosition.Y+(outline.AbsoluteSize.Y/2)) < (cam.ViewportSize.Y/2) then
								yy = -3
							else
								yy = 3
							end
						else
							yy = saved.Y.Scale
							yyy = saved.Y.Offset
						end
						--
						if window.x == false and window.y == false then
							screen.Enabled = false
						else
							ts:Create(outline, TweenInfo.new(0.5,Enum.EasingStyle.Quad,Enum.EasingDirection.In), {Position = UDim2.new(xx,xxx,yy,yyy)}):Play()
						end
						wait(0.5)
						cooldown = false
					else
						cooldown = true
						toggled = not toggled
						if window.x == false and window.y == false then
							screen.Enabled = true
						else
							ts:Create(outline, TweenInfo.new(0.5,Enum.EasingStyle.Quad,Enum.EasingDirection.Out), {Position = saved}):Play()
						end
						wait(0.5)
						cooldown = false
					end
				end
			end
		end
	end)
	--
	window.labels[#window.labels+1] = titletext
	-- // metatable indexing + return
	setmetatable(window, library)
	return window
end
--
function library:watermark()
	local watermark = {}
	--
	local outline = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(1,0),
			BackgroundColor3 = self.theme.accent,
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderSizePixel = 1,
			Size = UDim2.new(0,300,0,26),
			Position = UDim2.new(1,-10,0,10),
			ZIndex = 9900,
			Visible = false,
			Parent = self.screen
		}
	)
	--
	table.insert(self.themeitems["accent"]["BackgroundColor3"],outline)
	--
	local outline2 = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundColor3 = Color3.fromRGB(0, 0, 0),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderSizePixel = 1,
			Size = UDim2.new(1,-4,1,-4),
			Position = UDim2.new(0.5,0,0.5,0),
			ZIndex = 9901,
			Parent = outline
		}
	)
	--
	local indent = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundColor3 = Color3.fromRGB(20, 20, 20),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0.5,0,0.5,0),
			ZIndex = 9902,
			Parent = outline2
		}
	)
	--
	local title = utility.new(
		"TextLabel",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-10,1,0),
			Position = UDim2.new(0.5,0,0,0),
			Font = self.font,
			Text = "",
			TextColor3 = Color3.fromRGB(255,255,255),
			TextXAlignment = "Left",
			TextSize = self.textsize,
			TextStrokeTransparency = 0,
			ZIndex = 9903,
			Parent = indent
		}
	)
	--
	local con
	con = title:GetPropertyChangedSignal("TextBounds"):Connect(function()
		outline.Size = UDim2.new(0,title.TextBounds.X+20,0,26)
	end)
	--
	watermark = {
		["outline"] = outline,
		["outline2"] = outline2,
		["indent"] = indent,
		["title"] = title,
		["connection"] = con
	}
	--
	self.labels[#self.labels+1] = title
	--
	setmetatable(watermark,watermarks)
	return watermark
end
--
function watermarks:update(content)
	local content = content or {}
	local watermark = self
	--
	local text = ""
	--
	for i,v in pairs(content) do
		text = text..i..": "..v.."  "
	end
	--
	text = text:sub(0, -3)
	--
	watermark.title.Text = text
end
--
function watermarks:updateside(side)
	side = utility.removespaces(tostring(side):lower())
	--
	local sides = {
		topright = {
			AnchorPoint = Vector2.new(1,0),
			Position = UDim2.new(1,-10,0,10)
		},
		topleft = {
			AnchorPoint = Vector2.new(0,0),
			Position = UDim2.new(0,10,0,10)
		},
		bottomright = {
			AnchorPoint = Vector2.new(1,1),
			Position = UDim2.new(1,-10,1,-10)
		},
		bottomleft = {
			AnchorPoint = Vector2.new(0,1),
			Position = UDim2.new(0,10,1,-10)
		}
	}
	--
	if sides[side] then
		self.outline.AnchorPoint = sides[side].AnchorPoint
		self.outline.Position = sides[side].Position
	end
end
--
function library:loader(props)
	local name = props.name or props.Name or props.LoaderName or props.Loadername or props.loaderName or props.loadername or "Loader"
	local scriptname = props.scriptname or props.Scriptname or props.ScriptName or props.scriptName or "Universal"
	local closed = props.close or props.Close or props.closecallback or props.Closecallback or props.CloseCallback or props.closeCallback or function()end
	local logedin = props.login or props.Login or props.logincallback or props.Logincallback or props.LoginCallback or props.loginCallback or function()end
	local loader = {}
	--
	local screen = utility.new(
		"ScreenGui",
		{
			Name = tostring(math.random(0,999999))..tostring(math.random(0,999999)),
			DisplayOrder = 9999,
			ResetOnSpawn = false,
			ZIndexBehavior = "Global",
			Parent = cre
		}
	)
	local outline = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundColor3 = Color3.fromRGB(168, 52, 235),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderSizePixel = 1,
			Size = UDim2.new(0,300,0,90),
			Position = UDim2.new(0.5,0,0.5,0),
			ZIndex = 9900,
			Visible = false,
			Parent = screen
		}
	)
	--
	local outline2 = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundColor3 = Color3.fromRGB(0, 0, 0),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderSizePixel = 1,
			Size = UDim2.new(1,-4,1,-4),
			Position = UDim2.new(0.5,0,0.5,0),
			ZIndex = 9901,
			Parent = outline
		}
	)
	--
	local indent = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundColor3 = Color3.fromRGB(20, 20, 20),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0.5,0,0.5,0),
			ZIndex = 9902,
			Parent = outline2
		}
	)
	--
	local title = utility.new(
		"TextLabel",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-10,0,20),
			Position = UDim2.new(0.5,0,0,0),
			Font = "RobotoMono",
			Text = name,
			TextColor3 = Color3.fromRGB(168, 52, 235),
			TextXAlignment = "Center",
			TextSize = 12,
			TextStrokeTransparency = 0,
			ZIndex = 9903,
			Parent = indent
		}
	)
	--
	local scripttitle = utility.new(
		"TextLabel",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-10,0,20),
			Position = UDim2.new(0.5,0,0,20),
			Font = "RobotoMono",
			Text = "Script: "..scriptname,
			TextColor3 = Color3.fromRGB(255, 255, 255),
			TextXAlignment = "Center",
			TextSize = 12,
			TextStrokeTransparency = 0,
			ZIndex = 9903,
			Parent = indent
		}
	)
	--
	local makebutton = function(name,parent)
		local button_holder = utility.new(
			"Frame",
			{
				BackgroundTransparency = 1,
				BorderSizePixel = 0,
				ZIndex = 9904,
				Parent = parent
			}
		)
		--
		local button_outline = utility.new(
			"Frame",
			{
				BackgroundColor3 = Color3.fromRGB(24, 24, 24),
				BorderColor3 = Color3.fromRGB(12, 12, 12),
				BorderMode = "Inset",
				BorderSizePixel = 1,
				Position = UDim2.new(0,0,0,0),
				Size = UDim2.new(1,0,1,0),
				ZIndex = 9905,
				Parent = button_holder
			}
		)
		--
		local button_outline2 = utility.new(
			"Frame",
			{
				BackgroundColor3 = Color3.fromRGB(24, 24, 24),
				BorderColor3 = Color3.fromRGB(56, 56, 56),
				BorderMode = "Inset",
				BorderSizePixel = 1,
				Position = UDim2.new(0,0,0,0),
				Size = UDim2.new(1,0,1,0),
				ZIndex = 9906,
				Parent = button_outline
			}
		)
		--
		local button_color = utility.new(
			"Frame",
			{
				AnchorPoint = Vector2.new(0,0),
				BackgroundColor3 = Color3.fromRGB(30, 30, 30),
				BorderSizePixel = 0,
				Size = UDim2.new(1,0,0,0),
				Position = UDim2.new(0,0,0,0),
				ZIndex = 9907,
				Parent = button_outline2
			}
		)
		--
		utility.new(
			"UIGradient",
			{
				Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
				Rotation = 90,
				Parent = button_color
			}
		)
		--
		local button_button = utility.new(
			"TextButton",
			{
				AnchorPoint = Vector2.new(0,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,0,1,0),
				Position = UDim2.new(0,0,0,0),
				Text = name,
				TextColor3 = Color3.fromRGB(255,255,255),
				TextSize = 12,
				TextStrokeTransparency = 0,
				Font = "RobotoMono",
				ZIndex = 9908,
				Parent = button_holder
			}
		)
		--
		return {button_holder,button_outline,button_button}
	end
	--
	local close = makebutton("close",indent)
	local login = makebutton("login",indent)
	--
	close[1].AnchorPoint = Vector2.new(0.5,0)
	close[1].Size = UDim2.new(0.5,0,0,20)
	close[1].Position = UDim2.new(0.5,0,0,40)
	--
	login[1].AnchorPoint = Vector2.new(0.5,0)
	login[1].Size = UDim2.new(0.5,0,0,20)
	login[1].Position = UDim2.new(0.5,0,0,62)
	--
	close[3].MouseButton1Down:Connect(function()
		close[2].BorderColor3 = Color3.fromRGB(168, 52, 235)
		outline:TweenPosition(UDim2.new(-1.5,0,0.5,0),Enum.EasingDirection.Out,Enum.EasingStyle.Quad,0.75,true)
		closed()
		wait(0.05)
		close[2].BorderColor3 = Color3.fromRGB(12,12,12)
		wait(0.7)
		screen:Remove()
	end)
	--
	login[3].MouseButton1Down:Connect(function()
		login[2].BorderColor3 = Color3.fromRGB(168, 52, 235)
		outline:TweenPosition(UDim2.new(1.5,0,0.5,0),Enum.EasingDirection.Out,Enum.EasingStyle.Quad,0.75,true)
		logedin()
		wait(0.05)
		login[2].BorderColor3 = Color3.fromRGB(12,12,12)
		wait(0.7)
		screen:Remove()
	end)
	--
	loader = {
		["outline"] = outline,
		["outline2"] = outline2,
		["indent"] = indent,
		["title"] = title
	}
	--
	setmetatable(loader,loaders)
	return loader
end
--
function loaders:toggle()
	self.outline.Visible = true
end
--
function watermarks:toggle(bool)
	local watermark = self
	--
	watermark.outline.Visible = bool
end
--
function library:saveconfig()
	local cfg = {}
	--
	for i,v in pairs(self.pointers) do
		cfg[i] = {}
		for c,d in pairs(v) do
			cfg[i][c] = {}
			for x,z in pairs(d) do
				if typeof(z.current) == "Color3" then
					cfg[i][c][x] = {z.current.R,z.current.G,z.current.B}
				else
					cfg[i][c][x] = z.current
				end
			end
		end
	end
	--
	return hs:JSONEncode(cfg)
end
--
function library:loadconfig(cfg)
	local cfg = hs:JSONDecode(readfile(cfg))
	for i,v in pairs(cfg) do
		for c,d in pairs(v) do
			for x,z in pairs(d) do
				if z ~= nil then
					if self.pointers[i] ~= nil and self.pointers[i][c] ~= nil and self.pointers[i][c][x] ~= nil then
						self.pointers[i][c][x]:set(z)
					end
				end
			end
		end
	end
end
--
function library:settheme(theme,color)
	local window = self
	--
	if window.theme[theme] then
		window.theme[theme] = color
	end
	--
	if window.themeitems[theme] then
		for i,v in pairs(window.themeitems[theme]) do
			for z,x in pairs(v) do
				x[i] = color
			end
		end
	end
end
--
function library:setkey(key)
	if typeof(key) == "EnumItem" then
		local window = self
		window.key = key
	end
end
--
function library:settoggle(side,bool)
	if side == "x" then
		self.x = bool
	else
		self.y = bool
	end
end
--
function library:setfont(font)
	if font ~= nil then
		local window = self
		for i,v in pairs(window.labels) do
			if v ~= nil then
				v.Font = font
			end
		end
	end
end
--
function library:settextsize(size)
	if size ~= nil then
		local window = self
		for i,v in pairs(window.labels) do
			if v ~= nil then
				v.TextSize = size
			end
		end
	end
end
--
function library:page(props)
	-- // properties
	local name = props.name or props.Name or props.page or props.Page or props.pagename or props.Pagename or props.PageName or props.pageName or "new ui"
	-- // variables
	local page = {}
	-- // main
	local tabbutton = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(20, 20, 20),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(0,75,1,0),
			Parent = self.tabsbuttons
		}
	)
	--
	local outline = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Parent = tabbutton
		}
	)
	--
	local button = utility.new(
		"TextButton",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Text = "",
			Parent = tabbutton
		}
	)
	--
	local r_line = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(56, 56, 56),
			BorderSizePixel = 0,
			Size = UDim2.new(0,1,0,1),
			Position = UDim2.new(1,0,1,1),
			ZIndex = 2,
			Parent = outline
		}
	)
	--
	local l_line = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(1,0),
			BackgroundColor3 = Color3.fromRGB(56, 56, 56),
			BorderSizePixel = 0,
			Size = UDim2.new(0,1,0,1),
			Position = UDim2.new(0,0,1,1),
			ZIndex = 2,
			Parent = outline
		}
	)
	--
	local line = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,0,2),
			Position = UDim2.new(0,0,1,0),
			ZIndex = 2,
			Parent = outline
		}
	)
	--
	local label = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,20),
			Position = UDim2.new(0,0,0,0),
			Font = self.font,
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.textsize,
			TextStrokeTransparency = 0,
			Parent = outline
		}
	)
	--
	local pageholder = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-20,1,-20),
			Position = UDim2.new(0.5,0,0.5,0),
			Visible = false,
			Parent = self.tabs
		}
	)
	--
	local left = utility.new(
		"ScrollingFrame",
		{
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Size = UDim2.new(0.5,-5,1,0),
			Position = UDim2.new(0,0,0,0),
			AutomaticCanvasSize = "Y",
			CanvasSize = UDim2.new(0,0,0,0),
			ScrollBarImageTransparency = 1,
			ScrollBarImageColor3 = Color3.fromRGB(0,0,0),
			ScrollBarThickness = 0,
			ClipsDescendants = true,
			VerticalScrollBarInset = "None",
			VerticalScrollBarPosition = "Right",
			Parent = pageholder
		}
	)
	--
	utility.new(
		"UIListLayout",
		{
			FillDirection = "Vertical",
			Padding = UDim.new(0,10),
			Parent = left
		}
	)
	--
	local right = utility.new(
		"ScrollingFrame",
		{
			AnchorPoint = Vector2.new(1,0),
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Size = UDim2.new(0.5,-5,1,0),
			Position = UDim2.new(1,0,0,0),
			AutomaticCanvasSize = "Y",
			CanvasSize = UDim2.new(0,0,0,0),
			ScrollBarImageTransparency = 1,
			ScrollBarImageColor3 = Color3.fromRGB(0,0,0),
			ScrollBarThickness = 0,
			ClipsDescendants = true,
			VerticalScrollBarInset = "None",
			VerticalScrollBarPosition = "Right",
			Parent = pageholder
		}
	)
	--
	utility.new(
		"UIListLayout",
		{
			FillDirection = "Vertical",
			Padding = UDim.new(0,10),
			Parent = right
		}
	)
	-- // page tbl
	page = {
		["library"] = self,
		["outline"] = outline,
		["r_line"] = r_line,
		["l_line"] = l_line,
		["line"] = line,
		["page"] = pageholder,
		["left"] = left,
		["right"] = right,
		["open"] = false,
		["pointers"] = {}
	}
	--
	table.insert(self.pages,page)
	--
	button.MouseButton1Down:Connect(function()
		if page.open == false then
			for i,v in pairs(self.pages) do
				if v ~= page then
					if v.open then
						v.page.Visible = false
						v.open = false
						v.outline.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
						v.line.Size = UDim2.new(1,0,0,2)
						v.line.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
					end
				end
			end
			--
			self:closewindows()
			--
			page.page.Visible = true
			page.open = true
			page.outline.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
			page.line.Size = UDim2.new(1,0,0,3)
			page.line.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
		end
	end)
	--
	local pointer = props.pointer or props.Pointer or props.pointername or props.Pointername or props.PointerName or props.pointerName or nil
	--
	if pointer then
		self.pointers[tostring(pointer)] = page.pointers
	end
	--
	self.labels[#self.labels+1] = label
	-- // metatable indexing + return
	setmetatable(page, pages)
	return page
end
--
function pages:openpage()
	local page = self
	--
	if page.open == false then
		for i,v in pairs(page.library.pages) do
			if v ~= page then
				if v.open then
					v.page.Visible = false
					v.open = false
					v.outline.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
					v.line.Size = UDim2.new(1,0,0,2)
					v.line.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
				end
			end
		end
		--
		page.page.Visible = true
		page.open = true
		page.outline.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
		page.line.Size = UDim2.new(1,0,0,3)
		page.line.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
	end
end
--
function pages:section(props)
	-- // properties
	local name = props.name or props.Name or props.page or props.Page or props.pagename or props.Pagename or props.PageName or props.pageName or "new ui"
	local side = props.side or props.Side or props.sectionside or props.Sectionside or props.SectionSide or props.sectionSide or "left"
	local size = props.size or props.Size or props.yaxis or props.yAxis or props.YAxis or props.Yaxis or 200
	side = side:lower()
	-- // variables
	local section = {}
	-- // main
	local sectionholder = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,0,size),
			Parent = self[side]
		}
	)

	--[[BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Size = UDim2.new(0.5,-5,1,0),
			Position = UDim2.new(0,0,0,0),
			AutomaticCanvasSize = "Y",
			CanvasSize = UDim2.new(0,0,0,0),
			ScrollBarImageTransparency = 1,
			ScrollBarImageColor3 = Color3.fromRGB(0,0,0),
			ScrollBarThickness = 0,
			ClipsDescendants = false,
			VerticalScrollBarInset = "None",
			VerticalScrollBarPosition = "Right",
			Parent = pageholder
		}]]
	local outline = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Parent = sectionholder
		}
	)
	--
	local color = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundColor3 = self.library.theme.accent,
			BorderSizePixel = 0,
			Size = UDim2.new(1,-2,0,1),
			Position = UDim2.new(0.5,0,0,0),
			Parent = outline
		}
	)
	--
	table.insert(self.library.themeitems["accent"]["BackgroundColor3"],color)
	--
	--[[local content = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,1),
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Size = UDim2.new(1,-12,1,-25),
			Position = UDim2.new(0.5,0,1,-5),
			Parent = outline
		}
	)]]

	local content = utility.new(
		'Frame',
		{
			AnchorPoint = Vector2.new(0.5,1),
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Size = UDim2.new(1,-12,1,-25),
			Position = UDim2.new(0.5,0,1,-5),
			ClipsDescendants = true,
			Parent = outline
		}
	)
	
	--
	local title = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-5,0,20),
			Position = UDim2.new(0,5,0,0),
			Font = self.library.font,
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Center",
			Parent = outline
		}
	)
	--
	utility.new(
		"UIListLayout",
		{
			FillDirection = "Vertical",
			Padding = UDim.new(0,5),
			Parent = content
		}
	)
	-- // section tbl
	section = {
		["library"] = self.library,
		["sectionholder"] = sectionholder,
		["color"] = color,
		["content"] = content,
		["pointers"] = {}
	}
	--
	local pointer = props.pointer or props.Pointer or props.pointername or props.Pointername or props.PointerName or props.pointerName or nil
	--
	if pointer then
		if self.pointers then
			self.pointers[tostring(pointer)] = section.pointers
		end
	end
	--
	self.library.labels[#self.library.labels+1] = title
	-- // metatable indexing + return
	setmetatable(section, sections)
	return section
end
--
function pages:multisection(props)
	-- // properties
	local name = props.name or props.Name or props.page or props.Page or props.pagename or props.Pagename or props.PageName or props.pageName or "new ui"
	local side = props.side or props.Side or props.sectionside or props.Sectionside or props.SectionSide or props.sectionSide or "left"
	local size = props.size or props.Size or props.yaxis or props.yAxis or props.YAxis or props.Yaxis or 200
	side = side:lower()
	-- // variables
	local multisection = {}
	-- // main
	local sectionholder = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,0,size),
			Parent = self[side]
		}
	)
	--
	local outline = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Parent = sectionholder
		}
	)
	--
	local color = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundColor3 = self.library.theme.accent,
			BorderSizePixel = 0,
			Size = UDim2.new(1,-2,0,1),
			Position = UDim2.new(0.5,0,0,0),
			Parent = outline
		}
	)
	--
	table.insert(self.library.themeitems["accent"]["BackgroundColor3"],color)
	--
	local tabsholder = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0,1),
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,1,-15),
			Position = UDim2.new(0,0,1,0),
			Parent = outline
		}
	)
	--
	local title = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-5,0,20),
			Position = UDim2.new(0,5,0,0),
			Font = self.library.font,
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Left",
			Parent = outline
		}
	)
	--
	local buttons = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Size = UDim2.new(1,-6,0,20),
			Position = UDim2.new(0.5,0,0,5),
			Parent = tabsholder
		}
	)
	--
	local tabs = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,1),
			BackgroundColor3 = Color3.fromRGB(20, 20, 20),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,-6,1,-27),
			Position = UDim2.new(0.5,0,1,-3),
			Parent = tabsholder
		}
	)
	--
	utility.new(
		"UIListLayout",
		{
			FillDirection = "Horizontal",
			Padding = UDim.new(0,2),
			Parent = buttons
		}
	)
	--
	local tabs_outline = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Parent = tabs
		}
	)
	-- // section tbl
	multisection = {
		["library"] = self.library,
		["sectionholder"] = sectionholder,
		["color"] = color,
		["tabsholder"] = tabsholder,
		["mssections"] = {},
		["buttons"] = buttons,
		["tabs"] = tabs,
		["tabs_outline"] = tabs_outline,
		["pointers"] = {}
	}
	--
	local pointer = props.pointer or props.Pointer or props.pointername or props.Pointername or props.PointerName or props.pointerName or nil
	--
	if pointer then
		if self.pointers then
			self.pointers[tostring(pointer)] = multisection.pointers
		end
	end
	--
	self.library.labels[#self.library.labels+1] = title
	-- // metatable indexing + return
	setmetatable(multisection,multisections)
	return multisection
end
--
function multisections:section(props)
	local name = props.name or props.Name or props.page or props.Page or props.pagename or props.Pagename or props.PageName or props.pageName or "new ui"
	-- // variables
	local mssection = {}
	-- // main
	local tabbutton = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(20, 20, 20),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(0,60,0,20),
			Parent = self.buttons
		}
	)
	--
	local outline = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(20, 20, 20),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Parent = tabbutton
		}
	)
	--
	local button = utility.new(
		"TextButton",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Text = "",
			Parent = tabbutton
		}
	)
	--
	local r_line = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(56, 56, 56),
			BorderSizePixel = 0,
			Size = UDim2.new(0,1,0,1),
			Position = UDim2.new(1,0,1,1),
			ZIndex = 2,
			Parent = outline
		}
	)
	--
	local l_line = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(1,0),
			BackgroundColor3 = Color3.fromRGB(56, 56, 56),
			BorderSizePixel = 0,
			Size = UDim2.new(0,1,0,1),
			Position = UDim2.new(0,0,1,1),
			ZIndex = 2,
			Parent = outline
		}
	)
	--
	local line = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(20, 20, 20),
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,0,2),
			Position = UDim2.new(0,0,1,0),
			ZIndex = 2,
			Parent = outline
		}
	)
	--
	local label = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,20),
			Position = UDim2.new(0,0,0,0),
			Font = self.library.font,
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			Parent = outline
		}
	)
	--
	local content = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,1),
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Size = UDim2.new(1,-6,1,-27),
			Position = UDim2.new(0.5,0,1,-3),
			Parent = self.tabs_outline
		}
	)
	--
	utility.new(
		"UIListLayout",
		{
			FillDirection = "Vertical",
			Padding = UDim.new(0,5),
			Parent = content
		}
	)
	-- // mssection tbl
	mssection = {
		["library"] = self.library,
		["outline"] = outline,
		["r_line"] = r_line,
		["l_line"] = l_line,
		["line"] = line,
		["content"] = content,
		["open"] = false,
		["pointers"] = {}
	}
	--
	table.insert(self.mssections,mssection)
	--
	button.MouseButton1Down:Connect(function()
		if mssection.open == false then
			for i,v in pairs(self.mssections) do
				if v ~= mssection then
					if v.open then
						v.page.Visible = false
						v.open = false
						v.outline.BackgroundColor3 = Color3.fromRGB(31, 31 ,31)
						v.line.Size = UDim2.new(1,0,0,2)
						v.line.BackgroundColor3 = Color3.fromRGB(31, 31 ,31)
					end
				end
			end
			--
			mssection.library:closewindows()
			--
			mssection.content.Visible = true
			mssection.open = true
			mssection.outline.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
			mssection.line.Size = UDim2.new(1,0,0,3)
			mssection.line.BackgroundColor3 = Color3.fromRGB(24, 24, 24)
		end
	end)
	--
	local pointer = props.pointer or props.Pointer or props.pointername or props.Pointername or props.PointerName or props.pointerName or nil
	--
	if pointer then
		if self.pointers then
			self.pointers[tostring(pointer)] = mssection.pointers
		end
	end
	--
	self.library.labels[#self.library.labels+1] = label
	-- // metatable indexing + return
	setmetatable(mssection,mssections)
	return mssection
end
--
function sections:toggle(props)
	-- // properties
	local name = props.name or props.Name or props.page or props.Page or props.pagename or props.Pagename or props.PageName or props.pageName or "new ui"
	local def = props.def or props.Def or props.default or props.Default or props.toggle or props.Toggle or props.toggled or props.Toggled or false
	local callback = props.callback or props.callBack or props.CallBack or props.Callback or function()end
	-- // variables
	local toggle = {}
	-- // main
	local toggleholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,15),
			Parent = self.content
		}
	)
	--
	local outline = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(0,15,0,15),
			Parent = toggleholder
		}
	)
	--
	local button = utility.new(
		"TextButton",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Text = "",
			Parent = toggleholder
		}
	)
	--
	local title = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-20,1,0),
			Position = UDim2.new(0,20,0,0),
			Font = self.library.font,
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Left",
			Parent = toggleholder
		}
	)
	--
	local col = Color3.fromRGB(20, 20, 20)
	if def then
		col = self.library.theme.accent
	end
	--
	local color = utility.new(
		"Frame",
		{
			BackgroundColor3 = col,
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Parent = outline
		}
	)
	if def then
		table.insert(self.library.themeitems["accent"]["BackgroundColor3"],color)
	end
	--
	utility.new(
		"UIGradient",
		{
			Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
			Rotation = 90,
			Parent = color
		}
	)
	-- // toggle tbl
	toggle = {
		["library"] = self.library,
		["toggleholder"] = toggleholder,
		["title"] = title,
		["color"] = color,
		["callback"] = callback,
		["current"] = def
	}
	--
	button.MouseButton1Down:Connect(function()
		if toggle.current then
			toggle.callback(false)
			toggle.color.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
			local find = table.find(self.library.themeitems["accent"]["BackgroundColor3"],toggle.color)
			if find then
				table.remove(self.library.themeitems["accent"]["BackgroundColor3"],find)
			end
			toggle.current = false
		else
			toggle.callback(true)
			toggle.color.BackgroundColor3 = self.library.theme.accent
			table.insert(self.library.themeitems["accent"]["BackgroundColor3"],toggle.color)
			toggle.current = true
		end
	end)
	--
	local pointer = props.pointer or props.Pointer or props.pointername or props.Pointername or props.PointerName or props.pointerName or nil
	--
	if pointer then
		if self.pointers then
			self.pointers[tostring(pointer)] = toggle
		end
	end
	--
	self.library.labels[#self.library.labels+1] = title
	-- // metatable indexing + return
	setmetatable(toggle, toggles)
	return toggle
end
--
function toggles:set(bool)
	if bool ~= nil then
		local toggle = self
		toggle.callback(bool)
		toggle.current = bool
		if bool then
			toggle.color.BackgroundColor3 = self.library.theme.accent
			table.insert(self.library.themeitems["accent"]["BackgroundColor3"],toggle.color)
		else
			toggle.color.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
			local find = table.find(self.library.themeitems["accent"]["BackgroundColor3"],toggle.color)
			if find then
				table.remove(self.library.themeitems["accent"]["BackgroundColor3"],find)
			end
		end
	end
end
--
function sections:button(props)
	-- // properties
	local name = props.name or props.Name or "new button"
	local callback = props.callback or props.callBack or props.CallBack or props.Callback or function()end
	-- // variables
	local button = {}
	-- // main
	local buttonholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,20),
			Parent = self.content
		}
	)
	--
	local outline = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Parent = buttonholder
		}
	)
	--
	local outline2 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Parent = outline
		}
	)
	--
	local color = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(30, 30, 30),
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,1,0),
			Parent = outline2
		}
	)
	--
	local gradient = utility.new(
		"UIGradient",
		{
			Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
			Rotation = 90,
			Parent = color
		}
	)
	--
	local buttonpress = utility.new(
		"TextButton",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			Font = self.library.font,
			Parent = buttonholder
		}
	)
	--
	buttonpress.MouseButton1Down:Connect(function()
		callback()
		outline.BorderColor3 = self.library.theme.accent
		table.insert(self.library.themeitems["accent"]["BorderColor3"],outline)
		wait(0.05)
		outline.BorderColor3 = Color3.fromRGB(12, 12, 12)
		local find = table.find(self.library.themeitems["accent"]["BorderColor3"],outline)
		if find then
			table.remove(self.library.themeitems["accent"]["BorderColor3"],find)
		end
	end)
	-- // button tbl
	button = {
		["library"] = self.library
	}
	--
	self.library.labels[#self.library.labels+1] = buttonpress
	-- // metatable indexing + return
	setmetatable(button, buttons)
	return button
end
--
function sections:slider(props)
	-- // properties
	local name = props.name or props.Name or props.page or props.Page or props.pagename or props.Pagename or props.PageName or props.pageName or "new ui"
	local def = props.def or props.Def or props.default or props.Default or 0
	local max = props.max or props.Max or props.maximum or props.Maximum or 100
	local min = props.min or props.Min or props.minimum or props.Minimum or 0
	local rounding = props.rounding or props.Rounding or props.round or props.Round or props.decimals or props.Decimals or false
	local ticking = props.tick or props.Tick or props.ticking or props.Ticking or false
	local measurement = props.measurement or props.Measurement or props.digit or props.Digit or props.calc or props.Calc or ""
	local callback = props.callback or props.callBack or props.CallBack or props.Callback or function()end
	def = math.clamp(def,min,max)
	-- // variables
	local slider = {}
	-- // main
	local sliderholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,25),
			Parent = self.content
		}
	)
	--
	local outline = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,0,12),
			Position = UDim2.new(0,0,0,15),
			Parent = sliderholder
		}
	)
	--
	local outline2 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(30, 30, 30),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Parent = outline
		}
	)	
	--
	local value = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,2),
			Position = UDim2.new(0,0,0.5,0),
			Font = self.library.font,
			Text = def..measurement.."/"..max..measurement,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			ZIndex = 3,
			Parent = outline
		}
	)
	--
	local color = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(30, 30, 30),
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,1,0),
			Parent = outline2
		}
	)
	--
	utility.new(
		"UIGradient",
		{
			Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
			Rotation = 90,
			Parent = color
		}
	)
	--
	local slide = utility.new(
		"Frame",
		{
			BackgroundColor3 = self.library.theme.accent,
			BorderSizePixel = 0,
			Size = UDim2.new((1 / color.AbsoluteSize.X) * (color.AbsoluteSize.X / (max - min) * (def - min)),0,1,0),
			ZIndex = 2,
			Parent = outline
		}
	)
	table.insert(self.library.themeitems["accent"]["BackgroundColor3"],slide)
	--
	utility.new(
		"UIGradient",
		{
			Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
			Rotation = 90,
			Parent = slide
		}
	)
	--
	local sliderbutton = utility.new(
		"TextButton",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Text = "",
			Parent = sliderholder
		}
	)
	--
	local title = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,15),
			Position = UDim2.new(0,0,0,0),
			Font = self.library.font,
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Left",
			Parent = sliderholder
		}
	)
	-- // slider tbl
	slider = {
		["library"] = self.library,
		["outline"] = outline,
		["sliderbutton"] = sliderbutton,
		["title"] = title,
		["value"] = value,
		["slide"] = slide,
		["color"] = color,
		["max"] = max,
		["min"] = min,
		["current"] = def,
		["measurement"] = measurement,
		["tick"] = ticking,
		["rounding"] = rounding,
		["callback"] = callback
	}
	--
	local function slide()
		local size = math.clamp(plr:GetMouse().X - slider.color.AbsolutePosition.X ,0 ,slider.color.AbsoluteSize.X)
		local result = (slider.max - slider.min) / slider.color.AbsoluteSize.X * size + slider.min
		if slider.rounding then
			local newres = math.floor(result)
			value.Text = newres..slider.measurement.."/"..slider.max..slider.measurement
			slider.current = newres
			slider.callback(newres)
			if slider.tick then
				slider.slide:TweenSize(UDim2.new((1 / slider.color.AbsoluteSize.X) * (slider.color.AbsoluteSize.X / (slider.max - slider.min) * (newres - slider.min)) ,0 ,1 ,0) ,Enum.EasingDirection.Out ,Enum.EasingStyle.Quad ,0.15 ,true)
			else
				slider.slide:TweenSize(UDim2.new((1 / slider.color.AbsoluteSize.X) * size ,0 ,1 ,0) ,Enum.EasingDirection.Out ,Enum.EasingStyle.Quad ,0.15 ,true)
			end
		else
			local newres = utility.round(result ,2)
			value.Text = newres..slider.measurement.."/"..slider.max..slider.measurement
			slider.current = newres
			slider.callback(newres)
			if slider.tick then
				slider.slide:TweenSize(UDim2.new((1 / slider.color.AbsoluteSize.X) * (slider.color.AbsoluteSize.X / (slider.max - slider.min) * (newres - slider.min)) ,0 ,1 ,0) ,Enum.EasingDirection.Out ,Enum.EasingStyle.Quad ,0.15 ,true)
			else
				slider.slide:TweenSize(UDim2.new((1 / slider.color.AbsoluteSize.X) * size ,0 ,1 ,0) ,Enum.EasingDirection.Out ,Enum.EasingStyle.Quad ,0.15 ,true)
			end
		end
	end
	--
	sliderbutton.MouseButton1Down:Connect(function()
		slider.holding = true
		slide()
		table.insert(self.library.themeitems["accent"]["BorderColor3"],outline)
		outline.BorderColor3 = self.library.theme.accent
	end)
	--
	uis.InputChanged:Connect(function()
		if slider.holding then
			slide()
		end
	end)
	--
	uis.InputEnded:Connect(function(Input)
		if Input.UserInputType.Name == 'MouseButton1' and slider.holding then
			slider.holding = false
			outline.BorderColor3 = Color3.fromRGB(12, 12, 12)
			local find = table.find(self.library.themeitems["accent"]["BorderColor3"],outline)
			if find then
				table.remove(self.library.themeitems["accent"]["BorderColor3"],find)
			end
		end
	end)
	--
	local pointer = props.pointer or props.Pointer or props.pointername or props.Pointername or props.PointerName or props.pointerName or nil
	--
	if pointer then
		if self.pointers then
			self.pointers[tostring(pointer)] = slider
		end
	end
	--
	self.library.labels[#self.library.labels+1] = title
	self.library.labels[#self.library.labels+1] = value
	-- // metatable indexing + return
	setmetatable(slider, sliders)
	return slider
end
--
function sliders:set(value)
	local size = math.clamp((self.color.AbsoluteSize.X / (self.max - self.min) * (value - self.min)) ,0 ,self.color.AbsoluteSize.X)
	local result = value
	if self.rounding then
		local newres = math.floor(result)
		self.value.Text = newres..self.measurement.."/"..self.max..self.measurement
		self.current = newres
		self.callback(newres)
		if self.tick then
			self.slide:TweenSize(UDim2.new((1 / self.color.AbsoluteSize.X) * (self.color.AbsoluteSize.X / (self.max - self.min) * (newres - self.min)) ,0 ,1 ,0) ,Enum.EasingDirection.Out ,Enum.EasingStyle.Quad ,0.15 ,true)
		else
			self.slide:TweenSize(UDim2.new((1 / self.color.AbsoluteSize.X) * size ,0 ,1 ,0) ,Enum.EasingDirection.Out ,Enum.EasingStyle.Quad ,0.15 ,true)
		end
	else
		local newres = utility.round(result ,2)
		self.value.Text = newres..self.measurement.."/"..self.max..self.measurement
		self.current = newres
		self.callback(newres)
		if self.tick then
			self.slide:TweenSize(UDim2.new((1 / self.color.AbsoluteSize.X) * (self.color.AbsoluteSize.X / (self.max - self.min) * (newres - self.min)) ,0 ,1 ,0) ,Enum.EasingDirection.Out ,Enum.EasingStyle.Quad ,0.15 ,true)
		else
			self.slide:TweenSize(UDim2.new((1 / self.color.AbsoluteSize.X) * size ,0 ,1 ,0) ,Enum.EasingDirection.Out ,Enum.EasingStyle.Quad ,0.15 ,true)
		end
	end
end
--
function library:closewindows(ignore)
	local window = self
	--
	for i,v in pairs(window.dropdowns) do
		if v ~= ignore then
			if v.open then
				v.optionsholder.Visible = false
				v.indicator.Text = "-"
				v.open = false
			end
		end
	end
	--
	for i,v in pairs(window.multiboxes) do
		if v ~= ignore then
			if v.open then
				v.optionsholder.Visible = false
				v.indicator.Text = "-"
				v.open = false
			end
		end
	end
	--
	for i,v in pairs(window.buttonboxs) do
		if v ~= ignore then
			if v.open then
				v.optionsholder.Visible = false
				v.indicator.Text = "-"
				v.open = false
			end
		end
	end
	--
	for i,v in pairs(window.colorpickers) do
		if v ~= ignore then
			if v.open then
				v.cpholder.Visible = false
				v.open = false
			end
		end
	end
end
--
function sections:dropdown(props)
	-- // properties
	local name = props.name or props.Name or props.page or props.Page or props.pagename or props.Pagename or props.PageName or props.pageName or "new ui"
	local def = props.def or props.Def or props.default or props.Default or ""
	local max = props.max or props.Max or props.maximum or props.Maximum or 4
	local options = props.options or props.Options or props.Settings or props.settings or {}
	local callback = props.callback or props.callBack or props.CallBack or props.Callback or function()end
	-- // variables
	local dropdown = {}
	-- // main
	local dropdownholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,35),
			ZIndex = 2,
			Parent = self.content
		}
	)
	--
	local outline = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,0,20),
			Position = UDim2.new(0,0,0,15),
			Parent = dropdownholder
		}
	)
	--
	local outline2 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Parent = outline
		}
	)
	--
	local color = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(30, 30, 30),
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Parent = outline2
		}
	)
	--
	utility.new(
		"UIGradient",
		{
			Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
			Rotation = 90,
			Parent = color
		}
	)
	--
	local value = utility.new(
		"TextLabel",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-20,1,0),
			Position = UDim2.new(0,5,0,0),
			Font = self.library.font,
			Text = def,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Left",
			ClipsDescendants = true,
			Parent = outline
		}
	)
	--
	local indicator = utility.new(
		"TextLabel",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-10,1,0),
			Position = UDim2.new(0.5,0,0,0),
			Font = self.library.font,
			Text = "+",
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Right",
			ClipsDescendants = true,
			Parent = outline
		}
	)
	--
	local title = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,15),
			Position = UDim2.new(0,0,0,0),
			Font = self.library.font,
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Left",
			Parent = dropdownholder
		}
	)
	--
	local dropdownbutton = utility.new(
		"TextButton",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Text = "",
			Parent = dropdownholder
		}
	)
	--
	local optionsholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,0,20),
			Position = UDim2.new(0,0,0,34),
			Visible = false,
			Parent = dropdownholder
		}
	)
	--
	local size = #options
	--
	size = math.clamp(size,1,max)
	--
	local optionsoutline = utility.new(
		"ScrollingFrame",
		{
			BackgroundColor3 = Color3.fromRGB(56, 56, 56),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,size,2),
			Position = UDim2.new(0,0,0,0),
			ClipsDescendants = true,
			CanvasSize = UDim2.new(0,0,0,18*#options),
			ScrollBarImageTransparency = 0.25,
			ScrollBarImageColor3 = Color3.fromRGB(0,0,0),
			ScrollBarThickness = 5,
			VerticalScrollBarInset = "ScrollBar",
			VerticalScrollBarPosition = "Right",
			ZIndex = 5,
			Parent = optionsholder
		}
	)
	--
	utility.new(
		"UIListLayout",
		{
			FillDirection = "Vertical",
			Parent = optionsoutline
		}
	)
	-- // dropdown tbl
	dropdown = {
		["library"] = self.library,
		["optionsholder"] = optionsholder,
		["indicator"] = indicator,
		["options"] = options,
		["title"] = title,
		["value"] = value,
		["open"] = false,
		["titles"] = {},
		["current"] = def,
		["callback"] = callback
	}
	--
	table.insert(dropdown.library.dropdowns,dropdown)
	--
	for i,v in pairs(options) do
		local ddoptionbutton = utility.new(
			"TextButton",
			{
				AnchorPoint = Vector2.new(0,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,0,0,18),
				Text = "",
				ZIndex = 6,
				Parent = optionsoutline
			}
		)
		--
		local ddoptiontitle = utility.new(
			"TextLabel",
			{
				AnchorPoint = Vector2.new(0.5,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,-10,1,0),
				Position = UDim2.new(0.5,0,0,0),
				Font = self.library.font,
				Text = v,
				TextColor3 = Color3.fromRGB(255,255,255),
				TextSize = self.library.textsize,
				TextStrokeTransparency = 0,
				TextXAlignment = "Left",
				ClipsDescendants = true,
				ZIndex = 6,
				Parent = ddoptionbutton
			}
		)
		--
		self.library.labels[#self.library.labels+1] = ddoptiontitle
		--
		table.insert(dropdown.titles,ddoptiontitle)
		--
		if v == dropdown.current then ddoptiontitle.TextColor3 = self.library.theme.accent end
		--
		ddoptionbutton.MouseButton1Down:Connect(function()
			optionsholder.Visible = false
			dropdown.open = false
			indicator.Text = "+"
			for z,x in pairs(dropdown.titles) do
				if x.TextColor3 == self.library.theme.accent then
					x.TextColor3 = Color3.fromRGB(255,255,255)
				end
			end
			dropdown.current = v
			dropdown.value.Text = v
			ddoptiontitle.TextColor3 = self.library.theme.accent
			table.insert(self.library.themeitems["accent"]["TextColor3"],ddoptiontitle)
			dropdown.callback(v)
		end)
	end
	--
	dropdownbutton.MouseButton1Down:Connect(function()
		dropdown.library:closewindows(dropdown)
		for i,v in pairs(dropdown.titles) do
			if v.Text == dropdown.current then
				v.TextColor3 = dropdown.library.theme.accent
			else
				v.TextColor3 = Color3.fromRGB(255,255,255)
			end
		end
		optionsholder.Visible = not dropdown.open
		dropdown.open = not dropdown.open
		if dropdown.open then
			indicator.Text = "-"
		else
			indicator.Text = "+"
		end
	end)
	--
	local pointer = props.pointer or props.Pointer or props.pointername or props.Pointername or props.PointerName or props.pointerName or nil
	--
	if pointer then
		if self.pointers then
			self.pointers[tostring(pointer)] = dropdown
		end
	end
	--
	self.library.labels[#self.library.labels+1] = title
	self.library.labels[#self.library.labels+1] = value
	-- // metatable indexing + return
	setmetatable(dropdown, dropdowns)
	return dropdown
end
--
function sections:buttonbox(props)
	-- // properties
	local name = props.name or props.Name or props.page or props.Page or props.pagename or props.Pagename or props.PageName or props.pageName or "new ui"
	local def = props.def or props.Def or props.default or props.Default or ""
	local max = props.max or props.Max or props.maximum or props.Maximum or 4
	local options = props.options or props.Options or props.Settings or props.settings or {}
	local callback = props.callback or props.callBack or props.CallBack or props.Callback or function()end
	-- // variables
	local buttonbox = {}
	-- // main
	local buttonboxholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,35),
			ZIndex = 2,
			Parent = self.content
		}
	)
	--
	local outline = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,0,20),
			Position = UDim2.new(0,0,0,15),
			Parent = buttonboxholder
		}
	)
	--
	local outline2 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Parent = outline
		}
	)
	--
	local color = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(30, 30, 30),
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Parent = outline2
		}
	)
	--
	utility.new(
		"UIGradient",
		{
			Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
			Rotation = 90,
			Parent = color
		}
	)
	--
	local indicator = utility.new(
		"TextLabel",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-10,1,0),
			Position = UDim2.new(0.5,0,0,0),
			Font = self.library.font,
			Text = "+",
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Right",
			ClipsDescendants = true,
			Parent = outline
		}
	)
	--
	local title = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,15),
			Position = UDim2.new(0,0,0,0),
			Font = self.library.font,
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Left",
			Parent = buttonboxholder
		}
	)
	--
	local buttonboxbutton = utility.new(
		"TextButton",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Text = "",
			Parent = buttonboxholder
		}
	)
	--
	local optionsholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,0,20),
			Position = UDim2.new(0,0,0,34),
			Visible = false,
			Parent = buttonboxholder
		}
	)
	--
	local size = #options
	--
	size = math.clamp(size,1,max)
	--
	local optionsoutline = utility.new(
		"ScrollingFrame",
		{
			BackgroundColor3 = Color3.fromRGB(56, 56, 56),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,size,2),
			Position = UDim2.new(0,0,0,0),
			ClipsDescendants = true,
			CanvasSize = UDim2.new(0,0,0,18*#options),
			ScrollBarImageTransparency = 0.25,
			ScrollBarImageColor3 = Color3.fromRGB(0,0,0),
			ScrollBarThickness = 5,
			VerticalScrollBarInset = "ScrollBar",
			VerticalScrollBarPosition = "Right",
			ZIndex = 5,
			Parent = optionsholder
		}
	)
	--
	utility.new(
		"UIListLayout",
		{
			FillDirection = "Vertical",
			Parent = optionsoutline
		}
	)
	-- // buttonbox tbl
	buttonbox = {
		["library"] = self.library,
		["optionsholder"] = optionsholder,
		["indicator"] = indicator,
		["options"] = options,
		["title"] = title,
		["open"] = false,
		["titles"] = {},
		["current"] = def,
		["callback"] = callback
	}
	--
	table.insert(buttonbox.library.buttonboxs,buttonbox)
	--
	for i,v in pairs(options) do
		local bboptionbutton = utility.new(
			"TextButton",
			{
				AnchorPoint = Vector2.new(0,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,0,0,18),
				Text = "",
				ZIndex = 6,
				Parent = optionsoutline
			}
		)
		--
		local bboptiontitle = utility.new(
			"TextLabel",
			{
				AnchorPoint = Vector2.new(0.5,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,-10,1,0),
				Position = UDim2.new(0.5,0,0,0),
				Font = self.library.font,
				Text = v,
				TextColor3 = Color3.fromRGB(255,255,255),
				TextSize = self.library.textsize,
				TextStrokeTransparency = 0,
				TextXAlignment = "Left",
				ClipsDescendants = true,
				ZIndex = 6,
				Parent = bboptionbutton
			}
		)
		--
		self.library.labels[#self.library.labels+1] = bboptiontitle
		--
		table.insert(buttonbox.titles,bboptiontitle)
		--
		bboptionbutton.MouseButton1Down:Connect(function()
			optionsholder.Visible = false
			buttonbox.open = false
			indicator.Text = "+"
			buttonbox.current = v
			buttonbox.callback(v)
		end)
	end
	--
	buttonboxbutton.MouseButton1Down:Connect(function()
		buttonbox.library:closewindows(buttonbox)
		optionsholder.Visible = not buttonbox.open
		buttonbox.open = not buttonbox.open
		if buttonbox.open then
			indicator.Text = "-"
		else
			indicator.Text = "+"
		end
	end)
	--
	local pointer = props.pointer or props.Pointer or props.pointername or props.Pointername or props.PointerName or props.pointerName or nil
	--
	if pointer then
		if self.pointers then
			self.pointers[tostring(pointer)] = buttonbox
		end
	end
	--
	self.library.labels[#self.library.labels+1] = title
	-- // metatable indexing + return
	setmetatable(buttonbox, buttonboxs)
	return buttonbox
end
--
function dropdowns:set(value)
	if value ~= nil then
		local dropdown = self
		if table.find(dropdown.options,value) then
			self.current = tostring(value)
			self.value.Text = tostring(value)
			self.callback(tostring(value))
			for z,x in pairs(dropdown.titles) do
				if x.Text == value then
					x.TextColor3 = dropdown.library.theme.accent
				else
					x.TextColor3 = Color3.fromRGB(255,255,255)
				end
			end
		end
	end
end
--
function sections:multibox(props)
	-- // properties
	local name = props.name or props.Name or props.page or props.Page or props.pagename or props.Pagename or props.PageName or props.pageName or "new ui"
	local def = props.def or props.Def or props.default or props.Default or {}
	local max = props.max or props.Max or props.maximum or props.Maximum or 4
	local options = props.options or props.Options or props.Settings or props.settings or {}
	local callback = props.callback or props.callBack or props.CallBack or props.Callback or function()end
	local defstr = ""
	if #def > 1 then
		for i,v in pairs(def) do
			if i == #def then
				defstr = defstr..v
			else
				defstr = defstr..v..", "
			end
		end
	else
		for i,v in pairs(def) do
			defstr = defstr..v
		end
	end
	-- // variables
	local multibox = {}
	-- // main
	local multiboxholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,35),
			ZIndex = 2,
			Parent = self.content
		}
	)
	--
	local outline = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,0,20),
			Position = UDim2.new(0,0,0,15),
			Parent = multiboxholder
		}
	)
	--
	local outline2 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Parent = outline
		}
	)
	--
	local color = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(30, 30, 30),
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Parent = outline2
		}
	)
	--
	utility.new(
		"UIGradient",
		{
			Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
			Rotation = 90,
			Parent = color
		}
	)
	--
	local value = utility.new(
		"TextLabel",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-20,1,0),
			Position = UDim2.new(0,5,0,0),
			Font = self.library.font,
			Text = defstr,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Left",
			ClipsDescendants = true,
			Parent = outline
		}
	)
	--
	local indicator = utility.new(
		"TextLabel",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-10,1,0),
			Position = UDim2.new(0.5,0,0,0),
			Font = self.library.font,
			Text = "+",
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Right",
			ClipsDescendants = true,
			Parent = outline
		}
	)
	--
	local title = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,15),
			Position = UDim2.new(0,0,0,0),
			Font = self.library.font,
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Left",
			Parent = multiboxholder
		}
	)
	--
	local dropdownbutton = utility.new(
		"TextButton",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Text = "",
			Parent = multiboxholder
		}
	)
	--
	local optionsholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,0,20),
			Position = UDim2.new(0,0,0,34),
			Visible = false,
			Parent = multiboxholder
		}
	)
	--
	local size = #options
	--
	size = math.clamp(size,1,max)
	--
	local optionsoutline = utility.new(
		"ScrollingFrame",
		{
			BackgroundColor3 = Color3.fromRGB(56, 56, 56),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,size,2),
			Position = UDim2.new(0,0,0,0),
			ClipsDescendants = true,
			CanvasSize = UDim2.new(0,0,0,18*#options),
			ScrollBarImageTransparency = 0.25,
			ScrollBarImageColor3 = Color3.fromRGB(0,0,0),
			ScrollBarThickness = 5,
			VerticalScrollBarInset = "ScrollBar",
			VerticalScrollBarPosition = "Right",
			ZIndex = 5,
			Parent = optionsholder
		}
	)
	--
	utility.new(
		"UIListLayout",
		{
			FillDirection = "Vertical",
			Parent = optionsoutline
		}
	)
	-- // dropdown tbl
	multibox = {
		["library"] = self.library,
		["indicator"] = indicator,
		["optionsholder"] = optionsholder,
		["options"] = options,
		["value"] = value,
		["open"] = false,
		["titles"] = {},
		["current"] = def,
		["callback"] = callback
	}
	--
	table.insert(multibox.library.multiboxes,multibox)
	--
	for i,v in pairs(options) do
		local ddoptionbutton = utility.new(
			"TextButton",
			{
				AnchorPoint = Vector2.new(0,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,0,0,18),
				Text = "",
				ZIndex = 6,
				Parent = optionsoutline
			}
		)
		--
		local ddoptiontitle = utility.new(
			"TextLabel",
			{
				AnchorPoint = Vector2.new(0.5,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,-10,1,0),
				Position = UDim2.new(0.5,0,0,0),
				Font = self.library.font,
				Text = v,
				TextColor3 = Color3.fromRGB(255,255,255),
				TextSize = self.library.textsize,
				TextStrokeTransparency = 0,
				TextXAlignment = "Left",
				ClipsDescendants = true,
				ZIndex = 6,
				Parent = ddoptionbutton
			}
		)
		--
		self.library.labels[#self.library.labels+1] = ddoptiontitle
		--
		table.insert(multibox.titles,ddoptiontitle)
		--
		for c,b in pairs(def) do if v == b then ddoptiontitle.TextColor3 = self.library.theme.accent end end
		--
		ddoptionbutton.MouseButton1Down:Connect(function()
			local find = table.find(multibox.current,v)
			if find == nil then
				table.insert(multibox.current,v)
				local str = ""
				if #multibox.current > 1 then
					for i,v in pairs(multibox.current) do
						if i == #multibox.current then
							str = str..v
						else
							str = str..v..", "
						end
					end
				else
					for i,v in pairs(multibox.current) do
						str = str..v
					end
				end
				value.Text = str
				ddoptiontitle.TextColor3 = self.library.theme.accent
				table.insert(self.library.themeitems["accent"]["TextColor3"],ddoptiontitle)
				multibox.callback(multibox.current)
			else
				table.remove(multibox.current,find)
				local str = ""
				if #multibox.current > 1 then
					for i,v in pairs(multibox.current) do
						if i == #multibox.current then
							str = str..v
						else
							str = str..v..", "
						end
					end
				else
					for i,v in pairs(multibox.current) do
						str = str..v
					end
				end
				value.Text = str
				ddoptiontitle.TextColor3 = Color3.fromRGB(255,255,255)
				multibox.callback(multibox.current)
			end
		end)
	end
	--
	dropdownbutton.MouseButton1Down:Connect(function()
		multibox.library:closewindows(multibox)
		for i,v in pairs(multibox.titles) do
			if v.TextColor3 ~= Color3.fromRGB(255,255,255) then
				v.TextColor3 = self.library.theme.accent
			end
		end
		optionsholder.Visible = not multibox.open
		multibox.open = not multibox.open
		if multibox.open then
			indicator.Text = "-"
		else
			indicator.Text = "+"
		end
	end)
	--
	local pointer = props.pointer or props.Pointer or props.pointername or props.Pointername or props.PointerName or props.pointerName or nil
	--
	if pointer then
		if self.pointers then
			self.pointers[tostring(pointer)] = multibox
		end
	end
	--
	self.library.labels[#self.library.labels+1] = value
	self.library.labels[#self.library.labels+1] = title
	-- // metatable indexing + return
	setmetatable(multibox, multiboxs)
	return multibox
end
--
function buttonboxs:set(value)
	if value ~= nil then
		local dropdown = self
		if table.find(dropdown.options,value) then
			self.current = tostring(value)
			self.callback(tostring(value))
		end
	end
end
--
function multiboxs:set(tbl)
	if tbl then
		local multibox = self
		if typeof(tbl) == "table" then
			multibox.current = {}
			for i,v in pairs(tbl) do
				if table.find(multibox.options,v) then
					table.insert(multibox.current,v)
				end
			end
			--
			for i,v in pairs(multibox.titles) do
				if v.TextColor3 == multibox.library.theme.accent then
					v.TextColor3 = Color3.fromRGB(255,255,255)
				end
				if table.find(tbl,v.Text) then
					v.TextColor3 = multibox.library.theme.accent
				end
			end
			--
			local str = ""
			if #multibox.current > 1 then
				for i,v in pairs(multibox.current) do
					if i == #multibox.current then
						str = str..v
					else
						str = str..v..", "
					end
				end
			else
				for i,v in pairs(multibox.current) do
					str = str..v
				end
			end
			--
			multibox.value.Text = str
		end
	end
end
--
function sections:textbox(props)
	-- // properties
	local name = props.name or props.Name or props.page or props.Page or props.pagename or props.Pagename or props.PageName or props.pageName or "new ui"
	local def = props.def or props.Def or props.default or props.Default or ""
	local placeholder = props.placeholder or props.Placeholder or props.placeHolder or props.PlaceHolder or props.placeholdertext or props.PlaceHolderText or props.PlaceHoldertext or props.placeHolderText or props.placeHoldertext or props.Placeholdertext or props.PlaceholderText or props.placeholderText or ""
	local callback = props.callback or props.callBack or props.CallBack or props.Callback or function()end
	-- // variables
	local textbox = {}
	-- // main
	local textboxholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,35),
			ZIndex = 2,
			Parent = self.content
		}
	)
	--
	local outline = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,0,20),
			Position = UDim2.new(0,0,0,15),
			Parent = textboxholder
		}
	)
	--
	local outline2 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Parent = outline
		}
	)
	--
	local color = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(30, 30, 30),
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,1,0),
			Parent = outline2
		}
	)
	--
	local gradient = utility.new(
		"UIGradient",
		{
			Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
			Rotation = 90,
			Parent = color
		}
	)
	--
	local button = utility.new(
		"TextButton",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Text = "",
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			Font = self.library.font,
			Parent = textboxholder
		}
	)
	--
	local title = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,15),
			Position = UDim2.new(0,0,0,0),
			Font = self.library.font,
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Left",
			Parent = textboxholder
		}
	)
	--
	local tbox = utility.new(
		"TextBox",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-10,0,20),
			Position = UDim2.new(0.5,0,0,15),
			PlaceholderText = placeholder,
			Text = def,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextTruncate = "AtEnd",
			Font = self.library.font,
			Parent = textboxholder
		}
	)
	-- // textbox tbl
	textbox = {
		["library"] = self.library,
		["tbox"] = tbox,
		["current"] = def,
		["callback"] = callback
	}
	--
	button.MouseButton1Down:Connect(function()
		tbox:CaptureFocus()
	end)
	--
	tbox.Focused:Connect(function()
		outline.BorderColor3 = self.library.theme.accent
		table.insert(self.library.themeitems["accent"]["BorderColor3"],outline)
	end)
	--
	tbox.FocusLost:Connect(function(enterPressed)
		textbox.current = tbox.Text
		callback(tbox.Text)
		outline.BorderColor3 = Color3.fromRGB(12, 12, 12)
		local find = table.find(self.library.themeitems["accent"]["BorderColor3"],outline)
		if find then
			table.remove(self.library.themeitems["accent"]["BorderColor3"],find)
		end
	end)
	--
	local pointer = props.pointer or props.Pointer or props.pointername or props.Pointername or props.PointerName or props.pointerName or nil
	--
	if pointer then
		if self.pointers then
			self.pointers[tostring(pointer)] = textbox
		end
	end
	--
	self.library.labels[#self.library.labels+1] = title
	self.library.labels[#self.library.labels+1] = tbox
	-- // metatable indexing + return
	setmetatable(textbox, textboxs)
	return textbox
end
--
function textboxs:set(value)
	self.tbox.Text = value
	self.current = value
	self.callback(value)
end
--
function sections:keybind(props)
	-- // properties
	local name = props.name or props.Name or props.page or props.Page or props.pagename or props.Pagename or props.PageName or props.pageName or "new ui"
	local def = props.def or props.Def or props.default or props.Default or nil
	local callback = props.callback or props.callBack or props.CallBack or props.Callback or function()end
	local allowed = props.allowed or props.Allowed or 1
	--
	local default = ".."
	local typeis = nil
	--
	if typeof(def) == "EnumItem" then
		if def == Enum.UserInputType.MouseButton1 then
			if allowed == 1 then
				default = "MB1"
				typeis = "UserInputType"
			end
		elseif def == Enum.UserInputType.MouseButton2 then
			if allowed == 1 then
				default = "MB2"
				typeis = "UserInputType"
			end
		elseif def == Enum.UserInputType.MouseButton3 then
			if allowed == 1 then
				default = "MB3"
				typeis = "UserInputType"
			end
		else
			local capd = utility.capatalize(def.Name)
			if #capd > 1 then
				default = capd
			else
				default = def.Name
			end
			typeis = "KeyCode"
		end
	end
	-- // variables
	local keybind = {}
	-- // main
	local keybindholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,17),
			Parent = self.content
		}
	)
	--
	local outline = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(1,0),
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(0,40,1,0),
			Position = UDim2.new(1,0,0,0),
			Parent = keybindholder
		}
	)
	--
	local outline2 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Parent = outline
		}
	)
	--
	local value = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Font = self.library.font,
			Text = default,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Center",
			Parent = outline
		}
	)
	--
	outline.Size = UDim2.new(0,value.TextBounds.X+20,1,0)
	--
	local color = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(30, 30, 30),
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Parent = outline2
		}
	)
	--
	utility.new(
		"UIGradient",
		{
			Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
			Rotation = 90,
			Parent = color
		}
	)
	--
	local button = utility.new(
		"TextButton",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Text = "",
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			Font = self.library.font,
			Parent = keybindholder
		}
	)
	--
	local title = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Font = self.library.font,
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Left",
			Parent = keybindholder
		}
	)
	-- // keybind tbl
	keybind = {
		["library"] = self.library,
		["down"] = false,
		["outline"] = outline,
		["value"] = value,
		["allowed"] = allowed,
		["current"] = {typeis,utility.splitenum(def)},
		["pressed"] = false,
		["callback"] = callback
	}
	--
	button.MouseButton1Down:Connect(function()
		if keybind.down == false then
			outline.BorderColor3 = self.library.theme.accent
			table.insert(self.library.themeitems["accent"]["BorderColor3"],outline)
			wait()
			keybind.down = true
		end
	end)
	--
	button.MouseButton2Down:Connect(function()
		keybind.down = false
		keybind.current = {nil,nil}
		outline.BorderColor3 = Color3.fromRGB(12, 12, 12)
		local find = table.find(self.library.themeitems["accent"]["BorderColor3"],outline)
		if find then
			table.remove(self.library.themeitems["accent"]["BorderColor3"],find)
		end
		value.Text = ".."
		outline.Size = UDim2.new(0,value.TextBounds.X+20,1,0)
	end)
	--
	local function turn(typeis,current)
		outline.Size = UDim2.new(0,value.TextBounds.X+20,1,0)
		keybind.down = false
		keybind.current = {typeis,utility.splitenum(current)}
		outline.BorderColor3 = Color3.fromRGB(12, 12, 12)
		local find = table.find(self.library.themeitems["accent"]["BorderColor3"],outline)
		if find then
			table.remove(self.library.themeitems["accent"]["BorderColor3"],find)
		end
	end
	--
	uis.InputBegan:Connect(function(Input)
		if keybind.down then
			if Input.UserInputType == Enum.UserInputType.Keyboard then
				local capd = utility.capatalize(Input.KeyCode.Name)
				if #capd > 1 then
					value.Text = capd
				else
					value.Text = Input.KeyCode.Name
				end
				turn("KeyCode",Input.KeyCode)
				callback(Input.KeyCode)
			end
			if allowed == 1 then
				if Input.UserInputType == Enum.UserInputType.MouseButton1 then
					value.Text = "MB1"
					turn("UserInputType",Input)
					callback(Input)
				elseif Input.UserInputType == Enum.UserInputType.MouseButton2 then
					value.Text = "MB2"
					turn("UserInputType",Input)
					callback(Input)
				elseif Input.UserInputType == Enum.UserInputType.MouseButton3 then
					value.Text = "MB3"
					turn("UserInputType",Input)
					callback(Input)
				end
			end
		end
	end)
	--
	local pointer = props.pointer or props.Pointer or props.pointername or props.Pointername or props.PointerName or props.pointerName or nil
	--
	if pointer then
		if self.pointers then
			self.pointers[tostring(pointer)] = keybind
		end
	end
	--
	self.library.labels[#self.library.labels+1] = title
	self.library.labels[#self.library.labels+1] = value
	-- // metatable indexing + return
	setmetatable(keybind, keybinds)
	return keybind
end
--
function keybinds:set(key)
	if key then
		if typeof(key) == "EnumItem" or typeof(key) == "table" then
			if typeof(key) == "table" then
				if key[1] and key[2] then
					key = Enum[key[1]][key[2]]
				else
					return
				end
			end
			local keybind = self
			local typeis = ""
			--
			local default = ".."
			--
			if key == Enum.UserInputType.MouseButton1 then
				if keybind.allowed == 1 then
					default = "MB1"
					typeis = "UserInputType"
				end
			elseif key == Enum.UserInputType.MouseButton2 then
				if keybind.allowed == 1 then
					default = "MB2"
					typeis = "UserInputType"
				end
			elseif key == Enum.UserInputType.MouseButton3 then
				if keybind.allowed == 1 then
					default = "MB3"
					typeis = "UserInputType"
				end
			else
				local capd = utility.capatalize(key.Name)
				if #capd > 1 then
					default = capd
				else
					default = key.Name
				end
				typeis = "KeyCode"
			end
			--
			keybind.value.Text = default
			keybind.current = {typeis,utility.splitenum(key)}
			keybind.callback(keybind.current)
			keybind.outline.Size = UDim2.new(0,keybind.value.TextBounds.X+20,1,0)
			--
			if keybind.down then
				keybind.down = false
				keybind.outline.BorderColor3 = Color3.fromRGB(12, 12, 12)
				local find = table.find(self.library.themeitems["accent"]["BorderColor3"],keybind.outline)
				if find then
					table.remove(self.library.themeitems["accent"]["BorderColor3"],find)
				end
			end
		end
	end
end
--
function sections:colorpicker(props)
	-- // properties
	local name = props.name or props.Name or "new colorpicker"
	local cpname = props.cpname or props.Cpname or props.CPname or props.CPName or props.cPname or props.cpName or props.colorpickername or nil
	local def = props.def or props.Def or props.default or props.Default or Color3.fromRGB(255,255,255)
	local callback = props.callback or props.callBack or props.CallBack or props.Callback or function()end
	--
	local h,s,v = def:ToHSV()
	-- // variables
	local colorpicker = {}
	-- // main
	local colorpickerholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,15),
			ZIndex = 2,
			Parent = self.content
		}
	)
	--
	local outline = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(1,0),
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(0,30,1,0),
			Position = UDim2.new(1,0,0,0),
			Parent = colorpickerholder
		}
	)
	--
	local outline2 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Parent = outline
		}
	)
	--
	local cpcolor = utility.new(
		"Frame",
		{
			BackgroundColor3 = def,
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,1,0),
			Parent = outline2
		}
	)
	--
	utility.new(
		"UIGradient",
		{
			Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
			Rotation = 90,
			Parent = cpcolor
		}
	)
	--
	local title = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Font = self.library.font,
			Text = name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Left",
			Parent = colorpickerholder
		}
	)
	--
	local button = utility.new(
		"TextButton",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Text = "",
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			Font = self.library.font,
			Parent = colorpickerholder
		}
	)
	--
	local cpholder = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,0,230),
			Position = UDim2.new(0,0,1,5),
			Visible = false,
			ZIndex = 5,
			Parent = colorpickerholder
		}
	)
	--
	local outline2 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			ZIndex = 5,
			Parent = cpholder
		}
	)
	--
	local color = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundColor3 = self.library.theme.accent,
			BorderSizePixel = 0,
			Size = UDim2.new(1,-2,0,1),
			Position = UDim2.new(0.5,0,0,0),
			ZIndex = 5,
			Parent = outline2
		}
	)
	--
	table.insert(self.library.themeitems["accent"]["BackgroundColor3"],color)
	--
	local cptitle = utility.new(
		"TextLabel",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,-10,0,20),
			Position = UDim2.new(0.5,0,0,0),
			Font = self.library.font,
			Text = cpname or name,
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Left",
			ZIndex = 5,
			Parent = outline2
		}
	)
	--
	local cpholder2 = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(0.875,0,0,150),
			Position = UDim2.new(0,5,0,20),
			ZIndex = 5,
			Parent = outline2
		}
	)
	--
	local outline3 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromHSV(h,1,1),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			ZIndex = 5,
			Parent = cpholder2
		}
	)
	--
	local cpimage = utility.new(
		"ImageButton",
		{
			AutoButtonColor = false,
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,1,0),
			ZIndex = 5,
			Image = "rbxassetid://7074305282",
			Parent = outline3
		}
	)
	--
	local cpcursor = utility.new(
		"ImageLabel",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Size = UDim2.new(0,6,0,6),
			Position = UDim2.new(s,0,1-v,0),
			ZIndex = 5,
			Image = "rbxassetid://7074391319",
			Parent = cpimage
		}
	)
	--
	local huepicker = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(1,0),
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(0.05,0,0,150),
			Position = UDim2.new(1,-5,0,20),
			ZIndex = 5,
			Parent = outline2
		}
	)
	--
	local outline4 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(255, 255, 255),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			ZIndex = 5,
			Parent = huepicker
		}
	)
	--
	local huebutton = utility.new(
		"TextButton",
		{
			AnchorPoint = Vector2.new(0,0),
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Text = "",
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			Font = self.library.font,
			ZIndex = 5,
			Parent = huepicker
		}
	)
	--
	utility.new(
		"UIGradient",
		{
			Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(255, 0, 4)), ColorSequenceKeypoint.new(0.10, Color3.fromRGB(255, 153, 0)), ColorSequenceKeypoint.new(0.20, Color3.fromRGB(209, 255, 0)), ColorSequenceKeypoint.new(0.30, Color3.fromRGB(55, 255, 0)), ColorSequenceKeypoint.new(0.40, Color3.fromRGB(0, 255, 102)), ColorSequenceKeypoint.new(0.50, Color3.fromRGB(0, 255, 255)), ColorSequenceKeypoint.new(0.60, Color3.fromRGB(0, 102, 255)), ColorSequenceKeypoint.new(0.70, Color3.fromRGB(51, 0, 255)), ColorSequenceKeypoint.new(0.80, Color3.fromRGB(204, 0, 255)), ColorSequenceKeypoint.new(0.90, Color3.fromRGB(255, 0, 153)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 0, 4))},
			Rotation = 90,
			Parent = outline4
		}
	)
	--
	local huecursor = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0.5),
			BackgroundColor3 = Color3.fromRGB(255, 255, 255),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(0,12,0,6),
			Position = UDim2.new(0.5,0,h,0),
			ZIndex = 5,
			Parent = outline4
		}
	)
	--
	local huecursor_inline = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromHSV(h,1,1),
			BorderColor3 = Color3.fromRGB(255, 255, 255),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			ZIndex = 5,
			Parent = huecursor
		}
	)
	--
	local function textbox(parent,size,position)
		local textbox_holder = utility.new(
			"Frame",
			{
				BackgroundTransparency = 1,
				BorderSizePixel = 0,
				Position = position,
				Size = size,
				ZIndex = 5,
				Parent = parent
			}
		)
		--
		local outline5 = utility.new(
			"Frame",
			{
				BackgroundColor3 = Color3.fromRGB(24, 24, 24),
				BorderColor3 = Color3.fromRGB(12, 12, 12),
				BorderMode = "Inset",
				BorderSizePixel = 1,
				Position = UDim2.new(0,0,0,0),
				Size = UDim2.new(1,0,1,0),
				ZIndex = 5,
				Parent = textbox_holder
			}
		)
		--
		local outline6 = utility.new(
			"Frame",
			{
				BackgroundColor3 = Color3.fromRGB(24, 24, 24),
				BorderColor3 = Color3.fromRGB(56, 56, 56),
				BorderMode = "Inset",
				BorderSizePixel = 1,
				Position = UDim2.new(0,0,0,0),
				Size = UDim2.new(1,0,1,0),
				ZIndex = 5,
				Parent = outline5
			}
		)
		--
		local color2 = utility.new(
			"Frame",
			{
				AnchorPoint = Vector2.new(0,0),
				BackgroundColor3 = Color3.fromRGB(30, 30, 30),
				BorderSizePixel = 0,
				Size = UDim2.new(1,0,0,0),
				Position = UDim2.new(0,0,0,0),
				ZIndex = 5,
				Parent = outline6
			}
		)
		--
		utility.new(
			"UIGradient",
			{
				Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
				Rotation = 90,
				Parent = color2
			}
		)
		--
		local tbox = utility.new(
			"TextBox",
			{
				AnchorPoint = Vector2.new(0.5,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,0,1,0),
				Position = UDim2.new(0.5,0,0,0),
				PlaceholderColor3 = Color3.fromRGB(255,255,255),
				PlaceholderText = "",
				Text = "",
				TextColor3 = Color3.fromRGB(255,255,255),
				TextSize = self.library.textsize,
				TextStrokeTransparency = 0,
				Font = self.library.font,
				ZIndex = 5,
				Parent = textbox_holder
			}
		)
		--
		local tbox_button = utility.new(
			"TextButton",
			{
				AnchorPoint = Vector2.new(0,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,0,1,0),
				Position = UDim2.new(0,0,0,0),
				Text = "",
				TextColor3 = Color3.fromRGB(255,255,255),
				TextSize = self.library.textsize,
				TextStrokeTransparency = 0,
				Font = self.library.font,
				ZIndex = 5,
				Parent = textbox_holder
			}
		)
		--
		tbox_button.MouseButton1Down:Connect(function()
			tbox:CaptureFocus()
		end)
		--
		return {textbox_holder,tbox,outline5}
	end
	--
	local red = textbox(outline2,UDim2.new(0,62,0,20),UDim2.new(0,5,0,175))
	local green = textbox(outline2,UDim2.new(0,62,0,20),UDim2.new(0,5,0,175))
	green[1].AnchorPoint = Vector2.new(0.5,0)
	green[1].Position = UDim2.new(0.5,0,0,175)
	local blue = textbox(outline2,UDim2.new(0,62,0,20),UDim2.new(0,5,0,175))
	blue[1].AnchorPoint = Vector2.new(1,0)
	blue[1].Position = UDim2.new(1,-5,0,175)
	local hex = textbox(outline2,UDim2.new(1,-10,0,20),UDim2.new(0,5,0,200))
	hex[2].Size = UDim2.new(1,-12,1,0)
	hex[2].TextXAlignment = "Left"
	-- // colorpicker tbl
	colorpicker = {
		["library"] = self.library,
		["cpholder"] = cpholder,
		["cpcolor"] = cpcolor,
		["huecursor"] = huecursor,
		["outline3"] = outline3,
		["huecursor_inline"] = huecursor_inline,
		["cpcursor"] = cpcursor,
		["current"] = def,
		["open"] = false,
		["cp"] = false,
		["hue"] = false,
		["hsv"] = {h,s,v},
		["red"] = red[2],
		["green"] = green[2],
		["blue"] = blue[2],
		["hex"] = hex[2],
		["callback"] = callback
	}
	--
	table.insert(self.library.colorpickers,colorpicker)
	--
	local function updateboxes()
		colorpicker.red.PlaceholderText = "R: "..tostring(math.floor(colorpicker.current.R*255))
		colorpicker.green.PlaceholderText = "G: "..tostring(math.floor(colorpicker.current.G*255))
		colorpicker.blue.PlaceholderText = "B: "..tostring(math.floor(colorpicker.current.B*255))
		colorpicker.hex.PlaceholderText = "Hex: "..utility.to_hex(colorpicker.current)
	end
	--
	updateboxes()
	--
	local function movehue()
		local posy = math.clamp(plr:GetMouse().Y-outline3.AbsolutePosition.Y,0,outline3.AbsoluteSize.Y)
		local resy = (1/outline3.AbsoluteSize.Y)*posy
		outline3.BackgroundColor3 = Color3.fromHSV(resy,1,1)
		huecursor_inline.BackgroundColor3 = Color3.fromHSV(resy,1,1)
		colorpicker.hsv[1] = resy
		colorpicker.current = Color3.fromHSV(colorpicker.hsv[1],colorpicker.hsv[2],colorpicker.hsv[3])
		cpcolor.BackgroundColor3 = colorpicker.current
		updateboxes()
		colorpicker.callback(colorpicker.current)
		huecursor:TweenPosition(UDim2.new(0.5,0,resy,0),Enum.EasingDirection.Out,Enum.EasingStyle.Quad,0.15,true)
	end
	--
	local function movecp()
		local posx,posy = math.clamp(plr:GetMouse().X-outline3.AbsolutePosition.X,0,outline3.AbsoluteSize.X),math.clamp(plr:GetMouse().Y-outline3.AbsolutePosition.Y,0,outline3.AbsoluteSize.Y)
		local resx,resy = (1/outline3.AbsoluteSize.X)*posx,(1/outline3.AbsoluteSize.Y)*posy
		colorpicker.hsv[2] = resx
		colorpicker.hsv[3] = 1-resy
		colorpicker.current = Color3.fromHSV(colorpicker.hsv[1],colorpicker.hsv[2],colorpicker.hsv[3])
		cpcolor.BackgroundColor3 = colorpicker.current
		updateboxes()
		colorpicker.callback(colorpicker.current)
		cpcursor:TweenPosition(UDim2.new(resx,0,resy,0),Enum.EasingDirection.Out,Enum.EasingStyle.Quad,0.15,true)
	end
	--
	button.MouseButton1Down:Connect(function()
		self.library:closewindows(colorpicker)
		cpholder.Visible = not colorpicker.open
		colorpicker.open = not colorpicker.open
	end)
	--
	huebutton.MouseButton1Down:Connect(function()
		colorpicker.hue = true
		movehue()
	end)
	--
	cpimage.MouseButton1Down:Connect(function()
		colorpicker.cp = true
		movecp()
	end)
	--
	uis.InputChanged:Connect(function()
		if colorpicker.cp then
			movecp()
		end
		if colorpicker.hue then
			movehue()
		end
	end)
	--
	uis.InputEnded:Connect(function(Input)
		if Input.UserInputType.Name == 'MouseButton1'  then
			if colorpicker.cp then
				colorpicker.cp = false
			end
			if colorpicker.hue then
				colorpicker.hue = false
			end
		end
	end)
	--
	red[2].Focused:Connect(function()
		red[3].BorderColor3 = self.library.theme.accent
	end)
	--
	red[2].FocusLost:Connect(function()
		local saved = red[2].Text
		local num = tonumber(saved)
		if num then
			saved = tostring(math.clamp(tonumber(saved),0,255))
			red[2].Text = ""
			if saved then
				if #saved >= 1 and #saved <= 3 then
					red[2].PlaceholderText = "R: "..tostring(saved)
				end
				colorpicker:set(Color3.fromRGB(tonumber(saved),colorpicker.current.G*255,colorpicker.current.B*255))
				red[3].BorderColor3 = Color3.fromRGB(12,12,12)
			else
				red[3].BorderColor3 = Color3.fromRGB(12,12,12)
			end
		else
			red[2].Text = ""
			red[3].BorderColor3 = Color3.fromRGB(12,12,12)
		end
	end)
	--
	green[2].Focused:Connect(function()
		green[3].BorderColor3 = self.library.theme.accent
	end)
	--
	green[2].FocusLost:Connect(function()
		local saved = green[2].Text
		local num = tonumber(saved)
		if num then
			saved = tostring(math.clamp(tonumber(saved),0,255))
			green[2].Text = ""
			if saved then
				if #saved >= 1 and #saved <= 3 then
					green[2].PlaceholderText = "G: "..tostring(saved)
				end
				colorpicker:set(Color3.fromRGB(colorpicker.current.R*255,tonumber(saved),colorpicker.current.B*255))
				green[3].BorderColor3 = Color3.fromRGB(12,12,12)
			else
				green[3].BorderColor3 = Color3.fromRGB(12,12,12)
			end
		else
			green[2].Text = ""
			green[3].BorderColor3 = Color3.fromRGB(12,12,12)
		end
	end)
	--
	blue[2].Focused:Connect(function()
		blue[3].BorderColor3 = self.library.theme.accent
	end)
	--
	blue[2].FocusLost:Connect(function()
		local saved = blue[2].Text
		local num = tonumber(saved)
		if num then
			saved = tostring(math.clamp(tonumber(saved),0,255))
			blue[2].Text = ""
			if saved then
				if #saved >= 1 and #saved <= 3 then
					blue[2].PlaceholderText = "B: "..tostring(saved)
				end
				colorpicker:set(Color3.fromRGB(colorpicker.current.R*255,colorpicker.current.G*255,tonumber(saved)))
				blue[3].BorderColor3 = Color3.fromRGB(12,12,12)
			else
				blue[3].BorderColor3 = Color3.fromRGB(12,12,12)
			end
		else
			blue[2].Text = ""
			blue[3].BorderColor3 = Color3.fromRGB(12,12,12)
		end
	end)
	--
	hex[2].Focused:Connect(function()
		hex[3].BorderColor3 = self.library.theme.accent
	end)
	--
	hex[2].FocusLost:Connect(function()
		local saved = hex[2].Text
		if #saved >= 6 and #saved <= 7 then
			local e,s = pcall(function()
				utility.from_hex(saved)
			end)
			if e == true then
				local hexcolor = utility.from_hex(saved)
				if hexcolor then
					colorpicker:set(hexcolor)
					hex[2].Text = ""
					hex[3].BorderColor3 = Color3.fromRGB(12,12,12)
				else
					hex[2].Text = ""
					hex[3].BorderColor3 = Color3.fromRGB(12,12,12)
				end
			else
				hex[2].Text = ""
				hex[3].BorderColor3 = Color3.fromRGB(12,12,12)
			end
		else
			hex[2].Text = ""
			hex[3].BorderColor3 = Color3.fromRGB(12,12,12)
		end
	end)
	--
	local pointer = props.pointer or props.Pointer or props.pointername or props.Pointername or props.PointerName or props.pointerName or nil
	--
	if pointer then
		if self.pointers then
			self.pointers[tostring(pointer)] = colorpicker
		end
	end
	--
	self.library.labels[#self.library.labels+1] = title
	self.library.labels[#self.library.labels+1] = hex[2]
	self.library.labels[#self.library.labels+1] = red[2]
	self.library.labels[#self.library.labels+1] = green[2]
	self.library.labels[#self.library.labels+1] = blue[2]
	self.library.labels[#self.library.labels+1] = cptitle
	-- // metatable indexing + return
	setmetatable(colorpicker, colorpickers)
	return colorpicker
end
--
function colorpickers:set(color)
	if color then
		if typeof(color) == "table" then
			color = Color3.fromRGB(color[1]*255,color[2]*255,color[3]*255)
		end
		local colorpicker = self
		local h,s,v = color:ToHSV()
		--
		local function updateboxes()
			colorpicker.red.PlaceholderText = "R: "..tostring(math.floor(colorpicker.current.R*255))
			colorpicker.green.PlaceholderText = "G: "..tostring(math.floor(colorpicker.current.G*255))
			colorpicker.blue.PlaceholderText = "B: "..tostring(math.floor(colorpicker.current.B*255))
			colorpicker.hex.PlaceholderText = "Hex: "..utility.to_hex(colorpicker.current)
		end
		--
		local function movehue()
			colorpicker.outline3.BackgroundColor3 = Color3.fromHSV(h,1,1)
			colorpicker.huecursor_inline.BackgroundColor3 = Color3.fromHSV(h,1,1)
			colorpicker.hsv[1] = h
			colorpicker.current = Color3.fromHSV(colorpicker.hsv[1],colorpicker.hsv[2],colorpicker.hsv[3])
			colorpicker.cpcolor.BackgroundColor3 = colorpicker.current
			colorpicker.huecursor:TweenPosition(UDim2.new(0.5,0,h,0),Enum.EasingDirection.Out,Enum.EasingStyle.Quad,0.15,true)
		end
		--
		local function movecp()
			colorpicker.hsv[2] = s
			colorpicker.hsv[3] = v
			colorpicker.current = Color3.fromHSV(colorpicker.hsv[1],colorpicker.hsv[2],colorpicker.hsv[3])
			colorpicker.cpcolor.BackgroundColor3 = colorpicker.current
			colorpicker.cpcursor:TweenPosition(UDim2.new(s,0,1-v,0),Enum.EasingDirection.Out,Enum.EasingStyle.Quad,0.15,true)
		end
		--
		movehue()
		movecp()
		updateboxes()
		colorpicker.callback(colorpicker.current)
	end
end
--
function sections:configloader(props)
	-- // properties
	local folder = props.folder or props.Folder
	-- // variables
	local configloader = {}
	-- // main
	local clholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,222),
			Parent = self.content
		}
	)
	--
	local outline = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Parent = clholder
		}
	)
	--
	local outline2 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Parent = outline
		}
	)
	--
	local title = utility.new(
		"TextLabel",
		{
			BackgroundTransparency = 1,
			Size = UDim2.new(1,0,0,15),
			Position = UDim2.new(0,0,0,3),
			Font = self.library.font,
			Text = "configs",
			TextColor3 = Color3.fromRGB(255,255,255),
			TextSize = self.library.textsize,
			TextStrokeTransparency = 0,
			TextXAlignment = "Center",
			Parent = outline
		}
	)
	--
	self.library.labels[#self.library.labels+1] = title
	--
	local color = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundColor3 = self.library.theme.accent,
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,-6,0,1),
			Position = UDim2.new(0.5,0,0,19),
			Parent = outline
		}
	)
	--
	table.insert(self.library.themeitems["accent"]["BackgroundColor3"],color)
	--
	local buttonsholder = utility.new(
		"Frame",
		{
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,0,64),
			Position = UDim2.new(0,0,0,150),
			Parent = outline
		}
	)
	--
	local configsholder = utility.new(
		"Frame",
		{
			AnchorPoint = Vector2.new(0.5,0),
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(12, 12, 12),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,-10,0,120),
			Position = UDim2.new(0.5,0,0,25),
			Parent = outline
		}
	)
	--
	local outline3 = utility.new(
		"Frame",
		{
			BackgroundColor3 = Color3.fromRGB(24, 24, 24),
			BorderColor3 = Color3.fromRGB(56, 56, 56),
			BorderMode = "Inset",
			BorderSizePixel = 1,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			Parent = configsholder
		}
	)
	--
	local outline4 = utility.new(
		"ScrollingFrame",
		{
			BackgroundColor3 = Color3.fromRGB(56, 56, 56),
			BackgroundTransparency = 1,
			BorderSizePixel = 0,
			Size = UDim2.new(1,0,1,0),
			Position = UDim2.new(0,0,0,0),
			ClipsDescendants = true,
			AutomaticCanvasSize = "Y",
			CanvasSize = UDim2.new(0,0,0,0),
			ScrollBarImageTransparency = 0.25,
			ScrollBarImageColor3 = Color3.fromRGB(0,0,0),
			ScrollBarThickness = 5,
			VerticalScrollBarInset = "ScrollBar",
			VerticalScrollBarPosition = "Right",
			Parent = outline3
		}
	)
	--
	utility.new(
		"UIListLayout",
		{
			FillDirection = "Vertical",
			Padding = UDim.new(0,0),
			Parent = outline4
		}
	)
	--
	local createdbuttons = {}
	local selected
	--
	local makebutton = function(name,toggled)
		local createdbutton = utility.new(
			"TextButton",
			{
				AnchorPoint = Vector2.new(0,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,0,0,18),
				Position = UDim2.new(0,0,0,0),
				Text = "",
				Parent = outline4
			}
		)
		--
		local grey = utility.new(
			"Frame",
			{
				AnchorPoint = Vector2.new(0.5,0),
				BackgroundColor3 = Color3.fromRGB(125, 125, 125),
				BackgroundTransparency = 0.9,
				BorderSizePixel = 0,
				Size = UDim2.new(1,-4,1,0),
				Position = UDim2.new(0.5,0,0,0),
				Visible = false,
				Parent = createdbutton
			}
		)
		--
		local createdtitle = utility.new(
			"TextLabel",
			{
				AnchorPoint = Vector2.new(0.5,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,-10,1,0),
				Position = UDim2.new(0.5,0,0,0),
				Font = self.library.font,	
				Text = name,
				TextColor3 = Color3.fromRGB(255,255,255),
				TextSize = self.library.textsize,
				TextStrokeTransparency = 0,
				TextXAlignment = "Left",
				Parent = createdbutton
			}
		)
		--
		self.library.labels[#self.library.labels+1] = createdtitle
		--
		local createdb = {
			["button"] = createdbutton,
			["grey"] = grey,
			["title"] = createdtitle,
			["name"] = name
		}
		--
		table.insert(createdbuttons,createdb)
		--
		if toggled then
			createdb.grey.Visible = true
			createdb.title.TextColor3 = self.library.theme.accent
			table.insert(self.library.themeitems["accent"]["TextColor3"],createdb.title)
			selected = createdb
		end
		--
		createdbutton.MouseButton1Down:Connect(function()
			for i,v in pairs(createdbuttons) do
				if v ~= createdb then
					v.grey.Visible = false
					v.title.TextColor3 = Color3.fromRGB(255,255,255)
					local find = table.find(self.library.themeitems["accent"]["TextColor3"],v.title)
					if find then
						table.remove(self.library.themeitems["accent"]["TextColor3"],find)
					end
				end
			end
			--
			createdb.grey.Visible = true
			createdb.title.TextColor3 = self.library.theme.accent
			table.insert(self.library.themeitems["accent"]["TextColor3"],createdb.title)
			selected = createdb
		end)
	end
	--
	local newbutton = function(parent,name)
		local button_holder = utility.new(
			"Frame",
			{
				BackgroundTransparency = 1,
				BorderSizePixel = 0,
				ZIndex = 5,
				Parent = parent
			}
		)
		--
		local button_outline = utility.new(
			"Frame",
			{
				BackgroundColor3 = Color3.fromRGB(24, 24, 24),
				BorderColor3 = Color3.fromRGB(12, 12, 12),
				BorderMode = "Inset",
				BorderSizePixel = 1,
				Position = UDim2.new(0,0,0,0),
				Size = UDim2.new(1,0,1,0),
				ZIndex = 5,
				Parent = button_holder
			}
		)
		--
		local button_outline2 = utility.new(
			"Frame",
			{
				BackgroundColor3 = Color3.fromRGB(24, 24, 24),
				BorderColor3 = Color3.fromRGB(56, 56, 56),
				BorderMode = "Inset",
				BorderSizePixel = 1,
				Position = UDim2.new(0,0,0,0),
				Size = UDim2.new(1,0,1,0),
				ZIndex = 5,
				Parent = button_outline
			}
		)
		--
		local button_color = utility.new(
			"Frame",
			{
				AnchorPoint = Vector2.new(0,0),
				BackgroundColor3 = Color3.fromRGB(30, 30, 30),
				BorderSizePixel = 0,
				Size = UDim2.new(1,0,0,0),
				Position = UDim2.new(0,0,0,0),
				ZIndex = 5,
				Parent = button_outline2
			}
		)
		--
		utility.new(
			"UIGradient",
			{
				Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
				Rotation = 90,
				Parent = button_color
			}
		)
		--
		local button_button = utility.new(
			"TextButton",
			{
				AnchorPoint = Vector2.new(0,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,0,1,0),
				Position = UDim2.new(0,0,0,0),
				Text = name,
				TextColor3 = Color3.fromRGB(255,255,255),
				TextSize = self.library.textsize,
				TextStrokeTransparency = 0,
				Font = self.library.font,
				ZIndex = 5,
				Parent = button_holder
			}
		)
		--
		self.library.labels[#self.library.labels+1] = button_button
		--
		return {button_holder,button_outline,button_button}
	end
	--
	local function textbox(parent)
		local textbox_holder = utility.new(
			"Frame",
			{
				BackgroundTransparency = 1,
				BorderSizePixel = 0,
				ZIndex = 5,
				Parent = parent
			}
		)
		--
		local outline5 = utility.new(
			"Frame",
			{
				BackgroundColor3 = Color3.fromRGB(24, 24, 24),
				BorderColor3 = Color3.fromRGB(12, 12, 12),
				BorderMode = "Inset",
				BorderSizePixel = 1,
				Position = UDim2.new(0,0,0,0),
				Size = UDim2.new(1,0,1,0),
				ZIndex = 5,
				Parent = textbox_holder
			}
		)
		--
		local outline6 = utility.new(
			"Frame",
			{
				BackgroundColor3 = Color3.fromRGB(24, 24, 24),
				BorderColor3 = Color3.fromRGB(56, 56, 56),
				BorderMode = "Inset",
				BorderSizePixel = 1,
				Position = UDim2.new(0,0,0,0),
				Size = UDim2.new(1,0,1,0),
				ZIndex = 5,
				Parent = outline5
			}
		)
		--
		local color2 = utility.new(
			"Frame",
			{
				AnchorPoint = Vector2.new(0,0),
				BackgroundColor3 = Color3.fromRGB(30, 30, 30),
				BorderSizePixel = 0,
				Size = UDim2.new(1,0,0,0),
				Position = UDim2.new(0,0,0,0),
				ZIndex = 5,
				Parent = outline6
			}
		)
		--
		utility.new(
			"UIGradient",
			{
				Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(199, 191, 204)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 255, 255))},
				Rotation = 90,
				Parent = color2
			}
		)
		--
		local tbox = utility.new(
			"TextBox",
			{
				AnchorPoint = Vector2.new(0.5,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,0,1,0),
				Position = UDim2.new(0.5,0,0,0),
				PlaceholderColor3 = Color3.fromRGB(178, 178, 178),
				PlaceholderText = "",
				Text = "",
				TextColor3 = Color3.fromRGB(255,255,255),
				TextSize = self.library.textsize,
				TextStrokeTransparency = 0,
				Font = self.library.font,
				ZIndex = 5,
				Parent = textbox_holder
			}
		)
		--
		local tbox_button = utility.new(
			"TextButton",
			{
				AnchorPoint = Vector2.new(0,0),
				BackgroundTransparency = 1,
				Size = UDim2.new(1,0,1,0),
				Position = UDim2.new(0,0,0,0),
				Text = "",
				TextColor3 = Color3.fromRGB(255,255,255),
				TextSize = self.library.textsize,
				TextStrokeTransparency = 0,
				Font = self.library.font,
				ZIndex = 5,
				Parent = textbox_holder
			}
		)
		--
		tbox_button.MouseButton1Down:Connect(function()
			tbox:CaptureFocus()
		end)
		--
		return {textbox_holder,tbox,outline5}
	end
	--
	local refresh = function()
		for i,v in pairs(createdbuttons) do
			v.button:Remove()
			v.grey:Remove()
			v.title:Remove()
		end
		createdbuttons = {}
		for i,v in pairs(listfiles(folder)) do
			if v:sub(-4) == ".cfg" then
				if i == 1 then 
					makebutton(v:sub(#tostring(folder)+2, -5),true)
				else
					makebutton(v:sub(#tostring(folder)+2, -5),false)
				end
			end
		end
	end
	--
	refresh()
	--
	local name = textbox(buttonsholder)
	local load = newbutton(buttonsholder,"Load")
	local delete = newbutton(buttonsholder,"Delete")
	local save = newbutton(buttonsholder,"Save")
	local create = newbutton(buttonsholder,"Create")
	--
	name[1].Size = UDim2.new(1,-10,0,20)
	load[1].Size = UDim2.new(0.5,-6,0,20)
	delete[1].Size = UDim2.new(0.5,-6,0,20)
	save[1].Size = UDim2.new(0.5,-6,0,20)
	create[1].Size = UDim2.new(0.5,-6,0,20)
	--
	name[1].Position = UDim2.new(0.5,0,0,0)
	name[1].AnchorPoint = Vector2.new(0.5,0)
	--
	load[1].Position = UDim2.new(0,5,0,22)
	load[1].AnchorPoint = Vector2.new(0,0)
	--
	delete[1].Position = UDim2.new(1,-5,0,22)
	delete[1].AnchorPoint = Vector2.new(1,0)
	--
	save[1].Position = UDim2.new(0,5,0,44)
	save[1].AnchorPoint = Vector2.new(0,0)
	--
	create[1].Position = UDim2.new(1,-5,0,44)
	create[1].AnchorPoint = Vector2.new(1,0)
	--
	name[2].PlaceholderText = "Name"
	--
	local currentname = nil
	--
	name[2].Focused:Connect(function()
		name[3].BorderColor3 = self.library.theme.accent
	end)
	--
	name[2].FocusLost:Connect(function()
		local saved = name[2].Text
		if #saved >= 3 and #saved <= 15 then
			currentname = saved
		else
			name[2].Text = ""
			currentname = nil
		end
		name[3].BorderColor3 = Color3.fromRGB(12,12,12)
	end)
	--
	load[3].MouseButton1Down:Connect(function()
		self.library:loadconfig(folder..selected.name..".cfg")
		load[2].BorderColor3 = self.library.theme.accent
		wait(0.05)
		load[2].BorderColor3 = Color3.fromRGB(12,12,12)
	end)
	--
	delete[3].MouseButton1Down:Connect(function()
		delfile(folder..selected.name..".cfg")
		delete[2].BorderColor3 = self.library.theme.accent
		wait(0.05)
		delete[2].BorderColor3 = Color3.fromRGB(12,12,12)
		wait()
		refresh()
	end)
	--
	save[3].MouseButton1Down:Connect(function()
		writefile(folder..selected.name..".cfg", self.library:saveconfig())
		save[2].BorderColor3 = self.library.theme.accent
		wait(0.05)
		save[2].BorderColor3 = Color3.fromRGB(12,12,12)
		wait()
		refresh()
	end)
	--
	create[3].MouseButton1Down:Connect(function()
		writefile(folder..currentname..".cfg", self.library:saveconfig())
		create[2].BorderColor3 = self.library.theme.accent
		wait(0.05)
		create[2].BorderColor3 = Color3.fromRGB(12,12,12)
		wait()
		refresh()
	end)
	-- // button tbl
	configloader = {
		["library"] = self.library
	}
	-- // metatable indexing + return
	setmetatable(configloader, configloaders)
	return configloader 
end


local window = library:new({textsize = 18,font = Enum.Font.RobotoMono,name = "Batman Script",color = Color3.fromRGB(0,255,255)})

local Main_1_Page = window:page({name = "Main"})
local Main_2_Page = window:page({name = "Misc"})
local Main_3_Page = window:page({name = "Teleport"})

local Main_1_left = Main_1_Page:section({name = "General",side = "left",size = 500})

local Main_2_left = Main_2_Page:section({name = "Misc",side = "left",size = 500})

local Main_3_left = Main_3_Page:section({name = "Teleport",side = "left",size = 2000})
local Main_3_right = Main_3_Page:section({name = "Totem",side = "right",size = 1000})

Main_1_left:button({name = "Autofish Stackperfect (Key:F)",def = false,callback = function()


function ShowNotification(String)
    CoreGui:SetCore(
        "SendNotification",
        {
            Title = "Notification",
            Text = String,
            Duration = 1
        }
    )
end

-- Configuration variables
local config = {
    fpsCap = 9999,
    disableChat = false,            -- Set to true to hide the chat
    enableBigButton = true,        -- Set to true to enlarge the button in the shake UI
    bigButtonScaleFactor = 2,      -- Scale factor for big button size
    shakeSpeed = 0.05,             -- Lower value means faster shake (e.g., 0.05 for fast, 0.1 for normal)
    FreezeWhileFishing = false      -- Set to true to freeze your character while fishing
}

-- Set FPS cap
setfpscap(config.fpsCap)

-- Toggle autofarm variable
local autofarmEnabled = false

-- Services
local players = game:GetService("Players")
local vim = game:GetService("VirtualInputManager")
local run_service = game:GetService("RunService")
local replicated_storage = game:GetService("ReplicatedStorage")
local localplayer = players.LocalPlayer
local playergui = localplayer.PlayerGui
local StarterGui = game:GetService("StarterGui")

-- Disable chat if the option is enabled in config
if config.disableChat then
    StarterGui:SetCoreGuiEnabled(Enum.CoreGuiType.Chat, false)
end

-- Utility functions
local utility = {blacklisted_attachments = {"bob", "bodyweld"}}; do
    function utility.simulate_click(x, y, mb)
        vim:SendMouseButtonEvent(x, y, (mb - 1), true, game, 1)
        vim:SendMouseButtonEvent(x, y, (mb - 1), false, game, 1)
    end

    function utility.move_fix(bobber)
        for index, value in bobber:GetDescendants() do
            if (value.ClassName == "Attachment" and table.find(utility.blacklisted_attachments, value.Name)) then
                value:Destroy()
            end
        end
    end
end

local farm = {reel_tick = nil, cast_tick = nil}; do

    function farm.find_rod()
        local character = localplayer.Character
        if not character then return nil end

        for _, tool in ipairs(character:GetChildren()) do
            if tool:IsA("Tool") and (tool.Name:find("rod") or tool.Name:find("Rod")) then
                return tool
            end
        end
        return nil
    end

    function farm.freeze_character(freeze)
        local character = localplayer.Character
        if character then
            local humanoid = character:FindFirstChildOfClass("Humanoid")
            if humanoid then
                if freeze then
                    humanoid.WalkSpeed = 0
                    humanoid.JumpPower = 0
                else
                    humanoid.WalkSpeed = 16  -- Default WalkSpeed
                    humanoid.JumpPower = 50  -- Default JumpPower
                end
            end
        end
    end

    function farm.cast()
        local character = localplayer.Character
        if not character then return end

        local rod = farm.find_rod()
        if not rod then return end

        -- Instantly cast without cooldown
        local args = { [1] = 100, [2] = 1 }
        rod.events.cast:FireServer(unpack(args))
        farm.cast_tick = 0  -- Reset last cast time
    end

    function farm.shake()
        local shake_ui = playergui:FindFirstChild("shakeui")
        if shake_ui then
            local safezone = shake_ui:FindFirstChild("safezone")
            local button = safezone and safezone:FindFirstChild("button")

            if button then
                -- Apply big button option from config
                if config.enableBigButton then
                    button.Size = UDim2.new(config.bigButtonScaleFactor, 0, config.bigButtonScaleFactor, 0)
                else
                    button.Size = UDim2.new(1, 0, 1, 0)  -- Reset to default size if disabled
                end

                if button.Visible then
                    utility.simulate_click(
                        button.AbsolutePosition.X + button.AbsoluteSize.X / 2,
                        button.AbsolutePosition.Y + button.AbsoluteSize.Y / 2,
                        1
                    )
                end
            end
        end
    end

    function farm.reel()
        local reel_ui = playergui:FindFirstChild("reel")
        if not reel_ui then return end

        local reel_bar = reel_ui:FindFirstChild("bar")
        if not reel_bar then return end
      
        local reel_client = reel_bar:FindFirstChild("reel")
        if not reel_client then return end

        if reel_client.Disabled == true then
            reel_client.Disabled = false
        end

        local update_colors = getsenv(reel_client).UpdateColors

        -- Instant reel without waiting
        if update_colors then
            setupvalue(update_colors, 1, 100)
            replicated_storage.events.reelfinished:FireServer(getupvalue(update_colors, 1), true)
        end
    end
  
end

-- Toggle function to start or stop the autofarm
local function toggleAutofarm()
    autofarmEnabled = not autofarmEnabled
    if autofarmEnabled then
        print("Autofarm Enabled")
    else
        print("Autofarm Disabled")
        farm.freeze_character(false)  -- Unfreeze character when autofarm stops
    end
end

-- Bind the toggle to a key (e.g., "F")
local UserInputService = game:GetService("UserInputService")
UserInputService.InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.F then  -- Change 'P' to any preferred key
        toggleAutofarm()
    end
end)

-- Main loop with rod check, configurable shake speed, and freeze feature
run_service.Heartbeat:Connect(function()
    if autofarmEnabled then
        local rod = farm.find_rod() -- Check if player is holding a rod
        if rod then
            -- Freeze character if enabled in config
            if config.FreezeWhileFishing then
                farm.freeze_character(true)
            end
            farm.cast()
            farm.shake()
            farm.reel()
        else
            -- Unfreeze character when not fishing
            farm.freeze_character(false)
        end
    end
end)


end})

Main_1_left:button({name = "Autofish fail100% (Key:F)",def = false,callback = function()


	function ShowNotification(String)
		CoreGui:SetCore(
			"SendNotification",
			{
				Title = "Notification",
				Text = String,
				Duration = 1
			}
		)
	end
	
	-- Configuration variables
	local config = {
		fpsCap = 9999,
		disableChat = false,            -- Set to true to hide the chat
		enableBigButton = true,        -- Set to true to enlarge the button in the shake UI
		bigButtonScaleFactor = 2,      -- Scale factor for big button size
		shakeSpeed = 0.05,             -- Lower value means faster shake (e.g., 0.05 for fast, 0.1 for normal)
		FreezeWhileFishing = false      -- Set to true to freeze your character while fishing
	}
	
	-- Set FPS cap
	setfpscap(config.fpsCap)
	
	-- Toggle autofarm variable
	local autofarmEnabled = false
	
	-- Services
	local players = game:GetService("Players")
	local vim = game:GetService("VirtualInputManager")
	local run_service = game:GetService("RunService")
	local replicated_storage = game:GetService("ReplicatedStorage")
	local localplayer = players.LocalPlayer
	local playergui = localplayer.PlayerGui
	local StarterGui = game:GetService("StarterGui")
	
	-- Disable chat if the option is enabled in config
	if config.disableChat then
		StarterGui:SetCoreGuiEnabled(Enum.CoreGuiType.Chat, false)
	end
	
	-- Utility functions
	local utility = {blacklisted_attachments = {"bob", "bodyweld"}}; do
		function utility.simulate_click(x, y, mb)
			vim:SendMouseButtonEvent(x, y, (mb - 1), true, game, 1)
			vim:SendMouseButtonEvent(x, y, (mb - 1), false, game, 1)
		end
	
		function utility.move_fix(bobber)
			for index, value in bobber:GetDescendants() do
				if (value.ClassName == "Attachment" and table.find(utility.blacklisted_attachments, value.Name)) then
					value:Destroy()
				end
			end
		end
	end
	
	local farm = {reel_tick = nil, cast_tick = nil}; do
	
		function farm.find_rod()
			local character = localplayer.Character
			if not character then return nil end
	
			for _, tool in ipairs(character:GetChildren()) do
				if tool:IsA("Tool") and (tool.Name:find("rod") or tool.Name:find("Rod")) then
					return tool
				end
			end
			return nil
		end
	
		function farm.freeze_character(freeze)
			local character = localplayer.Character
			if character then
				local humanoid = character:FindFirstChildOfClass("Humanoid")
				if humanoid then
					if freeze then
						humanoid.WalkSpeed = 0
						humanoid.JumpPower = 0
					else
						humanoid.WalkSpeed = 16  -- Default WalkSpeed
						humanoid.JumpPower = 50  -- Default JumpPower
					end
				end
			end
		end
	
		function farm.cast()
			local character = localplayer.Character
			if not character then return end
	
			local rod = farm.find_rod()
			if not rod then return end
	
			-- Instantly cast without cooldown
			local args = { [1] = 100, [2] = 1 }
			rod.events.cast:FireServer(unpack(args))
			farm.cast_tick = 0  -- Reset last cast time
		end
	
		function farm.shake()
			local shake_ui = playergui:FindFirstChild("shakeui")
			if shake_ui then
				local safezone = shake_ui:FindFirstChild("safezone")
				local button = safezone and safezone:FindFirstChild("button")
	
				if button then
					-- Apply big button option from config
					if config.enableBigButton then
						button.Size = UDim2.new(config.bigButtonScaleFactor, 0, config.bigButtonScaleFactor, 0)
					else
						button.Size = UDim2.new(1, 0, 1, 0)  -- Reset to default size if disabled
					end
	
					if button.Visible then
						utility.simulate_click(
							button.AbsolutePosition.X + button.AbsoluteSize.X / 2,
							button.AbsolutePosition.Y + button.AbsoluteSize.Y / 2,
							1
						)
					end
				end
			end
		end
	
		function farm.reel()
			local reel_ui = playergui:FindFirstChild("reel")
			if not reel_ui then return end
	
			local reel_bar = reel_ui:FindFirstChild("bar")
			if not reel_bar then return end
		  
			local reel_client = reel_bar:FindFirstChild("reel")
			if not reel_client then return end
	
			if reel_client.Disabled == true then
				reel_client.Disabled = false
			end
	
			local update_colors = getsenv(reel_client).UpdateColors
	
			-- Instant reel without waiting
			if update_colors then
				setupvalue(update_colors, 1, 0)
				replicated_storage.events.reelfinished:FireServer(getupvalue(update_colors, 1), true)
			end
		end
	  
	end
	
	-- Toggle function to start or stop the autofarm
	local function toggleAutofarm()
		autofarmEnabled = not autofarmEnabled
		if autofarmEnabled then
			print("Autofarm Enabled")
		else
			print("Autofarm Disabled")
			farm.freeze_character(false)  -- Unfreeze character when autofarm stops
		end
	end
	
	-- Bind the toggle to a key (e.g., "F")
	local UserInputService = game:GetService("UserInputService")
	UserInputService.InputBegan:Connect(function(input)
		if input.KeyCode == Enum.KeyCode.F then  -- Change 'P' to any preferred key
			toggleAutofarm()
		end
	end)
	
	-- Main loop with rod check, configurable shake speed, and freeze feature
	run_service.Heartbeat:Connect(function()
		if autofarmEnabled then
			local rod = farm.find_rod() -- Check if player is holding a rod
			if rod then
				-- Freeze character if enabled in config
				if config.FreezeWhileFishing then
					farm.freeze_character(true)
				end
				farm.cast()
				farm.shake()
				farm.reel()
			else
				-- Unfreeze character when not fishing
				farm.freeze_character(false)
			end
		end
	end)
	
	
	end})

Main_1_left:button({name = "Press F (mobile)",def = false,callback = function()
    local VirtualInputManager = game:GetService("VirtualInputManager")

-- Simulate pressing the F key once
VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.F, false, game)  -- Key down
task.wait(0.1)  -- Wait a short time to simulate key press duration
VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.F, false, game)  -- Key up
end})

Main_1_left:button({name = "Freeze (Key:X)",def = false,callback = function()
	local Players = game:GetService("Players")
	local UserInputService = game:GetService("UserInputService")
	local LocalPlayer = Players.LocalPlayer
	local toggleKey = Enum.KeyCode.X
	
	local isFrozen = false
	local freezeCFrame
	
	-- Function to save the player's current CFrame
	local function savePosition()
		local character = LocalPlayer.Character
		if character and character:FindFirstChild("HumanoidRootPart") then
			freezeCFrame = character.HumanoidRootPart.CFrame
		end
	end
	
	-- Function to keep teleporting the player back to the saved CFrame
	local function freezePlayer()
		while isFrozen do
			local character = LocalPlayer.Character
			if character and character:FindFirstChild("HumanoidRootPart") and freezeCFrame then
				character.HumanoidRootPart.CFrame = freezeCFrame
			end
			task.wait(0.1)  -- Adjust delay for smoother or stricter freezing
		end
	end
	
	-- Toggle freeze on or off with the key press
	UserInputService.InputBegan:Connect(function(input, gameProcessedEvent)
		if not gameProcessedEvent and input.KeyCode == toggleKey then
			isFrozen = not isFrozen
			if isFrozen then
				savePosition()
				freezePlayer()
				print("Freeze enabled.")
			else
				print("Freeze disabled.")
			end
		end
	end)	
end})

Main_1_left:button({name = "Press X (mobile)",def = false,callback = function()
    local VirtualInputManager = game:GetService("VirtualInputManager")

-- Simulate pressing the F key once
VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.X, false, game)  -- Key down
task.wait(0.1)  -- Wait a short time to simulate key press duration
VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.X, false, game)  -- Key up
end})

Main_1_left:button({name = "Dupe Rod Of The Eternal King key:(P)",def = false,callback = function()
	local UserInputService = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")

local targetPlayer = Players.LocalPlayer
local runningRodSwitch = false

local function toggleRodSwitching()
    runningRodSwitch = not runningRodSwitch

    if runningRodSwitch then
        print("Started rod switching.")
        task.spawn(function()
            while runningRodSwitch do
                ReplicatedStorage.events.equiprod:FireServer("Rod Of The Depths")
                ReplicatedStorage.events.equiprod:FireServer("Rod Of The Eternal King")
                task.wait(0.03)
            end
        end)
    else
        print("Stopped rod switching.")
    end
end

UserInputService.InputBegan:Connect(function(input, isProcessed)
    if not isProcessed then
        if input.KeyCode == Enum.KeyCode.P then
            toggleRodSwitching()
        end
    end
end)

local function equipAndSendOffer(item)
    item.Parent = targetPlayer.Character
    print("Item equipped:", item.Name)
end
end})

Main_1_left:button({name = "Dupe Wisdom key:(O)",def = false,callback = function()
	local UserInputService = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")

local targetPlayer = Players.LocalPlayer
local runningRodSwitch = false

local function toggleRodSwitching()
    runningRodSwitch = not runningRodSwitch

    if runningRodSwitch then
        print("Started rod switching.")
        task.spawn(function()
            while runningRodSwitch do
                ReplicatedStorage.events.equiprod:FireServer("Rod Of The Depths")
                ReplicatedStorage.events.equiprod:FireServer("Wisdom Rod")
                task.wait(0.03)
            end
        end)
    else
        print("Stopped rod switching.")
    end
end

UserInputService.InputBegan:Connect(function(input, isProcessed)
    if not isProcessed then
        if input.KeyCode == Enum.KeyCode.O then
            toggleRodSwitching()
        end
    end
end)

local function equipAndSendOffer(item)
    item.Parent = targetPlayer.Character
    print("Item equipped:", item.Name)
end
end})

Main_1_left:button({name = "Dupe Fang key:(L)",def = false,callback = function()
	local UserInputService = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")

local targetPlayer = Players.LocalPlayer
local runningRodSwitch = false

local function toggleRodSwitching()
    runningRodSwitch = not runningRodSwitch

    if runningRodSwitch then
        print("Started rod switching.")
        task.spawn(function()
            while runningRodSwitch do
                ReplicatedStorage.events.equiprod:FireServer("Rod Of The Depths")
                ReplicatedStorage.events.equiprod:FireServer("Rod Of The Forgotten Fang")
                task.wait(0.03)
            end
        end)
    else
        print("Stopped rod switching.")
    end
end

UserInputService.InputBegan:Connect(function(input, isProcessed)
    if not isProcessed then
        if input.KeyCode == Enum.KeyCode.L then
            toggleRodSwitching()
        end
    end
end)

local function equipAndSendOffer(item)
    item.Parent = targetPlayer.Character
    print("Item equipped:", item.Name)
end
end})

Main_1_left:keybind({name = "set ui keybind",def = nil,callback = function(key)
   window.key = key
end})

Main_2_left:button({name = "fps 10",callback = function()
	setfpscap(10)
end})

Main_2_left:button({name = "recall fps",callback = function()
	setfpscap(1000)
end})

Main_2_left:button({name = "Inf Oxygen",callback = function()
    local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- Find the LocalPlayer's character in workspace
local playerFolder = workspace:FindFirstChild(LocalPlayer.Name)
local oxygenScript = playerFolder and playerFolder:FindFirstChild("client") and playerFolder.client:FindFirstChild("oxygen")

-- Check if the script exists and is a LocalScript, then disable it
if oxygenScript and oxygenScript:IsA("LocalScript") then
    oxygenScript.Disabled = true
end

end})

Main_2_left:button({name = "Equip tool",callback = function()
		local Players = game:GetService("Players")
		local player = Players.LocalPlayer
		local character = player.Character or player.CharacterAdded:Wait()
		local backpack = player:WaitForChild("Backpack")
		
		-- Function to equip a tool
		local function equipTool(toolName)
			local tool = backpack:FindFirstChild(toolName) or character:FindFirstChild(toolName)
			if tool and tool:IsA("Tool") then
				tool.Parent = character
			end
		end
		
		-- Example usage
		equipTool("No-Life Rod")
		equipTool("Rapid Rod")
		equipTool("Nocturnal Rod")
		equipTool("Lucky Rod")
		equipTool("Destiny Rod")
		equipTool("Aurora Rod")
		equipTool("Fast Rod")
		equipTool("Training Rod")
		equipTool("Buddy Bond Rod")
		equipTool("Reinforced Rod")
		equipTool("Rod Of The Depths")
		equipTool("Scurvy Rod")
		equipTool("Steady Rod")
		equipTool("Trident Rod")
		equipTool("Ultratech Rod")
		equipTool("Tetra Rod")
		equipTool("Mythical Rod")
		equipTool("Magma Rod")
		equipTool("Magnet Rod")
		equipTool("Mystic Staff")
		equipTool("Midas Rod")
		equipTool("Executive Rod")
		equipTool("Haunted Rod")
		equipTool("Fischer's Rod")
		equipTool("Kings Rod")
end})

Main_2_left:button({name = "Sell All",callback = function()
    workspace:WaitForChild("world"):WaitForChild("npcs"):WaitForChild("Marc Merchant"):WaitForChild("merchant"):WaitForChild("sellall"):InvokeServer()
end})

Main_2_left:button({name = "Sell Held Item",callback = function()
    workspace:WaitForChild("world"):WaitForChild("npcs"):WaitForChild("Marc Merchant"):WaitForChild("merchant"):WaitForChild("sell"):InvokeServer()
end})

Main_2_left:button({name = "Appraise Held Item",callback = function()
    workspace:WaitForChild("world"):WaitForChild("npcs"):WaitForChild("Appraiser"):WaitForChild("appraiser"):WaitForChild("appraise"):InvokeServer()
end})

Main_2_left:button({name = "TP To Seller",callback = function()
    local player = game.Players.LocalPlayer
player.Character.HumanoidRootPart.CFrame = CFrame.new(476, 151, 232)
end})

Main_2_left:button({name = "Auto fix map",callback = function()
	for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do 
        if v.Name == "Treasure Map" then
            game.Players.LocalPlayer.Character.Humanoid:EquipTool(v)
            workspace.world.npcs["Jack Marrow"].treasure.repairmap:InvokeServer()
        end
    end
end})

Main_2_left:button({name = "Auto Press E",callback = function()
	local VirtualInputManager = game:GetService("VirtualInputManager")

for i = 1, 50 do
    VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.E, false, game)
    VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.E, false, game)
    wait(0.3) -- Small delay to avoid overwhelming the game
end

end})

Main_2_left:button({name = "White Screen (Key:P)",callback = function()
	local enabled = true

local function toggle3DRendering()
    enabled = not enabled
    game:GetService("RunService"):Set3dRenderingEnabled(enabled)
    print("3D rendering enabled:", enabled)
end

game:GetService("UserInputService").InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.P then
        toggle3DRendering()
    end
end)
end})

Main_3_left:button({name = "Frightful Pool",callback = function()
    local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Workspace = game:GetService("Workspace")

-- Target CFrame with Y offset
local targetPart = Workspace.zones.fishing.FischFright24

if targetPart then
    -- Get the current position of the target part and add 100 to the Y coordinate
    local newPosition = targetPart.Position + Vector3.new(0, 100, 0)

    -- Teleport the LocalPlayer's character to the new position
    local character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
    character:SetPrimaryPartCFrame(CFrame.new(newPosition))
else
    print("Not Spawn Yet.")
end
end})

Main_3_left:button({name = "Merchant Boat",callback = function()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local targetObject = workspace.active:FindFirstChild("Merchant Boat") and workspace.active["Merchant Boat"]:FindFirstChild("1")
    
    if character and targetObject then
        local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
        if humanoidRootPart then
            -- Teleport the player to the target object's CFrame
            humanoidRootPart.CFrame = targetObject.CFrame
        else
            warn("HumanoidRootPart not found.")
        end
    else
        warn("Merchant Boat 1")
    end
    
end})

Main_2_left:button({name = "Buy Relic",callback = function()
	while wait(0.2) do
		workspace:WaitForChild("world"):WaitForChild("npcs"):WaitForChild("Merlin"):WaitForChild("Merlin"):WaitForChild("power"):InvokeServer()
	end 
end})

Main_2_left:button({name = "Go To Witch",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(405, 135, 318))
end})

Main_2_left:button({name = "Sell Held Item",callback = function()
    workspace:WaitForChild("world"):WaitForChild("npcs"):WaitForChild("Marc Merchant"):WaitForChild("merchant"):WaitForChild("sell"):InvokeServer()
end})

Main_2_left:button({name = "Deploy Crab Cage",callback = function()
    local args = {
		[1] = {
			["CFrame"] = CFrame.new(2814.69384765625, 126.5, -646.474365234375, 0.6434483528137207, 7.951216574042519e-09, -0.7654895186424255, -4.285541521653613e-08, 1, -2.563592182980301e-08, 0.7654895186424255, 4.9300762583470714e-08, 0.6434483528137207)
		}
	}
	
	game:GetService("Players").LocalPlayer.Character:FindFirstChild("Crab Cage").Deploy:FireServer(unpack(args))
end})

Main_2_left:button({name = "Deploy 5000 Cages",callback = function()
	for i = 1, 5000 do
		local args = {
			[1] = {
				["CFrame"] = CFrame.new(2814.69384765625, 126.5, -646.474365234375, 0.6434483528137207, 7.951216574042519e-09, -0.7654895186424255, -4.285541521653613e-08, 1, -2.563592182980301e-08, 0.7654895186424255, 4.9300762583470714e-08, 0.6434483528137207)
			}
		}
	
		game:GetService("Players").LocalPlayer.Character:FindFirstChild("Crab Cage").Deploy:FireServer(unpack(args))
	end

end})

Main_2_left:button({name = "Fps Boost",callback = function()
    local ToDisable = {
        Textures = true,
        VisualEffects = true,
        Parts = true,
        Particles = true,
        Sky = true
    }
    
    local ToEnable = {
        FullBright = false
    }
    
    local Stuff = {}
    
    for _, v in next, game:GetDescendants() do
        if ToDisable.Parts then
            if v:IsA("Part") or v:IsA("Union") or v:IsA("BasePart") then
                v.Material = Enum.Material.SmoothPlastic
                table.insert(Stuff, 1, v)
            end
        end
        
        if ToDisable.Particles then
            if v:IsA("ParticleEmitter") or v:IsA("Smoke") or v:IsA("Explosion") or v:IsA("Sparkles") or v:IsA("Fire") then
                v.Enabled = false
                table.insert(Stuff, 1, v)
            end
        end
        
        if ToDisable.VisualEffects then
            if v:IsA("BloomEffect") or v:IsA("BlurEffect") or v:IsA("DepthOfFieldEffect") or v:IsA("SunRaysEffect") then
                v.Enabled = false
                table.insert(Stuff, 1, v)
            end
        end
        
        if ToDisable.Textures then
            if v:IsA("Decal") or v:IsA("Texture") then
                v.Texture = ""
                table.insert(Stuff, 1, v)
            end
        end
        
        if ToDisable.Sky then
            if v:IsA("Sky") then
                v.Parent = nil
                table.insert(Stuff, 1, v)
            end
        end
    end
    
    game:GetService("TestService"):Message("Effects Disabler Script : Successfully disabled "..#Stuff.." assets / effects. Settings :")
    
    for i, v in next, ToDisable do
        print(tostring(i)..": "..tostring(v))
    end
    
    if ToEnable.FullBright then
        local Lighting = game:GetService("Lighting")
        
        Lighting.FogColor = Color3.fromRGB(255, 255, 255)
        Lighting.FogEnd = math.huge
        Lighting.FogStart = math.huge
        Lighting.Ambient = Color3.fromRGB(255, 255, 255)
        Lighting.Brightness = 5
        Lighting.ColorShift_Bottom = Color3.fromRGB(255, 255, 255)
        Lighting.ColorShift_Top = Color3.fromRGB(255, 255, 255)
        Lighting.OutdoorAmbient = Color3.fromRGB(255, 255, 255)
        Lighting.Outlines = true
    end
end})

Main_2_left:button({name = "infinteyield",callback = function()
    loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
end})

Main_3_left:button({name = "Ancient Isle (new)",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(6066, 195, 288))
end})

Main_3_left:button({name = "Ancient Isle น้ำตก (new)",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(5807, 135, 407))
end})

Main_3_left:button({name = "Pillar totem (new)",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-3154, -755, 2197))
end})

Main_3_left:button({name = "Rod craft (new)",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-3160, -745, 1683))
end})

Main_3_left:button({name = "Tp megalodon (new)",callback = function()

	local player = game.Players.LocalPlayer
	local targetPath = workspace.zones.fishing:WaitForChild("Megalodon Default")
	local yOffset = 10
	local baseplateOffset = -10
	
	if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
		local rootPart = player.Character.HumanoidRootPart
	
		-- Teleport player to the target location
		rootPart.CFrame = targetPath.CFrame + Vector3.new(0, yOffset, 0)
	
		-- Create a baseplate under the player's position
		local baseplate = Instance.new("Part")
		baseplate.Size = Vector3.new(10, 1, 10) -- Size of the baseplate
		baseplate.Position = rootPart.Position + Vector3.new(0, baseplateOffset, 0)
		baseplate.Anchored = true
		baseplate.BrickColor = BrickColor.new("Bright green") -- Optional, to give it a color
		baseplate.Parent = workspace
	end
	
	
end})

Main_3_left:button({name = "Tp meteor (new)",callback = function()
	local player = game.Players.LocalPlayer
local meteorItems = workspace:WaitForChild("MeteorItems")

-- Function to teleport to the first found part in MeteorItems
local function teleportToMeteorItem()
    if not player.Character or not player.Character:FindFirstChild("HumanoidRootPart") then return end
    local rootPart = player.Character.HumanoidRootPart

    for _, item in ipairs(meteorItems:GetDescendants()) do
        if item:IsA("BasePart") then
            rootPart.CFrame = item.CFrame
            break -- Teleport to the first part found
        end
    end
end

teleportToMeteorItem()

end})

Main_3_left:button({name = "Moosewood",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(386, 135, 252))
end})

Main_3_left:button({name = "Statue",callback = function()
    local Players = game:GetService("Players")
    Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(73, 142, -1028))
end})

Main_3_left:button({name = "Lava",callback = function()
    local Players = game:GetService("Players")
    Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-1889, 168, 329))
end})

Main_3_left:button({name = "Arch",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(999, 131, -1237))
end})

Main_3_left:button({name = "spike",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-1255, 138, 1554))
end})

Main_3_left:button({name = "Birch",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(1742, 142, -2502))
end})

Main_3_left:button({name = "Mushgrove",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(2501, 131, -721))
end})

Main_3_left:button({name = "Keepers",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(1296, -805, -299))
end})

Main_3_left:button({name = "Executive",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-30, -247, 199))
end})

Main_3_left:button({name = "Swamp",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(2501, 131, -721))
end})

Main_3_left:button({name = "Snowcap",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(2649, 142, 2521))
end})

Main_3_left:button({name = "Wilson",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(2939, 281, 2567))
end})

Main_3_left:button({name = "Roslit",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-1477, 134, 672))
end})

Main_3_left:button({name = "Vertigo",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-112, -515, 1040))
end})

Main_3_left:button({name = "Sunstone",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-933, 132, -1120))
end})

Main_3_left:button({name = "Terrapin",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-144, 145, 1910))
end})

Main_3_left:button({name = "Birch",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(1739, 141, -2486))
end})

Main_3_left:button({name = "Deepshop",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-984, -245, -2704))
end})

Main_3_left:button({name = "Deepshop2",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-1659, -214, -2846))
end})

Main_3_left:button({name = "Trident",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-1484, -224, -2198))
end})

Main_3_left:button({name = "Brine Pool",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-1788, -143, -3418))
end})

Main_3_left:button({name = "Deep Ocean (safeplace)",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-508, -62, -7688))
end})

Main_3_left:button({name = "Buy luck",callback = function()
	local Players = game:GetService("Players")
	Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-931, 226, -995))
end})

Main_3_left:button({name = "Forsaken shore",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-2504, 136, 1573))
end})

Main_3_left:button({name = "Captain goldenfish",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-2753, 217, 1729))
end})

Main_3_left:button({name = "Priate",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-2823, 214, 1521))
end})

Main_3_left:button({name = "Chest",callback = function()
	local chests = workspace.world.chests:GetChildren()
local player = game.Players.LocalPlayer
local lastChest = 0  -- Keeps track of the last teleported chest

-- Teleport to the next chest
lastChest = (lastChest % #chests) + 1  -- Cycle through each chest
player.Character.HumanoidRootPart.CFrame = chests[lastChest].CFrame

end})

Main_3_left:button({name = "Shipwreck",callback = function()
	local Players = game:GetService("Players")
	Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-3596, 141, 1605))
end})

Main_3_left:button({name = "Snowcap inside",callback = function()
	local Players = game:GetService("Players")
	Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(2848, 135, 2615))
end})

Main_3_left:button({name = "upper deepsolate",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-791, 142, -3103))
end})

Main_3_left:button({name = "Vertigo outside",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-7, -706, 1229))
end})

Main_3_left:button({name = "Vertigo inside",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(95, -701, 1225))
end})

Main_3_left:button({name = "Depth",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(574, -704, 1225))
end})

Main_3_left:button({name = "Depth merchant",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(949, -712, 1255))
end})

Main_3_left:button({name = "Abyssal",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(1208.90796, -716.287781, 1316.12476, -0.258864403, 0, 0.965913713, 0, 1, 0, -0.965913713, 0, -0.258864403))
end})

Main_3_left:button({name = "Hexed",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(1051.00208, -632.073181, 1316.28882, -0.998992562, 0, -0.0448761396, 0, 1, 0, 0.0448761396, 0, -0.998992562))
end})

Main_3_left:button({name = "Best Farm Zone",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(1047, -782, 1056))
end})

Main_3_left:button({name = "The Depths Serpent Zone",callback = function()
-- Script to teleport to "The Depths - Serpent" or show a notification
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
local HumanoidRootPart = Character:WaitForChild("HumanoidRootPart")

-- Pathway to the target zone
local zonePath = workspace.zones.fishing:FindFirstChild("The Depths - Serpent")

-- Function to notify player
local function notifyPlayer(message)
    game.StarterGui:SetCore("SendNotification", {
        Title = "Notification";
        Text = message;
        Duration = 5; -- Duration of notification
    })
end

-- Check if the zone exists
if zonePath then
    -- Teleport to the zone
    HumanoidRootPart.CFrame = zonePath.CFrame
    notifyPlayer("Teleported to The Depths - Serpent!")
else
    -- Notify if the zone does not exist
    notifyPlayer("The Depths - Serpent has not spawned yet!")
end
end})

Main_3_left:button({name = "Rod of the Depths",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(1703, -903, 1444))
end})

Main_3_left:button({name = "GUi check isonade",callback = function()
	wait(0.1)
local PathwayName = "Isonade"
local PathwayParent = workspace.zones.fishing

-- Create GUI
local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "IsonadeNotifier"
screenGui.Parent = playerGui

local textLabel = Instance.new("TextLabel")
textLabel.Size = UDim2.new(0.5, 0, 0.1, 0) -- Width and height
textLabel.Position = UDim2.new(0.25, 0, 0.05, 0) -- Center at top
textLabel.BackgroundTransparency = 1 -- Transparent background
textLabel.Text = ""
textLabel.Font = Enum.Font.SourceSansBold
textLabel.TextSize = 36
textLabel.TextColor3 = Color3.new(1, 0, 0) -- Red text
textLabel.Parent = screenGui

-- Monitor Isonade
local function monitorIsonade()
    while true do
        local pathway = PathwayParent:FindFirstChild(PathwayName)
        if pathway then
            textLabel.Text = "Isonade spawned!!!"
        else
            textLabel.Text = "" -- Clear text when Isonade is gone
        end
        wait(0.5) -- Check every 0.5 seconds
    end
end

-- Start monitoring in a separate thread
task.spawn(monitorIsonade)

end})

Main_3_left:button({name = "Tp to Isonade",callback = function()
	local Players = game:GetService("Players")

local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

local targetPathway = workspace.zones.fishing:FindFirstChild("Isonade")
if targetPathway then
    local targetPosition = targetPathway.Position
    -- Set the Y-axis to 130 while keeping the X and Z coordinates of the pathway
    humanoidRootPart.CFrame = CFrame.new(targetPosition.X, 130, targetPosition.Z)
else
    warn("Target pathway not found!")
end

end})

Main_3_left:button({name = "Scurvy Rod (new)",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-2826, 215, 1513))
end})

Main_3_left:button({name = "Secert elevator",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(2232, -803, 1014))
end})

Main_3_left:button({name = "AncientIslesMini",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(4040, 131, 78))
end})

Main_3_left:button({name = "Relic Rod",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(4098, 40, 28))
end})

Main_3_left:button({name = "TP BOAT MOOSEWOOD (new)",callback = function()
	local player = game.Players.LocalPlayer
	local boatsFolder = workspace:WaitForChild("active"):WaitForChild("boats")
	local targetPosition = Vector3.new(328, 121, 298) -- Set the desired position here
	
	-- Function to search for a part named "Base" in the model
	local function findBasePart(model)
		for _, descendant in pairs(model:GetDescendants()) do
			if descendant:IsA("BasePart") and descendant.Name == "Base" then
				return descendant
			end
		end
		return nil
	end
	
	-- Function to set PrimaryPart and teleport the player's boat
	local function teleportBoat()
		local playerName = player.Name
		local boat = boatsFolder:FindFirstChild(playerName)
		
		if boat and boat:IsA("Model") then
			-- Set a PrimaryPart if it doesn't have one
			if not boat.PrimaryPart then
				local basePart = findBasePart(boat)
				if basePart then
					boat.PrimaryPart = basePart
				else
					warn("No part named 'Base' found in the boat model.")
					return
				end
			end
			
			-- Teleport the boat
			boat:SetPrimaryPartCFrame(CFrame.new(targetPosition))
		else
			warn("Boat for player not found in workspace.active.boats")
		end
	end
	
	-- Execute the teleport
	teleportBoat()
	
end})

Main_3_left:button({name = "TP BOAT ISLE (new)",callback = function()
	local player = game.Players.LocalPlayer
	local boatsFolder = workspace:WaitForChild("active"):WaitForChild("boats")
	local targetPosition = Vector3.new(5772, 128, 355) -- Set the desired position here
	
	-- Function to search for a part named "Base" in the model
	local function findBasePart(model)
		for _, descendant in pairs(model:GetDescendants()) do
			if descendant:IsA("BasePart") and descendant.Name == "Base" then
				return descendant
			end
		end
		return nil
	end
	
	-- Function to set PrimaryPart and teleport the player's boat
	local function teleportBoat()
		local playerName = player.Name
		local boat = boatsFolder:FindFirstChild(playerName)
		
		if boat and boat:IsA("Model") then
			-- Set a PrimaryPart if it doesn't have one
			if not boat.PrimaryPart then
				local basePart = findBasePart(boat)
				if basePart then
					boat.PrimaryPart = basePart
				else
					warn("No part named 'Base' found in the boat model.")
					return
				end
			end
			
			-- Teleport the boat
			boat:SetPrimaryPartCFrame(CFrame.new(targetPosition))
		else
			warn("Boat for player not found in workspace.active.boats")
		end
	end
	
	-- Execute the teleport
	teleportBoat()
	
end})


Main_3_right:button({name = "Sundial Totem",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-1146, 134, -1071))
end})

Main_3_right:button({name = "Eclipse Totem",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(5967, 274, 841))
end})

Main_3_right:button({name = "Meteor Totem",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-1949, 275, 231))
end})

Main_3_right:button({name = "Tempest Totem",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(34, 133, 1941))
end})

Main_3_right:button({name = "Windset Totem",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(2844, 179, 2700))
end})

Main_3_right:button({name = "Smokescreen Totem",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(2791, 140, -626))
end})

Main_3_right:button({name = "Aurora Totem",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(-1812, -137, -3282))
end})

Main_3_right:button({name = "Dr. Finneus (NPC)",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(1169.18237, 132.075562, 2456.31689, 0, 0, -1, 0, 1, 0, 1, 0, 0))
end})

Main_3_right:button({name = "Abyssus (NPC)",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(1399.04749, -1018.03229, 966.244202, -0.351242661, -0.155072242, -0.923353255, 0.0506991558, 0.981591761, -0.184139013, 0.934910834, -0.111490704, -0.336914897))
end})

Main_3_right:button({name = "Aspicientis (NPC)",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(1214.53125, -708.644043, 1320.80188, 0.225700855, 0.128283948, 0.965713382, -0.0272023976, 0.991735399, -0.125383079, -0.973816752, 0.00202933699, 0.227325141))
end})

Main_3_right:button({name = "Occultus (NPC)",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(1022.30933, -705.266174, 1564.73145, 0.996510863, -0.0350344256, 0.0757544413, 0.0481100902, 0.982790411, -0.178349033, -0.0682023838, 0.181371287, 0.981046855))
end})

Main_3_right:button({name = "Perditus (NPC)",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(770.052124, -730.62854, 1383.49512, 0.980628371, 0.0350823216, -0.19271028, -0.0284765773, 0.99891156, 0.0369425006, 0.193796545, -0.0307391342, 0.980560064))
end})

Main_3_right:button({name = "Submersus (NPC)",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(1211.42651, -1015.7981, 1315.828, -0.990251422, 0.0733327195, 0.118424594, 0.0506683066, 0.981590569, -0.184153795, -0.12974897, -0.176358193, -0.975737095))
end})

Main_3_right:button({name = "Tenebris (NPC)",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(1061.18408, -631.130432, 1310.31323, -0.730399609, -0.0307225361, 0.682328701, -0.0463540554, 0.998914301, -0.00464264117, -0.681445241, -0.0350196883, -0.731030703))
end})

Main_3_right:button({name = "FARM XP",callback = function()
	local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

-- List of positions
local positions = {
    Vector3.new(386, 135, 252),
    Vector3.new(73, 142, -1028),
    Vector3.new(-1889, 168, 329),
    Vector3.new(-1255, 138, 1554),
    Vector3.new(999, 131, -1237),
    Vector3.new(1742, 142, -2502),
    Vector3.new(2501, 131, -721),
    Vector3.new(1296, -805, -299),
    Vector3.new(-30, -247, 199),
    Vector3.new(2501, 131, -721),
    Vector3.new(2649, 142, 2521),
    Vector3.new(2939, 281, 2567),
    Vector3.new(-1477, 134, 672),
    Vector3.new(-112, -515, 1040),
    Vector3.new(-933, 132, -1120),
    Vector3.new(-144, 145, 1910),
    Vector3.new(1739, 141, -2486),
    Vector3.new(-984, -245, -2704),
    Vector3.new(-1659, -214, -2846),
    Vector3.new(-1484, -224, -2198),
    Vector3.new(-1788, -143, -3418),
    Vector3.new(-2504, 136, 1573),
    Vector3.new(-791, 142, -3103),
    Vector3.new(-7, -706, 1229),
    Vector3.new(95, -701, 1225),
    Vector3.new(574, -704, 1225),
    Vector3.new(949, -712, 1255),
    Vector3.new(1703, -903, 1444)
}

-- Teleport to each position with a 3-second delay
for _, position in ipairs(positions) do
    humanoidRootPart.CFrame = CFrame.new(position)
    print("Teleported to:", position)
    task.wait(2) -- Wait 3 seconds
end

end})

Main_3_right:button({name = "Deep ocean Fragment",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(5843, 79, 383))
end})

Main_3_right:button({name = "Earth Fragment",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(5972, 274, 846))
end})

Main_3_right:button({name = "Elcipse Fragment",callback = function()
    local Players = game:GetService("Players")
Players.LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(6073, 444, 684))
end})


return library
