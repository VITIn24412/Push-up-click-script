-- Load the Orion library
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()

-- Create the main window
local Window = OrionLib:MakeWindow({
    Name = "Push-Up Training Simulator Hub",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "PushUpTrainingSimulatorHub"
})

-- Function to auto-click
local function AutoClick()
    while _G.AutoClickEnabled do
        game:GetService("ReplicatedStorage").Packages._Index:FindFirstChild("sleitnick_knit@1.5.1").knit.Services.TrainService.RE.Train:FireServer()
        wait(0.1) -- Adjust the click speed as needed
    end
end

-- Function to auto-rebirth
local function AutoRebirth()
    while _G.AutoRebirthEnabled do
        game:GetService("ReplicatedStorage").Packages._Index:FindFirstChild("sleitnick_knit@1.5.1").knit.Services.RebirthService.RF.Rebirth:InvokeServer()
        wait(1) -- Adjust the rebirth speed as needed
    end
end

-- Function to auto-equip best pets
local function AutoEquipBestPets()
    while _G.AutoEquipBestPetsEnabled do
        game:GetService("ReplicatedStorage").Packages._Index:FindFirstChild("sleitnick_knit@1.5.1").knit.Services.PetService.RE.EquipBestPets:FireServer()
        wait(10) -- Adjust the equip speed as needed
    end
end

-- Function to auto-spin
local function AutoSpin()
    while _G.AutoSpinEnabled do
        game:GetService("ReplicatedStorage").Packages._Index:FindFirstChild("sleitnick_knit@1.5.1").knit.Services.SpinningWheelService.RF.StartSpin:InvokeServer()
        wait(1) -- Adjust the spin speed as needed
    end
end

-- Function to auto-open egg
local function AutoOpenEgg(eggName)
    while _G.AutoOpenEggEnabled do
        local args = { [1] = eggName, [2] = 1 }
        game:GetService("ReplicatedStorage").Packages._Index:FindFirstChild("sleitnick_knit@1.5.1").knit.Services.EggHatchService.RE.Hatch:FireServer(unpack(args))
        wait(1) -- Adjust the egg open speed as needed
    end
end

-- GUI setup
local AutoFarmTab = Window:MakeTab({
    Name = "Auto Farm",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

AutoFarmTab:AddToggle({
    Name = "Enable Auto Click",
    Default = false,
    Callback = function(Value)
        _G.AutoClickEnabled = Value
        if Value then
            spawn(AutoClick)
        end
    end
})

local AutoRebirthTab = Window:MakeTab({
    Name = "Auto Rebirth",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

AutoRebirthTab:AddToggle({
    Name = "Enable Auto Rebirth",
    Default = false,
    Callback = function(Value)
        _G.AutoRebirthEnabled = Value
        if Value then
            spawn(AutoRebirth)
        end
    end
})

local AutoEggTab = Window:MakeTab({
    Name = "Auto Egg",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local EggList = {
    "Bee Egg",
    "Fruit Egg",
    "Angel Egg",
    "Reaper Egg",
    "Crab Egg",
    "Raven Egg"
}

local selectedEgg = EggList[1]

AutoEggTab:AddDropdown({
    Name = "Select Egg",
    Default = EggList[1],
    Options = EggList,
    Callback = function(Value)
        selectedEgg = Value
    end
})

AutoEggTab:AddToggle({
    Name = "Auto Open Egg",
    Default = false,
    Callback = function(Value)
        _G.AutoOpenEggEnabled = Value
        if Value then
            local eggMappings = {
                ["Bee Egg"] = "Egg_1_1",
                ["Fruit Egg"] = "Egg_1_2",
                ["Angel Egg"] = "Egg_1_3",
                ["Reaper Egg"] = "Egg_1_4",
                ["Crab Egg"] = "Egg_1_5",
                ["Raven Egg"] = "Egg_1_6"
            }
            spawn(function() AutoOpenEgg(eggMappings[selectedEgg]) end)
        end
    end
})

AutoEggTab:AddToggle({
    Name = "Auto Equip Best Pets",
    Default = false,
    Callback = function(Value)
        _G.AutoEquipBestPetsEnabled = Value
        if Value then
            spawn(AutoEquipBestPets)
        end
    end
})

local AutoSpinTab = Window:MakeTab({
    Name = "Auto Spin",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

AutoSpinTab:AddToggle({
    Name = "Enable Auto Spin",
    Default = false,
    Callback = function(Value)
        _G.AutoSpinEnabled = Value
        if Value then
            spawn(AutoSpin)
        end
    end
})
