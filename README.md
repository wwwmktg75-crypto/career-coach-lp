# キャリアコーチLP

AIキャリアコーチ（ワーママ向け）のランディングページです。

---

## Repository のやり方（GitHubに上げる手順）

### 1. GitHubでリポジトリを新規作成

1. [GitHub](https://github.com) にログインする  
2. 右上の **「+」** → **「New repository」** をクリック  
3. 次のように入力する  
   - **Repository name**: 例）`career-coach-lp`（好きな名前でOK）  
   - **Description**: 任意（例：キャリアコーチLP）  
   - **Public** を選択  
   - **「Add a README file」はチェックしない**（すでにローカルにあるため）  
4. **「Create repository」** をクリック  

### 2. 作成したリポジトリのURLをコピー

- 表示されたページの **「Code」** ボタン → **HTTPS** のURLをコピー  
- 例：`https://github.com/あなたのユーザー名/career-coach-lp.git`

### 3. ターミナルでプッシュする

```bash
# キャリアコーチLPフォルダに移動
cd /Users/akiko/Desktop/claudecode/キャリアコーチLP

# リモートを追加（URLは自分のリポジトリに書き換え）
git remote add origin https://github.com/あなたのユーザー名/career-coach-lp.git

# メインブランチを main にそろえる（すでに main の場合は不要）
git branch -M main

# プッシュ
git push -u origin main
```

- 初回の `git push` で GitHub のログインを求められたら、ブラウザまたはトークンで認証する  
- 完了すると、GitHub のリポジトリページにファイルが表示される  

### 4. 今後、変更を反映するとき

```bash
cd /Users/akiko/Desktop/claudecode/キャリアコーチLP
git add .
git commit -m "変更内容のメッセージ"
git push
```

---

## Vercelでデプロイする手順（詳しく）

### 前提

- GitHub にリポジトリを作成し、`git push` まで完了していること。

---

### ステップ1: Vercelにログイン

1. ブラウザで **https://vercel.com** を開く  
2. 右上の **「Log In」** をクリック  
3. **「Continue with GitHub」** を選ぶ  
4. GitHub の認証画面で **「Authorize Vercel」** をクリック  
5. 初回だけ「Vercel がリポジトリにアクセスする権限」を聞かれたら、**必要なリポジトリだけ** または **All repositories** を選んで **「Save」**

---

### ステップ2: プロジェクトを新規作成（Import）

1. Vercel のダッシュボード（トップページ）で、**「Add New…」** をクリック  
2. メニューから **「Project」** を選ぶ  
3. **「Import Git Repository」** の一覧に、GitHub のリポジトリが表示される  
   - 出てこない場合: **「Adjust GitHub App Permissions」** をクリックし、該当リポジトリへのアクセスを許可する  
4. **career-coach-lp**（または付けたリポジトリ名）の右側の **「Import」** をクリック  

---

### ステップ3: 設定画面で確認・変更

次の画面（**Configure Project**）で、以下を確認する。

| 項目 | 設定する値 | 説明 |
|------|------------|------|
| **Project Name** | そのまま or 好きな名前 | そのままでOK（例: career-coach-lp） |
| **Framework Preset** | **Other** を選ぶ | 重要。Next.js などにしないこと |
| **Root Directory** | 変更しない（空のまま） | リポジトリのルートがプロジェクトのルートになる |
| **Build and Output Settings** | 下記のとおり | 静的サイトなのでビルド不要 |

**Build and Output Settings の詳細:**

- **Build Command**  
  - 何も入力しない（空欄のまま）  
  - または **「Override」** にチェックを入れて、入力欄を空にする  

- **Output Directory**  
  - 何も入力しない（空欄のまま）  
  - ルートの `index.html` をそのまま配信するため  

- **Install Command**  
  - そのままでOK（空欄でよい）  

5. 設定を確認したら、画面下の **「Deploy」** をクリック  

---

### ステップ4: デプロイ完了を待つ

1. **「Building」** のログが流れる（数十秒〜1分程度）  
2. **「Congratulations!」** と表示されたら成功  
3. **「Visit」** ボタンをクリックすると、LP の公開URLが開く  
4. このURL（例: `https://career-coach-lp-xxxx.vercel.app`）が本番のアドレス  

---

### 「No Production Deployment」と表示されるとき

デプロイが失敗したり、まだ1回も本番デプロイができていないときに表示されます。次を順に試す。

#### 対処A: ビルド設定を直す

1. Vercel のダッシュボードで、該当 **プロジェクト** をクリック  
2. 上部タブの **「Settings」** をクリック  
3. 左メニューの **「General」** を開く  
4. 下にスクロールして **「Build & Development Settings」** を探す  
5. **「Override」** にチェックを入れる  
6. 次のようにする  
   - **Framework Preset**: **Other**  
   - **Build Command**: 空欄（削除する）  
   - **Output Directory**: 空欄  
   - **Install Command**: 空欄でOK  
7. **「Save」** をクリック  
8. 上部タブの **「Deployments」** に移動  
9. 一番上のデプロイの右側 **「⋯」**（3点メニュー）→ **「Redeploy」** をクリック  
10. **「Redeploy」** を再度クリックして実行  

#### 対処B: vercel.json を入れてから再デプロイ

リポジトリに `vercel.json` があるか確認する（すでに追加済みならそのまま）。

```json
{
  "outputDirectory": "."
}
```

- まだない場合は、プロジェクトのルートに上記の `vercel.json` を追加してコミット・プッシュする  
- その後、Vercel の **Deployments** で **「Redeploy」** する（または GitHub への push で自動的に再デプロイされる）  

#### 対処C: プロジェクトをいったん削除してやり直す

1. **Settings** → 一番下の **「Delete Project」** でプロジェクトを削除  
2. ダッシュボードの **「Add New…」** → **「Project」** で、同じリポジトリを再度 **Import**  
3. **Configure Project** で **Framework Preset: Other**、**Build Command: 空** にして **Deploy**  

---

### デプロイ後の更新のしかた

LP の内容を変えたあと、GitHub に push すると Vercel が自動で再デプロイします。

```bash
cd /Users/akiko/Desktop/claudecode/キャリアコーチLP
git add .
git commit -m "更新内容のメモ"
git push
```

- 数分以内に Vercel の **Deployments** に新しいデプロイが並び、完了すると本番URLの内容が更新されます。  
- 手動でやりたい場合は **Deployments** → 最新の **「Redeploy」** でも同じです。  

---

## v0で編集する場合

このLPを **v0（v0.dev）** で編集するときの流れです。v0 はプロンプトやコードから UI を生成・変更できるツールです。

### 1. v0 を開く

- ブラウザで **https://v0.dev** を開く  
- Vercel / GitHub でログインする（初回だけ）

### 2. 編集のやり方（2パターン）

#### パターンA: 変更したい部分のコードを貼って直す

1. **「New Chat」** またはチャット入力欄を開く  
2. 編集したい範囲の **HTML** を `mama_index.html` からコピーして貼り付ける  
   - 例：「ファーストビューの見出し部分」「悩みセクション」「フッター」など  
3. プロンプトで指示する  
   - 例：「この見出しのフォントサイズを大きくして」「このセクションの背景色を #f5f5f5 に変更して」「このボタンにホバーアニメーションを追加して」  
4. v0 が返した **コード** をコピーする  
5. ローカルの `mama_index.html` の該当部分を、そのコードで**置き換える**  
6. 画像パスは `image/〇〇.png` のままになるよう、必要なら戻して保存  

※ v0 は React/TSX を出しやすいので、「HTML のままで出力して」と書くと扱いやすいです。

#### パターンB: 文言やレイアウトを文章で説明してコードをもらう

1. v0 のチャットに、**やりたいこと**を日本語で書く  
   - 例：「キャリアコーチLPの「こんな悩み」セクション。見出しの下に、3つのカードを縦並びで、カードは角丸で影付き。Tailwind のクラスで書いて。HTML で出力して」  
2. 生成された **HTML + Tailwind** のコードをコピーする  
3. `mama_index.html` の該当ブロックをそのコードに差し替える  
4. 画像やリンクのパス（`image/xxx.png` など）を、このリポジトリの構成に合わせて直す  

### 3. 注意すること

- **画像パス**: v0 は `image/xxx.png` のような相対パスを知らないので、生成コード内の `src` は自分で `image/〇〇.png` に合わせて直す。  
- **クラス名**: このLPは Tailwind（CDN）を使っているので、v0 で出た Tailwind クラスはそのまま使える。  
- **全体を v0 に渡すと長すぎる**ので、**編集したいブロックだけ**をコピーして渡すとやりやすい。  

### 4. 「Preview Not Supported」と表示されるとき

v0 でリポジトリを開いていると、次のメッセージが出ることがあります。

> **Preview Not Supported**  
> You can still ask v0 to make changes. Once you're ready, open a PR to create a preview deployment.

**意味:**
- このプロジェクト（静的 HTML）では、v0 内の**リアルタイムプレビュー**は使えません。
- **v0 で変更を依頼することはできる**ので、チャットで「〇〇を変更して」と指示してコードをもらえます。
- **プレビューを見る**には、変更を反映したあと **PR（Pull Request）を出す**か **main に push** すると、Vercel のプレビュー／本番URLで確認できます。

**進め方:**
1. v0 のチャットで「この部分を〇〇に変更して」と依頼する  
2. 出てきたコードをコピーし、ローカルの `mama_index.html` に反映する  
3. プレビューを見るには次のどちらか  
   - **A.** ローカルで `index.html` をブラウザで開いて確認  
   - **B.** 変更をコミット → **PR を作成** するか **main に push** → Vercel のデプロイURLで確認  

### 5. 編集後の反映

1. ローカルで `mama_index.html`（と必要なら `index.html`）を保存  
2. 表示を確認したら、いつも通り Git でコミット・プッシュ  
   ```bash
   cd /Users/akiko/Desktop/claudecode/キャリアコーチLP
   git add mama_index.html index.html
   git commit -m "v0で〇〇を修正"
   git push
   ```  
3. Vercel が自動で再デプロイし、本番URLに反映される  

---

## 構成

- `index.html` … トップページ（Vercelのルートで表示）
- `mama_index.html` … 同上のコピー
- `image/` … 画像一式
- `vercel.json` … Vercel 用設定（静的サイト）
