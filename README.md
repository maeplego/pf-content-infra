# pf-content-infra

技術ブログと URL 短縮を、同じ Postgres / Redis で起動する Compose です。学習用です。公開デモの短縮先は `localhost` と `127.0.0.1` だけです。

製品コードは [pf-content-blog](https://github.com/maeplego/pf-content-blog) と [pf-content-shortener](https://github.com/maeplego/pf-content-shortener) にあります。このリポジトリは束ね役です。兄弟ディレクトリとして clone してください。

## 起動

```powershell
cd deploy
copy .env.example .env
docker compose up -d --build
```

| URL | 用途 |
| --- | --- |
| http://localhost:3007 | 公開ブログ |
| http://localhost:3007/demo | Markdown、下書き/公開、短縮の手順 |
| http://localhost:3007/admin | 開発ログイン → プレビュー → 公開 |
| http://localhost:8094/health | 短縮 |

停止は `docker compose down` です。シード記事は架空です。認証は開発用だけです。

P03 で cover をアップロードする場合は [pf-media](https://github.com/maeplego/pf-media) をホストで起動し、次で `MEDIA_API_URL` を渡します。

```powershell
docker compose -f compose.yaml -f compose.media.yaml up -d --build
```

| URL | 用途 |
| --- | --- |
| http://localhost:3007/admin | 管理画面（`MEDIA_API_URL` 設定時 cover アップロード可） |

Compose 起動後のヘルス:

```powershell
node scripts/compose-smoke.mjs http://localhost:3007/api/health http://localhost:8094/health http://localhost:8094/ready
```

Kubernetes 連携は [pf-cloud-k8s](https://github.com/maeplego/pf-cloud-k8s) の content overlay です。
