# キャリアコーチLP

AIキャリアコーチ（ワーママ向け）のランディングページです。

## Vercelでデプロイする手順

1. **GitHubにリポジトリを作成**
   - GitHubで新規リポジトリ（例: `career-coach-lp`）を作成する

2. **リモートを追加してプッシュ**
   ```bash
   cd キャリアコーチLP
   git remote add origin https://github.com/あなたのユーザー名/リポジトリ名.git
   git branch -M main
   git push -u origin main
   ```

3. **Vercelでプロジェクトをインポート**
   - [Vercel](https://vercel.com) にログイン
   - 「Add New」→「Project」
   - 上記のGitHubリポジトリを選択
   - **Root Directory**: そのまま（リポジトリルートに index.html があるため）
   - 「Deploy」をクリック

4. デプロイ後、表示されるURLでLPを確認できます。

## 構成

- `index.html` … トップページ（Vercelのルートで表示）
- `mama_index.html` … 同上のコピー
- `image/` … 画像一式
