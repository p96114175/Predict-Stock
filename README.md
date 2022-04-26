# Predict-Stock P96114175
  
# Model & Methods

一開始先分析了 Close price & Open price，後來發現兩個間數據差異不大

因此訓練時挑選其中一個Close price as feature，並應用預測時間序列資料模型 LSTM 進行訓練。

由於最後結果須輸出20天預測，因此在訓練時我們將train data 以20天為一份進行訓練

預測結果如圖:

  ![image](https://user-images.githubusercontent.com/102530486/165242516-04f4bf9a-f355-4cc3-86ad-9cb038b0f617.png)

# Install
    pip install -r requirements.txt
# Run the code

將trader.py、training.csv、testing testing.csv、output.csv載下後(需在同資料夾內)

    python app.py --training training.csv --testing testing.csv --output output.csv
    
# Maket Strategy
  定義出以下四種變數作為後續邏輯判斷之依據
  
  ▶ buy_price  
  ▶ current_holding_stock    
  ▶ last_day_price    
  ▶ action 
  
  以current_holding_stock(目前持有股票數)來說，可分成三種狀態，分別為1(持有一張)、0(未持有)、-1(持有負一 張)，接著分別以各自碰見的情況進行判斷。
  
    If current_holding_stock(目前持有股票數) = 1:
      If 未來預測價格 > 買進價格
        action(採取行動) = -1(賣出)
      else:
        action(採取行動) =  0(不採取行動)
    elif current_holding_stock(目前持有股票數) = 0:
      If 未來預測價格 < 前一天價格
        action(採取行動) = 1(買進)
      elif 未來預測價格 > 前一天價格
        action(採取行動) = -1(賣出)
      else:
        action(採取行動) =  0(不採取行動)  
    elif current_holding_stock(目前持有股票數) = -1:
      If 未來預測價格 < 買進價格
        action(採取行動) = 1(買進)
      else:
        action(採取行動) =  0(不採取行動)
    
