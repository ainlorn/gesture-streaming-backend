# SLT-EKB

####
Репозитарий создан для участников хакатона "Код города 300. ЧитAI жесты" в части задачи "Разработка сервисов для слабослышащих людей"

## Задача:
Разработать идею и концепцию применения модели машинного обучения SLT2TEXT для распознавания жестов русского жестового языка.
В рамках задачи участникам предоставляется модель SLT2TEXT, которая преобразует видеопоток/файл с жестами в текст.
Участникам необходимо придумать сервис (приложение для телефона, веб сайт, прочее) направленный на решение одного из следующих вопросов:
- проблемы комуникации слабослышаших людей в повседневной жизни;
- досуг и развлечения;
- образование;
- прочее.

Как пример, сервис-тренажер для изучения жестового языка, сурдопереводчик, видео игры с активным использованием жестового языка и тд.

## Критерии оценивания
Оценка решний будет производиться членами жюри по 4 направлениям:
- Идея, возможность её реализации, потенциальная польза, перкспективность монетизации, затраты на разработку. Должны быть раскрыты следующие темы: какую потребность закрывает (насколько это важно), какая целевая аудитория и её охват, ресурсы на реализацию

- Техническая реализация (веб-демо, приложение или что-то другое), проработка архитектуры, выбранный технический стек, производительность решения, возможности масштабирования

- Презентация (структурная составляющая: качество слайдов, дизайн, структура презентации и т.п.)

- Выступление (оценка выступления спикера/спикеров, взаимодействие с аудиторией, ответы на вопросы жюри)

В рамках каждого критерия оценка будет производиться по 5-балльной системе от 0 до 4, где 4 является максимально возможной
оценкой, а 0 - минимально возможной.

| **Баллы**  | **Оценка идеи (за идею даются двойные баллы)**                                                                    | **Оценка продукта**                                                                                     | **Внешний вид и юзабилити**                              | **Презентация и навыки публичного выступления**                                        |
|:----------:|-------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------------------------------------------------------|
| **4**      | Идея решения соответствует потребностям, хорошо проработана и закрывает потребности широкой аудитории             | Результат соответствует критериям успешного решения задачи и значительно превосходит ожидания заказчика | Интерфейс понятен, удобен                                | Презентация высокого качества, уложились в тайминг, полностью раскрывает идею продукта |
| **3**      | Идея решения соответствует потребностям, но не расчитана на широкую аудиторию и требует дополнительной проработки | Результат соответствует критериям успешного решения задачи и устраивает заказчика                       | Интерфейс понятен, удобен, но реализован с ограничениями | Презентация имеет незначительные замечания, в большей мере раскрывает идею продукта    |
| **2**      | Идея решения соответствует потребностям, но плохо проработана, не закрывает потребности широкой аудитории         | Результат частично соответствует критериям успешного решения задачи                                     | Интерфейс непонятен                                      | Презентация понятна, но сделана плохо или команда не уложилась в тайминг               |
| **1**      | Идея решения не соответствует потребностям                                                                        | Результат не соответствует критериям успешного решения задачи                                           | Есть критичные замечания                                 | Презентация не раскрывает продукт, непонятна                                          |
| **0**      | Идея непонятна                                                                                                    | Результата нет                                                                                          | Отсутствует внешний вид продукта                         | Презентация не подготовлена                                                            |


## Ограничения стека
- ограничений стека нет


## Необходимая техника
- любой ноутбук

## Использование модели SLT2TEXT
- Клонировать данный репозиторий;
- Установить необходимые зависимости:
```python
  cd code
  pip install -r requirements.txt
``` 
- Cкачать модель по распознаванию жестов: https://sc.link/BNnGk, поместить её в папку с проектом.
- (Опционально) Скачать примеры видео с Русским жестовым языком https://sc.link/BQ . Их можно использовать для отладки модели в режиме 
распознавания видео или выучить несколько жестов и показывать их на камеру.

Также в данном репозитории находится докер образ с уже установленными зависимостями и моделью распознавания.   
! Использование докер-контейнера не позволит использовать видео с камеры для распознавания жестов.

### Примеры работы с моделью SLT2TEXT
Мы предлагаем 2 способа использовать модель:
- Расшифровка видео с камеры в онлайн режиме.  
```python
  python webcam_demo.py
``` 
Основные параметры скрипта (подробнее - в коде в **webcam_demo.py**):
```python
  --threshold - степень уверенности модели в распознанном жесте. Чем выше значение, тем меньше ложных срабатываний.
  --device - на каком устройстве запускать модель. По умолчанию использется 'cpu'
``` 

- Расшифровка видеофайла.
В модель подаётся один или несколько видеофайлов, на выходе - распознанные моделью жесты. 
```python
  python video_demo.py -c config.json demo.mp4

  config.json - конфигурационный файл
  demo.mp4 - видеофайл для расшифровки
``` 
Основные параметры конфигурационного файла:
```python
  --model - путь до используемой модели
  --threshold - степень уверенности модели в распознанном жесте. Чем выше значение, тем меньше ложных срабатываний.
  --topk - количество прогнозов модели на один семпл по убыванию степени уверенности модели.
``` 


## Использование докер-файла
    При желании использовать докер, можно воспользоваться докерфайлом из данного репозитория: 
        -  docker build -t slt_ekb:1.0 .
        -  docker run -v "Path_to_file\filename.mp4:/app/filename.mp4" slt_ekb:1.0 "app/filename.mp4"
    Проброс видеопотока с камеры внуть контейнера не реализован. 
