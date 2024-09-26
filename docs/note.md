# Task 1

## 觀察 100 張圖片  
1. 填色不完全：100%
2. 填色溢出：87% 
3. 異常填色：57%  

## 想法  
原先想法是使用侵蝕與膨脹現象去做處理，但發現單獨使用侵蝕與膨脹，效果不佳；因此改為使用開閉運算。  
目前正在研究 GitHub 上的程式碼 (postprocessing_background_mask.ipynb)。  

## 問題
填色不完全與異常填色的部分還是沒有改善，但溢出的部分有改進。