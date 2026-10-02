# git branch ....

# git branch 怎麼用

`git branch` 用來查看、建立、重新命名與刪除 Git 分支。

常用指令：

```bash
# 查看本地分支（* 是目前所在分支）
git branch

# 查看本地與遠端分支
git branch -a

# 建立新分支
git branch feature-login

# 切換到分支
git switch feature-login

# 建立並立刻切換
git switch -c feature-login

# 重新命名目前分支
git branch -m new-name

# 安全刪除已合併的分支
git branch -d feature-login

# 強制刪除尚未合併的分支（小心）
git branch -D feature-login
```

典型工作流程：

```bash
git switch main
git pull
git switch -c feature-login

# 修改檔案後
git add .
git commit -m "Add login feature"

# 回到主分支並合併
git switch main
git merge feature-login

# 清理已合併的分支
git branch -d feature-login
```

若要把新分支推到遠端：

```bash
git push -u origin feature-login
```

之後在同一分支只需執行 `git push`。較舊的教學可能使用 `git checkout -b feature-login`，效果與 `git switch -c feature-login` 類似。

# git checkout -b 和 branch  有何關係

`git checkout -b <名稱>` 可以理解成「建立分支，然後立刻切換過去」。

```bash
git checkout -b feature
```

大致等同：

```bash
git branch feature       # 建立分支
git checkout feature     # 切換到該分支
```

現代 Git 更推薦語意清楚的寫法：

```bash
git switch -c feature
```

三者關係：

- `git branch feature`：只建立分支，不切換。
- `git checkout feature`：切換到已存在的分支。
- `git checkout -b feature`：建立並切換。
- `git switch -c feature`：也是建立並切換，較新且更直觀。

例如目前在 `main`：

```bash
git checkout -b login
```

會讓 `login` 從目前 `main` 所指向的 commit 建立，並使你立刻位於 `login` 分支上。

若想從特定分支或 commit 建立：

```bash
git checkout -b login origin/main
# 或
git switch -c login origin/main
```