
-- =========================================
-- VOLT HUB - CONFIG SAVE / LOAD SYSTEM
-- =========================================

local HttpService = game:GetService("HttpService")

local FOLDER_NAME = "Volt Hub"
local FILE_NAME = FOLDER_NAME .. "/config.json"

-- CONFIG PADRÃO (todas as configurações salváveis)
local Config = {
    -- Farming
    AutoFarm = false,
    AutoKatakuri = false,
    AutoBone = false,
    FarmMode = "Farm Level",
    
    -- Settings Farming
    WeaponType = "Melee",
    BringMob = true,
    AutoClick = false,
    AutoV3 = false,
    AutoV4 = false,
    BringModeDistance = 350,
    
    -- Stats
    AutoStatus = false,
    StatusSelected = "Melee",
    StatusPoints = 1,
    
    -- Chest Farm
    AutoChest = false,
    HopChest = false,
    ChestLimit = 10,
    
    -- Islands
    SelectedIsland = nil,
    TweenSpeed = 300,
    
    -- Team
    SelectedTeam = "Pirata"
}

-- =========================================
-- CRIAR PASTA SE NÃO EXISTIR
-- =========================================
if not isfolder(FOLDER_NAME) then
    makefolder(FOLDER_NAME)
end

-- =========================================
-- SAVE CONFIG
-- =========================================
local function SaveConfig()
    local success, err = pcall(function()
        writefile(FILE_NAME, HttpService:JSONEncode(Config))
    end)

    if success then
        Fl:Notify({
            Title = "Config System",
            Content = "Configurações salvas!",
            Duration = 3
        })
    else
        warn("[Volt Hub] Erro ao salvar config:", err)
    end
end

-- =========================================
-- LOAD CONFIG
-- =========================================
local function LoadConfig()
    if not isfile(FILE_NAME) then
        SaveConfig()
        return
    end

    local success, data = pcall(function()
        return HttpService:JSONDecode(readfile(FILE_NAME))
    end)

    if success and type(data) == "table" then
        for k, v in pairs(data) do
            Config[k] = v
        end
        
        -- Aplicar configurações carregadas às variáveis globais
        getgenv().AF = Config.AutoFarm
        getgenv().AK = Config.AutoKatakuri
        getgenv().AB = Config.AutoBone
        getgenv().FarmMode = Config.FarmMode
        getgenv().WP = Config.WeaponType
        getgenv().BM = Config.BringMob
        getgenv().AC = Config.AutoClick
        getgenv().AV3 = Config.AutoV3
        getgenv().GRaceClickAutov4 = Config.AutoV4
        getgenv().BringMode = Config.BringModeDistance
        getgenv().AS = Config.AutoStatus
        getgenv().SA = Config.StatusSelected
        getgenv().SP = Config.StatusPoints
        getgenv().AutoChest = Config.AutoChest
        getgenv().HopChest = Config.HopChest
        getgenv().ChestLimit = Config.ChestLimit
        getgenv().SelectedIsland = Config.SelectedIsland
        getgenv().TweenSpeed = Config.TweenSpeed
        getgenv().SelectedTeam = Config.SelectedTeam
        
        Fl:Notify({
            Title = "Config System",
            Content = "Configurações carregadas!",
            Duration = 3
        })
    else
        warn("[Volt Hub] Config inválida, recriando...")
        SaveConfig()
    end
end

-- =========================================
-- ATUALIZAR FUNÇÕES EXISTENTES
-- =========================================

-- Modificar o TG_MAIN para salvar automaticamente
local TG_MAIN_Original = TG_MAIN.OnChanged
TG_MAIN:OnChanged(function(v)
    TG_MAIN_Original(v)
    Config.AutoFarm = getgenv().AF
    Config.AutoKatakuri = getgenv().AK
    Config.AutoBone = getgenv().AB
    SaveConfig()
end)

-- Modificar WeaponType Dropdown
TabSF:AddDropdown("Weap",{Title="Select Weapon",Values={"Melee","Sword"},Default=1}):OnChanged(function(v)
    getgenv().WP=v
    Config.WeaponType = v
    SaveConfig()
end)

-- Modificar BringMob Toggle
TabSF:AddToggle("BM",{Title="Bring Mob",Default=Config.BringMob}):OnChanged(function(v)
    getgenv().BM=v
    Config.BringMob = v
    SaveConfig()
end)

-- Modificar AutoClick Toggle
TabSF:AddToggle("AC",{Title="Auto Click",Default=Config.AutoClick}):OnChanged(function(v)
    getgenv().AC=v
    Config.AutoClick = v
    SaveConfig()
end)

-- Modificar AutoV3 Toggle
TabSF:AddToggle("AV3",{Title="Auto Turn on v3",Default=Config.AutoV3}):OnChanged(function(v)
    getgenv().AV3=v
    Config.AutoV3 = v
    SaveConfig()
end)

-- Modificar AutoV4 Toggle
TabSF:AddToggle("AV4",{Title="Auto Turn on v4",Default=Config.AutoV4}):OnChanged(function(v)
    getgenv().GRaceClickAutov4=v
    Config.AutoV4 = v
    SaveConfig()
end)

-- Modificar FarmMode Dropdown
TabF:AddDropdown("FarmSel",{Title="Select Farming",Values={"Farm Level","Farm Katakuri","Farm Bone"},Default=1}):OnChanged(function(v)
    getgenv().FarmMode=v
    Config.FarmMode = v
    SaveConfig()
end)

-- Modificar Status Dropdown
TabSt:AddDropdown("Stat",{Title="Selecionar Status",Values={"Melee","Defense","Sword","Gun","Blox Fruit"},Default=1}):OnChanged(function(v)
    getgenv().SA=({Melee="Melee",Defense="Defense",Sword="Sword",Gun="Gun",["Blox Fruit"]="Fruit"})[v]
    Config.StatusSelected = getgenv().SA
    SaveConfig()
end)

-- Modificar Status Points Slider
TabSt:AddSlider("Pts",{Title="Select Points",Default=Config.StatusPoints,Min=1,Max=100,Rounding=0}):OnChanged(function(v)
    getgenv().SP=v
    Config.StatusPoints = v
    SaveConfig()
end)

-- Modificar AutoStatus Toggle
TabSt:AddToggle("AS",{Title="Auto Status",Default=Config.AutoStatus}):OnChanged(function(v)
    getgenv().AS=v
    Config.AutoStatus = v
    SaveConfig()
end)

-- =========================================
-- ADICIONAR NA SEÇÃO DE CHEST FARM
-- =========================================

-- Modificar ChestInput
local ChestInput = TabEF:AddInput("ChestValue", {
    Title = "Select Value Chest",
    Default = tostring(Config.ChestLimit),
    Placeholder = "Digite o número de baús",
    Numeric = true,
    Callback = function(value)
        local num = tonumber(value)
        if num and num > 0 then
            getgenv().ChestLimit = math.floor(num)
            Config.ChestLimit = getgenv().ChestLimit
            SaveConfig()
        end
    end
})

-- Modificar TG_AutoChest
TG_AutoChest:OnChanged(function(v)
    getgenv().AutoChest = v
    Config.AutoChest = v
    SaveConfig()
    
    if v then
        getgenv().ChestCollected = 0
        getgenv().IgnoredChests = {}
    else
        SAT()
        RNP()
    end
end)

-- Modificar TG_HopChest
TG_HopChest:OnChanged(function(v)
    getgenv().HopChest = v
    Config.HopChest = v
    SaveConfig()
end)

-- =========================================
-- ADICIONAR NA SEÇÃO DE ISLANDS
-- =========================================

-- Modificar IslandDropdown
IslandDropdown:OnChanged(function(v)
    getgenv().SelectedIsland = v
    Config.SelectedIsland = v
    SaveConfig()
end)

-- Modificar VelocitySlider
VelocitySlider:OnChanged(function(value)
    local roundedValue = math.floor(value / 10 + 0.5) * 10
    roundedValue = math.max(50, math.min(350, roundedValue))
    
    getgenv().TweenSpeed = roundedValue
    Config.TweenSpeed = roundedValue
    SaveConfig()
    
    if roundedValue ~= value then
        VelocitySlider:SetValue(roundedValue)
    end
end)

-- =========================================
-- ADICIONAR NA SEÇÃO DE TEAM
-- =========================================

-- Modificar TeamDropdown
TeamDropdown:OnChanged(function(v)
    getgenv().SelectedTeam = v
    Config.SelectedTeam = v
    SaveConfig()
end)

-- =========================================
-- ADICIONAR BOTÕES DE CONFIG NO TAB SETTINGS
-- =========================================

TabSe:AddSection("Config System")

TabSe:AddButton({
    Title = "Save Config",
    Description = "Salvar todas as configurações",
    Callback = function()
        SaveConfig()
    end
})

TabSe:AddButton({
    Title = "Load Config",
    Description = "Carregar configurações salvas",
    Callback = function()
        LoadConfig()
    end
})

TabSe:AddButton({
    Title = "Reset Config",
    Description = "Restaurar configurações padrão",
    Callback = function()
        if isfile(FILE_NAME) then
            delfile(FILE_NAME)
        end
        
        -- Resetar para valores padrão
        Config = {
            AutoFarm = false,
            AutoKatakuri = false,
            AutoBone = false,
            FarmMode = "Farm Level",
            WeaponType = "Melee",
            BringMob = true,
            AutoClick = false,
            AutoV3 = false,
            AutoV4 = false,
            BringModeDistance = 350,
            AutoStatus = false,
            StatusSelected = "Melee",
            StatusPoints = 1,
            AutoChest = false,
            HopChest = false,
            ChestLimit = 10,
            SelectedIsland = nil,
            TweenSpeed = 300,
            SelectedTeam = "Pirata"
        }
        
        SaveConfig()
        
        Fl:Notify({
            Title = "Config System",
            Content = "Config resetada com sucesso!",
            Duration = 3
        })
    end
})

-- =========================================
-- INIT - CARREGAR CONFIG AO INICIAR
-- =========================================
task.spawn(function()
    task.wait(1) -- Aguardar UI carregar
    LoadConfig()
end)
-- CONFIG
local PIRATE,MARINE=true,false
local RS,PS,WS,TS,VU,LT,RSvc=game:GetService("ReplicatedStorage"),game:GetService("Players"),game:GetService("Workspace"),game:GetService("TweenService"),game:GetService("VirtualUser"),game:GetService("Lighting"),game:GetService("RunService")
local LP=PS.LocalPlayer;repeat task.wait()until RS:FindFirstChild("Remotes")and RS.Remotes:FindFirstChild("CommF_")
if not LP.Team then task.wait(3);RS.Remotes.CommF_:InvokeServer("SetTeam",PIRATE and"Pirates"or"Marines")end
wait(1);repeat task.wait()until LP.Character and LP.Character:FindFirstChild("HumanoidRootPart");task.wait(2)
local Remotes,CF,QuestIlha=RS:WaitForChild("Remotes",5),RS.Remotes:FindFirstChild("CommF_"),getgenv().QuestIlha
getgenv().AF,getgenv().AK,getgenv().AB,getgenv().AS,getgenv().SA,getgenv().SP,getgenv().WP,getgenv().BM,getgenv().BringMode,getgenv().AC=false,false,false,false,"Melee",1,"Melee",true,350,false
getgenv().CurrentQuestName,getgenv().CurrentQuestLevel,getgenv().KataIndex,getgenv().BoneIndex,getgenv().AV3,getgenv().GRaceClickAutov4,getgenv().FarmMode,getgenv().LastQuestAttempt,getgenv().GSelectWeapon,getgenv().TweenCompleted=nil,nil,1,1,false,false,"Farm Level",0,nil,false
LP.Idled:Connect(function()VU:CaptureController();VU:ClickButton2(Vector2.new())end)
hookfunction(require(RS.Effect.Container.Death),function()end);hookfunction(require(RS.Effect.Container.Respawn),function()end)
World1,World2,World3=game.PlaceId==2753915549 or game.PlaceId==85211729168715,game.PlaceId==4442272183 or game.PlaceId==79091703265657,game.PlaceId==7449423635 or game.PlaceId==100117331123089
function GetSea()return World1 and 1 or World2 and 2 or World3 and 3 or 1 end
local function GL()local ok,v=pcall(function()return LP.Data.Level.Value end)return ok and v or 1 end
local function GQ()if not QuestIlha or not QuestIlha.GetQuestForLevel then return nil end;local q=QuestIlha.GetQuestForLevel(GL());if not q then return nil end;local qSea,pSea=q.Sea or 1,GetSea();if qSea>pSea then return QuestIlha.GetLastQuestForSea and QuestIlha.GetLastQuestForSea(pSea)or q end;return q end
local function HQ()local ok,r=pcall(function()return LP.PlayerGui.Main.Quest.Visible end)return ok and r end
local function CQ()if CF and HQ()then pcall(function()CF:InvokeServer("AbandonQuest")task.wait(0.3)end)end end
local function IFA()return getgenv().AF or getgenv().AK or getgenv().AB end
local function DAC(char)if not char then return end;for _,p in pairs(char:GetDescendants())do if p:IsA("BasePart")then p.CanCollide=false end end end
local function RNP()local c=LP.Character;if not c then return end;local hrp,hum=c:FindFirstChild("HumanoidRootPart"),c:FindFirstChild("Humanoid");if hrp and hum then DAC(c);hrp.Anchored=false;hrp.AssemblyLinearVelocity=Vector3.new();hum:ChangeState(11);task.wait(0.1);hum:ChangeState(8)end end
local function IMN(obj)if isnetworkowner then return isnetworkowner(obj)end;local c=LP.Character;return c and c:FindFirstChild("HumanoidRootPart")and(obj.Position-c.HumanoidRootPart.Position).Magnitude<=getgenv().BringMode end
local CBP=nil
local function BM(mn,tcf)if not getgenv().BM or not getgenv().TweenCompleted then return end;local c=LP.Character;if not c or not c:FindFirstChild("HumanoidRootPart")then return end;local hrp,t=c.HumanoidRootPart,tcf or CBP or hrp.CFrame*CFrame.new(0,-20,0);for _,m in pairs(WS.Enemies:GetChildren())do if m.Name==mn and m:FindFirstChild("Humanoid")and m:FindFirstChild("HumanoidRootPart")and m.Humanoid.Health>0 and(m.HumanoidRootPart.Position-hrp.Position).Magnitude<=getgenv().BringMode and IMN(m.HumanoidRootPart)then m.HumanoidRootPart.CFrame=t;m.HumanoidRootPart.CanCollide=false;m.HumanoidRootPart.Size=Vector3.new(50,50,50);if m:FindFirstChild("Head")then m.Head.CanCollide=false end;m.Humanoid.WalkSpeed=0;m.Humanoid.JumpPower=0;m.Humanoid:ChangeState(14);m.Humanoid:ChangeState(11);if m.Humanoid:FindFirstChild("Animator")then m.Humanoid.Animator:Destroy()end end end;if sethiddenproperty then sethiddenproperty(LP,"SimulationRadius",math.huge)end end
function EquipWeapon(toolName)local character,backpack=LP.Character or LP.CharacterAdded:Wait(),LP.Backpack;for _,tool in pairs(backpack:GetChildren())do if tool:IsA("Tool")and tool.Name==toolName then tool.Parent=character;getgenv().GSelectWeapon=toolName;return end end;for _,tool in pairs(character:GetChildren())do if tool:IsA("Tool")and tool.Name==toolName then getgenv().GSelectWeapon=toolName;return end end end
local function EQ()if not IFA()then return end;local tt=getgenv().WP=="Sword"and"Sword"or"Melee";for _,v in ipairs(LP.Backpack:GetChildren())do if v:IsA("Tool")and v.ToolTip==tt then EquipWeapon(v.Name)return end end end
local function FMS(n)for _,m in ipairs(WS.Enemies:GetChildren())do if m.Name==n and m:FindFirstChild("Humanoid")and m:FindFirstChild("HumanoidRootPart")and m.Humanoid.Health>0 then return m end end end
local function FAM(list)for _,n in ipairs(list)do local m=FMS(n);if m then return m,n end end end
local function GF()local ok,v=pcall(function()return LP.Data.Fragments.Value end)return ok and v or 0 end
local function RR()if GF()<3000 or not CF then return false end;return pcall(function()CF:InvokeServer("BlackbeardReward","Reroll","2")end)end
local function FP()LT.GlobalShadows=false;LT.FogEnd=9e9;LT.Brightness=0;LT.OutdoorAmbient=Color3.new(0,0,0);settings().Rendering.QualityLevel=Enum.QualityLevel.Level01;for _,v in pairs(LT:GetChildren())do if v:IsA("Sky")or v:IsA("BloomEffect")or v:IsA("SunRaysEffect")or v:IsA("ColorCorrectionEffect")or v:IsA("BlurEffect")or v:IsA("DepthOfFieldEffect")then v:Destroy()end end;for _,v in pairs(WS:GetDescendants())do if v:IsA("BasePart")or v:IsA("UnionOperation")or v:IsA("MeshPart")then v.Material=Enum.Material.Plastic;v.Reflectance=0;v.CastShadow=false;if v:IsA("MeshPart")then v.TextureID=""end elseif v:IsA("Decal")or v:IsA("Texture")or v:IsA("ParticleEmitter")or v:IsA("Trail")or v:IsA("Beam")or v:IsA("Fire")or v:IsA("SpotLight")or v:IsA("Smoke")or v:IsA("Sparkles")or v:IsA("PointLight")or v:IsA("SurfaceLight")then v:Destroy()elseif v:IsA("SpecialMesh")then v.TextureId=""end end;for _,char in pairs(WS:GetChildren())do if char:IsA("Model")and char~=LP.Character then for _,p in pairs(char:GetDescendants())do if p:IsA("BasePart")or p:IsA("MeshPart")then p.Material=Enum.Material.Plastic;if p:IsA("MeshPart")then p.TextureID=""end elseif p:IsA("Accessory")or p:IsA("Hat")or p:IsA("Shirt")or p:IsA("Pants")or p:IsA("ShirtGraphic")or p:IsA("Decal")or p:IsA("Texture")then p:Destroy()end end end end;pcall(function()LP.PlayerGui.Notifications:Destroy()end);pcall(function()for _,gui in pairs(LP.PlayerGui:GetChildren())do if gui.Name=="Notification"or gui.Name=="PopupNotification"then gui:Destroy()end end end)end
local function US(t,k)local VIM=game:GetService("VirtualInputManager");VIM:SendKeyEvent(true,k,false,game);task.wait(0.05);VIM:SendKeyEvent(false,k,false,game)end
local Stepped=RSvc.Stepped;local AT,FC,GT,HC=nil,nil,nil,nil
local function SF()if FC then FC:Disconnect();FC=nil end;CBP=nil end
local function SH()if HC then HC:Disconnect();HC=nil end end
local function SAT()if AT then AT:Cancel();AT=nil end;SF();SH();if GT then GT:Cancel();GT=nil end;getgenv().TweenCompleted=false end
local function TF25(hrp,tHRP,spd)if not hrp or not tHRP then return end;spd=spd or 300;if AT then AT:Cancel();AT=nil end;SF();getgenv().TweenCompleted=false;local c=LP.Character;if c and IFA()then DAC(c)end;local tCF,dist=tHRP.CFrame*CFrame.new(0,25,0),(hrp.Position-tHRP.Position).Magnitude;AT=TS:Create(hrp,TweenInfo.new(math.max(dist/spd,0.05),Enum.EasingStyle.Linear),{CFrame=tCF});AT:Play();AT.Completed:Once(function()getgenv().TweenCompleted=true;FC=Stepped:Connect(function()if not tHRP or not tHRP.Parent or not IFA()then SF();return end;local c=LP.Character;if not c then SF();return end;local cHRP=c:FindFirstChild("HumanoidRootPart");if not cHRP then SF();return end;DAC(c);local nCF=tHRP.CFrame*CFrame.new(0,25,0);cHRP.AssemblyLinearVelocity=Vector3.zero;cHRP.CFrame=nCF;CBP=nCF*CFrame.new(0,-25,0)end)end)end
local function TTG(hrp,tCF,spd)if not hrp then return end;spd=spd or 250;SF();SH();if GT then GT:Cancel();GT=nil end;if AT then AT:Cancel();AT=nil end;getgenv().TweenCompleted=false;local c=LP.Character;if c and IFA()then DAC(c)end;local dist,dur=(hrp.Position-tCF.Position).Magnitude,math.max((hrp.Position-tCF.Position).Magnitude/spd,0.1);GT=TS:Create(hrp,TweenInfo.new(dur,Enum.EasingStyle.Linear),{CFrame=tCF});GT:Play();HC=RSvc.Heartbeat:Connect(function()if not hrp or not hrp.Parent then SH();return end;local c=LP.Character;if c and IFA()then DAC(c)end;hrp.Velocity=Vector3.new(0,0,0)end);GT.Completed:Wait();SH();GT=nil;getgenv().TweenCompleted=true end
local KM,BonM={"Cookie Crafter","Cake Guard","Baking Staff","Head Baker","Cocoa Warrior"},{"Reborn Skeleton","Living Zombie","Demonic Soul","Posessed Mummy","Peanut Scout"}
local KS,BS=CFrame.new(-2091,70,-12373),CFrame.new(-9506,172,6057)
local Fl=loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local Win=Fl:CreateWindow({Title="Volt Hub V3",SubTitle="Blox Fruits Delta",TabWidth=160,Size=UDim2.fromOffset(580,460),Acrylic=false,Theme="Dark"})
local TabM,TabSe,TabS,TabLP,TabSF,TabF,TabSt=Win:AddTab({Title="Tab Main",Icon="home"}),Win:AddTab({Title="Tab Settings",Icon="settings"}),Win:AddTab({Title="Tab Shop",Icon="shopping-bag"}),Win:AddTab({Title="LocalPlayer",Icon="user"}),Win:AddTab({Title="Tab Settings Farming",Icon="clock"}),Win:AddTab({Title="Tab Farming",Icon="sword"}),Win:AddTab({Title="Tab Status & ESP",Icon="eye"})
TabM:AddButton({Title="Discord",Description="Volt Comunnity",Callback=function()setclipboard("https://discord.gg/29BDQqHYbJ")end})
TabS:AddSection("Shop");TabS:AddButton({Title="Buy Buso",Callback=function()if CF then CF:InvokeServer("BuyHaki","Buso")end end});TabS:AddButton({Title="Rerrol Race",Callback=RR})
TabSF:AddSection("Settings Farming");TabSF:AddDropdown("Weap",{Title="Select Weapon",Values={"Melee","Sword"},Default=1}):OnChanged(function(v)getgenv().WP=v end);TabSF:AddToggle("BM",{Title="Bring Mob",Default=true}):OnChanged(function(v)getgenv().BM=v end);TabSF:AddToggle("AC",{Title="Auto Click",Default=false}):OnChanged(function(v)getgenv().AC=v end);TabSF:AddToggle("AV3",{Title="Auto Turn on v3",Default=false}):OnChanged(function(v)getgenv().AV3=v end);TabSF:AddToggle("AV4",{Title="Auto Turn on v4",Default=false}):OnChanged(function(v)getgenv().GRaceClickAutov4=v end)
TabF:AddSection("Farming");TabF:AddDropdown("FarmSel",{Title="Select Farming",Values={"Farm Level","Farm Katakuri","Farm Bone"},Default=1}):OnChanged(function(v)getgenv().FarmMode=v end)
local TG_MAIN=TabF:AddToggle("MainFarm",{Title="Auto Farm",Default=false})
TG_MAIN:OnChanged(function(v)if v then if getgenv().FarmMode=="Farm Katakuri"and(GL()<1500 or not World3)or getgenv().FarmMode=="Farm Bone"and(GL()<1500 or not World3)then TG_MAIN:SetValue(false);return end;if getgenv().FarmMode=="Farm Level"then getgenv().AF,getgenv().AK,getgenv().AB=true,false,false elseif getgenv().FarmMode=="Farm Katakuri"then getgenv().AF,getgenv().AK,getgenv().AB,getgenv().KataIndex=false,true,false,1 elseif getgenv().FarmMode=="Farm Bone"then getgenv().AF,getgenv().AK,getgenv().AB,getgenv().BoneIndex=false,false,true,1 end else getgenv().AF,getgenv().AK,getgenv().AB=false,false,false;RNP();SAT()end end)
TabSt:AddSlider("Pts",{Title="Select Points",Default=1,Min=1,Max=100,Rounding=0}):OnChanged(function(v)getgenv().SP=v end);TabSt:AddDropdown("Stat",{Title="Selecionar Status",Values={"Melee","Defense","Sword","Gun","Blox Fruit"},Default=1}):OnChanged(function(v)getgenv().SA=({Melee="Melee",Defense="Defense",Sword="Sword",Gun="Gun",["Blox Fruit"]="Fruit"})[v]end);TabSt:AddToggle("AS",{Title="Auto Status",Default=false}):OnChanged(function(v)getgenv().AS=v end)
TabSe:AddSection("Server HOP");TabSe:AddButton({Title="Rejoin",Callback=function()game:GetService("TeleportService"):Teleport(game.PlaceId,LP)end});TabSe:AddButton({Title="Hop Server near player",Callback=function()task.spawn(function()local HS,TS2,srvs=game:GetService("HttpService"),game:GetService("TeleportService"),{};local ok,res=pcall(function()return game:HttpGet("https://games.roblox.com/v1/games/"..game.PlaceId.."/servers/Public?sortOrder=Asc&limit=100")end);if ok then local d=HS:JSONDecode(res);if d and d.data then for _,s in ipairs(d.data)do if s.playing and s.playing>=1 and s.playing<=8 and s.id~=game.JobId then table.insert(srvs,s.id)end end end end;if #srvs>0 then TS2:TeleportToPlaceInstance(game.PlaceId,srvs[math.random(1,#srvs)],LP)else TS2:Teleport(game.PlaceId,LP)end end)end});TabSe:AddButton({Title="Fps Boost",Callback=FP})
local SG=Instance.new("ScreenGui");SG.Name="VoltToggle";SG.ResetOnSpawn=false;SG.Parent=LP:WaitForChild("PlayerGui");local BTN=Instance.new("ImageButton");BTN.Size=UDim2.fromOffset(70,70);BTN.Position=UDim2.new(0,20,0,20);BTN.BackgroundTransparency=1;BTN.Image="rbxassetid://101674777317269";BTN.ScaleType=Enum.ScaleType.Fit;BTN.AutoButtonColor=false;BTN.ImageTransparency=0;BTN.Parent=SG;local UIC=Instance.new("UICorner");UIC.CornerRadius=UDim.new(1,0);UIC.Parent=BTN
local dragging,dragInput,dragStart,startPos;local function update(input)local delta=input.Position-dragStart;BTN.Position=UDim2.new(startPos.X.Scale,startPos.X.Offset+delta.X,startPos.Y.Scale,startPos.Y.Offset+delta.Y)end;BTN.InputBegan:Connect(function(input)if input.UserInputType==Enum.UserInputType.MouseButton1 or input.UserInputType==Enum.UserInputType.Touch then dragging=true;dragStart=input.Position;startPos=BTN.Position;input.Changed:Connect(function()if input.UserInputState==Enum.UserInputState.End then dragging=false end end)end end);BTN.InputChanged:Connect(function(input)if input.UserInputType==Enum.UserInputType.MouseMovement or input.UserInputType==Enum.UserInputType.Touch then dragInput=input end end);game:GetService("UserInputService").InputChanged:Connect(function(input)if input==dragInput and dragging then update(input)end end);BTN.MouseButton1Click:Connect(function()Win.Root.Visible=not Win.Root.Visible end)
local RA,RH;task.spawn(function()task.wait(2);local M=RS:WaitForChild("Modules",5);if M then local N=M:FindFirstChild("Net");if N then RA,RH=N:FindFirstChild("RE/RegisterAttack"),N:FindFirstChild("RE/RegisterHit")end end end)
task.spawn(function()while task.wait(0.1)do if IFA()and RA and RH then local tgts={};for _,m in pairs(WS.Enemies:GetChildren())do if m:FindFirstChild("Head")and m:FindFirstChild("Humanoid")and m.Humanoid.Health>0 then local valid=false;if getgenv().AF then local q=GQ();if q and m.Name==(q.M or q.Mon)then valid=true end elseif getgenv().AK then for _,n in ipairs(KM)do if m.Name==n then valid=true;break end end elseif getgenv().AB then for _,n in ipairs(BonM)do if m.Name==n then valid=true;break end end end;if valid then table.insert(tgts,{m,m.Head})end end end;if #tgts>0 then RA:FireServer(0.1);RH:FireServer(tgts[1][2],tgts)end end end end)
task.spawn(function()while task.wait(0.1)do if getgenv().AC and RA and RH then local c,hrp=LP.Character,LP.Character and LP.Character:FindFirstChild("HumanoidRootPart");if not hrp then continue end;local tgts={};for _,m in pairs(WS.Enemies:GetChildren())do if m:FindFirstChild("Head")and m:FindFirstChild("Humanoid")and m.Humanoid.Health>0 and m:FindFirstChild("HumanoidRootPart")and(hrp.Position-m.HumanoidRootPart.Position).Magnitude<=50 then table.insert(tgts,{m,m.Head})end end;if #tgts>0 then RA:FireServer(0.1);RH:FireServer(tgts[1][2],tgts)end end end end)
task.spawn(function()while task.wait(0.5)do if IFA()then EQ();local c=LP.Character;if c then DAC(c)end end end end)
local function PM(c,hrp,hum,fMob,mn)DAC(c);hum:ChangeState(11);local r=fMob:FindFirstChild("HumanoidRootPart");if r then TF25(hrp,r,300);while fMob.Parent and fMob.Humanoid.Health>0 and IFA()and hum.Health>0 do BM(mn);task.wait(0.05)end;SAT()end end
local function HMR(mList,iVar,sCF)local aM,mn=FAM(mList);if aM then for i,n in ipairs(mList)do if n==mn then getgenv()[iVar]=i;break end end;local h,r=aM:FindFirstChild("Humanoid"),aM:FindFirstChild("HumanoidRootPart");if h and r and h.Health>0 then local c,hrp,hum=LP.Character,LP.Character:FindFirstChild("HumanoidRootPart"),LP.Character:FindFirstChild("Humanoid");if c and hrp and hum then PM(c,hrp,hum,aM,mn);if not FMS(mn)then getgenv()[iVar]=getgenv()[iVar]+1;if getgenv()[iVar]>#mList then getgenv()[iVar]=1 end end end end else if not FMS(mList[getgenv()[iVar]])then getgenv()[iVar]=getgenv()[iVar]+1;if getgenv()[iVar]>#mList then getgenv()[iVar]=1 end end;local c,hrp=LP.Character,LP.Character and LP.Character:FindFirstChild("HumanoidRootPart");if c and hrp then SAT();TTG(hrp,sCF,250);task.wait(0.5)end end end
local function TryGetQuest(qN,qL,qCF)local currentTime=tick();if currentTime-getgenv().LastQuestAttempt<1 then return false end;local c,hrp=LP.Character,LP.Character and LP.Character:FindFirstChild("HumanoidRootPart");if not c or not hrp then return false end;local dist=(hrp.Position-qCF.Position).Magnitude;if dist>5 then SAT();TTG(hrp,qCF,250);return false end;getgenv().LastQuestAttempt=currentTime;local success=pcall(function()CF:InvokeServer("StartQuest",qN,qL)end);if success then getgenv().CurrentQuestName,getgenv().CurrentQuestLevel=qN,qL;task.wait(1);return true end;return false end
task.spawn(function()while task.wait(0.15)do if not IFA()then continue end;local c,hrp,hum=LP.Character,LP.Character and LP.Character:FindFirstChild("HumanoidRootPart"),LP.Character and LP.Character:FindFirstChild("Humanoid");if not c or not hrp or not hum or hum.Health<=0 then if hum and hum.Health<=0 then SAT();repeat task.wait()until LP.Character and LP.Character:FindFirstChild("HumanoidRootPart")and LP.Character:FindFirstChild("Humanoid")and LP.Character.Humanoid.Health>0;task.wait(1)end;continue end;if getgenv().AF then local q=GQ();if not q then continue end;local qN,qL,mn,msCF=q.N or q.NameQuest,q.L or q.LevelQuest,q.M or q.Mon,q.SC or q.CFrameMon;local qCF=q.C or q.CFrameQuest or CFrame.new(msCF.Position.X,msCF.Position.Y>0 and msCF.Position.Y or 50,msCF.Position.Z);if getgenv().CurrentQuestName~=qN or getgenv().CurrentQuestLevel~=qL then CQ();getgenv().CurrentQuestName,getgenv().CurrentQuestLevel=nil,nil;SAT();task.wait(0.5)end;if not HQ()then if not TryGetQuest(qN,qL,qCF)then continue end end;local fMob=FMS(mn);if fMob then PM(c,hrp,hum,fMob,mn)else SAT();TTG(hrp,CFrame.new(msCF.Position.X,msCF.Position.Y>0 and msCF.Position.Y or 50,msCF.Position.Z),250);task.wait(0.5)end elseif getgenv().AK then HMR(KM,"KataIndex",KS)elseif getgenv().AB then HMR(BonM,"BoneIndex",BS)end end end)
task.spawn(function()while task.wait(1)do if getgenv().AS and getgenv().SA and CF then CF:InvokeServer("AddPoint",getgenv().SA,getgenv().SP)end end end)
task.spawn(function()while task.wait(0.3)do if getgenv().AV3 then RS.Remotes.CommE:FireServer("ActivateAbility")end end end)
spawn(function()while wait(0.2)do if getgenv().GRaceClickAutov4 then local c=LP.Character;if c and c:FindFirstChild("RaceEnergy")then local rE=c.RaceEnergy;if rE and rE.Value>=1 then US(nil,"Y")end end end end end)
Fl:Notify({Title="Volt Hub",Content="Carregado! Sea: "..GetSea().." | Lv: "..GL(),Duration=5})
-- ESP Manager & Fruits + Auto Collect Fruits (MÓDULO SEPARADO)
local PS=game:GetService("Players");local WS=game:GetService("Workspace")
local RS=game:GetService("ReplicatedStorage");local TweenService=game:GetService("TweenService")
local CS=game:GetService("CollectionService");local RunService=game:GetService("RunService")
local Plr=PS.LocalPlayer

if not Win or not Fl then return end

local TabEF=Win:AddTab({Title="Stack Farming",Icon="swords"})

local ESP_Player=false;local ESP_Fruit=false;local ESP_Island=false;local ESP_Chest=false
local AutoRF=false;local AutoSF=false;local AQK=false

local function MakeTag(part,text,color,stroke,isIsland)
    if not part or not part:IsA("BasePart")then return end
    local gui=part:FindFirstChild("NexusESP_Tag")
    if not gui then
        gui=Instance.new("BillboardGui");gui.Name="NexusESP_Tag"
        gui.Size=UDim2.new(0,150,0,25);gui.AlwaysOnTop=true;gui.LightInfluence=0;gui.MaxDistance=1e6;gui.Adornee=part
        local tl=Instance.new("TextLabel");tl.Name="TextLabel"
        tl.BackgroundTransparency=1;tl.Size=UDim2.new(1,0,1,0)
        tl.Font=Enum.Font.SourceSansBold;tl.Parent=gui
        gui.Parent=part
    end
    local tl=gui:FindFirstChild("TextLabel")
    if tl then 
        tl.Text=text;tl.TextColor3=color or Color3.new(1,1,1)
        if isIsland then
            tl.TextStrokeTransparency=1;tl.TextSize=20
        elseif stroke then
            tl.TextStrokeTransparency=0.3;tl.TextStrokeColor3=Color3.new(0,0,0);tl.TextSize=18
        else
            tl.TextStrokeTransparency=1;tl.TextSize=16
        end
    end
end

local function ClearESP()
    for _,v in ipairs(WS:GetDescendants())do
        if v:IsA("BillboardGui")and v.Name=="NexusESP_Tag"then v:Destroy()end
    end
end

local FruitNames={"Bomb-Bomb","Spike-Spike","Chop-Chop","Spring-Spring","Kilo-Kilo","Smoke-Smoke","Flame-Flame","Ice-Ice","Sand-Sand","Dark-Dark","Ghost-Ghost","Magma-Magma","Quake-Quake","Buddha-Buddha","Love-Love","Spider-Spider","Phoenix-Phoenix","Portal-Portal","Rumble-Rumble","Pain-Pain","Blizzard-Blizzard","Gravity-Gravity","Dough-Dough","Shadow-Shadow","Venom-Venom","Control-Control","Spirit-Spirit","Dragon-Dragon","Leopard-Leopard"}
local FruitSet={}for _,n in ipairs(FruitNames)do FruitSet[n]=true end

local function IsFruitModel(m)
    if not m or not m:IsA("Model")then return false end
    return FruitSet[m.Name]or m.Name:find("Fruit")~=nil
end

local function GetNearestFruit()
    local my=Plr.Character and Plr.Character:FindFirstChild("HumanoidRootPart")
    if not my then return end
    local best,dist=nil,1e9
    for _,m in ipairs(WS:GetChildren())do
        if IsFruitModel(m)then
            local p=m:FindFirstChildWhichIsA("BasePart")
            if p then
                local d=(p.Position-my.Position).Magnitude
                if d<dist then dist,best=d,p end
            end
        end
    end
    return best
end

local function AnyFruit()
    for _,m in ipairs(WS:GetChildren())do if IsFruitModel(m)then return true end end
    return false
end

local function HasFruitInInventory()
    for _,tool in pairs(Plr.Backpack:GetChildren())do
        if tool:FindFirstChild("EatRemote",true)then return true end
    end
    local char=Plr.Character
    if char then
        for _,tool in pairs(char:GetChildren())do
            if tool:IsA("Tool")and tool:FindFirstChild("EatRemote",true)then return true end
        end
    end
    return false
end

local function UpdateESPPlayers()
    if not ESP_Player then return end
    for _,pl in ipairs(PS:GetPlayers())do
        if pl~=Plr then
            local ch=pl.Character;local hrp=ch and ch:FindFirstChild("HumanoidRootPart")
            if hrp then
                local my=Plr.Character and Plr.Character:FindFirstChild("HumanoidRootPart")
                local dist=my and math.floor((hrp.Position-my.Position).Magnitude)or 0
                MakeTag(hrp,pl.Name.." ("..dist.."m)",Color3.fromRGB(0,170,255),true)
            end
        end
    end
end

local function UpdateESPFruits()
    if not ESP_Fruit then return end
    local my=Plr.Character and Plr.Character:FindFirstChild("HumanoidRootPart")
    for _,m in ipairs(WS:GetChildren())do
        if IsFruitModel(m)then
            local p=m:FindFirstChildWhichIsA("BasePart")
            if p then
                local dist=my and math.floor((p.Position-my.Position).Magnitude)or 0
                MakeTag(p,m.Name.." ("..dist.."m)",Color3.new(1,0,0),true)
            end
        end
    end
end

local IslandTags={"Island","SpawnIsland","Location","MapIsland"}
local function IsIslandByStructure(obj)
    if not obj:IsA("Model")then return false end
    local name=obj.Name:lower()
    if name:find("island")or name:find("ilha")then return true end
    return obj:FindFirstChild("NPCs")or obj:FindFirstChild("Locations")or obj:FindFirstChild("Spawns")or obj:FindFirstChild("Enemies")or obj:FindFirstChildWhichIsA("SpawnLocation",true)
end

local function GetIslandPart(obj)
    return obj.PrimaryPart or obj:FindFirstChildWhichIsA("SpawnLocation",true)or obj:FindFirstChildWhichIsA("BasePart")
end

local function UpdateESPIslands()
    if not ESP_Island then return end
    local my=Plr.Character and Plr.Character:FindFirstChild("HumanoidRootPart")
    local done={}
    for _,tag in ipairs(IslandTags)do
        for _,obj in ipairs(CS:GetTagged(tag))do
            if not done[obj]and obj:IsA("Model")then
                local part=GetIslandPart(obj)
                if part then
                    local dist=my and math.floor((part.Position-my.Position).Magnitude)or 0
                    MakeTag(part,obj.Name.." ("..dist.."m)",Color3.fromRGB(255,170,0),false,true)
                    done[obj]=true
                end
            end
        end
    end
    for _,obj in ipairs(WS:GetDescendants())do
        if not done[obj]and IsIslandByStructure(obj)then
            local part=GetIslandPart(obj)
            if part then
                local dist=my and math.floor((part.Position-my.Position).Magnitude)or 0
                MakeTag(part,obj.Name.." ("..dist.."m)",Color3.fromRGB(255,170,0),false,true)
                done[obj]=true
            end
        end
    end
end

local function GetChestColor(chestName)
    local name=chestName:lower()
    if name:find("diamond")or name:find("diamante")then return Color3.fromRGB(0,255,255)
    elseif name:find("gold")or name:find("dourado")or name:find("golden")then return Color3.fromRGB(255,255,0)
    else return Color3.fromRGB(0,255,0)end
end

local ChestTags={"Chest","Treasure","Loot","ChestModel","Interactable"}
local function IsChestByStructure(obj)
    if not obj:IsA("Model")then return false end
    local name=obj.Name:lower()
    return name:find("chest")or name:find("baú")or obj:FindFirstChild("Root")or obj:FindFirstChild("Hitbox")or obj:FindFirstChildWhichIsA("ClickDetector",true)
end

local function GetChestPart(obj)
    if obj:IsA("BasePart")then return obj
    elseif obj:IsA("Model")then return obj.PrimaryPart or obj:FindFirstChildWhichIsA("BasePart")end
end

local function UpdateESPChests()
    if not ESP_Chest then return end
    local my=Plr.Character and Plr.Character:FindFirstChild("HumanoidRootPart")
    local done={}
    for _,tag in ipairs(ChestTags)do
        for _,obj in ipairs(CS:GetTagged(tag))do
            if not done[obj]then
                local part=GetChestPart(obj)
                if part then
                    local dist=my and math.floor((part.Position-my.Position).Magnitude)or 0
                    MakeTag(part,"Chest ("..dist.."m)",GetChestColor(obj.Name),true)
                    done[obj]=true
                end
            end
        end
    end
    for _,obj in ipairs(WS:GetDescendants())do
        if not done[obj]and IsChestByStructure(obj)then
            local part=GetChestPart(obj)
            if part then
                local dist=my and math.floor((part.Position-my.Position).Magnitude)or 0
                MakeTag(part,"Chest ("..dist.."m)",GetChestColor(obj.Name),true)
                done[obj]=true
            end
        end
    end
end

-- Tab Status & ESP (ESP Section)
if TabSt then
    TabSt:AddSection("ESP")
    TabSt:AddToggle("ESPPlayer",{Title="ESP Players",Default=false}):OnChanged(function(v)ESP_Player=v;if not v then ClearESP()end end)
    TabSt:AddToggle("ESPFruit",{Title="ESP Fruits",Default=false}):OnChanged(function(v)ESP_Fruit=v;if not v then ClearESP()end end)
    TabSt:AddToggle("ESPIsland",{Title="ESP Ilha",Default=false}):OnChanged(function(v)ESP_Island=v;if not v then ClearESP()end end)
    TabSt:AddToggle("ESPChest",{Title="ESP Chest",Default=false}):OnChanged(function(v)ESP_Chest=v;if not v then ClearESP()end end)
end

-- Tab Stack Farming
TabEF:AddSection("Auto Fruits")
TabEF:AddToggle("AutoRF",{Title="Auto Random Fruit",Default=false}):OnChanged(function(v)AutoRF=v end)
TabEF:AddToggle("ACF_MOD",{Title="Auto Collect Fruits",Default=false}):OnChanged(function(v)getgenv().ACF=v end)
TabEF:AddToggle("AutoStoreFruit",{Title="Auto Store Fruit",Default=false}):OnChanged(function(v)AutoSF=v end)

-- Accept Quest Katakuri/Bone Toggle (Em Tab Farming)
if TabF then
    TabF:AddToggle("AcceptQuestKB",{Title="Accept Quest Katakuri/Bone",Default=false}):OnChanged(function(v)AQK=v end)
end

_G.RemoveNotifications=false;local NotifLoop,NotifConnection=nil,nil
local function StartRemovingNotifications()
    if NotifLoop then return end
    pcall(function()local PlayerGui=Plr:WaitForChild("PlayerGui")for _,gui in pairs(PlayerGui:GetChildren())do if gui:IsA("ScreenGui")then for _,child in pairs(gui:GetDescendants())do if child.Name:find("Notification")or child.Name:find("Notify")or child.Name:find("Alert")or(child:IsA("Frame")and child.Name:find("Popup"))then child:Destroy()end end end end end)
    NotifLoop=task.spawn(function()while _G.RemoveNotifications do task.wait(0.05)pcall(function()local PlayerGui=Plr:WaitForChild("PlayerGui")for _,gui in pairs(PlayerGui:GetChildren())do if gui:IsA("ScreenGui")then for _,child in pairs(gui:GetDescendants())do if child.Name:find("Notification")or child.Name:find("Notify")or child.Name:find("Alert")or(child:IsA("Frame")and child.Name:find("Popup"))then child:Destroy()end end end end end)end end)
    local PlayerGui=Plr:WaitForChild("PlayerGui")
    NotifConnection=PlayerGui.DescendantAdded:Connect(function(child)if not _G.RemoveNotifications then return end;task.wait()pcall(function()if child.Name:find("Notification")or child.Name:find("Notify")or child.Name:find("Alert")or(child:IsA("Frame")and child.Name:find("Popup"))then child:Destroy()end end)end)
end

local function StopRemovingNotifications()
    if NotifLoop then task.cancel(NotifLoop);NotifLoop=nil end
    if NotifConnection then NotifConnection:Disconnect();NotifConnection=nil end
end

local NoClipEnabled,NoClipConnection=false,nil
local function EnableNoClip()
    NoClipEnabled=true;if NoClipConnection then return end
    NoClipConnection=RunService.Stepped:Connect(function()if not NoClipEnabled then return end;local char=Plr.Character;if not char then return end;for _,part in pairs(char:GetDescendants())do if part:IsA("BasePart")then part.CanCollide=false end end end)
end

local function DisableNoClip()
    NoClipEnabled=false;if NoClipConnection then NoClipConnection:Disconnect();NoClipConnection=nil end
    local char=Plr.Character;if char then for _,part in pairs(char:GetDescendants())do if part:IsA("BasePart")and part.Name~="HumanoidRootPart"then part.CanCollide=true end end end
end

-- Movendo toggles para Tab Settings Farming (abaixo do Auto Active v4)
if TabSF then
    TabSF:AddToggle("ABuso",{Title="Auto Active Buso",Default=false}):OnChanged(function(v)_G.BusoAuto=v end)
    TabSF:AddToggle("RemoveNotif",{Title="Remove Notifications",Default=false}):OnChanged(function(v)_G.RemoveNotifications=v;if v then StartRemovingNotifications()else StopRemovingNotifications()end end)
    TabSF:AddToggle("NoClip",{Title="NoClip",Default=false}):OnChanged(function(v)if v then EnableNoClip()else DisableNoClip()end end)
end

-- Teleport Sea Buttons
if TabM and CF then
    local function GetSea()
        if game.PlaceId==2753915549 or game.PlaceId==85211729168715 then return 1
        elseif game.PlaceId==4442272183 or game.PlaceId==79091703265657 then return 2
        elseif game.PlaceId==7449423635 or game.PlaceId==100117331123089 then return 3
        else return 1 end
    end
    
    TabM:AddButton({Title="Teleport Sea 1",Description="Viajar para Sea 1",Callback=function()
        if GetSea()==1 then return end
        CF:InvokeServer("TravelMain")
    end})
    
    TabM:AddButton({Title="Teleport Sea 2",Description="Viajar para Sea 2",Callback=function()
        if GetSea()==2 then return end
        CF:InvokeServer("TravelDressrosa")
    end})
    
    TabM:AddButton({Title="Teleport Sea 3",Description="Viajar para Sea 3",Callback=function()
        if GetSea()==3 then return end
        CF:InvokeServer("TravelZou")
    end})
end

-- Auto Accept Quest para Katakuri/Bone
local function HQ()local ok,r=pcall(function()return Plr.PlayerGui.Main.Quest.Visible end)return ok and r end
getgenv().LastQuestAccept=0

task.spawn(function()
    while task.wait(3)do
        pcall(function()
            if not AQK or not CF then return end
            local isKata,isBone=getgenv().AK,getgenv().AB
            if not isKata and not isBone then return end
            
            local qN,qL=isKata and "CakeQuest2" or "HauntedQuest2",2
            local now=tick()
            
            if not HQ()and now-getgenv().LastQuestAccept>5 then
                CF:InvokeServer("StartQuest",qN,qL)
                getgenv().LastQuestAccept=now
            end
        end)
    end
end)

-- Loop de ESP e Auto Random Fruit
task.spawn(function()
    while task.wait(0.25)do
        pcall(function()
            for _,v in ipairs(WS:GetDescendants())do if v:IsA("BillboardGui")and v.Name=="NexusESP_Tag"and(not v.Adornee or not v.Adornee.Parent)then v:Destroy()end end
            if ESP_Player then UpdateESPPlayers()end
            if ESP_Fruit then UpdateESPFruits()end
            if ESP_Island then UpdateESPIslands()end
            if ESP_Chest then UpdateESPChests()end
            if AutoRF and CF then CF:InvokeServer("Cousin","Buy")end
        end)
    end
end)

-- Auto Store Fruit
local UpdStFruit=function()
    -- Armazena frutas do Backpack
    for _,tool in pairs(Plr.Backpack:GetChildren())do 
        local eatRemote=tool:FindFirstChild("EatRemote",true)
        if eatRemote then 
            RS.Remotes.CommF_:InvokeServer("StoreFruit",eatRemote.Parent:GetAttribute("OriginalName"),Plr.Backpack:FindFirstChild(tool.Name))
        end 
    end
    -- Armazena frutas na mão do player
    local char=Plr.Character
    if char then
        for _,tool in pairs(char:GetChildren())do
            if tool:IsA("Tool")then
                local eatRemote=tool:FindFirstChild("EatRemote",true)
                if eatRemote then
                    RS.Remotes.CommF_:InvokeServer("StoreFruit",eatRemote.Parent:GetAttribute("OriginalName"),char:FindFirstChild(tool.Name))
                end
            end
        end
    end
end
task.spawn(function()while true do task.wait(0.5)if not AutoSF then continue end;pcall(function()UpdStFruit()end)end end)

-- Auto Buso
spawn(function()while task.wait(0.5)do pcall(function()local Player=game:GetService("Players").LocalPlayer;if _G.BusoAuto then local HasBusoName,BusoName="HasBuso","Buso";if Player.Character and not Player.Character:FindFirstChild(HasBusoName)then game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(BusoName)end end end)end end)

-- Auto Collect Fruits
local activeTween,heartbeatConn=nil,nil
local function StopTweenAndHeartbeat()
    if activeTween then activeTween:Cancel();activeTween=nil end
    if heartbeatConn then heartbeatConn:Disconnect();heartbeatConn=nil end
end

local isCollecting=false

task.spawn(function()
    while task.wait(0.3)do
        pcall(function()
            if not getgenv().ACF then 
                StopTweenAndHeartbeat()
                isCollecting=false
                return 
            end
            
            if isCollecting then return end
            
            if not AnyFruit()then 
                StopTweenAndHeartbeat()
                isCollecting=false
                return 
            end
            
            isCollecting=true
            
            local wasAF,wasAK,wasAB=getgenv().AF,getgenv().AK,getgenv().AB
            getgenv().AF,getgenv().AK,getgenv().AB=false,false,false
            
            local fruitPart=GetNearestFruit()
            if not fruitPart then 
                getgenv().AF,getgenv().AK,getgenv().AB=wasAF,wasAK,wasAB
                isCollecting=false
                return 
            end
            
            local char=Plr.Character
            local hrp=char and char:FindFirstChild("HumanoidRootPart")
            if not hrp then 
                getgenv().AF,getgenv().AK,getgenv().AB=wasAF,wasAK,wasAB
                isCollecting=false
                return 
            end
            
            local distance=(hrp.Position-fruitPart.Position).Magnitude
            local duration=distance/250
            
            activeTween=TweenService:Create(hrp,TweenInfo.new(duration,Enum.EasingStyle.Linear),{CFrame=fruitPart.CFrame})
            activeTween:Play()
            
            heartbeatConn=RunService.Heartbeat:Connect(function()
                if not fruitPart or not fruitPart.Parent then 
                    StopTweenAndHeartbeat()
                    return 
                end
                if not getgenv().ACF then 
                    StopTweenAndHeartbeat()
                    return 
                end
                hrp.Velocity=Vector3.new(0,0,0)
            end)
            
            activeTween.Completed:Wait()
            task.wait(0.2)
            
            StopTweenAndHeartbeat()
            
            -- Aguarda a coleta da fruta atual
            local maxWait=3
            local waited=0
            while waited<maxWait and fruitPart and fruitPart.Parent do
                task.wait(0.1)
                waited=waited+0.1
                if HasFruitInInventory()then break end
            end
            
            getgenv().AF,getgenv().AK,getgenv().AB=wasAF,wasAK,wasAB
            isCollecting=false
        end)
    end
end)
-- Módulo: Estilo de Luta, TTK e Boss Farm - Nexus Hub V3
local RS = game:GetService("ReplicatedStorage")
local TS = game:GetService("TweenService")
local RSvc = game:GetService("RunService")
local Plr = game:GetService("Players").LocalPlayer
local WS = game:GetService("Workspace")

local Remotes = RS:WaitForChild("Remotes", 5)
local CF = Remotes:FindFirstChild("CommF_")

-- Configurações globais
getgenv().AutoBuyLegendarySword = false
getgenv().SelectBoss = nil
getgenv().AutoFarmBoss = false
getgenv().AutoFarmAllBoss = false

-- Detecção de Sea
local placeId = game.PlaceId
World1 = placeId == 2753915549 or placeId == 85211729168715
World2 = placeId == 4442272183 or placeId == 79091703265657
World3 = placeId == 7449423635 or placeId == 100117331123089

function GetSea()
    if World1 then return 1 
    elseif World2 then return 2 
    elseif World3 then return 3 
    else return 1 end
end

-- Sistema de Tween Anti-Tremor
local activeTween, heartbeatConn = nil, nil

local function StopTweenAndHeartbeat()
    if activeTween then activeTween:Cancel() activeTween = nil end
    if heartbeatConn then heartbeatConn:Disconnect() heartbeatConn = nil end
end

local function TweenToPosition(targetCFrame)
    local char, hrp = Plr.Character, Plr.Character and Plr.Character:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    StopTweenAndHeartbeat()
    local distance = (hrp.Position - targetCFrame.Position).Magnitude
    activeTween = TS:Create(hrp, TweenInfo.new(distance / 250, Enum.EasingStyle.Linear), {CFrame = targetCFrame})
    activeTween:Play()
    heartbeatConn = RSvc.Heartbeat:Connect(function()
        if not hrp or not hrp.Parent then StopTweenAndHeartbeat() return end
        hrp.Velocity = Vector3.new(0, 0, 0)
    end)
    return activeTween
end

local function SetNoClip(char, enabled)
    if not char then return end
    for _, p in ipairs(char:GetDescendants()) do
        if p:IsA("BasePart") and (p.Name == "HumanoidRootPart" or p.Name == "UpperTorso" or p.Name == "LowerTorso" or p.Name == "Torso") then
            p.CanCollide = not enabled
        end
    end
end

local function EquipWeapon()
    pcall(function()
        local c, bp = Plr.Character, Plr.Backpack
        if not c or not c:FindFirstChild("Humanoid") then return end
        local tool = nil
        if getgenv().WP == "Sword" then
            for _, v in ipairs(bp:GetChildren()) do
                if v:IsA("Tool") and (v.ToolTip == "Sword" or v.Name:find("Katana") or v.Name:find("Blade")) then
                    tool = v break
                end
            end
        end
        if not tool then tool = bp:FindFirstChild("Combat") end
        if tool then c.Humanoid:EquipTool(tool) end
    end)
end

-- Posições dos NPCs de Fighting Styles
local FightingStyleNPCs = {
    ["Dark Step"] = {pos = CFrame.new(-983.618, 12.45, 3990.463), sea = 1},
    ["Electro"] = {pos = CFrame.new(-5382.782, 12.55, -2148.818), sea = 1},
    ["Fishman Karate"] = {pos = CFrame.new(61586.722, 18.9, 989.584), sea = 1},
    ["Dragon Breath"] = {pos = CFrame.new(699.572, 186.99, 656.837), sea = 2},
    ["Death Step"] = {pos = CFrame.new(6358.787, 296.661, -6766.079), sea = 2},
    ["Sharkman Karate"] = {pos = CFrame.new(-2602.152, 239.212, -10315.58), sea = 2},
    ["Electric Claw"] = {pos = CFrame.new(6358.787, 296.661, -6766.079), sea = 3},
    ["Dragon Talon"] = {pos = CFrame.new(5666.225, 1211.307, 866.386), sea = 3},
    ["Godhuman"] = {pos = CFrame.new(-13777.618, 334.652, -9879.684), sea = 3},
    ["Sanguine Art"] = {pos = CFrame.new(-16515.053, 23.17, -193.006), sea = 3}
}

local function BuyFightingStyle(styleName, remoteCommand)
    local styleData = FightingStyleNPCs[styleName]
    if not styleData then return end
    
    local currentSea = GetSea()
    if currentSea < styleData.sea then
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "Volt Hub V3",
            Text = "Você precisa estar no Sea " .. styleData.sea .. " para comprar " .. styleName,
            Duration = 5
        })
        return
    end
    
    local tween = TweenToPosition(styleData.pos)
    if tween then
        tween.Completed:Wait()
        task.wait(0.5)
        StopTweenAndHeartbeat()
        pcall(remoteCommand)
    end
end

local function BuyLegendarySword()
    if not CF then return end
    for _, sword in ipairs({"Shisui", "Saddi", "Wando"}) do
        local hasSword = false
        pcall(function()
            if Plr.Backpack:FindFirstChild(sword) or (Plr.Character and Plr.Character:FindFirstChild(sword)) then
                hasSword = true
            end
        end)
        if not hasSword then
            pcall(function() CF:InvokeServer("BuyItem", "Legendary Sword Dealer", sword) end)
            task.wait(0.5)
        end
    end
end

-- IMPORTANTE: Aguarda as tabs serem criadas
task.wait(1)

-- Verifica se TabS existe antes de adicionar
if TabS then
    TabS:AddSection("Estilos de Lutas")
    
    TabS:AddButton({Title = "Buy Dark Step", Callback = function() BuyFightingStyle("Dark Step", function() CF:InvokeServer("BuyBlackLeg") end) end})
    TabS:AddButton({Title = "Buy Eletric", Callback = function() BuyFightingStyle("Electro", function() CF:InvokeServer("BuyElectro") end) end})
    TabS:AddButton({Title = "Buy Water Kung Fu", Callback = function() BuyFightingStyle("Fishman Karate", function() CF:InvokeServer("BuyFishmanKarate") end) end})
    TabS:AddButton({Title = "Buy Dragon Breath", Callback = function() BuyFightingStyle("Dragon Breath", function() CF:InvokeServer("BlackbeardReward", "DragonClaw", "1") CF:InvokeServer("BlackbeardReward", "DragonClaw", "2") end) end})
    TabS:AddButton({Title = "Buy Death Step", Callback = function() BuyFightingStyle("Death Step", function() CF:InvokeServer("BuyDeathStep") end) end})
    TabS:AddButton({Title = "Buy Sharkman Karatê", Callback = function() BuyFightingStyle("Sharkman Karate", function() CF:InvokeServer("BuySharkmanKarate", true) CF:InvokeServer("BuySharkmanKarate") end) end})
    TabS:AddButton({Title = "Buy Eletric Claw", Callback = function() BuyFightingStyle("Electric Claw", function() CF:InvokeServer("BuyElectricClaw", "Start") CF:InvokeServer("BuyElectricClaw") end) end})
    TabS:AddButton({Title = "Buy Dragon Talon", Callback = function() BuyFightingStyle("Dragon Talon", function() CF:InvokeServer("BuyDragonTalon", true) CF:InvokeServer("BuyDragonTalon") end) end})
    TabS:AddButton({Title = "Buy GodHuman", Callback = function() BuyFightingStyle("Godhuman", function() CF:InvokeServer("BuyGodhuman", true) CF:InvokeServer("BuyGodhuman") end) end})
    TabS:AddButton({Title = "Buy Sanguine Art", Callback = function() BuyFightingStyle("Sanguine Art", function() CF:InvokeServer("BuySanguineArt", true) CF:InvokeServer("BuySanguineArt") end) end})
    
    local TG_ABLS = TabS:AddToggle("AutoBuyLegSword", {Title = "Auto Buy Legendary Sword", Default = false})
    TG_ABLS:OnChanged(function(v) getgenv().AutoBuyLegendarySword = v end)
end

-- Verifica se TabSe existe antes de adicionar o botão de códigos
if TabSe then
    TabSe:AddButton({
        Title = "Redeem All Codes",
        Callback = function()
            local codes = {
                "LIGHTNINGABUSE", "1LOSTADMIN", "ADMINFIGHT", "GIFTINGHOURS", "NOMOREHACK",
                "BANEXPLOIT", "WildDares", "BossBuild", "GetPranked", "EARNFRUITS",
                "KITTRESET", "Bignews", "CHANDLER", "Fudd10", "fudd10v2",
                "Sub2UncleKizaru", "FIGHT4FRUIT", "kittgaming", "TRIPLEABUSE",
                "Sub2CaptainMaui", "Sub2Fer999", "EnyuisPro", "Magicbus", "JCWK",
                "Starcodeheo", "Bluxxy", "SUB2GAMERROBOT_EXP1", "Sub2NoobMaster123",
                "Sub2Daigrock", "Axiore", "TantaiGaming", "StrawHatMaine",
                "Sub2OfficialNoobie", "TheGreatAce", "JULYUPDATERESET", "ADMINHACKED",
                "SEATROLLING", "24NOADMIN", "ADMINTROLL", "NEWTROLL", "SECRETADMIN",
                "staffbattle", "NOEXPLOIT", "NOOB2ADMIN", "CODESLIDE", "fruitconcepts",
                "krazydares"
            }
            
            local Redeem = Remotes and Remotes:FindFirstChild("Redeem")
            if not Redeem then 
                game:GetService("StarterGui"):SetCore("SendNotification", {
                    Title = "Volt Hub V3",
                    Text = "Sistema de códigos indisponível!",
                    Duration = 5
                })
                return 
            end
            
            for i, code in ipairs(codes) do
                task.wait(0.1)
                pcall(function()
                    Redeem:InvokeServer(code)
                end)
            end
            
            game:GetService("StarterGui"):SetCore("SendNotification", {
                Title = "Volt Hub V3",
                Text = "Todos os códigos foram resgatados!",
                Duration = 5
            })
        end
    })
end

task.spawn(function()
    while task.wait(5) do
        if getgenv().AutoBuyLegendarySword then pcall(BuyLegendarySword) end
    end
end)

-- Boss Farm System
local tableBoss = {}
if World1 then
    tableBoss = {"The Gorilla King", "Bobby", "Yeti", "Mob Leader", "Vice Admiral", "Warden", "Chief Warden", "Swan", "Magma Admiral", "Fishman Lord", "Wysper", "Thunder God", "Cyborg", "Saber Expert"}
elseif World2 then
    tableBoss = {"Diamond", "Jeremy", "Fajita", "Don Swan", "Smoke Admiral", "Cursed Captain", "Darkbeard", "Order", "Awakened Ice Admiral", "Tide Keeper"}
elseif World3 then
    tableBoss = {"Stone", "Island Empress", "Kilo Admiral", "Captain Elephant", "Beautiful Pirate", "rip_indra True Form", "Longma", "Soul Reaper", "Cake Queen", "Cake Prince", "Dough King"}
end

-- Verifica se TabEF existe
if TabEF then
    TabEF:AddSection("Boss Farm")
    
    local Dropdown = TabEF:AddDropdown("Dropdown", {Title = "Select Boss", Values = tableBoss, Multi = false})
    Dropdown:OnChanged(function(Value) getgenv().SelectBoss = Value end)
    
    local Toggle = TabEF:AddToggle("Toggle", {Title = "Auto Kill Boss", Default = getgenv().AutoFarmBoss})
    Toggle:OnChanged(function(Value)
        getgenv().AutoFarmBoss = Value
        if not Value then
            StopTweenAndHeartbeat()
            local char = Plr.Character
            if char and char:FindFirstChild("HumanoidRootPart") and char:FindFirstChild("Humanoid") then
                char.HumanoidRootPart.Anchored = false
                char.HumanoidRootPart.AssemblyLinearVelocity = Vector3.new()
                char.Humanoid:ChangeState(Enum.HumanoidStateType.RunningNoPhysics)
                task.wait(0.1)
                char.Humanoid:ChangeState(Enum.HumanoidStateType.Freefall)
            end
        end
    end)
    
    local Toggle2 = TabEF:AddToggle("Toggle2", {Title = "Auto Kill All Boss", Default = false})
    Toggle2:OnChanged(function(Value)
        getgenv().AutoFarmAllBoss = Value
        if not Value then
            StopTweenAndHeartbeat()
            local char = Plr.Character
            if char and char:FindFirstChild("HumanoidRootPart") and char:FindFirstChild("Humanoid") then
                char.HumanoidRootPart.Anchored = false
                char.HumanoidRootPart.AssemblyLinearVelocity = Vector3.new()
                char.Humanoid:ChangeState(Enum.HumanoidStateType.RunningNoPhysics)
                task.wait(0.1)
                char.Humanoid:ChangeState(Enum.HumanoidStateType.Freefall)
            end
        end
    end)
end

-- Loop Auto Kill Boss
spawn(function()
    while task.wait(0.2) do
        if getgenv().AutoFarmBoss and getgenv().SelectBoss then
            pcall(function()
                local char, hrp, hum = Plr.Character, Plr.Character and Plr.Character:FindFirstChild("HumanoidRootPart"), Plr.Character and Plr.Character:FindFirstChild("Humanoid")
                if not char or not hrp or not hum then return end
                
                local boss = WS.Enemies:FindFirstChild(getgenv().SelectBoss)
                if boss then
                    for _, v in pairs(WS.Enemies:GetChildren()) do
                        if v.Name == getgenv().SelectBoss and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                            repeat
                                task.wait()
                                SetNoClip(char, true)
                                EquipWeapon()
                                v.HumanoidRootPart.CanCollide = false
                                v.Humanoid.WalkSpeed = 0
                                v.HumanoidRootPart.Size = Vector3.new(80, 80, 80)
                                hum:ChangeState(Enum.HumanoidStateType.RunningNoPhysics)
                                hrp.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 25, 0)
                                hrp.AssemblyLinearVelocity = Vector3.zero
                            until not getgenv().AutoFarmBoss or not v.Parent or v.Humanoid.Health <= 0
                            StopTweenAndHeartbeat()
                        end
                    end
                else
                    local replicatedBoss = RS:FindFirstChild(getgenv().SelectBoss)
                    if replicatedBoss and replicatedBoss:FindFirstChild("HumanoidRootPart") then
                        local tween = TweenToPosition(replicatedBoss.HumanoidRootPart.CFrame * CFrame.new(5, 10, 7))
                        if tween then tween.Completed:Wait() end
                    end
                end
            end)
        end
    end
end)

-- Loop Auto Kill All Boss
spawn(function()
    while task.wait(0.2) do
        if getgenv().AutoFarmAllBoss then
            pcall(function()
                for i, boss in pairs(tableBoss) do
                    if WS.Enemies:FindFirstChild(boss) then
                        for i, v in pairs(WS.Enemies:GetChildren()) do
                            if v.Name == boss and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                local char, hrp, hum = Plr.Character, Plr.Character and Plr.Character:FindFirstChild("HumanoidRootPart"), Plr.Character and Plr.Character:FindFirstChild("Humanoid")
                                if not char or not hrp or not hum then return end
                                repeat
                                    task.wait()
                                    SetNoClip(char, true)
                                    EquipWeapon()
                                    v.HumanoidRootPart.CanCollide = false
                                    v.Humanoid.WalkSpeed = 0
                                    v.HumanoidRootPart.Size = Vector3.new(80, 80, 80)
                                    hum:ChangeState(Enum.HumanoidStateType.RunningNoPhysics)
                                    hrp.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 25, 0)
                                    hrp.AssemblyLinearVelocity = Vector3.zero
                                until not getgenv().AutoFarmAllBoss or not v.Parent or v.Humanoid.Health <= 0
                                StopTweenAndHeartbeat()
                            end
                        end
                    else
                        if RS:FindFirstChild(boss) then
                            local replicatedBoss = RS:FindFirstChild(boss)
                            if replicatedBoss and replicatedBoss:FindFirstChild("HumanoidRootPart") then
                                local tween = TweenToPosition(replicatedBoss.HumanoidRootPart.CFrame * CFrame.new(5, 10, 2))
                                if tween then tween.Completed:Wait() end
                            end
                        end
                    end
                end
            end)
        end
    end
end)

-- Sistema de Ataque
local RA, RH
task.spawn(function()
    task.wait(2)
    pcall(function()
        local M = RS:WaitForChild("Modules", 5)
        if M then
            local N = M:FindFirstChild("Net")
            if N then
                RA = N:FindFirstChild("RE/RegisterAttack")
                RH = N:FindFirstChild("RE/RegisterHit")
            end
        end
    end)
end)

task.spawn(function()
    while task.wait(0.1) do
        if (getgenv().AutoFarmBoss or getgenv().AutoFarmAllBoss) and RA and RH then
            pcall(function()
                local targetBosses = {}
                if getgenv().AutoFarmBoss and getgenv().SelectBoss then
                    table.insert(targetBosses, getgenv().SelectBoss)
                elseif getgenv().AutoFarmAllBoss then
                    targetBosses = tableBoss
                end
                for _, bossName in pairs(targetBosses) do
                    for _, v in pairs(WS.Enemies:GetChildren()) do
                        if v.Name == bossName and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Head") and v.Humanoid.Health > 0 then
                            local targets = {{v, v.Head}}
                            RA:FireServer(0.1)
                            RH:FireServer(v.Head, targets)
                            break
                        end
                    end
                end
            end)
        end
    end
end)
-- ============================================
-- SEÇÃO DE CHEST FARM (Tab Stack Farming)
-- ============================================

TabEF:AddSection("Chest Farm")

-- Variáveis globais para Chest
getgenv().AutoChest = false
getgenv().HopChest = false
getgenv().ChestLimit = 10
getgenv().ChestCollected = 0
getgenv().IgnoredChests = {} -- Blacklist de baús já tentados

-- Input para definir quantidade de baús
local ChestInput = TabEF:AddInput("ChestValue", {
    Title = "Select Value Chest",
    Default = "10",
    Placeholder = "Digite o número de baús",
    Numeric = true,
    Callback = function(value)
        local num = tonumber(value)
        if num and num > 0 then
            getgenv().ChestLimit = math.floor(num)
        end
    end
})

-- Toggle Auto Chest
local TG_AutoChest = TabEF:AddToggle("AutoChest", {
    Title = "Auto Chest",
    Default = false
})

TG_AutoChest:OnChanged(function(v)
    getgenv().AutoChest = v
    if v then
        getgenv().ChestCollected = 0
        getgenv().IgnoredChests = {} -- Limpar blacklist ao iniciar
    else
        SAT() -- Parar todos os tweens ativos
        RNP() -- Resetar física do personagem
    end
end)

-- Toggle Hop Chest
local TG_HopChest = TabEF:AddToggle("HopChest", {
    Title = "Hop Chest",
    Default = false
})

TG_HopChest:OnChanged(function(v)
    getgenv().HopChest = v
end)

-- Função para buscar baús no Workspace (COM BLACKLIST)
local function GetChests()
    local chests = {}

    for _, obj in pairs(workspace:GetDescendants()) do
        if obj:IsA("Model") and obj.Name:lower():find("chest") then
            -- Verificar se o chest NÃO está na blacklist
            if not getgenv().IgnoredChests[obj] then
                if obj:FindFirstChild("TouchInterest", true)
                or obj:FindFirstChildOfClass("ClickDetector", true)
                or obj:FindFirstChildOfClass("ProximityPrompt", true) then
                    table.insert(chests, obj)
                end
            end
        end
    end

    return chests
end

-- Função para obter a posição do baú (CFrame)
local function GetChestPosition(chest)
    if chest:IsA("BasePart") then
        return chest.CFrame
    elseif chest:IsA("Model") then
        -- Tentar pegar o PrimaryPart primeiro
        if chest.PrimaryPart then
            return chest.PrimaryPart.CFrame
        end
        -- Se não tiver, pegar qualquer BasePart
        local part = chest:FindFirstChildWhichIsA("BasePart")
        if part then
            return part.CFrame
        end
    end
    return nil
end

-- Loop de Auto Chest
task.spawn(function()
    while task.wait(0.1) do
        if getgenv().AutoChest then
            pcall(function()
                -- Verificar se atingiu o limite
                if getgenv().ChestCollected >= getgenv().ChestLimit then
                    getgenv().AutoChest = false
                    TG_AutoChest:SetValue(false)
                    SAT()
                    RNP()
                    
                    -- Se Hop Chest estiver ativado
                    if getgenv().HopChest then
                        Fl:Notify({
                            Title = "Chest Farm",
                            Content = "Hop Chest em 5s...",
                            Duration = 5
                        })
                        
                        task.wait(5)
                        
                        -- Hop para outro servidor
                        local TeleportService = game:GetService("TeleportService")
                        TeleportService:Teleport(game.PlaceId, Plr)
                    end
                    
                    return
                end
                
                local char = Plr.Character
                local hrp = char and char:FindFirstChild("HumanoidRootPart")
                local hum = char and char:FindFirstChild("Humanoid")
                
                if not char or not hrp or not hum or hum.Health <= 0 then return end
                
                -- Buscar chests no Workspace (já filtra pela blacklist)
                local chests = GetChests()
                
                if #chests > 0 then
                    local nearestChest = nil
                    local nearestDistance = math.huge
                    
                    -- Encontrar o baú mais próximo
                    for _, chest in pairs(chests) do
                        local chestCFrame = GetChestPosition(chest)
                        
                        if chestCFrame then
                            local distance = (hrp.Position - chestCFrame.Position).Magnitude
                            
                            if distance < nearestDistance then
                                nearestDistance = distance
                                nearestChest = chest
                            end
                        end
                    end
                    
                    if nearestChest then
                        local chestCFrame = GetChestPosition(nearestChest)
                        
                        if chestCFrame then
                            -- Guardar referência do baú antes de ir até ele
                            local chestReference = nearestChest
                            
                            -- Ativar NoClip
                            SNL(char, true)
                            hum:ChangeState(Enum.HumanoidStateType.RunningNoPhysics)
                            
                            -- Usar TTG (Tween sem tremor) para ir direto até o baú
                            TTG(hrp, chestCFrame, 300)
                            
                            -- Aguardar para coletar o baú
                            task.wait(1)
                            
                            -- ADICIONAR O BAÚ NA BLACKLIST IMEDIATAMENTE
                            getgenv().IgnoredChests[chestReference] = true
                            
                            -- Incrementar contador (independente se foi destruído ou não)
                            getgenv().ChestCollected = getgenv().ChestCollected + 1
                        end
                    end
                else
                    -- Não há mais baús disponíveis no mapa
                    if getgenv().ChestCollected >= getgenv().ChestLimit then
                        getgenv().AutoChest = false
                        TG_AutoChest:SetValue(false)
                        SAT()
                        RNP()
                        
                        if getgenv().HopChest then
                            Fl:Notify({
                                Title = "Chest Farm",
                                Content = "Hop Chest em 5s...",
                                Duration = 5
                            })
                            
                            task.wait(5)
                            
                            local TeleportService = game:GetService("TeleportService")
                            TeleportService:Teleport(game.PlaceId, Plr)
                        end
                    else
                        task.wait(5) -- Aguarda 5 segundos antes de verificar novamente
                    end
                end
            end)
        end
    end
end)

-- ============================================
-- MÓDULO DE ILHAS (Tab Local Player)
-- ============================================

TabLP:AddSection("Tab Island")

-- Tabela de ilhas por Sea
local IslandsBySea = {
    [1] = { -- Sea 1
        "StartingArea",
        "Jungle",
        "Pirate Village",
        "Desert",
        "Frozen Village",
        "MarineFord",
        "Colosseum",
        "Sky Island 1",
        "Sky Island 2",
        "Sky Island 3",
        "Prison",
        "Magma Village",
        "Under Water Island",
        "Upper Skylands",
        "Fountain City"
    },
    [2] = { -- Sea 2
        "Kingdom of Rose",
        "Cafe",
        "Mansion",
        "Graveyard",
        "Snow Mountain",
        "Hot and Cold",
        "Cursed Ship",
        "Ice Castle",
        "Forgotten Island",
        "Dark Arena",
        "Green Zone",
        "Swan Room"
    },
    [3] = { -- Sea 3
        "Port Town",
        "Hydra Island",
        "Great Tree",
        "Castle On The Sea",
        "Floating Turtle",
        "Haunted Castle",
        "Sea of Treats",
        "Tiki Outpost"
    }
}

-- Coordenadas das ilhas
local IslandPositions = {
    -- Sea 1
    ["StartingArea"] = CFrame.new(1071.2, 16.3, 1426.86),
    ["Jungle"] = CFrame.new(-1192.07, 50, -51.23),
    ["Pirate Village"] = CFrame.new(-1147, 4.8, 3833.5),
    ["Desert"] = CFrame.new(944.15, 6.4, 4373.3),
    ["Frozen Village"] = CFrame.new(1253, 88.3, -1344.6),
    ["MarineFord"] = CFrame.new(-4914.8, 50.4, 4281.7),
    ["Colosseum"] = CFrame.new(-1427.6, 7.3, -2792.6),
    ["Sky Island 1"] = CFrame.new(-4970.21, 717.7, -2622.35),
    ["Sky Island 2"] = CFrame.new(-7894.6, 5547.5, -380.29),
    ["Sky Island 3"] = CFrame.new(-7894.6, 5547.5, -380.29),
    ["Prison"] = CFrame.new(4854.16, 5.7, 734.85),
    ["Magma Village"] = CFrame.new(-5247.7, 12.8, 8504.6),
    ["Under Water Island"] = CFrame.new(61163.8, 11.6, 1819.7),
    ["Upper Skylands"] = CFrame.new(-7894.6, 5547.5, -380.29),
    ["Fountain City"] = CFrame.new(5127.1, 59.1, 4105.07),
    
    -- Sea 2
    ["Kingdom of Rose"] = CFrame.new(-246.7, 38.4, 5373.8),
    ["Cafe"] = CFrame.new(-387.6, 73.1, 298.9),
    ["Mansion"] = CFrame.new(-12550.5, 337.2, -7449.6),
    ["Graveyard"] = CFrame.new(-5320.9, 47.3, -2496.5),
    ["Snow Mountain"] = CFrame.new(753.7, 408.2, -5274.6),
    ["Hot and Cold"] = CFrame.new(-6063.9, 15.3, -5127.2),
    ["Cursed Ship"] = CFrame.new(923.2, 125.9, 32852.8),
    ["Ice Castle"] = CFrame.new(5812.6, 88.7, -6184.5),
    ["Forgotten Island"] = CFrame.new(-3053.9, 236.4, -10145.3),
    ["Dark Arena"] = CFrame.new(3686.0, 117.7, -3220.0),
    ["Green Zone"] = CFrame.new(-2448.5, 73.0, -3210.1),
    ["Swan Room"] = CFrame.new(2284.91, 15.2, 905.48),
    
    -- Sea 3
    ["Port Town"] = CFrame.new(-290.7, 6.7, 5343.5),
    ["Hydra Island"] = CFrame.new(5228.8, 604.2, -345.0),
    ["Great Tree"] = CFrame.new(2681.2, 1682.8, -7190.9),
    ["Castle On The Sea"] = CFrame.new(-5075.5, 314.5, -2952.3),
    ["Floating Turtle"] = CFrame.new(-13274.5, 332.0, -7632.1),
    ["Haunted Castle"] = CFrame.new(-9515.7, 172.1, 5613.1),
    ["Sea of Treats"] = CFrame.new(-2077.3, 252.6, -12373.9),
    ["Tiki Outpost"] = CFrame.new(-16542.4, 55.7, 1044.4)
}

-- Variável global para controlar tween de ilha e velocidade
getgenv().TweenToIsland = false
getgenv().SelectedIsland = nil
getgenv().TweenSpeed = 300

-- Função para obter ilhas do Sea atual
local function GetCurrentSeaIslands()
    local currentSea = GetSea()
    return IslandsBySea[currentSea] or {}
end

-- Criar Dropdown com ilhas do Sea atual
local currentIslands = GetCurrentSeaIslands()
local IslandDropdown = TabLP:AddDropdown("IslandSel", {
    Title = "Select Island",
    Values = currentIslands,
    Default = 1
})

IslandDropdown:OnChanged(function(v)
    getgenv().SelectedIsland = v
end)

-- Toggle para ativar Tween to Island
local TG_Island = TabLP:AddToggle("TweenIsland", {
    Title = "Tween to Island",
    Default = false
})

TG_Island:OnChanged(function(v)
    getgenv().TweenToIsland = v
    
    if v then
        task.spawn(function()
            if not getgenv().SelectedIsland then
                TG_Island:SetValue(false)
                return
            end
            
            local targetCFrame = IslandPositions[getgenv().SelectedIsland]
            if not targetCFrame then
                TG_Island:SetValue(false)
                return
            end
            
            local c = Plr.Character
            local hrp = c and c:FindFirstChild("HumanoidRootPart")
            
            if not c or not hrp then
                TG_Island:SetValue(false)
                return
            end
            
            -- Usar a função TTG existente para teleporte suave com velocidade customizada
            TTG(hrp, targetCFrame, getgenv().TweenSpeed)
            
            -- Desativar após chegar
            task.wait(0.5)
            TG_Island:SetValue(false)
            getgenv().TweenToIsland = false
        end)
    end
end)

-- Slider para velocidade do Tween (de 10 em 10)
local VelocitySlider = TabLP:AddSlider("TweenVelocity", {
    Title = "Select Velocity Tween",
    Default = 300,
    Min = 50,
    Max = 350,
    Rounding = 0
})

VelocitySlider:OnChanged(function(value)
    -- Arredondar para o múltiplo de 10 mais próximo
    local roundedValue = math.floor(value / 10 + 0.5) * 10
    
    -- Garantir que está dentro dos limites
    roundedValue = math.max(50, math.min(350, roundedValue))
    
    getgenv().TweenSpeed = roundedValue
    
    -- Atualizar o slider para o valor arredondado
    if roundedValue ~= value then
        VelocitySlider:SetValue(roundedValue)
    end
end)

-- Atualizar dropdown quando mudar de Sea
task.spawn(function()
    local lastSea = GetSea()
    while task.wait(5) do
        local currentSea = GetSea()
        if currentSea ~= lastSea then
            lastSea = currentSea
            -- Atualizar as ilhas no dropdown
            local newIslands = GetCurrentSeaIslands()
            -- Recriar o dropdown com as novas ilhas
            IslandDropdown:SetValues(newIslands)
            getgenv().SelectedIsland = newIslands[1]
        end
    end
end)

-- ============================================
-- SEÇÃO DE MUDANÇA DE TIME
-- ============================================

TabLP:AddSection("Tab Time")

-- Variáveis para controle de time
getgenv().SelectedTeam = "Pirata"

-- Função para verificar o time atual do jogador
local function GetCurrentTeam()
    local playerTeam = Plr.Team
    if playerTeam then
        return playerTeam.Name
    end
    return nil
end

-- Dropdown para selecionar time
local TeamDropdown = TabLP:AddDropdown("TeamSel", {
    Title = "Select Time",
    Values = {"Pirata", "Marine"},
    Default = 1
})

TeamDropdown:OnChanged(function(v)
    getgenv().SelectedTeam = v
end)

-- Toggle para mudar de time
local TG_ChangeTeam = TabLP:AddToggle("ChangeTeam", {
    Title = "Change Time",
    Default = false
})

TG_ChangeTeam:OnChanged(function(v)
    if v then
        task.spawn(function()
            local currentTeam = GetCurrentTeam()
            local selectedTeam = getgenv().SelectedTeam
            
            -- Verificar se já está no time selecionado
            if (selectedTeam == "Pirata" and currentTeam == "Pirates") or 
               (selectedTeam == "Marine" and currentTeam == "Marines") then
                TG_ChangeTeam:SetValue(false)
                return
            end
            
            -- Determinar qual NPC usar
            local npcName = selectedTeam == "Pirata" and "Pirate Recruiter" or "Marine Recruiter"
            
            -- Buscar o NPC no workspace
            local npc = workspace:FindFirstChild(npcName, true)
            
            if npc then
                -- Tentar encontrar o RemoteEvent relacionado ao NPC
                local args = {
                    [1] = npcName
                }
                
                -- Procurar pelo RemoteEvent correto no ReplicatedStorage
                local ReplicatedStorage = game:GetService("ReplicatedStorage")
                local remotes = ReplicatedStorage:GetDescendants()
                
                for _, remote in pairs(remotes) do
                    if remote:IsA("RemoteEvent") and (remote.Name == "SetTeam" or remote.Name == "ChangeTeam" or remote.Name:find("Team")) then
                        pcall(function()
                            remote:FireServer(unpack(args))
                        end)
                    end
                end
                
                -- Aguardar um pouco para a mudança acontecer
                task.wait(1)
            end
            
            -- Desativar o toggle
            TG_ChangeTeam:SetValue(false)
        end)
    end
end)
-- ============================================
-- MÓDULO COMPLETO: Bones, Refund & Cake Prince
-- ============================================

-- Criar Tab Quest & Itens
local TabQI = Win:AddTab({Title="Tab Quest & Itens",Icon="package"})
TabQI:AddSection("Items & Random")

-- Auto Bone Surprise
local AutoRandomBones = false

local ToggleRandomBones = TabQI:AddToggle("RandomBones", {
    Title = "Auto Bone Surprise",
    Description = "Reroll Bone And Surprise",
    Default = false
})

ToggleRandomBones:OnChanged(function(v)
    AutoRandomBones = v
end)

task.spawn(function()
    while task.wait(0.5) do
        if AutoRandomBones and World3 then
            pcall(function()
                RS.Remotes.CommF_:InvokeServer("Bones", "Buy", 1, 1)
            end)
        end
    end
end)

-- Adicionar Others na Tab Shop
TabS:AddSection("Others")

TabS:AddButton({
    Title = "Buy Refund Status",
    Callback = function()
        if World1 then return end
        pcall(function() CF:InvokeServer("BlackbeardReward", "Refund", "1") end)
        task.wait(0.1)
        pcall(function() CF:InvokeServer("BlackbeardReward", "Refund", "2") end)
        task.wait(0.1)
        pcall(function() CF:InvokeServer("Refund") end)
        task.wait(0.1)
        pcall(function() CF:InvokeServer("RefundStats") end)
    end
})

-- ============================================
-- SISTEMA CAKE PRINCE
-- ============================================
getgenv().FarmingCakePrince = false

local function IsCakePrinceAlive()
    local boss = WS.Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]")
    return boss and boss:FindFirstChild("Humanoid") and boss:FindFirstChild("HumanoidRootPart") and boss.Humanoid.Health > 0
end

local function GetCakePrinceBoss()
    if not IsCakePrinceAlive() then return nil end
    return WS.Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]")
end

local function StartCakePrinceFarm()
    if getgenv().FarmingCakePrince then return end
    getgenv().FarmingCakePrince = true
    
    task.spawn(function()
        while getgenv().AK and IsCakePrinceAlive() and getgenv().FarmingCakePrince do
            pcall(function()
                local boss = GetCakePrinceBoss()
                if not boss then 
                    getgenv().FarmingCakePrince = false
                    return 
                end
                
                local c = Plr.Character
                if not c then return end
                
                local hrp = c:FindFirstChild("HumanoidRootPart")
                local hum = c:FindFirstChild("Humanoid")
                
                if not hrp or not hum or hum.Health <= 0 then return end
                
                -- Equipar arma
                if getgenv().WP == "Sword" then
                    for _, v in ipairs(Plr.Backpack:GetChildren()) do
                        if v:IsA("Tool") and v.ToolTip == "Sword" then
                            EquipWeapon(v.Name)
                            break
                        end
                    end
                elseif getgenv().WP == "Melee" then
                    for _, v in ipairs(Plr.Backpack:GetChildren()) do
                        if v:IsA("Tool") and v.ToolTip == "Melee" then
                            EquipWeapon(v.Name)
                            break
                        end
                    end
                end
                
                local bossHRP = boss:FindFirstChild("HumanoidRootPart")
                if not bossHRP then return end
                
                -- Desabilitar colisão do personagem
                for _, part in ipairs(c:GetDescendants()) do
                    if part:IsA("BasePart") then
                        part.CanCollide = false
                    end
                end
                
                hum:ChangeState(Enum.HumanoidStateType.RunningNoPhysics)
                
                -- Posicionar perto do boss
                local targetCF = bossHRP.CFrame * CFrame.new(0, 25, 0)
                hrp.CFrame = targetCF
                hrp.AssemblyLinearVelocity = Vector3.zero
                
                -- Bring boss
                if getgenv().BM then
                    local canBring = true
                    if isnetworkowner then
                        canBring = isnetworkowner(bossHRP)
                    else
                        canBring = (bossHRP.Position - hrp.Position).Magnitude <= 350
                    end
                    
                    if canBring then
                        bossHRP.CFrame = targetCF * CFrame.new(0, -25, 0)
                        bossHRP.CanCollide = false
                        bossHRP.Size = Vector3.new(50, 50, 50)
                        
                        if boss:FindFirstChild("Head") then
                            boss.Head.CanCollide = false
                        end
                        
                        boss.Humanoid.WalkSpeed = 0
                        boss.Humanoid.JumpPower = 0
                        boss.Humanoid:ChangeState(14)
                        boss.Humanoid:ChangeState(11)
                        
                        if boss.Humanoid:FindFirstChild("Animator") then
                            boss.Humanoid.Animator:Destroy()
                        end
                    end
                end
            end)
            
            task.wait(0.05)
        end
        
        -- Boss morreu
        getgenv().FarmingCakePrince = false
        SAT()
    end)
end

-- Detectar spawn
WS.Enemies.ChildAdded:Connect(function(child)
    if child.Name == "Cake Prince [Lv. 2300] [Raid Boss]" then
        task.wait(1)
        if getgenv().AK and IsCakePrinceAlive() and not getgenv().FarmingCakePrince then
            SAT()
            task.wait(0.5)
            StartCakePrinceFarm()
        end
    end
end)

-- Detectar morte
WS.Enemies.ChildRemoved:Connect(function(child)
    if child.Name == "Cake Prince [Lv. 2300] [Raid Boss]" then
        getgenv().FarmingCakePrince = false
        SAT()
    end
end)

-- Backup check
task.spawn(function()
    while task.wait(3) do
        if getgenv().AK and not getgenv().FarmingCakePrince and IsCakePrinceAlive() then
            SAT()
            task.wait(0.5)
            StartCakePrinceFarm()
        end
    end
end)

-- ============================================
-- SUBSTITUIR LOOP PRINCIPAL
-- ============================================
-- Encontre e DELETE o loop principal antigo (task.spawn(function() while task.wait(0.15)...)
-- E SUBSTITUA por este:

task.spawn(function()
while task.wait(0.15) do
    pcall(function()
        if not IFA() then return end
        
        -- ✅ PARAR SE ESTIVER FARMANDO CAKE PRINCE
        if getgenv().FarmingCakePrince then return end
        
        local c = Plr.Character
        if not c then return end
        
        local hrp, hum = c:FindFirstChild("HumanoidRootPart"), c:FindFirstChild("Humanoid")
        
        if not hrp or not hum or hum.Health <= 0 then
            if hum and hum.Health <= 0 then
                SAT()
                repeat task.wait() until Plr.Character and Plr.Character:FindFirstChild("HumanoidRootPart") and Plr.Character:FindFirstChild("Humanoid") and Plr.Character.Humanoid.Health > 0
                task.wait(1)
            end
            return
        end
        
        if getgenv().AF then
            local q = GQ()
            if not q then return end
            
            local qN, qL, mn, msCF = q.N or q.NameQuest, q.L or q.LevelQuest, q.M or q.Mon, q.SC or q.CFrameMon
            local qCF = q.C or q.CFrameQuest or CFrame.new(msCF.Position.X, msCF.Position.Y > 0 and msCF.Position.Y or 50, msCF.Position.Z)
            
            if getgenv().CurrentQuestName ~= qN or getgenv().CurrentQuestLevel ~= qL then
                CQ()
                getgenv().CurrentQuestName, getgenv().CurrentQuestLevel = nil, nil
                SAT()
                task.wait(0.5)
            end
            
            if not HQ() then
                if not TryGetQuest(qN, qL, qCF) then return end
            end
            
            local fMob = FMS(mn)
            if fMob then
                PM(c, hrp, hum, fMob, mn)
            else
                SAT()
                TTG(hrp, CFrame.new(msCF.Position.X, msCF.Position.Y > 0 and msCF.Position.Y or 50, msCF.Position.Z), 250)
                task.wait(0.5)
            end
            
        elseif getgenv().AK then
            -- ✅ VERIFICAÇÃO DUPLA ANTES DE FARMAR MOBS
            if getgenv().FarmingCakePrince then return end
            HMR(KM, "KataIndex", KS)
            
        elseif getgenv().AB then
            HMR(BonM, "BoneIndex", BS)
        end
    end)
end
end)
