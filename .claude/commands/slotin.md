# /slotin [卡牌名稱] — 放入限定槽

將符合條件的卡牌從自由槽移動到對應的限定槽。

## 執行流程

1. 委託 game-engine 讀取 game-state.json（cards）
2. 在 free_slots 中尋找指定卡牌

3. **未找到**：「你的自由槽中沒有這張卡牌。」

4. **找到後**：
   - 確認此卡牌屬於某個限定槽（使用 /card-lookup 確認編號）
   - 若不屬於限定槽：「這張卡牌不屬於任何限定槽。」
   - 若對應限定槽已有卡牌：「限定槽 #[number] 已經有 [existing card] 了。」
   - 若可放入：
     a. 從 free_slots 移除
     b. 加入 specified_slots（key = 槽號，value = 卡牌資料）
     c. specified_count +1
     d. 描述卡牌滑入 Book 的限定槽位，邊框轉為紅色

5. 更新 action_count +1
6. 委託 game-engine 寫入 game-state.json
