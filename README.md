12/25 筆記
===


## 終端機指令
- cd . 現在的檔案夾位置
- cd .. 上一層案夾
- cd ~ 我的目錄，就是目前這個使用者的目錄
- -a  all 全部
- -l  long 查看完整名稱
- -al
- touch 可以建立檔案
  - touch 檔名(不存在)會直接建立
- ls  列出全部檔案（包含隱藏檔）



## 新建repository
- 先在本地端建立數據庫
初始化並且被git託管
``` bash=
$git init
```
- 將檔案加入到緩存區
```bash=
//兩種都可以
$git add .
$git add 檔案名
```
- 提交
```bash=
$ git commit -m "commit 資訊 "
$ git ci -m " commit 資訊"
```
- 將本地數據庫加入遠端數據庫 remote
```bash=
$git remote add <遠端數據庫簡稱> <url>
```
- 推到遠端伺服器更新 push
```bash=
//第一次推上去需要完整
$git push -u origin main
```


## 分支
- 建立
```bash=
$git branch 分支名
$git br 分支名
```
- 切換分支
```bash=
$git switch 分支名
$git checkout 分支名(舊版)
```
- push分支
```bash=
$git push -u origin

//如果是新建分支第一次push
$git push -u origin 分支名
$git push --set-upstream origin 分支名

//以後持續記錄新版本就可以直接push
$git push
```

## 分支操作
```bash=
//分支改名
$git branch -M main
//可以查看所有的分支
$git branch
//刪除
$git branch -d 分支名
```
## 合併分支
「盡量」避免衝突
可以頻繁地 merge 你的功能分支 （當然還是要保持完整性）
```bash=
//把a分支合併進去 main 裏面
# 1. 切換回 main 分支
git switch main
# 2. 把 a 合併進來
git merge a
```
main(正式版)的merge要小心

---

**12/26 筆記**

### 面試前要準備!!
- 觀念要可以說得出來、解釋得出來
- 複習以前的東西
- 開讀書會

### 要去補充的資訊 
* 資料結構
* 演算法
* 資料庫
  - 正規化
* 網路
* 作業系統
        -  管理電腦操作

#### 訂單設計
> orders 裡的 total_amount
- 經常被讀取、不會變動就可以寫進資料庫
- 雖然違反資料庫設計原則
> orders 裡的 show_amount
- 可能有退貨，會員中心訂單顯示的價格
> 訂單有幾項商品會放在 order_detail 
- 訂單商品明細需要存price
    - 因為可能價格會有調整(訂單當下的資訊(price)需要紀錄)
- 出現在會員中心、訂單管理->就必須存下來

## 程式執行效率 big O
- 空間上、時間上*
- 在電腦裡=>乘除 效率較低
- big O(1)等級 => 一個n，n是常數，沒有迴圈
- big O(n)等級 => 一個n，一層迴圈
- big O(n^2)等級 => 2個n，2層迴圈

### 名詞解釋
[參考網站](https://jimmyswebnote.com/javascript-sync-async/)
- 同步synchronous
- 非同步(異步)asynchronous
- 事件循環（event loop）
    -JS的EVENT LOOP和NODE.JS的不一樣
![](https://i.imgur.com/p7nfN41.png)


>## NODE.JS
- 不是程式語言
- 核心是V8引擎
- 單執行緒、非阻塞、非同步(異步)IO、event loop
- JS是瀏覽器執行
        - NodeJS 另外一個可以執行 Javascript 的地方 
- 安裝
    - 官網
        - current :最新版
        - active :正在積極維護
        - LTS :長期維護
        - EOL :end of life，生命週期結束、不再維護
    - nvm 
        - node version manager
        - nvm -v =>看版本
        - nvm list =>列出你目前主機安裝的版本  
- node 指令
    - node 檔案名 =>執行
- ducument.getElementBy、window.location 
  - document, window,... 這些是瀏覽器提供的物件
 所以這些物件不可以在 nodejs 裡面用

>## 作業系統
thread --> 
- Program : 意旨軟體工程師在 IDE、editor等所寫的程式碼(code)，也就是說還尚未load入記憶體的 code
- Process( 程序、進程 ) : 執行中的程式
    - 點開應用程式就是將 Program 活化成 Process
    - 每一個 Process 是互相獨立的 
    - process是thread的容器
-![](https://i.imgur.com/ZVdr56W.png)
    - 以工廠為比喻，滿好懂(https://miro.medium.com/max/600/1*MtB9qFeTNeqVr_bDMz_Cxw.jpeg)
- Thread (執行緒、線程 multi-thread)
    - 同一個 Process 底下的 Thread 共享資源，如 記憶體、變數等，不同的Process 則否 
    - 若執行緒之間互搶資源，則可能產生死結
- Thread pool(執行緒池)
- 排程演算法: FIFO(First In First Out) / SJF(Shortest-Job-First):時間短就先排

- Deadlock(阻塞/死結)
        -  死結<=>活結(兩人互相禮讓，卻恰巧站到同一側，再次讓開，又站到同一側，同樣的情況不斷重複下去導致雙方都無法通過)
    - process 1和process 2互相卡住不相讓
    - p1在a資源但又需要b資源才能執行，p2在b資源但又需要a資源才能執行，p1、2互相等待資源被釋放所以卡住了
- Context Switching(內容轉換)
    -  切換process會有成本(載入需要時間)，盡可能減少Context Switching效率會較快
    -  解法
        -  增加register : 盡可能讓每個Process分到一個resgister，但它貴所以這是不實際的用法
        -  用thread : 切分process，thread彼此可以分享Memory Space，私有訊息量不多所以可以降低Context Switching對記憶體進行大量存取，可降低Context Switch負擔。
- Race Condition **
    - 多個線程可以訪問共享數據，它們試圖同時更改它們時就會發生競爭狀態，線程調度可以在多個線程間轉換，所以會不知道線程訪問的順序。


- stack   :資料結構名字
- heap    :資料結構名字，沒存檔會不見


## JS 觀念
- Hoisting 去補充*
- 文件裡有寫ECMAscript 是JS原生的 
- JavaScript 是一個同步語言(網路有人也有說是非同步，不要太相信網路啊哈)
    - 心得:很容易被同步的中文影響，會以為是全部一起執行，但其實是一個執行完才會繼續下一個執行
>遞迴recursive
 - 會重複呼叫自己這個函式
 - 需要停止點
 - 電腦演算法
       
```javascript=
// 範例 從1加到n
function sum(n) {
    if (n < 1)
      return 0;
    return n + sum(n - 1);
    //重複呼叫 sum(n - 1) 直到 n<1 才停止
}
```
### 記得要做的事
1. Hoisting
2. MDC
3. 寫組內js array 筆記
