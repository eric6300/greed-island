# /go [地點] — 前往指定地點

移動到島上的另一個地點。

## 執行流程

1. 委託 game-engine 讀取 game-state.json（location, player stats, story.world_state）
2. 使用 /location-info 確認目的地是否存在且可從當前位置到達

3. **驗證**：
   - 目的地不存在 →「這個地方似乎不存在。」
   - 不相鄰 → 計算需經過的路徑，描述長途旅程
   - Limeiro 且 specified_count < 99 →「Limeiro 的大門紋絲不動。你還沒有資格進入。」
   - 特殊事件模式中 →「你現在無法離開。[事件名稱] 正在進行中。」

4. **移動處理**：
   - 相鄰地點：描述短途旅程。20% 機率遇到隨機怪物（使用 /combat-rules 處理）
   - 遠距離（2+ 步）：描述較長旅程，days_elapsed +1，40% 機率遭遇

5. **抵達後**：
   - 更新 location 為目的地
   - 更新 action_count +1（每 5 次 = +1 天）
   - 長途移動額外 days_elapsed +1
   - 簡短描述抵達場景
   - 列出可見 NPC 和可用設施

6. **遭遇處理**：
   - 若觸發遭遇：先描述遭遇場景，進入戰鬥
   - 戰鬥結束後才描述抵達目的地

7. 委託 game-engine 更新 game-state.json
