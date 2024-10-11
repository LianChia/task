# Task1
## 取出牙本質dentin
目的是為了不讓牙本質被覆蓋掉，所以需要先取出dentin再將其用保護遮罩遮住
1. 使用model1以及model2來取出dentin  
    以下是model1以及model2的標籤  
    Model 1 Labels (Classes):  
    {0: 'Dentin', 1: 'Maxillary_sinus', 2: 'Background'}

    Model 2 Labels (Classes):  
    {0: 'Alveolar_bone', 1: 'Caries', 2: 'Crown', 3: 'Dentin', 4: 'Enamel', 5: 'Implant', 6: 'Mandibular_alveolar_nerve', 7: 'Maxillary_sinus', 8: 'Periapical_lesion', 9: 'Post_and_core', 10: 'Pulp', 11: 'Restoration', 12: 'Root_canal_filling', 13: 'Background'}  
    主要需要model1的 "Dentin"以及model2的"Enamel"、 "Caries"
2. 設定保護遮罩  
## 取出牙齦Alveolar_bone
目的是補足後處理時的不完整
1. 使用model2並按照第一步來取出Alveolar_bone。
2. 設定保護遮罩。
##  後處理  
把推理圖片(AI)以及保護遮罩(dentin)、保護遮罩(Alveolar_bone)堆疊，但產出圖片中間還是有缺點，所以後續進行顏色調整再疊回推理圖片(AI)上。

# Task2
## 上色
先導入圖片與標籤來重新上色。

## 平均IOU
1. 取300資料夾的遮罩  
    之前展夆的code(spilt_mask.py)會把color_1.png分離不同的牙齦、牙齒、牙冠和象牙質區域並儲存起來，修改code變成不會分離並合併在一起。  
2. 取目前圖片的遮罩  
再回到(postprocessing_background_mask.ipynb)利用.png、.npy、.json檔來取得目前圖片的遮罩。  
3. 計算個別平均IOU  
    300-IOU ：平均 IoU: 0.7460267282351231  
    目前圖片：平均 IoU: 0.5036748092774207  
    10/09
4. 1011更新
   將真實集彩色圖片轉成黑白圖後尋找最佳閥值來進行最佳IOU計算
