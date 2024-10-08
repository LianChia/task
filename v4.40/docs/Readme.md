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
1. 使用model2並按照第一步來取出Alveolar_bone
2. 設定保護遮罩  
##  後處理  
把推理圖片(AI)以及保護遮罩(dentin)、保護遮罩(Alveolar_bone)堆疊，但產出圖片中間還是有缺點，所以後續進行顏色調整再疊回推理圖片(AI)上

# Task2
## 上色
先導入圖片與標籤來重新上色

## 平均IOU