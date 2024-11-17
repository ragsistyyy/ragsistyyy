






local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Consistt/Ui/main/UnLeaked"))()


library.rank = "dev"
local Wm = library:Watermark("zizihub.xyz | v" .. library.version ..  " | " .. library:GetUsername() .. " | rank: " .. library.rank)
local FpsWm = Wm:AddWatermark("fps: " .. library.fps)
coroutine.wrap(function()
    while wait(.75) do
        FpsWm:Text("fps: " .. library.fps)
    end
end)()


local Notif = library:InitNotifications()

for i = 20,0,-1 do 
    task.wait(0.05)
    local LoadingXSX = Notif:Notify("Loading zizihub.xyz v2, please be patient.", 3, "information") -- notification, alert, error, success, information
end 

library.title = "      zizihub.xyz | project delta | dev access"

library:Introduction()
wait(1)
local Init = library:Init()

local Tab1 = Init:NewTab("Combat")

local Section1 = Tab1:NewSection("Ragebot")

local Toggle1 = Tab1:NewToggle("silent", false, function(value)
    local vers = value and "on" or "off"
end)

local Toggle1 = Tab1:NewToggle("include ai", false, function(value)
    local vers = value and "on" or "off"
end)

local Toggle1 = Tab1:NewToggle("fov circle", false, function(value)
    local vers = value and "on" or "off"
end)


local Slider1 = Tab1:NewSlider("fov circle", "", true, "/", {min = 0, max = 100, default = 0}, function(value)
    print(value)
end)

local Slider1 = Tab1:NewSlider("hitchance", "", true, "/", {min = 0, max = 100, default = 0}, function(value)
    print(value)
end)

local Section1 = Tab1:NewSection("Legitbot")


local Toggle1 = Tab1:NewToggle("aimbot", false, function(value)
    local vers = value and "on" or "off"
end)

local Toggle1 = Tab1:NewToggle("sensitivity", false, function(value)
    local vers = value and "on" or "off"
end)

local Slider1 = Tab1:NewSlider("smoothness", "", true, "/", {min = 0, max = 100, default = 0}, function(value)
    print(value)
end)

local Toggle1 = Tab1:NewToggle("fov circle", false, function(value)
    local vers = value and "on" or "off"
end)


local Selector1 = Tab1:NewSelector("Hitbox", "hitpart", {"Head", "Hummanoidrootpart", "UpperTorso", "LowerTorso"}, function(d)
    print(d)
end)


local Tab1 = Init:NewTab("Visuals")

local Section1 = Tab1:NewSection("ESP")

local Toggle1 = Tab1:NewToggle("enable esp", false, function(value)
    local vers = value and "on" or "off"
end)

local Slider1 = Tab1:NewSlider("distance limit", "", true, "/", {min = 0, max = 5000, default = 0}, function(value)
    print(value)
end)

local Toggle1 = Tab1:NewToggle("included AI", false, function(value)
    local vers = value and "on" or "off"
end)

local Toggle1 = Tab1:NewToggle("bounding Box", false, function(value)
    local vers = value and "on" or "off"
    -- settings
local settings = {
   defaultcolor = Color3.fromRGB(255,0,0),
   teamcheck = false,
   teamcolor = true
};

-- services
local runService = game:GetService("RunService");
local players = game:GetService("Players");

-- variables
local localPlayer = players.LocalPlayer;
local camera = workspace.CurrentCamera;

-- functions
local newVector2, newColor3, newDrawing = Vector2.new, Color3.new, Drawing.new;
local tan, rad = math.tan, math.rad;
local round = function(...) local a = {}; for i,v in next, table.pack(...) do a[i] = math.round(v); end return unpack(a); end;
local wtvp = function(...) local a, b = camera.WorldToViewportPoint(camera, ...) return newVector2(a.X, a.Y), b, a.Z end;

local espCache = {};
local function createEsp(player)
   local drawings = {};
   
   drawings.box = newDrawing("Square");
   drawings.box.Thickness = 1;
   drawings.box.Filled = false;
   drawings.box.Color = settings.defaultcolor;
   drawings.box.Visible = false;
   drawings.box.ZIndex = 2;

   drawings.boxoutline = newDrawing("Square");
   drawings.boxoutline.Thickness = 3;
   drawings.boxoutline.Filled = false;
   drawings.boxoutline.Color = newColor3();
   drawings.boxoutline.Visible = false;
   drawings.boxoutline.ZIndex = 1;

   espCache[player] = drawings;
end

local function removeEsp(player)
   if rawget(espCache, player) then
       for _, drawing in next, espCache[player] do
           drawing:Remove();
       end
       espCache[player] = nil;
   end
end

local function updateEsp(player, esp)
   local character = player and player.Character;
   if character then
       local cframe = character:GetModelCFrame();
       local position, visible, depth = wtvp(cframe.Position);
       esp.box.Visible = visible;
       esp.boxoutline.Visible = visible;

       if cframe and visible then
           local scaleFactor = 1 / (depth * tan(rad(camera.FieldOfView / 2)) * 2) * 1000;
           local width, height = round(4 * scaleFactor, 5 * scaleFactor);
           local x, y = round(position.X, position.Y);

           esp.box.Size = newVector2(width, height);
           esp.box.Position = newVector2(round(x - width / 2, y - height / 2));
           esp.box.Color = settings.teamcolor and player.TeamColor.Color or settings.defaultcolor;

           esp.boxoutline.Size = esp.box.Size;
           esp.boxoutline.Position = esp.box.Position;
       end
   else
       esp.box.Visible = false;
       esp.boxoutline.Visible = false;
   end
end

-- main
for _, player in next, players:GetPlayers() do
   if player ~= localPlayer then
       createEsp(player);
   end
end

players.PlayerAdded:Connect(function(player)
   createEsp(player);
end);

players.PlayerRemoving:Connect(function(player)
   removeEsp(player);
end)

runService:BindToRenderStep("esp", Enum.RenderPriority.Camera.Value, function()
   for player, drawings in next, espCache do
       if settings.teamcheck and player.Team == localPlayer.Team then
           continue;
       end

       if drawings and player ~= localPlayer then
           updateEsp(player, drawings);
       end
   end
end)
end)

local Toggle1 = Tab1:NewToggle("skeleton", false, function(value)
    local vers = value and "on" or "off"
    local Player = game:GetService("Players").LocalPlayer
local Mouse = Player:GetMouse()
local Camera = game:GetService("Workspace").CurrentCamera
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")
local Draw = Drawing.new

-- Function to create new drawing lines
local function CreateLine()
    local line = Draw("Line")
    line.Visible = false
    line.Color = Color3.fromRGB(255, 0, 0)
    line.Thickness = 1
    line.Transparency = 1
    return line
end

-- Function to initialize ESP for a player
local function CreatePlayerESP(plr)
    local limbs = {}
    repeat wait() until plr.Character and plr.Character:FindFirstChild("Humanoid")

    -- Ensure we continue if character is valid and humanoid exists
    if not plr.Character or not plr.Character:FindFirstChild("Humanoid") then return end
    
    -- Check if player uses R15 rig
    local isR15 = (plr.Character.Humanoid.RigType == Enum.HumanoidRigType.R15)

    -- Initialize limb lines based on rig type (R6 vs R15)
    if isR15 then
        limbs = {
            Head_UpperTorso = CreateLine(),
            UpperTorso_LowerTorso = CreateLine(),
            UpperTorso_LeftUpperArm = CreateLine(),
            LeftUpperArm_LeftLowerArm = CreateLine(),
            LeftLowerArm_LeftHand = CreateLine(),
            UpperTorso_RightUpperArm = CreateLine(),
            RightUpperArm_RightLowerArm = CreateLine(),
            RightLowerArm_RightHand = CreateLine(),
            LowerTorso_LeftUpperLeg = CreateLine(),
            LeftUpperLeg_LeftLowerLeg = CreateLine(),
            LeftLowerLeg_LeftFoot = CreateLine(),
            LowerTorso_RightUpperLeg = CreateLine(),
            RightUpperLeg_RightLowerLeg = CreateLine(),
            RightLowerLeg_RightFoot = CreateLine()
        }
    else
        limbs = {
            Head_Spine = CreateLine(),
            Spine = CreateLine(),
            LeftArm = CreateLine(),
            LeftArm_UpperTorso = CreateLine(),
            RightArm = CreateLine(),
            RightArm_UpperTorso = CreateLine(),
            LeftLeg = CreateLine(),
            LeftLeg_LowerTorso = CreateLine(),
            RightLeg = CreateLine(),
            RightLeg_LowerTorso = CreateLine()
        }
    end

    -- Function to update visibility for limb lines
    local function SetVisibility(state)
        for _, line in pairs(limbs) do
            line.Visible = state
        end
    end

    -- Main update function for R15
    local function UpdateR15()
        return RunService.RenderStepped:Connect(function()
            if plr.Character and plr.Character:FindFirstChild("Humanoid") and plr.Character.Humanoid.Health > 0 then
                local rootPos, inView = Camera:WorldToViewportPoint(plr.Character.HumanoidRootPart.Position)
                if inView then
                    local H = Camera:WorldToViewportPoint(plr.Character.Head.Position)
                    local UT = Camera:WorldToViewportPoint(plr.Character.UpperTorso.Position)
                    local LT = Camera:WorldToViewportPoint(plr.Character.LowerTorso.Position)
                    local LUA = Camera:WorldToViewportPoint(plr.Character.LeftUpperArm.Position)
                    local LLA = Camera:WorldToViewportPoint(plr.Character.LeftLowerArm.Position)
                    local LH = Camera:WorldToViewportPoint(plr.Character.LeftHand.Position)
                    local RUA = Camera:WorldToViewportPoint(plr.Character.RightUpperArm.Position)
                    local RLA = Camera:WorldToViewportPoint(plr.Character.RightLowerArm.Position)
                    local RH = Camera:WorldToViewportPoint(plr.Character.RightHand.Position)
                    local LUL = Camera:WorldToViewportPoint(plr.Character.LeftUpperLeg.Position)
                    local LLL = Camera:WorldToViewportPoint(plr.Character.LeftLowerLeg.Position)
                    local LF = Camera:WorldToViewportPoint(plr.Character.LeftFoot.Position)
                    local RUL = Camera:WorldToViewportPoint(plr.Character.RightUpperLeg.Position)
                    local RLL = Camera:WorldToViewportPoint(plr.Character.RightLowerLeg.Position)
                    local RF = Camera:WorldToViewportPoint(plr.Character.RightFoot.Position)

                    -- Update limb line positions
                    limbs.Head_UpperTorso.From = Vector2.new(H.X, H.Y)
                    limbs.Head_UpperTorso.To = Vector2.new(UT.X, UT.Y)

                    limbs.UpperTorso_LowerTorso.From = Vector2.new(UT.X, UT.Y)
                    limbs.UpperTorso_LowerTorso.To = Vector2.new(LT.X, LT.Y)

                    limbs.UpperTorso_LeftUpperArm.From = Vector2.new(UT.X, UT.Y)
                    limbs.UpperTorso_LeftUpperArm.To = Vector2.new(LUA.X, LUA.Y)
                    limbs.LeftUpperArm_LeftLowerArm.From = Vector2.new(LUA.X, LUA.Y)
                    limbs.LeftUpperArm_LeftLowerArm.To = Vector2.new(LLA.X, LLA.Y)
                    limbs.LeftLowerArm_LeftHand.From = Vector2.new(LLA.X, LLA.Y)
                    limbs.LeftLowerArm_LeftHand.To = Vector2.new(LH.X, LH.Y)

                    limbs.UpperTorso_RightUpperArm.From = Vector2.new(UT.X, UT.Y)
                    limbs.UpperTorso_RightUpperArm.To = Vector2.new(RUA.X, RUA.Y)
                    limbs.RightUpperArm_RightLowerArm.From = Vector2.new(RUA.X, RUA.Y)
                    limbs.RightUpperArm_RightLowerArm.To = Vector2.new(RLA.X, RLA.Y)
                    limbs.RightLowerArm_RightHand.From = Vector2.new(RLA.X, RLA.Y)
                    limbs.RightLowerArm_RightHand.To = Vector2.new(RH.X, RH.Y)

                    limbs.LowerTorso_LeftUpperLeg.From = Vector2.new(LT.X, LT.Y)
                    limbs.LowerTorso_LeftUpperLeg.To = Vector2.new(LUL.X, LUL.Y)
                    limbs.LeftUpperLeg_LeftLowerLeg.From = Vector2.new(LUL.X, LUL.Y)
                    limbs.LeftUpperLeg_LeftLowerLeg.To = Vector2.new(LLL.X, LLL.Y)
                    limbs.LeftLowerLeg_LeftFoot.From = Vector2.new(LLL.X, LLL.Y)
                    limbs.LeftLowerLeg_LeftFoot.To = Vector2.new(LF.X, LF.Y)

                    limbs.LowerTorso_RightUpperLeg.From = Vector2.new(LT.X, LT.Y)
                    limbs.LowerTorso_RightUpperLeg.To = Vector2.new(RUL.X, RUL.Y)
                    limbs.RightUpperLeg_RightLowerLeg.From = Vector2.new(RUL.X, RUL.Y)
                    limbs.RightUpperLeg_RightLowerLeg.To = Vector2.new(RLL.X, RLL.Y)
                    limbs.RightLowerLeg_RightFoot.From = Vector2.new(RLL.X, RLL.Y)
                    limbs.RightLowerLeg_RightFoot.To = Vector2.new(RF.X, RF.Y)

                    -- Show ESP if not already visible
                    if not limbs.Head_UpperTorso.Visible then
                        SetVisibility(true)
                    end
                else
                    -- Hide ESP when out of view
                    if limbs.Head_UpperTorso.Visible then
                        SetVisibility(false)
                    end
                end
            else
                -- Hide ESP when player dies
                if limbs.Head_UpperTorso.Visible then
                    SetVisibility(false)
                end
            end
        end)
    end

    -- Update function for R6 players
    local function UpdateR6()
        return RunService.RenderStepped:Connect(function()
            if plr.Character and plr.Character:FindFirstChild("Humanoid") and plr.Character.Humanoid.Health > 0 then
                local rootPos, inView = Camera:WorldToViewportPoint(plr.Character.HumanoidRootPart.Position)
                if inView then
                    local H = Camera:WorldToViewportPoint(plr.Character.Head.Position)
                    local UT = Camera:WorldToViewportPoint(plr.Character.Torso.Position)
                    local LT = Camera:WorldToViewportPoint(plr.Character.LowerTorso.Position)
                    local LUA = Camera:WorldToViewportPoint(plr.Character["Left Arm"].Position)
                    local LLA = Camera:WorldToViewportPoint(plr.Character["Left Arm"].Position)
                    local RUA = Camera:WorldToViewportPoint(plr.Character["Right Arm"].Position)

                    -- Update limb line positions
                    limbs.Head_Spine.From = Vector2.new(H.X, H.Y)
                    limbs.Head_Spine.To = Vector2.new(UT.X, UT.Y)

                    limbs.Spine.From = Vector2.new(UT.X, UT.Y)
                    limbs.Spine.To = Vector2.new(LT.X, LT.Y)

                    limbs.LeftArm.From = Vector2.new(LUA.X, LUA.Y)
                    limbs.LeftArm.To = Vector2.new(LLA.X, LLA.Y)

                    limbs.RightArm.From = Vector2.new(RUA.X, RUA.Y)
                    limbs.RightArm.To = Vector2.new(LLA.X, LLA.Y)

                    -- Show ESP if not visible
                    if not limbs.Head_Spine.Visible then
                        SetVisibility(true)
                    end
                else
                    -- Hide ESP if out of view
                    if limbs.Head_Spine.Visible then
                        SetVisibility(false)
                    end
                end
            end
        end)
    end

    -- Start updates based on rig type
    if isR15 then
        UpdateR15()
    else
        UpdateR6()
    end
end

-- Create ESP for existing players
for _, plr in pairs(Players:GetPlayers()) do
    if plr.Name ~= Player.Name then
        CreatePlayerESP(plr)
    end
end

-- Connect to PlayerAdded for new players
Players.PlayerAdded:Connect(function(plr)
    if plr.Name ~= Player.Name then
        CreatePlayerESP(plr)
    end
end)
end)

local Toggle1 = Tab1:NewToggle("distance esp", false, function(value)
    local vers = value and "on" or "off"
end)

local Toggle1 = Tab1:NewToggle("names", false, function(value)
    local vers = value and "on" or "off"
end)

local Toggle1 = Tab1:NewToggle("chams", false, function(value)
    local vers = value and "on" or "off"
end)

local Toggle1 = Tab1:NewToggle("health bar", false, function(value)
    local vers = value and "on" or "off"
end)

local Section1 = Tab1:NewSection("Special")

local Toggle1 = Tab1:NewToggle("zoom", false, function(value)
    local vers = value and "on" or "off"
end):AddKeybind(Enum.KeyCode.C)

local Slider1 = Tab1:NewSlider("zoom amount", "", true, "/", {min = 0, max = 5000, default = 0}, function(value)
    print(value)
end)

local Section1 = Tab1:NewSection("Special n°2")

local Toggle1 = Tab1:NewToggle("third person", false, function(value)
    local vers = value and "on" or "off"
end)

local Toggle1 = Tab1:NewToggle("ambient/fb", false, function(value)
    local vers = value and "on" or "off"
end)


















local FinishedLoading = Notif:Notify("Loaded zizihub.xyz", 4, "success")

-- // FUNCTION DOCS: 
--[[
    MAIN COMPONENT DOCS:

    -- // local library = loadstring(game:HttpGet(link: url))()
    -- // library.title = text: string
    -- // local Window = library:Init()

    -- [library.title contains rich text]

    -- / library:Remove()
    -- destroys the library

    -- / library:Text("new")
    -- sets the lbrary's text to something new

    - / library:UpdateKeybind(Enum.KeyCode.RightAlt)
    -- sets the lbrary's keybind to switch visibility to something new

    __________________________

    -- // local notificationLibrary = library:InitNotifications()
    -- // local Notification = notificationLibrary:Notify(text: string, time: number, type: string (information, notification, alert, error, success))

    -- [Notify contains rich text]

    -- / 3rd argument is a function, used like this:
    
    Notif:Notify("Function notification", 7, function()
        print("done")
    end)

    -- / Welcome:Text("new text")
    -- sets the notifications text to something differet [ADDS A +0.4 ONTO YOUR TIMER]

    __________________________

    -- // local Wm = library:Watermark(text: string)

    -- [Watermark contains rich text]

    -- / Wm:Hide()
    -- hides the watermark from eye view

    -- / Wm:Show()
    -- makes the watermark visible at the top of your screen

    -- / Wm:Text("new")
    -- sets the watermark's text to something new

    -- / Wm:Remove()
    -- destroys the watermark

    __________________________

    -- // local Tab1 = Init:NewTab(text: string)

    -- [tab title contains rich text]

    -- / Tab1:Open()
    -- opens the tab you want

    -- / Tab1:Remove()
    -- destroys the tab

    -- / Tab1:Hide()
    -- hides the tab from eye view

    -- / Tab1:Show()
    -- makes the tab visible on the selection table

    -- / Tab1:Text("new")
    -- sets the tab's text to something new

    __________________________

    -- [label contains rich text]

    -- / Label1:Text("new")
    -- sets the label's text to something new

    -- / Label1:Remove()
    -- destroys the label

    -- / Label1:Hide()
    -- hides the label from eye view

    -- / Label1:Show()
    -- makes the tab visible on the page that is used

    -- / Label1:Align("le")
    -- aligns the label to a new point in text X

    __________________________

    -- [Button contains rich text]

    -- / Button1:AddButton("text", function() end)
    -- adds a new button inside of the frame [CAN ONLY GO UP TO 4 BUTTONS AT A TIME]

    -- / Button1:Fire()
    -- executes the script within the button

    -- / Button1:Text("new")
    -- sets the button's text to something new

    -- / Button1:Hide()
    -- hides the button from eye view

    -- / Button1:Show()
    -- makes the button visible

    -- / Button1:Remove()
    -- destroys the button

    __________________________

    -- [Sections contain rich text]

    -- / Section1:Text("new")
    -- sets the section's text to something new

    -- / Section1:Hide()
    -- hides the section from eye view

    -- / Section1:Show()
    -- makes the section visible

    -- / Section1:Remove()
    -- destroys the section

    __________________________

    -- [Toggles contain rich text]

    -- / Toggle1:Text("new")
    -- sets the toggle's text to something new

    -- / Toggle1:Hide()
    -- hides the toggle from eye view

    -- / Toggle1:Show()
    -- makes the toggle visible

    -- / Toggle1:Remove()
    -- destroys the toggle

    -- / Toggle1:Change()
    -- changes the toggles state to the opposite

    -- / Toggle1:Set(true)
    -- sets the toggle to true even if it is true

    -- / Toggle1:AddKeybind(Enum.KeyCode.P, false, function() end) -- false / true is used for just changing the toggles state
    -- adds a keybind to the toggle

    -- / Toggle1:SetFunction(function() end)
    -- sets the toggles function

    __________________________

    -- [Keybinds contain rich text]

    -- / Keybind1:Text("new")
    -- sets the keybind's text to something new

    -- / Keybind1:Hide()
    -- hides the keybind from eye view

    -- / Keybind1:Show()
    -- makes the keybind visible

    -- / Keybind1:Remove()
    -- destroys the keybind

    -- / Keybind1:SetKey(Enum.KeyCode.P)
    -- sets the keybinds new key

    -- / Keybind1:Fire()
    -- fires the keybind function

    -- / Keybind1:SetFunction(function() end)
    -- sets the new keybind function

    __________________________

    -- [Textboxes contain rich text]

    -- / Textbox1:Input("new")
    -- sets the text box's input to something new

    -- / Textbox1:Place("new")
    -- sets the text box's placeholder to something new

    -- / Textbox1:Fire()
    -- fires the textbox function

    -- / Textbox1:SetFunction(function() end)
    -- sets the text boxes new function

    -- / Textbox1:Text("new")
    -- sets the textbox's text to something new

    -- / Textbox1:Hide()
    -- hides the textbox from eye view

    -- / Textbox1:Show()
    -- makes the textbox visible

    -- / Textbox1:Remove()
    -- destroys the textbox

    __________________________

    -- [Selectors contain rich text]

    -- / Selector1:SetFunction(function() end)
    -- sets the selector new function

    -- / Selector1:Text("new")
    -- sets the selector's text to something new

    -- / Selector1:Hide()
    -- hides the selector from eye view

    -- / Selector1:Show()
    -- makes the selector visible

    -- / Selector1:Remove()
    -- destroys the selector

    __________________________

    -- [Sliders contain rich text]

    -- / Slider1:Value(1)
    -- sets the slider new value

    -- / Slider1:SetFunction(function() end)
    -- sets the slider new function

    -- / Slider1:Text("new")
    -- sets the slider's text to something new

    -- / Slider1:Hide()
    -- hides the slider from eye view

    -- / Slider1:Show()
    -- makes the slider visible

    -- / Slider1:Remove()
    -- destroys the slider

    ---------------------------------------------------------------------------------------------------------

    MISC SEMI USELESS DOCS:

    -- / library.rank = ""
    -- returns the rank you choose (default = "private")

    -- / library.fps
    -- returns FPS you're getting in game

    -- / library.version
    -- returns the version of the library

    -- / library.title = ""
    -- returns the title of the library

    -- / library:GetDay("word") -- word, short, month, year
    -- returns the os day

    -- / library:GetTime("24h") -- 24h, 12h, minute, half, second, full, ISO, zone
    -- returns the os time

    -- / library:GetMonth("word") -- word, short, digit
    -- returns the os month

    -- / library:GetWeek("year_S") -- year_S, day, year_M
    -- returns the os week

    -- / library:GetYear("digits") -- digits, full
    -- returns the os year

    -- / library:GetUsername()
    -- returns the localplayers username

    -- / library:GetUserId()
    -- returns the localplayers userid

    -- / library:GetPlaceId()
    -- returns the games place id

    -- / library:GetJobId()
    -- returns the games job id

    -- / library:CheckIfLoaded()
    -- returns true if you're fully loaded

    -- / library:Rejoin()
    -- rejoins the same server as you was in

    -- / library:Copy("stuff")
    -- copies the inputed string

    -- / library:UnlockFps(500) -- only works with synapse
    -- sets the max fps to something you choose
    
    -- / library:PromptDiscord("invite")
    -- invites you to a discord
]]
