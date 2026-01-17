-- QuestIlha.lua  (RODAR PRIMEIRO, arquivo separado)

local QuestIlha = {}

QuestIlha.QuestData = {
    [1] = {NameQuest = "BanditQuest1", LevelQuest = 1, Mon = "Bandit", CFrameQuest = CFrame.new(1059.37,16.5,1549.99), CFrameMon = CFrame.new(1045,17,1560)},
    [10] = {NameQuest = "JungleQuest", LevelQuest = 1, Mon = "Monkey", CFrameQuest = CFrame.new(-1598.08911, 35.5501175, 153.377838), CFrameMon = CFrame.new(-1448.51806640625, 67.85301208496094, 11.46579647064209)},
    [15] = {NameQuest = "JungleQuest", LevelQuest = 2, Mon = "Gorilla", CFrameQuest = CFrame.new(-1598.08911, 35.5501175, 153.377838), CFrameMon = CFrame.new(-1129.8836669921875, 40.46354675292969, -525.4237060546875)},
    [30] = {NameQuest = "BuggyQuest1", LevelQuest = 1, Mon = "Pirate", CFrameQuest = CFrame.new(-1141.07483, 4.10001802, 3831.5498), CFrameMon = CFrame.new(-1103.513427734375, 13.752052307128906, 3896.091064453125)},
    [40] = {NameQuest = "BuggyQuest1", LevelQuest = 2, Mon = "Brute", CFrameQuest = CFrame.new(-1141.07483, 4.10001802, 3831.5498), CFrameMon = CFrame.new(-1140.083740234375, 14.809885025024414, 4322.92138671875)},
    [60] = {NameQuest = "DesertQuest", LevelQuest = 1, Mon = "Desert Bandit", CFrameQuest = CFrame.new(894.488647, 5.14000702, 4392.43359), CFrameMon = CFrame.new(924.7998046875, 6.44867467880249, 4481.5859375)},
    [75] = {NameQuest = "DesertQuest", LevelQuest = 2, Mon = "Desert Officer", CFrameQuest = CFrame.new(894.488647, 5.14000702, 4392.43359), CFrameMon = CFrame.new(1608.2822265625, 8.614224433898926, 4371.00732421875)},
    [90] = {NameQuest = "SnowQuest", LevelQuest = 1, Mon = "Snow Bandit", CFrameQuest = CFrame.new(1389.74451, 88.1519318, -1298.90796), CFrameMon = CFrame.new(1354.347900390625, 87.27277374267578, -1393.946533203125)},
    [100] = {NameQuest = "SnowQuest", LevelQuest = 2, Mon = "Snowman", CFrameQuest = CFrame.new(1389.74451, 88.1519318, -1298.90796), CFrameMon = CFrame.new(1201.6412353515625, 144.57958984375, -1550.0670166015625)},
    [120] = {NameQuest = "MarineQuest2", LevelQuest = 1, Mon = "Chief Petty Officer", CFrameQuest = CFrame.new(-5039.58643, 27.3500385, 4324.68018), CFrameMon = CFrame.new(-4881.23095703125, 22.65204429626465, 4273.75244140625)},
    [150] = {NameQuest = "SkyQuest", LevelQuest = 1, Mon = "Sky Bandit", CFrameQuest = CFrame.new(-4839.53027, 716.368591, -2619.44165), CFrameMon = CFrame.new(-4953.20703125, 295.74420166015625, -2899.22900390625)},
    [175] = {NameQuest = "SkyQuest", LevelQuest = 2, Mon = "Dark Master", CFrameQuest = CFrame.new(-4839.53027, 716.368591, -2619.44165), CFrameMon = CFrame.new(-5259.8447265625, 391.3976745605469, -2229.035400390625)},
    [190] = {NameQuest = "PrisonerQuest", LevelQuest = 1, Mon = "Prisoner", CFrameQuest = CFrame.new(5308.93115, 1.65517521, 475.120514), CFrameMon = CFrame.new(5098.9736328125, -0.3204058110713959, 474.2373352050781)},
    [210] = {NameQuest = "PrisonerQuest", LevelQuest = 2, Mon = "Dangerous Prisoner", CFrameQuest = CFrame.new(5308.93115, 1.65517521, 475.120514), CFrameMon = CFrame.new(5654.5634765625, 15.633401870727539, 866.2991943359375)},
    [250] = {NameQuest = "ColosseumQuest", LevelQuest = 1, Mon = "Toga Warrior", CFrameQuest = CFrame.new(-1580.04663, 6.35000277, -2986.47534), CFrameMon = CFrame.new(-1820.21484375, 51.68385696411133, -2740.6650390625)},
    [275] = {NameQuest = "ColosseumQuest", LevelQuest = 2, Mon = "Gladiator", CFrameQuest = CFrame.new(-1580.04663, 6.35000277, -2986.47534), CFrameMon = CFrame.new(-1292.838134765625, 56.380882263183594, -3339.031494140625)},
    [300] = {NameQuest = "MagmaQuest", LevelQuest = 1, Mon = "Military Soldier", CFrameQuest = CFrame.new(-5313.37012, 10.9500084, 8515.29395), CFrameMon = CFrame.new(-5411.16455078125, 11.081554412841797, 8454.29296875)},
    [325] = {NameQuest = "MagmaQuest", LevelQuest = 2, Mon = "Military Spy", CFrameQuest = CFrame.new(-5313.37012, 10.9500084, 8515.29395), CFrameMon = CFrame.new(-5802.8681640625, 86.26241302490234, 8828.859375)},
    [375] = {NameQuest = "FishmanQuest", LevelQuest = 1, Mon = "Fishman Warrior", CFrameQuest = CFrame.new(61122.65234375, 18.497442245483, 1569.3997802734), CFrameMon = CFrame.new(60878.30078125, 18.482830047607422, 1543.7574462890625)},
    [400] = {NameQuest = "FishmanQuest", LevelQuest = 2, Mon = "Fishman Commando", CFrameQuest = CFrame.new(61122.65234375, 18.497442245483, 1569.3997802734), CFrameMon = CFrame.new(61922.6328125, 18.482830047607422, 1493.934326171875)},
    [450] = {NameQuest = "SkyExp1Quest", LevelQuest = 1, Mon = "Guarda de Deus", CFrameQuest = CFrame.new(-4721.88867, 843.874695, -1949.96643), CFrameMon = CFrame.new(-4710.04296875, 845.2769775390625, -1927.3079833984375)},
    [475] = {NameQuest = "SkyExp1Quest", LevelQuest = 2, Mon = "Shanda", CFrameQuest = CFrame.new(-7859.09814, 5544.19043, -381.476196), CFrameMon = CFrame.new(-7678.48974609375, 5566.40380859375, -497.2156066894531)},
    [525] = {NameQuest = "SkyExp2Quest", LevelQuest = 1, Mon = "Royal Squad", CFrameQuest = CFrame.new(-7906.81592, 5634.6626, -1411.99194), CFrameMon = CFrame.new(-7624.25244140625, 5658.13330078125, -1467.354248046875)},
    [550] = {NameQuest = "SkyExp2Quest", LevelQuest = 2, Mon = "Royal Soldier", CFrameQuest = CFrame.new(-7906.81592, 5634.6626, -1411.99194), CFrameMon = CFrame.new(-7836.75341796875, 5645.6640625, -1790.6236572265625)},
    [625] = {NameQuest = "FountainQuest", LevelQuest = 1, Mon = "Galley Pirate", CFrameQuest = CFrame.new(5259.81982, 37.3500175, 4050.0293), CFrameMon = CFrame.new(5551.02197265625, 78.90135192871094, 3930.412841796875)},
    [650] = {NameQuest = "FountainQuest", LevelQuest = 2, Mon = "Galley Captain", CFrameQuest = CFrame.new(5259.81982, 37.3500175, 4050.0293), CFrameMon = CFrame.new(5441.95166015625, 42.50205993652344, 4950.09375)},
    [700] = {NameQuest = "Area1Quest", LevelQuest = 1, Mon = "Raider", CFrameQuest = CFrame.new(-429.543518, 71.7699966, 1836.18188), CFrameMon = CFrame.new(-728.3267211914062, 52.779319763183594, 2345.7705078125)},
    [725] = {NameQuest = "Area1Quest", LevelQuest = 2, Mon = "Mercenary", CFrameQuest = CFrame.new(-429.543518, 71.7699966, 1836.18188), CFrameMon = CFrame.new(-1004.3244018554688, 80.15886688232422, 1424.619384765625)},
    [775] = {NameQuest = "Area2Quest", LevelQuest = 1, Mon = "Swan Pirate", CFrameQuest = CFrame.new(638.43811, 71.769989, 918.282898), CFrameMon = CFrame.new(1068.664306640625, 137.61428833007812, 1322.1060791015625)},
    [800] = {NameQuest = "Area2Quest", LevelQuest = 2, Mon = "Factory Staff", CFrameQuest = CFrame.new(632.698608, 73.1055908, 918.666321), CFrameMon = CFrame.new(73.07867431640625, 81.86344146728516, -27.470672607421875)},
    [875] = {NameQuest = "MarineQuest3", LevelQuest = 1, Mon = "Marine Lieutenant", CFrameQuest = CFrame.new(-2440.79639, 71.7140732, -3216.06812), CFrameMon = CFrame.new(-2821.372314453125, 75.89727783203125, -3070.089111328125)},
    [900] = {NameQuest = "MarineQuest3", LevelQuest = 2, Mon = "Marine Captain", CFrameQuest = CFrame.new(-2440.79639, 71.7140732, -3216.06812), CFrameMon = CFrame.new(-1861.2310791015625, 80.17658233642578, -3254.697509765625)},
    [950] = {NameQuest = "ZombieQuest", LevelQuest = 1, Mon = "Zombie", CFrameQuest = CFrame.new(-5497.06152, 47.5923004, -795.237061), CFrameMon = CFrame.new(-5657.77685546875, 78.96973419189453, -928.68701171875)},
    [975] = {NameQuest = "ZombieQuest", LevelQuest = 2, Mon = "Vampire", CFrameQuest = CFrame.new(-5497.06152, 47.5923004, -795.237061), CFrameMon = CFrame.new(-6037.66796875, 32.18463897705078, -1340.6597900390625)},
    [1000] = {NameQuest = "SnowMountainQuest", LevelQuest = 1, Mon = "Snow Trooper", CFrameQuest = CFrame.new(609.858826, 400.119904, -5372.25928), CFrameMon = CFrame.new(549.1473388671875, 427.3870544433594, -5563.69873046875)},
    [1050] = {NameQuest = "SnowMountainQuest", LevelQuest = 2, Mon = "Winter Warrior", CFrameQuest = CFrame.new(609.858826, 400.119904, -5372.25928), CFrameMon = CFrame.new(1142.7451171875, 475.6398010253906, -5199.41650390625)},
    [1100] = {NameQuest = "IceSideQuest", LevelQuest = 1, Mon = "Lab Subordinate", CFrameQuest = CFrame.new(-6064.06885, 15.2422857, -4902.97852), CFrameMon = CFrame.new(-5707.4716796875, 15.951709747314453, -4513.39208984375)},
    [1125] = {NameQuest = "IceSideQuest", LevelQuest = 2, Mon = "Horned Warrior", CFrameQuest = CFrame.new(-6064.06885, 15.2422857, -4902.97852), CFrameMon = CFrame.new(-6341.36669921875, 15.951770782470703, -5723.162109375)},
    [1175] = {NameQuest = "FireSideQuest", LevelQuest = 1, Mon = "Magma Ninja", CFrameQuest = CFrame.new(-5428.03174, 15.0622921, -5299.43457), CFrameMon = CFrame.new(-5449.6728515625, 76.65874481201172, -5808.20068359375)},
    [1200] = {NameQuest = "FireSideQuest", LevelQuest = 2, Mon = "Lava Pirate", CFrameQuest = CFrame.new(-5428.03174, 15.0622921, -5299.43457), CFrameMon = CFrame.new(-5213.33154296875, 49.73788070678711, -4701.451171875)},
    [1250] = {NameQuest = "ShipQuest1", LevelQuest = 1, Mon = "Ship Deckhand", CFrameQuest = CFrame.new(1037.80127, 125.092171, 32911.6016), CFrameMon = CFrame.new(1212.0111083984375, 150.79205322265625, 33059.24609375)},
    [1275] = {NameQuest = "ShipQuest1", LevelQuest = 2, Mon = "Ship Engineer", CFrameQuest = CFrame.new(1037.80127, 125.092171, 32911.6016), CFrameMon = CFrame.new(919.4786376953125, 43.54401397705078, 32779.96875)},
    [1300] = {NameQuest = "ShipQuest2", LevelQuest = 1, Mon = "Ship Steward", CFrameQuest = CFrame.new(968.80957, 125.092171, 33244.125), CFrameMon = CFrame.new(919.4385375976562, 129.55599975585938, 33436.03515625)},
    [1325] = {NameQuest = "ShipQuest2", LevelQuest = 2, Mon = "Ship Officer", CFrameQuest = CFrame.new(968.80957, 125.092171, 33244.125), CFrameMon = CFrame.new(1036.0179443359375, 181.4390411376953, 33315.7265625)},
    [1350] = {NameQuest = "FrostQuest", LevelQuest = 1, Mon = "Arctic Warrior", CFrameQuest = CFrame.new(5667.6582, 26.7997818, -6486.08984), CFrameMon = CFrame.new(5966.24609375, 62.97002029418945, -6179.3828125)},
    [1375] = {NameQuest = "FrostQuest", LevelQuest = 2, Mon = "Snow Lurker", CFrameQuest = CFrame.new(5667.6582, 26.7997818, -6486.08984), CFrameMon = CFrame.new(5407.07373046875, 69.19437408447266, -6880.88037109375)},
    [1425] = {NameQuest = "ForgottenQuest", LevelQuest = 1, Mon = "Sea Soldier", CFrameQuest = CFrame.new(-3054.44458, 235.544281, -10142.8193), CFrameMon = CFrame.new(-3028.2236328125, 64.67451477050781, -9775.4267578125)},
    [1450] = {NameQuest = "ForgottenQuest", LevelQuest = 2, Mon = "Water Fighter", CFrameQuest = CFrame.new(-3054.44458, 235.544281, -10142.8193), CFrameMon = CFrame.new(-3352.9013671875, 285.01556396484375, -10534.841796875)},
    [1500] = {NameQuest = "PiratePortQuest", LevelQuest = 1, Mon = "Pirate Millionaire", CFrameQuest = CFrame.new(-290.074677, 42.9034653, 5581.58984), CFrameMon = CFrame.new(-245.9963836669922, 47.30615234375, 5584.1005859375)},
    [1525] = {NameQuest = "PiratePortQuest", LevelQuest = 2, Mon = "Pistol Billionaire", CFrameQuest = CFrame.new(-290.074677, 42.9034653, 5581.58984), CFrameMon = CFrame.new(-187.3301544189453, 86.23987579345703, 6013.513671875)},
    [1575] = {NameQuest = "DragonCrewQuest", LevelQuest = 1, Mon = "Dragon Crew Warrior", CFrameQuest = CFrame.new(6737, 127, -713), CFrameMon = CFrame.new(6737, 127, -713)},
    [1600] = {NameQuest = "DragonCrewQuest", LevelQuest = 2, Mon = "Dragon Crew Archer", CFrameQuest = CFrame.new(6737, 127, -713), CFrameMon = CFrame.new(6743, 484, 209)},
    [1625] = {NameQuest = "AmazonQuest2", LevelQuest = 1, Mon = "Female Islander", CFrameQuest = CFrame.new(5446.8793945313, 601.62945556641, 749.45672607422), CFrameMon = CFrame.new(4685.25830078125, 735.8078002929688, 815.3425903320312)},
    [1650] = {NameQuest = "AmazonQuest2", LevelQuest = 2, Mon = "Giant Islander", CFrameQuest = CFrame.new(5446.8793945313, 601.62945556641, 749.45672607422), CFrameMon = CFrame.new(4729.09423828125, 590.436767578125, -36.97627639770508)},
    [1700] = {NameQuest = "MarineTreeIsland", LevelQuest = 1, Mon = "Marine Commodore", CFrameQuest = CFrame.new(2180.54126, 27.8156815, -6741.5498), CFrameMon = CFrame.new(2286.0078125, 73.13391876220703, -7159.80908203125)},
    [1725] = {NameQuest = "MarineTreeIsland", LevelQuest = 2, Mon = "Marine Rear Admiral", CFrameQuest = CFrame.new(2179.98828125, 28.731239318848, -6740.0551757813), CFrameMon = CFrame.new(3656.773681640625, 160.52406311035156, -7001.5986328125)},
    [1775] = {NameQuest = "DeepForestIsland3", LevelQuest = 1, Mon = "Fishman Raider", CFrameQuest = CFrame.new(-10581.6563, 330.872955, -8761.18652), CFrameMon = CFrame.new(-10407.5263671875, 331.76263427734375, -8368.5166015625)},
    [1800] = {NameQuest = "DeepForestIsland3", LevelQuest = 2, Mon = "Capitão Homem-Peixe", CFrameQuest = CFrame.new(-10581.6563, 330.872955, -8761.18652), CFrameMon = CFrame.new(-10994.701171875, 352.38140869140625, -9002.1103515625)},
    [1825] = {NameQuest = "DeepForestIsland", LevelQuest = 1, Mon = "Forest Pirate", CFrameQuest = CFrame.new(-13234.04, 331.488495, -7625.40137), CFrameMon = CFrame.new(-13274.478515625, 332.3781433105469, -7769.58056640625)},
    [1850] = {NameQuest = "DeepForestIsland", LevelQuest = 2, Mon = "Mythological Pirate", CFrameQuest = CFrame.new(-13234.04, 331.488495, -7625.40137), CFrameMon = CFrame.new(-13680.607421875, 501.08154296875, -6991.189453125)},
    [1900] = {NameQuest = "DeepForestIsland2", LevelQuest = 1, Mon = "Jungle Pirate", CFrameQuest = CFrame.new(-12680.3818, 389.971039, -9902.01953), CFrameMon = CFrame.new(-12256.16015625, 331.73828125, -10485.8369140625)},
    [1925] = {NameQuest = "DeepForestIsland2", LevelQuest = 2, Mon = "Pirata Mosqueteiro", CFrameQuest = CFrame.new(-12680.3818, 389.971039, -9902.01953), CFrameMon = CFrame.new(-13457.904296875, 391.545654296875, -9859.177734375)},
    [1975] = {NameQuest = "HauntedQuest1", LevelQuest = 1, Mon = "Reborn Skeleton", CFrameQuest = CFrame.new(-9479.2168, 141.215088, 5566.09277), CFrameMon = CFrame.new(-8763.7236328125, 165.72299194335938, 6159.86181640625)},
    [2000] = {NameQuest = "HauntedQuest1", LevelQuest = 2, Mon = "Living Zombie", CFrameQuest = CFrame.new(-9479.2168, 141.215088, 5566.09277), CFrameMon = CFrame.new(-10144.1318359375, 138.62667846679688, 5838.0888671875)},
    [2025] = {NameQuest = "HauntedQuest2", LevelQuest = 1, Mon = "Demonic Soul", CFrameQuest = CFrame.new(-9516.99316, 172.017181, 6078.46533), CFrameMon = CFrame.new(-9505.8720703125, 172.10482788085938, 6158.9931640625)},
    [2050] = {NameQuest = "HauntedQuest2", LevelQuest = 2, Mon = "Posessed Mummy", CFrameQuest = CFrame.new(-9516.99316, 172.017181, 6078.46533), CFrameMon = CFrame.new(-9582.0224609375, 6.251527309417725, 6205.478515625)},
    [2075] = {NameQuest = "NutsIslandQuest", LevelQuest = 1, Mon = "Peanut Scout", CFrameQuest = CFrame.new(-2104.3908691406, 38.104167938232, -10194.21875), CFrameMon = CFrame.new(-2143.241943359375, 47.72198486328125, -10029.9951171875)},
    [2100] = {NameQuest = "NutsIslandQuest", LevelQuest = 2, Mon = "Peanut President", CFrameQuest = CFrame.new(-2104.3908691406, 38.104167938232, -10194.21875), CFrameMon = CFrame.new(-1859.35400390625, 38.10316848754883, -10422.4296875)},
    [2125] = {NameQuest = "IceCreamIslandQuest", LevelQuest = 1, Mon = "Ice Cream Chef", CFrameQuest = CFrame.new(-820.64825439453, 65.819526672363, -10965.795898438), CFrameMon = CFrame.new(-872.24658203125, 65.81957244873047, -10919.95703125)},
    [2150] = {NameQuest = "IceCreamIslandQuest", LevelQuest = 2, Mon = "Ice Cream Commander", CFrameQuest = CFrame.new(-820.64825439453, 65.819526672363, -10965.795898438), CFrameMon = CFrame.new(-558.06103515625, 112.04895782470703, -11290.7744140625)},
    [2200] = {NameQuest = "CakeQuest1", LevelQuest = 1, Mon = "Cookie Crafter", CFrameQuest = CFrame.new(-2021.32007, 37.7982254, -12028.7295), CFrameMon = CFrame.new(-2374.13671875, 37.79826354980469, -12125.30859375)},
    [2225] = {NameQuest = "CakeQuest1", LevelQuest = 2, Mon = "Cake Guard", CFrameQuest = CFrame.new(-2021.32007, 37.7982254, -12028.7295), CFrameMon = CFrame.new(-1598.3070068359375, 43.773197174072266, -12244.5810546875)},
    [2250] = {NameQuest = "CakeQuest2", LevelQuest = 1, Mon = "Equipe de Confeitaria", CFrameQuest = CFrame.new(-1927.91602, 37.7981339, -12842.5391), CFrameMon = CFrame.new(-1887.8099365234375, 77.6185073852539, -12998.3505859375)},
    [2275] = {NameQuest = "CakeQuest2", LevelQuest = 2, Mon = "Head Baker", CFrameQuest = CFrame.new(-1927.91602, 37.7981339, -12842.5391), CFrameMon = CFrame.new(-2216.188232421875, 82.884521484375, -12869.2939453125)},
    [2300] = {NameQuest = "ChocQuest1", LevelQuest = 1, Mon = "Guerreiro de Cacau", CFrameQuest = CFrame.new(233.22836303710938, 29.876001358032227, -12201.2333984375), CFrameMon = CFrame.new(-21.55328369140625, 80.57499694824219, -12352.3876953125)},
    [2325] = {NameQuest = "ChocQuest1", LevelQuest = 2, Mon = "Chocolate Bar Battler", CFrameQuest = CFrame.new(233.22836303710938, 29.876001358032227, -12201.2333984375), CFrameMon = CFrame.new(582.590576171875, 77.18809509277344, -12463.162109375)},
    [2350] = {NameQuest = "ChocQuest2", LevelQuest = 1, Mon = "Sweet Thief", CFrameQuest = CFrame.new(150.5066375732422, 30.693693161010742, -12774.5029296875), CFrameMon = CFrame.new(165.1884765625, 76.05885314941406, -12600.8369140625)},
    [2375] = {NameQuest = "ChocQuest2", LevelQuest = 2, Mon = "Candy Rebel", CFrameQuest = CFrame.new(150.5066375732422, 30.693693161010742, -12774.5029296875), CFrameMon = CFrame.new(134.86563110351562, 77.2476806640625, -12876.5478515625)},
    [2400] = {NameQuest = "CandyQuest1", LevelQuest = 1, Mon = "Candy Pirate", CFrameQuest = CFrame.new(-1150.0400390625, 20.378934860229492, -14446.3349609375), CFrameMon = CFrame.new(-1310.5003662109375, 26.016523361206055, -14562.404296875)},
    [2425] = {NameQuest = "CandyQuest1", LevelQuest = 2, Mon = "Snow Demon", CFrameQuest = CFrame.new(-1150.0400390625, 20.378934860229492, -14446.3349609375), CFrameMon = CFrame.new(-880.2006225585938, 71.24776458740234, -14538.609375)},
    [2450] = {NameQuest = "TikiQuest1", LevelQuest = 1, Mon = "Isle Outlaw", CFrameQuest = CFrame.new(-16545.9355, 55.6863556, -173.230499), CFrameMon = CFrame.new(-16120.6035, 116.520554, -103.038849)},
    [2475] = {NameQuest = "TikiQuest1", LevelQuest = 2, Mon = "Island Boy", CFrameQuest = CFrame.new(-16545.9355, 55.6863556, -173.230499), CFrameMon = CFrame.new(-16751.3125, 121.226219, -264.015015)},
    [2500] = {NameQuest = "TikiQuest2", LevelQuest = 1, Mon = "Guerreiro Beijado pelo Sol", CFrameQuest = CFrame.new(-16539.078125, 55.68632888793945, 1051.5738525390625), CFrameMon = CFrame.new(-16294.6748, 32.7874393, 1062.4856)},
    [2525] = {NameQuest = "TikiQuest2", LevelQuest = 2, Mon = "Isle Champion", CFrameQuest = CFrame.new(-16539.078125, 55.68632888793945, 1051.5738525390625), CFrameMon = CFrame.new(-16933.2129, 93.3503036, 999.450989)}
}

function QuestIlha.GetQuestForLevel(level)
    local selected, highest = nil, 0
    for req, data in pairs(QuestIlha.QuestData) do
        if level >= req and req > highest then
            highest = req
            selected = data
        end
    end
    return selected
end

-- expõe o módulo globalmente pra outros scripts do executor
getgenv().QuestIlha = QuestIlha
-- CONFIG
local PIRATE = true
local MARINE = false

local RS = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")
local LP = Players.LocalPlayer

repeat task.wait() until RS:FindFirstChild("Remotes")
repeat task.wait() until RS.Remotes:FindFirstChild("CommF_")

if not LP.Team then
    task.wait(3)
    if PIRATE then RS.Remotes.CommF_:InvokeServer("SetTeam", "Pirates")
    elseif MARINE then RS.Remotes.CommF_:InvokeServer("SetTeam", "Marines") end
end

wait(1)
local PS,WS,TS,VU,LT,RSvc=game:GetService("Players"),game:GetService("Workspace"),game:GetService("TweenService"),game:GetService("VirtualUser"),game:GetService("Lighting"),game:GetService("RunService")
local Plr=PS.LocalPlayer;repeat task.wait()until Plr.Character and Plr.Character:FindFirstChild("HumanoidRootPart");task.wait(2)
local Remotes=RS:WaitForChild("Remotes",5);local CF=Remotes:FindFirstChild("CommF_");local QuestIlha=getgenv().QuestIlha

getgenv().AF,getgenv().AK,getgenv().AB,getgenv().AS,getgenv().SA,getgenv().SP=false,false,false,false,"Melee",1
getgenv().AR,getgenv().SR,getgenv().WP,getgenv().BM,getgenv().BringMode,getgenv().AC=false,"Human","Melee",true,350,false
getgenv().CurrentQuestName,getgenv().CurrentQuestLevel,getgenv().KataIndex,getgenv().BoneIndex=nil,nil,1,1
getgenv().AV3,getgenv().GRaceClickAutov4,getgenv().FarmMode,getgenv().LastQuestAttempt=false,false,"Farm Level",0
getgenv().GSelectWeapon=nil
Plr.Idled:Connect(function()VU:CaptureController();VU:ClickButton2(Vector2.new())end)

hookfunction(require(RS.Effect.Container.Death),function()end)
hookfunction(require(RS.Effect.Container.Respawn),function()end)

World1=game.PlaceId==2753915549 or game.PlaceId==85211729168715
World2=game.PlaceId==4442272183 or game.PlaceId==79091703265657
World3=game.PlaceId==7449423635 or game.PlaceId==100117331123089

function GetSea()if World1 then return 1 elseif World2 then return 2 elseif World3 then return 3 else return 1 end end
local function GL()local ok,v=pcall(function()return Plr.Data.Level.Value end)return ok and v or 1 end
local function GQ()if not QuestIlha or not QuestIlha.GetQuestForLevel then return nil end;local q=QuestIlha.GetQuestForLevel(GL());if not q then return nil end;local qSea=q.Sea or 1;local pSea=GetSea();if qSea>pSea then return QuestIlha.GetLastQuestForSea and QuestIlha.GetLastQuestForSea(pSea)or q end;return q end
local function HQ()local ok,r=pcall(function()return Plr.PlayerGui.Main.Quest.Visible end)return ok and r end
local function CQ()pcall(function()if CF and HQ()then CF:InvokeServer("AbandonQuest")task.wait(0.3)end end)end
local function IFA()return getgenv().AF or getgenv().AK or getgenv().AB end
local function SNL(char,enable)if not char then return end;for _,p in ipairs(char:GetDescendants())do if p:IsA("BasePart")and(p.Name=="HumanoidRootPart"or p.Name=="UpperTorso"or p.Name=="LowerTorso"or p.Name=="Torso")then p.CanCollide=not enable end end end
local function RNP()pcall(function()local c=Plr.Character;if not c then return end;local hrp,hum=c:FindFirstChild("HumanoidRootPart"),c:FindFirstChild("Humanoid");if not hrp or not hum then return end;SNL(c,false);hrp.Anchored=false;hrp.AssemblyLinearVelocity=Vector3.new();hum:ChangeState(Enum.HumanoidStateType.RunningNoPhysics);task.wait(0.1);hum:ChangeState(Enum.HumanoidStateType.Freefall)end)end
local function IMN(obj)if isnetworkowner then return isnetworkowner(obj)end;local c=Plr.Character;if not c or not c:FindFirstChild("HumanoidRootPart")then return false end;return(obj.Position-c.HumanoidRootPart.Position).Magnitude<=getgenv().BringMode end
local CBP=nil
local function BM(mn,tcf)if not getgenv().BM then return end;local c=Plr.Character;if not c or not c:FindFirstChild("HumanoidRootPart")then return end;local hrp=c.HumanoidRootPart;local t=tcf or CBP or hrp.CFrame*CFrame.new(0,-20,0);for _,m in pairs(WS.Enemies:GetChildren())do if m.Name==mn and m:FindFirstChild("Humanoid")and m:FindFirstChild("HumanoidRootPart")and m.Humanoid.Health>0 and(m.HumanoidRootPart.Position-hrp.Position).Magnitude<=getgenv().BringMode and IMN(m.HumanoidRootPart)then pcall(function()m.HumanoidRootPart.CFrame=t;m.HumanoidRootPart.CanCollide=false;m.HumanoidRootPart.Size=Vector3.new(50,50,50);if m:FindFirstChild("Head")then m.Head.CanCollide=false end;m.Humanoid.WalkSpeed=0;m.Humanoid.JumpPower=0;m.Humanoid:ChangeState(14);m.Humanoid:ChangeState(11);if m.Humanoid:FindFirstChild("Animator")then m.Humanoid.Animator:Destroy()end end)end end;if sethiddenproperty then pcall(function()sethiddenproperty(Plr,"SimulationRadius",math.huge)end)end end

function EquipWeapon(toolName)
    pcall(function()
        local character = Plr.Character or Plr.CharacterAdded:Wait()
        local backpack = Plr.Backpack
        for _, tool in pairs(backpack:GetChildren()) do
            if tool:IsA("Tool") and tool.Name == toolName then
                tool.Parent = character
                getgenv().GSelectWeapon = toolName
                return
            end
        end
        for _, tool in pairs(character:GetChildren()) do
            if tool:IsA("Tool") and tool.Name == toolName then
                getgenv().GSelectWeapon = toolName
                return
            end
        end
    end)
end

local function EQ()
    if not IFA() then return end
    pcall(function()
        if getgenv().WP == "Sword" then
            for _, v in ipairs(Plr.Backpack:GetChildren()) do
                if v:IsA("Tool") and v.ToolTip == "Sword" then
                    EquipWeapon(v.Name)
                    return
                end
            end
        elseif getgenv().WP == "Melee" then
            for _, v in ipairs(Plr.Backpack:GetChildren()) do
                if v:IsA("Tool") and v.ToolTip == "Melee" then
                    EquipWeapon(v.Name)
                    return
                end
            end
        end
    end)
end

local function FMS(n)for _,m in ipairs(WS.Enemies:GetChildren())do if m.Name==n and m:FindFirstChild("Humanoid")and m:FindFirstChild("HumanoidRootPart")and m.Humanoid.Health>0 then return m end end end
local function FAM(list)for _,n in ipairs(list)do local m=FMS(n);if m then return m,n end end end
local function GR()local ok,v=pcall(function()return Plr.Data.Race.Value end)return ok and v or"Unknown"end
local function GF()local ok,v=pcall(function()return Plr.Data.Fragments.Value end)return ok and v or 0 end
local function RR()if GF()<3000 or not CF then return false end;return pcall(function()CF:InvokeServer("BlackbeardReward","Reroll","2")end)end
local function FP()pcall(function()LT.GlobalShadows=false;LT.FogEnd=9e9;settings().Rendering.QualityLevel=Enum.QualityLevel.Level01;for _,v in ipairs(WS:GetDescendants())do if v:IsA("BasePart")or v:IsA("UnionOperation")or v:IsA("MeshPart")then v.Material=Enum.Material.Plastic;v.Reflectance=0 elseif v:IsA("Decal")or v:IsA("Texture")then v.Transparency=1 elseif v:IsA("ParticleEmitter")or v:IsA("Trail")then v.Lifetime=NumberRange.new(0)elseif v:IsA("Fire")or v:IsA("SpotLight")or v:IsA("Smoke")or v:IsA("Sparkles")then v.Enabled=false end end end)end
local function US(t,k)pcall(function()local VIM=game:GetService("VirtualInputManager");VIM:SendKeyEvent(true,k,false,game);task.wait(0.05);VIM:SendKeyEvent(false,k,false,game)end)end

local Stepped=RSvc.Stepped;local AT,FC,GT,HC=nil,nil,nil,nil
local function SF()if FC then FC:Disconnect();FC=nil end;CBP=nil end
local function SH()if HC then HC:Disconnect();HC=nil end end
local function SAT()if AT then AT:Cancel();AT=nil end;SF();SH();if GT then GT:Cancel();GT=nil end end
local function TF25(hrp,tHRP,spd)if not hrp or not tHRP then return end;spd=spd or 300;if AT then AT:Cancel();AT=nil end;SF();local tCF=tHRP.CFrame*CFrame.new(0,25,0);local dist=(hrp.Position-tCF.Position).Magnitude;AT=TS:Create(hrp,TweenInfo.new(math.max(dist/spd,0.05),Enum.EasingStyle.Linear),{CFrame=tCF});AT:Play();AT.Completed:Once(function()FC=Stepped:Connect(function()if not tHRP or not tHRP.Parent or not IFA()then SF();return end;local c=Plr.Character;if not c then SF();return end;local cHRP=c:FindFirstChild("HumanoidRootPart");if not cHRP then SF();return end;local nCF=tHRP.CFrame*CFrame.new(0,25,0);cHRP.AssemblyLinearVelocity=Vector3.zero;cHRP.CFrame=nCF;CBP=nCF*CFrame.new(0,-25,0)end)end)end
local function TTG(hrp,tCF,spd)if not hrp then return end;spd=spd or 250;SF();SH();if GT then GT:Cancel();GT=nil end;if AT then AT:Cancel();AT=nil end;local dist=(hrp.Position-tCF.Position).Magnitude;local dur=math.max(dist/spd,0.1);GT=TS:Create(hrp,TweenInfo.new(dur,Enum.EasingStyle.Linear),{CFrame=tCF});GT:Play();HC=RSvc.Heartbeat:Connect(function()if not hrp or not hrp.Parent then SH();return end;hrp.Velocity=Vector3.new(0,0,0)end);GT.Completed:Wait();SH();GT=nil end

local KM={"Cookie Crafter","Cake Guard","Baking Staff","Head Baker","Cocoa Warrior"}
local BonM={"Reborn Skeleton","Living Zombie","Demonic Soul","Posessed Mummy","Peanut Scout"}
local KS,BS=CFrame.new(-2091,70,-12373),CFrame.new(-9506,172,6057)

local Fl=loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local Win=Fl:CreateWindow({Title="Volt Hub V3",SubTitle="Blox Fruits Delta",TabWidth=160,Size=UDim2.fromOffset(580,460),Acrylic=false,Theme="Darker"})

local TabM=Win:AddTab({Title="Tab Main",Icon="home"})
local TabSe=Win:AddTab({Title="Tab Settings",Icon="settings"})
local TabS=Win:AddTab({Title="Tab Shop",Icon="shopping-bag"})
local TabLP=Win:AddTab({Title="LocalPlayer",Icon="user"})
local TabSF=Win:AddTab({Title="Tab Settings Farming",Icon="clock"})
local TabF=Win:AddTab({Title="Tab Farming",Icon="sword"})
local TabSt=Win:AddTab({Title="Tab Status & ESP",Icon="eye"})

TabM:AddButton({Title="Discord",Description="Copiar link",Callback=function()setclipboard("https://discord.gg/29BDQqHYbJ")end})
TabS:AddSection("Shop")
TabS:AddButton({Title="Comprar Haki",Description="25k Beli",Callback=function()if CF then CF:InvokeServer("BuyHaki","Buso")end end})
TabS:AddButton({Title="Comprar Race",Description="3k Frags (1x)",Callback=function()RR()end})

TabSF:AddSection("Settings Farming")
TabSF:AddDropdown("Weap",{Title="Weapon Style",Values={"Melee","Sword"},Default=1}):OnChanged(function(v)getgenv().WP=v end)
TabSF:AddToggle("BM",{Title="Bring Mob (2)",Default=true}):OnChanged(function(v)getgenv().BM=v end)
TabSF:AddToggle("AC",{Title="Auto Click",Default=false}):OnChanged(function(v)getgenv().AC=v end)
TabSF:AddToggle("AV3",{Title="Auto Active v3",Default=false}):OnChanged(function(v)getgenv().AV3=v end)
TabSF:AddToggle("AV4",{Title="Auto Active v4",Default=false}):OnChanged(function(v)getgenv().GRaceClickAutov4=v end)

TabF:AddSection("Farming")
TabF:AddDropdown("FarmSel",{Title="Select Farming",Values={"Farm Level","Farm Katakuri","Farm Bone"},Default=1}):OnChanged(function(v)getgenv().FarmMode=v end)
local TG_MAIN=TabF:AddToggle("MainFarm",{Title="Auto Farm",Default=false})
TG_MAIN:OnChanged(function(v)
if v then
if getgenv().FarmMode=="Farm Katakuri"and(GL()<1500 or not World3)then TG_MAIN:SetValue(false);return end
if getgenv().FarmMode=="Farm Bone"and(GL()<1500 or not World3)then TG_MAIN:SetValue(false);return end
if getgenv().FarmMode=="Farm Level"then getgenv().AF,getgenv().AK,getgenv().AB=true,false,false
elseif getgenv().FarmMode=="Farm Katakuri"then getgenv().AF,getgenv().AK,getgenv().AB,getgenv().KataIndex=false,true,false,1
elseif getgenv().FarmMode=="Farm Bone"then getgenv().AF,getgenv().AK,getgenv().AB,getgenv().BoneIndex=false,false,true,1 end
else getgenv().AF,getgenv().AK,getgenv().AB=false,false,false;RNP();SAT()end
end)

TabSt:AddSlider("Pts",{Title="Pontos por Upgrade",Default=1,Min=1,Max=100,Rounding=0}):OnChanged(function(v)getgenv().SP=v end)
TabSt:AddDropdown("Stat",{Title="Selecionar Status",Values={"Melee","Defense","Sword","Gun","Blox Fruit"},Default=1}):OnChanged(function(v)getgenv().SA=({Melee="Melee",Defense="Defense",Sword="Sword",Gun="Gun",["Blox Fruit"]="Fruit"})[v]end)
TabSt:AddToggle("AS",{Title="Auto Status",Default=false}):OnChanged(function(v)getgenv().AS=v end)

TabSe:AddSection("Server HOP")
TabSe:AddButton({Title="Rejoin",Description="Reconectar",Callback=function()game:GetService("TeleportService"):Teleport(game.PlaceId,Plr)end})
TabSe:AddButton({Title="Hop Server",Description="Poucos players",Callback=function()task.spawn(function()pcall(function()local HS,TS2,srvs=game:GetService("HttpService"),game:GetService("TeleportService"),{};local ok,res=pcall(function()return game:HttpGet("https://games.roblox.com/v1/games/"..game.PlaceId.."/servers/Public?sortOrder=Asc&limit=100")end);if ok then local d=HS:JSONDecode(res);if d and d.data then for _,s in ipairs(d.data)do if s.playing and s.playing>=1 and s.playing<=8 and s.id~=game.JobId then table.insert(srvs,s.id)end end end end;if #srvs>0 then TS2:TeleportToPlaceInstance(game.PlaceId,srvs[math.random(1,#srvs)],Plr)else TS2:Teleport(game.PlaceId,Plr)end end)end)end})
TabSe:AddButton({Title="FPS Boost",Description="Tirar Lag",Callback=FP})

local SG=Instance.new("ScreenGui");SG.Name="VoltToggle";SG.ResetOnSpawn=false;SG.Parent=Plr:WaitForChild("PlayerGui")
local BTN=Instance.new("ImageButton")
BTN.Size=UDim2.fromOffset(70,70)
BTN.Position=UDim2.new(0,20,0,20)
BTN.BackgroundTransparency=1
BTN.Image="rbxassetid://101674777317269"
BTN.ScaleType=Enum.ScaleType.Fit
BTN.AutoButtonColor=false
BTN.ImageTransparency=0
BTN.Parent=SG
local UIC=Instance.new("UICorner");UIC.CornerRadius=UDim.new(1,0);UIC.Parent=BTN

local dragging,dragInput,dragStart,startPos
local function update(input)local delta=input.Position-dragStart;BTN.Position=UDim2.new(startPos.X.Scale,startPos.X.Offset+delta.X,startPos.Y.Scale,startPos.Y.Offset+delta.Y)end
BTN.InputBegan:Connect(function(input)if input.UserInputType==Enum.UserInputType.MouseButton1 or input.UserInputType==Enum.UserInputType.Touch then dragging=true;dragStart=input.Position;startPos=BTN.Position;input.Changed:Connect(function()if input.UserInputState==Enum.UserInputState.End then dragging=false end end)end end)
BTN.InputChanged:Connect(function(input)if input.UserInputType==Enum.UserInputType.MouseMovement or input.UserInputType==Enum.UserInputType.Touch then dragInput=input end end)
game:GetService("UserInputService").InputChanged:Connect(function(input)if input==dragInput and dragging then update(input)end end)
BTN.MouseButton1Click:Connect(function()Win.Root.Visible=not Win.Root.Visible end)

local RA,RH;task.spawn(function()task.wait(2);pcall(function()local M=RS:WaitForChild("Modules",5);if M then local N=M:FindFirstChild("Net");if N then RA,RH=N:FindFirstChild("RE/RegisterAttack"),N:FindFirstChild("RE/RegisterHit")end end end)end)

task.spawn(function()while task.wait(0.1)do if IFA()and RA and RH then pcall(function()local tgts={};for _,m in ipairs(WS.Enemies:GetChildren())do if m:FindFirstChild("Head")and m:FindFirstChild("Humanoid")and m.Humanoid.Health>0 then local valid=false;if getgenv().AF then local q=GQ();if q and m.Name==(q.M or q.Mon)then valid=true end elseif getgenv().AK then for _,n in ipairs(KM)do if m.Name==n then valid=true;break end end elseif getgenv().AB then for _,n in ipairs(BonM)do if m.Name==n then valid=true;break end end end;if valid then table.insert(tgts,{m,m.Head})end end end;if #tgts>0 then RA:FireServer(0.1);RH:FireServer(tgts[1][2],tgts)end end)end end end)

task.spawn(function()while task.wait(0.1)do if getgenv().AC and RA and RH then pcall(function()local c=Plr.Character;local hrp=c and c:FindFirstChild("HumanoidRootPart");if not hrp then return end;local tgts={};for _,m in ipairs(WS.Enemies:GetChildren())do if m:FindFirstChild("Head")and m:FindFirstChild("Humanoid")and m.Humanoid.Health>0 and m:FindFirstChild("HumanoidRootPart")and(hrp.Position-m.HumanoidRootPart.Position).Magnitude<=50 then table.insert(tgts,{m,m.Head})end end;if #tgts>0 then RA:FireServer(0.1);RH:FireServer(tgts[1][2],tgts)end end)end end end)

task.spawn(function()while task.wait(0.5)do if IFA()then EQ()end end end)

local function PM(c,hrp,hum,fMob,mn)SNL(c,true);hum:ChangeState(Enum.HumanoidStateType.RunningNoPhysics);local r=fMob:FindFirstChild("HumanoidRootPart");if r then TF25(hrp,r,300);while fMob.Parent and fMob.Humanoid.Health>0 and IFA()and hum.Health>0 do BM(mn);task.wait(0.05)end;SAT()end end

local function HMR(mList,iVar,sCF)local aM,mn=FAM(mList);if aM then for i,n in ipairs(mList)do if n==mn then getgenv()[iVar]=i;break end end;local h,r=aM:FindFirstChild("Humanoid"),aM:FindFirstChild("HumanoidRootPart");if h and r and h.Health>0 then local c,hrp,hum=Plr.Character,Plr.Character:FindFirstChild("HumanoidRootPart"),Plr.Character:FindFirstChild("Humanoid");if c and hrp and hum then PM(c,hrp,hum,aM,mn);if not FMS(mn)then getgenv()[iVar]=getgenv()[iVar]+1;if getgenv()[iVar]>#mList then getgenv()[iVar]=1 end end end end else if not FMS(mList[getgenv()[iVar]])then getgenv()[iVar]=getgenv()[iVar]+1;if getgenv()[iVar]>#mList then getgenv()[iVar]=1 end end;local c,hrp=Plr.Character,Plr.Character and Plr.Character:FindFirstChild("HumanoidRootPart");if c and hrp then SAT();TTG(hrp,sCF,250);task.wait(0.5)end end end

local function TryGetQuest(qN,qL,qCF)local currentTime=tick();if currentTime-getgenv().LastQuestAttempt<1 then return false end;local c=Plr.Character;if not c then return false end;local hrp=c:FindFirstChild("HumanoidRootPart");if not hrp then return false end;local dist=(hrp.Position-qCF.Position).Magnitude;if dist>5 then SAT();TTG(hrp,qCF,250);return false end;getgenv().LastQuestAttempt=currentTime;local success=pcall(function()CF:InvokeServer("StartQuest",qN,qL)end);if success then getgenv().CurrentQuestName=qN;getgenv().CurrentQuestLevel=qL;task.wait(1);return true end;return false end

task.spawn(function()
while task.wait(0.15)do pcall(function()
if not IFA()then return end
local c=Plr.Character;if not c then return end
local hrp,hum=c:FindFirstChild("HumanoidRootPart"),c:FindFirstChild("Humanoid")
if not hrp or not hum or hum.Health<=0 then 
if hum and hum.Health<=0 then SAT();repeat task.wait()until Plr.Character and Plr.Character:FindFirstChild("HumanoidRootPart")and Plr.Character:FindFirstChild("Humanoid")and Plr.Character.Humanoid.Health>0;task.wait(1)end;return 
end

if getgenv().AF then
local q=GQ();if not q then return end
local qN,qL,mn,msCF=q.N or q.NameQuest,q.L or q.LevelQuest,q.M or q.Mon,q.SC or q.CFrameMon
local qCF=q.C or q.CFrameQuest or CFrame.new(msCF.Position.X,msCF.Position.Y>0 and msCF.Position.Y or 50,msCF.Position.Z)

if getgenv().CurrentQuestName~=qN or getgenv().CurrentQuestLevel~=qL then 
CQ();getgenv().CurrentQuestName,getgenv().CurrentQuestLevel=nil,nil;SAT();task.wait(0.5)
end

if not HQ()then if not TryGetQuest(qN,qL,qCF)then return end end

local fMob=FMS(mn)
if fMob then PM(c,hrp,hum,fMob,mn)
else SAT();TTG(hrp,CFrame.new(msCF.Position.X,msCF.Position.Y>0 and msCF.Position.Y or 50,msCF.Position.Z),250);task.wait(0.5)end
elseif getgenv().AK then HMR(KM,"KataIndex",KS)
elseif getgenv().AB then HMR(BonM,"BoneIndex",BS)end
end)end
end)

task.spawn(function()while task.wait(1)do if getgenv().AS and getgenv().SA and CF then pcall(function()CF:InvokeServer("AddPoint",getgenv().SA,getgenv().SP)end)end end end)
task.spawn(function()while task.wait(0.3)do if getgenv().AV3 then pcall(function()RS.Remotes.CommE:FireServer("ActivateAbility")end)end end end)
spawn(function()while wait(0.2)do pcall(function()if getgenv().GRaceClickAutov4 then local c=Plr.Character;if c and c:FindFirstChild("RaceEnergy")then local rE=c.RaceEnergy;if rE and rE.Value>=1 then US(nil,"Y")end end end end)end end)

Fl:Notify({Title="Volt Hub V3",Content="Carregado! Sea: "..GetSea().." | Lv: "..GL(),Duration=5})
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
    ["Dark Step"] = CFrame.new(-983.6179809570312, 12.449996948242188, 3990.462890625),
    ["Electro"] = CFrame.new(-5382.7822265625, 12.550003051757812, -2148.818115234375),
    ["Fishman Karate"] = CFrame.new(61586.722, 18.9, 989.584),
    ["Dragon Breath"] = CFrame.new(699.572, 186.99, 656.837),
    ["Death Step"] = CFrame.new(6358.787, 296.661, -6766.079),
    ["Electric Claw"] = CFrame.new(6358.787, 296.661, -6766.079),
    ["Sharkman Karate"] = CFrame.new(-2602.152, 239.212, -10315.58),
    ["Dragon Talon"] = CFrame.new(5666.225, 1211.307, 866.386),
    ["Godhuman"] = CFrame.new(-13777.618, 334.652, -9879.684),
    ["Sanguine Art"] = CFrame.new(-16515.053, 23.17, -193.006)
}

local function BuyFightingStyle(styleName, remoteCommand)
    local npcPos = FightingStyleNPCs[styleName]
    if not npcPos then return end
    local tween = TweenToPosition(npcPos)
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

-- Adiciona seção na aba Shop
TabS:AddSection("Estilos de Lutas")

TabS:AddButton({Title = "Buy Dark Step", Callback = function() BuyFightingStyle("Dark Step", function() CF:InvokeServer("BuyBlackLeg") end) end})
TabS:AddButton({Title = "Buy Eletric", Callback = function() BuyFightingStyle("Electro", function() CF:InvokeServer("BuyElectro") end) end})
TabS:AddButton({Title = "Buy Water Kung Fu", Callback = function() BuyFightingStyle("Fishman Karate", function() CF:InvokeServer("BuyFishmanKarate") end) end})
TabS:AddButton({Title = "Buy Dragon Breath", Callback = function() BuyFightingStyle("Dragon Breath", function() CF:InvokeServer("BlackbeardReward", "DragonClaw", "1") CF:InvokeServer("BlackbeardReward", "DragonClaw", "2") end) end})
TabS:AddButton({Title = "Buy Death Step", Callback = function() BuyFightingStyle("Death Step", function() CF:InvokeServer("BuyDeathStep") end) end})
TabS:AddButton({Title = "Buy Eletric Claw", Callback = function() BuyFightingStyle("Electric Claw", function() CF:InvokeServer("BuyElectricClaw", "Start") CF:InvokeServer("BuyElectricClaw") end) end})
TabS:AddButton({Title = "Buy Sharkman Karatê", Callback = function() BuyFightingStyle("Sharkman Karate", function() CF:InvokeServer("BuySharkmanKarate", true) CF:InvokeServer("BuySharkmanKarate") end) end})
TabS:AddButton({Title = "Buy Dragon Talon", Callback = function() BuyFightingStyle("Dragon Talon", function() CF:InvokeServer("BuyDragonTalon", true) CF:InvokeServer("BuyDragonTalon") end) end})
TabS:AddButton({Title = "Buy GodHuman", Callback = function() BuyFightingStyle("Godhuman", function() CF:InvokeServer("BuyGodhuman", true) CF:InvokeServer("BuyGodhuman") end) end})
TabS:AddButton({Title = "Buy Sanguine Art", Callback = function() BuyFightingStyle("Sanguine Art", function() CF:InvokeServer("BuySanguineArt", true) CF:InvokeServer("BuySanguineArt") end) end})

local TG_ABLS = TabS:AddToggle("AutoBuyLegSword", {Title = "Auto Buy Legendary Sword", Default = false})
TG_ABLS:OnChanged(function(v) getgenv().AutoBuyLegendarySword = v end)

task.spawn(function()
    while task.wait(5) do
        if getgenv().AutoBuyLegendarySword then pcall(BuyLegendarySword) end
    end
end)

-- ===== SISTEMA DE BOSS FARM (MOVIDO PARA TAB STACK FARMING) =====
local placeId = game.PlaceId
local worldMap = {[2753915549] = true, [4442272183] = true, [7449423635] = true}
if worldMap[placeId] then
    if placeId == 2753915549 then World1 = true
    elseif placeId == 4442272183 then World2 = true
    elseif placeId == 7449423635 then World3 = true end
end

local tableBoss = {}
if World1 then
    tableBoss = {"The Gorilla King", "Bobby", "Yeti", "Mob Leader", "Vice Admiral", "Warden", "Chief Warden", "Swan", "Magma Admiral", "Fishman Lord", "Wysper", "Thunder God", "Cyborg", "Saber Expert"}
elseif World2 then
    tableBoss = {"Diamond", "Jeremy", "Fajita", "Don Swan", "Smoke Admiral", "Cursed Captain", "Darkbeard", "Order", "Awakened Ice Admiral", "Tide Keeper"}
elseif World3 then
    tableBoss = {"Stone", "Island Empress", "Kilo Admiral", "Captain Elephant", "Beautiful Pirate", "rip_indra True Form", "Longma", "Soul Reaper", "Cake Queen", "Cake Prince", "Dough King"}
end

-- MOVIDO PARA TAB STACK FARMING (TabEF)
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

-- Sistema de Ataque (RegisterAttack/RegisterHit)
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
-- MÓDULO AUTO FARM MATERIAL
-- Cole este código abaixo do script principal do Volt

-- Material Data
local MaterialData = {
    -- Sea 3
    ["Scrap Metal"] = {Mob = "Jungle Pirate", CFrame = CFrame.new(-12347, 332, -10452)},
    ["Demonic Wisp"] = {Mob = "Demonic Soul", CFrame = CFrame.new(-9507, 172, 6158)},
    ["Conjured Cocoa"] = {Mob = "Cocoa Warrior", CFrame = CFrame.new(-82, 25, -12309)},
    ["Dragon Scale"] = {Mob = "Dragon Crew Archer", CFrame = CFrame.new(6719, 484, 181)},
    ["Gunpowder"] = {Mob = "Pistol Billionaire", CFrame = CFrame.new(-379, 73, 5550)},
    ["Fish Tail"] = {Mob = "Fishman Raider", CFrame = CFrame.new(-10646, 332, -8490)},
    ["Mini Tusk"] = {Mob = "Mythological Pirate", CFrame = CFrame.new(-13620, 470, -6969)},
    
    -- Sea 2
    ["Radioactive Material"] = {Mob = "Factory Staff", CFrame = CFrame.new(494, 73, 157)},
    ["Mystic Droplet"] = {Mob = "Sea Soldier", CFrame = CFrame.new(-3373, 27, -9776)},
    ["Magma Ore"] = {Mob = "Lava Pirate", CFrame = CFrame.new(-5091, 29, -4944)},
    ["Vampire Fang"] = {Mob = "Vampire", CFrame = CFrame.new(-5996, 6, -1297)},
    
    -- Sea 1 e 2
    ["Angel Wings"] = {Mob = "Royal Squad", CFrame = CFrame.new(-7899, 5546, -379)},
    
    -- Ectoplasma (3 mobs possíveis)
    ["Ectoplasm"] = {Mob = "Ship Deckhand", CFrame = CFrame.new(924, 125, 32853)}
}

-- Variáveis Globais
getgenv().AMaterial = false
getgenv().SelectedMaterial = nil
local MaterialTweenActive = false

-- Função para obter materiais do Sea atual
local function GetMaterialsForCurrentSea()
    if World3 then
        return {
            "Scrap Metal",
            "Demonic Wisp",
            "Conjured Cocoa",
            "Dragon Scale",
            "Gunpowder",
            "Fish Tail",
            "Mini Tusk",
            "Ectoplasm"
        }
    elseif World2 then
        return {
            "Radioactive Material",
            "Mystic Droplet",
            "Magma Ore",
            "Vampire Fang",
            "Angel Wings",
            "Ectoplasm"
        }
    elseif World1 then
        return {
            "Angel Wings",
            "Ectoplasm"
        }
    end
    return {"Scrap Metal"}
end

-- Função para encontrar mob específico
local function FindMaterialMob(mobName)
    if mobName == "Ship Deckhand" then
        local mobList = {"Ship Deckhand", "Ship Steward", "Ship Officer"}
        for _, name in ipairs(mobList) do
            for _, m in ipairs(WS.Enemies:GetChildren()) do
                if m.Name == name and m:FindFirstChild("Humanoid") and m:FindFirstChild("HumanoidRootPart") and m.Humanoid.Health > 0 then
                    return m, name
                end
            end
        end
        return nil, nil
    end
    
    if mobName == "Royal Squad" then
        local mobList = {"Royal Squad", "Shanda"}
        for _, name in ipairs(mobList) do
            for _, m in ipairs(WS.Enemies:GetChildren()) do
                if m.Name == name and m:FindFirstChild("Humanoid") and m:FindFirstChild("HumanoidRootPart") and m.Humanoid.Health > 0 then
                    return m, name
                end
            end
        end
        return nil, nil
    end
    
    for _, m in ipairs(WS.Enemies:GetChildren()) do
        if m.Name == mobName and m:FindFirstChild("Humanoid") and m:FindFirstChild("HumanoidRootPart") and m.Humanoid.Health > 0 then
            return m, mobName
        end
    end
    return nil, nil
end

-- UI - Tab Farming
TabF:AddSection("Material")

local MaterialDropdown = TabF:AddDropdown("MatSel", {
    Title = "Select Material",
    Values = GetMaterialsForCurrentSea(),
    Default = 1
})

MaterialDropdown:OnChanged(function(v)
    getgenv().SelectedMaterial = v
end)

local TG_MATERIAL = TabF:AddToggle("AutoMat", {
    Title = "Auto Farm Material",
    Default = false
})

TG_MATERIAL:OnChanged(function(v)
    getgenv().AMaterial = v
    if not v then
        MaterialTweenActive = false
        RNP()
        SAT()
    end
end)

-- Loop Principal do Material Farm (SÓ TWEEN, SEM TELEPORTE)
task.spawn(function()
    while task.wait(0.15) do
        pcall(function()
            if not getgenv().AMaterial then return end
            if not getgenv().SelectedMaterial then return end
            
            local materialInfo = MaterialData[getgenv().SelectedMaterial]
            if not materialInfo then return end
            
            local c = Plr.Character
            if not c then return end
            
            local hrp, hum = c:FindFirstChild("HumanoidRootPart"), c:FindFirstChild("Humanoid")
            if not hrp or not hum or hum.Health <= 0 then
                if hum and hum.Health <= 0 then
                    MaterialTweenActive = false
                    SAT()
                    repeat task.wait() until Plr.Character and Plr.Character:FindFirstChild("HumanoidRootPart") and Plr.Character:FindFirstChild("Humanoid") and Plr.Character.Humanoid.Health > 0
                    task.wait(1)
                end
                return
            end
            
            local targetMob, actualMobName = FindMaterialMob(materialInfo.Mob)
            
            if targetMob then
                local r = targetMob:FindFirstChild("HumanoidRootPart")
                if r then
                    -- ATIVA NO COLLIDE E NO PHYSICS
                    SNL(c, true)
                    hum:ChangeState(Enum.HumanoidStateType.RunningNoPhysics)
                    
                    -- SE NÃO ESTÁ EM COMBATE, USA TWEEN PARA IR ATÉ O MOB
                    if not MaterialTweenActive then
                        local targetPos = r.CFrame * CFrame.new(0, 25, 0)
                        local distance = (hrp.Position - targetPos.Position).Magnitude
                        
                        -- Só faz tween se estiver longe
                        if distance > 10 then
                            MaterialTweenActive = true
                            
                            -- Cria tween suave
                            local tweenInfo = TweenInfo.new(
                                distance / 300,  -- Velocidade 300
                                Enum.EasingStyle.Linear,
                                Enum.EasingDirection.InOut
                            )
                            
                            local tween = TS:Create(hrp, tweenInfo, {CFrame = targetPos})
                            tween:Play()
                            
                            -- Aguarda o tween terminar OU o mob morrer
                            local tweenFinished = false
                            tween.Completed:Connect(function()
                                tweenFinished = true
                            end)
                            
                            -- Espera tween terminar mantendo velocidade zero
                            while not tweenFinished and targetMob.Parent and targetMob.Humanoid.Health > 0 and getgenv().AMaterial do
                                hrp.AssemblyLinearVelocity = Vector3.zero
                                task.wait()
                            end
                            
                            if not targetMob.Parent or targetMob.Humanoid.Health <= 0 then
                                MaterialTweenActive = false
                                tween:Cancel()
                                return
                            end
                        else
                            MaterialTweenActive = true
                        end
                    end
                    
                    -- LOOP DE ATAQUE - MANTÉM PLAYER FIXO NO AR
                    while targetMob.Parent and targetMob.Humanoid.Health > 0 and getgenv().AMaterial and hum.Health > 0 do
                        -- TRAVA O PLAYER NO AR (IGUAL AO VOLT)
                        if r and r.Parent then
                            hrp.CFrame = r.CFrame * CFrame.new(0, 25, 0)
                            hrp.AssemblyLinearVelocity = Vector3.zero
                        end
                        
                        -- BRING MOB
                        BM(actualMobName)
                        
                        task.wait(0.05)
                    end
                    
                    MaterialTweenActive = false
                    SAT()
                end
            else
                MaterialTweenActive = false
                SAT()
                TTG(hrp, materialInfo.CFrame, 250)
                task.wait(0.5)
            end
        end)
    end
end)

-- Sistema de RegisterHit e RegisterAttack para Material (usa as variáveis globais RA e RH do Volt)
task.spawn(function()
    while task.wait(0.1) do
        if getgenv().AMaterial and RA and RH then
            pcall(function()
                local tgts = {}
                for _, m in ipairs(WS.Enemies:GetChildren()) do
                    if m:FindFirstChild("Head") and m:FindFirstChild("Humanoid") and m.Humanoid.Health > 0 then
                        local valid = false
                        if getgenv().AMaterial and getgenv().SelectedMaterial then
                            local materialInfo = MaterialData[getgenv().SelectedMaterial]
                            if materialInfo then
                                -- Verifica se é o mob do material
                                if materialInfo.Mob == "Ship Deckhand" then
                                    if m.Name == "Ship Deckhand" or m.Name == "Ship Steward" or m.Name == "Ship Officer" then
                                        valid = true
                                    end
                                elseif materialInfo.Mob == "Royal Squad" then
                                    if m.Name == "Royal Squad" or m.Name == "Shanda" then
                                        valid = true
                                    end
                                elseif m.Name == materialInfo.Mob then
                                    valid = true
                                end
                            end
                        end
                        if valid then
                            table.insert(tgts, {m, m.Head})
                        end
                    end
                end
                if #tgts > 0 then
                    RA:FireServer(0.1)
                    RH:FireServer(tgts[1][2], tgts)
                end
            end)
        end
    end
end)

print("Módulo Auto Farm Material carregado com sucesso!")
