1. 需先在環境內部署 Docker
   
2. 一鍵部署與執行 Juice Shop 靶機 <br>
  - sudo docker run -d -p 3000:3000 --name juice-shop bkimminich/juice-shop

3. 在實體電腦瀏覽器輸入：http://IP:<Host_Port> <br>
 - 成功後，將看到 Juice Shop 的首頁
<br>
<br>

停止環境
 - docker stop juice-shop
<br>

再次啟動
 - docker start juice-shop 
