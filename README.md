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
