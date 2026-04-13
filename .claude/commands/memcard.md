# /memcard — 記憶卡狀態

查看記憶卡（存檔）的完整狀態。

## 執行流程

1. 委託 game-engine 讀取 game-state.json
2. 若不存在：回應「尚未開始遊戲。請輸入 /start。」

3. 顯示以下格式：

```
💾 記憶卡

擁有者：[player.name]
通關次數：[memory_card.clear_count] 次
最佳紀錄：[最短天數] 天（[陣營]）  ← 若 clear_count > 0

歷史紀錄：                          ← 若 clear_count > 0
  周目 1 │ [faction] │ [days] 天 │ [ending]
         │ 帶出：[card1]、[card2]、[card3]
  周目 2 │ ...

現在進度：
  位置：[location]
  念等級：[nen.level]（[nen.type]）
  限定卡：[specified_count]/99（#000 另計）
  咒語卡：[spell card count] 張
  Jenny：[jenny]
  遊玩天數：[story.world_state.days_elapsed]
  行動數：[story.world_state.action_count]

傳家寶：
  [heirloom.name]（效率 [efficiency]%）  ← 列出所有，若無則「無」

未解鎖結局：
  [根據 meta_flags 中為 false 的項目列出]
  - 奇犽路線（需要知道考試日期）     ← knew_exam_date = false
  - 拯救 巴特拉 戀人               ← battera_saved = false
  - 取得 大天使的氣息             ← angels_breath_obtained = false
  - TRUE ENDING                      ← true_ending_unlocked = false

⚠ 每個行動都會自動記錄。死亡即為永久。
```

4. 若 clear_count = 0 且無歷史，省略歷史紀錄和最佳紀錄行
5. 以沉浸式語氣描述記憶卡的外觀（微微發光的水晶卡片）
