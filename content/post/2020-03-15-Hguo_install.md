---
title: "Hugo安裝發佈於Github.io"
subtitle:    "使用Hugo部署於Github的一些心得"
description: "我實際執行的過程紀實"
excerpt: "沒有需要特別摘述的地方。"
date: 2020-03-15
author:      "Minshain"
draft: false
image: "https://img.zhaohuabing.com/in-post/2018-05-01-may-day-jiulonghu/snowmountain.jpg"
categories:  [ TECH ]
---
# Step 1: 安裝Hugo
安裝hugo，我的作業系統是Win10，並且是使用 [chocolatey](https://chocolatey.org/)做管理軟體，安裝Hugo使用下列指令。
```
choco install hugo -confirm
```
或如果你要附加擴充功能 Sass/SCSS 版
```
choco install hugo-extended -confirm
```
如果你是其他的作業系統，請參考[HUGO install安裝指南](https://gohugo.io/getting-started/installing)。
# Step 2: 建立網站資料夾
使用命令列提示，建立網站要用的資料夾，使用hugo的指令建立，是為了同時建立網站所需的資料夾結構及相關文件。這邊我們以`hugo_blog`名稱為例。
```
hugo new site hugo_blog
```
# Step 3: 新增佈景主題
可參考 <https://themes.gohugo.io>看看有那些主題可以使用，我們以`hamburg`這個主題為範例，新增的方式有兩種:
1. 使用`Git clone下`載到themes/hamburg資料夾底下。
```
cd hugo_blog
git init
git clone https://github.com/hauke96/hugo-theme-hamburg.git themes/hamburg
```
2. 使用`Git Submodule`新增連結hamburg專案在themes/hamburg資料夾底下，如果官方更新了程式碼， git submodule 會幫助大家進行程式碼的更新，這樣隨時隨地都可以取得最新的程式碼。
```
git submodule add https://github.com/hauke96/hugo-theme-hamburg.git themes/hamburg
```
新增完必須編輯`config.toml`，設定使用主題的名稱，可以使用指令直接`echo 'theme = "hamburg"' >> config.toml`寫入，也可以直接開啟檔案來改。
```
baseURL = "https://minshain.github.io/" #改成你github帳號名稱
languageCode = "zh-tw"
title = "Welcome My HUGO Blog" #標題可自行更改
theme = "hamburg" #主題名稱
```
# Step 4: 新增新文章
```
hugo new posts/my-first-file.md
```
在時檔案會在`content/posts`資料夾裡產生，此檔可使用任意文字編輯器打開markdown文件，將 draft 改成 false，文件內容任意更改。
```
---
title: "My First"
date: 2020-03-14T00:33:10+08:00
draft: false
---
測試部落格
```
如果`draft: true`，則在下達hugo server指令時必須加參數 -D，否則不會顯示這篇文章。
# Step 5: 啟動Hugo服務
```
hugo server -D
```
系統顯示
```
PS D:\hugo_blog> hugo server -D

                   | EN
-------------------+-----
  Pages            | 11
  Paginator pages  |  0
  Non-page files   |  0
  Static files     | 15
  Processed images |  0
  Aliases          |  1
  Sitemaps         |  1
  Cleaned          |  0

Built in 41 ms
Watching for changes in C:\Users\minsh\Dropbox\hugo_blog\{archetypes,content,data,layouts,static,themes}
Watching for config changes in C:\Users\minsh\Dropbox\hugo_blog\config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```
開始任意的網路遊覽器，並輸入[**http://localhost:1313/**](http://localhost:1313)或 [**http://127.0.0.1:1313**](http://127.0.0.1:1313)可以預覽成果。
# Step 6: 部署到GitHub
## 1. 在GitHub建立Repositories
在Github建立`你的帳號.github.io`(使用自己的GitHub帳號)
## 2. 建立public資料夾，並連結GitHub 上自己帳號的repositories
```
git submodule add -f https://github.com/你的帳號/你的帳號.github.io.git public
```
## 3. 執行Hugo指令
```
hugo
```
執行`hugo`指令，自動產生編譯可發佈的檔案至public資料夾
## 4. 將 public 資料夾上版到Github上自己帳號的Repositories
```
cd public
git init
git remote add origin https://github.com/你的帳號/你的帳號.github.io.git
git add .
git commit -m "It my first Hugo commit"
git push origin master
```
完成後，在瀏覽器輸入自己帳號的網址http://你的帳號.github.io，會看到跟本機一樣的部落格。
## 5.備份
發佈基本上到上一步驟就完成了，身為一名工程師，養成將網站資料夾上傳到Github上備份，做好版本管理，也是不可缺少的。
### a. 在Github建立`hugo_blog`名稱的Repositories
### b. hugo_blog資料夾連結到GitHub 上的hugo_blog
```
cd ..
git init
git remote add origin https://github.com/你的帳號/hugo_blog.git
```
### c. 上傳
```
git add --all
git commit -m "My hugo_blog file first commit V1090314"
git push origin master
```
# 備註
## 1. 新增留言版，建立[Disqus](https://help.disqus.com/en/)帳號，之後編輯config.toml
```
baseURL = "https://你的帳號.github.io/" 
languageCode = "zh-tw"
title = "我的第一個部落格"
theme = "hamburg"

[params]
disqus = "你的Disqus帳號"
```
disqus放你的Disqus帳號的`Username`，在Disqus要先填資料時要在語言的部分，填哪種語言留言板就顯示哪種呈現，請在admin->Edit Settings->General裡的Language選擇Chinese，就可顯示中文樣式，目前Disqus沒有繁體中文只有簡體，先將就點用吧。
## 2. 在文章中新增標籤，方便搜尋部落格資料
```
title: "My First Content"
date: 2019-05-20T00:33:10+08:00
draft: false
tags: ["First"]
```

#### 參考資料
<https://coolgood88142.github.io/zh-tw/posts/hugo/>

<https://siddharam.com.tw/post/20190418/>

<https://medium.com/@chswei/%E5%9C%A8-github-%E9%83%A8%E7%BD%B2-hugo-%E9%9D%9C%E6%85%8B%E7%B6%B2%E7%AB%99-9c40682dfe40>
