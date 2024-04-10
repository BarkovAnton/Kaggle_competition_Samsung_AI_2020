# Kaggle competition in 2020 (Samsung AI Center)

## Cleaned vs Dirty V2
Classify if a plate is cleaned or dirty?
https://www.kaggle.com/c/platesv2/overview

### Список применяемых аугментаций:
     - center_crop = img вырезается из центра исходника, size = (224,224) 
     - resize     = исходник сжимается до size = (224,224) 
     - Hflip       = горизонтальное отзеркаливание  
     - Vflip       = вертикальное отзеркаливание  
     - canny       = применение детектора Canny с наложением на img полученных граней 

 ### Состав train датасета (128 img):
      [0] 16 dirty img + 16 cleaned img, аугментации - center_crop, canny                                      
      [1] 16 dirty img + 16 cleaned img, аугментации - center_crop, Hflip, canny
      [2] 16 dirty img + 16 cleaned img, аугментации - center_crop, Vflip, canny
      [3] 16 dirty img + 16 cleaned img, аугментации - center_crop
                                       
 ### Состав val датасета (8 img):
      [0] 4 dirty img + 4 cleaned img, аугментации - resize, canny

batch_size принят равным 4.  Итоговый размер train_dataloader - 32 батча из 128 img

Получение наилучшего результата заключалось в выборе best_model путем перебора 10-и seed'ов и 
сравниванием значений loss и acc для каждой обученной модели. 
Чем выше acc и меньше loss (для моделей с одинаковым acc), тем предпочтительней модель.

Полученные графики по acc и loss в папке /graphics_acc_loss

Примеры img с примененными аугментациями в папке /img_example

Возможно после 23 эпохи идет небольшое переобучение, хотя снижение количества эпох дало меньшую accuracy

### Модель в формате .sav решает задачу с accuracy 0.96370
