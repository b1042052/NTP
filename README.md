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
![螢幕擷取畫面 2022-06-07 212950](https://user-images.githubusercontent.com/106873001/172393551-499f23d1-ba35-445b-a7f1-e296f4f9fa3b.png)

   內部網路應為[192.168.x.x]
  
  
 * 下載NTP
 ```shell
 sudo apt-get install ntp
 ```
 

    



## 實作二 : 設定其他時區
