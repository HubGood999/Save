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

-- แท็บ Farm Normal
local TabFarm = Window:NewTab("Farm Normal")
local SectionFarmNormal = TabFarm:NewSection("Farm Normal")
SectionFarmNormal:NewButton("", "ButtonInfo", function()
    print("Clicked")
end)

-- แท็บ Farm Kaitun
local TabFarmKaitun = Window:NewTab("Farm kaitun")
local SectionFarmKaitun = TabFarmKaitun:NewSection("Farm kaitun")
SectionFarmKaitun:NewButton("Clicked to Farmkaitun", "ButtonInfo", function()
    print("Clicked")
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

-- เพิ่มการตั้งค่าระยะการตีและความเร็วในการเดินใน Helper
local hitboxMagnitude = 500 -- ระยะการตีเริ่มต้น
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
