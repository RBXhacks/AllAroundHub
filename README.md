local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()


local Window = Rayfield:CreateWindow({
	Name = "Victor_Heimdal Hub",
	Icon = 0, -- Icon in Topbar. Can use Lucide Icons (string) or Roblox Image (number). 0 to use no icon (default).
	LoadingTitle = "Rayfield",
	LoadingSubtitle = "Credit: Sirius",
	Theme = "AmberGlow", -- Check https://docs.sirius.menu/rayfield/configuration/themes

	DisableRayfieldPrompts = false,
	DisableBuildWarnings = false, -- Prevents Rayfield from warning when the script has a version mismatch with the interface

	ConfigurationSaving = {
		Enabled = true,
		FolderName = nil, -- Create a custom folder for your hub/game
		FileName = "Big Hub"
	},

	Discord = {
		Enabled = false, -- Prompt the user to join your Discord server if their executor supports it
		Invite = "noinvitelink", -- The Discord invite code, do not include discord.gg/. E.g. discord.gg/ ABCD would be ABCD
		RememberJoins = true -- Set this to false to make them join the discord every time they load it up
	},

	KeySystem = true, -- Set this to true to use our key system
	KeySettings = {
		Title = "This legendary script needs key",
		Subtitle = "GIMME KEYYYY",
		Note = "Ask the owner nicely for the key ", -- Use this to tell the user how to get a key
		FileName = "Key", -- It is recommended to use something unique as other scripts using Rayfield may overwrite your key file
		SaveKey = true, -- The user's key will be saved, but if you change the key, they will be unable to use your script
		GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
		Key = {"ezE","Victor_Heimdal-IsKing","WsbErBøsse"} -- List of keys that will be accepted by the system, can be RAW file links (pastebin, github etc) or simple strings ("hello","key22")
	}
})

local char = game.Players.LocalPlayer.Character
local hum = char.Humanoid

local Tab = Window:CreateTab("Main", 4483362458) -- Title, Image
local Tab1 = Window:CreateTab("Misc", 4483362458) -- Title, Image

local Slider = Tab:CreateSlider({
	Name = "JumpPower",
	Range = {0, 500},
	Increment = 10,
	Suffix = "JumpPower",
	CurrentValue = 10,
	Flag = "Slider1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
	Callback = function(Value)
		if Value then
			hum.JumpPower = Value
		end
	end
})

local Slider1 = Tab:CreateSlider({
	Name = "WalkSpeed",
	Range = {0, 500},
	Increment = 10,
	Suffix = "WalkSpeed",
	CurrentValue = 10,
	Flag = "Slider2", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
	Callback = function(Value)
		if Value then
			hum.WalkSpeed = Value
		end
	end
})

local Toggle = Tab1:CreateToggle({
   Name = "NoClip",
   CurrentValue = false,
   Flag = "Toggle1215", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
      if Value == true then
        game.RunService.Stepped:Connect(function()
            game.Players.LocalPlayer.Character.Head.CanCollide = false 
            game.Players.LocalPlayer.Character.Torso.CanCollide = false
        end)
            else
            game.RunService.Stepped:Connect(function()
            game.Players.LocalPlayer.Character.Head.CanCollide = true 
            game.Players.LocalPlayer.Character.Torso.CanCollide = true
        end)
   end
})

local Button = Tab:CreateButton({
	Name = "Force Revome hacks",
	Callback = function()
		Rayfield:Destroy()
	end
})

local Input = Tab1:CreateInput({
	Name = "Chat",
	CurrentValue = "",
	PlaceholderText = "Put text here",
	RemoveTextAfterFocusLost = false,
	Flag = "Input231",
	Callback = function(Text)
		local TextChatService = game:GetService("TextChatService")
		TextChatService.TextChannels.RBXGeneral:SendAsync(Text)
	end 
})
local Input2 = Tab1:CreateInput({
	Name = "Kick Player",
	CurrentValue = "",
	PlaceholderText = "Put text here",
	RemoveTextAfterFocusLost = false,
	Flag = "Input231",
	Callback = function(Text)
		game.Players:WaitForChild(Text):Kick("Your a nigger frfr")
	end 
})

local Dropdown = Tab:CreateDropdown({
   Name = "Health function",
   Options = {"Faster Regen","Normal Regen","Risky Regen"},
   CurrentOption = {"Normal Regen"},
   MultipleOptions = false,
   Flag = "yoDropdown1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Options)
		if Options == "Faster Regen" then
			hum.HealthChanged:Connect(function(health)
                if health < hum.MaxHealth then     
                   while wait(.3) do
                    hum.Health += 5
                    end
                end
            end)
			elseif Options == "Risky Regen" then
				hum.HealthChanged:Connect(function(health)
                if health < hum.MaxHealth then
                    hum.Health += hum.MaxHealth
                end
            end)
			elseif Options == "Normal Regen" then
				hum.HealthChanged:Connect(function(health)
                if health < hum.MaxHealth then
                    while wait(1) do
                    hum.Health += 5
                    end
                end
            end)
		end
   end
})


Rayfield:LoadConfiguration()
