# /talk [NPC 名稱] — 與 NPC 對話

與指定的 NPC 進行對話互動。

## 執行流程

1. 委託 game-engine 讀取 game-state.json（location, npc_relationships, story.flags, nen.level）
2. 使用 /npc-profile [NPC名稱] 確認該 NPC 是否在當前位置（根據遊戲階段）

3. **NPC 不在場**：
   「你環顧四周，[NPC名稱] 似乎不在這裡。」
   若知道 NPC 常出沒地點，可暗示：「你隱約記得有人提過，[NPC] 常在 [地點] 一帶活動。」

4. **判斷互動深度**：

   **啟動 Subagent 的條件**（深度互動）：
   - 玩家輸入超過 20 字且明確針對比司吉/西索/磊札/甘舒
   - 特殊事件模式中的 NPC 對話
   - 涉及訓練、合作、威脅、重要決策的對話

   **GM 直接處理**（輕量互動）：
   - 簡短打招呼、路過
   - 一般 NPC（非四大關鍵 NPC）
   - 簡單問答

5. **啟動 Subagent 時**：
   傳入 prompt：
   「玩家想要 [對話目的]。
    當前狀態：念Lv.[level]，[nen.type]，今天是 Day [days_elapsed]。
    關係狀態：[從 npc_relationships 讀取]。
    請以 [NPC名稱] 的身份回應，並根據你的記憶調整態度。」

   接收 subagent 回應，直接呈現給玩家。

6. **GM 直接處理時**：
   根據 /npc-profile 的性格描述，以該 NPC 的語氣回應。
   簡短但保持人格特色。

7. 對話結束後：
   - 更新 npc_relationships（若有變化）
   - 更新 action_count +1
   - 委託 game-engine 寫入 game-state.json
