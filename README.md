# 臺灣各級行政區域 GeoJSON

---

如果需要自己重畫行政區域地圖的步驟：
1. 安裝 [mapshaper](https://github.com/mbloch/mapshaper)： 
``` bash=
apt-get install npm
npm install -g mapshaper
```

2. 安裝 json 轉檔用套件 jq： <br> [jq 教學](https://newtoypia.blogspot.com/2015/03/json-jq.html)
``` bash=
apt-get install jq
```

3. 將「政府資料開放平台-鄉鎮市區界線」的壓縮檔下載下來 <br> 透過 ogr2ogr or 線上工具把檔案轉成 GeoJSON


4. 最後使用 jq 篩選出各地區資料，並使用 mapshaper 簡化地圖資料，輸出 GeoJSON ，以新北市為例
``` bash=
jq '.features = (.features | map(select(.properties.COUNTYNAME=="新北市")))' TOWN_MOI_1100415.json | mapshaper - -simplify 10% -o - > Taiwan_New_Taipei_City.geo.json
```

---

資料來源：https://data.gov.tw/dataset/7441

參考資料：https://newtoypia.blogspot.com/2015/08/admin-boundary.html


