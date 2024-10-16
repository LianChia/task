# 優化並計算平均IOU
## 未使用Optuna
遮罩處理前的IOU：  
平均 IoU: 0.9988908774589454
  
遮罩處理後的IOU：   
平均 IoU: 0.9793180381450941  

## 使用Optuna
遮罩處理前的IOU：  
最佳參數:  {'kernel_shape': 'rect', 'kernel_size': 29, 'iterations': 10, 'flood_fill': False}  
最佳 IOU:  0.9830615234375001  
平均 IOU:  0.9567515803747362  
  
遮罩處理後的IOU：  
最佳參數:  {'kernel_shape': 'rect', 'kernel_size': 30, 'iterations': 9, 'flood_fill': False}  
最佳 IOU:  0.9830615234375001  
平均 IOU:  0.9604628703569215  
