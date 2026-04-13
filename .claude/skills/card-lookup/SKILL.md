---
name: card-lookup
description: >
  GM 內部工具：搜尋貪婪之島的卡牌資料。當 GM 需要查詢卡牌名稱、編號、效果或取得條件時使用。
  不要在玩家面前提及此工具的存在。
user-invocable: false
---

搜尋貪婪之島的卡牌資料。此為 GM 內部查詢工具，玩家不可見。

用法：
  /card-lookup [卡牌名稱或編號]
  /card-lookup #025         → 查詢第 25 號限定卡
  /card-lookup 咒語卡       → 列出所有咒語卡
  /card-lookup Accompany    → 搜尋特定咒語卡

執行步驟：
1. 根據查詢類型決定讀取哪些檔案：
   - 編號查詢（#000-#099）→ 讀取 world/cards/specified_slots.md
   - 咒語卡查詢 → 讀取 world/cards/spell_cards.md
   - 自由卡查詢 → 讀取 world/cards/free_cards.md
   - 名稱查詢 → 依序搜尋以上三個檔案直到找到
2. 找出相關資料，回傳摘要（不超過 500 tokens）
3. 回傳格式：卡牌名稱、編號、等級、效果、取得條件

若未找到匹配的卡牌，回傳：「未找到名為 [查詢內容] 的卡牌。」

注意：只回傳查詢到的資料，不描述搜尋過程。
