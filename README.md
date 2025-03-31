# computer_vision_3
Отслеживание движущегося объекта на видео
## Принцип поиска объекта  
![first]([https://github.com/LugenderGeist/computer_vision_1/blob/main/scream.jpg](https://github.com/LugenderGeist/computer_vision_3/blob/main/clear.gif))
Для поиска объекта в данной работе применяются встроенные в библиотеку open CV функции.

Для отоборажения результатов необходимо создать новое видео, собранное из полученных кадров. Для этого воспользуемся функциями:
- cv2.VideoCapture
- cv2.VideoWriter_fourcc
- cv2.VideoWriter

Для предварительной обоработки кадров имеет смысл пользоваться функциями cv2.MORPH_OPEN, cv2.MORPH_CLOSE, cv2.GaussianBlur.  

Для решения одной из основных задач, для определения фона, используется функция cv2.createBackgroundSubtractorMOG2: 

Для наложения созданной маски используется функция cv2.bitwise_and:  
  
![second]([https://github.com/LugenderGeist/computer_vision_1/blob/main/scream.jpg](https://github.com/LugenderGeist/computer_vision_3/blob/main/grayscale.gif))
После того, как объект определяется достаточно хорошо можно перейти к выделению его рамкой. Для этого также воспользуемся встроенными функциями 
- cv2.findContours
- cv2.contourArea
- cv2.boundingRect
- cv2.rectangle
  
![third]([https://github.com/LugenderGeist/computer_vision_1/blob/main/scream.jpg](https://github.com/LugenderGeist/computer_vision_3/blob/main/result.gif))
