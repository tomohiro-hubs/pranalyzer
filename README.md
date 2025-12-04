# PR Analyzer

太陽光発電所のPR（Performance Ratio）を可視化するクライアントサイド静的Webアプリケーションです。
日次発電量CSVをアップロードするだけで、発電所全体およびPCSごとのPRを計算・可視化します。

## 機能

*   **CSVインポート**: クライアントサイドでCSVを解析（サーバーへのデータ送信なし）
*   **自動計算**:
    *   発電所全体のPR（Performance Ratio）
    *   PCSごとのPR
*   **可視化**:
    *   **サマリー**: 期間、平均PR、最大/最小PR日
    *   **日次PR一覧**: テーブル形式での詳細表示（ソート可能）
    *   **PCS別ヒートマップ**: 日付 x PCS ID のマトリクスでPR分布を色分け表示
*   **エクスポート**: 計算結果（PR値）を付与したCSVデータのダウンロード
*   **完全静的動作**: GitHub Pagesなどで動作可能

## 技術スタック

*   **Framework**: React + Vite + TypeScript
*   **Styling**: Tailwind CSS
*   **Routing**: React Router (HashRouter)
*   **Icons**: Lucide React
*   **CSV Parser**: PapaParse

## プロジェクト構成

```
src/
├── components/     # UIコンポーネント (Header, Tabs, Visualization Widgets)
├── pages/          # ページコンポーネント (About)
├── utils/          # ロジック (CSV Parser, PR計算)
├── types.ts        # TypeScript型定義
├── App.tsx         # メインアプリケーションロジック
└── main.tsx        # エントリーポイント
public/
└── data.json       # 発電所・PCSメタデータ設定ファイル
```

## 開発・実行方法

### 1. インストール

```bash
npm install
```

### 2. ローカルサーバー起動

```bash
npm run dev
```

### 3. ビルド

```bash
npm run build
```

## 設定 (public/data.json)

発電所やPCSの定格容量（DC）は `public/data.json` で定義されています。
運用環境に合わせてこのファイルを修正してください。

```json
{
  "plant": {
    "id": "plant-1",
    "name": "My Solar Plant",
    "defaultPdcKw": 1000.0
  },
  "pcsList": [
    { "id": "1-1-1", "name": "PCS 1", "ratedDcKw": 50.0 },
    ...
  ]
}
```

## CSVフォーマット仕様

以下のヘッダを持つCSVファイルが必要です。

*   `date`: YYYY-MM-DD
*   `irradiation_h`: 日射量 (kWh/m² etc)
*   `plant_pdc_kw`: 発電所DC定格 (kW) ※1行目の値が使用されます
*   `pcs_{ID}_kwh`: 各PCSの発電量 (kWh)

## ライセンス

MIT
