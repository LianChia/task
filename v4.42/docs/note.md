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

### 使用Optuna來優化參數  
結合閾值並調整kernel_size、iterations的範圍縮小  
新增CLAHE（自適應直方圖均衡化）、邊緣檢測    
最佳參數:  {'kernel_shape': 'ellipse', 'kernel_size': 19, 'iterations': 2, 'flood_fill': False, 'multi_stage': False, 'apply_blur': True, 'edge_detection': False, 'apply_clahe': False}  
最佳參數計算的平均 IOU:  0.8359075306711994

# 以下兩項不採用

### 使用 Optuna + 尋找閾值(1)
最佳參數:  {'kernel_shape': 'ellipse', 'kernel_size': 17, 'iterations': 20, 'flood_fill': False, 'multi_stage': True}  
最佳 IOU:  0.8577816747158178  
平均 IOU (使用最佳參數):  0.7283899739583333  

### 使用 Optuna + 尋找閾值 + 高斯模糊、邊緣檢測(2)
最佳參數:  {'kernel_shape': 'circle', 'kernel_size': 11, 'iterations': 19, 'flood_fill': False, 'multi_stage': True, 'apply_blur': True, 'edge_detection': False}
最佳 IOU:  0.8579678311681096  
平均 IOU (使用最佳參數):  0.7659951934394204

---10/18---
### 問題解決(1)
最佳參數:  {'kernel_shape': 'ellipse', 'kernel_size': 7, 'iterations': 17, 'flood_fill': False, 'multi_stage': False}  
最佳 IOU:  0.9284324550400342  
平均 IOU (使用最佳參數):  0.8471935556788613  

### 問題解決(2) 額外增加直方圖均衡化
最佳參數:  {'kernel_shape': 'rect', 'kernel_size': 11, 'iterations': 11, 'flood_fill': False, 'multi_stage': True, 'apply_canny': False, 'apply_gaussian_blur': True, 'apply_clahe': True}  
最佳 IOU:  0.9281206257158015  
平均 IOU (使用最佳參數):  0.8650807773690715  

平均 IoU 計算的錯誤:  
問題: 最初的程式碼中，average_iou_b = calculate_average_iou(best_params_b) 使用了未定義的函數 calculate_average_iou，這會導致錯誤。  
解決方案: 修改為直接計算平均 IoU，將最佳參數應用於所有圖片，然後計算其 IoU。  
groundtruth_files 未定義:  
問題: 在處理完 Optuna 優化後，計算平均 IoU 時，groundtruth_files 變數未被定義，導致程式執行出錯。  
解決方案: 在計算平均 IoU 的部分，重新定義了 groundtruth_files，確保它在使用前已正確讀取。  
驗證集的 IOU 計算:  
問題: 在最初程式碼中，沒有進行驗證集的 IOU 計算，這可能導致過度擬合的問題。  
解決方案: 添加了訓練集和驗證集的分割，以及對每個集計算其 IoU，這有助於評估模型的泛化能力。  
重複讀取圖片:  
問題: 在最初的程式碼中，可能重複讀取同一張圖片進行處理，增加了計算的冗餘。  
解決方案: 將讀取圖片的邏輯提取到單獨的迴圈中，使其在計算平均 IoU 時不會重複讀取。  

### 同問題(2)增加交叉驗證並加快計算速度
最佳參數:  {'kernel_shape': 'ellipse', 'kernel_size': 13, 'iterations': 9, 'flood_fill': False, 'multi_stage': True, 'apply_canny': False, 'apply_gaussian_blur': False, 'apply_clahe': True}  
最佳 IOU:  0.9256446822633648  
平均 IOU (使用最佳參數):  0.8477866754730468  


---10/21---  
數據增加至300張  
300-Mask未處理：  
平均 IoU: 0.7646949307574317  

img-Mask未處理：  
使用Optuna：  
最佳參數:  {'kernel_shape': 'rect', 'kernel_size': 30, 'iterations': 9, 'flood_fill': True, 'multi_stage': False, 'apply_canny': True, 'apply_gaussian_blur': True, 'apply_clahe': False}  
最佳 IOU:  0.8017575954861108  
平均 IOU (使用最佳參數):  0.7434252577039933  

---10/22---  
數據減少至100張  
300-Mask未處理：  
平均 IoU: 0.7784320308551098  

300-Mask處理後：  
平均 IoU: 0.7912775269332354







---10/28---  
最初實驗
使用自適應門檻  
混淆矩陣:
[[ 2468596 16171209]
 [ 9351374 94888821]]
準確率 (Accuracy): 79.23%
精確率 (Precision): 85.44%
召回率 (Recall): 91.03%
F1 分數 (F1 Score): 88.15%

使用optuna去找自適應門檻(10)  
最佳 F1 分數: 99.44%  

[I 2024-10-28 16:46:23,477] Trial 6 finished with value: 99.44308260210258 and parameters: {'block_size': 3, 'C': 5}. Best is trial 6 with value: 99.44308260210258.  
混淆矩陣:  
[[    16611    854097]  
 [   506819 121502473]]  
準確率 (Accuracy): 98.89%  
精確率 (Precision): 99.30%  
召回率 (Recall): 99.58%  
F1 分數 (F1 Score): 99.44%  