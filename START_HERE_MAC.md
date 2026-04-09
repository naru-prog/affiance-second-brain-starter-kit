# はじめての方へ — Mac完全ガイド

> 「ターミナルって何？」「Gitって食べ物？」というレベルでも大丈夫。
> 上から順に、書かれているとおりに操作するだけで、あなた専用のAIセカンドブレインが立ち上がります。
>
> **所要時間: 約45分**（途中で休憩してOK）
> **対象: Mac ユーザー / 初心者**

---

## 用意するもの

- Mac本体（macOS 12 以降を推奨）
- インターネット接続
- メールアドレス1つ（GitHub登録用）

以上です。お金はかかりません。

---

## 全体の流れ

```
[1] ターミナルを開けるようになる        … 5分
[2] Homebrew をインストール（道具箱）   … 10分
[3] Git・VS Code・GitHub CLI を入れる   … 10分
[4] GitHub アカウントを作る             … 5分
[5] スターターキットを配置              … 3分
[6] setup.sh を実行                     … 5分
[7] VS Code で開いて Claude Code を入れる … 5分
[8] CLAUDE.md にあなたの名前を書く       … 2分
```

各ステップに **「✅ ここまでできたら次へ」** チェックを置いています。
不安なときは Claude に「ここで止まったよ、エラーは○○」と聞けばOKです。

---

## ステップ1: ターミナルを開く

「ターミナル」とは、Macに文字で命令を出すためのアプリです。普段は使わなくても、Macには最初から入っています。

### 開き方

1. キーボードで `⌘ Command` + `スペース` を同時に押す
2. 画面中央に検索バーが出てくる（Spotlight検索）
3. `terminal` と入力
4. 「ターミナル.app」が出てきたら `Enter` キーを押す

黒い（または白い）画面が出てきましたか？それがターミナルです。怖がらなくて大丈夫。

### 試しに1つコマンドを打ってみる

ターミナルに以下を **コピペ** して `Enter`:

```
echo "hello brain"
```

`hello brain` と返ってきたら成功です。

> 💡 **コピペのコツ:** ターミナルへの貼り付けは `⌘ Command` + `V` です。

**✅ ここまでできたら次へ**

---

## ステップ2: Homebrew をインストール

Homebrew（ホームブリュー）は、Mac用の **「ソフトウェア自動インストーラ」** です。これがあると、あとの作業が一気に楽になります。

ターミナルに以下を1行コピペして `Enter`:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

途中で **Macのログインパスワードを聞かれます**。入力してください（画面には何も表示されませんが、ちゃんと入力されています）。

`==> Installation successful!` のような表示が出たら完了。**約5〜10分** かかります。

### Apple Silicon Mac (M1/M2/M3/M4) の場合の追加作業

インストール完了後、画面の最後のほうに「Run these two commands…」という英語メッセージが出ます。そこに書かれている2行を **そのままコピペして実行** してください。だいたいこんな感じ:

```
echo >> ~/.zprofile
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

確認:

```
brew --version
```

`Homebrew 4.x.x` のように表示されればOK。

**✅ ここまでできたら次へ**

---

## ステップ3: Git・VS Code・GitHub CLI を入れる

Homebrew が動くようになったので、ここから一気に必要な道具を入れます。
ターミナルに以下を1行ずつコピペして `Enter`:

```
brew install git
```

```
brew install --cask visual-studio-code
```

```
brew install gh
```

各コマンドは **数十秒〜数分** かかります。`==> Pouring …` などのメッセージが流れたら待ってください。

### VS Code に「code」コマンドを通す

VS Code をターミナルから起動できるようにします。

1. Launchpad（F4キー or Dockのロケット）から **Visual Studio Code** を起動
2. `⌘ Command` + `⇧ Shift` + `P` を同時押し → 上部に検索バー出現
3. `Shell Command: Install 'code' command in PATH` と入力 → 出てきたものを `Enter`
4. パスワードを求められたら入力

ターミナルに戻って確認:

```
code --version
git --version
gh --version
```

それぞれバージョン番号が出ればOK。

**✅ ここまでできたら次へ**

---

## ステップ4: GitHub アカウントを作る

GitHub（ギットハブ）は **あなたのBrainをクラウドにバックアップする場所** です。無料プランで十分。

1. ブラウザで https://github.com を開く
2. 右上 **Sign up** をクリック
3. メール → パスワード → ユーザー名 を入力
4. 認証メールが来るのでクリックして完了

### ターミナルから GitHub にログインする

```
gh auth login
```

質問に **キーボードの矢印キー** で答えていきます:

| 質問 | 答え |
|---|---|
| Where do you use GitHub? | **GitHub.com** |
| What is your preferred protocol? | **HTTPS** |
| Authenticate Git with your GitHub credentials? | **Yes** |
| How would you like to authenticate? | **Login with a web browser** |

**ワンタイムコード** が画面に表示されます（例: `ABCD-1234`）。これをメモして `Enter`。

ブラウザが自動で開くので、コードを貼り付け → Authorize。

ターミナルに `✓ Logged in as ...` と出れば成功。

**✅ ここまでできたら次へ**

---

## ステップ5: スターターキットを配置

このフォルダ（`starter-kit/`）を、自分の作業場所にコピーします。

1. **Finder** を開く
2. 配布された `starter-kit` フォルダを選択 → `⌘C` でコピー
3. サイドバーから **書類 (Documents)** を開く
4. `⌘V` で貼り付け
5. 貼り付けたフォルダを右クリック → **名前を変更** → `my-brain` にする

ターミナルに戻って、そのフォルダに移動:

```
cd ~/Documents/my-brain
```

中身を確認:

```
ls
```

`CLAUDE.md  setup.sh  knowledge  ...` のように一覧が出ればOK。

**✅ ここまでできたら次へ**

---

## ステップ6: setup.sh を実行

ここで一気にBrainの中身が整います。

```
chmod +x setup.sh
```

（これは「このファイルを実行可能にする」という意味。エラーが出なければOK）

```
./setup.sh
```

途中で **2回質問** されます:

- 「あなたの名前を入力してください」 → フルネームでOK（例: `Taro Yamada`）
- 「あなたのメールアドレスを入力してください」 → GitHubで使ったメールと同じ

最後に **`🎉 セットアップ完了！`** と出れば成功です。

**✅ ここまでできたら次へ**

---

## ステップ7: VS Code で開く + Claude Code を入れる

```
code .
```

（最後のドットも忘れずに）

VS Code が開きます。初回は右下に **「Do you trust the authors?」** と聞かれるので **「Yes, I trust」** をクリック。

### 推奨拡張機能をまとめて入れる

右下に **「Do you want to install the recommended extensions?」** という通知が出ます → **「Install」** をクリック。

これで以下が自動で入ります:
- Claude Code
- Draw.io Integration
- Markdown All in One
- YAML

### Claude Code にログイン

1. 左サイドバーの **🤖 Claudeアイコン** をクリック
2. **「Sign in」** ボタン → ブラウザが開く → Anthropicアカウントでログイン
3. VS Code に戻ると、Claudeパネルが使えるようになっています

**✅ ここまでできたら次へ**

---

## ステップ8: CLAUDE.md にあなたの名前を書く

これが最後のステップ。あなたのAI相棒に名前と人格を与えます。

1. VS Code 左サイドバーで **`CLAUDE.md`** をクリックして開く
2. `⌘F` で検索バーを出す → さらに矢印アイコンで **置換モード** に切り替え
3. `{{AI_NAME}}` を検索 → 好きな名前で置換（例: `Aria`、`Lumi`、`Serena` など）
4. `{{YOUR_NAME}}` を検索 → あなたの名前で置換
5. `⌘S` で保存

> 💡 **AI相棒の名前が決まらない人へ:** Claudeパネルで「私のAI相棒の名前を3つ提案して。短くて呼びやすいもの」と頼むと候補をくれます。

### 動作テスト

Claudeパネルに以下を打ち込んで `Enter`:

```
あなたの名前と役割を教えて
```

CLAUDE.md に書いた名前で答えてくれたら **完成です** 🎉

---

## 最後に: 初回コミット（セーブポイントを作る）

ターミナルに戻って:

```
cd ~/Documents/my-brain
git add .
git commit -m "initial setup"
```

これで「いまの状態」がGitに保存されました。今後何かあっても、ここに戻れます。

### （任意）GitHubにバックアップ

```
gh repo create my-brain --private --source=. --push
```

**必ず `--private` を付けてください**（公開されると正本が世界中から見えます）。

---

## トラブルシューティング

| 症状 | 原因 | 対処 |
|---|---|---|
| `command not found: brew` | Homebrewのパスが通っていない | ステップ2の「Apple Silicon の追加作業」を実行 |
| `command not found: code` | VS Code の `code` コマンド未設定 | ステップ3 の `Shell Command: Install...` を再実行 |
| `Permission denied` (setup.sh) | 実行権限がない | `chmod +x setup.sh` を先に実行 |
| `gh: not found` | GitHub CLI 未インストール | `brew install gh` |
| Claudeが「正本がありません」と言う | まだ正本が空 | これは正常。S03で作っていきます |
| VS Code が真っ白 | 拡張機能の読み込み中 | 1分待つ |

---

## 困ったら

1. まず **Claudeパネルにエラーメッセージをそのまま貼り付けて聞く**（これが一番速い）
2. それでも解決しなければ、講座のサポートチャネルへ

ようこそ、セカンドブレインの世界へ。
