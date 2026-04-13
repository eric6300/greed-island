# /cards — 快速查看卡牌數量

簡潔顯示當前持有的卡牌統計。

## 執行流程

1. 委託 game-engine 讀取 game-state.json 的 cards 區段

2. 統計並顯示：

```
📊 卡牌統計
限定槽：[specified_count]/99（#000 另計）
咒語卡：[spell card count] 張
自由卡：[other free cards]/45 張
傳家寶：[heirloom count] 張
合計：[total] 張
```

3. 不更新 action_count（純查詢指令）
