# 貪婪之島 — 傳家寶系統

## 基本規則

上一周目帶出的 3 張卡牌，在新周目開始時成為「傳家寶」：
- 自動出現在 Book 自由槽
- 效果降為原版 60%（從遊戲世界帶出後念力減弱）
- 不佔用限定槽，可正常使用
- 同一張卡連續兩個周目都帶出 → 效果恢復 100%

## 策略影響範例

| 帶出的卡 | 下一周目效果 |
|---------|------------|
| Angel's Breath | 微弱治癒能力（60% = 恢復 60% HP 而非全部）|
| Accompany | 開局可直接傳送到任意城市（一次）|
| Paladin's Necklace | 對甘舒炸彈有部分抵抗力（60% 防禦）|
| Risky Dice | 保留，可繼續使用（骰子效果不受效率影響）|
| Holy Water | 抵擋 6 次攻擊型咒語（60% of 10）|
| Plot of Beach | 通往 Poseidon's Cavern（60% 獎品品質）|
| Blue Planet | 收藏價值，可直接完成比司吉的願望支線 |
| Sword of Truth | 攻擊 +9（60% of +15）|

## 連續帶出規則

```
第 1 次帶出：current_efficiency = 0.6
第 2 次帶出（連續）：current_efficiency = 1.0
中斷後重新帶出：current_efficiency = 0.6（重新計算）
```

## game-state.json 格式

```json
"heirlooms": [
  {
    "name": "Angel's Breath",
    "original_effect": "完全恢復 HP",
    "current_efficiency": 0.6,
    "consecutive_runs": 1
  }
]
```
