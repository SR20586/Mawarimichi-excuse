# まわりみち・エクスキューズ 🌀

**全宇宙まわりみち機構・時空管理局** が運営する、言い訳証明書 電子申請システムです。

あなたの「遅刻した」「課題が終わらなかった」などの些細な事実を、AIが壮大な宇宙的不可抗力として認定し、重厚な公文書風の「言い訳証明書」を発行します。

## セットアップ

### 1. 依存関係のインストール

```bash
cd mawarimichi-excuse
npm install
```

### 2. 環境変数の設定

`.env.local` ファイルに GLM API キーを設定してください：

```
GLM_API_KEY=your_glm_api_key_here
```

GLM API キーは [Z ai](https://z.ai/subscribe?_channel_track_key=bFOzJZF1&gad_source=1&gad_campaignid=23473939863&gbraid=0AAAABCK8KLx7x48RX9SyeywYho4tEz7JG&gclid=Cj0KCQjwpv7NBhCzARIsADkIfWwj5zV91YDPt5Xw9VSEO1Hft0aXUFhD5MZoH0qTc666T0xCx71WvmUaAh4PEALw_wcB) で取得してください。

### 3. 開発サーバーの起動

```bash
npm run dev
```

[http://localhost:3000](http://localhost:3000) を開いてアプリを使用できます。

## Vercelでデプロイする方法（ローカル設定以外）

### 方法A: Vercelダッシュボードからデプロイ

1. GitHub にこのリポジトリを push する
2. Vercel にログインして「Add New... > Project」を開く
3. 対象リポジトリを Import する
4. Framework Preset は Next.js のままで進める
5. Project Settings > Environment Variables で以下を設定する
	- Name: GLM_API_KEY
	- Value: 発行した API キー
	- Environment: Production（必要に応じて Preview / Development も追加）
6. Deploy を実行する

環境変数を追加・変更した場合は、再デプロイしてください。

### 方法B: Vercel CLI からデプロイ

```bash
npm i -g vercel
vercel login
vercel link
vercel env add GLM_API_KEY production
vercel --prod
```

Preview 環境にも設定する場合は以下を実行します。

```bash
vercel env add GLM_API_KEY preview
```

## 技術スタック

- **フロントエンド**: Next.js 15 (App Router) + TypeScript
- **スタイリング**: カスタムCSS（2000年代初頭の日本の役所風デザイン） + Tailwind CSS
- **画像生成**: html2canvas（証明書をPNG画像としてダウンロード）
- **AI**: GLM API（glm-4.7-flash / OpenAI互換API）

## ディレクトリ構成

```
mawarimichi-excuse/
├── src/
│   ├── app/
│   │   ├── api/
│   │   │   └── generate/
│   │   │       └── route.ts        # GLM API連携エンドポイント
│   │   ├── globals.css             # 役所風グローバルCSS
│   │   ├── layout.tsx              # ルートレイアウト
│   │   └── page.tsx                # メインページ
│   ├── components/
│   │   ├── ApplicationForm.tsx     # 申請フォーム
│   │   ├── CertificatePreview.tsx  # 証明書プレビュー＋画像DL
│   │   └── LoadingOverlay.tsx      # ローディング表示
│   └── types/
│       └── index.ts                # 型定義
├── .env.local                      # 環境変数（要設定）
├── next.config.ts
├── package.json
├── postcss.config.mjs
└── tsconfig.json
```

## 注意事項

※ 本システムで発行される証明書は、3次元空間における法的効力を一切有しません。  
※ ジョークアプリです。実際の遅刻の言い訳に使用しないでください（使用しても当局は責任を負いません）。
