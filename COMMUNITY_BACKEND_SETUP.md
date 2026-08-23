# LOCAL ATLAS — Community Editing Backend

共同編集UI・API・公開フィードは実装済みです。公開ユーザーはGitHubへ遷移せず、各ページの「＋ 書き足す」から投稿します。

## 最後に必要な1回だけの設定

1. GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token
2. Repository access: **Only select repositories** → `Akiokn0903/nishi-ogikubo`
3. Repository permissions: **Issues: Read and write** のみ付与（Contents等は不要）
4. 発行したtokenをコピー
5. Vercel → Project `nishi-ogikubo` → Settings → Environment Variables
6. Name: `GITHUB_WRITE_TOKEN`
7. Value: 発行したtoken
8. Production / Preview / Development を選択して保存
9. Redeploy

## 仕組み

- ブラウザ: `/community.js` がサイト内モーダルを表示
- POST: `/api/contribute` が入力を検証
- 保存: GitHub Issuesへ `[ATLAS:category/topic]` 形式で保存
- 表示: GitHub Public Issues APIから各ページの投稿だけを読み込み、ページ内に即時表示
- GitHub画面への遷移は不要

## セキュリティ

- tokenはVercel環境変数のみ。HTML/JS/GitHubリポジトリには入れない
- token権限はIssuesのRead/Writeだけに限定
- APIで文字数、URL数、許可済みcategory/topic、honeypotを検証
- 投稿規約とPrivacy Policyを公開済み
