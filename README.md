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


local args = {
    [1] = "Support Gacha",
    [2] = 20
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Gacha"):InvokeServer(unpack(args))
wait(0.5)
local args = {
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
local args = {
    [1] = "10000",
    [2] = "Withdraw"
}

game:GetService("ReplicatedStorage"):WaitForChild("BankingRemotes"):WaitForChild("MainRemote"):FireServer(unpack(args))

wait(1.5)
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

humanoidRootPart.CFrame = CFrame.new(-3184, 34, 3234)
wait(1.5)
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

humanoidRootPart.CFrame = CFrame.new(-3184, 34, 3234)

local args = {
    [1] = "Pickaxe",
    [2] = 1
}
wait(1)
game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
wait(1)
local args = {
    [1] = "Iphone",
    [2] = 1
}

local args = {
            [1] = "Basket",
            [2] = 1
        }
        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
wait(1)

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
wait(1)
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

humanoidRootPart.CFrame = CFrame.new(-4540, 38, -227)
wait(0.5)
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

humanoidRootPart.CFrame = CFrame.new(-4540, 38, -227)
wait(2.5)
local args = {
    [1] = "Update",
    [2] = {
        ["7"] = "Pickaxe"
    }
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("UpdateSlot"):FireServer(unpack(args))
wait(2)
local args = {
    [1] = "Use",
    [2] = "Pickaxe"
}
game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
local player = game:GetService("Players").LocalPlayer

local args = {
    [1] = "Use",
    [2] = "Basket"
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))

-- สร้าง loop เพื่อให้ทำงานทุก 10 วินาที
while true do
    local stoneAmount = player.Inventory:FindFirstChild("Stone").Value  -- ตรวจสอบจำนวนหิน

    if stoneAmount >= 60 then  -- ถ้าจำนวนหินครบ 60 หรือมากกว่า
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ย้ายผู้เล่นไปที่ตำแหน่งที่ต้องการ
        humanoidRootPart.CFrame = CFrame.new(4855, 34, 897)
        wait(0.5)
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ย้ายผู้เล่นไปที่ตำแหน่งที่ต้องการ
        humanoidRootPart.CFrame = CFrame.new(4855, 34, 897)
        wait(0.5)

        -- ส่งคำสั่งซื้อสินค้า

        break  -- ออกจาก loop เมื่อทำการซื้อสินค้าแล้ว
    else
        print("ยังไม่ครบ 60 หิน")
    end

    wait(10)  -- รอ 10 วินาทีก่อนตรวจสอบอีกครั้ง
    wait(0.25)
local args = {
    [1] = "Update",
    [2] = {
        ["6"] = "Basket"
    }
}

end
-- สร้าง loop เพื่อให้ทำงานทุก 10 วินาที
while true do
    local CabbageAmount = player.Inventory:FindFirstChild("Cabbage").Value  -- ตรวจสอบจำนวนหิน

    if CabbageAmount >= 60 then  -- ถ้าจำนวนหินครบ 60 หรือมากกว่า
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ย้ายผู้เล่นไปที่ตำแหน่งที่ต้องการ
        humanoidRootPart.CFrame = CFrame.new(-2960, 33, 92)
        wait(0.5)
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ย้ายผู้เล่นไปที่ตำแหน่งที่ต้องการ
        humanoidRootPart.CFrame = CFrame.new(-2960, 33, 92)
        wait(0.5)


        break  -- ออกจาก loop เมื่อทำการซื้อสินค้าแล้ว
    else
        print("ยังไม่ครบ 60 หิน")
    end
    

    wait(10)  -- รอ 10 วินาทีก่อนตรวจสอบอีกครั้ง
    wait(0.25)
local args = {
    [1] = "Update",
    [2] = {
        ["6"] = "Basket"
    }
}

end
-- สร้าง loop เพื่อให้ทำงานทุก 10 วินาที
while true do
    local BananaAmount = player.Inventory:FindFirstChild("Banana").Value  -- ตรวจสอบจำนวนหิน

    if BananaAmount >= 50 then  -- ถ้าจำนวนหินครบ 60 หรือมากกว่า
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ย้ายผู้เล่นไปที่ตำแหน่งที่ต้องการ
        humanoidRootPart.CFrame = CFrame.new(3426, 33, -227)
        wait(0.5)
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ย้ายผู้เล่นไปที่ตำแหน่งที่ต้องการ
        humanoidRootPart.CFrame = CFrame.new(3426, 33, -227)
        wait(0.5)

        -- ส่งคำสั่งซื้อสินค้า

        break  -- ออกจาก loop เมื่อทำการซื้อสินค้าแล้ว
    else
        print("ยังไม่ครบ 60 หิน")
    end
    

    wait(10)  -- รอ 10 วินาทีก่อนตรวจสอบอีกครั้ง
    wait(0.25)
local args = {
    [1] = "Update",
    [2] = {
        ["6"] = "Basket"
    }
}

end
-- สร้าง loop เพื่อให้ทำงานทุก 10 วินาที
while true do
    local StrawberryAmount = player.Inventory:FindFirstChild("Strawberry").Value  -- ตรวจสอบจำนวนหิน

    if StrawberryAmount >= 60 then  -- ถ้าจำนวนหินครบ 60 หรือมากกว่า
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ย้ายผู้เล่นไปที่ตำแหน่งที่ต้องการ
        humanoidRootPart.CFrame = CFrame.new(6156, 34, -470)
        wait(0.5)
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ย้ายผู้เล่นไปที่ตำแหน่งที่ต้องการ
        humanoidRootPart.CFrame = CFrame.new(6156, 34, -470)
        wait(0.5)

        -- ส่งคำสั่งซื้อสินค้า

        break  -- ออกจาก loop เมื่อทำการซื้อสินค้าแล้ว
    else
        print("ยังไม่ครบ 60 หิน")
    end

    wait(10)  -- รอ 10 วินาทีก่อนตรวจสอบอีกครั้ง
    wait(0.25)
local args = {
    [1] = "Update",
    [2] = {
        ["6"] = "Basket"
    }
}

end
-- สร้าง loop เพื่อให้ทำงานทุก 10 วินาที
while true do
    local WatermelonAmount = player.Inventory:FindFirstChild("Watermelon").Value  -- ตรวจสอบจำนวนหิน

    if WatermelonAmount >= 60 then  -- ถ้าจำนวนหินครบ 60 หรือมากกว่า
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ย้ายผู้เล่นไปที่ตำแหน่งที่ต้องการ
        humanoidRootPart.CFrame = CFrame.new(3409, 35, 2087)
        wait(0.5)
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ย้ายผู้เล่นไปที่ตำแหน่งที่ต้องการ
        humanoidRootPart.CFrame = CFrame.new(3409, 35, 2087)
        wait(0.5)

        -- ส่งคำสั่งซื้อสินค้า

        break  -- ออกจาก loop เมื่อทำการซื้อสินค้าแล้ว
    else
        print("ยังไม่ครบ 60 หิน")
    end

    wait(10)  -- รอ 10 วินาทีก่อนตรวจสอบอีกครั้ง
    wait(0.25)
local args = {
    [1] = "Update",
    [2] = {
        ["6"] = "Basket"
    }
}

end
-- สร้าง loop เพื่อให้ทำงานทุก 10 วินาที
while true do
    local AppleAmount = player.Inventory:FindFirstChild("Apple").Value  -- ตรวจสอบจำนวนหิน

    if AppleAmount >= 60 then  -- ถ้าจำนวนหินครบ 60 หรือมากกว่า
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ย้ายผู้เล่นไปที่ตำแหน่งที่ต้องการ
        humanoidRootPart.CFrame = CFrame.new(2899, 40, -840)
        wait(0.5)
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ย้ายผู้เล่นไปที่ตำแหน่งที่ต้องการ
        humanoidRootPart.CFrame = CFrame.new(2899, 40, -840)
        wait(0.5)

        -- ส่งคำสั่งซื้อสินค้า

        break  -- ออกจาก loop เมื่อทำการซื้อสินค้าแล้ว
    else
        print("ยังไม่ครบ 60 หิน")
    end

    wait(10)  -- รอ 10 วินาทีก่อนตรวจสอบอีกครั้ง
    wait(0.25)
local args = {
    [1] = "Update",
    [2] = {
        ["6"] = "Basket"
    }
}

end

