# 網頁搜圖

## 概念:
![](https://i.imgur.com/Vm8auDz.png)

圖片大部分節點都是img，和src獲取圖片網址

## 困難點:

1.如何獲取只在文中的圖片?而非廣告,logo,推薦,或其他隱藏但不重要的圖片

2.如果找到圖片網址中的節點，以上圖來看，圖片網址是data-src

3.怎麼處理抓到的圖片網址，有許多不是完整網址，會缺少他們網站代表性的部分url，導致無法獲得正確圖片。
ex:
. ./. ./attachement/jpg/7a2911.jpg
/attachment/3sd2sdf.jpg
//attachment/5sdfds.png
## 解決方式:
針對問題1:
***機密*** XD

針對問題2:
找尋節點符合以下格式
\s*([-_a-zA-Z]*src)=
再使用此節點取得圖片網址。

**有機會失敗**

針對問題3:
透過傳入的url，找出http(s)?://.+/為第一個測試的header，如果requests.get(header+imgage_url) 狀態碼是404，代表這個header是錯誤的，使用while迴圈，原本傳入的url取代上面pattern後，再繼續找下一個/，再去更新header重複上面動作，直到找出真正的header也就是requests.get(header+image_url).status_code == 200。

## 無法處理的問題

1.無法做到100%的準確率，還是會有各種失誤或多抓的圖片

2.如果圖片網址沒有jpg,jpeg,png等標記，幾乎會失敗

3.問題1的準則出錯，就會失敗

4.程式是使用get獲取方式，任何有鎖有擋的網站，皆會失敗，無一例外。

**備註**:

如果文中沒有圖片或是程式無法處理，會返回
“No pictures or can not deal with.”
的訊息

