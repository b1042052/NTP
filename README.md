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

* 輸入剛在ubuntu找到的IP，點選[立即更新]

![螢幕擷取畫面 2022-06-07 220828](https://user-images.githubusercontent.com/106873001/172402466-d2ea19d2-fede-471d-9f61-8904e2043237.png)

顯示同步成功，代表著windows連接上ubuntu的網路時間

![螢幕擷取畫面 2022-06-07 220921](https://user-images.githubusercontent.com/106873001/172404162-7361ccf4-f60d-4f49-8779-00bb6dd491ed.png)


-以下為建立server端


* 修改組態檔
  
 ```shell
 sudo nano /etc/ntp.conf
 ```
 - pool組態前面用[#]註解掉，並加上中華電信提供的台灣標準時間的網址，網址五擇一即可 (https://www.stdtime.gov.tw/chinese/bulletin/NTP%20promo.txt)
   
   server 網址 iburst
 
 ![image](https://user-images.githubusercontent.com/106873001/172410136-0d8a56a6-7666-4179-aa77-2f0f73141df1.png)


* 重啟伺服器
```shell
sudo service ntp restart    
```

* 確認是否連連接成功
```shell
sudo ntpd -pn
```

 [ * ]代表正在使用
 
![螢幕擷取畫面 2022-06-08 012100](https://user-images.githubusercontent.com/106873001/172444480-ee57f946-adf4-4fe1-bae7-c2a6cd26d761.png)



-以下為建立client端

* 建立另一台虛擬機

* 將網路設定成[橋接介面卡]

* 下載NTPDATE

```shell
sudo apt-get install ntpdate
```

* 把client端的時間調亂

  - ubuntu點選右上角有個[設定值]
  
![172440055-f4b2e26c-3047-437a-b507-2ada08885b96](https://user-images.githubusercontent.com/106873001/172441249-0fc6ac60-87d0-4ba3-98b1-be7416e1e8e5.png)


  - 選擇[日期與時刻]，並打亂時間
![螢幕擷取畫面 2022-06-08 010043](https://user-images.githubusercontent.com/106873001/172440625-6d60276a-4e17-4941-ae0c-ddb4c1c3ea23.png)

* 連接server端時間

```shell
sudo ntpdate [server IP]
```
此為連接成功，且時間也從被調亂變回正常時間
![螢幕擷取畫面 2022-06-08 012800](https://user-images.githubusercontent.com/106873001/172445958-a0d2a011-0228-4328-99a9-138edf978f9a.png)

畫線處為已成功與server端同步，並顯示server端的IP



## 實作二 : server端設定其他時區

* 查看其他時區表
```shell
timedatectl list-timezones
```

![image](https://user-images.githubusercontent.com/106873001/172449644-caabe4c0-a1c7-45e4-9c18-f85cab8343fd.png)


* 更改時區
```shell
sudo timedatectl set-timezone [你選擇的時區]
```
時間已成功更改成當地時區

![image](https://user-images.githubusercontent.com/106873001/172450395-1cd8eb23-d72a-46de-a41f-5c7f218e07b1.png)

接下來只要讓剛才client端連接，client端也會與server端同步時間

```shell
sudo ntpdate [server IP]
```
