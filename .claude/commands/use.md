# /use [卡牌名稱] — 使用卡牌

使用持有的卡牌，發動其效果。

## 執行流程

1. 委託 game-engine 讀取 game-state.json（cards）
2. 在 free_slots 和 specified_slots 中搜尋指定卡牌

3. **未找到**：「你沒有持有這張卡牌。」

4. **找到後，依卡牌類型處理**：

   **移動類**（Accompany, Leave, Magnetic Force）：
   - Accompany：指定玩家名或地點 → 傳送（更新 location）
   - Leave：暫時離開貪婪之島（特殊場景）
   - Magnetic Force：傳送到指定玩家位置

   **攻擊類**（Thief, Pickpocket, Levy, Tax Collector's Gauntlet）：
   - 需要指定目標（NPC 或其他玩家）
   - 骰子判定成功率
   - 成功：從目標取得卡牌
   - 失敗：卡牌消耗但無效果

   **防禦類**（Holy Water, Fortress, Blackout Curtain, Breath, Relax）：
   - 應用 buff 效果到 game-state
   - Holy Water：接下來防禦 10 次攻擊型咒語，免疫偷竊
   - Fortress：1 小時（5 個行動）內免疫所有攻擊

   **情報類**（List, Analysis, Trace, Eye of God, Recommend, Lottery, Fluoroscopy）：
   - 揭示對應資訊
   - Eye of God：永久效果（不消耗，標記為永久啟用）

   **治癒類**（Archangel's Breath）：
   - 完全恢復 HP

   **複製類**（Clone）：
   - 需指定要複製的卡和目標隊友 → 使用 /clone 邏輯

   **轉換類**（Return）：
   - 將已使用的卡恢復原始形式（限 C 級以下）

5. 使用後從 slots 移除（除非永久效果）
6. 以戲劇性方式描述卡牌啟動效果
7. 更新 action_count +1
8. 委託 game-engine 寫入 game-state.json

## 限制
- GM 專屬卡（如 Eliminate）玩家無法使用
- 傳家寶卡牌效果按 efficiency 比例降低
