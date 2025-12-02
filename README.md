# Orion Library
This documentation is for the stable release of Orion Library.

## Booting the Library
```lua
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()
```



## Creating a Window
```lua
local Window = OrionLib:MakeWindow({Name = "Title of the library", HidePremium = false, SaveConfig = true, ConfigFolder = "OrionTest"})

--[[
Name = <string> - The name of the UI.
HidePremium = <bool> - Whether or not the user details shows Premium status or not.
SaveConfig = <bool> - Toggles the config saving in the UI.
ConfigFolder = <string> - The name of the folder where the configs are saved.
IntroEnabled = <bool> - Whether or not to show the intro animation.
IntroText = <string> - Text to show in the intro animation.
IntroIcon = <string> - URL to the image you want to use in the intro animation.
Icon = <string> - URL to the image you want displayed on the window.
CloseCallback = <function> - Function to execute when the window is closed.
]]
```



## Creating a Tab
```lua
local Tab = Window:MakeTab({
	Name = "Tab 1",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

--[[
Name = <string> - The name of the tab.
Icon = <string> - The icon of the tab.
PremiumOnly = <bool> - Makes the tab accessible to Sirus Premium users only.
]]
```
## Creating a Section
```lua
local Section = Tab:AddSection({
	Name = "Section"
})

--[[
Name = <string> - The name of the section.
]]
```
You can add elements to sections the same way you would add them to a tab normally.

## Notifying the user
```lua
OrionLib:MakeNotification({
	Name = "Title!",
	Content = "Notification content... what will it say??",
	Image = "rbxassetid://4483345998",
	Time = 5
})

--[[
Title = <string> - The title of the notification.
Content = <string> - The content of the notification.
Image = <string> - The icon of the notification.
Time = <number> - The duration of the notfication.
]]
```



## Creating a Button
```lua
Tab:AddButton({
	Name = "Button!",
	Callback = function()
      		print("button pressed")
  	end    
})

--[[
Name = <string> - The name of the button.
Callback = <function> - The function of the button.
]]
```


## Creating a Checkbox toggle
```lua
Tab:AddToggle({
	Name = "This is a toggle!",
	Default = false,
	Callback = function(Value)
		print(Value)
	end    
})

--[[
Name = <string> - The name of the toggle.
Default = <bool> - The default value of the toggle.
Callback = <function> - The function of the toggle.
]]
```

### Changing the value of an existing Toggle
```lua
CoolToggle:Set(true)
```


### new sample
```lua
OrionLib:AddTheme("DarkBlue", {
    Main = Color3.fromRGB(15, 15, 25),
    Second = Color3.fromRGB(25, 30, 40),
    Stroke = Color3.fromRGB(60, 90, 150),
    Divider = Color3.fromRGB(50, 70, 120),
    Text = Color3.fromRGB(200, 220, 255),
    TextDark = Color3.fromRGB(140, 160, 200)
})

OrionLib:AddTheme("CyberPunk", {
    Main = Color3.fromRGB(10, 10, 15),
    Second = Color3.fromRGB(20, 20, 30),
    Stroke = Color3.fromRGB(255, 0, 150),
    Divider = Color3.fromRGB(0, 255, 200),
    Text = Color3.fromRGB(0, 255, 255),
    TextDark = Color3.fromRGB(255, 0, 150)
})

OrionLib:AddTheme("Forest", {
    Main = Color3.fromRGB(20, 30, 20),
    Second = Color3.fromRGB(30, 45, 30),
    Stroke = Color3.fromRGB(100, 180, 100),
    Divider = Color3.fromRGB(80, 140, 80),
    Text = Color3.fromRGB(200, 255, 200),
    TextDark = Color3.fromRGB(150, 200, 150)
})

OrionLib:AddTheme("Sunset", {
    Main = Color3.fromRGB(30, 20, 25),
    Second = Color3.fromRGB(45, 30, 35),
    Stroke = Color3.fromRGB(255, 120, 80),
    Divider = Color3.fromRGB(200, 100, 120),
    Text = Color3.fromRGB(255, 200, 180),
    TextDark = Color3.fromRGB(200, 150, 140)
})

OrionLib:AddTheme("Ocean", {
    Main = Color3.fromRGB(10, 25, 35),
    Second = Color3.fromRGB(20, 35, 50),
    Stroke = Color3.fromRGB(80, 180, 220),
    Divider = Color3.fromRGB(60, 140, 180),
    Text = Color3.fromRGB(180, 230, 255),
    TextDark = Color3.fromRGB(140, 190, 220)
})


local Window = OrionLib:MakeWindow({
    Name = "Ultimate Hub - デモ",
    Size = {Width = 615, Height = 344},
    SaveConfig = true,
    ConfigFolder = "UltimateHubDemo",
    IntroEnabled = true,
    IntroText = "Ultimate Hub",
    Theme = "DarkBlue",
    Position = "Center"
})

local MainTab = Window:MakeTab({
    Name = "メイン",
    Icon = "rbxassetid://7485051715",
    PremiumOnly = false
})

local Section1 = MainTab:AddSection({
    Name = "基本的な要素"
})

Section1:AddLabel("これはラベルです")

Section1:AddParagraph("パラグラフ", "これは複数行のテキストを表示できるパラグラフ要素です。長いテキストも適切に折り返されます。ほんとあにほんあにたあはあさたらたたたはららたらら")

Section1:AddButton({
    Name = "ボタン",
    Callback = function()
        OrionLib:MakeNotification({
            Name = "ボタン",
            Content = "ボタンがクリックされました！",
            Time = 3
        })
    end
})

local BadgeButton = Section1:AddButtonWithBadge({
    Name = "通知付きボタン",
    BadgeCount = 5,
    Callback = function(btn)
        btn:ClearBadge()
        OrionLib:MakeNotification({
            Name = "バッジ",
            Content = "バッジがクリアされました",
            Time = 3
        })
    end
})

task.spawn(function()
    wait(3)
    BadgeButton:SetBadge(10)
end)

Section1:AddToggle({
    Name = "トグル",
    Default = false,
    Callback = function(Value)
        print("トグル値:", Value)
    end
})

Section1:AddSlider({
    Name = "スライダー",
    Min = 0,
    Max = 100,
    Default = 50,
    Color = Color3.fromRGB(255, 100, 100),
    Increment = 1,
    ValueName = "値",
    Callback = function(Value)
        print("スライダー値:", Value)
    end
})

Section1:AddDropdown({
    Name = "ドロップダウン",
    Default = "オプション1",
    Options = {"オプション1", "オプション2", "オプション3", "オプション4"},
    Callback = function(Value)
        print("選択された値:", Value)
    end
})

Section1:AddBind({
    Name = "キーバインド",
    Default = Enum.KeyCode.E,
    Hold = false,
    Callback = function()
        print("キーが押されました")
    end
})

Section1:AddTextbox({
    Name = "テキストボックス",
    Default = "デフォルトテキスト",
    TextDisappear = false,
    Callback = function(Value)
        print("入力されたテキスト:", Value)
    end
})

Section1:AddColorpicker({
    Name = "カラーピッカー",
    Default = Color3.fromRGB(255, 0, 0),
    Callback = function(Value)
        print("選択された色:", Value)
    end
})

local Section2 = MainTab:AddSection({
    Name = "高度な要素"
})

local ProgressBar = Section2:AddProgressBar({
    Name = "プログレスバー",
    Max = 100,
    Default = 0,
    Color = Color3.fromRGB(0, 255, 100),
    ShowPercentage = true
})

task.spawn(function()
    for i = 1, 100 do
        ProgressBar:Set(i)
        wait(0.05)
    end
end)

local PomodoroTimer = Section2:AddTimer({
    Name = "ポモドーロタイマー (25分)",
    Duration = 1500,
    AutoStart = false,
    OnComplete = function()
        OrionLib:MakeNotification({
            Name = "タイマー完了",
            Content = "25分が経過しました！休憩しましょう。",
            Time = 10
        })
    end,
    OnTick = function(remaining)
    end
})

local RatingWidget = Section2:AddRating({
    Name = "評価",
    Max = 5,
    Default = 0,
    Color = Color3.fromRGB(255, 215, 0),
    Callback = function(value)
        if value >= 4 then
            OrionLib:MakeNotification({
                Name = "ありがとうございます！",
                Content = "高評価をいただきありがとうございます！",
                Time = 5
            })
        end
    end
})

Section2:AddPlayerParagraph(LocalPlayer.UserId)

Section2:AddImageParagraph(
    "rbxassetid://7485051715",
    "これは画像付きパラグラフです。アイコンと一緒にテキストを表示できます。"
)

local UITab = Window:MakeTab({
    Name = "UI設定",
    Icon = "rbxassetid://7734068321",
    PremiumOnly = false
})

local ThemeSection = UITab:AddSection({
    Name = "テーマ設定"
})

ThemeSection:AddLabel("利用可能なテーマ:")

ThemeSection:AddDropdown({
    Name = "テーマ選択",
    Default = "DarkBlue",
    Options = {"Default", "DarkBlue", "CyberPunk", "Forest", "Sunset", "Ocean"},
    Callback = function(Value)
        OrionLib:SetTheme(Value)
        OrionLib:MakeNotification({
            Name = "テーマ変更",
            Content = "テーマを " .. Value .. " に変更しました",
            Time = 3
        })
    end
})

ThemeSection:AddParagraph(
    "テーマについて",
    "異なるテーマを選択してUIの外観を変更できます。各テーマには独自の配色が設定されています。"
)

local NotificationSection = UITab:AddSection({
    Name = "通知テスト"
})

NotificationSection:AddButton({
    Name = "成功通知",
    Callback = function()
        OrionLib:MakeNotification({
            Name = "成功",
            Content = "操作が正常に完了しました",
            Image = "rbxassetid://4384403532",
            Time = 5
        })
    end
})

NotificationSection:AddButton({
    Name = "警告通知",
    Callback = function()
        OrionLib:MakeNotification({
            Name = "警告",
            Content = "注意が必要な操作です",
            Image = "rbxassetid://3610239960",
            Time = 5,
        })
    end
})

NotificationSection:AddButton({
    Name = "エラー通知",
    Callback = function()
        OrionLib:MakeNotification({
            Name = "エラー",
            Content = "エラーが発生しました",
            Image = "rbxassetid://7072725342",
            Time = 5,
        })
    end
})

local ExamplesTab = Window:MakeTab({
    Name = "使用例",
    Icon = "rbxassetid://7733964719",
    PremiumOnly = false
})

local Example1 = ExamplesTab:AddSection({
    Name = "カウンターアプリ"
})

local counterValue = 0
local counterLabel = Example1:AddLabel("カウント: 0")

Example1:AddButton({
    Name = "増加 (+1)",
    Callback = function()
        counterValue = counterValue + 1
        counterLabel:Set("カウント: " .. counterValue)
    end
})

Example1:AddButton({
    Name = "減少 (-1)",
    Callback = function()
        counterValue = counterValue - 1
        counterLabel:Set("カウント: " .. counterValue)
    end
})

Example1:AddButton({
    Name = "リセット",
    Callback = function()
        counterValue = 0
        counterLabel:Set("カウント: " .. counterValue)
    end
})

local Example2 = ExamplesTab:AddSection({
    Name = "設定保存例"
})

Example2:AddToggle({
    Name = "設定1",
    Default = false,
    Save = true,
    Flag = "Setting1",
    Callback = function(Value)
        print("設定1:", Value)
    end
})

Example2:AddSlider({
    Name = "設定2",
    Min = 0,
    Max = 100,
    Default = 50,
    Save = true,
    Flag = "Setting2",
    Callback = function(Value)
        print("設定2:", Value)
    end
})

Example2:AddColorpicker({
    Name = "色設定",
    Default = Color3.fromRGB(255, 255, 255),
    Save = true,
    Flag = "ColorSetting",
    Callback = function(Value)
        print("色設定:", Value)
    end
})

local Example3 = ExamplesTab:AddSection({
    Name = "動的コンテンツ"
})

local dynamicDropdown = Example3:AddDropdown({
    Name = "動的ドロップダウン",
    Default = "アイテム1",
    Options = {"アイテム1", "アイテム2", "アイテム3"},
    Callback = function(Value)
        print("選択:", Value)
    end
})

Example3:AddButton({
    Name = "オプションを追加",
    Callback = function()
        local newOptions = {}
        for i = 1, 10 do
            table.insert(newOptions, "アイテム" .. i)
        end
        dynamicDropdown:Refresh(newOptions, true)
        OrionLib:MakeNotification({
            Name = "更新",
            Content = "ドロップダウンが更新されました",
            Time = 3
        })
    end
})

local InfoTab = Window:MakeTab({
    Name = "情報",
    Icon = "rbxassetid://7734053426",
    PremiumOnly = false
})

local InfoSection = InfoTab:AddSection({
    Name = "ライブラリ情報"
})

InfoSection:AddParagraph(
    "Ultimate Hub",
    "これは高度なUI機能を持つカスタムライブラリのデモンストレーションです。"
)

InfoSection:AddLabel("バージョン: 1.0.0")
InfoSection:AddLabel("作成者: HfSapSatu & Team")

InfoSection:AddParagraph(
    "機能一覧",
    "• 複数のテーマサポート\n• プログレスバー\n• タイマー機能\n• 評価システム\n• バッジ付きボタン\n• プレイヤー情報表示\n• 画像付きパラグラフ\n• 設定の保存/読み込み\n• カスタム通知\n• 検索機能"
)

local StatsSection = InfoTab:AddSection({
    Name = "統計情報"
})

local fpsLabel = StatsSection:AddLabel("FPS: 計算中...")
local pingLabel = StatsSection:AddLabel("Ping: 計算中...")
local memoryLabel = StatsSection:AddLabel("メモリ: 計算中...")

task.spawn(function()
    while true do
        local fps = math.floor(1 / game:GetService("RunService").RenderStepped:Wait())
        fpsLabel:Set("FPS: " .. fps)
        
        local ping = math.floor(game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValue())
        pingLabel:Set("Ping: " .. ping .. " ms")
        
        local memory = math.floor(game:GetService("Stats"):GetTotalMemoryUsageMb())
        memoryLabel:Set("メモリ: " .. memory .. " MB")
        
        wait(1)
    end
end)

local CreditsTab = Window:MakeTab({
    Name = "クレジット",
    Icon = "rbxassetid://7734068321",
    PremiumOnly = false
})

local CreditsSection = CreditsTab:AddSection({
    Name = "開発チーム"
})

CreditsSection:AddPlayerParagraph(LocalPlayer.UserId)

CreditsSection:AddParagraph(
    "特別な感謝",
    "このライブラリの開発に協力してくれた全ての人に感謝します。"
)

CreditsSection:AddButton({
    Name = "Discordに参加",
    Callback = function()
        OrionLib:MakeNotification({
            Name = "Discord",
            Content = "Discordサーバーリンクがクリップボードにコピーされました",
            Time = 5
        })
    end
})

CreditsSection:AddButton({
    Name = "GitHubを開く",
    Callback = function()
        OrionLib:MakeNotification({
            Name = "GitHub",
            Content = "GitHubリポジトリリンクがクリップボードにコピーされました",
            Time = 5
        })
    end
})

OrionLib:MakeNotification({
    Name = "ようこそ！",
    Content = "Ultimate Hubへようこそ。各タブを確認して機能を試してください。",
    Image = "rbxassetid://4384403532",
    Time = 8
})
-- 既存のExamplesTabの後に追加

local AdvancedTab = Window:MakeTab({
    Name = "高度な要素",
    Icon = "rbxassetid://7733920644",
    PremiumOnly = false
})

-- 1. コードエディターのデモ
local EditorSection = AdvancedTab:AddSection({
    Name = "コードエディター"
})

EditorSection:AddParagraph(
    "コードエディター",
    "シンタックスハイライト付きの複数行テキストエディター。コードの編集やスクリプトの作成に最適です。"
)

local codeEditor = EditorSection:AddCodeEditor({
    Name = "Luaスクリプトエディター",
    Default = [[-- サンプルコード
local function greet(name)
    print("Hello, " .. name .. "!")
end

greet("World")]],
    Height = 180,
    Callback = function(code)
        print("コードが更新されました:", code)
    end
})

EditorSection:AddButton({
    Name = "コードを実行",
    Callback = function()
        local code = codeEditor:Get()
        local success, result = pcall(function()
            loadstring(code)()
        end)
        if success then
            OrionLib:MakeNotification({
                Name = "実行成功",
                Content = "コードが正常に実行されました",
                Time = 3
            })
        else
            OrionLib:MakeNotification({
                Name = "実行エラー",
                Content = "エラー: " .. tostring(result),
                Time = 5
            })
        end
    end
})

EditorSection:AddButton({
    Name = "コードをリセット",
    Callback = function()
        codeEditor:Set("-- ここにコードを入力してください")
    end
})

-- 2. タブコンテナのデモ
local TabContainerSection = AdvancedTab:AddSection({
    Name = "タブコンテナ"
})

TabContainerSection:AddParagraph(
    "タブコンテナ",
    "複数のタブを持つコンテナ。関連する設定やオプションをグループ化して整理できます。"
)

local tabContainer = TabContainerSection:AddTabContainer({
    Name = "設定タブ",
    Tabs = {"一般", "グラフィック", "オーディオ", "ゲームプレイ"},
    Default = "一般"
})

-- 各タブにコンテンツを追加
local generalTab = tabContainer:GetTab("一般")
generalTab:AddLabel("一般設定")
generalTab:AddToggle({
    Name = "自動保存",
    Default = true,
    Callback = function(value)
        print("自動保存:", value)
    end
})
generalTab:AddSlider({
    Name = "UI スケール",
    Min = 80,
    Max = 120,
    Default = 100,
    ValueName = "%",
    Callback = function(value)
        print("UIスケール:", value)
    end
})

local graphicsTab = tabContainer:GetTab("グラフィック")
graphicsTab:AddLabel("グラフィック設定")
graphicsTab:AddDropdown({
    Name = "品質",
    Options = {"低", "中", "高", "最高"},
    Default = "高",
    Callback = function(value)
        print("品質:", value)
    end
})
graphicsTab:AddToggle({
    Name = "影を有効化",
    Default = true,
    Callback = function(value)
        print("影:", value)
    end
})
graphicsTab:AddToggle({
    Name = "アンチエイリアス",
    Default = false,
    Callback = function(value)
        print("AA:", value)
    end
})

local audioTab = tabContainer:GetTab("オーディオ")
audioTab:AddLabel("オーディオ設定")
audioTab:AddSlider({
    Name = "マスターボリューム",
    Min = 0,
    Max = 100,
    Default = 80,
    ValueName = "%",
    Callback = function(value)
        print("マスターボリューム:", value)
    end
})
audioTab:AddSlider({
    Name = "BGMボリューム",
    Min = 0,
    Max = 100,
    Default = 60,
    ValueName = "%",
    Callback = function(value)
        print("BGM:", value)
    end
})
audioTab:AddSlider({
    Name = "効果音ボリューム",
    Min = 0,
    Max = 100,
    Default = 70,
    ValueName = "%",
    Callback = function(value)
        print("効果音:", value)
    end
})

local gameplayTab = tabContainer:GetTab("ゲームプレイ")
gameplayTab:AddLabel("ゲームプレイ設定")
gameplayTab:AddSlider({
    Name = "マウス感度",
    Min = 1,
    Max = 10,
    Default = 5,
    Callback = function(value)
        print("感度:", value)
    end
})
gameplayTab:AddToggle({
    Name = "インバート Y軸",
    Default = false,
    Callback = function(value)
        print("Yインバート:", value)
    end
})

-- 3. ファイルインプットのデモ
local FileSection = AdvancedTab:AddSection({
    Name = "ファイル入力"
})

FileSection:AddParagraph(
    "ファイル入力",
    "ファイルのアップロードやインポート機能。設定ファイルの読み込みなどに使用できます。"
)

local fileInput = FileSection:AddFileInput({
    Name = "設定ファイルをインポート",
    AllowedExtensions = {".json", ".txt", ".cfg"},
    Callback = function(fileName, fileContent)
        OrionLib:MakeNotification({
            Name = "ファイル読み込み",
            Content = "ファイル名: " .. fileName,
            Time = 5
        })
        print("ファイル内容:", fileContent)
    end
})

FileSection:AddButton({
    Name = "サンプルファイルをロード",
    Callback = function()
        local sampleData = {
            setting1 = true,
            setting2 = 50,
            setting3 = "option1"
        }
        OrionLib:MakeNotification({
            Name = "サンプルロード",
            Content = "サンプル設定がロードされました",
            Time = 3
        })
        print("サンプルデータ:", game:GetService("HttpService"):JSONEncode(sampleData))
    end
})

-- 4. データテーブルのデモ
local TableSection = AdvancedTab:AddSection({
    Name = "データテーブル"
})

TableSection:AddParagraph(
    "データテーブル",
    "ソート可能なデータテーブル。プレイヤー情報や統計データの表示に最適です。"
)

local sampleData = {
    {"Player1", 1250, "オンライン"},
    {"Player2", 890, "オフライン"},
    {"Player3", 2100, "オンライン"},
    {"Player4", 450, "オンライン"},
    {"Player5", 1680, "オフライン"},
    {"Player6", 3200, "オンライン"},
    {"Player7", 720, "オフライン"}
}

local dataTable = TableSection:AddDataTable({
    Name = "プレイヤーランキング",
    Columns = {"プレイヤー", "スコア", "ステータス"},
    Data = sampleData,
    RowHeight = 32
})

TableSection:AddButton({
    Name = "新しいプレイヤーを追加",
    Callback = function()
        local randomScore = math.random(100, 3000)
        local randomStatus = math.random(1, 2) == 1 and "オンライン" or "オフライン"
        dataTable:AddRow({"Player" .. math.random(100, 999), randomScore, randomStatus})
        OrionLib:MakeNotification({
            Name = "プレイヤー追加",
            Content = "新しいプレイヤーが追加されました",
            Time = 2
        })
    end
})

TableSection:AddButton({
    Name = "テーブルをクリア",
    Callback = function()
        dataTable:Clear()
        OrionLib:MakeNotification({
            Name = "クリア完了",
            Content = "テーブルがクリアされました",
            Time = 2
        })
    end
})

TableSection:AddButton({
    Name = "サンプルデータを再読み込み",
    Callback = function()
        dataTable.Data = sampleData
        dataTable:Refresh()
        OrionLib:MakeNotification({
            Name = "再読み込み",
            Content = "サンプルデータを再読み込みしました",
            Time = 2
        })
    end
})

-- 5. クイックアクションのデモ
local QuickActionsSection = AdvancedTab:AddSection({
    Name = "クイックアクション"
})

QuickActionsSection:AddParagraph(
    "クイックアクション",
    "よく使う機能へのショートカットボタン。グリッド状に配置されます。"
)

local quickActions = QuickActionsSection:AddQuickActions({
    Name = "便利機能",
    Actions = {
        {
            Name = "通知",
            Icon = "rbxassetid://7733920644",
            Callback = function()
                OrionLib:MakeNotification({
                    Name = "テスト通知",
                    Content = "クイックアクションから実行されました",
                    Time = 3
                })
            end
        },
        {
            Name = "リセット",
            Icon = "rbxassetid://7734000129",
            Callback = function()
                OrionLib:MakeNotification({
                    Name = "リセット",
                    Content = "設定をリセットしました",
                    Time = 3
                })
            end
        },
        {
            Name = "保存",
            Icon = "rbxassetid://7734053495",
            Callback = function()
                if OrionLib.SaveCfg then
                    SaveCfg(game.GameId)
                    OrionLib:MakeNotification({
                        Name = "保存完了",
                        Content = "設定が保存されました",
                        Time = 3
                    })
                end
            end
        },
        {
            Name = "ヘルプ",
            Icon = "rbxassetid://7734053426",
            Callback = function()
                OrionLib:MakeNotification({
                    Name = "ヘルプ",
                    Content = "ドキュメントを開きます",
                    Time = 3
                })
            end
        },
        {
            Name = "更新",
            Icon = "rbxassetid://7734056813",
            Callback = function()
                OrionLib:MakeNotification({
                    Name = "更新チェック",
                    Content = "最新バージョンを確認中...",
                    Time = 3
                })
            end
        },
        {
            Name = "テーマ",
            Icon = "rbxassetid://7734068321",
            Callback = function()
                local themes = {"Default", "DarkBlue", "CyberPunk", "Forest", "Sunset", "Ocean"}
                local randomTheme = themes[math.random(1, #themes)]
                OrionLib:SetTheme(randomTheme)
                OrionLib:MakeNotification({
                    Name = "テーマ変更",
                    Content = "ランダムテーマ: " .. randomTheme,
                    Time = 3
                })
            end
        },
        {
            Name = "統計",
            Icon = "rbxassetid://7733992358",
            Callback = function()
                local fps = math.floor(1 / game:GetService("RunService").RenderStepped:Wait())
                local ping = math.floor(game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValue())
                OrionLib:MakeNotification({
                    Name = "統計情報",
                    Content = string.format("FPS: %d | Ping: %dms", fps, ping),
                    Time = 5
                })
            end
        },
        {
            Name = "スクショ",
            Icon = "rbxassetid://7734053495",
            Callback = function()
                OrionLib:MakeNotification({
                    Name = "スクリーンショット",
                    Content = "スクリーンショットを撮影しました",
                    Time = 3
                })
            end
        }
    }
})

-- 実用例: すべての高度な要素を組み合わせた例
local CombinedSection = AdvancedTab:AddSection({
    Name = "統合デモ"
})

CombinedSection:AddParagraph(
    "統合デモ",
    "複数の高度な要素を組み合わせた実用的な例です。"
)

-- スクリプトマネージャー風のUI
local scriptManager = CombinedSection:AddTabContainer({
    Name = "スクリプトマネージャー",
    Tabs = {"スクリプト", "履歴", "設定"},
    Default = "スクリプト"
})

local scriptsTab = scriptManager:GetTab("スクリプト")
scriptsTab:AddLabel("保存されたスクリプト")

local scriptTable = scriptsTab:AddDataTable({
    Name = "スクリプトリスト",
    Columns = {"名前", "サイズ", "日付"},
    Data = {
        {"AutoFarm.lua", "2.5KB", "2024/12/01"},
        {"ESP.lua", "1.8KB", "2024/12/02"},
        {"SpeedHack.lua", "1.2KB", "2024/12/02"}
    },
    RowHeight = 28
})

local historyTab = scriptManager:GetTab("履歴")
historyTab:AddLabel("実行履歴")
local executionCount = historyTab:AddLabel("実行回数: 0")
local lastExecution = historyTab:AddLabel("最終実行: なし")

local execCount = 0
historyTab:AddButton({
    Name = "履歴をクリア",
    Callback = function()
        execCount = 0
        executionCount:Set("実行回数: 0")
        lastExecution:Set("最終実行: なし")
    end
})

local settingsTab = scriptManager:GetTab("設定")
settingsTab:AddLabel("マネージャー設定")
settingsTab:AddToggle({
    Name = "自動実行",
    Default = false,
    Callback = function(value)
        print("自動実行:", value)
    end
})
settingsTab:AddToggle({
    Name = "実行前に確認",
    Default = true,
    Callback = function(value)
        print("確認:", value)
    end
})

-- アクションボタン
CombinedSection:AddQuickActions({
    Name = "スクリプト操作",
    Actions = {
        {
            Name = "実行",
            Icon = "rbxassetid://7733964719",
            Callback = function()
                execCount = execCount + 1
                executionCount:Set("実行回数: " .. execCount)
                lastExecution:Set("最終実行: " .. os.date("%H:%M:%S"))
                OrionLib:MakeNotification({
                    Name = "実行",
                    Content = "スクリプトを実行しました",
                    Time = 2
                })
            end
        },
        {
            Name = "編集",
            Icon = "rbxassetid://7734053495",
            Callback = function()
                OrionLib:MakeNotification({
                    Name = "編集",
                    Content = "エディターを開きます",
                    Time = 2
                })
            end
        },
        {
            Name = "削除",
            Icon = "rbxassetid://7072725342",
            Callback = function()
                OrionLib:MakeNotification({
                    Name = "削除",
                    Content = "選択したスクリプトを削除しました",
                    Time = 2
                })
            end
        },
        {
            Name = "共有",
            Icon = "rbxassetid://7733992358",
            Callback = function()
                OrionLib:MakeNotification({
                    Name = "共有",
                    Content = "リンクをクリップボードにコピーしました",
                    Time = 3
                })
            end
        }
    }
})

-- パフォーマンスモニター
local PerformanceSection = AdvancedTab:AddSection({
    Name = "パフォーマンスモニター"
})

local perfData = {
    {"FPS", "60", "正常"},
    {"Ping", "45ms", "良好"},
    {"メモリ", "512MB", "正常"},
    {"CPU", "35%", "正常"}
}

local perfTable = PerformanceSection:AddDataTable({
    Name = "システム情報",
    Columns = {"項目", "値", "状態"},
    Data = perfData,
    RowHeight = 30
})

-- リアルタイム更新
task.spawn(function()
    while wait(2) do
        if not OrionLib:IsRunning() then break end
        
        local fps = math.floor(1 / game:GetService("RunService").RenderStepped:Wait())
        local ping = math.floor(game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValue())
        local memory = math.floor(game:GetService("Stats"):GetTotalMemoryUsageMb())
        
        local fpsStatus = fps >= 50 and "正常" or fps >= 30 and "注意" or "警告"
        local pingStatus = ping <= 100 and "良好" or ping <= 200 and "普通" or "悪い"
        local memStatus = memory <= 1000 and "正常" or memory <= 2000 and "注意" or "警告"
        
        perfTable.Data = {
            {"FPS", tostring(fps), fpsStatus},
            {"Ping", ping .. "ms", pingStatus},
            {"メモリ", memory .. "MB", memStatus},
            {"CPU", math.random(20, 60) .. "%", "正常"}
        }
        perfTable:Refresh()
    end
end)

PerformanceSection:AddQuickActions({
    Name = "システム操作",
    Actions = {
        {
            Name = "最適化",
            Icon = "rbxassetid://7734056813",
            Callback = function()
                OrionLib:MakeNotification({
                    Name = "最適化",
                    Content = "システムを最適化しています...",
                    Time = 3
                })
            end
        },
        {
            Name = "GC実行",
            Icon = "rbxassetid://7733920644",
            Callback = function()
                collectgarbage("collect")
                OrionLib:MakeNotification({
                    Name = "ガベージコレクション",
                    Content = "メモリをクリーンアップしました",
                    Time = 2
                })
            end
        }
    }
})
```
## Creating a Color Picker
```lua
Tab:AddColorpicker({
	Name = "Colorpicker",
	Default = Color3.fromRGB(255, 0, 0),
	Callback = function(Value)
		print(Value)
	end	  
})

--[[
Name = <string> - The name of the colorpicker.
Default = <color3> - The default value of the colorpicker.
Callback = <function> - The function of the colorpicker.
]]
```

### Setting the color picker's value
```lua
ColorPicker:Set(Color3.fromRGB(255,255,255))
```


## Creating a Slider
```lua
Tab:AddSlider({
	Name = "Slider",
	Min = 0,
	Max = 20,
	Default = 5,
	Color = Color3.fromRGB(255,255,255),
	Increment = 1,
	ValueName = "bananas",
	Callback = function(Value)
		print(Value)
	end    
})

--[[
Name = <string> - The name of the slider.
Min = <number> - The minimal value of the slider.
Max = <number> - The maxium value of the slider.
Increment = <number> - How much the slider will change value when dragging.
Default = <number> - The default value of the slider.
ValueName = <string> - The text after the value number.
Callback = <function> - The function of the slider.
]]
```

### Change Slider Value
```lua
Slider:Set(2)
```
Make sure you make your slider a variable (local CoolSlider = Tab:AddSlider...) for this to work.


## Creating a Label
```lua
Tab:AddLabel("Label")
```

### Changing the value of an existing label
```lua
CoolLabel:Set("Label New!")
```


## Creating a Paragraph
```lua
Tab:AddParagraph("Paragraph","Paragraph Content")
```

### Changing an existing paragraph
```lua
CoolParagraph:Set("Paragraph New!", "New Paragraph Content!")
```
## Player a Paragraph 
```lua
local playerPara = Main_Tab:AddPlayerParagraph(7059643752, "説明文")
```
## Inage a Paragraph 
```lua
local myParagraph = Main_Tab:AddImageParagraph("rbxassetid://123456789", "最初のテキストです。")
```
## Creating an Adaptive Input
```lua
Tab:AddTextbox({
	Name = "Textbox",
	Default = "default box input",
	TextDisappear = true,
	Callback = function(Value)
		print(Value)
	end	  
})

--[[
Name = <string> - The name of the textbox.
Default = <string> - The default value of the textbox.
TextDisappear = <bool> - Makes the text disappear in the textbox after losing focus.
Callback = <function> - The function of the textbox.
]]
```


## Creating a Keybind
```lua
Tab:AddBind({
	Name = "Bind",
	Default = Enum.KeyCode.E,
	Hold = false,
	Callback = function()
		print("press")
	end    
})

--[[
Name = <string> - The name of the bind.
Default = <keycode> - The default value of the bind.
Hold = <bool> - Makes the bind work like: Holding the key > The bind returns true, Not holding the key > Bind returns false.
Callback = <function> - The function of the bind.
]]
```

### Chaning the value of a bind
```lua
Bind:Set(Enum.KeyCode.E)
```


## Creating a Dropdown menu
```lua
Tab:AddDropdown({
	Name = "Dropdown",
	Default = "1",
	Options = {"1", "2"},
	Callback = function(Value)
		print(Value)
	end    
})
```
## Multidropdown
```lua
local multiDropdown = Main_Tab:AddMultipleDropdown({
    Name = "使える武器",
    Options = {"剣", "弓", "杖", "斧"},
    Default = "剣",
    Callback = function(selectedValues)
        print("選んだ武器: "..table.concat(selectedValues, ", "))
    end,
    Flag = "WeaponDropdown"
})
```

## PlayerDropdown
```lua
local playerDropdown = Main_Tab:AddPlayersDropdown({
    Name = "ターゲット選択",
    MultipleSelection = true, -- 複数選択にする場合
    Callback = function(selectedPlayers)
        for _, name in ipairs(selectedPlayers) do
            print("ターゲット: "..name)
        end
    end,
    Flag = "PlayerDropdown"
})

```
### Adding a set of new Dropdown buttons to an existing menu
```lua
Dropdown:Refresh(List<table>,true)
```

The above boolean value "true" is whether or not the current buttons will be deleted.
### Selecting a dropdown option
```lua
Dropdown:Set("dropdown option")
```

# Finishing your script (REQUIRED)
The below function needs to be added at the end of your code.
```lua
OrionLib:Init()
```

### How flags work.
The flags feature in the ui may be confusing for some people. It serves the purpose of being the ID of an element in the config file, and makes accessing the value of an element anywhere in the code possible.
Below in an example of using flags.
```lua
Tab1:AddToggle({
    Name = "Toggle",
    Default = true,
    Save = true,
    Flag = "toggle"
})

print(OrionLib.Flags["toggle"].Value) -- prints the value of the toggle.
```
Flags only work with the toggle, slider, dropdown, bind, and colorpicker.

### Making your interface work with configs.
In order to make your interface use the configs function you first need to add the `SaveConfig` and `ConfigFolder` arguments to your window function. The explanation of these arguments in above.
Then you need to add the `Flag` and `Save` values to every toggle, slider, dropdown, bind, and colorpicker you want to include in the config file.
The `Flag = <string>` argument is the ID of an element in the config file.
The `Save = <bool>` argument includes the element in the config file.
Config files are made for every game the library is launched in.

## Destroying the Interface
```lua
OrionLib:Destroy()
```
