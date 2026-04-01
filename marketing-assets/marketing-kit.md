# Freelancer Business OS — Marketing & Thumbnail Kit

> Gumroad や Etsy、その他プラットフォームで販売するための画像作成ガイドです。
> `bg-aurora-dark.png` と `bg-cyber-glass.png` をFigmaの背景に敷いて使用してください。

## 📐 プラットフォーム別 推奨サイズ

| プラットフォーム | サイズ (Width x Height) | 用途 |
|----------------|-----------------------|------|
| **Gumroad**    | 1280 x 720 px (16:9) | Cover image（最重要） |
| **Gumroad**    | 600 x 600 px (1:1)   | Thumbnail（検索・一覧用） |
| **Etsy**       | 2700 x 2025 px (4:3) | Primary Listing Photo |
| **Notion**     | 1500 x 500 px (3:1)  | Template Cover |

---

## 📸 撮影すべき3つのスクリーンショット

Notionを開いて、以下のスクリーンショット（見栄え良くMacのスクリーンショット機能 `Cmd + Shift + 4` → `Space` でウィンドウ単位で撮影）を用意します。

1. **Dashboard Hero Image（全景）**
   - 上部の Rate Simulator と Revenue Progress、タイマーが入った状態で一番綺麗に見える構図。
2. **Pomodoro Timer 稼働中**
   - 赤（Focus）や緑（Break）のリングが半分ほど進んだ「動いている感」のある状態。
3. **Database Linked Views**
   - Projects（Kanban）とTasks（This Week）が綺麗に並んでいるところ。

---

## 🎨 Figmaでのサムネイル構成案（Main Cover Image用）

Gumroadのカバー画像（1280x720）を作るときの「勝てる」テンプレート構成です。

### レイヤー構造 (下から順に)

1. **背景レイヤー**: `bg-aurora-dark.png` を画面いっぱいに配置（暗めに調節）
2. **スクショレイヤー**: 「Dashboard Hero Image」を中央から少し右にずらして配置。
   - 効果（Effect）から **"Drop Shadow"** を追加（黒, ぼかし: 30%, Y軸: 15）して浮かせる。
   - 少し（2〜3度）だけ左に傾けると、よりダイナミックな印象になります。
3. **テキストレイヤー**: 左側に白・または薄い紫で大きく配置。

### 推奨コピーライティング（英語圏向け）

#### 🔹 The Ultimate Freelance Workspace

- 大見出し（H1）: `Freelancer Business OS`
- 小見出し（H2）: `Your all-in-one Notion workspace to manage clients, track revenue, and focus.`
- アクセント文字（バッジ）: `Includes 3 Custom Interactive Widgets 🔥`

#### 🔹 機能を絞ったアピール（2枚目以降の画像用）

- **画像2**: `Calculate Your Perfect Rate`
  - Simulatorのスクショを拡大。「$85/hr」の部分に丸印など。
- **画像3**: `Interactive Focus Timer included`
  - ポモドーロタイマーのスクショ。
- **画像4**: `7 Connected Databases`
  - Notionのデータベース一覧とリレーション図。

---

## 💎 デザインのコツ（Premium Aesthetic）

- **フォント**: `Inter`（Notionと同じ）, または `Outfit`, `Space Grotesk` のようなモダンなサンセリフ体を使用してください。
- **カラー**: 黄色や赤などの原色は避け、背景のネオンブルーや紫から拾った色（スポイトツールを使用）をアクセントカラーにすると統一感が出ます。
- **Notionアイコンの使用**: 画面の隅にNotionのロゴ（白一色など）を配置し、「Notion Template」であることを明示します。
