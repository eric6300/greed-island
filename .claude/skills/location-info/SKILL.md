---
name: location-info
description: >
  GM 內部工具：查詢貪婪之島的地點資訊。當 GM 需要描述場景、確認地點設施或判斷移動路線時使用。
  不要在玩家面前提及此工具的存在。
user-invocable: false
---

查詢貪婪之島的地點資訊。此為 GM 內部查詢工具，玩家不可見。

用法：
  /location-info [地點名稱]
  /location-info Masadora    → 查詢 Masadora 的詳細資訊
  /location-info Antokiba    → 查詢 Antokiba 的設施和活動

執行步驟：
1. 讀取 world/locations.md，找到指定地點
2. 讀取 world/shops.md（若該地點有商店）
3. 回傳：
   - 地點描述（氛圍、外觀）
   - 可用設施（商店、競技場等）
   - 特殊機制（進入條件、特殊規則）
   - 該地點可遇到的 NPC
   - 連接地點及距離（相鄰 = 短途，非相鄰 = 長途 +1 天）
   - 可取得的卡牌提示

若未找到地點，回傳：「未找到名為 [查詢內容] 的地點。」

注意：只回傳該地點相關資訊，其他地點略過。回傳不超過 600 tokens。
