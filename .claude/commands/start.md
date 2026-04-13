# /start — 開始遊戲

開始新遊戲或從存檔繼續。

## 執行流程

### 1. 檢查存檔
委託 game-engine 讀取 game-state.json。

**若存檔存在**：
- 讀取玩家名稱、位置、狀態
- 以沉浸式語氣描述：「你的意識逐漸清晰。你在 [location]。」
- 簡短描述當前場景，提供行動選項
- 結束

**若存檔不存在**：進入新遊戲流程 ↓

### 2. 新遊戲：Eta 迎接

描述玩家乘坐小船抵達 Shiso Tree（紫蘇之樹）。
Eta（中性、親切、制式的遊戲嚮導）迎接玩家：

「歡迎來到貪婪之島。我是 Eta，負責說明遊戲規則。」

Eta 簡要說明：
- 這座島上有 100 張限定槽卡，蒐集全部即可通關
- 說出「Book」可召喚咒語書查看卡牌
- 擊敗敵人或完成任務後，說出「Gain」可將物品轉為卡牌
- 咒語卡可在 Masadora 購買
- 死亡是永久的——這座島是真實的

詢問玩家名字。

### 3. 水見式（念系判定）

Eta 帶領玩家到一杯水前：
「接下來是水見式。請將雙手放在杯子兩側，集中精神。
 在此之前，我需要了解你一些事情。」

**依序提出 5-7 個問題**（每次一個，等待回答）：

1. 「面對一個比你強大得多的敵人，你的第一反應是？」
   → 正面迎擊 = 強化系傾向 / 迂迴策略 = 操作系傾向

2. 「你更在意事情的結果，還是過程？」
   → 結果 = 放出系傾向 / 過程 = 具現化系傾向

3. 「朋友背叛了你。你會？」
   → 原諒 = 強化系 / 報復 = 變化系 / 分析原因 = 操作系 / 無法釋懷 = 具現化系

4. 「描述你理想中的一天。」
   → 冒險行動 = 強化/放出 / 創作體驗 = 變化 / 安靜思考 = 具現化/操作

5. 「你最無法忍受的是什麼？」
   → 不公正 = 強化 / 無聊 = 變化 / 低效率 = 放出 / 失控 = 操作 / 不完美 = 具現化

6. 「如果可以擁有一種超能力？」
   → 力量 = 強化 / 變形 = 變化 / 遠距離攻擊 = 放出 / 控制 = 操作 / 創造 = 具現化

7. （可選）「你做決定時，更依賴直覺還是邏輯？」
   → 直覺 = 強化/變化 / 邏輯 = 操作/具現化 / 都不是 = 特質系

**判定規則**：統計各系傾向次數，最高者為玩家念系。
若出現平手或答案非常特殊/矛盾 → 特質系。

**描述水見式現象**：
- 強化系：水量明顯增加，水溢出杯緣
- 變化系：水的顏色緩緩改變（根據個性決定顏色）
- 放出系：杯子突然移動，水面劇烈搖晃
- 操作系：水中出現一個微小的生物在游動
- 具現化系：水中析出細微的結晶或雜質
- 特質系：發生無法歸類的異象（根據玩家個性創造獨特現象）

Eta 宣布結果並解釋該念系的特點。

**應用初始加成**：
- 強化系：physique +3, endurance +2
- 變化系：hatsu_power +8
- 放出系：output +10, speed +2
- 操作系：perception +5
- 具現化系：stability +8
- 特質系：全屬性 +1

### 4. 必殺技（發）設計

Eta：「最後一步。你的念已經覺醒，現在需要塑造你的『發』——你獨有的念能力。」

**依序提出 3 個問題**：

1. 「你最想保護的東西是什麼？」
2. 「你願意為此付出什麼代價？」
3. 「用一句話描述你理想中的戰鬥方式。」

**根據回答和念系生成必殺技**：
- name：反映玩家性格或誓約精神的名稱
- description：具體效果描述
- limitation：誓約內容（越嚴苛效果越強）
- limitation_tier：0（無誓約）到 4（極限），根據第 2 題的犧牲程度決定
- base_coefficient：2.0（無誓約）到 3.0（極限誓約）
- aura_cost：根據效果強度決定（20-50）
- range：close / mid / far，根據念系和第 3 題決定
- trigger_condition：特殊觸發條件（可為空）

向玩家展示設計出的必殺技，描述第一次發動時的感覺。

### 5. 建立存檔

委託 game-engine 建立 game-state.json，初始值：
- player.name = 玩家輸入的名字
- jenny = 100,000
- physical: hp=100, hp_max=100, stamina=100, stamina_max=100, physique=10, speed=10, endurance=10, perception=10（加上念系加成）
- nen: type=判定結果, level=5, aura=200, aura_max=200, output=20, stability=10, recovery=5, hatsu_power=15（加上念系加成）
- techniques: ten=true, zetsu=true, 其餘 false
- ryu: tier=0, current_ratio={attack:50, defense:50}, local_focus_unlocked=false
- ability: 根據設計填入
- location = "Shiso Tree"
- party = []
- cards: specified_slots={}, free_slots=[], specified_count=0
- faction: current="solo", reputation 全 0, victory_condition="standard_clear"
- npc_relationships: 全部初始值
- story.flags: 全部 false（battera_contract_active=true, battera_lover_alive=true）
- story.world_state: days_elapsed=1, current_month_day=11, action_count=0, genthru_cards_held=0, active_players_count=200
- history_wall: 全部 natural, pressure_level=0
- memory_card: clear_count=0（若是多周目，保留上一周目的 memory_card）

### 6. 開場

描述 Shiso Tree 的場景：巨大的紫蘇樹，遠處可見通往各方的道路。

提供初始選項：
[1] 前往 Rubicuta（最近的小鎮）
[2] 直接前往 Masadora（魔法之城，可購買咒語卡）
[3] 探索 Shiso Tree 周圍
[4] 詢問 Eta 更多資訊
