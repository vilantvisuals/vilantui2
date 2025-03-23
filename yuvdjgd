-- Full UI Library with Enlarged and Well-Aligned UI Elements
-- quick note, ronaldo is the goat.

local Lib = {}

local tweenService = game:GetService("TweenService")
local UIS = game:GetService("UserInputService")

function Lib:Drag(frame, parent)
    parent = parent or frame
    local dragging, dragInput, dragStart, startPos

    local function update(input)
        local delta = input.Position - dragStart
        local position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        tweenService:Create(parent, TweenInfo.new(0.25), {Position = position}):Play()
    end

    frame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            startPos = parent.Position
            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    UIS.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
            if dragging then
                update(input)
            end
        end
    end)
end

function Lib.Window(Title)
    Title = Title or "UI Library"

    local UiLib = Instance.new("ScreenGui")
    local Main = Instance.new("Frame")
    local MainCorner = Instance.new("UICorner")
    local TabFrame = Instance.new("Frame")
    local UICorner = Instance.new("UICorner")
    local TabNavigator = Instance.new("ScrollingFrame")
    local UIPadding = Instance.new("UIPadding")
    local UIListLayout = Instance.new("UIListLayout")
    local TopBar = Instance.new("Frame")
    local TopCorner = Instance.new("UICorner")
    local LibraryTitle = Instance.new("TextLabel")
    local ContentHolder = Instance.new("Folder")

    -- Enlarged UI sizes
    Main.Size = UDim2.new(0, 700, 0, 500)
    Main.Position = UDim2.new(0.5, -350, 0.5, -250)

    -- UI Properties
    UiLib.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
    UiLib.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

    Main.Parent = UiLib
    Main.BackgroundColor3 = Color3.fromRGB(31, 25, 44)
    Main.ZIndex = 2

    MainCorner.CornerRadius = UDim.new(0, 15)
    MainCorner.Parent = Main

    -- Draggable top bar
    TopBar.Size = UDim2.new(1, 0, 0, 60)
    TopBar.BackgroundColor3 = Color3.fromRGB(18, 15, 24)
    TopBar.Parent = Main

    TopCorner.CornerRadius = UDim.new(0, 15)
    TopCorner.Parent = TopBar

    LibraryTitle.Text = "UI Library"
    LibraryTitle.Parent = TopBar
    LibraryTitle.Size = UDim2.new(0, 300, 0, 50)
    LibraryTitle.TextScaled = true
    LibraryTitle.TextColor3 = Color3.fromRGB(227, 227, 227)
    LibraryTitle.BackgroundTransparency = 1
    LibraryTitle.Font = Enum.Font.SourceSansBold

    Lib:Drag(TopBar, Main)

    -- Tab Navigator
    TabFrame.Size = UDim2.new(0, 180, 1, -60)
    TabFrame.Position = UDim2.new(0, 0, 0, 60)
    TabFrame.BackgroundColor3 = Color3.fromRGB(18, 15, 24)
    TabFrame.Parent = Main
    UICorner.Parent = TabFrame

    TabNavigator.Size = UDim2.new(1, 0, 1, 0)
    TabNavigator.Parent = TabFrame
    TabNavigator.CanvasSize = UDim2.new(0, 0, 1, 0)

    ContentHolder.Parent = Main

    local TabSys = {}
    local first = true

    function TabSys.CreateTab(TabTitle)
        local TabContent = Instance.new("ScrollingFrame")
        local TabSwitcher = Instance.new("TextButton")
        local TabCorner = Instance.new("UICorner")
        local ContentLayout = Instance.new("UIListLayout")

        -- Enlarged UI elements
        TabSwitcher.Size = UDim2.new(0, 160, 0, 40)
        TabSwitcher.TextSize = 20
        TabSwitcher.Parent = TabNavigator

        TabContent.Size = UDim2.new(1, -200, 1, -60)
        TabContent.Position = UDim2.new(0, 200, 0, 60)
        TabContent.Parent = ContentHolder
        TabContent.ClipsDescendants = true

        ContentLayout.Parent = TabContent
        ContentLayout.Padding = UDim.new(0, 15)

        if first then
            first = false
            TabContent.Visible = true
            TabSwitcher.BackgroundTransparency = 0.7
        else
            TabContent.Visible = false
            TabSwitcher.BackgroundTransparency = 0.9
        end

        local Content = {}

        function Content.CreateButton(BtnTitle, callback)
            local Button = Instance.new("TextButton")
            Button.Size = UDim2.new(0, 300, 0, 60)
            Button.TextSize = 24
            Button.Text = BtnTitle
            Button.Parent = TabContent
            Button.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
            Button.MouseButton1Click:Connect(callback)
        end

        function Content.CreateToggle(ToggleTitle, callback)
            local Toggle = Instance.new("TextButton")
            Toggle.Size = UDim2.new(0, 300, 0, 60)
            Toggle.TextSize = 24
            Toggle.Text = ToggleTitle
            Toggle.Parent = TabContent
            Toggle.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
            Toggle.MouseButton1Click:Connect(function()
                callback(not Toggle.Active)
                Toggle.Active = not Toggle.Active
            end)
        end

        return Content
    end

    return TabSys
end

return Lib
