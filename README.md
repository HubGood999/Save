-- สร้าง UI เดิม
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local TextBox = Instance.new("TextBox")
local UICorner = Instance.new("UICorner")
local ImageLabel = Instance.new("ImageLabel")
local UICorner_2 = Instance.new("UICorner")
local SubmitButton = Instance.new("TextButton")
local UICorner_3 = Instance.new("UICorner")
local EnterKeyButton = Instance.new("TextButton")
local UICorner_5 = Instance.new("UICorner")

-- Properties
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Frame.BorderColor3 = Color3.fromRGB(0, 0, 0)
Frame.BorderSizePixel = 0
Frame.Position = UDim2.new(0.363154203, 0, 0.372076035, 0)
Frame.Size = UDim2.new(0, 390, 0, 218)

TextBox.Parent = Frame
TextBox.BackgroundColor3 = Color3.fromRGB(25, 232, 255)
TextBox.BorderColor3 = Color3.fromRGB(0, 0, 0)
TextBox.BorderSizePixel = 0
TextBox.Position = UDim2.new(0.226871744, 0, 0.542553127, 0)
TextBox.Size = UDim2.new(0, 200, 0, 32)
TextBox.Font = Enum.Font.SourceSans
TextBox.Text = ""
TextBox.TextColor3 = Color3.fromRGB(0, 0, 0)
TextBox.TextSize = 14.000

UICorner.Parent = TextBox

ImageLabel.Parent = Frame
ImageLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ImageLabel.BackgroundTransparency = 1.000
ImageLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
ImageLabel.BorderSizePixel = 0
ImageLabel.Size = UDim2.new(0, 100, 0, 100)
ImageLabel.Image = "http://www.roblox.com/asset/?id=80978555660719"

UICorner_2.Parent = ImageLabel

SubmitButton.Parent = Frame
SubmitButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
SubmitButton.BackgroundTransparency = 0
SubmitButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
SubmitButton.BorderSizePixel = 0
SubmitButton.Position = UDim2.new(0.02, 0, 0.82, 0)
SubmitButton.Size = UDim2.new(0, 150, 0, 40)
SubmitButton.Font = Enum.Font.Bangers
SubmitButton.Text = "Submit"
SubmitButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SubmitButton.TextSize = 14.000

UICorner_3.Parent = SubmitButton

EnterKeyButton.Parent = Frame
EnterKeyButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
EnterKeyButton.BackgroundTransparency = 1.000
EnterKeyButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
EnterKeyButton.BorderSizePixel = 0
EnterKeyButton.Position = UDim2.new(0.226871744, 0, 0.3, 0)
EnterKeyButton.Size = UDim2.new(0, 200, 0, 32)
EnterKeyButton.Font = Enum.Font.SourceSans
EnterKeyButton.Text = "Enter your key here"
EnterKeyButton.TextColor3 = Color3.fromRGB(255, 0, 0)
EnterKeyButton.TextSize = 14.000

UICorner_5.Parent = EnterKeyButton

-- สร้างสคริปต์ตรวจสอบคีย์
local function checkKey()
    local key = TextBox.Text
    if key == "กั้กเน่า" then
        -- ลบ UI เดิม
        ScreenGui:Destroy()
        
        -- รันสคริปต์หลังจากคีย์ผ่านแล้ว
        local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
        local Window = Library.CreateLib("NOOB HUB", "DarkTheme")

        -- แท็บและ Section สำหรับการเลือกผู้เล่น
        local PlayerTab = Window:NewTab("ผู้เล่น")
        local PlayerSection = PlayerTab:NewSection("เลือกผู้เล่น!")

        -- สร้างรายการของผู้เล่น
        Plr = {}
        for i, v in pairs(game:GetService("Players"):GetChildren()) do
            table.insert(Plr, v.Name) 
        end

        -- สร้าง dropdown สำหรับเลือกผู้เล่น
        local drop = PlayerSection:NewDropdown("เลือกผู้เล่น!", "คลิกเพื่อเลือก", Plr, function(t)
            PlayerTP = t
        end)

        -- ปุ่มสำหรับการ TP ไปยังผู้เล่นที่เลือก
        PlayerSection:NewButton("คลิกเพื่อ TP", "", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[PlayerTP].Character.HumanoidRootPart.CFrame
        end)

        -- Toggle สำหรับ TP อัตโนมัติ
        PlayerSection:NewToggle("TP อัตโนมัติ", "", function(t)
            _G.TPPlayer = t
            while _G.TPPlayer do
                wait()
                if PlayerTP then
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[PlayerTP].Character.HumanoidRootPart.CFrame
                end
            end
        end)

        -- ปุ่มรีเฟรช dropdown
        PlayerSection:NewButton("รีเฟรชรายการผู้เล่น", "รีเฟรชรายการผู้เล่น", function()
            drop:Refresh(Plr)
        end)

        -- แท็บและ Section สำหรับการไปที่ตำแหน่งต่างๆ
        local AirDropTab = Window:NewTab("ฟังก์ชัน")
        local AirDropSection = AirDropTab:NewSection("ฟังก์ชัน")

        -- ฟังก์ชันสำหรับการใช้งาน item
        local function useItem(slotNumber)
            local args = {
                [1] = "Use",
                [2] = slotNumber
            }

            -- เรียกใช้งาน RemoteEvent ใน ReplicatedStorage
            local replicatedStorage = game:GetService("ReplicatedStorage")
            local remote = replicatedStorage:WaitForChild("Remote"):WaitForChild("UpdateSlot")

            -- ส่งข้อมูลไปยังเซิร์ฟเวอร์
            remote:FireServer(unpack(args))
        end

        -- ฟังก์ชันสำหรับขายไอเทม
        local function sellItems()
            local items = {"Gold", "Diamond", "Meat", "Scrap", "Steel", "Wood"}
            for _, item in ipairs(items) do
                local args = {
                    [1] = item,
                    [2] = "1"
                }
                game:GetService("ReplicatedStorage"):WaitForChild("WorldMarket_Remotes"):WaitForChild("RemoteEvent"):FireServer(unpack(args))
            end
        end

        -- ฟังก์ชันสำหรับไปที่ตำแหน่งต่างๆ
        local function teleportToPosition(position)
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(position)
        end

        -- ฟังก์ชันสำหรับการไปที่ตำแหน่งของแต่ละฟังก์ชัน
        local function autoTeleport(position, useItemSlot)
            teleportToPosition(position)
            if useItemSlot then
                useItem(useItemSlot)
            end
        end

        -- สร้างปุ่มและ Toggle สำหรับการไปที่ตำแหน่งต่างๆ

        -- ตำแหน่งคราฟ
        local craftPosition = Vector3.new(2247, -21, -6240)
        AirDropSection:NewButton("ไปที่ตำแหน่งคราฟ", "", function()
            autoTeleport(craftPosition)
        end)
        AirDropSection:NewToggle("ไปที่ตำแหน่งคราฟอัตโนมัติ", "", function(t)
            _G.AutoCraft = t
            while _G.AutoCraft do
                wait()
                autoTeleport(craftPosition)
            end
        end)

        -- ตำแหน่งแต่งสีรถ
        local paintPosition = Vector3.new(-1734, -20, -1495)
        AirDropSection:NewButton("ไปที่ตำแหน่งแต่งสีรถ", "", function()
            autoTeleport(paintPosition)
        end)
        AirDropSection:NewToggle("ไปที่ตำแหน่งแต่งสีรถอัตโนมัติ", "", function(t)
            _G.AutoPaint = t
            while _G.AutoPaint do
                wait()
                autoTeleport(paintPosition)
            end
        end)

        -- ตำแหน่งขุดเพชรม่วง
        local diamondPosition = Vector3.new(2575, -32, -7082)
        AirDropSection:NewButton("ไปที่ตำแหน่งขุดเพชรม่วง", "", function()
            autoTeleport(diamondPosition)
        end)
        AirDropSection:NewToggle("ไปที่ตำแหน่งขุดเพชรม่วงอัตโนมัติ", "", function(t)
            _G.AutoDiamond = t
            while _G.AutoDiamond do
                wait()
                autoTeleport(diamondPosition)
            end
        end)

        -- ตำแหน่งฟาร์มแอปเปิ้ล
        local applePosition = Vector3.new(-339, -21, -4625)
        AirDropSection:NewButton("ไปที่ตำแหน่งฟาร์มแอปเปิ้ล", "", function()
            autoTeleport(applePosition)
        end)
        AirDropSection:NewToggle("ไปที่ตำแหน่งฟาร์มแอปเปิ้ลอัตโนมัติ", "", function(t)
            _G.AutoApple = t
            while _G.AutoApple do
                wait()
                autoTeleport(applePosition)
            end
        end)

        -- ฟังก์ชันการขายของอัตโนมัติ
        AirDropSection:NewButton("ขายของ", "", function()
            sellItems()
        end)
        AirDropSection:NewToggle("ขายของอัตโนมัติ", "", function(t)
            _G.AutoSell = t
            while _G.AutoSell do
                wait()
                sellItems()
            end
        end)
    else
        game.Players.LocalPlayer:Kick("Invalid key!")
    end
end

-- กำหนดเหตุการณ์เมื่อผู้เล่นคลิกปุ่ม Submit
SubmitButton.MouseButton1Click:Connect(checkKey)
