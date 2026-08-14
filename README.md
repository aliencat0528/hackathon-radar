# hackathon-radar — 黑客松賽事追蹤與報名通知

在報名開放時通知你，並附上判斷「要不要投」所需的三段資訊。

![Version](https://img.shields.io/badge/version-0.1.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

## 功能特色

- **報名窗口觸發**——只在報名開放／截止逼近時通知，不做固定週報（← `HR-003`）
- **三段式訊息**——今年比賽主旨 + 去年得獎作品（含功能描述）+ 今年趨勢變化，湊不齊就明說（← `HR-002`）
- **來源分級**——每個日期都帶 `source_tier`，**推估日期不得觸發通知**（← `HR-004`）
- **雙通道**——email 先行驗證格式，主力目標為 LINE（← `HR-001`）

## 快速開始

> 📌 目前為 v0.1.0：**只有文件與資料契約，尚無實作程式碼**（← `HR-005`）。
> 本節在寫入抓取與寄送邏輯後補齊。

```bash
# 檢視目前的追蹤清單
cat data/events.yaml
# 預期：以 events: 為根的 YAML，每筆含 name / status / dates / source_tier
```

## 使用方式

### 追蹤清單

`data/events.yaml` 是唯一的事實來源。新增一場賽事時，最少要填 `name`、`eligibility`、
`dates.registration`，且每個日期都要標 `source_tier`。

### 通知訊息

模板與三段式的填寫規則見 `docs/NOTIFICATION.md`。
無法湊齊三段時，訊息會降級為「僅日期提醒」並在信中列出缺哪一段——
**不允許靜默省略**。

## 專案結構

```
hackathon-radar/
├── CLAUDE.md              # 規範差異（scopes、來源分級、訊息硬規則）
├── prepare.md             # 決策記錄 HR-001 ~ HR-005
├── README.md
├── data/
│   └── events.yaml        # 追蹤清單（唯一事實來源）
└── docs/
    └── NOTIFICATION.md    # 通知訊息模板與三段式規則
```

## 測試

> 📌 尚無自動化測試。目前的驗證方式是**人工寄出樣本信確認可讀性**（← `HR-005`）。

```bash
# 資料契約格式檢查（待實作）
```

## 開發階段 / 里程碑

| 階段 | 內容 | 狀態 |
|------|------|------|
| M1 | 資料契約 + 通知模板 + 樣本信驗證格式 | 進行中 |
| M2 | 來源抓取（官網 / Devpost 藝廊），產生 `events.yaml` | 未開始 |
| M3 | 排程與觸發判斷（含 `inferred` 不觸發的守門） | 未開始 |
| M4 | LINE Messaging API 接通，email 降為備援 | 未開始 |

## 版本歷史

### v0.1.0 (2026-08-14)

- **立項** — 資料契約、通知三段式規則、來源四級分類；不含實作程式碼

## 授權

MIT License

---

## 相關文件

- 通知訊息模板 → `docs/NOTIFICATION.md`
- 決策記錄 → `prepare.md`
- README 更新觸發條件、版本規則、CHANGELOG 格式 → `../.claude/specs/docs.md`
