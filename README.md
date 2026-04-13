# 貪婪之島 × Claude Code

> 基於 Hunter × Hunter 原著漫畫（富樫義博）的文字 RPG 遊戲
> 以 Terminal + Claude Code 為介面

## 開始遊戲

```bash
git clone https://github.com/eric6300/greed-island
cd greed-island
claude
```

進入 Claude Code 後，輸入 `/start` 開始冒險。

## 遊戲特色

- **零依賴**：只需要 git + Claude Code，不需要安裝任何 runtime
- **沉浸式敘事**：GM 以文字描述整個遊戲世界，永遠不跳出角色
- **忠實還原**：100 張限定槽卡、40 張咒語卡、12+ 地點、完整念能力系統
- **Roguelike**：死亡是永久的，每次通關解鎖新的可能性
- **歷史之壁**：某些事件必然發生，你能改變的只有形式
- **NPC 記憶**：關鍵 NPC 會記住你的行為，態度隨互動演變

## 指令一覽

| 指令 | 功能 |
|------|------|
| `/start` | 開始新遊戲或繼續 |
| `/book` | 召喚咒語書，查看卡牌 |
| `/look` | 查看當前場景 |
| `/go [地點]` | 前往指定地點 |
| `/talk [NPC]` | 與 NPC 對話 |
| `/gain` | 撿取場景中的卡牌 |
| `/cards` | 快速查看持有卡牌數量 |
| `/use [卡牌]` | 使用卡牌 |
| `/transform [來源] [目標]` | 卡牌轉換 |
| `/slotin [卡牌]` | 將卡牌放入限定槽 |
| `/clone [卡牌] [對象]` | 複製卡牌給隊友 |
| `/memcard` | 查看記憶卡狀態 |

口語咒語（不需要斜線）：`Book`、`Gain`

## 系統需求

- [Claude Code CLI](https://claude.ai/code)（需有效訂閱）
- Git

## License

MIT License. See [LICENSE](LICENSE) for details.

本遊戲為粉絲作品，非官方授權。
所有 Hunter × Hunter 相關內容版權歸富樫義博及集英社所有。
