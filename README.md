# Hunt Buddy (TW)

**Hunt Buddy** 的 FFXIV 台服（繁體中文客戶端）移植版，用來追蹤每日討伐令（蒼天、紅蓮、漆黑、曉月等）的目標與擊殺進度。

- 原版：https://github.com/SheepGoMeh/HuntBuddy
- 基於版本：原版 commit `768413a68d8670545297b8277f3e74ab42a4454c`（[PR] API 13 Update，2025-08-08，插件版本 1.2.2.0）
- Dalamud API：13（`Dalamud.NET.Sdk/13.0.0`）
- 分支：`tw-api13`

## 遊戲內使用

- `/phb`：開啟主視窗
- `/phb next`：自動挑選下一個要打的討伐目標，並在地圖上插旗
- `/phb local`：切換「目前地區的討伐目標」視窗
- `/phb list`：在聊天欄列出所有討伐目標

![](https://github.com/sheepgomeh/huntbuddy/raw/master/res/image1.png)

## 程式修改

`HuntBuddy/Plugin.cs`（修正原版 bug，原版最新版本仍存在）：

- 在 2.x 地區（例如東拉諾西亞）身上有 2.x 討伐令時，`/phb next` 會因為怪物沒有座標資料而發生 `KeyNotFoundException`。
- 修改後，沒有座標的目標仍會被挑選並在聊天欄顯示，但不插旗。

其他修改：

- `HuntBuddy/HuntBuddy.json`：名稱改為 `Hunt Buddy (TW)`，`RepoUrl` 指向本 repo。`InternalName` 未更動，原本的設定會保留。

## 台服已確認功能

- 主視窗正確讀取已接的討伐令，版本、地區、怪物名稱都顯示中文
- `/phb next` 正常運作（含 2.x 地區）

## 注意事項

- 原作者沒有收錄 2.x（ARR）討伐目標和 B 級精英怪的座標，這兩類不會插旗。
- 「傳送到最近的以太之光」需要另外安裝 Teleporter 插件；搜尋功能需要 XivEsp 插件。沒裝時不影響其他功能。

## 編譯方式

```bat
git checkout tw-api13
set DALAMUD_HOME=%APPDATA%\FFXIVSimpleLauncher\Dalamud\Injector
dotnet build HuntBuddy\HuntBuddy.csproj -c Release
```

產生的檔案在 `HuntBuddy\bin\Release\HuntBuddy.dll`，可在 `/xlsettings` → 實驗性功能 → 開發插件位置加入。

## 原作者與授權

原作者為 Dragon、SheepGoMeh 及其他貢獻者，所有權利歸原作者所有。原 repo 沒有附授權檔案，本 fork 僅供個人在台服使用。

台服版的問題請回報到本 repo，**不要**回報給原作者。
