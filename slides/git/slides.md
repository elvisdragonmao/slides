---
theme: ../_shared/theme-em
title: Git & GitHub 基礎
titleTemplate: "%s — 毛哥EM"
author: 毛哥EM
---

# Git & GitHub

從 `final-final-real-2` 到真正的版本控制

毛哥EM

---
src: ../global/me.md
---

## 文章教學

<https://emtech.cc/p/github-and-git/>

今天不求你背完 Git。

只希望下課之後，你知道：**自己的修改現在到底在哪裡。**

---
layout: statement
---

你們用過 Git / GitHub 嗎？

---
layout: statement
---

「等等，剛才寫錯了……可以改回來嗎？」

---
layout: statement
---

「額……原本真的是這樣嗎？怎麼突然跑不起來了？」

---
layout: section
---

# 版本控制

先從大家都做過的「土法煉鋼」開始。

---
layout: image
---

<img src="./img/folder-1.webp" class="mx-auto h-full" />

---
layout: image
---

<img src="./img/folder-2.webp" class="mx-auto h-full" />

---
layout: image
---

<img src="./img/folder-3.webp" class="mx-auto h-full" />

---
layout: image
---

<img src="./img/folder-4.webp" class="mx-auto h-full" />

---
layout: statement
---

`project-final-final-真的-這次真的是最後.zip`

其實你已經在做版本控制了。

只是做得挺糟的。

---
layout: statement
---

「可以把程式碼 Email 給我嗎？」

---
layout: statement
---

「欸等等，這垃圾是誰寫的？」

---

## 我們真正想知道的事情

- 以前長什麼樣子？
- 哪一天改了什麼？
- 是誰改的？
- 為什麼改？
- 改壞了，能不能回去？
- 十個人一起改，要怎麼合？

這些問題，就是 **Version Control** 想解決的。

---
layout: statement
---

introducing...

---
layout: statement
---

# Git

---

## Git 可以幹嘛？

- 專案版本控制：記錄修改歷史
- 團隊協作：多人同時開發、最後再整合
- 回溯錯誤：回到之前正常的狀態
- 讓每次修改都有作者、時間與說明
- Open Source 協作

> _「哦，原來這個垃圾是我寫的。」_

---

## 先講最重要的：Git ≠ GitHub

<div class="grid grid-cols-2 gap-8 mt-8">
<div>

### Git

版本控制軟體

- 跑在你的電腦上
- 可以離線使用
- 管理 Commit / Branch / Merge

</div>
<div>

### GitHub

線上 Git 託管與協作平台

- 放遠端 Repository
- Pull Request / Issue / Actions
- 團隊協作與 Open Source 社群

</div>
</div>

---

## Git 是什麼？

**分散式版本控制系統（DVCS）**

- 每個人的電腦都可以保有完整 Repository 歷史
- 沒網路也能 Commit、看歷史、切 Branch
- 有網路再跟 Remote 交換新的 Commit

<div class="mt-8 text-xl opacity-70">
Git 管的是「版本歷史」，不只是幫你同步檔案。
</div>

---

## Repository：專案的時光機

一個被 Git 管理的專案叫做 **Repository / Repo**。

Repo 裡不只有現在的檔案，還有整個版本歷史。

```text
A  建立網站
│
B  加入登入頁面
│
C  修正登入 Bug
│
D  加入深色模式
```

A、B、C、D 每一個節點，都是一個 **Commit**。

---

## Commit：幫專案留一個存檔點

可以先把 Commit 想成：

> **「這一次修改，我決定正式留下來。」**

一個好的 Commit 通常應該：

- 做一件相對完整的事情
- 有清楚的 Commit Message
- 之後看得懂「為什麼改」

```text
feat: add login form
fix: correct navbar overflow
docs: update installation guide
```

---

## Git 的核心流程

```text
Working Directory
      │
      │ git add
      ▼
 Staging Area
      │
      │ git commit
      ▼
 Local Repository
      │
      │ git push
      ▼
    Remote
```

今天最重要的，就是先把這張圖裝進腦袋。

---

## 用「寄包裹」理解 Git

| Git               | 寄包裹                   |
| ----------------- | ------------------------ |
| Working Directory | 你的工作桌               |
| `git add`         | 把這次想寄的東西放進箱子 |
| Staging Area      | 箱子裡準備寄出的內容     |
| `git commit`      | 封箱，留下正式紀錄       |
| Commit Message    | 箱子上寫「這次改了什麼」 |
| Remote            | 收件地址                 |
| `git push`        | 寄出去                   |
| `git pull`        | 把遠端的新東西拿回來整合 |

---
layout: section
---

# 先把 Git 跑起來

等等直接做一次。

---

## 安裝 Git

<https://git-scm.com/>

有套件管理器也可以直接裝：

```bash
# macOS
brew install git

# Ubuntu / Debian
sudo apt install git

# Windows
winget install --id Git.Git -e --source winget
```

安裝完可以確認：

```bash
git --version
```

---

## 第一次使用：設定作者資訊

```bash
git config --global user.name "你的名字"
git config --global user.email "you@example.com"
```

檢查：

```bash
git config --global --list
```

這是 **Commit 的作者資訊**，不是 GitHub 帳號密碼。

---
layout: statement
---

# 實作時間

把今天做的網站 / 專案放上 GitHub。

---

## GitHub 是什麼？

☁️ 線上 Git Repository 託管與協作平台

- Repository
- Issue / Discussion
- Pull Request / Code Review
- GitHub Actions
- GitHub Pages
- Open Source 社群

<div class="mt-6 opacity-70">
可以把它想成工程師的 Facebook + 協作中心 + 部署入口。
</div>

---

## 建立第一個 Repository

<div class="grid grid-cols-2 gap-8 items-center">
<div>

GitHub → **New repository**

先設定：

- Repository name
- Description
- Public / Private

今天為了流程簡單：

- README 先不勾
- `.gitignore` 先不勾
- License 先不勾

</div>
<div>

<img src="./img/create-repo.webp" class="rounded-xl shadow max-h-[420px] mx-auto" />

</div>
</div>

---

## Clone：把 Repository 拿回電腦

<div class="grid grid-cols-2 gap-8 items-center">
<div>

```bash
git clone https://github.com/USERNAME/git-workshop.git
cd git-workshop
```

`clone` 不只是下載現在的檔案。

它會把：

- Repository
- Commit 歷史
- Remote 設定

一起拿下來。

</div>
<div>

<img src="./img/codebase.webp" class="rounded-xl shadow max-h-[420px] mx-auto" />

</div>
</div>

---

## 先正常寫你的 Code

<div class="grid grid-cols-2 gap-8 items-center">
<div>

建立一個 `hi.txt`：

```text
Hello Git!
```

或是直接編輯今天做的網站。

Git 不會妨礙你寫程式。

它只是在旁邊默默看著。

</div>
<div>

<img src="./img/edit-text.webp" class="rounded-xl shadow max-h-[420px] mx-auto" />

</div>
</div>

---

## `git status`：我在哪？現在發生什麼事？

```bash
git status
```

如果哪天 Git 看起來怪怪的，先打它。

它會告訴你：

- 目前在哪條 Branch
- 哪些檔案改過
- 哪些檔案已 Stage
- 哪些檔案還沒 Stage

<div class="mt-6 text-xl">
不知道要幹嘛？先 `git status`。
</div>

---

## `git add`：把這次要 Commit 的東西放進箱子

```bash
git add hi.txt
```

一次選多個：

```bash
git add index.html style.css script.js
```

全部都要：

```bash
git add .
```

<div class="mt-6 opacity-70">
正式專案建議先 `git status` / `git diff` 看一下，不要把 `.env`、API Key、4GB 奇怪檔案一起裝箱。
</div>

---

## `.gitignore`：有些東西 Git 就不要管

```text
node_modules/
.env
.DS_Store
*.log
```

尤其 `.env` 常常會有：

- API Key
- Token
- Database Password

<div class="mt-8 text-xl">
**Secret 一旦 Push 到公開 Repo，不要只刪檔案。請直接把 Secret 作廢並重新產生。**
</div>

---

## `git commit`：封箱

<div class="grid grid-cols-2 gap-8 items-center">
<div>

```bash
git commit -m "feat: say hello"
```

Commit Message 就是在說：

> 這一版到底做了什麼？

例如：

```text
feat: add login page
fix: navbar overflow
docs: update README
```

</div>
<div>

<img src="./img/commit.webp" class="rounded-xl shadow max-h-[420px] mx-auto" />

</div>
</div>

---

## Commit 完，東西還只在你電腦

```text
Working Directory
      │
      │ git add
      ▼
 Staging Area
      │
      │ git commit
      ▼
 Local Repository   ← 你現在在這
```

所以：

```bash
git commit
```

**不是上傳。**

---

## `git push`：真的寄出去

```bash
git push
```

第一次 Push 某條 Branch，常見會寫：

```bash
git push -u origin main
```

- `origin`：Remote 名稱
- `main`：Branch 名稱
- `-u`：順便記住 upstream，之後可以直接 `git push`

---

## `git pull`：把遠端更新拿回來

```bash
git pull
```

初學可以先理解成：

> **把 Remote 的新 Commit 拿回來，整合到現在的 Branch。**

它不是單純「下載檔案」。

也因為有「整合」這件事，等等才會遇到最經典的：

**Merge Conflict**

---

## 日常 Git Loop

```bash
# 看一下現在怎樣
git status

# 開發...

# 看自己改了什麼
git diff

# 放進下一個 Commit
git add .

# 留下紀錄
git commit -m "feat: do something"

# 傳到 Remote
git push
```

別人有更新：

```bash
git pull
```

---

## 幾個超常用的查看指令

```bash
# 看狀態
git status

# 看還沒 Stage 的修改
git diff

# 看 Commit 歷史
git log --oneline

# 看漂亮一點的圖
git log --oneline --graph --all
```

你不用背所有 Git 指令。

但這四個真的很值得記。

---
layout: section
---

# Branch

不要直接在正式版本上亂搞。

---

## Branch：開一條平行世界

```text
main
A ─── B ─── C
          \
           D ─── E
               feat/login
```

`main` 可以繼續保持穩定。

你在 `feat/login` 裡慢慢把登入功能寫完。

做完、測完，再合回去。

---

## 建立與切換 Branch

建立並直接切過去：

```bash
git switch -c feat/login
```

切回 `main`：

```bash
git switch main
```

舊教學常看到：

```bash
git checkout -b feat/login
```

今天新手先記 `git switch` 就好，語意比較清楚。

---

## 在 Branch 上工作

```bash
git switch -c feat/login

# 修改檔案...

git add .
git commit -m "feat: add login form"
git push -u origin feat/login
```

現在 Remote 上就會有：

```text
main
feat/login
```

---

## `git merge`：把 Branch 合回去

先站在**要接收修改**的 Branch：

```bash
git switch main
git pull
```

再把 `feat/login` 合進來：

```bash
git merge feat/login
git push
```

記法：

> **把「指定的 Branch」合進「我現在所在的 Branch」。**

---
layout: statement
---

# Merge Conflict

Git：「這兩個答案我不敢幫你猜。」

---

## Conflict 怎麼來的？

海鷗改同一行：

```text
Hello from Seagull!
```

Ben 也改同一行：

```text
Hello from Ben!
```

Git 不知道誰才是對的。

所以它不亂選，而是停下來叫你決定。

---

## 你可能會看到這個

```text
<<<<<<< HEAD
Hello from main!
=======
Hello from dev!
>>>>>>> dev
```

翻成人話：

```text
目前這邊是 main 的版本
----------------------
另外一邊是 dev 的版本

你決定最後要留下什麼。
```

Conflict 不是 Git 壞掉。

是 Git 很誠實地說：**「我不知道。」**

---

## 用 VS Code 解 Conflict

VS Code 通常會提供：

- Accept Current
- Accept Incoming
- Accept Both
- Compare Changes

也可以直接自己改成真正想要的內容。

解完：

```bash
git add <resolved-files>
git commit
git push
```

---

## Remote：到底要 Push 去哪？

查看目前 Remote：

```bash
git remote -v
```

可能看到：

```text
origin  https://github.com/elvis/project.git (fetch)
origin  https://github.com/elvis/project.git (push)
```

`origin` 只是大家慣用的 Remote 名稱。

你真的要叫它 `banana` 也不是不行。

---

## 本機原本就有專案？用 `git init`

```bash
cd my-project
git init

git add .
git commit -m "chore: initial commit"
```

GitHub 建立空 Repo 後：

```bash
git remote add origin https://github.com/USERNAME/my-project.git
git branch -M main
git push -u origin main
```

這是「先有本機專案，後來才放 GitHub」的常見流程。

---
layout: section
---

# 團隊協作

真正開始跟別人一起寫 Code。

---

## Pull Request：我想把我的修改合進去

Pull Request（PR）大概是在說：

> **「嗨，我做了一組修改，可以幫我看一下，然後合進去嗎？」**

一個 PR 不只是「按 Merge」。

它通常包含：

- 修改內容
- 討論
- Code Review
- 自動測試
- 最後的 Merge

---

## 同一個團隊：Branch → PR

```bash
git switch main
git pull

git switch -c feat/login

# 開發...
git add .
git commit -m "feat: add login"

git push -u origin feat/login
```

GitHub：

```text
base:    main
compare: feat/login
```

然後開 Pull Request。

---

## PR 要寫什麼？

不要只寫：

```text
fixed bug
```

可以寫：

```text
Fix mobile navbar overflow

原因：
Navbar 使用固定寬度，在 375px 以下會 overflow。

修改：
- 改用 flex-wrap
- 調整 mobile breakpoint
- 補上相關測試
```

讓 Reviewer 不用先通靈。

---

## 別人的專案：Fork

你沒有原 Repository 的 Write 權限時，常見流程：

```text
原作者 Repository
       │
       │ Fork
       ▼
你的 GitHub Repository
       │
       │ Clone
       ▼
你的電腦
       │
       │ Commit + Push
       ▼
你的 GitHub
       │
       │ Pull Request
       ▼
原作者 Repository
```

---

## Fork 後常見的 Remote

```bash
git remote -v
```

```text
origin    你的 Fork
upstream  原作者
```

加上原作者：

```bash
git remote add upstream https://github.com/ORIGINAL-OWNER/project.git
```

這樣就能分清楚：

- `origin`：我自己的 Fork
- `upstream`：真正的原專案

---

## Code Review：不要看到綠色按鈕就按

Reviewer 會看：

- 這段 Code 有沒有 Bug？
- 命名與結構合理嗎？
- 有沒有漏掉 Edge Case？
- 有沒有測試？
- 為什麼 Password 在這裡？

常見結果：

- Comment
- Request changes
- Approve

---

## GitHub Actions：叫機器先幫你檢查

```text
Pull Request
    │
    ▼
Lint
    │
    ▼
Test
    │
    ▼
Build
    │
    ▼
Security Check
    │
    ▼
✅ 可以 Merge
```

也可以：

```text
Merge 到 main → Build → Deploy → 網站上線
```

---

## PR 的三種 Merge 方法

### Merge commit

保留 Branch 合併的節點，歷史完整。

### Squash and merge

把 PR 裡很多小 Commit 壓成一個再進 `main`。

### Rebase and merge

把 Commit 重新接到最新 `main` 後面，歷史比較直。

<div class="mt-6 opacity-70">
今天先知道有三種就好；真正團隊會依歷史策略選擇。
</div>

---

## 一套真的可以拿去用的流程

```text
更新 main
   ↓
開 Branch
   ↓
開發 / Commit
   ↓
Push
   ↓
Pull Request
   ↓
Actions / Code Review
   ↓
修改
   ↓
Approve
   ↓
Merge
   ↓
刪 Branch
   ↓
本機 Pull 最新 main
```

---

## Branch 名稱怎麼取？

常見例如：

```text
feat/login
feat/profile
fix/navbar
fix/payment-timeout
docs/install-guide
refactor/auth
```

重點不是一定要照格式。

重點是：**看到名字就知道這條 Branch 在幹嘛。**

不要：

```text
test
test2
newnew
aaa
```

---

## 幾個常見翻車點

- Commit 前沒看 `git status`
- `.env` / Secret 被加進 Git
- 所有人都直接改 `main`
- 一個 Commit 同時做 17 件不相干的事情
- PR Description 只寫 `update`
- Conflict 一出現就開始刪檔案

<div class="mt-8 text-xl">
Git 通常沒有你想像中那麼容易壞。

很多時候它只是比你更清楚「你現在到底改了什麼」。

</div>

---
layout: section
---

# 最後複習

---

## 先把這幾個記起來就好

```bash
# 拿專案
git clone <url>

# 看狀態
git status

# 看修改
git diff

# 放進下一個 Commit
git add .

# 留下版本紀錄
git commit -m "訊息"

# 傳上去
git push

# 拿遠端更新
git pull
```

---

## Branch 先記這組

```bash
# 建立並切換
git switch -c feat/xxx

# 切換
git switch main

# 合併
git merge feat/xxx

# 看歷史
git log --oneline --graph --all
```

---
layout: statement
---

你不需要背 Git Manual。

你需要知道的是：

**我的修改現在在哪？**

---

## 腦袋裡要有這張地圖

```text
我的修改現在在哪？

Working Directory？
        ↓
Staging Area？
        ↓
Local Commit？
        ↓
哪條 Branch？
        ↓
Remote 有沒有？
        ↓
要合去哪裡？
```

指令忘記可以查。

這張地圖沒有，就會變成施法。

---
layout: statement
---

所有很大的開源專案，

最後其實都是這樣長大的：

**一個 Commit，再下一個 Commit。**

---

## 下次看到一個 Bug

可以試試看：

```text
Fork
↓
Branch
↓
改掉它
↓
Commit
↓
Push
↓
Pull Request
```

下一個 Commit，也許就是你的。

---

## 完整文章

<https://emtech.cc/p/github-and-git/>

<div class="mt-10 text-3xl">
Q & A
</div>

---
src: ../global/cc.md
---
