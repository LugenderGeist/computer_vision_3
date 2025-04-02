# computer_vision_3
Целью данной работы является поиск движещуегося объекта на видео при неподвижной камере. Необходимо:
- Обработать видео с целью лучшего распознавания объекта
- Создать маску фона
- Наложить маску на каждый кадр и выделить движущийся объект
- Выделить движущийся объект рамкой
  
В данной работе будет использоваться следующее видео:
![first](https://github.com/LugenderGeist/computer_vision_3/blob/main/clear.gif)  
## Поиск объекта  
Для работы с видео будем использовать встроенные в библиотеку open CV функции. Для предварительной обоработки кадров имеет смысл пользоваться функциями:
- *cv2.MORPH_OPEN* - использование морфологических операций, эрозии и последующей дилатации. Так как в нашем случае объект темне фона - будет использовать этот вариант.
- *cv2.MORPH_CLOSE* - использование морфологических операций, дилатации и последующей эрозии. Пригодилось бы, если бы объект был светлее фона.
- *cv2.GaussianBlur* - фильтр Гаусса, использующийся для размывания мелких деталей, неважных для задачи. Поможет в случае наличия шумов, влияющих на обработку.
 
Для отоборажения результатов определения объекта необходимо создать новое видео, собранное из полученных кадров. Для этого воспользуемся функциями:
- *cv2.VideoCapture* для считывания видео с файла.
- *cv2.VideoWriter_fourcc* для создания кодека для записи видео. Кодек определяет формат сжатия видео, который будет использоваться при записи
- *cv2.VideoWriter* для записи видео из последовательности кадров.

Чтобы выделить движущийся объект - нужно создать маску неподвижного фона. Для этого используется функция *cv2.createBackgroundSubtractorMOG2* - анализируется несколько кадров, для каждого из которых для каждого пикселя опрелеяется распределение значений интенсивности. Пиксели, у которых значения интенсивности не изменяются со временем, становятся частью фона.  
Для этой функции важны три параметра:
- *history* - определяет число кадров для построения модели фона
- *varThreshold* - определяет порог чувствительности для определения пикселя как часть фона. Чем выше значение, тем меньше чувствительность (меньше пикселей будет считаться объектом).
- *detectShadows* - проверяет, насколько яркость пикселей текущего кадра отличается от модели фона. Тени обычно имеют меньшую яркость по сравнению с фоном, но их цвет остается близким к цвету фона. В данном случае у объекта нет тени, но за шариком движутся преломленные лучи, более светлые, чем шарик. Поэтому необходимо определить, поможет ли эта настройка в определени объекта.

Для наложения созданной маски используется функция:
- *cv2.bitwise_and* - сравнивает два изображения пиксель за пикселем. Она оставляет только те пиксели, которые "совпадают" в обоих изображениях. Если пиксель есть в одном изображении, но отсутствует в другом, он будет удален.  
![second](https://github.com/LugenderGeist/computer_vision_3/blob/main/grayscale.gif)  
## Выделение объекта  
После того, как объект определяется достаточно хорошо можно перейти к выделению его рамкой. Для этого также воспользуемся встроенными функциями:
- *cv2.findContours* - 
- *cv2.contourArea* - 
- *cv2.boundingRect* - 
- *cv2.rectangle* -

![third](https://github.com/LugenderGeist/computer_vision_3/blob/main/result.gif)  
