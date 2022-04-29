-- Credits to Sy

print("1")
game.StarterGui:SetCore("SendNotification", {
    Title = "Bronze Tree";
    Text = "Feel the best Gamesense at Bronze Tree",
    Duration = 5
}) 
local library = {}

library.__index = library

function library:Tween(asset, info, thing)
    game:GetService("TweenService"):Create(asset, info, thing):Play()
end

function library:DropInfo(asset, info, tbl)
    if not tbl.debounce then
        tbl.debounce = true

        local newText = asset:FindFirstChild("Text"):Clone()
        newText.Parent = asset
        newText.Name = "Info"
        newText.TextTransparency = 1
        newText.TextSize = 24
        newText.Position = UDim2.new(asset:FindFirstChild("Text").Position.X.Scale, asset:FindFirstChild("Text").Position.X.Offset, ((asset:FindFirstChild("Text").Position.Y.Scale / 2) * 3), asset:FindFirstChild("Text").Position.Y.Offset)
        newText.Text = info

        local textAsset = asset:FindFirstChild("Text")

        library:Tween(asset, TweenInfo.new(0.5), {Size = UDim2.new(asset.Size.X.Scale, asset.Size.X.Offset, (asset.Size.Y.Scale * 2), asset.Size.Y.Offset)})
        library:Tween(textAsset, TweenInfo.new(0.5), {Position = UDim2.new(textAsset.Position.X.Scale, textAsset.Position.X.Offset, (textAsset.Position.Y.Scale / 2), textAsset.Position.Y.Offset), Size = UDim2.new(textAsset.Size.X.Scale, textAsset.Size.X.Offset, (textAsset.Size.Y.Scale / 2), textAsset.Size.Y.Offset)})
        library:Tween(asset["Down"], TweenInfo.new(0.3), {Rotation = 180, Position = UDim2.new(asset["Down"].Position.X.Scale, asset["Down"].Position.X.Offset, (asset["Down"].Position.Y.Scale / 2), asset["Down"].Position.Y.Offset)})
        wait(0.5)

        library:Tween(newText, TweenInfo.new(0.5), {TextTransparency = 0})

        wait(0.5)

        tbl.debounce = false
        tbl.showingInfo = true
    end
end

function library:RetractInfo(asset, tbl)
    if not tbl.debounce then
        tbl.debounce = true
        library:Tween(asset["Info"], TweenInfo.new(0.25), {TextTransparency = 1})
        library:Tween(asset["Down"], TweenInfo.new(0.3), {Rotation = 0, Position = UDim2.new(asset["Down"].Position.X.Scale, asset["Down"].Position.X.Offset, (asset["Down"].Position.Y.Scale * 2), asset["Down"].Position.Y.Offset)})
        library:Tween(asset, TweenInfo.new(0.5), {Size = UDim2.new(asset.Size.X.Scale, asset.Size.X.Offset, (asset.Size.Y.Scale / 2), asset.Size.Y.Offset)})	

        local textAsset = asset:FindFirstChild("Text")
        library:Tween(textAsset, TweenInfo.new(0.5), {Position = UDim2.new(textAsset.Position.X.Scale, textAsset.Position.X.Offset, (textAsset.Position.Y.Scale * 2), textAsset.Position.Y.Offset), Size = UDim2.new(textAsset.Size.X.Scale, textAsset.Size.X.Offset, (textAsset.Size.Y.Scale * 2), textAsset.Size.Y.Offset)})

        wait(0.5)
        asset["Info"]:Destroy()
        tbl.debounce = false
        tbl.showingInfo = false
    end
end

function library:RoundNumber(num, numDecimalPlaces)
    return tonumber(string.format("%." .. (numDecimalPlaces or 0) .. "f", num))
end

function library:Ripple(ui, button, x, y, tbl)
    --stole this from my old lib
    --[[
    spawn(function()
        local circle = ui.Circle:Clone()
        circle.Parent = button;
        local pos = UDim2.new(0,x-button.AbsolutePosition.X,0,y-button.AbsolutePosition.Y-36)
        circle.Position = pos
        circle.Size = UDim2.new(0,1,0,1)
        circle.ImageTransparency = .5

        local goal = {}
        goal.Size = UDim2.new((0.175)*7, 0, ((tbl and tbl.showingInfo == false and 2) or (tbl and tbl.showingInfo == true and 1))*7, 0)
        goal.ImageTransparency = 1

        local tween = game:GetService("TweenService"):Create(circle, TweenInfo.new(0.7,Enum.EasingStyle.Sine,Enum.EasingDirection.Out), goal)
        tween:Play()
        tween.Completed:Wait()
        circle:Destroy();
    end)--]]

    -- this is fresh code from a yt vid ik

    if x and y then
        spawn(function()
            local c = ui.Circle:Clone()
            c.Parent = button;

            c.ImageTransparency = 0.6

            local x, y = (x-button.AbsolutePosition.X), (y-button.AbsolutePosition.Y-36)
            c.Position = UDim2.new(0, x, 0, y)
            local len, size = 0.75, nil
            if button.AbsoluteSize.X >= button.AbsoluteSize.Y then
                size = (button.AbsoluteSize.X * 1.5)
            else
                size = (button.AbsoluteSize.Y * 1.5)
            end
            local tween = {}
            tween.Size = UDim2.new(0, size, 0, size)
            tween.Position = UDim2.new(0.5, (-size / 2), 0.5, (-size / 2))
            tween.ImageTransparency = 1

            local newTween = game:GetService("TweenService"):Create(c, TweenInfo.new(len, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), tween)

            newTween:Play()

            newTween.Completed:Wait()

            c:Destroy()
        end)
    end
end

function library.Create(title, titleUnder)
    local lib = {}

    lib.UI = game:GetObjects("rbxassetid://6849423853")[1]
    lib.UI.Parent = game.CoreGui

    lib.Tabs = {}

    lib.UI.Main.Left.UIName.Text = title
    lib.UI.Main.Left.GameName.Text = titleUnder

    local content, isReady = game.Players:GetUserThumbnailAsync(game.Players.LocalPlayer.UserId, Enum.ThumbnailType.HeadShot, Enum.ThumbnailSize.Size48x48)
    lib.UI.Main.Left.BottomLeft.Icon.Image = content
    lib.UI.Main.Left.BottomLeft.PlayerName.Text = game.Players.LocalPlayer.Name

    lib.Notifications = {}
    lib.Notifications.Queue = {}
    lib.Notifications.Current = nil

    local MainFrame = lib.UI.Main

    --Dragging
    local dragging
    local dragInput
    local dragStart
    local startPos

    local function update(input)
        local delta = input.Position - dragStart
        game:GetService("TweenService"):Create(MainFrame, TweenInfo.new(0.1), {Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)}):Play()
    end

    MainFrame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            startPos = MainFrame.Position

            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    MainFrame.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
            dragInput = input
        end
    end)

    game:GetService("UserInputService").InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            update(input)
        end
    end)

    return setmetatable(lib, library)
end

function library:Tab(name, imageId)
    local tab = {}

    tab.Assets = {}

    tab.Lib = self
    tab.Tab = self.UI.Main.Left.Container.Template:Clone()
    tab.Tab.Name = name
    tab.Tab.TabName.Text = name
    tab.Tab.Parent = self.UI.Main.Left.Container

    if imageId then
        tab.Tab.TabIcon.Image = "rbxassetid://" .. imageId
    end

    table.insert(self.Tabs, tab)

    tab.Show = function()
        tab.Tab.Visible = true
    end

    tab.Hide = function()
        tab.Tab.Visible = false
    end

    tab.Fix = function()
        self.UI.Main.Container.AutomaticCanvasSize = Enum.AutomaticSize.None
        self.UI.Main.Container.AutomaticCanvasSize = Enum.AutomaticSize.Y
    end

    local totalAssets = 0
    for i,v in pairs(self.Tabs) do
        totalAssets = totalAssets + 1
    end

    if totalAssets == 1 then
        -- first tab
        delay(0.1, function()
            for i,v in pairs(tab.Assets) do
                if v then
                    v.Show()
                end
            end
            library:Tween(tab.Tab, TweenInfo.new(0.5), {BackgroundTransparency = 0})
        end)
    end

    tab.Fix()

    tab.Tab.MouseButton1Up:Connect(function()
        for i,v in pairs(self.Tabs) do
            library:Tween(v.Tab, TweenInfo.new(0.5), {BackgroundTransparency = 1})
            for i,v in pairs(v.Assets) do
                v.Hide()
            end
        end

        for i,v in pairs(tab.Assets) do
            v.Show()
        end
        tab.Fix()
        library:Tween(tab.Tab, TweenInfo.new(0.5), {BackgroundTransparency = 0})
    end)

    tab.Show()

    return setmetatable(tab, library)
end

function library:Button(text, info, callback)
    local button = {}

    button.callback = callback or function() end
    button.debounce = false
    button.showingInfo = false
    button.button = self.Lib.UI.Main.Container.Button:Clone()
    button.button.Parent = self.Lib.UI.Main.Container
    button.button:FindFirstChild("Text").Text = (text or "No Text")
    button.button.Name = (text or "No Text")

    button.Show = function()
        button.button.Visible = true
    end

    button.Hide = function()
        button.button.Visible = false
    end

    button.button.Down.MouseButton1Up:Connect(function()
        if not button.showingInfo then
            library:DropInfo(button.button, info, button)
        else
            library:RetractInfo(button.button, button)
        end
    end)

    button.button.MouseButton1Up:Connect(function(x,y)
        if not button.debounce then
            library:Ripple(self.Lib.UI, button.button, x, y, button)
            button.callback()
        end
    end)

    table.insert(self.Assets, button)

    return setmetatable(button, library)
end

function library:Toggle(text, info, state, callback)
    local toggle = {}

    toggle.callback = callback or function() end
    toggle.debounce = false
    toggle.showingInfo = false
    toggle.state = state
    toggle.toggle = self.Lib.UI.Main.Container.Toggle:Clone()
    toggle.toggle.Parent = self.Lib.UI.Main.Container
    toggle.toggle:FindFirstChild("Text").Text = (text or "No Text")
    toggle.toggle.Name = (text or "No Text")

    toggle.Show = function()
        toggle.toggle.Visible = true
    end

    toggle.Hide = function()
        toggle.toggle.Visible = false
    end

    toggle.Refresh = function()
        if toggle.state then
            toggle.state = false
            toggle.debounce = true
            spawn(function()
                toggle.callback(toggle.state)
            end)
            local circle = toggle.toggle.Whole.Inner
            local newPosition = UDim2.new((circle.Position.X.Scale / 3), circle.Position.X.Offset, circle.Position.Y.Scale, circle.Position.Y.Offset)

            library:Tween(circle, TweenInfo.new(0.2), {Position = newPosition})
            library:Tween(circle.Parent, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(213, 213, 213)})

            wait(0.3)
            toggle.debounce = false
        else 
            toggle.state = true
            toggle.debounce = true
            spawn(function()
                toggle.callback(toggle.state)
            end)
            local circle = toggle.toggle.Whole.Inner
            local newPosition = UDim2.new((circle.Position.X.Scale * 3), circle.Position.X.Offset, circle.Position.Y.Scale, circle.Position.Y.Offset)

            library:Tween(circle, TweenInfo.new(0.2), {Position = newPosition})
            library:Tween(circle.Parent, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(0, 0, 0)})

            wait(0.3)
            toggle.debounce = false
        end
    end

    spawn(function()
        if toggle.state then
            toggle.debounce = true
            local circle = toggle.toggle.Whole.Inner
            local newPosition = UDim2.new((circle.Position.X.Scale * 3), circle.Position.X.Offset, circle.Position.Y.Scale, circle.Position.Y.Offset)

            library:Tween(circle, TweenInfo.new(0.2), {Position = newPosition})
            library:Tween(circle.Parent, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(0, 0, 0)})

            wait(0.3)
            toggle.debounce = false
        end
    end)

    toggle.toggle.Down.MouseButton1Up:Connect(function()
        if not toggle.showingInfo then
            library:DropInfo(toggle.toggle, info, toggle)
        else
            library:RetractInfo(toggle.toggle, toggle)
        end
    end)

    toggle.toggle.MouseButton1Up:Connect(function(x,y)
        if not toggle.debounce then
            library:Ripple(self.Lib.UI, toggle.toggle, x, y, toggle)
            toggle.Refresh()
        end
    end)

    local ran, failed = pcall(function()
        toggle.callback(toggle.state)
    end)

    if ran then
        print("Ran sucessfully.")
    else
        print("Failed to run but no worries!", failed)
    end

    table.insert(self.Assets, toggle)
    return setmetatable(toggle, library)
end

function library:Seperator()
    local seperator = {}

    seperator.asset = self.Lib.UI.Main.Container.Seperator:Clone()
    seperator.asset.Parent = self.Lib.UI.Main.Container

    seperator.Show = function()
        seperator.asset.Visible = true
    end

    seperator.Hide = function()
        seperator.asset.Visible = false
    end

    table.insert(self.Assets, seperator)
    return setmetatable(seperator, library)
end

function library:Slider(name, min, max, starting, callback)
    local slider = {}

    slider.callback = callback or function() end
    slider.min = min or 1
    slider.max = max or 100

    slider.asset = self.Lib.UI.Main.Container.Slider:Clone()
    slider.asset.Name = (name or "None")
    slider.asset:FindFirstChild("Slider").Text = (name or "None")
    slider.asset.Parent = self.Lib.UI.Main.Container
    slider.holdAsset = self.Lib.UI.Main.Container

    slider.holdAsset = slider.asset.Holder.Holder.Circle

    local mouse = game.Players.LocalPlayer:GetMouse()
    local uis = game:GetService("UserInputService")
    local Value;

    local bound = slider.holdAsset.Parent.Parent.AbsoluteSize.X
    
    function slider.Refresh(new, bool)
        local pos = (bound * (new/slider.max))

        library:Tween(slider.holdAsset.Parent, TweenInfo.new(0.1), {Size = UDim2.new(0, pos, 1, 0)})

        slider.asset.Percentage.Text = new
        
        if bool then
            slider.callback(new)
        end
    end
    
    slider.Refresh(starting)
    
    slider.holdAsset.MouseButton1Down:Connect(function()
        local Num = (((tonumber(slider.max) - tonumber(slider.min)) / bound) * slider.holdAsset.Parent.AbsoluteSize.X) + tonumber(slider.min)
        local IsDecimal = select(2, math.modf(starting)) ~= 0
        print(IsDecimal)
        Value = (not IsDecimal and math.ceil(Num)) or (IsDecimal and library:RoundNumber(Num, 1)) or 0
        pcall(function()
            slider.callback(Value)
        end)
        library:Tween(slider.holdAsset.Parent, TweenInfo.new(0.1), {Size = UDim2.new(0, math.clamp(mouse.X - slider.holdAsset.Parent.AbsolutePosition.X, 0, bound), 1, 0)})
        moveconnection = mouse.Move:Connect(function()
            slider.asset.Percentage.Text = Value
            local Num = (((tonumber(slider.max) - tonumber(slider.min)) / bound) * slider.holdAsset.Parent.AbsoluteSize.X) + tonumber(slider.min)
            local IsDecimal = select(2, math.modf(starting)) ~= 0
            Value = (not IsDecimal and math.ceil(Num)) or (IsDecimal and library:RoundNumber(Num, 1))
            pcall(function()
                slider.callback(Value)
            end)
            print((mouse.X - slider.holdAsset.Parent.AbsolutePosition.X))
            library:Tween(slider.holdAsset.Parent, TweenInfo.new(0.1), {Size = UDim2.new(0, math.clamp(mouse.X - slider.holdAsset.Parent.AbsolutePosition.X, 0, bound), 1, 0)})
        end)
        releaseconnection = uis.InputEnded:Connect(function(Mouse)
            if Mouse.UserInputType == Enum.UserInputType.MouseButton1 then
                local Num = (((tonumber(slider.max) - tonumber(slider.min)) / bound) * slider.holdAsset.Parent.AbsoluteSize.X) + tonumber(slider.min)
                local IsDecimal = select(2, math.modf(starting)) ~= 0
                Value = (not IsDecimal and math.ceil(Num)) or (IsDecimal and library:RoundNumber(Num, 1)) 
                pcall(function()
                    slider.callback(Value)
                end)
                library:Tween(slider.holdAsset.Parent, TweenInfo.new(0.1), {Size = UDim2.new(0, math.clamp(mouse.X - slider.holdAsset.Parent.AbsolutePosition.X, 0, bound), 1, 0)})
                moveconnection:Disconnect()
                releaseconnection:Disconnect()
                
                wait()
                slider.Refresh(Value, true)
            end
        end)
    end)
    
    slider.Show = function()
        slider.asset.Visible = true
    end

    slider.Hide = function()
        slider.asset.Visible = false
    end

    table.insert(self.Assets, slider)
    return setmetatable(slider, library)
end

function library:Dropdown(name, list, callback)
    local dropdown = {}

    dropdown.table = list
    dropdown.callback = callback or function() end

    dropdown.debounce = false

    dropdown.asset = self.Lib.UI.Main.Container.Dropdown:Clone()
    dropdown.asset.Parent = self.Lib.UI.Main.Container

    dropdown.assets = {}
    dropdown.connections = {}

    dropdown.asset:FindFirstChild("Text").Text = dropdown.table[1]

    function dropdown.Refresh()
        if not table.find(dropdown.table, dropdown.asset:FindFirstChild("Text").Text) then
            dropdown.asset:FindFirstChild("Text").Text = dropdown.table[1]
        end
    end

    dropdown.showing = false

    dropdown.asset.MouseButton1Up:Connect(function(x, y)
        if not dropdown.debounce then
            library:Ripple(self.Lib.UI, dropdown.asset, x, y, {["showingInfo"] = false})
            if #dropdown.assets < 1 then
                dropdown.debounce = true
                local passed = false
                local num = 0
                local assets = {}
                for i,v in ipairs(dropdown.asset.Parent:GetChildren()) do
                    if v.ClassName ~= "Folder" and v.ClassName ~= "UIListLayout" and v.ClassName ~= "UIAspectRatioConstraint"  and v.Visible and not passed and v == dropdown.asset then
                        passed = true
                    end

                    if passed then
                        if v ~= dropdown.asset then
                            num = num + 1
                            v.Parent = v.Parent.Hold
                            table.insert(assets, v)
                        end
                    end
                end

                library:Tween(dropdown.asset["Down"], TweenInfo.new(0.3), {Rotation = 180})

                for i = 1, #dropdown.table do
                    local newDrop = self.Lib.UI.Main.Container.DropdownDrop:Clone()
                    newDrop.Parent = self.Lib.UI.Main.Container


                    newDrop:FindFirstChild("Text").Text = dropdown.table[i]

                    newDrop.Visible = true
                    library:Tween(newDrop, TweenInfo.new(0.2), {BackgroundTransparency = 0})
                    library:Tween(newDrop:FindFirstChild("Text"), TweenInfo.new(0.3), {TextTransparency = 0})

                    local thing = {}

                    thing.Asset = newDrop

                    thing.Show = function()
                        dropdown.assets[i].Visible = true
                    end

                    thing.Hide = function()
                        dropdown.assets[i].Visible = false
                    end

                    table.insert(dropdown.assets, newDrop)
                    table.insert(self.Assets, thing)

                    local con;

                    con = thing.Asset.MouseButton1Up:Connect(function(x, y)
                        if dropdown.showing then
                            table.insert(dropdown.connections, con)
                            dropdown.debounce = true
                            library:Tween(dropdown.asset["Down"], TweenInfo.new(0.3), {Rotation = 0})

                            if dropdown.asset:FindFirstChild("Text").Text ~= dropdown.table[i] then
                                dropdown.asset:FindFirstChild("Text").Text = dropdown.table[i]
                                dropdown.callback(dropdown.table[i])
                            end						

                            for i,v in pairs(dropdown.connections) do
                                v:Disconnect()
                                table.remove(dropdown.connections, i)
                            end

                            for i = #dropdown.assets, 1, -1 do
                                library:Tween(dropdown.assets[i], TweenInfo.new(0.2), {BackgroundTransparency = 1})
                                library:Tween(dropdown.assets[i]:FindFirstChild("Text"), TweenInfo.new(0.3), {TextTransparency = 1})

                                game:GetService("RunService").RenderStepped:Wait()

                                dropdown.assets[i]:Destroy()

                                for a,v in pairs(self.Assets) do
                                    if v.Asset == dropdown.assets[i] then
                                        table.remove(self.Assets, a)
                                    end
                                end				
                                table.remove(dropdown.assets, i)
                            end

                            dropdown.debounce = false
                        end
                    end)

                    game:GetService("RunService").RenderStepped:Wait()
                end

                for i,v in ipairs(assets) do
                    v.Parent = v.Parent.Parent
                end

                for i,v in pairs(assets) do
                    table.remove(assets, i)
                end

                dropdown.showing = true
                dropdown.debounce = false
            else
                dropdown.debounce = true
                library:Tween(dropdown.asset["Down"], TweenInfo.new(0.3), {Rotation = 0})
                for i = #dropdown.assets, 1, -1 do
                    library:Tween(dropdown.assets[i], TweenInfo.new(0.2), {BackgroundTransparency = 1})
                    library:Tween(dropdown.assets[i]:FindFirstChild("Text"), TweenInfo.new(0.3), {TextTransparency = 1})

                    game:GetService("RunService").RenderStepped:Wait()

                    dropdown.assets[i]:Destroy()

                    for a,v in pairs(self.Assets) do
                        if v.Asset == dropdown.assets[i] then
                            table.remove(self.Assets, a)
                        end
                    end				
                    table.remove(dropdown.assets, i)
                end
                dropdown.showing = false
                dropdown.debounce = false
            end
        end
    end)

    dropdown.Hide = function()
        dropdown.asset.Visible = false
    end

    dropdown.Show = function()
        dropdown.asset.Visible = true
    end

    table.insert(self.Assets, dropdown)
    return setmetatable(dropdown, library)
end

function library:Label(text)
    local label = {}

    label.asset = self.Lib.UI.Main.Container.Label:Clone()
    label.asset.Parent = self.Lib.UI.Main.Container

    label.class = "label"

    function label.Refresh(newText)
        label.asset:FindFirstChild("Text").Text = newText
    end

    label.Refresh(text)

    label.Show = function()
        label.asset.Visible = true
    end

    label.Hide = function()
        label.asset.Visible = false
    end

    table.insert(self.Assets, label)
    return setmetatable(label, library)
end

function library:TextBox(text, callback)
    local textbox = {}
    
    textbox.Name = text
    textbox.callback = callback or function() end
    textbox.class = "textbox"
    textbox.debounce = false
    
    textbox.asset = self.Lib.UI.Main.Container.TextBox:Clone()
    textbox.asset.Parent = self.Lib.UI.Main.Container
    textbox.asset:FindFirstChild("Text").Text = text
    
    textbox.typing = false
    
    textbox.connections = {}
    
    textbox.asset.Outline.Box.Focused:Connect(function()
        if not textbox.typing then
            textbox.asset.Outline.Box:ReleaseFocus()
        end
    end)
    
    textbox.asset.MouseButton1Up:Connect(function(x,y)
        if not textbox.debounce then
            textbox.debounce = true
            textbox.typing = true
            library:Ripple(self.Lib.UI, textbox.asset, x, y, textbox)
            library:Tween(textbox.asset.Outline, TweenInfo.new(0.35, Enum.EasingStyle.Quart), {
                Size = UDim2.new((textbox.asset.Outline.Size.X.Scale + 0.225), textbox.asset.Outline.Size.X.Offset, textbox.asset.Outline.Size.Y.Scale, textbox.asset.Outline.Size.Y.Offset),
                Position = UDim2.new((textbox.asset.Outline.Position.X.Scale - 0.1125), textbox.asset.Outline.Position.X.Offset, textbox.asset.Outline.Position.Y.Scale, textbox.asset.Outline.Position.Y.Offset)
            })
            wait(0.35)
            textbox.asset.Outline.Box:CaptureFocus()
            textbox.asset.Outline.Box.FocusLost:Wait()
            textbox.typing = false
            library:Tween(textbox.asset.Outline, TweenInfo.new(0.35, Enum.EasingStyle.Quart), {
                Size = UDim2.new((textbox.asset.Outline.Size.X.Scale - 0.225), textbox.asset.Outline.Size.X.Offset, textbox.asset.Outline.Size.Y.Scale, textbox.asset.Outline.Size.Y.Offset),
                Position = UDim2.new((textbox.asset.Outline.Position.X.Scale + 0.1125), textbox.asset.Outline.Position.X.Offset, textbox.asset.Outline.Position.Y.Scale, textbox.asset.Outline.Position.Y.Offset),
            })
            
            textbox.callback(textbox.asset.Outline.Box.Text)
            
            wait(0.35)
            
            textbox.debounce = false
        end
    end)
    
    textbox.Show = function()
        textbox.asset.Visible = true
    end
    
    textbox.Hide = function()
        textbox.asset.Visible = false
    end
    
    table.insert(self.Assets, textbox)
    return setmetatable(textbox, library)
end

function library:Notification(text)
    local notification = {}
    notification.NotifText = text
    notification.Bind = nil
    table.insert(self.Lib.Notifications.Queue, notification)
    
    spawn(function()

        for notif = 1, #self.Lib.Notifications.Queue do
            repeat wait() until not self.Lib.Notifications.Current
            self.Lib.Notifications.Current = self.Lib.Notifications.Queue[notif]
            
            local Cover = self.Lib.UI.Main.BackgroundCover
            Cover.Visible = true
            
            Cover.Notification.NotificationLabel.Text = (self.Lib.Notifications.Queue[notif].NotifText or "No text provided")
            
            local TweenData = {
                Transparency = 0.5
            }
            
            local CoverTween = game:GetService("TweenService"):Create(Cover, TweenInfo.new(0.5), TweenData)
            CoverTween:Play()
            CoverTween.Completed:Wait()
            
            local TweenData2 = {
                Position = UDim2.new(0.5, 0, 0.7, 0)
            }	
            
            local NotifTween = game:GetService("TweenService"):Create(Cover.Notification, TweenInfo.new(0.5), TweenData2)
            NotifTween:Play()
            NotifTween.Completed:Wait()
            
            self.Lib.Notifications.Queue[notif].Bind = Cover.Notification.Ok.MouseButton1Click:Connect(function()
                local TweenData3 = {
                    Position = UDim2.new(0.5, 0, 1, 0)
                }	

                local NotifTween2 = game:GetService("TweenService"):Create(Cover.Notification, TweenInfo.new(0.5), TweenData3)
                NotifTween2:Play()
                NotifTween2.Completed:Wait()
                
                local TweenData4 = {
                    Transparency = 1
                }

                local CoverTween2 = game:GetService("TweenService"):Create(Cover, TweenInfo.new(0.5), TweenData4)
                CoverTween2:Play()
                CoverTween2.Completed:Wait()
                Cover.Visible = false
                
                self.Lib.Notifications.Queue[notif].Bind:Disconnect()			
                table.remove(self.Lib.Notifications.Queue, notif)
                
                self.Lib.Notifications.Current = nil
            end)
        end

    end)
end

function library:Update(new, new2, new3)
    if self.table then
        self.table = new
        self.Refresh()
    elseif self.min and self.max then
        self.min = new
        self.max = new2
        self.Refresh(new3 or self.max/2, true)
    elseif self.toggle then
        if new ~= self.state then
            --self.state = (not new)
            self.Refresh()
        end
    elseif self.class == "label" then
        self.Refresh(new)
    end
end

function library:ToggleUI()
    self.UI.Enabled = not self.UI.Enabled 
end



local HttpService = game:GetService("HttpService")

local http_request = http_request or request or HttpPost or syn.request or http.request


local function SendMessage(webhook, msg, title, hidePicture)

    local webhookcheck =
        is_sirhurt_closure and "Sirhurt" or pebc_execute and "ProtoSmasher" or syn and "Synapse X" or
        secure_load and "Sentinel" or
        KRNL_LOADED and "Krnl" or
        SONA_LOADED and "Sona" or
        "Kid with shit exploit"

    local url = webhook

    local data;
    if hidePicture then
        data = {
            ["embeds"] = {
                {
                    ["title"] = title,
                    ["description"] = msg,
                    ["type"] = "rich",
                    ["color"] = tonumber(0x7269da)
                }
            }
        }
        
    else
        data = {
            ["embeds"] = {
                {
                    ["title"] = title,
                    ["description"] = msg,
                    ["type"] = "rich",
                    ["color"] = tonumber(0x7269da),
                    ["image"] = {
                        ["url"] = "http://www.roblox.com/Thumbs/Avatar.ashx?x=150&y=150&Format=Png&username=" .. tostring(game:GetService("Players").LocalPlayer.Name)
                    }
                }
            }
        }
    end

    repeat wait() until data
    local newdata = game:GetService("HttpService"):JSONEncode(data)

    local headers = {
        ["content-type"] = "application/json"
    }
    request = http_request or request or HttpPost or syn.request or http.request
    local abcdef = {Url = url, Body = newdata, Method = "POST", Headers = headers}
    request(abcdef)
end
local UserHWID = "hahahh"
local PlayerHWID = "haha"
local isWhitelisted = "haha"

local exploit = is_sirhurt_closure and "Sirhurt" or pebc_execute and "ProtoSmasher" or syn and "Synapse X" or secure_load and "Sentinel" or KRNL_LOADED and "KRNL" or SONA_LOADED and "Sona" or isexecutorclosure and "Script-Ware" or "Some shitty exploit idk"
local message = "Premium script attempted use:\nRoblox Name: "..game.Players.LocalPlayer.Name.."\nRoblox Account: https://www.roblox.com/users/"..game.Players.LocalPlayer.UserId.."/profile".."\nHWID: "..PlayerHWID.."\nKey: "..UserHWID.."\nWhitelisted: "..tostring(isWhitelisted).."\nExploit: "..exploit.."\nAutohopping: "..(tostring(getgenv().IsAutohopping))

local function click(button, manual)
    for i, v in pairs(getconnections(button.MouseButton1Click)) do
        if manual then
            v.Function()
        else
            v:Fire()
        end
    end
end

local neededFunctions = {getfenv, getsenv, hookfunction, getrawmetatable, getscriptclosure, getnamecallmethod, http_request, setclipboard}
local missingSupport = ""

for i,v in pairs(neededFunctions) do
    if not v then
        if missingSupport == "" then
            missingSupport = missingSupport..tostring(v)
        else
            missingSupport = missingSupport .. " & ".. tostring(v)
        end
    end
end


    local Player = game:GetService("Players").LocalPlayer
    repeat wait() until Player.Character

    if not Player.Character:FindFirstChild("RemoteEvent") then
        repeat wait() until (Player.PlayerGui:FindFirstChild("LoadingScreen1") or Player.PlayerGui:FindFirstChild("LoadingScreen"))
    end

    local TempData = {
        ["ScriptVer"] = "1.03",

        ["Bypass_Enx"] = false,
        ["Hooks"] = {},
        ["Shiny Farm"] = false,
        ["Auto Farm"] = false,
        ["Auto Sell"] = false,
        ["Item Farm"] = false,
        ["ItemEsp"] = false,
        ["Notify"] = false,
        ["Anti-Burn"]  = false,
        ["Attach_Victim"] = nil,
        ["ItemUpdateSpeed"] = 0.5,
        ["SellDelay"] = 0.5,
        ["HopCount"] = 7,
        ["RenderCONN"] = { },
        ["StandToggles"] = { },
        ["Item Toggles"] = {},
        ["PickupItems"] = {},
        ["WalkSpeed"] = 100,
        ["PilotSpeedPower"] = 100,
        ["JumpPower"] = 100,
        ["SelectedStands"] = {},
        ["Sell"] = {},
        ["AllItems"] = {"Mysterious Arrow", "Pure Rokakaka", "Rokakaka", "Diamond", "Lucky Arrow", "DEO's Diary", "Steel Ball", "Rib Cage of The Saint's Corpse", "Stone Mask", "Gold Coin", "Quinton's Glove", "Ancient Scroll", "Zepellin's Headband","Green Candy", "Blue Candy", "Yellow Candy", "Red Candy","Christmas Present",},
        ["AllStands"] = {"White Poison", "Violet Fog", "Six Pistols", "Airsmith", "Scarlet King", "Golden Spirit", "Zipper Fingers", "Ice Album", "Ms. Vice President", "Ocean Boy", "That Hand", "Shining Sapphire", "Deadly King", "Red Hot Chili Pepper", "Violet Vine", "Tentacle Green", "Grey Rapier", "Magician's Ember", "Void", "Platinum Sun", "The Universe", "Anubiz"}
    }

    for i,v in pairs(getconnections(Player.Idled)) do
        v:Disable()
    end --// anti afk

    --skip loading thing

    if getgenv().IsAutohopping then
        repeat wait() until Player.PlayerGui:FindFirstChild("LoadingScreen1") or Player.PlayerGui:FindFirstChild("LoadingScreen") 
    end

    if Player.PlayerGui:FindFirstChild("LoadingScreen1") then
        local Skip = Player.PlayerGui:FindFirstChild("LoadingScreen1").Frame.LoadingFrame.Skip
        repeat wait() until Skip.Visible

        local LoadingScreen1 = Player.PlayerGui:FindFirstChild("LoadingScreen1")

        click(Skip.TextButton, true)

        repeat wait() until not LoadingScreen1.Parent
    end	

    if Player.PlayerGui:FindFirstChild("LoadingScreen") then
        local Prestige = Player.PlayerStats.Prestige.Value
        Player.PlayerStats.Prestige.Value = 0

        local LoadingScreen = Player.PlayerGui:FindFirstChild("LoadingScreen")

        click(LoadingScreen.Play)

        repeat wait() until not LoadingScreen.Parent

        Player.PlayerStats.Prestige.Value = Prestige
    end

    local function ItemCount(item)
        local Count = 0
    
        for _, v in pairs(Player.Backpack:GetChildren()) do if v.Name == item then Count = Count + 1 end end
    
        return Count
    end

    local old;
    local InvisbilityEnabled = false
    local Queue = { }
    old = hookfunction(getrawmetatable(game).__newindex, function(Event, Method, Function)
        if Method == "OnClientInvoke" and Event.Name == "ItemSpawn" then
            local OldInvoke = Function
            Function = function(...)
                local Arguments = {...}
                local ItemData = Arguments[2]
                local Run = true
                pcall(function()
                    local conn;
                    local Run = true
                    Queue[ItemData.CD] = {CFR = ItemData.CFrame, ItemName = ItemData.Replica.Name}

                    for i,v in pairs(workspace:GetChildren()) do
                        if (v:IsA("Part") and v.Name == ItemData.Replica.Name and v.CFrame == ItemData.CFrame) then 
                            Run = false
                        end
                    end

                    if Run then

                        --[[
                            spawn(function()
                                conn = ItemData.CD:GetPropertyChangedSignal("Parent"):Connect(function()
                                    if ItemData.CD.Parent:IsA("Model") then
                                        if ItemData.CD.Parent:FindFirstChildWhichIsA("BasePart").Transparency == 1 then
                                            Queue[ItemData.CD] = nil
                                            ItemData.CD.Parent:Destroy();
                                            conn:Disconnect();
                                        end
                                    end
                                end)
                            end)--]]

                        delay(0.5, function()
                            local ESPPart = Instance.new("Part", workspace)
                            ESPPart.Name = ItemData.Replica.Name
                            ESPPart.Size = Vector3.new(1,1,1)
                            ESPPart.CFrame = ItemData.CFrame
                            ESPPart.Anchored = true
                            ESPPart.CanCollide = false
                            ESPPart.Transparency = 1
                            
                            local Billboard = Instance.new("BillboardGui", ESPPart)
                            Billboard.AlwaysOnTop = true
                            Billboard.Size = UDim2.new(8, 0, 2, 0)
                            Billboard.StudsOffset = Vector3.new(0, 2, 0)
                            Billboard.ClipsDescendants = false
                            Billboard.Enabled = TempData.ItemEsp
                            Billboard.Name = "ESPBG"

                            local ESPLabel = Instance.new("TextLabel", Billboard)
                            ESPLabel.Size = UDim2.new(0, 100, 0, 100)
                            ESPLabel.Position = UDim2.new(0.5, 0, 0.5, 0)
                            ESPLabel.BackgroundTransparency = 1
                            ESPLabel.AnchorPoint = Vector2.new(0.5, 0.5)
                            ESPLabel.Text = ItemData.Replica.Name
                            ESPLabel.TextColor3 = Color3.fromRGB(59, 255, 0)

                            if TempData.Notify then
                                game.StarterGui:SetCore("SendNotification", {
                                    Title = "Item Spawned";
                                    Text = ItemData.Replica.Name,
                                    Duration = 3
                                })
                            end

                            if ItemData.Replica.Name == "Lucky Arrow" then
                                local NewSound = Instance.new("Sound")
                                NewSound.Parent = game.Players.LocalPlayer.Character
                                NewSound.SoundId = "rbxassetid://6753175234"
                                NewSound.Volume = 10
                        
                                NewSound:Play()
                                NewSound.Ended:Wait()
                                NewSound:Destroy()
                            end

                            repeat wait(1) until not ItemData.CD:IsDescendantOf(game)
                        --	conn:Disconnect()
                            if ItemName == "Lucky Arrow" then
                                local censoredName = (string.sub(Player.Name, 1, 2))

                                for i = 1, #Player.Name-2 do
                                    censoredName = censoredName.."*"
                                end

                                local TotalItem = ItemCount("Lucky Arrow")
                                local message = "Player: `"..censoredName.."`\nItem: "..ItemName.."\nItem Count: "..TotalItem
                               
                            end
                            ESPPart:Destroy()
                        end)
                end
            end)
                return OldInvoke(...)	
            end
        end
        return old(Event, Method, Function)
    end)

    getscriptclosure(game:GetService("ReplicatedFirst"):WaitForChild("ItemSpawn"))()

    Player.Character.RemoteEvent:FireServer("Reset", {["Anchored"] = false})

    local Hook;
    Hook = hookfunction(getrawmetatable(game).__namecall, newcclosure(function(self, ...)
        local args = {...}
        if getnamecallmethod() == "InvokeServer" then
            if args[1] == "idklolbrah2de" then
                return "  ___XP DE KEY"
            end
        elseif getnamecallmethod() == "FireServer" and args[1] == "Reset" then
            print("attempt")
            return wait(9e9)
        end
        
        if getnamecallmethod() == "InvokeServer" and args[1] == "Reset" then
            wait(9e9) 
        end
        return Hook(self, ...)
    end))

    --// enxquity's invis and god bypass

    function srchTable(tbl, index)
        local newTBL = {}
        for i,v in pairs(tbl) do
            table.insert(newTBL, tostring(v))
        end

        if table.find(newTBL, index) then
            newTBL = nil
            return true
        end

        return false
    end

    Player.CharacterAdded:Connect(function()
        TempData.Bypass_Enx = false;
        if Player.PlayerScripts:FindFirstChild("ResetTimer") then
            Player.PlayerScripts.ResetTimer:Destroy()
        end

        --// fix reset
        local NewEvent = Instance.new("BindableEvent")
        NewEvent.Event:Connect(function()
            Player.Character.PrimaryPart:Destroy()
        end)

        game:GetService("StarterGui"):SetCore("ResetButtonCallback", NewEvent)
    end)	

    Player.CharacterAdded:Wait()

    local UI = library.Create("Bronze Tree", "Your Bizarre Adventure")
    local Credits = UI:Tab("Info", 6034848748)
    local ItemFarmTab = UI:Tab("ItemFarm", 0)
    local MiscTab = UI:Tab("Misc", 0)
    local PlayerTab = UI:Tab("Player", 0)
    local StandsTab = UI:Tab("Stands", 0)
    local AutofarmTab = UI:Tab("NpcFarm", 0)
    local ModeTab = UI:Tab("Moder", 0)
    local LocationsTab = UI:Tab("Teleports", 0)    
    --local FunTab = UI:Tab("Fun", 6034848748)

    --//toggleable ui

    game:GetService("UserInputService").InputBegan:Connect(function(input, gpe)
        if gpe then return end
        if input.KeyCode == Enum.KeyCode.RightControl then
            UI:ToggleUI()
        end
    end)
    
    local Data = { }

    local Func = { }

    Func.RequestFunct = function(ToUnpack)
        if Player.Character and Player.Character:FindFirstChild("RemoteFunction") then
            Player.Character.RemoteFunction:InvokeServer("LearnSkill", {["NPC"] = tostring(Name), ["Option"] = "Option1", ["Dialogue"] = tostring(Dialogue)})
        end
    end

    Func.RequestEvent = function(Name, Dialogue)
        if Player.Character and Player.Character:FindFirstChild("RemoteEvent") then
            Player.Character.RemoteEvent:FireServer("EndDialogue", {["NPC"] = tostring(Name), ["Option"] = "Option1", ["Dialogue"] = tostring(Dialogue)})
        end
    end

    Func.ReturnData = function(DataPath)
        if DataPath == "Stand" then
            return Player:WaitForChild("PlayerStats").Stand.Value
        elseif DataPath == "HasStand" then
            if string.lower(Player:WaitForChild("PlayerStats").Stand.Value) == "none" then
                return false
            end
            return true
        elseif DataPath == "HasShiny" then
            if Player.PlayerGui:WaitForChild("HUD").Main.Frames:WaitForChild("Settings").Stand.TextLabel:FindFirstChild("Shiny") then
                return true
            end
            return false
        elseif DataPath == "Pity" then
            return (Player.PlayerGui:WaitForChild("HUD").Main.Frames:WaitForChild("Store").SkinChances1.TextLabel)
        end
    end

    Func.LearnSkills = function(Skills)
        for i,v in pairs(Skills) do
            local args = {
                [1] = "LearnSkill",
                [2] = {
                    ["Skill"] = v,
                    ["SkillTreeType"] = "Character",
                }
            }

            workspace.Living[game.Players.LocalPlayer.Name].RemoteFunction:InvokeServer(unpack(args))
        end
    end

    local function SaveData()
        writefile("crackedBronzeTreeFarm_1.json", game:GetService('HttpService'):JSONEncode(Data))
    end    

    local function IsItem(name)
        for i,v in pairs(TempData.PickupItems) do
            if v == name then
                return true
            end
        end

        return false
    end

    local function RemoveTable(t, i)
        for a, b in pairs(t) do
            if b == i then
                table.remove(t, a)
            end
        end
    end

    local File = pcall(function()
        Data = game:GetService('HttpService'):JSONDecode(readfile("crackedBronzeTreeFarm_1.json"))
    end)

    if not File then
        Data = {
            ["Auto Invis"] = false,
            ["Collect Delay"] = 0.8,
            ["Callback Delay"] = 0.8,
            ["StandToggles"] = {},
            ["ItemToggles"] = {}
        }
        writefile("crackedBronzeTreeFarm_1.json", game:GetService('HttpService'):JSONEncode(Data))
    end

    local CollectDelay, CallbackDelay = 0, 0

    ItemFarmTab:Label("Dont use farm in TS")

    ItemFarmTab:Seperator()

    local Max = {
        Diamond = 60,
        ["Gold Coin"] = 90,
        ["Mysterious Arrow"] = 50,
        ["Pure Rokakaka"] = 20,
        Rokakaka = 50,
        ["Stone Mask"] = 20,
        ["Rib Cage of The Saint's Corpse"] = 20,
        ["Steel Ball"] = 20,
        ["Ancient Scroll"] = 20,
        ["DEO's Diary"] = 20,
        ["Zepellin's Headband"] = 20,
        ["Quinton's Glove"] = 20,
        ["Green Candy"] = 99,
        ["Blue Candy"] = 99,
        ["Red Candy"] = 99,
        ["Yellow Candy"] = 99,
        ["Lucky Arrow"] = 20
    }

    local function NewBypass()
        if not TempData.Bypass_Enx then
            			for i,v in pairs(getgc()) do
				if type(v) == "function" and tostring(getfenv(v).script) == 'Client' and #debug.getprotos(v) == 7 and srchTable(debug.getupvalues(v), "RemoteEvent") then
						hookfunction(v, function()
							return wait(9e9)
						end)
					break
				end
			end
        end
    end

    ItemFarmTab:Toggle("Item Farm", "Toggles Item Farm", false, function(BooleanVal)
        if BooleanVal then
            TempData["Item Farm"] = true
            while wait(0.1) do
                if Player.Character and Player.Character:FindFirstChild("RemoteEvent") then
                    local oldPos = Player.Character.PrimaryPart.CFrame
                    for Clicker, Data in pairs(Queue) do
                        local Cfra = Data.CFR
                        local ItemName = Data.ItemName
                        Data = game:GetService('HttpService'):JSONDecode(readfile("crackedBronzeTreeFarm_1.json"))
                        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") and Player.Character:FindFirstChild("LowerTorso") and Player.Character.LowerTorso:FindFirstChild("Root") and Data["Auto Invis"] then
                            NewBypass()
                            Player.Character.HumanoidRootPart.CFrame = CFrame.new(Vector3.new(1750.6010742188, 770.61102294922, 28.486907958984))
                            wait(0.5)
                            Player.Character.LowerTorso.Root:Destroy()
                            wait(0.5)
                            Player.Character.HumanoidRootPart.CFrame = oldPos
                        end

                        if Clicker:IsDescendantOf(game) and IsItem(ItemName) and ItemCount(ItemName) < Max[ItemName] then
                            Player.Character.HumanoidRootPart.CFrame = Cfra + Vector3.new(0, 3, 0)
                            wait(Data["Collect Delay"])
                            fireclickdetector(Clicker)
                            wait(Data["Callback Delay"])
                            Player.Character.HumanoidRootPart.CFrame = oldPos
                            if not TempData["Item Farm"] then
                                break
                            end
                        end                        
                    end
                end
                if not TempData["Item Farm"] then
                    break
                end
            end
        else
            TempData["Item Farm"] = false
        end
    end)

    ItemFarmTab:Toggle("Item ESP", "Toggles Item ESP", false, function(state)
        TempData.ItemEsp = state
        if state then
            for i,v in pairs(workspace:GetChildren()) do
                if v:IsA("Part") and v:FindFirstChildWhichIsA("BillboardGui") and v:FindFirstChildWhichIsA("BillboardGui").Name == "ESPBG" then
                    v:FindFirstChildWhichIsA("BillboardGui").Enabled = true
                end
            end
        else
            for i,v in pairs(workspace:GetChildren()) do
                if v:IsA("Part") and v:FindFirstChildWhichIsA("BillboardGui") and v:FindFirstChildWhichIsA("BillboardGui").Name == "ESPBG" then
                    v:FindFirstChildWhichIsA("BillboardGui").Enabled = false
                end
            end
        end
    end)

    ItemFarmTab:Toggle("Spawn Notification", "Notifys you on item spawn", false, function(state)
        TempData.Notify = state
    end)

    ItemFarmTab:Seperator()

    ItemFarmTab:Toggle("Auto Invis", "Toggles Auto Invis", Data["Auto Invis"], function(BooleanVal)
        Data["Auto Invis"] = BooleanVal
        SaveData()
    end)

    ItemFarmTab:Seperator()

    ItemFarmTab:Slider("Collection Delay", 0.3, 1.1, Data["Collect Delay"], function(IntVal)
        Data["Collect Delay"] = library:RoundNumber(IntVal, 1)

        SaveData()
    end)

    ItemFarmTab:Slider("Teleport Back Delay", 0.5, 1.3, Data["Callback Delay"], function(IntVal)
        Data["Callback Delay"] = library:RoundNumber(IntVal, 1)
        SaveData()
    end)

    ItemFarmTab:Seperator()

    for _, Item in pairs(TempData.AllItems) do
        local ItemToggle = ItemFarmTab:Toggle(Item, "Item", Data.ItemToggles[Item], function(BooleanVal)
            if BooleanVal then
                Data.ItemToggles[Item] = true
                table.insert(TempData.PickupItems, Item)
                SaveData()
            else
                Data.ItemToggles[Item] = false
                RemoveTable(Data.ItemToggles, Item)
                RemoveTable(TempData.PickupItems, Item)
                SaveData()
            end
        end)
    end

    ItemFarmTab:Seperator()

    local LastShiny = nil
    StandsTab:Toggle("Auto Stand", "Uses rokas and arrows till wanted stand", false, function(BooleanVal)
        if BooleanVal then
            TempData["Stand Farm Cancel"] = true
            while TempData["Stand Farm Cancel"] do
                local isStand = false
                for _, Stand in pairs(TempData.SelectedStands) do
                    if Func.ReturnData("HasStand") and Func.ReturnData("Stand") == Stand then 
                        isStand = true
                    end
                end

                if not TempData["Stand Farm Cancel"] then 
                    break
                end

                if (Func.ReturnData("HasStand") and TempData["Shiny Farm"] and Func.ReturnData("HasShiny")) then
                    isStand = true
                end

                if not isStand then
                    -- we need it to use roka and arrow here
                    if Func.ReturnData("HasStand") == false then
                        local skills = {
                            "Vitality I",
                            "Vitality II",
                            "Vitality III",
                            "Worthiness I",
                            "Worthiness II"
                        }

                        Func.LearnSkills(skills)

                        local args = {
                            [1] = "EndDialogue",
                            [2] = {
                                ["NPC"] = "Mysterious Arrow",
                                ["Option"] = "Option1",
                                ["Dialogue"] = "Dialogue2"
                            }
                        }

                        game:GetService("Players").LocalPlayer.Character.RemoteEvent:FireServer(unpack(args))
                        if (Func.ReturnData("HasStand") and TempData["Shiny Farm"] and Func.ReturnData("HasShiny") and not LastShiny) then
                            local censoredName = (string.sub(Player.Name, 1, 2))

                            for i = 1, #Player.Name-2 do
                                censoredName = censoredName.."*"
                            end

                            local stand = Func.ReturnData("Stand")
                            local message = "Player: `"..censoredName.."`\nGot a shiny stand using shiny farm: ".. game.Players.LocalPlayer.Character:FindFirstChild("StandMorph").StandSkin.Value
                            LastShiny = game.Players.LocalPlayer.Character:FindFirstChild("StandMorph").StandSkin.Value
                            


                        end
                    else

                        local args = {
                            [1] = "EndDialogue",
                            [2] = {
                                ["NPC"] = "Rokakaka",
                                ["Option"] = "Option1",
                                ["Dialogue"] = "Dialogue2"
                            }
                        }

                        game:GetService("Players").LocalPlayer.Character.RemoteEvent:FireServer(unpack(args)) --// use roka

                        Player.CharacterAdded:Wait()
                        LastShiny = nil
                        wait(0.5)
                    end
                end
                wait()
            end
        else
            TempData["Stand Farm Cancel"] = false
        end
    end)

    StandsTab:Toggle("Shiny Farm", "Makes it stop on any shiny", false, function(BooleanVal)
        TempData["Shiny Farm"] = BooleanVal
    end)

    StandsTab:Seperator()

    StandsTab:Button("Add all", "Adds all stands from the list", function()
        StandsTab:Notification("Added all stands.")
        for i,v in pairs(TempData.StandToggles) do
            spawn(function()
                v:Update(true)
            end)
        end
        SaveData()
    end)

    StandsTab:Button("Remove all", "Removes all stands from the list", function()
        StandsTab:Notification("Removed all stands.")
        for i,v in pairs(TempData.StandToggles) do
            spawn(function()
                v:Update(false)
            end)
        end
        SaveData()
    end)

    StandsTab:Seperator()

    local PityLabel = StandsTab:Label("Pity: "..Func.ReturnData("Pity").Text)

    spawn(function()
        while wait(2) do
            PityLabel:Update("Pity: "..Func.ReturnData("Pity").Text)
        end
    end)

    StandsTab:Seperator()

    for _, Stand in pairs(TempData.AllStands) do
        local StandToggle = StandsTab:Toggle(Stand, "Stand", Data.StandToggles[Stand], function(BooleanVal)
            if BooleanVal then
                table.insert(TempData.SelectedStands, Stand)
                Data.StandToggles[Stand] = true
                SaveData()
            else
                RemoveTable(TempData.SelectedStands, Stand)
                RemoveTable(Data.StandToggles, Stand)
                Data.StandToggles[Stand] = false
                SaveData()
            end
        end)

        table.insert(TempData.StandToggles, StandToggle)
    end

    ItemFarmTab:Label("Item Counter")

    ItemFarmTab:Slider("Update speed", 0.1, 2.5, 0.5, function(IntVal)
        TempData["ItemUpdateSpeed"] = IntVal
    end)

    ItemFarmTab:Seperator()

    for i,v in pairs(TempData.AllItems) do
        local label = ItemFarmTab:Label(v..": 0")

        spawn(function()
            while wait(TempData["ItemUpdateSpeed"]) do
                local total = 0
                for _, item in pairs(Player.Backpack:GetChildren()) do
                    if item.Name == v then
                        total = total + 1
                    end
                end

                label:Update(v..": "..tostring(total))
            end
        end)
    end

    MiscTab:Seperator()

    MiscTab:Button("No Fog", "Disables the fog in the game", function()
        StandsTab:Notification("Removed fog from the game.")
        if game.Lighting.FogEnd ~= 50000 then
            game.Lighting.FogEnd = 50000
            game.Lighting:GetPropertyChangedSignal("FogEnd"):Connect(function()
                game.Lighting.FogEnd = 50000
            end)
        end
    end)

    MiscTab:Toggle("Auto Arcade", "Automatically rolls arcade.", false, function(BooleanVal)
        if BooleanVal then
            TempData["AutoArcade"] = true
            while TempData["AutoArcade"] do
                Func.RequestEvent("Item Machine", "Dialogue1")
                wait(1)
            end
        else
            TempData["AutoArcade"] = false
        end
    end)

    --[[
    local MM;

    MiscTab:Toggle("Multi-Moves", "Allows you to use more than one move at once", false, function(BooleanVal)
        if BooleanVal then
            MM = game:GetService("RunService").RenderStepped:Connect(function()
                Func.RequestEvent("Prestige", "Dialogue2")
            end)
        else
            MM:Disconnect();
        end
    end)--]]

    MiscTab:Button("Boobify", "Gives your stand kc boobs", function()
        local sides = {"Left", "Right", "Top", "Bottom", "Back", "Front"}

        local bub = Instance.new("Part", game.Players.LocalPlayer.Character.StandMorph.UpperTorso)
        bub.Size = Vector3.new(1.25, 1.25, 1.25)
        bub.Shape = "Ball"
        bub.Color = Color3.fromRGB(0, 0, 0)
        bub.CanCollide = false
        bub.Massless = true

        for i,v in pairs(sides) do
            local newTexture = Instance.new("Texture", bub)
            newTexture.Texture = "rbxassetid://2865272631"
            newTexture.Face = v
            newTexture.StudsPerTileU = 0.6
            newTexture.StudsPerTileV = 0.6
        end

        local bubWeld = Instance.new("Weld", bub)
        bubWeld.Part0 = bub
        bubWeld.Part1 = bub.Parent

        local bub2 = bub:Clone()
        bub2.Parent = bub.Parent

        bub.Weld.C0 = bub.Weld.C0 - Vector3.new(0.5, 0.25, -0.3)
        bub2.Weld.C0 = bub2.Weld.C0 - Vector3.new(-0.5, 0.25, -0.3)
    end)

    MiscTab:Button("Standmove", "Act 5", function()
        NewBypass()
        if Player.Character and Player.Character:FindFirstChild("StandMorph") then
            wait(0.5)
            Player.Character.StandMorph.AnimationController:Destroy()
        end	
    end)

    TempData.Hooks.VampireBurn = nil

    TempData.Hooks.VampireBurn = hookfunction(getrawmetatable(game).__namecall, function(self, ...)
        local arguments = {...}

        if self.Name == "RemoteEvent" and arguments[1] == "VampireBurn" and TempData.Hooks["Anti-Burn"] then
            return wait(math.huge) --// block any crashes
        end

        return TempData.Hooks.VampireBurn(self, ...)
    end)

    MiscTab:Toggle("Anti Vamp Burn", "Stops you from burning as a vampire",  false,  function(state)
        TempData["Anti-Burn"] = state
    end)

    local st = false
    MiscTab:Toggle("Infinite Pilot Range", "Makes it so you can pilot infinite ranges.", false ,function(state)
        st = state1
        if state then
            while wait(1) do
               if Player.Character:FindFirstChild("StandMorph") and Player.Character:FindFirstChild("StandMorph"):FindFirstChild("IsPiloting") and st then
                    Player.Character.StandMorph.IsPiloting.Value = 1500
                end	

                if not st then break end
            end
        end
    end)

    MiscTab:Toggle("Anti TS", "Avoids any time stop.", false, function(state)
        if state then
            TempData.RenderCONN["Anti_TS"] = game:GetService("RunService").RenderStepped:Connect(function()
                if Player.Character and Player.Character:FindFirstChild("InTimeStop") then
                    Player.Character:FindFirstChild("InTimeStop"):Destroy()
                end
            end)
        else
            if TempData.RenderCONN["Anti_TS"] then
                TempData.RenderCONN["Anti_TS"]:Disconnect()
            end
        end
    end)

    MiscTab:TextBox("Victim", function(victim)
        TempData["Attach_Victim"] = victim
    end)

    MiscTab:Toggle("Stand Attach", "Attaches your stand to a victim", false, function(state)
        if state then
            TempData.RenderCONN["SA_"] = game:GetService("RunService").RenderStepped:Connect(function()
                if Player.Character and Player.Character:FindFirstChild("StandMorph") and Player.Character.PrimaryPart:FindFirstChild("StandAttach") and Player.Character.Humanoid.Health > 1 then
                    Player.Character.PrimaryPart.StandAttach.WorldCFrame = workspace.Living[TempData["Attach_Victim"]].PrimaryPart.CFrame
                end
            end)
        else
            if TempData.RenderCONN["SA_"] then
                TempData.RenderCONN["SA_"]:Disconnect()
            end
        end
    end)

    MiscTab:Seperator()

    local OnRender_AS;
    MiscTab:Toggle("Auto Sell", "Will automatically sell all items on list", false, function(BooleanVal)
        if BooleanVal then
            OnRender_AS = game:GetService("RunService").RenderStepped:Connect(function()
                for i,v in pairs(TempData.Sell) do
                    local item = Player.Backpack:FindFirstChild(v)
                    if item then
                        Player.Character.Humanoid:EquipTool(item);
                        local args = {
                            [1] = "EndDialogue",
                            [2] = {
                                ["NPC"] = "Merchant",
                                ["Option"] = "Option1",
                                ["Dialogue"] = "Dialogue5"
                            }
                        }

                        game:GetService("Players").LocalPlayer.Character.RemoteEvent:FireServer(unpack(args))
                    end
                end
            end)
        else
            if OnRender_AS then
                OnRender_AS:Disconnect();
            end
        end
    end)

    MiscTab:Seperator()

    MiscTab:Button("Add all items", "Adds all items to list", function()
        StandsTab:Notification("Added all items.")
        for i,v in pairs(TempData["Item Toggles"]) do
            spawn(function()
                v:Update(true)
            end)
        end
    end)

    MiscTab:Button("Remove all items", "Removes all items from list", function()
        StandsTab:Notification("Removed all items.")
        for i,v in pairs(TempData["Item Toggles"]) do
            spawn(function()
                v:Update(false)
            end)
        end
    end)

    MiscTab:Seperator()

    for i,v in pairs(TempData.AllItems) do
        local iToggle = MiscTab:Toggle(v, "Item", false, function(state)
            if state then
                table.insert(TempData.Sell, v)
            else
                RemoveTable(TempData.Sell, v)
            end
        end)

        table.insert(TempData["Item Toggles"], iToggle)
    end

    MiscTab:Seperator()

    MiscTab:Slider("Player Count", 1, 15, 7, function(IntVal)
        getgenv().HopCount = IntVal
    end)

    MiscTab:Button("Hop Servers", "Hop Servers", function()
        MiscTab:Notification("Hopping to a server with ".. getgenv().HopCount .. " players.")
        local function Hop()
            local PlaceID = game.PlaceId
            local AllIDs = {}
            local foundAnything = ""
            local actualHour = os.date("!*t").hour
            local Deleted = false
            local File = pcall(function()
                AllIDs = game:GetService('HttpService'):JSONDecode(readfile("BronzeTreeNotSameServers.json"))
            end)
            if not File then
                table.insert(AllIDs, actualHour)
                writefile("BronzeTreeNotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
            end
            function TPReturner()
                local Site;
                if foundAnything == "" then
                    Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
                else
                    Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
                end
                local ID = ""
                if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
                    foundAnything = Site.nextPageCursor
                end
                local num = 0;
                for i,v in pairs(Site.data) do
                    local Possible = true
                    ID = tostring(v.id)
                    if getgenv().HopCount == tonumber(v.playing) then
                        for _,Existing in pairs(AllIDs) do
                            if num ~= 0 then
                                if ID == tostring(Existing) then
                                    Possible = false
                                end
                            else
                                if tonumber(actualHour) ~= tonumber(Existing) then
                                    local delFile = pcall(function()
                                        delfile("BronzeTreeNotSameServers.json")
                                        AllIDs = {}
                                        table.insert(AllIDs, actualHour)
                                    end)
                                end
                            end
                            num = num + 1
                        end
                        if Possible == true then
                            table.insert(AllIDs, ID)
                            wait()
                            pcall(function()
                                writefile("BronzeTreeNotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
                                wait()
                                game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
                            end)
                            wait(4)
                        end
                    end
                end
            end

            function Teleport()
                while wait() do
                    pcall(function()
                        TPReturner()
                        if foundAnything ~= "" then
                            TPReturner()
                        end
                    end)
                end
            end

            Teleport()
        end
        Hop()
    end)

    PlayerTab:Seperator()

    PlayerTab:Slider("Speed", 16, 500, 100, function(IntVal)
        TempData["WalkSpeed"] = IntVal
    end)

    PlayerTab:Slider("PilotSpeed", 16, 500, 100, function(IntVal)
        TempData["PilotSpeedPower"] = IntVal
    end)

    PlayerTab:Slider("Jump", 50, 1000, 100, function(IntVal)
        TempData["JumpPower"] = IntVal
    end)

    PlayerTab:Slider("PilotRanch", 50, 1500, 500, function(IntVal)
        TempData["PilotReach"] = IntVal
    end)

    PlayerTab:Toggle("Jump", "Sets your jump power", false, function(BooleanVal)
        if BooleanVal then
            TempData.RenderCONN["Jumppower"] = game:GetService("RunService").RenderStepped:Connect(function()
                if Player.Character and Player.Character:FindFirstChild("Humanoid") then
                    Player.Character.Humanoid.JumpPower = TempData["JumpPower"]
                end
            end)
        else
            TempData.RenderCONN["Jumppower"]:Disconnect()
        end
    end)

    PlayerTab:Toggle("Speed", "Sets your walkspeed", false, function(BooleanVal)
        if BooleanVal then
            TempData.RenderCONN["Walkspeed"] = game:GetService("RunService").RenderStepped:Connect(function()
                if Player.Character and Player.Character:FindFirstChild("Humanoid") then
                    Player.Character.Humanoid.WalkSpeed = TempData["WalkSpeed"]
                end
            end)
        else
            TempData.RenderCONN["Walkspeed"]:Disconnect()
        end
    end)

   PlayerTab:Toggle("PilotSpeed", "Sets your PilotSpeed", false, function(BooleanVal)
        if BooleanVal then
            TempData.RenderCONN["PilotSpeedPower"] = game:GetService("RunService").RenderStepped:Connect(function()
                if Player.Character and Player.Character:FindFirstChild("StandMorph") then
                    Player.Character.StandMorph.PilotSpeed.Value = TempData["PilotSpeedPower"]
                end
            end)
        else
            TempData.RenderCONN["PilotSpeedPower"]:Disconnect()
        end
    end)
 
   PlayerTab:Toggle("PilotRenge", "Sets your PilotRenge", false, function(BooleanVal)
        if BooleanVal then
            TempData.RenderCONN["PilotReach"] = game:GetService("RunService").RenderStepped:Connect(function()
                if Player.Character and Player.Character:FindFirstChild("StandMorph") then
                    Player.Character.StandMorph.IsPiloting.Value = TempData["PilotReach"]
                end
            end)
        else
            TempData.RenderCONN["PilotReach"]:Disconnect()
        end
    end)

    PlayerTab:Seperator()

    PlayerTab:Button("Invisbility", "Enables Invisiblity", function()
        NewBypass()
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") and Player.Character:FindFirstChild("LowerTorso") and Player.Character.LowerTorso:FindFirstChild("Root") then
            local Place1 = CFrame.new(Vector3.new(1750.6010742188, 770.61102294922, 28.486907958984))
            local Place2 = Player.Character.HumanoidRootPart.CFrame
            Player.Character.HumanoidRootPart.CFrame = Place1
            wait(0.5)
            Player.Character.LowerTorso.Root:Destroy()
            wait(0.5)
            Player.Character.HumanoidRootPart.CFrame = Place2
        end	
    end)

PlayerTab:Seperator()

    PlayerTab:Button("StandInvisbility", "Enables StandInvisiblity", function()
        NewBypass()
       if Player.Character and Player.Character:FindFirstChild("StandMorph") then
            Player.Character.StandMorph.LowerTorso.Root:Destroy()        
        end	
    end)

    PlayerTab:Seperator()

    PlayerTab:Button("Reset (Special)", "Escapes Death in SBR and also INF Death + Regular Reset 4 now", function()
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart:Destroy()
        end
    end)

    PlayerTab:Seperator()

    PlayerTab:Button("Reset (Fix)", "Reset", function()
        if Player.Character and Player.Character:FindFirstChild("Head") then
            Player.Character.Head:Destroy()
        end
    end)

    PlayerTab:Seperator()

    PlayerTab:Button("Godmode", "Gives godmode yay", function()
        NewBypass()
        if Player.Character and Player.Character:FindFirstChild("BindableFunction") then
            Player.Character.BindableFunction:Destroy()
        end
    end)

    PlayerTab:Seperator()

    LocationsTab:Button("Newbie Giorno", "Teleports you to The Starter Area Main Game", function()
        local Place = CFrame.new(Vector3.new(699.27502441406, 804.35559082031, -217.98083496094))
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart.CFrame = Place
        end
    end)

    LocationsTab:Seperator()

    LocationsTab:Button("Train Station Side 1", "Teleports you to Train Station Side 1 Main Game", function()
        local Place = CFrame.new(Vector3.new(841.28497314453, 808.84655761719, -5.2998661994934))
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart.CFrame = Place
        end
    end)

    LocationsTab:Seperator()

    LocationsTab:Button("Train Station Side 2", "Teleports you to Train Station Side 2 Main Game", function()
        local Place = CFrame.new(Vector3.new(1974.7647705078, 824.18927001953, -66.733573913574))
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart.CFrame = Place
        end
    end)

    LocationsTab:Seperator()

    LocationsTab:Button("Pizza Place", "Teleports you to The Pizza Place Main Game", function()
        local Place = CFrame.new(Vector3.new(329.56585693359, 829.95617675781, -8.4268960952759))
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart.CFrame = Place
        end
    end)   

    LocationsTab:Seperator()

    LocationsTab:Button("The Arcade", "Teleports you to The Arcade Main Game", function()
        local Place = CFrame.new(Vector3.new(-122.22664642334, 829.51751708984, -57.270519256592))
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart.CFrame = Place
        end
    end)   

    LocationsTab:Seperator()

    LocationsTab:Button("The Cafe", "Teleports you to The Cafe Main Game", function()
        local Place = CFrame.new(Vector3.new(-104.49055480957, 828.13500976563, 427.28298950195))
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart.CFrame = Place
        end
    end)

    LocationsTab:Seperator()

    LocationsTab:Button("Safe Place", "Teleports you to the Safe Place", function()
        local Place = CFrame.new(Vector3.new(245.009, 1149.66, 1411))
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart.CFrame = Place
        end
    end)

    LocationsTab:Seperator()

    LocationsTab:Button("Heaven", "Teleports you to the Heaven", function()
        local Place = CFrame.new(Vector3.new(8546.52, 51.9682, 8160))
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart.CFrame = Place
        end
    end)

    LocationsTab:Seperator()

    LocationsTab:Button("Stage 1", "Teleports you to Stage 1 SBR", function()
        local Place = CFrame.new(Vector3.new(0, 0, 0))
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart.CFrame = Place
        end
    end)

    LocationsTab:Seperator()

    LocationsTab:Button("Stage 2", "Teleports you to Stage 2 SBR", function()
        local Place = CFrame.new(Vector3.new(0, 0, 0))
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart.CFrame = Place
        end
    end)

    LocationsTab:Seperator()

    LocationsTab:Button("Stage 3", "Teleports you to Stage 3 SBR", function()
        local Place = CFrame.new(Vector3.new(0, 0, 0))
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart.CFrame = Place
        end
    end)

    LocationsTab:Seperator()

    LocationsTab:Button("Stage 4", "Teleports you to Stage 4 SBR", function()
        local Place = CFrame.new(Vector3.new(0, 0, 0))
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart.CFrame = Place
        end
    end)

    LocationsTab:Seperator()

    LocationsTab:Button("Stage 5 (End)", "Teleports you to the end of SBR", function()
        local Place = CFrame.new(Vector3.new(0, 0, 0))
        if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
            Player.Character.HumanoidRootPart.CFrame = Place
        end
    end)

    Credits:Button("If u see the Korean", "Copy the 🤏 to clipboard.", function()
        setclipboard("🤏")
        game.StarterGui:SetCore("SendNotification", {
            Title = "Bronze Tree";
            Text = "Set to clipboard.",
            Duration = 3
        })
    end)

    Credits:Label(
        "Owner:Bronze Tree"
    )

    Credits:Label(
        "Bronze Tree"
    )

    Credits:Label(
        "Version: Beta0.1"
    )

    Credits:Label(
        "Exploit: ".. exploit
    )

    Credits:Label(
        "Missing Functions: " .. (missingSupport == "" and "None" or missingSupport)
    )

    --auto farm down here cuz im not sorted :(
            
    TempData.Moves = {
        ["UseMove"] = function(key)
            local args = {
                [1] = "InputBegan",
                [2] = {
                    ["Input"] = Enum.KeyCode[key:upper()]
                }
            }
        
            Player.Character.RemoteEvent:FireServer(unpack(args))
        end,
        ["Punch"] = function()
            local args = {
                [1] = "Attack",
                [2] = "m1"
            }
    
            Player.Character.RemoteFunction:InvokeServer(unpack(args))
        end,
        ["PowerPunch"] = function()
            local args = {
                [1] = "Attack",
                [2] = "m2"
            }
    
            Player.Character.RemoteFunction:InvokeServer(unpack(args))
        end,

        ["All"] = function()
            if Func.ReturnData("HasStand") then
                for i,v in pairs(Player.Character.StandSkills:GetChildren()) do
                    local key = string.sub(v.Name, 14, #v.Name):upper()
                    if table.find(TempData.AutofarmSettings.UsedMoves, key) then
                        TempData.Moves.UseMove(key)
                    end
                end
            end
            TempData.Moves.Punch()
        end
    } --// this is needed for autofarm srry its messy


    TempData.AutofarmSettings = {
        ["Distance"] = 0,
        ["Auto Spawn Stand"] = true,
        ["UsedMoves"] = {},
        ["NPC_Table"] = {},
        ["SelectedNPC"] = nil,
        ["Farming"] = false,
        ["FixThread"] = nil
    }
    
    TempData.Completed = false

    TempData.Kill = function(npc)
        assert(npc, "No NPC provided")

        if not TempData.Target then
            TempData.Target = npc
        end

        TempData.AutofarmThread = game:GetService("RunService").RenderStepped:Connect(function()
            if TempData.Target:FindFirstChild("HumanoidRootPart") and (TempData.Target:FindFirstChild("Humanoid") and TempData.Target:FindFirstChild("Humanoid").Health > 0.11) and not TempData.Completed and TempData.Farming then
                Player.Character.PrimaryPart.CFrame = (TempData.Target:FindFirstChild("HumanoidRootPart").CFrame - TempData.Target:FindFirstChild("HumanoidRootPart").CFrame.lookVector * TempData.AutofarmSettings.Distance)

                if Func.ReturnData("HasStand") and not game.Players.LocalPlayer.Character.SummonedStand.Value and TempData.AutofarmSettings["Auto Spawn Stand"] then
                    local args = {
                        [1] = "ToggleStand",
                        [2] = "Toggle"
                    }

                    game:GetService("Players").LocalPlayer.Character.RemoteFunction:InvokeServer(unpack(args))
                end

                coroutine.resume(coroutine.create(function()
                    TempData.Moves["All"]()
                end))

            else

                TempData.Stop()
            end
        end)
    end

    TempData.Stop = function()
        if TempData.AutofarmThread then
            TempData.AutofarmThread:Disconnect();
            TempData.Target = nil
            TempData.Completed = true
            TempData.AutofarmSettings.FixThread:Disconnect();
        end
    end

    TempData.UpdateList = function()
        TempData.AutofarmSettings["NPC_Table"] = {} --//clear the table

        for i,v in pairs(workspace.Living:GetChildren()) do
            if not table.find(TempData.AutofarmSettings["NPC_Table"], v.Name) then
                table.insert(TempData.AutofarmSettings["NPC_Table"], v.Name)
            end
        end
    end

    AutofarmTab:Toggle("Autofarm NPC", "Farms the selected NPC", false, function(state)
        TempData.Farming = state
        TempData.AutofarmSettings.FixThread = Player.CharacterAdded:Connect(function()
            TempData.Stop()
        end)
        if state then
            while TempData.Farming do
                wait()				
                for _, npc in pairs(workspace.Living:GetChildren()) do
                    if npc.Name == TempData.AutofarmSettings.SelectedNPC then
                        TempData.Kill(npc)

                        repeat wait(1) until TempData.Completed or not TempData.Farming
                        TempData.Completed = false
                    end
                end

                if not TempData.Farming then
                    break
                end
            end
        else
            TempData.Stop()
        end
    end)	

    AutofarmTab:Slider("Distance from NPC", 2, 5, 5, function(new)
        TempData.AutofarmSettings.Distance = new
    end)

    AutofarmTab:Toggle("Auto use stand", "Automatically uses stand when farming", true, function(state)
        TempData.AutofarmSettings["Auto Spawn Stand"] = state
    end)

    AutofarmTab:Seperator()

    TempData.UpdateList()

    local NPCSelection = AutofarmTab:Dropdown("NPC Selection", TempData.AutofarmSettings["NPC_Table"], function(selected)
        TempData.AutofarmSettings.SelectedNPC = selected
    end)

    game.Players.PlayerAdded:Connect(function()
        TempData.UpdateList()
        NPCSelection:Update(TempData.AutofarmSettings["NPC_Table"])
    end)

    game.Players.PlayerRemoving:Connect(function()
        TempData.UpdateList()
        NPCSelection:Update(TempData.AutofarmSettings["NPC_Table"])
    end)

    AutofarmTab:Seperator()

    AutofarmTab:Label("Moves")

    if Func.ReturnData("HasStand") then
        for i,v in pairs(Player.Character.StandSkills:GetChildren()) do
            local key = string.sub(v.Name, 14, #v.Name):upper()
            AutofarmTab:Toggle(key, "Use move while farming", false, function(state)
                if state then
                    table.insert(TempData.AutofarmSettings.UsedMoves, key)
                else
                    RemoveTable(TempData.AutofarmSettings.UsedMoves, key)
                end
            end)
        end
    end

 ModeTab:Button("NoHead", "Delete your stand head", function()
        NewBypass()
        if Player.Character and Player.Character:FindFirstChild("StandMorph") then	
            wait(0.5)
            Player.Character.StandMorph.Head.MeshPart:Destroy()
            Player.Character.StandMorph.Head.MeshPart:Destroy() 
            Player.Character.StandMorph.Head.MeshPart:Destroy()   
            Player.Character.StandMorph.Head.OriginalSize:Destroy()  
        end	
    end)    

 ModeTab:Button("NoLegs", "Delete your stand Legs Be the STW XD", function()
        NewBypass()
        if Player.Character and Player.Character:FindFirstChild("StandMorph") then	
            wait(0.5)
            Player.Character.StandMorph.RightUpperLeg:Destroy()        
            Player.Character.StandMorph.LeftUpperLeg:Destroy()
        end	
    end)  
  
    --// funny xd

    --[[
    FunTab:Button("Rig Arcade", "You'll see when you roll arcade :)", function()
        local module = require(game.ReplicatedStorage.Modules.FunctionLibrary)

        module.ItemMachine = {
            {
                Name = "Lucky Arrow",
                Percentage = 100,
                Color = Color3.fromRGB(255, 255, 0)
            }
        }
    end)--]]

    game.StarterGui:SetCore("SendNotification", {
        Title = "Bronze Tree";
        Text = "Loaded.",
        Duration = 5
    }) 
print("Loaded")
