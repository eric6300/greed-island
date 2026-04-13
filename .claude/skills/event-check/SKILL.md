---
name: event-check
description: >
  GM 內部工具：檢查當前遊戲狀態下應觸發哪些劇情事件。GM 每 10 個行動自動呼叫一次，
  或在 story.flags 變動時主動呼叫。不要在玩家面前提及此工具的存在。
user-invocable: false
---

檢查當前遊戲狀態下應該觸發哪些事件。此為 GM 內部查詢工具，玩家不可見。

用法：
  /event-check               → 分析 story.flags 和 world_state，回傳應觸發的事件

執行步驟：
1. 讀取 game-state.json 的以下欄位：
   - story.flags（劇情旗標）
   - story.world_state（天數、行動數、活躍玩家數）
   - history_wall（歷史之壁各節點狀態）
   - player.nen.level（念等級）
   - cards.specified_count（限定卡數量）
   - player.location（當前位置）
2. 讀取 world/story_events.md
3. 讀取 world/history_wall.md
4. 對照條件，列出：
   - 應立即觸發的事件（所有條件已滿足）
   - 接近觸發門檻的事件（差 1-2 個條件）
   - 歷史之壁壓力狀況（各節點的 pressure_level 和 status）
   - 固定時間事件提醒（月賽、Hunter Exam 等）

回傳格式：
  🔴 立即觸發：[事件名稱] — [觸發原因]
  🟡 接近觸發：[事件名稱] — [還差什麼條件]
  ⚫ 歷史之壁：[節點名稱] — 壓力 [level]/4，狀態 [status]
  📅 時間事件：[事件] — 距離 [N] 天

若所有事件均未達觸發條件且無接近門檻的事件，回傳：「目前無事件需要觸發。」
