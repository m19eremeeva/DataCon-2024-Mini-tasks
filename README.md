# DataCon-2024-Mini-tasks
Этот репозиторий содержит исходные данные и задания для участников DataCon-2024
Для удобства работы и проверки, склонируйте себе этот репозиторий и ведите работу по мини-таскам в соответствующих директориях. При обращении в коде к исходным или дополнительным файлам, используйте относительные пути. Не забудьте подробно описать шаги вашего решения либо в самом файле .ipynb, либо в дополнительном .md файле в соответствующей директории.


## Общее описание задачи
Участникам необходимо применить различные методы обработки данных, анализа и машинного обучения для **предсказания константы диссоциации (Kd) комплекса аптамер-мишень**, которая определяет афинность аптамера к заданной молекуле. Исходный набор данных находится в папке raw_data, его полное описание, а также методы сбора данных можно найти в исходной публикации (https://academic.oup.com/nar/article/52/D1/D351/7334094). В ходе четырех мини-тасков участники пройдут путь от сырых необработанных данных до полноценной модели машинного обучения. Описание всех заданий, а также критерии их оценивания приведены ниже.

## Мини-таск №1: Data preprocessing

### Описание
Первоначальная обработка и подготовка данных является ключевым этапом для последующего анализа и построения модели. В рамках этого мини-таска участникам необходимо:

1. Очистить и преобразовать числовые параметры, в том числе **таргетную величину Kd**, из строкового типа данных в числовой тип. Это может включать удаление лишних символов, конвертацию в правильный числовой формат и приведение значений к единому виду. Рекомендуется использовать для этого регулярные выражения и библиотеку re.
2. Обработать другие параметры, которые покажутся важными для предсказания целевой переменной (например, провести энкодинг состава буфера или типа аптамера)
3. Для малых молекул преобразовать названия в SMILES-представление, а для белковых мишеней - в последовательность аминокислот. Дополнить датафрейм этой информацией. Для достоверности полученных данных советуем пользоваться комбинацией библиотек requests и API баз данных (например, PubChem для поиска SMILES по названию и UniProt для поиска последовательности аминокислот белка по названию)
4. Найти дополнительную информацию о мишенях через различные открытые базы данных и источники. Дополнить датафрейм этой информацией, чтобы обогатить данные для последующего анализа.
5. Проверить качество и полноту полученного датафрейма, устранить возможные пропуски данных и неоднозначности.

### Критерии оценивания
- Корректная обработка строковых параметров (0-5 баллов).
- Сохранение дополнительных параметров из исходного датасета или добавление дополнительной информации о мишенях в датасет (0-3 балла)
- Процент сохранения данных при преобразовании названий мишеней в SMILES или последовательности аминокислот (0-10 баллов).
- Обработка пропущенных значений в датасете (0-2 балла).
- Общее качество, чистота и полнота полученного датасета (0-5 баллов).

## Мини-таск №2: Descriptors calculation + Data analysis and visualization

### Описание (часть 1)
Для дальнейшего анализа и построения предсказательных моделей необходимо рассчитать различные дескрипторы (признаки) для последовательностей аптамеров (РНК или ДНК) и характеристик мишеней (белковых или малых молекул). Участникам нужно:

1. Выбрать из датафрейма данные только для одного типа аптамеров (РНК или ДНК) и одного типа мишеней (малые молекулы или белковые мишени). То есть на выходе у участников должна получиться одна из комбинаций: РНК аптамеры-белки, РНК аптамеры-малые молекулы, ДНК аптамеры-белки, ДНК аптамеры-малые молекулы.
2. Использовать подходящие Python-пакеты (например, RDKit, Mordred, PyBioMed) для вычисления разнообразных дескрипторов, отражающих структурные и физико-химические свойства последовательностей аптамеров и характеристик мишеней. Также можно использовать другие подходы к репрезентации молекул, например, эмбеддинги языковых моделей. Сравнение различных подходов будет плюсом.
3. Реализовать код для расчета выбранных дескрипторов и добавить их в датафрейм.
4. Обосновать выбор дескрипторов и проанализировать их достоинства и недостатки.

### Критерии оценивания (часть 1)
- Применение инструментов для расчета дескрипторов аптамеров (0-5 баллов).
- Применение инструментов для расчета дескрипторов мишеней (0-5 баллов).
- Качество и ресурсоёмкость реализованного кода для вычисления дескрипторов (0-5 баллов).
- Обоснованность выбора дескрипторов и их сравнение (0-10 баллов).

### Описание (часть 2)
Для глубокого понимания данных и выявления важных закономерностей участникам необходимо провести всесторонний анализ и визуализацию данных, полученных в предыдущих мини-тасках. В рамках этого мини-таска:

1. Реализовать различные визуализации данных, которые позволят изучить распределение, взаимосвязи и паттерны, в том числе относительно **таргетной величины Kd**. Примеры визуализаций: гистограммы, scatter-plots, корреляционные матрицы, t-SNE, PCA и т.д.
2. Провести очистку от выбросов и аномальных значений, если таковые выявятся на этапе визуализации или анализа данных.
2. Выявить наиболее информативные признаки (как рассчитанные дескрипторы, так и другие параметры) для предсказания **константы диссоциации Kd**. Использовать методы отбора признаков, например, корреляционный анализ или статистические тесты.
3. Сделать обоснованные выводы по результатам анализа данных, включая интерпретацию обнаруженных закономерностей и их связь с предметной областью.

### Критерии оценивания (часть 2)
- Качество, разнообразие и информативность визуализаций данных, в том числе относительно **таргетной величины Kd** (0-10 баллов).
- Глубина и обоснованность выводов, сделанных по результатам анализа данных (0-10 баллов).
- Отбор признаков и их очистка от выбросов (0-5 баллов)

## Мини-таск №4: Machine Learning

### Описание
Заключительный мини-таск направлен на разработку модели машинного обучения для **предсказания константы диссоциации Kd** комплекса аптамер-мишень. Участникам необходимо:

1. Выбрать подходящий алгоритм машинного обучения (например, регрессия, деревья решений, нейронные сети и т.д.) для решения задачи предсказания **таргетной величины Kd**.
2. Подготовить данные для обучения модели, включая масштабирование признаков, разделение на обучающую, валидационную и тестовую выборки.
3. Реализовать процесс отбора важных признаков, чтобы улучшить качество модели.
4. Обучить модель, подобрать оптимальные гиперпараметры и оценить ее качество с помощью соответствующих метрик (MSE, R^2, MAE и др.).
5. Проанализировать и интерпретировать полученные результаты. Сделать выводы о возможностях и ограничениях построенной модели для предсказания **константы диссоциации Kd**.

### Критерии оценивания
- Корректность выбора и реализации алгоритма машинного обучения для предсказания **таргетной величины Kd** (0-10 баллов).
- Качество подготовки данных для обучения и оценки модели, включая масштабирование и отбор признаков (0-10 баллов).
- Обоснованность выбора метрик оценки качества модели и их интерпретация (0-5 баллов).
