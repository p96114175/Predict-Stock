# Predict-Stock
  1554
# Install
    pip install -r requirements.txt
# Implement
    python app.py --training training.csv --testing testing.csv --output output.csv
    
# Action
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
      If 未來預測價格 < 買進價格
        action(採取行動) = 1(買進)
      elif 未來預測價格 > 買進價格
        action(採取行動) = -1(賣出)
      else:
        action(採取行動) =  0(不採取行動)  
    elif current_holding_stock(目前持有股票數) = -1:
      If 未來預測價格 < 買進價格
        action(採取行動) = 1(買進)
      else:
        action(採取行動) =  0(不採取行動)
    
