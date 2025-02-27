# Задача на реграссию.

Мы примерно понимаем, что чем выше человек, тем он больше весит. Давайте возьмем некоторые данные иобучим модель машинного обучения предсказывать вес человека по его росту.

## Откройте Jupyter, новую тетрадку.

В первой ячейке устанавливаем требуемые пакеты:

`!pip install pandas scikit-learn matplotlib`

В следующей ячейке импортируем:

```python
import pandas as pd
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt
```

## Наши данные

В следующей ячейке

```python
data = pd.DataFrame({
   "height":[162,180,170,155],
   "weight":[54.5,90, 50.1, 45.8]
})
data
```

## Модель обучения

`lr = LinearRegression()`

## Обучение

`lr.fit(data[['height']], data['weight'])`

## Результат обучения

`lr.coef_, lr.intercept_`

Если все получилось правильно, то ваши коэффициенты будут: 1.6 и -209.6

Таким образом, наша расчетная формула для веса:

**вес = 1.6 * рост -209.6**

## Предсказываем

Теперь подставляем в модель какой-нибудь рост (например, 175) и получаем вес:

`lr.predict([[175]])`

Вы должны получить 73.49. Похже на правду?

Поиграйте сами, повычисляйте рост для разных весов. Например для вашего.

## График

Теперь нанесем модель на данные

Вычислим предсказанные значения для наших данных:

`data['predicted'] = lr.predict(data[['height']])`

Нанесем на график наши данные точками и нашу модель линией:

```python
fig, ax = plt.subplots(figsize=(3,2))
data.sort_values(by="height").plot.line(ax=ax, x="height", y="weight", style='o')
data.sort_values(by="height").plot.line(ax=ax, x="height", y="predicted")
```

![ml-1-plotresult](../img/ml-1-plotresult.jpg)

## Ограничения модели

Попробуйте вычислить вес ребенка с ростом 100 (3-х летний ребенок)

Вы получите вес -49 кг!! Но такого не бывает! Дело в том, что маленькие дети растут подругомузакону, а у нас в данных только взрослые, и модель предсказывает более-менее правильно только в дипазоне данных, на которых она обучилась.

# Классификация

## Данные

Предположим, что мы добавили еше колонку пола в наши данные. Пусть это будет целевая переменная, а рост и вес сделаем признаками.

```python
data = pd.DataFrame({
   "height":[162,180,170,155],
   "weight":[54.5,90, 50.1, 45.8],
   "sex":[1,0, 1, 0]
})
data
```

Где 0 - мужчина, 1 - женщина. (Мы так закодировали, это наш выбор)

## Модель теперь другая

```python
from sklearn.linear_model import LogisticRegression
lr = LogisticRegression()
```

## Обучаем почти так же:

`lr.fit(data[['height', 'weight']], data['sex'])`

## Предсказываем

`lr.predict([[175, 60]])`

Мы получаем вероятности для мужчин и женщин. Их сумма равна 1.


