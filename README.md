# NTP伺服器
## 組員
B1042052 黃子凌

B1042090 張傑崴
## NTP介紹
* 一、NTP是什麼
  - Network Time Protocal (網路時間協議)
  - 讓不同時區的人可以透過網路來同步時間
  
* 二、為何要架設NTP伺服器
  - 分流-可以避免因為某部時間伺服器主機突然掛點時，其他主機仍可以提供NTP主機做更新

* 三、實際應用
  - 目前已廣泛應用於金融、通信、交通、廣電、國防、教育等等
  - 例如 : 股市、證券、期貨、遠端視訊軟體
  
## 實作一 : 同步時間
* 將網路設定成[橋接介面卡]

![圖片1](https://user-images.githubusercontent.com/106873001/172388904-5f3ec5d6-45d0-44e0-b7db-86efca4e787c.png)

* 確認IP
```shell
sudo apt install net-tools
```
```shell
ifconfig
```

內部網路應為[192.168.x.x]

![螢幕擷取畫面 2022-06-07 212950](https://user-images.githubusercontent.com/106873001/172393551-499f23d1-ba35-445b-a7f1-e296f4f9fa3b.png)

   
  
  
 * 下載NTP
 ```shell
 sudo apt-get install ntp
 ```
 
 * 在windows設定中選擇[時鐘和區域]

![螢幕擷取畫面 2022-06-07 214652](https://user-images.githubusercontent.com/106873001/172399165-75486242-6e65-4247-ad53-d1777e4b73fc.png)

* 選擇[設定時間和日期]

![螢幕擷取畫面 2022-06-07 214939](https://user-images.githubusercontent.com/106873001/172399395-dde03cd0-a89e-48c1-9fc6-248a6f8d01ac.png)

* 選擇[網際網路時間]，並點選[變更設定]

![螢幕擷取畫面 2022-06-07 220052](https://user-images.githubusercontent.com/106873001/172400327-918a9446-8c4b-42c8-874c-7dc72bb8d1a6.png)

* 輸入剛在ubuntu找到的IP，並點選[立即更新]

![螢幕擷取畫面 2022-06-07 220828](https://user-images.githubusercontent.com/106873001/172402466-d2ea19d2-fede-471d-9f61-8904e2043237.png)

會顯示同步成功，代表著windows連接上ubuntu的網路時間

![螢幕擷取畫面 2022-06-07 220921](https://user-images.githubusercontent.com/106873001/172404162-7361ccf4-f60d-4f49-8779-00bb6dd491ed.png)


-以下為建立server端


* 修改組態檔
  
 ```shell
 sudo nano /etc/ntp.conf
 ```
 - pool組態前面用[#]註解掉，並加上中華電信提供的台灣標準時間的網址(https://www.stdtime.gov.tw/chinese/bulletin/NTP%20promo.txt)，網址五擇一即可
 
 ![image](https://user-images.githubusercontent.com/106873001/172410136-0d8a56a6-7666-4179-aa77-2f0f73141df1.png)


* 重啟伺服器
```shell
sudo service ntp restart    
```


## 實作二 : 設定其他時區
