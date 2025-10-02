# WebAuthn Passkey Auto-Creation Demo

Safari 18のAutomatic Passkey Upgradesとconditional mediationを使用したパスキー自動作成のデモサイトです。

## 🚀 デモサイト

GitHub Pagesでデプロイされたデモサイト: https://[YOUR_USERNAME].github.io/[REPOSITORY_NAME]/

## 📋 機能

- **ログインページ** (`index.html`)
  - シンプルなログインフォーム
  - フォーム送信でダッシュボードに遷移

- **ダッシュボードページ** (`dashboard.html`) 
  - ページ読み込み時に自動でパスキー作成を試行
  - Conditional mediation (`mediation: "conditional"`) を使用
  - 詳細なデバッグ情報表示
  - 自動作成失敗時の手動作成機能

## 🛠️ 技術仕様

### WebAuthn実装
- **Conditional Mediation**: `navigator.credentials.create()` with `mediation: "conditional"`
- **Platform Authenticator**: タッチID/FaceID等のプラットフォーム認証器を使用
- **Resident Key**: パスワードレス認証に対応

### セキュリティ
- **HTTPS必須**: WebAuthnはHTTPS環境でのみ動作
- **CSP設定**: Content Security Policyでセキュリティを強化
- **Same-Origin Policy**: クロスオリジンリクエストを制限

## 🌐 GitHub Pagesデプロイ手順

### 1. リポジトリ設定
```bash
git clone [YOUR_REPOSITORY_URL]
cd [REPOSITORY_NAME]
```

### 2. GitHub Pages有効化
1. GitHubリポジトリの「Settings」タブを開く
2. 左メニューから「Pages」を選択
3. Source: 「GitHub Actions」を選択

### 3. 自動デプロイ
- `main`ブランチにpushすると自動でデプロイされます
- `.github/workflows/pages.yml`でCI/CD設定済み

### 4. HTTPS設定確認
- GitHub Pagesは自動でHTTPS化されます
- カスタムドメインを使用する場合はHTTPS設定を確認してください

## 🧪 テスト環境

### 対応ブラウザ
- ✅ Safari 18+ (macOS/iOS) - Automatic Passkey Upgrades対応
- ✅ Chrome/Edge (デスクトップ) - WebAuthn Level 3対応
- ⚠️ Firefox - 一部制限あり

### 推奨テスト手順
1. Safari 18以降でデモサイトにアクセス
2. Apple Password Managerに既存の認証情報が保存されていることを確認
3. ログインページでApple Password Managerを使用してログイン
4. ダッシュボードでパスキーの自動作成を確認

## 📁 ファイル構成

```
├── .github/
│   └── workflows/
│       └── pages.yml          # GitHub Actions設定
├── .nojekyll                  # Jekyll無効化
├── index.html                 # ログインページ
├── dashboard.html             # メインページ（パスキー作成）
└── README.md                  # このファイル
```

## 🔧 ローカル開発

HTTPSが必要なため、ローカルでは以下の方法でテストしてください：

### 方法1: GitHub Codespaces
```bash
# Codespacesで自動的にHTTPS環境が提供されます
```

### 方法2: ローカルHTTPSサーバー
```bash
# mkcertでローカル証明書作成
brew install mkcert
mkcert -install
mkcert localhost 127.0.0.1

# HTTPSサーバー起動
python3 -m http.server 8000 --bind 127.0.0.1
# または
npx serve -s . --ssl-cert localhost.pem --ssl-key localhost-key.pem
```

## 🐛 トラブルシューティング

### パスキー作成が失敗する場合
1. **HTTPS確認**: `https://`でアクセスしているか確認
2. **ブラウザサポート**: Safari 18+またはChrome/Edge最新版を使用
3. **Apple Password Manager**: 既存の認証情報が保存されているか確認
4. **デバッグログ**: ダッシュボードのデバッグ情報を確認

### GitHub Pagesデプロイ失敗
1. **Actions権限**: リポジトリ設定でActions権限を確認
2. **Pages設定**: Source設定が「GitHub Actions」になっているか確認
3. **ワークフローログ**: Actionsタブでエラーログを確認

## 📚 参考資料

- [Safari 18のPasskey Upgrades](https://zenn.dev/gebo/articles/webauthn-safari18-passkey-upgrades)
- [WebAuthn Level 3仕様](https://www.w3.org/TR/webauthn-3/)
- [Credential Management API](https://www.w3.org/TR/credential-management-1/)
- [GitHub Pages Documentation](https://docs.github.com/ja/pages)

## 📄 ライセンス

MIT License