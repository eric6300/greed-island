# /transform [來源卡牌] [目標] — 卡牌轉換

將卡牌轉換為實體物品，或使用 Return 卡恢復已使用的卡牌。

## 執行流程

1. 委託 game-engine 讀取 game-state.json（cards）
2. 確認來源卡牌存在於 Book 中

3. **卡牌 → 實體物品**：
   - 將卡牌從 Book 中移除
   - 描述卡牌化為光芒，凝聚成實體物品
   - 物品可在遊戲中直接使用（如汽油、武器等）
   - 注意：實體物品無法再變回卡牌（除非重新滿足取得條件並 Gain）

4. **使用 Return 卡恢復**：
   - 確認持有 Return 咒語卡
   - 確認目標卡牌為 C 級以下
   - 消耗 Return 卡
   - 恢復目標卡牌到原始狀態

5. 更新 action_count +1
6. 委託 game-engine 寫入 game-state.json
