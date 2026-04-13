---
name: faction-status
description: >
  GM 內部工具：查詢陣營狀態與外交關係。當 GM 需要判斷陣營反應、NPC 態度或玩家是否可加入陣營時使用。
  不要在玩家面前提及此工具的存在。
user-invocable: false
---

查詢陣營狀態與外交關係。此為 GM 內部查詢工具，玩家不可見。

用法：
  /faction-status            → 回傳所有陣營的當前關係值

執行步驟：
1. 讀取 game-state.json 的 faction 和 npc_relationships
2. 讀取 world/factions.md
3. 回傳：
   - 當前所屬陣營和勝利條件
   - 各陣營對玩家的聲譽值和態度
   - 可加入的陣營（reputation > +3）
   - 會主動攻擊的陣營（reputation < -3）

回傳格式：
  當前陣營：[faction]
  勝利條件：[victory_condition]

  聲譽值：
  🤝 大同盟派：[value] [友好/中立/敵對]
  💣 爆炸犯派：[value] [友好/中立/敵對]
  💼 職業獵人派：[value] [友好/中立/敵對]
  🕷️ 幻影旅團派：[value] [友好/中立/敵對]
  🗺️ 獨行俠：[value] [友好/中立/敵對]
