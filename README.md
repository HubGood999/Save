local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("water hub", "BloodTheme")

-- แท็บ Discord
local Tab = Window:NewTab("water hub")
local Section = Tab:NewSection("Discord")

-- สร้างปุ่มคัดลอก
local CopyButton = Section:NewButton("Copy discord", "discord water hubd", function()
    setclipboard("https://discord.gg/N9tJkTMkPc")
    print("คัดลอกลิงก์ Discord แล้ว!")
end)

local TabFarm = Window:NewTab("main")
local SectionFarmNormal = TabFarm:NewSection("main help")



-- แท็บ Farm Normal
local TabFarm = Window:NewTab("Farm Normal")
local SectionFarmNormal = TabFarm:NewSection("Farm Normal")

SectionFarmNormal:NewButton("Farm Oil", "Farm Oil", function()
    local hitboxMagnitude = 500 -- ระยะการตีที่ต้องการ
local hasTeleported = false -- ตัวแปรเพื่อควบคุมการวาบ

-- ฟังก์ชันในการขยายระยะการตี
local function setHitboxMagnitude(player)
    if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local humanoidRootPart = player.Character.HumanoidRootPart
        local originalSize = humanoidRootPart.Size
        humanoidRootPart.Size = Vector3.new(hitboxMagnitude, originalSize.Y, hitboxMagnitude)
    end
end

-- ขยายระยะการตีสำหรับผู้เล่นทุกคนที่มีอยู่
for _, player in pairs(game.Players:GetPlayers()) do
    setHitboxMagnitude(player)
end

-- ตรวจสอบเมื่อมีผู้เล่นใหม่เข้ามา และขยายระยะการตีให้ด้วย
game.Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        setHitboxMagnitude(player)
    end)
end)

-- ฟังก์ชันหลักที่จะรันทุก 2 วินาที
while true do
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

    -- เช็คว่าต้องวาบหรือไม่
    if not hasTeleported then
        humanoidRootPart.CFrame = CFrame.new(-3184, 34, 3234)
        wait(2) -- รอ 2 วินาทีที่ตำแหน่งนี้

        -- ทำการซื้อสินค้า
        local items = {
            {"Tea", 10},
            {"Water", 10},
            {"Bread", 10},
            {"Pickaxe", 1},
            {"Sickle", 1},
            {"Axe", 1},
            {"Jackhammer", 1},
            {"Cleaver", 1},
            {"Basket", 1}
        }

        for _, item in pairs(items) do
            local args = {
                [1] = item[1],
                [2] = item[2]
            }
            game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
        end

        hasTeleported = true -- ตั้งค่าว่าวาบแล้ว
    end

    humanoidRootPart.CFrame = CFrame.new(-2533, 13, 5159)

    local oilAmount = player.Inventory:FindFirstChild("Oil")
    if oilAmount and oilAmount.Value >= 60 then
        local args = {
            [1] = "Oil",
            [2] = "60"
        }
        game:GetService("ReplicatedStorage"):WaitForChild("WorldMarket_Remotes"):WaitForChild("RemoteEvent"):FireServer(unpack(args))

        -- หลังจากขายน้ำมัน ให้กลับไปวาบใหม่
        hasTeleported = false -- รีเซ็ตตัวแปรเพื่อให้วาบใหม่ในรอบถัดไป
    end

    wait(2) -- รอ 2 วินาที
end

end)

-- สร้างรายการตัวเลือก
local farmLocations = {
    ["Farm Stone"] = CFrame.new(-4539, 38, -227),
    ["Farm Cabbage"] = CFrame.new(4855, 34, 897),
    ["Farm Banana"] = CFrame.new(-2960, 33, 92),
    ["Farm Strawberry"] = CFrame.new(3426, 33, -227),
    ["Farm Apple"] = CFrame.new(3409, 35, 2087),
    ["Farm Orange"] = CFrame.new(2379, 37, 3164),
    ["Farm Meat"] = CFrame.new(4174, 34, 3484),
    ["Farm Wood"] = CFrame.new(-4784, 33, 1391),
    ["Farm Rice"] = CFrame.new(2061, 21, -406),
    ["Farm Oil"] = CFrame.new(-2533, 13, 5159)
}

local selectedFarm = nil  -- ตัวแปรเก็บฟาร์มที่เลือก

-- สร้าง Dropdown เพื่อเลือกสิ่งที่ต้องการฟาร์ม
SectionFarmNormal:NewDropdown("Select Farm", "Choose a farming location", {"Farm Stone", "Farm Cabbage", "Farm Banana", "Farm Strawberry", "Farm Apple", "Farm Orange", "Farm Meat", "Farm Wood", "Farm Rice", "Farm Oil"}, function(option)
    selectedFarm = option  -- เก็บค่าที่เลือกไว้
end)

-- สร้างปุ่มสำหรับกดไปยังตำแหน่งที่เลือก
SectionFarmNormal:NewButton("Confirm Farm", "Go to selected farm location", function()
    if selectedFarm then  -- ตรวจสอบว่ามีการเลือกฟาร์มแล้วหรือยัง
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ย้ายไปยังตำแหน่งฟาร์มที่เลือก
        humanoidRootPart.CFrame = farmLocations[selectedFarm]
    else
        print("Please select a farm location first!")  -- แสดงข้อความหากยังไม่ได้เลือกฟาร์ม
    end
end)


-- แท็บ Farm Kaitun
local TabFarmKaitun = Window:NewTab("Farm kaitun")
local SectionFarmKaitun = TabFarmKaitun:NewSection("Farm kaitun")
SectionFarmKaitun:NewButton("Clicked to Farmkaitun", "ButtonInfo", function()
local hitboxMagnitude = 500 -- ระยะการตีที่ต้องการ

-- ฟังก์ชันในการขยายระยะการตี
local function setHitboxMagnitude(player)
    if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local humanoidRootPart = player.Character.HumanoidRootPart
        local originalSize = humanoidRootPart.Size
        humanoidRootPart.Size = Vector3.new(hitboxMagnitude, originalSize.Y, hitboxMagnitude)
    end
end

-- ขยายระยะการตีสำหรับผู้เล่นทุกคนที่มีอยู่
for _, player in pairs(game.Players:GetPlayers()) do
    setHitboxMagnitude(player)
end

-- ตรวจสอบเมื่อมีผู้เล่นใหม่เข้ามา และขยายระยะการตีให้ด้วย
game.Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        setHitboxMagnitude(player)
    end)
end)
-- ฟังก์ชันหลักสำหรับทำงานต่าง ๆ
local function mainLoop()
    while true do
        local args = {
            [1] = "Support Gacha",
            [2] = 20
        }

        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Gacha"):InvokeServer(unpack(args))
        wait(0.5)

        args = {
            [1] = "GachaCar250kg.",
            [2] = 20
        }

        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Gacha"):InvokeServer(unpack(args))
        wait(0.5)

        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        humanoidRootPart.CFrame = CFrame.new(-1658, 42, 2338)
        wait(1.5)

        args = {
            [1] = "10000",
            [2] = "Withdraw"
        }

        game:GetService("ReplicatedStorage"):WaitForChild("BankingRemotes"):WaitForChild("MainRemote"):FireServer(unpack(args))

        wait(1.5)
        humanoidRootPart.CFrame = CFrame.new(-3184, 34, 3234)
        wait(1.5)
        local args = {
    [1] = "Tea",
    [2] = 10
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
local args = {
    [1] = "Water",
    [2] = 10
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
local args = {
    [1] = "Bread",
    [2] = 10
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
        local args = {
    [1] = "Pickaxe",
    [2] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
local args = {
    [1] = "Sickle",
    [2] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
local args = {
    [1] = "Axe",
    [2] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
local args = {
    [1] = "Jackhammer",
    [2] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
local args = {
    [1] = "Cleaver",
    [2] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
local args = {
            [1] = "Basket",
            [2] = 1
        }
        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))

        humanoidRootPart.CFrame = CFrame.new(4855, 34, 897)
        wait(0.5)

        -- เริ่มรอบใหม่หลังจากทำงานเสร็จ
        wait(1)

        -- ฟังก์ชันสำหรับดึงจำนวนของไอเท็มที่ระบุ
        local function getItemAmount(itemName)
            local item = player.Inventory:FindFirstChild(itemName)
            return item and item.Value or 0
        end

        -- ตัวแปรที่ใช้ตรวจสอบว่าได้ทำการเทเลพอร์ตแล้วหรือยัง
        local teleportedItems = {
            noTeleported = false,
            aTeleported = false,
            noETeleported = false,
            ABCD = false,
            ABCDF = false,
            ABCDFGH = false,
            ABCDFG = false,
            ABCDFGO = false,
            ABCDFGOP = false
        }

        -- ตารางข้อมูลสำหรับไอเท็มและพิกัดการเทเลพอร์ต
        local teleportLocations = {
            {name = "Cabbage", amount = 60, cframe = CFrame.new(-2960, 33, 92), flag = "noTeleported"},
            {name = "Banana", amount = 50, cframe = CFrame.new(3426, 33, -227), flag = "aTeleported"},
            {name = "Strawberry", amount = 60, cframe = CFrame.new(3409, 35, 2087), flag = "noETeleported"},
            {name = "Apple", amount = 60, cframe = CFrame.new(2379, 37, 3164), flag = "ABCD"},
            {name = "Orange", amount = 60, cframe = CFrame.new(4174, 34, 3484), flag = "ABCDF"},
            {name = "Meat", amount = 60, cframe = CFrame.new(-4784, 33, 1391), flag = "ABCDFGH"},
            {name = "Wood", amount = 60, cframe = CFrame.new(2061, 21, -406), flag = "ABCDFG"},
            {name = "Rice", amount = 60, cframe = CFrame.new(-2533, 13, 5159), flag = "ABCDFGO"},
            {name = "Oil", amount = 60, cframe = CFrame.new(857, 35, 3338), flag = "ABCDFGOP"}
        }

        -- ฟังก์ชันสำหรับขายไอเท็ม
        local function sellItem(itemName, amount)
            local args = {itemName, tostring(amount)}
            game:GetService("ReplicatedStorage"):WaitForChild("WorldMarket_Remotes"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
        end

        -- ลูปหลัก
        while true do
            for _, teleportData in ipairs(teleportLocations) do
                local itemAmount = getItemAmount(teleportData.name)
                if itemAmount >= teleportData.amount and not teleportedItems[teleportData.flag] then
                    humanoidRootPart.CFrame = teleportData.cframe -- เทเลพอร์ตไปที่พิกัดที่ระบุ
                    teleportedItems[teleportData.flag] = true -- อัปเดตสถานะการเทเลพอร์ต
                end
                wait(0.5)
            end

            -- ตรวจสอบว่าได้เทเลพอร์ตไปพิกัดสุดท้ายแล้วหรือไม่
            if teleportedItems["ABCDFGOP"] then
                -- รันคำสั่งขายไอเท็ม
                sellItem("Watermelon", 60)
                sellItem("Apple", 60)
                sellItem("Strawberry", 60)
                sellItem("Orange", 60)
                sellItem("Wood", 60)
                sellItem("Banana", 50)
                sellItem("Meat", 60)
                sellItem("Cabbage", 60)
                sellItem("Rice", 60)
                sellItem("Oil", 60)
                break -- ออกจากลูปเมื่อทุกเงื่อนไขถูกต้อง
            end

            wait(1) -- ดีเลย์เล็กน้อยเพื่อป้องกันการใช้ CPU สูงเกินไป
        end
    end
end

-- เรียกใช้ฟังก์ชันหลัก
mainLoop()
local hitboxMagnitude = 500 -- ระยะการตีที่ต้องการ

-- ฟังก์ชันในการขยายระยะการตี
local function setHitboxMagnitude(player)
    if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local humanoidRootPart = player.Character.HumanoidRootPart
        local originalSize = humanoidRootPart.Size
        humanoidRootPart.Size = Vector3.new(hitboxMagnitude, originalSize.Y, hitboxMagnitude)
    end
end

-- ขยายระยะการตีสำหรับผู้เล่นทุกคนที่มีอยู่
for _, player in pairs(game.Players:GetPlayers()) do
    setHitboxMagnitude(player)
end

-- ตรวจสอบเมื่อมีผู้เล่นใหม่เข้ามา และขยายระยะการตีให้ด้วย
game.Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        setHitboxMagnitude(player)
    end)
end)

wait(1)
-- ฟังก์ชันหลักสำหรับทำงานต่าง ๆ
local function mainLoop()
    while true do
        local args = {
            [1] = "Support Gacha",
            [2] = 20
        }

        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Gacha"):InvokeServer(unpack(args))
        wait(0.5)

        args = {
            [1] = "GachaCar250kg.",
            [2] = 20
        }

        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Gacha"):InvokeServer(unpack(args))
        wait(0.5)

        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        humanoidRootPart.CFrame = CFrame.new(-1658, 42, 2338)
        wait(1.5)

        args = {
            [1] = "10000",
            [2] = "Withdraw"
        }

        game:GetService("ReplicatedStorage"):WaitForChild("BankingRemotes"):WaitForChild("MainRemote"):FireServer(unpack(args))

        wait(1.5)
        humanoidRootPart.CFrame = CFrame.new(-3184, 34, 3234)
        wait(1.5)

        local args = {
    [1] = "Pickaxe",
    [2] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
local args = {
    [1] = "Sickle",
    [2] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
local args = {
    [1] = "Axe",
    [2] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
local args = {
    [1] = "Jackhammer",
    [2] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
local args = {
    [1] = "Cleaver",
    [2] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
local args = {
            [1] = "Basket",
            [2] = 1
        }
        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))

        humanoidRootPart.CFrame = CFrame.new(4855, 34, 897)
        wait(0.5)

        -- เริ่มรอบใหม่หลังจากทำงานเสร็จ
        wait(1)

        -- ฟังก์ชันสำหรับดึงจำนวนของไอเท็มที่ระบุ
        local function getItemAmount(itemName)
            local item = player.Inventory:FindFirstChild(itemName)
            return item and item.Value or 0
        end

        -- ตัวแปรที่ใช้ตรวจสอบว่าได้ทำการเทเลพอร์ตแล้วหรือยัง
        local teleportedItems = {
            noTeleported = false,
            aTeleported = false,
            noETeleported = false,
            ABCD = false,
            ABCDF = false,
            ABCDFGH = false,
            ABCDFG = false,
            ABCDFGO = false,
            ABCDFGOP = false
        }

        -- ตารางข้อมูลสำหรับไอเท็มและพิกัดการเทเลพอร์ต
        local teleportLocations = {
            {name = "Cabbage", amount = 60, cframe = CFrame.new(-2960, 33, 92), flag = "noTeleported"},
            {name = "Banana", amount = 50, cframe = CFrame.new(3426, 33, -227), flag = "aTeleported"},
            {name = "Strawberry", amount = 60, cframe = CFrame.new(3409, 35, 2087), flag = "noETeleported"},
            {name = "Apple", amount = 60, cframe = CFrame.new(2379, 37, 3164), flag = "ABCD"},
            {name = "Orange", amount = 60, cframe = CFrame.new(4174, 34, 3484), flag = "ABCDF"},
            {name = "Meat", amount = 60, cframe = CFrame.new(-4784, 33, 1391), flag = "ABCDFGH"},
            {name = "Wood", amount = 60, cframe = CFrame.new(2061, 21, -406), flag = "ABCDFG"},
            {name = "Rice", amount = 60, cframe = CFrame.new(-2533, 13, 5159), flag = "ABCDFGO"},
            {name = "Oil", amount = 60, cframe = CFrame.new(857, 35, 3338), flag = "ABCDFGOP"}
        }

        -- ฟังก์ชันสำหรับขายไอเท็ม
        local function sellItem(itemName, amount)
            local args = {itemName, tostring(amount)}
            game:GetService("ReplicatedStorage"):WaitForChild("WorldMarket_Remotes"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
        end

        -- ลูปหลัก
        while true do
            for _, teleportData in ipairs(teleportLocations) do
                local itemAmount = getItemAmount(teleportData.name)
                if itemAmount >= teleportData.amount and not teleportedItems[teleportData.flag] then
                    humanoidRootPart.CFrame = teleportData.cframe -- เทเลพอร์ตไปที่พิกัดที่ระบุ
                    teleportedItems[teleportData.flag] = true -- อัปเดตสถานะการเทเลพอร์ต
                end
                wait(0.5)
            end

            -- ตรวจสอบว่าได้เทเลพอร์ตไปพิกัดสุดท้ายแล้วหรือไม่
            if teleportedItems["ABCDFGOP"] then
                -- รันคำสั่งขายไอเท็ม
                sellItem("Watermelon", 60)
                sellItem("Apple", 60)
                sellItem("Strawberry", 60)
                sellItem("Orange", 60)
                sellItem("Wood", 60)
                sellItem("Banana", 50)
                sellItem("Meat", 60)
                sellItem("Cabbage", 60)
                sellItem("Rice", 60)
                sellItem("Oil", 60)
                break -- ออกจากลูปเมื่อทุกเงื่อนไขถูกต้อง
            end

            wait(1) -- ดีเลย์เล็กน้อยเพื่อป้องกันการใช้ CPU สูงเกินไป
        end
    end
end

-- ดึงข้อมูลผู้เล่นที่รันสคริปต์
local player = game:GetService("Players").LocalPlayer
local hitboxMagnitude = 500 -- ระยะการตีที่ต้องการ

-- ฟังก์ชันในการขยายระยะการตี
local function setHitboxMagnitude(player)
    if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local humanoidRootPart = player.Character.HumanoidRootPart
        local originalSize = humanoidRootPart.Size
        humanoidRootPart.Size = Vector3.new(hitboxMagnitude, originalSize.Y, hitboxMagnitude)
    end
end

-- ขยายระยะการตีสำหรับผู้เล่นทุกคนที่มีอยู่
for _, otherPlayer in pairs(game.Players:GetPlayers()) do
    setHitboxMagnitude(otherPlayer)
end

-- ตรวจสอบเมื่อมีผู้เล่นใหม่เข้ามา และขยายระยะการตีให้ด้วย
game.Players.PlayerAdded:Connect(function(newPlayer)
    newPlayer.CharacterAdded:Connect(function()
        setHitboxMagnitude(newPlayer)
    end)
end)

-- ทำงานทุก 10 วินาที
while true do
    wait(10)  -- รอ 10 วินาที

    -- เช็คสถานะ Shield และใช้งาน Tea
    if player and player.Status and player.Status.Shield and player.Status.Shield.Value > 50 then
        local args = {
            [1] = "Use",
            [2] = "Tea"
        }
        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
    end

    -- เช็คสถานะ Thirsty และใช้งาน Water
    if player and player.Status and player.Status.Thirsty and player.Status.Thirsty.Value < 50 then
        local args = {
            [1] = "Use",
            [2] = "Water"
        }
        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
    end

    -- เช็คสถานะ Hunger และใช้งาน Bread
    if player and player.Status and player.Status.Hunger and player.Status.Hunger.Value < 50 then
        local args = {
            [1] = "Use",
            [2] = "Bread"
        }
        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
    end
end
local hitboxMagnitude = 500 -- ระยะการตีที่ต้องการ

-- ฟังก์ชันในการขยายระยะการตี
local function setHitboxMagnitude(player)
    if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local humanoidRootPart = player.Character.HumanoidRootPart
        local originalSize = humanoidRootPart.Size
        humanoidRootPart.Size = Vector3.new(hitboxMagnitude, originalSize.Y, hitboxMagnitude)
    end
end

-- ขยายระยะการตีสำหรับผู้เล่นทุกคนที่มีอยู่
for _, player in pairs(game.Players:GetPlayers()) do
    setHitboxMagnitude(player)
end

-- ตรวจสอบเมื่อมีผู้เล่นใหม่เข้ามา และขยายระยะการตีให้ด้วย
game.Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        setHitboxMagnitude(player)
    end)
end)

end)
-- แท็บ Helper สำหรับเลือกผู้เล่นและฝากเงิน
local TabHelper = Window:NewTab("Helper")
local SectionHelper = TabHelper:NewSection("Helper")

-- สร้าง Dropdown สำหรับเลือกผู้เล่น
local selectedPlayer = nil
local playersList = {}

-- ฟังก์ชันในการอัปเดตรายชื่อผู้เล่น
local function updatePlayersList()
    playersList = {}
    for _, player in pairs(game:GetService("Players"):GetPlayers()) do
        table.insert(playersList, player.Name)
    end
end

-- เรียกอัปเดตรายชื่อผู้เล่นเมื่อเริ่มต้น
updatePlayersList()

-- Dropdown เลือกผู้เล่น
SectionHelper:NewDropdown("เลือกผู้เล่น", "เลือกผู้เล่นเพื่อปฏิสัมพันธ์", playersList, function(selected)
    selectedPlayer = selected
    print("Selected Player: " .. selectedPlayer)
end)

-- ปุ่มสำหรับดำเนินการบางอย่างกับผู้เล่นที่เลือก
SectionHelper:NewButton("ดำเนินการกับผู้เล่น", "ทำบางอย่างกับผู้เล่นที่เลือก", function()
    if selectedPlayer then
        local player = game:GetService("Players"):FindFirstChild(selectedPlayer)
        if player then
            -- ใส่ฟังก์ชันที่ต้องการทำกับผู้เล่น
            print("ทำบางอย่างกับผู้เล่น: " .. player.Name)
        else
            print("ไม่พบผู้เล่นที่เลือก")
        end
    else
        print("ยังไม่ได้เลือกผู้เล่น")
    end
end)

-- ส่วนการกรอกและฝากเงิน
local depositAmount = "0"

-- สร้าง TextBox ให้ผู้เล่นกรอกจำนวนเงินที่ต้องการฝาก
SectionHelper:NewTextBox("Deposit Money", "Amount to be deposited", function(value)
    depositAmount = value -- เก็บค่าที่ผู้เล่นกรอก
    print("Amount of money: " .. depositAmount)
end)

-- ปุ่มฝากเงิน
SectionHelper:NewButton("Deposit Money", "Click to deposit money", function()
    if tonumber(depositAmount) and tonumber(depositAmount) > 0 then
        local args = {
            [1] = tostring(depositAmount), -- ใช้จำนวนเงินที่ผู้เล่นกรอกเป็นข้อความ
            [2] = "Deposit"
        }

        local BankingRemotes = game:GetService("ReplicatedStorage"):WaitForChild("BankingRemotes")
        local MainRemote = BankingRemotes:WaitForChild("MainRemote")

        if MainRemote then
            MainRemote:FireServer(unpack(args)) -- เรียกใช้งาน RemoteEvent
            print("ทำการฝากเงิน: " .. depositAmount .. " บาท")
        else
            print("ไม่พบ RemoteEvent ที่ใช้ในการฝากเงิน")
        end
    else
        print("กรุณากรอกจำนวนเงินที่ถูกต้อง (ต้องมากกว่า 0)")
    end
end)

-- ส่วนการกรอกและฝากเงิน
local ezAmount = "0"

-- สร้าง TextBox ให้ผู้เล่นกรอกจำนวนเงินที่ต้องการฝาก
SectionHelper:NewTextBox("Withdraw Money", "Amount to be deposited", function(value)
    ezAmount = value -- เก็บค่าที่ผู้เล่นกรอก
    print("Amount of money: " .. ezAmount)
end)

SectionHelper:NewButton("Withdraw Money", "Click to deposit money", function()
if tonumber(ezAmount) and tonumber(ezAmount) > 0 then
        local args = {
            [1] = tostring(ezAmount), -- ใช้จำนวนเงินที่ผู้เล่นกรอกเป็นข้อความ
            [2] = "Withdraw"
        }

        local BankingRemotes = game:GetService("ReplicatedStorage"):WaitForChild("BankingRemotes")
        local MainRemote = BankingRemotes:WaitForChild("MainRemote")

        if MainRemote then
            MainRemote:FireServer(unpack(args)) -- เรียกใช้งาน RemoteEvent
            print("ทำการฝากเงิน: " .. depositAmount .. " บาท")
        else
            print("ไม่พบ RemoteEvent ที่ใช้ในการฝากเงิน")
        end
    else
        print("กรุณากรอกจำนวนเงินที่ถูกต้อง (ต้องมากกว่า 0)")
    end
end)
SectionFarmKaitun:NewButton("eat auto every", "ButtonInfo", function()
-- ดึงข้อมูลผู้เล่นที่รันสคริปต์
local player = game:GetService("Players").LocalPlayer

while true do
    wait(10)  -- รอ 10 วินาที

    -- เช็คสถานะ Shield และใช้งาน Tea
    if player and player.Status and player.Status.Shield and player.Status.Shield.Value > 50 then
        local args = {
            [1] = "Use",
            [2] = "Tea"
        }
        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
    end

    -- เช็คสถานะ Thirsty และใช้งาน Water
    if player and player.Status and player.Status.Thirsty and player.Status.Thirsty.Value < 50 then
        local args = {
            [1] = "Use",
            [2] = "Water"
        }
        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
    end

    -- เช็คสถานะ Hunger และใช้งาน Bread
    if player and player.Status and player.Status.Hunger and player.Status.Hunger.Value < 50 then
        local args = {
            [1] = "Use",
            [2] = "Bread"
        }
        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
    end
end

end)

-- เพิ่มการตั้งค่าระยะการตีและความเร็วในการเดินใน Helper
local hitboxMagnitude = 0 -- ระยะการตีเริ่มต้น
local walkSpeed = 16 -- ความเร็วในการเดินเริ่มต้น

local function setHitboxMagnitude(player, magnitude)
    if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local humanoidRootPart = player.Character.HumanoidRootPart
        local originalSize = humanoidRootPart.Size
        humanoidRootPart.Size = Vector3.new(magnitude, originalSize.Y, magnitude)
    end
end

local function setWalkSpeed(player, speed)
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        local humanoid = player.Character.Humanoid
        humanoid.WalkSpeed = speed
    end
end

-- Slider สำหรับเลือกระยะการตี
SectionHelper:NewSlider("เลือกระยะการตี", 100, 1000, hitboxMagnitude, function(value)
    hitboxMagnitude = value
    for _, player in pairs(game.Players:GetPlayers()) do
        setHitboxMagnitude(player, hitboxMagnitude)
    end
end)

-- Slider สำหรับปรับความเร็วในการเดิน
SectionHelper:NewSlider("ปรับความเร็วในการเดิน", 16, 1000, walkSpeed, function(value)
    walkSpeed = value
    for _, player in pairs(game.Players:GetPlayers()) do
        setWalkSpeed(player, walkSpeed)
    end
end)

-- ปุ่มสำหรับเดินทะลุ
SectionHelper:NewButton("เดินทะลุ", "เดินทะลุสิ่งกีดขวาง", function()
    local RunService = game:GetService("RunService")
local character = game.Players.LocalPlayer.Character

-- ปิดการชนของทุกชิ้นส่วนของตัวละคร
local function disableCollisions()
    for _, part in pairs(character:GetChildren()) do
        if part:IsA("BasePart") then
            part.CanCollide = false
        end
    end
end

-- รันฟังก์ชันทุกเฟรม
RunService.RenderStepped:Connect(disableCollisions)

end)
SectionHelper:NewButton("Respawn", "Respawn", function()
    local args = {
    [1] = "Respawn",
    [2] = game:GetService("Players").LocalPlayer
}

game:GetService("ReplicatedStorage"):WaitForChild("ReviveSystem"):WaitForChild("Event"):FireServer(unpack(args))
end)
