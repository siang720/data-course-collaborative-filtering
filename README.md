# Data course - Collaborative filtering

### 專案目的
建立一個推薦系統，推薦商品給曾經在Mimi Beauty網站上購買過美妝商品的客戶。

### 執行方式
透過分析美妝產品資料(product data)、用戶評分資料(review data)，設計推薦邏輯，推薦商品給客戶。

### 資料切割方式
* Training data：日期在2018-09-01之前的用戶評分資料。
* Testing data：日期介於2018-09-01及2018-09-30的用戶評分資料。

### 推薦邏輯
使用Collaborative filtering演算法，包含手刻user-based、手刻item-based、使用套件surprise，計算出similarity matrix之後，給予推薦商品。

#### User-based
利用客戶在training data中的評價紀錄，計算出similarity matrix，針對目標客戶找出相似的使用者，再從這些使用者曾經購買過的商品之中，挑選出評價較高且沒有被目標客戶購買過的商品，推薦給目標客戶。

#### item-based
同樣是利用客戶在training data中的評價紀錄，計算出item之間的similarity matrix，針對目標客戶曾經購買過的商品，找出較相似的商品，推薦給目標客戶。

#### surprise套件
運用surprise套件來取代手刻計算，這次使用item-based的方式，觀察是否與手刻計算有同樣的結果。

### 使用工具及平台
Python, Colab

### 推薦結果

#### User-based：Recall = 0
由於584位目標客戶之中，只有38位在training data中有購買紀錄，所以只能針對這38位給予推薦，命中機率下降許多。
嘗試用不同參數去篩選用來計算similarity matrix的users，包含：
* 推薦商品數k：10、20、30
* 使用者評價篩選下限：至少2筆評價、至少3筆評價、完全不篩選。

不過各種參數組合recall皆為0，推測應該是新使用者較多所導致。

#### Item-based：Recall = 0.169
透過調整training data的起始日，發現最高可以獲得0.169的Recall，起始日在2018-04-01~2018-05-14之間都可以獲得0.169的recall。

#### Surprise套件：Recall與手刻相同
這次使用surprise中item-based的算法來與手刻的item-based比較，發現結論與上述相同。不過套件可以用更快速的方式完成計算。
