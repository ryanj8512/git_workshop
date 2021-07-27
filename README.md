# Git
## 版本控制系統 Version Control System (VCS)

版本控制（Version Control）是一種軟體工程技巧，籍以在開發的過程中，確保由不同人所編輯的同一檔案都得到更新。版本控制是一種記錄一個或若干文件內容變化，以便將來查閱特定版本修訂情況的系統。

- 本地版本控制系統
其中最流行的一種叫做 RCS，現今許多計算機系統上都還看得到它的蹤影

    ![https://i.imgur.com/phS1FSC.png](https://i.imgur.com/phS1FSC.png)

- 集中化的版本控制系統（Centralized Version Control Systems，CVCS）
這類系統，諸如 CVS、Subversion 以及 Perforce 等，都有一個單一的集中管理的服務器

    ![https://i.imgur.com/xRK4VXX.png](https://i.imgur.com/xRK4VXX.png)

- 分散式版本控制系統（Distributed Version Control System， DVCS）
在這類系統中，像 Git、Mercurial、Bazaar 以及 Darcs 等，客戶端並不只提取最新版本的文件快照，而是把代碼倉庫完整地鏡像下來。

![](https://i.imgur.com/AUidNn3.png)


- 分散式相比於集中式的最大區別在於開發者可以提交到本地，每個開發者通過克隆（git clone），在本地機器上拷貝一個完整的Git倉庫。
[版本控制系統Version Control System](https://www.jianshu.com/p/8cf7fa473028)

---

## 常用的終端機指令

![](https://i.imgur.com/Ck94ec9.png)

參數的意義，不同指令會不一樣，但通常會是這樣
-a ==> all   全部
-f ==> force 強制
-l  ==> list 列表

---

## 安裝 git

確認電腦裡是否有安裝過 git:

```bash=
# 查看git版本
$ git --version
```

沒有安裝過的到 [https://git-scm.com/download/win](https://git-scm.com/download/win) 下載安裝檔

windows:
[https://gitbook.tw/chapters/environment/install-git-in-windows.html](https://gitbook.tw/chapters/environment/install-git-in-windows.html)

---

## 設定環境變數

建議可以打 github 的帳號跟註冊的 email

```bash=
$ git config --global user.name "ryanj8512"
$ git config --global user.email "ryanj8512@gmail.com"
```

確認設定的情況

```bash=
$ git config --list
```

git 的設定檔 [cat 是查看檔案]

```bash=
cat ~/.gitconfig
```

---

### 建立 git 資料夾

初始化 git 資料夾會出現 .git資料夾

```bash=
# 建立檔案夾
$ mkdir git-workshop

# 進入該檔案夾
$ cd git-workshop

# 初始化 git 專案
$ git init

# 檢查看看是否有建立 .git 檔案夾
$ ls -al
```

![](https://i.imgur.com/jWMqNFi.png)

---

### 在 repo 中新增、修改、刪除檔案

==把git管理的檔案夾刪掉，就脫離git管理，版本也會不見; 只要.git檔案夾沒有刪掉，都會找到所有紀錄==

master (main) -> 只要 git 初始化之後，會自動建立的一個主分支

在 BLM 過後，master 被改成叫 main，如果想改 main 的去修改 `cd ~/.gitconfig`，加上以下這段：

```bash=
# 修改預設master=>main
[init]
        defaultBranch = main

# 使編輯器不會進入到VI
[core]
        editor = nano
```

```bash=
# 新增檔案
$ touch hello.txt

# 刪除資料夾 (f 強制)
$ rm -rf .git

# 查看檔案內容
$ cat hello.txt

# 編輯檔案內容
$ nano hello.txt

# 查看資料夾狀態
$ git status
```

---

## 版本控制的狀態分為工作區、暫存區與儲存庫

![https://i.imgur.com/hGK7bxd.png](https://i.imgur.com/hGK7bxd.png)

![https://i.imgur.com/luUKlnD.png](https://i.imgur.com/luUKlnD.png)

git commit:，盡量小、但要完整; 不能把寫到一半的東西和會讓專案壞掉的東西放上去

```bash=
# 把檔案從 工作目錄 加到 暫存區
$ git add hello.txt

# 提交暫存區的檔案到儲存庫(repo)
$ git commit -m "紀錄這次提交的緣由"

# 查看過去版本的紀錄
$ git log
```

---

## 當在git 監管下，修改文件時，查看文件會出現下列訊息

![](https://i.imgur.com/2qtZzvd.png)

### 可以查看檔案修改前後內容，會有+號顯示

```bash==
# 比較檔案的差異 確認後，可以按 q 離開
$ git diff
```

![](https://i.imgur.com/E2KXPbn.png)
確認修改內容後，可 add 重新提交

## 同時 add 跟 commit，只有針對已經 tracked 檔案才有效

要有新增和刪除才能進行，使用 `ctrl+k` 可刪除行

![](https://i.imgur.com/kERUcWR.png)
紅色為刪除，綠色+為新增

```bash==
# 同時add和commit
$ git commit -am "刪除第一行，新增3"
```

![](https://i.imgur.com/kl9JSld.png)

使用 git log 查看時
![](https://i.imgur.com/xN8Zhbe.png)

## 移除檔案注意事項

```bash==
# 從git中移除，但真正刪除檔案
$ git rm {檔案名稱}

# 從git中移除，仍保留硬碟中的檔案
$ git rm --cached {檔案名稱}
```

### rm 直接刪除檔案

![](https://i.imgur.com/nzPK3W9.png)

git add -> 把這個刪除的動作加進去 git 裡
![](https://i.imgur.com/CTLaFct.png)

git commit -> 把刪除動作記錄下來，可用log查詢到
![](https://i.imgur.com/Sp7YPdu.png)

### git rm = 刪除 + git add這個刪除的動作
![](https://i.imgur.com/42HpKlB.png)


### git rm —cached = 刪除但仍保留硬碟中的檔案
![](https://i.imgur.com/txWAZS7.png)


當commit完之後
![](https://i.imgur.com/7ecMAnW.png)


![](https://i.imgur.com/g2sGukQ.png)


### 從repo返回工作目錄

```bash==
# 從暫存區域回到工作目錄
$ git restore --staged {檔案名稱}

# 捨棄在工作目錄的改變(包括修改與刪除)
$ git restore {檔案名稱}

```

- **範例**
    - 當 rm 檔案時，改變的是工作目錄
        - (use "git restore <file>..." to discard changes in working directory)
        提醒可用 git restore回復檔案，此檔案是在工作目錄下刪除的
![](https://i.imgur.com/Wo0l9q0.png)

        - 當用 git restore 救回檔案變化：
![](https://i.imgur.com/k5wvHm2.png)

    - 當 git rm 時，因為 git rm是包含了 add動作，所以檔案是落入暫存區
        - 提示用 git restore --staged <file> 救回檔案
        ![](https://i.imgur.com/XM7Dx1Y.png)

        - 從 工作目錄救回檔案，提示用 git restore <file>
        ![](https://i.imgur.com/LGl7xXh.png)


        - 救回檔案
![](https://i.imgur.com/H8UqhNz.png)

---

## git log 指令的運用:

```bash==
# 看commitID跟歷史紀錄
$ git log

# hashtag會縮寫成一行，簡短行數有利閱讀
$ git log --oneline

# 分支多才看的出來簡短
$ git log --oneline --graph

# 查看特定檔案的紀錄
$ git log a.txt

# 查看特定檔案的修改紀錄內容
$ git log -p a.txt

# 統計 commit 有幾次的修改紀錄
$ git log --stat

# 可以搜尋關鍵字
$ git log --grep="delete"

# 查看內容是誰編寫的
$ git blame hello.txt

```

---

## 建立分支與合併

開發環境(個人電腦) --- 測試環境 --- Staging 環境 ---> 正式環境

> 分支名稱通常會有規範
feature-xxxx、fix-xxxx

```bash==
# 新增分支
$ git branch {branch-name}

# 檢視分支
$ git branch
```
![](https://i.imgur.com/eiGGNLd.png)

```bash
# 切換分支
$ git switch {branch-name}
$ git checkout {branch-name}
```
![](https://i.imgur.com/c2zl5m9.png)

> 在不同分支下修改檔案時，修改過的commit檔案會在當下分支，原版本的檔案會停留在原本分支

- 範例

    hello.txt 在feature-login 分支下修改 "add 444"時，main分支會停留在沒有修改時的版本
    ![](https://i.imgur.com/bgeREiI.png)

    當回main分支時，開啟 hello.txt 檔案時，版本是無修改時的
   ![](https://i.imgur.com/7LLzPj0.png)

    在 feature-login分支時，檔案版本是最新修改過的
![](https://i.imgur.com/W17RwbF.png)


```bash==
# 合併分支, 例如把 feature-login 合併進去 main
$ git merge feature-login
```

- **分支注意重點解決方式**
    - 先開一個 feature-A 分支，並且在這個分支開發功能A
    - 切換回 main(master)，從這裡切一個 fix-B 的分支
![](https://i.imgur.com/lJYtQQ0.png)
    新增分支 fix-B

    - 在 fix-B 這個分支上修改 bug
![](https://i.imgur.com/Eg9Rdua.jpg)
在 fix-B 修改 hello.txt 檔案內容

    - 切換回 main(master)，把 fix-B merge 進 main(master)
![](https://i.imgur.com/iBRRvnn.png)


- **樹狀圖理解方式**
    - 新開了 feature-login 分支，並且作修改，跑出一個分支節點出來
![](https://i.imgur.com/PVviESU.png)

    - 新開了 fix-B 分支，並且和 main 有 merge，合併再一起
![](https://i.imgur.com/r1NGcTg.png)

    - 新增 fix-C 分支並且修改 hello.txt檔案的狀態樹狀
![](https://i.imgur.com/aU51hpf.png)

    - 對 main 的 hello.txt 作修改，就會往前跑
![](https://i.imgur.com/GfE3wzz.png)

- **當 merge 時，修改內容發生衝突時**
    - 在main底下合併fix-C分支時，會偵測檔案裏面重疊的內容
![](https://i.imgur.com/6Aq8Jxj.png)

    - 合併分支衝突修改完內容後
![](https://i.imgur.com/4O8uf4T.png)

    - 將檔案 commit 後
![](https://i.imgur.com/y03mcPc.png)
<br>![](https://i.imgur.com/XOBOg7y.png)

    - 現在要將 feature-login 合併進去 main，解衝突後
![](https://i.imgur.com/y79Dnzh.png)

---

## 和 github 做連結

### 增加一個遠端repo 的連結，這個遠端的名稱叫做 origin

```bash==
$ git remote add origin {url}

$ git branch -M main
```

### 以下指令二選一做，設定 main 這個分支跟 origin 遠端的main 分支做連結且 push 上去

```bash==
$ git push --set-upstream origin main
$ git push -u origin main
```

![](https://i.imgur.com/lz1ySx4.png)

![](https://i.imgur.com/GhZe9z7.png)


### 設定 set-upstream 過後，就可以不用指定 origin {分支名稱}

```bash==
$ git push
```

這些都是紀錄在 .git/config

![](https://i.imgur.com/R3MjIZd.png)