# /clone [卡牌名稱] [隊友名稱] — 複製卡牌給隊友

使用 Clone 咒語卡將一張卡牌複製給隊友。

## 執行流程

1. 委託 game-engine 讀取 game-state.json（cards, party）

2. **檢查 Clone 咒語卡**：
   - 在 free_slots 中尋找 Clone 咒語卡
   - 若未持有：「你需要持有 Clone 咒語卡才能進行複製。」

3. **檢查目標卡牌**：
   - 確認指定卡牌存在於 Book 中
   - 若不存在：「你沒有持有 [卡牌名稱]。」

4. **檢查隊友**：
   - 確認指定隊友在 party 中
   - 若不在：「[隊友名稱] 不在你的隊伍中。」

5. **執行複製**：
   - 消耗一張 Clone 咒語卡
   - 原始卡牌保留在玩家 Book 中
   - 描述複製過程：卡牌發出金光，一張完全相同的副本浮現，飄向隊友的 Book
   - 記錄複製事件

6. 更新 action_count +1
7. 委託 game-engine 寫入 game-state.json

## 限制
- 每次複製消耗一張 Clone 卡
- GM 專屬卡無法複製
- SS 級卡牌無法複製
