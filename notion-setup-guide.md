# Freelancer Business OS — Notion Setup Guide

> このガイドに沿って、Notionで7つのデータベースを順番に構築していきます。  
> 所要時間の目安: 約60〜90分（全Phase）

---

## 🔧 事前準備

1. Notionで新しいページを作成し、タイトルを **「Freelancer Business OS」** にする
2. ページアイコンを 🚀 に設定
3. カバー画像を設定（ダークグラデーション推奨）

---

## Phase 1: 🏷 Categories（カテゴリマスタ）

> **最初に作る理由**: 他のDBから参照される「マスタデータ」なので、先に用意しておく必要があります。

### 手順

1. `/database` → **Database - Full page** を選択
2. タイトルを **「Categories」** に変更
3. アイコンを 🏷 に設定

### プロパティを追加

| プロパティ名 | Type | 設定方法 |
|-------------|------|---------|
| Category Name | Title | （デフォルトのTitle列をリネーム） |
| Type | Select | オプション: `Income`, `Expense` |
| Icon | Text | 各カテゴリの絵文字を入れる欄 |

### 初期データを入力

以下のカテゴリを1行ずつ追加してください:

**Income（収入）:**
| Category Name | Type | Icon |
|--------------|------|------|
| Client Work | Income | 💼 |
| Digital Products | Income | 📦 |
| Consulting | Income | 🎯 |
| Affiliate | Income | 🔗 |
| Other Income | Income | 💰 |

**Expense（経費）:**
| Category Name | Type | Icon |
|--------------|------|------|
| Software & Tools | Expense | 🖥 |
| Hardware | Expense | ⌨️ |
| Marketing | Expense | 📣 |
| Education | Expense | 📚 |
| Co-working | Expense | 🏢 |
| Communication | Expense | 📱 |
| Insurance | Expense | 🛡 |
| Travel | Expense | ✈️ |
| Professional Services | Expense | 👔 |
| Other Expense | Expense | 📋 |

### ビューを作成

1. **Default view** をそのまま **All Categories** にリネーム
2. **Group by** → `Type` を設定（Income / Expense でグループ分け）

✅ **Phase 1 完了！**

---

## Phase 2: 📊 Transactions（入出金トラッカー）

> **最重要DB。** シミュレーターで算出した目標時給と、実際の収支を比較する財務の心臓部です。

### 手順

1. `/database` → **Database - Full page** を選択
2. タイトルを **「Transactions」** に変更
3. アイコンを 📊 に設定

### プロパティを追加

| プロパティ名 | Type | 設定方法 |
|-------------|------|---------|
| Description | Title | （デフォルトのTitle列をリネーム） |
| Type | Select | オプション: `💚 Income`, `🔴 Expense` |
| Amount | Number | Format: `Dollar` に設定 |
| Category | Relation | → **Categories** DB を選択 |
| Date | Date | — |
| Payment Method | Select | `Bank`, `PayPal`, `Stripe`, `Cash`, `Credit Card` |
| Is Recurring | Checkbox | — |
| Tax Deductible | Checkbox | — |
| Receipt | Files & media | — |
| Notes | Text | — |

### ビューを作成

1. **All Transactions** (Table) — Sort: Date (Descending)
2. **+ Add a view** → **Income Only** (Table) — Filter: Type = 💚 Income
3. **+ Add a view** → **Expenses Only** (Table) — Filter: Type = 🔴 Expense
4. **+ Add a view** → **Monthly Overview** (Table) — Group by: Date (Month)
5. **+ Add a view** → **Tax Deductible** (Table) — Filter: Tax Deductible = ✓

### サンプルデータを2〜3件入力

テンプレートの購入者が使い方を理解できるよう、サンプルデータを入れておきましょう:

| Description | Type | Amount | Category | Date |
|------------|------|--------|----------|------|
| Logo Design for Acme Corp | 💚 Income | $2,500 | Client Work | 今日の日付 |
| Figma Annual Plan | 🔴 Expense | $144 | Software & Tools | 今日の日付 |
| Website Development | 💚 Income | $4,000 | Client Work | 先週の日付 |

✅ **Phase 2 完了！**

---

## Phase 3: 🤝 Clients（クライアントCRM）

### 手順

1. `/database` → **Database - Full page** を選択
2. タイトルを **「Clients」** に変更
3. アイコンを 🤝 に設定

### プロパティを追加

| プロパティ名 | Type | 設定方法 |
|-------------|------|---------|
| Client Name | Title | （デフォルトのTitle列をリネーム） |
| Status | Select | `🟢 Active`, `🟡 Lead`, `🔵 Prospect`, `⚪ Past` |
| Contact Name | Text | — |
| Email | Email | — |
| Phone | Phone | — |
| Website | URL | — |
| Industry | Select | `Tech`, `Marketing`, `E-commerce`, `Healthcare`, `Education`, `Other` |
| Source | Select | `Referral`, `Cold Outreach`, `Upwork`, `LinkedIn`, `Website`, `Other` |
| Hourly Rate | Number | Format: `Dollar` |
| Notes | Text | — |
| Created | Created time | — |

### ビューを作成

1. **All Clients** (Table) — Sort: Status, then Name
2. **+ Add a view** → **Pipeline** (Board) — Group by: Status
3. **+ Add a view** → **Top Clients** (Table) — ※ "Total Revenue" Rollupを追加後にSort設定

### サンプルデータ

| Client Name | Status | Contact | Industry | Rate |
|------------|--------|---------|----------|------|
| Acme Corporation | 🟢 Active | John Smith | Tech | $85 |
| StartupXYZ | 🟡 Lead | Jane Doe | E-commerce | — |

✅ **Phase 3 完了！**

---

## Phase 4: 📋 Projects（プロジェクト管理）

### 手順

1. `/database` → **Database - Full page** を選択
2. タイトルを **「Projects」** に変更
3. アイコンを 📋 に設定

### プロパティを追加

| プロパティ名 | Type | 設定方法 |
|-------------|------|---------|
| Project Name | Title | （デフォルトのTitle列をリネーム） |
| Client | Relation | → **Clients** DB を選択 |
| Status | Select | `📝 Proposal`, `🟢 Active`, `⏸ On Hold`, `✅ Completed`, `❌ Cancelled` |
| Priority | Select | `🔴 High`, `🟡 Medium`, `🟢 Low` |
| Type | Select | `Fixed Price`, `Hourly`, `Retainer`, `Pro Bono` |
| Budget | Number | Format: `Dollar` |
| Start Date | Date | — |
| Deadline | Date | — |
| Estimated Hours | Number | — |
| Notes | Text | — |

### 重要: Clients DB側にリレーションを確認

- Projects の `Client` Relationを作成すると、Clients DB 側にも自動で `Projects` リレーションが追加されます
- Clients DB で **Rollup** を追加:
  - プロパティ名: `Active Projects`
  - Relation: Projects
  - Property: Status
  - Calculate: `Count values` → Filter to Active only

### ビューを作成

1. **Kanban** (Board) — Group by: Status
2. **Timeline** (Timeline) — Start Date → Deadline
3. **By Client** (Table) — Group by: Client

### サンプルデータ

| Project | Client | Status | Type | Budget | Start | Deadline |
|---------|--------|--------|------|--------|-------|----------|
| Brand Redesign | Acme Corporation | 🟢 Active | Fixed Price | $5,000 | 今月1日 | 来月末 |

✅ **Phase 4 完了！**

---

## Phase 5: ✅ Tasks（タスク管理）

### 手順

1. `/database` → **Database - Full page** を選択
2. タイトルを **「Tasks」** に変更
3. アイコンを ✅ に設定

### プロパティを追加

| プロパティ名 | Type | 設定方法 |
|-------------|------|---------|
| Task | Title | — |
| Project | Relation | → **Projects** DB を選択 |
| Status | Status | `Not Started`, `In Progress`, `Blocked`, `Done` |
| Priority | Select | `🔴 Urgent`, `🟡 Important`, `🟢 Normal`, `⚪ Low` |
| Due Date | Date | — |
| Hours Logged | Number | — |
| Tags | Multi-select | `Design`, `Development`, `Writing`, `Admin`, `Meeting`, `Review` |
| Notes | Text | — |
| Completed Date | Date | — |

### 重要: Projects DB に Rollup を追加

- Projects DB に Rollup を追加:
  - プロパティ名: `Actual Hours`
  - Relation: Tasks
  - Property: Hours Logged
  - Calculate: `Sum`

### ビューを作成

1. **Board** (Board) — Group by: Status
2. **This Week** (Calendar) — Due Date で表示
3. **My Tasks** (Table) — Sort: Due Date (Ascending)

### サンプルデータ

| Task | Project | Status | Priority | Due | Hours |
|------|---------|--------|----------|-----|-------|
| Create mood board | Brand Redesign | Done | 🟢 Normal | 先週 | 2 |
| Design logo options | Brand Redesign | In Progress | 🟡 Important | 今週 | — |
| Client presentation | Brand Redesign | Not Started | 🔴 Urgent | 来週 | — |

✅ **Phase 5 完了！**

---

## Phase 6: 💰 Invoices（請求書管理）

### 手順

1. `/database` → **Database - Full page** を選択
2. タイトルを **「Invoices」** に変更
3. アイコンを 💰 に設定

### プロパティを追加

| プロパティ名 | Type | 設定方法 |
|-------------|------|---------|
| Invoice # | Title | 例: `INV-2025-001` |
| Client | Relation | → **Clients** DB を選択 |
| Project | Relation | → **Projects** DB を選択 |
| Status | Select | `📝 Draft`, `📤 Sent`, `⏳ Overdue`, `✅ Paid`, `❌ Cancelled` |
| Amount | Number | Format: `Dollar` |
| Tax Amount | Formula | `prop("Amount") * 0.25` |
| Net After Tax | Formula | `prop("Amount") - prop("Tax Amount")` |
| Issue Date | Date | — |
| Due Date | Date | — |
| Paid Date | Date | — |
| Payment Method | Select | `Bank Transfer`, `PayPal`, `Stripe`, `Wise`, `Other` |
| Transactions | Relation | → **Transactions** DB を選択 |
| Notes | Text | — |

### 重要: Clients DB に Revenue Rollup を追加

- Clients DB に Rollup を追加:
  - プロパティ名: `Total Revenue`
  - Relation: Invoices
  - Property: Amount
  - Calculate: `Sum`
- これで **Top Clients** ビューを Total Revenue で降順ソートできるようになります

### ビューを作成

1. **All Invoices** (Table) — Sort: Issue Date (Desc)
2. **Pipeline** (Board) — Group by: Status
3. **Overdue** (Table) — Filter: Status = ⏳ Overdue

### サンプルデータ

| Invoice # | Client | Project | Status | Amount | Issue Date |
|-----------|--------|---------|--------|--------|-----------|
| INV-2025-001 | Acme Corporation | Brand Redesign | ✅ Paid | $2,500 | 先月 |
| INV-2025-002 | Acme Corporation | Brand Redesign | 📤 Sent | $2,500 | 今月 |

✅ **Phase 6 完了！**

---

## Phase 7: 🔄 Subscriptions（サブスク管理）

### 手順

1. `/database` → **Database - Full page** を選択
2. タイトルを **「Subscriptions」** に変更
3. アイコンを 🔄 に設定

### プロパティを追加

| プロパティ名 | Type | 設定方法 |
|-------------|------|---------|
| Service Name | Title | — |
| Status | Select | `🟢 Active`, `⏸ Paused`, `❌ Cancelled` |
| Cost | Number | Format: `Dollar` |
| Billing Cycle | Select | `Monthly`, `Quarterly`, `Annually` |
| Monthly Cost | Formula | 下記参照 |
| Annual Cost | Formula | `prop("Monthly Cost") * 12` |
| Category | Relation | → **Categories** DB を選択 |
| Renewal Date | Date | — |
| URL | URL | — |
| Essential | Checkbox | — |
| Notes | Text | — |

### Monthly Cost の Formula

```
if(prop("Billing Cycle") == "Monthly", prop("Cost"), if(prop("Billing Cycle") == "Quarterly", prop("Cost") / 3, if(prop("Billing Cycle") == "Annually", prop("Cost") / 12, 0)))
```

### ビューを作成

1. **Active** (Table) — Filter: Status = 🟢 Active, Sort: Monthly Cost (Desc)
2. **By Category** (Table) — Group by: Category

### サンプルデータ

| Service | Status | Cost | Cycle | Category | Essential |
|---------|--------|------|-------|----------|-----------|
| Notion | 🟢 Active | $96 | Annually | Software & Tools | ✓ |
| Figma | 🟢 Active | $144 | Annually | Software & Tools | ✓ |
| Zoom | 🟢 Active | $13.99 | Monthly | Communication | ✓ |
| Canva Pro | 🟢 Active | $120 | Annually | Software & Tools | |

✅ **Phase 7 完了！**

---

## Final: 🏠 Dashboard（ダッシュボードページ）

> 全DBを1つのページに集約する「テンプレートの顔」を作ります。

### 手順

1. 最初に作った **「Freelancer Business OS」** ページを開く
2. 以下の構成でコンテンツを配置:

```
📌 レイアウト構成:

[Header Section]
  🚀 Welcome to your Freelancer Business OS
  "Everything you need to run your freelance business."

[2-Column: Widgets]
  左: 💰 Rate Simulator (embed)
  右: 📈 Revenue Progress (embed)

[Full Width: Timer]
  🍅 Pomodoro Timer (embed)

[2-Column: Quick Views]
  左: 📋 Projects → Linked view (Kanban, filter: Active)
  右: ✅ Tasks → Linked view (Board, filter: This Week)

[2-Column: Financial]
  左: 💰 Invoices → Linked view (Pipeline Board)
  右: 📊 Transactions → Linked view (Monthly Overview)

[Full Width: Management]
  🤝 Clients → Linked view (Pipeline Board)

[2-Column: Bottom]
  左: 🔄 Subscriptions → Linked view (Active only)
  右: 🏷 Categories → Linked view (Grouped by Type)
```

### Linked view の作り方

各DBのビューをダッシュボードに表示するには:
1. `/linked` と入力
2. **Linked view of database** を選択
3. 対象のDBを選択
4. 表示したいビューを選択

### 仕上げのコツ

- **Callout ブロック** を使ってセクションヘッダーを作る（例: `💰 Financial Overview`）
- **Divider** でセクション間を区切る
- **2カラムレイアウト** は文章を書いてからドラッグで並べる
- 各Linked viewは **高さを制限** して見やすくする

✅ **全Phase完了！テンプレートが完成しました！🎉**

---

## 📝 完成後のチェックリスト

- [ ] 全7つのDBにサンプルデータが入っている
- [ ] 全DBのリレーションが正しく機能している
- [ ] Rollup（Total Revenue, Actual Hours等）が正しく集計されている
- [ ] 3つのウィジェットが正しく埋め込まれている
- [ ] ダッシュボードのLinked viewが正しく表示される
- [ ] テンプレートを「Duplicate」して動作確認
