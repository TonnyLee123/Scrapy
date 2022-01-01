一、Scrapy框架是什麼
- 是一個網頁爬蟲「框架」，擁有完整的Python網頁爬蟲開發功能，也提供開發人員能夠進行客製化，並且，有一定的專案架構及執行流程，所以在未來的維護上較為容易。
- Twisted非同步網路框架所建立的，執行效率也非常的好，適用於大型的Python網頁爬蟲專案。

二、Scrapy框架模組
- Scrapy框架是由以下5個主要模組結合而成，各自有負責的職責，來達成有效率的非同步Python網頁爬蟲。

SPIDERS：撰寫Python網頁爬蟲程式碼的地方，向ENGINE(引擎)發送網頁請求，以及將ENGINE(引擎)所接收的回應結果進行解析與爬取。
ENGINE：核心模組，就像汽車的引擎一樣，負責控制各個模組、傳遞請求及資料。
SCHEDULER：將ENGINE所接收的SPIDERS(爬蟲程式)請求進行列隊，也就是排隊的意思，來調度請求的順序。
DOWNLOADER：負責下載ENGINE(引擎)接收到SCHEDULER(調度器)調度請求的網頁**HTML原始碼**，提供回應結果給ENGINE(引擎)。
ITEM PIPELINE：將SPIDERS(爬蟲程式)所取得的資料進行後續處理，像是資料清理、存入資料庫(例：MySQL)或存入檔案文件(例：CSV、JSON)等。

三、Scrapy框架執行流程
Scrapy框架的流程圖：

1 ENGINE：Hi！Spider, 你要處理哪一個網站？
2 Spider：我要處理xxxx.com。
3 ENGINE：你把第一個需要處理的URL給我吧。
4 Spider：給你，第一個URL是xxxxxxx.com。
5 ENGINE：Hi！SCHEDULER，我這有request請求你幫我排序入隊一下。
6 SCHEDULER：好的，正在處理你等一下。
7 ENGINE：Hi！排程器，把你處理好的request請求給我。
8 SCHEDULER：給你，這是我處理好的request
9 ENGINE：Hi！DOWNLOADER，幫我下載一下這個request請求
10 DOWNLOADER：好的！給你(respone)，這是下載好的東西。（如果失敗：sorry，這個request下載失敗了。然後引擎告訴SCHEDULER，這個request下載失敗了，你記錄一下，我們待會兒再下載）
11 ENGINE：Hi！Spider，這是下載好的東西，你自己處理一下（注意！這兒responses預設是交給def parse()這個函式處理的）
12 Spider：Hi！引擎，我這裡有兩個結果，這個是我需要跟進的URL，還有這個是我獲取到的Item資料。
13 ENGINE：Hi ！ITEM PIPELINE我這兒有個item你幫我處理一下！SCHEDULER！這是需要跟進URL你幫我處理下。然後從第四步開始迴圈，直到獲取完老大需要全部資訊。
14 ITEM PIPELINE：好的，現在就做！

製作 Scrapy 爬蟲 4步驟：
1. 新建專案 (scrapy startproject xxx)：新建一個新的爬蟲專案
2. 明確目標 （編寫items.py）：明確你想要抓取的目標
3. 製作爬蟲 （spiders/xxspider.py）：製作爬蟲開始爬取網頁
4. 儲存內容 （pipelines.py）：設計管道儲存爬取內容

