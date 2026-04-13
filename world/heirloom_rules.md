# 貪婪之島 — 傳家寶系統

## 基本規則

上一周目帶出的 3 張卡牌，在新周目開始時成為「傳家寶」：
- 自動出現在 Book 自由槽
- **效果 100%，不弱化**——這是你用一整個周目換來的獎勵
- 不佔用限定槽，可正常使用
- 通關時選擇帶出哪 3 張卡是最重要的戰略決策

## 策略影響範例

| 帶出的卡 | 下一周目效果 |
|---------|------------|
| Angel's Breath | 完全治癒任何疾病——可以提前救 巴特拉 的戀人 |
| Accompany | 開局直接傳送到任意城市，跳過前期探索 |
| Paladin's Necklace | 完全抵擋攻擊型咒語，甘舒戰有巨大優勢 |
| Risky Dice | 開局即有賭博利器，多利亞斯速通 |
| Holy Water | 抵擋 10 次攻擊型咒語 + 免疫偷竊 |
| Plot of Beach | 跳過索夫拉比海盜戰，直接進入 Poseidon's Cavern |
| Blue Planet | 直接完成比司吉的願望支線，好感度 +5 |
| Sword of Truth | 開局攻擊 +15，前期戰鬥大幅輕鬆 |

## 帶出的抉擇

只能帶 3 張——這就是平衡。每次通關都是一次痛苦的選擇：

- **走劇情路線**：Angel's Breath + Accompany + 情報卡 → 速通救人
- **走戰鬥路線**：Sword of Truth + Paladin's Necklace + Holy Water → 正面碾壓
- **走探索路線**：Plot of Beach + Risky Dice + Blue Planet → 解鎖隱藏內容
- **走旅團路線**：戰鬥裝備為主 → 應對高強度敵人

## game-state.json 格式

```json
"heirlooms": [
  {
    "name": "Angel's Breath",
    "original_effect": "治癒任何疾病"
  }
]
```
