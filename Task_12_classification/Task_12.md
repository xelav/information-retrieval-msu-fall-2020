# Задание 12 от 26.10.20 (Классификация текстов)

Валентин Александров, 620 группа

## Постановка задачи

- Система рубрикации должна классифицировать
поток документов по двум рубрикам.
- Эксперт отнес к первой рубрике 75 документов, ко
второй рубрике – 50 документов.
- Система отнесла:
  - к первой рубрике 100 документов, из них 50
  правильно.
  - ко второй рубрике 40 документов, из них 30
  правильно.
- Найти макро-характеристики качества классификации
(точность, полноту, F-меру) - и микро-характеристики (точность, полноту, F-меру).

## Решение

$N = 175$

### Метрики для первой рубрики

Confusion Matrix для первой рубрики:

| Assigned\Actual | Positive | Negative |
|-----------------|----------|----------|
| Positive        | TP = 50  | FP = 50  |
| Negative        | FN = 25  | TN = 50  |

$Precision = \frac{TP}{TP+FP} = 0.5$
$Recall = \frac{TP}{TP+FN} = \frac{2}{3}$
$F1 score = \frac{2Precision\cdot Recall}{Precision + Recall} = 0.571$

### Метрики для второй рубрики

Confusion Matrix для второй рубрики:

| Assigned\Actual | Positive | Negative |
|-----------------|----------|----------|
| Positive        | TP = 30  | FP = 10  |
| Negative        | FN = 20  | TN = 115 |

$Precision = \frac{TP}{TP+FP} = 0.75$
$Recall = \frac{TP}{TP+FN} = 0.6$
$F1 score = \frac{2Precision\cdot Recall}{Precision + Recall} = 0.666$

### Макро-метрики

$Precision_{Macro} = 0.625$
$Recall_{Macro} = 0.633$
$F1_{Macro} = 0.619$
$F1_{macro}^{*} = 0.628$ (см. раздел ["Дополнительно: альтернативное макро-усреднение для F1"](#alternative-f1))

### Микро-метрики

Суммированная Confusion Matrix:

| Assigned\Actual | Positive | Negative |
|-----------------|----------|----------|
| Positive        | TP = 80  | FP = 60  |
| Negative        | FN = 45  | TN = 165 |

$Precision_{Micro} = 0.571$
$Recall_{Micro} = 0.64$
$F1_{Micro} = 0.608$

### <a name="alternative-f1"></a> Дополнительно: альтернативное макро-усреднение для F1

Существует альтернативная формула для макро-усреднения F1, которая заключается в вычислении гармоничксого среднего макро-усредненных точности и полноты:

$$F1_{macro}^{*} = \frac{2Precision_{macro}\cdot Recall_{macro}}{Precision_{macro} + Recall_{macro}} $$

$F1_{macro}^{*} = 0.628$

Данная метрика предложена в статье [_"A systematic analysis of performance measures for classification tasks"_](https://scholar.google.com/scholar?cluster=14636768960278377699&hl=en&as_sdt=0,5&sciodt=0,5). В статье [_"Macro F1 and Macro F1"_](https://arxiv.org/pdf/1911.03347.pdf) проводится сравнение двух макро-метрик. Авторы предлагают пользоваться "обычным" $F1_{macro}$, так как $F1_{macro}^{*}$ значительно завышает метрику для классификаторов склонным к одному роду ошибок.
Вся информация была взята из [данной статьи](https://towardsdatascience.com/a-tale-of-two-macro-f1s-8811ddcf8f04).