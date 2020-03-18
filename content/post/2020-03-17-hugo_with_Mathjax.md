---
layout:     post
title:       "在Hugo中以Mathjax實現顯示數學式" 
subtitle:    ""
description: ""
excerpt: "摘述。"
date:         2020-03-17
author:      "陳銘祥"
image: "/img/post-bg-coffee.jpeg" #專屬該篇文章的背景圖片
published: true #如果草稿尚未發表，改為"false"
tags:
    - Hugo
    - mathjax
#URL: "/2020/03/17/Hugo_with_Mathjax/" #想要在網址列顯示的樣子
categories:  [ Tips ] #分類，會影響下拉式選單。[ "Life" ] ["TIP"]
markup: mmark
---
# HTML 中的數學公式
要在HTML網頁中顯示數學公式並不是很簡單的一件事情，一般最簡單的方法，就是用Word打好後直接複製貼上，或是轉成圖片來做使用，這是最為穩妥一定能夠顯示的方式，但也帶來耗時耗力的困擾，如果數字要更改，更要重新編寫。
我目前測試成功的方式，是使用`MathJax`來進行處理，效果和兼容性都還不錯。

# Markdown 後端
Hugo預設使用的markdown處理後端是Blackfriday，此外也支持使用Mmark．後者是從前者fork而來的．為了避免麻煩，建議在寫包含數學公式的文章時，直接宣告使用Mmark．只需要在markdown文件的front matter裡加上一行：
```
markup: mmark
```
即可切換到Mmark．推薦使用Mmark的原因，主要是無需更多的設定就可以開始寫數學公式了，數學公式全部用`兩個錢號(Dollar sign)`包圍起來，行內公式和行間公式都是一樣的，區別在於行間公式前後加上一個空行，這樣就可以讓Mmark 自動判斷你需要的是行內公式還是行間公式了．行內公式像這樣 $$f(x) = \sin(x)$$，行間公式的例子：
```
$$
f(x) = \sin(x)
$$
```
顯示效果為：
$$
f(x) = \sin(x)
$$

另一個範例，在題目中使用行內公式，及題目後顯示行間公式。
```
When $$a \ne 0$$, there are two solutions to `\(ax^2 + bx + c = 0\)` and they are:

$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}$$
```
顯示效果為 :
When $$a \ne 0$$, there are two solutions to `\(ax^2 + bx + c = 0\)` and they are:

$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}$$

# Hugo 的設置
這個很簡單，只需要在hugo的主題目錄裡，加上一行代碼到你的部落格頁面一定會包含的文件即可．一般可以選擇加入到themes/cleanwhite/layouts/partials/footer.html裡，這裡的cleanwhite是我使用的hugo主題名稱．需要增加的一行代碼為：
```
<!---mathjax 數學公式支援-->
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.2/MathJax.js?config=TeX-MML-AM_SVG">
</script>
```
MathJax還有很多可以設置的選項，這裡不講，因為我也很少用，有興趣的可以參考MathJax的配置．

# 數學公式的書寫
接下來就可以愉快的在markdown 中書寫數學公式了。

# 問與答
- 如果無法顯示行內公式，請查看文章前端是否有加上 `markup: mmark` 宣告使用格式。
- 使用Mmark格式，在cleanwhite主題中，將文章前面將**無法顯示目錄(TOC)**。


參考資料:\
<https://butui.me/post/yet-best-math-formula-support-for-hugo-with-mathjax/>\
<https://gohugo.io/content-management/formats/#mathjax-with-hugo>\
<https://docs.mathjax.org/en/latest/index.html>

--------
END