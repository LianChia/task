# 優化並計算平均IOU
## 300
### 未使用Optuna
遮罩處理前的IOU：  
平均 IoU: 0.8114603760004598
  
遮罩處理後的IOU：   
平均 IoU: 0.8066555201004715  

### 使用Optuna
遮罩處理前的IOU：  
A組最佳參數:  {'kernel_shape': 'ellipse', 'kernel_size': 7, 'iterations': 5, 'flood_fill': True, 'multi_stage': True}  
A組最佳 IOU:  0.813315729320885  
A組平均 IOU:  0.8038650172968524  
  
遮罩處理後的IOU：  
B組最佳參數:  {'kernel_shape': 'ellipse', 'kernel_size': 5, 'iterations': 9, 'flood_fill': True, 'multi_stage': True}  
B組最佳 IOU:  0.8066855113131804  
B組平均 IOU (使用最佳參數):  0.8066855113131804  

### 使用 Optuna + 尋找閾值
B組最佳參數:  {'kernel_shape': 'ellipse', 'kernel_size': 19, 'iterations': 2, 'flood_fill': True, 'multi_stage': True}  
B組最佳 IOU:  0.8066795317744591  

### 使用 Optuna + 尋找閾值 + 高斯模糊、邊緣檢測
B組最佳參數:  {'kernel_shape': 'ellipse', 'kernel_size': 7, 'iterations': 5, 'flood_fill': False, 'multi_stage': False, 'apply_blur': True, 'edge_detection': False}  
B組最佳 IOU:  0.8073309211250995  
B組平均 IOU (使用最佳參數):  0.8066786239040766  

## img
### 未使用Optuna
平均 IoU: 0.8350125762942182

### 使用Optuna
最佳參數:  {'kernel_shape': 'ellipse', 'kernel_size': 17, 'iterations': 20, 'flood_fill': False, 'multi_stage': True}  
最佳 IOU:  0.8577800583498668  
平均 IOU:  0.8096051453554824  

# 以下不採用

### 使用 Optuna + 尋找閾值
最佳參數:  {'kernel_shape': 'ellipse', 'kernel_size': 17, 'iterations': 20, 'flood_fill': False, 'multi_stage': True}  
最佳 IOU:  0.8577816747158178  
平均 IOU (使用最佳參數):  0.7283899739583333  

### 使用 Optuna + 尋找閾值 + 高斯模糊、邊緣檢測
最佳參數:  {'kernel_shape': 'circle', 'kernel_size': 11, 'iterations': 19, 'flood_fill': False, 'multi_stage': True, 'apply_blur': True, 'edge_detection': False}
最佳 IOU:  0.8579678311681096
平均 IOU (使用最佳參數):  0.7659951934394204