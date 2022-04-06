# y-vector

Статья, на основе которой сделано задание: https://www.isca-speech.org/archive/pdfs/interspeech_2021/zhu21b_interspeech.pdf. В статье описывается построение векторного представления (эмбеддингов) на сырых аудио данных (.wav).

Отличительной особенностью y-векторов от других подходов, основанных на извлечении признаков из сырых данных (например, таких как wav2vec), является то, что в данном случае используются три паралелльных канала со свёртками с разными ядрами, выполняющих функции фильтров разных частот. После свёрток по каналам  происходит частотное и временное сжатие-расширение в трёх последующих блоках. Для повышения точности происходит объединение карт признаков с различных слоёв для каждого фрейма данных.


Выбранный датасет для экспериментов - VCTK (https://datashare.ed.ac.uk/handle/10283/2950). VCTK включает в себя речевые данные, произнесенные 109 носителями английского языка с различными акцентами. В данном случае решалась задача идентификации, то есть классификация на 109 классов. При этом в исходной статье про y-вектора рассматривалась задача верификации, поэтому полученные результаты сравнивались с результатами из статьи про VCTK датасете
Статья по VCTK: https://www.researchgate.net/publication/320280030_Dilated_Recurrent_Neural_Networks. 
В данной статье в качетстве метрики использовалась accuracy:
MFCC+GRU                   - 0.77
сырые данные + Dilited GRU - 0.74
сырые данные + Fused GRU   - 0.65

**параметры обучения:**
  - эпохи - 2
  - шаг обучения - 0.0001
  - батч - 64
  - функция потерь - CrossEntropyLoss
  - длина входящего фрагмента - 3.5с
Если входящий файл меньше 3.5с, то он дополняется до длины в 3.5с самим собой.

При разбиении данных 80/20 на валидационном множестве accuracy составляет 0.96. 

