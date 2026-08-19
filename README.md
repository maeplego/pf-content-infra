# pf-content-infra

P08 の単体連携 Compose です。ブログ（`pf-content-blog`）と短縮（`pf-content-shortener`）を同じ Postgres / Redis 上で起動します。**overlay E と Kubernetes は未着手。**

学習用です。公開デモの短縮先は `localhost` / `127.0.0.1` だけです。

## デモ

リポジトリはワークスペースの兄弟ディレクトリです。このフォルダから:

```powershell
cd deploy
copy .env.example .env
docker compose up -d --build
```

| URL | 用途 |
| --- | --- |
| http://localhost:3007 | 公開ブログ |
| http://localhost:3007/demo | Markdown + 下書き/公開 + 短縮の手順 |
| http://localhost:3007/admin | Dev login → 下書きプレビュー → Publish |
| http://localhost:8094/health | 短縮 liveness |
| http://localhost:8094/ready | 短縮 readiness |

停止: `docker compose down`。

シード記事は架空の Harbor Press。実在の個人情報は使いません。画像はブログの `/harbor.svg`（P03 任意・未接続）。

## 既知の制限

- 開発認証のみ（`X-Dev-User-Sub` / 管理 cookie）
- レート制限、日次グラフ UI、OIDC、overlay E なし
