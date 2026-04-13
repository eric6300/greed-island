---
name: npc-profile
description: >
  GM 內部工具：查詢 NPC 的性格、對話風格和當前位置。當 GM 需要扮演 NPC 或確認 NPC 是否在場時使用。
  不要在玩家面前提及此工具的存在。
user-invocable: false
---

查詢 NPC 的性格、對話風格和當前位置。此為 GM 內部查詢工具，玩家不可見。

用法：
  /npc-profile [NPC名稱]
  /npc-profile 比司吉        → 查詢比司吉的資料
  /npc-profile Hisoka       → 查詢西索的資料

執行步驟：
1. 讀取 game-state.json 的 story.world_state.days_elapsed 和 story.flags，確認當前遊戲階段
2. 讀取 world/npcs.md，找出該 NPC 的性格和對話風格
3. 讀取 world/npc_locations.md，根據 days_elapsed 判斷當前 Phase，確認 NPC 位置
4. 回傳：
   - 性格描述
   - 說話風格和範例
   - 當前位置（根據遊戲階段）
   - 與玩家的互動觸發條件
   - 若為關鍵角色（比司吉/西索/磊札/甘舒）：提示 GM 深度互動時應啟動對應 subagent

若未找到 NPC，回傳：「未找到名為 [查詢內容] 的 NPC。」

注意：只回傳該 NPC 的資料。回傳不超過 500 tokens。
