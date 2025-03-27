# Naruto Character Recognition with PyTorch 🌀

Этот проект — практическая реализация нейронной сети для распознавания персонажей из аниме "Наруто" с использованием PyTorch 🔥. Мы обучаем модель классифицировать лица героев, таких как Наруто, Саске и Сакура, на основе датасета с изображениями 📸.

## Описание 📝

Проект включает:
1. Подготовку данных 🛠️ (загрузка, разбиение на train/test).
2. Создание кастомного датасета и загрузчика с `torch.utils.data` 📦.
3. Простую полносвязную нейронную сеть 🧠.
4. Обучение и оценку модели 📈.
5. Визуализацию ошибок и матрицу ошибок 🎨.

Датасет содержит изображения 13 персонажей "Наруто" с аннотациями в `train.csv` и `test.csv`.

## Требования ⚙️

- Python 3.7+ 🐍
- PyTorch 🔥
- Torchvision 🌟
- NumPy 🔢
- Pandas 🐼
- OpenCV (cv2) 📷
- Matplotlib 🎨
- Seaborn 📊
- TQDM ⏳


Пошаговое решение задачи 🛤️
Вот что происходит в коде для решения задачи классификации:

### Подготовка данных 📦
* Загружаем аннотации из train.csv и test.csv с помощью Pandas 🐼.
* Создаем кастомный класс FaceDataset, наследуемый от torch.utils.data.Dataset 📏.
* Применяем преобразования (transforms): уменьшаем изображения до 64x64, преобразуем в тензоры и нормализуем 🌟.
* Создаем DataLoader для батчевой обработки данных (batch_size=64) 🚚.

### Создание нейронной сети 🧠
* Определяем простую полносвязную сеть CoolEasyNet с несколькими слоями 🌐.
* Входной размер: 3x64x64 (RGB-изображения), выходной — 13 классов (персонажей) 🎯.
* Переносим модель на GPU для ускорения (model.cuda()) ⚡.

### Обучение модели 📚
* Используем функцию потерь CrossEntropyLoss и оптимизатор SGD (lr=0.01, momentum=0.9) 🔧.
* Пишем функцию train_net для обучения в течение 10 эпох:
* Прогоняем батчи через сеть ➡️.
* Считаем лосс и обновляем веса с помощью градиентного спуска 🔄.
* Логируем лосс и точность для train и test 🖥️.

### Оценка модели ✅
* Пишем функцию evaluate_net для тестирования на тестовой выборке 📊.
* Считаем средний лосс и точность (accuracy) на тесте 📈.
* Получаем предсказания с помощью get_preds и строим матрицу ошибок с confusion_matrix 🎨.

### Анализ результатов 🔍
* Визуализируем матрицу ошибок (confusion matrix) с помощью Seaborn 📉.
* Показываем примеры ошибок классификации с функцией vis_mistakes (до 4 изображений) 🖼️.
* Сортируем ошибки по уверенности модели (score) для анализа 🤔.


В данном проекте используется функция softmax в коде для получения вероятностей предсказаний модели в функции get_preds.
В Computer Vision дойти до 80% довольно просто, для получения 95% - нужно больше поизучать

* Больше слоёв, количество нейронов
* Можно взять картинки больше
* Взять разрешение меньше - не будет лишних деталей
* Можно учить дольше - long training всегда приносит отличные результаты
* Можно использовать OpenCV для создания синтетических данных ( синтетические данные могут не полностью замещать реальные номера, нельзя обучаться только на синтетике, нужны и реальные номера, важно использовать плюс к синтетическим изображениям - генеративные модели, чтобы одна сеть говорила - что на реальный, например автомобильный номер, при решении задачи распознавания автомобильных номеров, не похоже)
* Аугментация данных, флипать, поворачивать, цветовую гамму менять, чтобы сеть тренировалась справляться с трудностями - чтобы она становилась лучше и
лучше решала задачи, которые мы перед ней ставим

Дальнейшее изучение: 
Свёрточные Нейронные сети, Трансформеры
