# ПРОЕКТ: Обучение с учителем: качество модели

В роли стажера отдела цифровых технологий интернет-магазина «В один клик» разработать решение, которое позволит персонализировать предложения постоянным клиентам, чтобы увеличить их покупательскую активность.

# Задачи проекта
1. Построить модель, которая предскажет вероятность снижения покупательской активности клиента в следующие три месяца.
2. На основе данных моделирования и прибыльности клиентов выделить сегмент покупателей и разработать для него персонализированные предложения.

# Краткое описание проведенной работы:

Главные задачи проекта это построение модели машинного обучения, которая предскажет вероятность снижения покупательской активности клиента, и разработка на основе данных моделирования и прибыльности клиентов персонализированных предложений для повышения покупательской активности для определенного сегмента покупателей.

**В качестве исходных данных имеется 4 датасета:**
- таблица, которая содержит данные о поведении покупателя на сайте, о коммуникациях с покупателем и его продуктовом поведении
- таблица с данными о выручке, которую получает магазин с покупателя, то есть сколько покупатель всего потратил за период взаимодействия с сайтом
- таблица с данными о времени (в минутах), которое покупатель провёл на сайте в течение периода
- таблица с данными о среднемесячной прибыли покупателя за последние 3 месяца: какую прибыль получает магазин от продаж каждому покупателю


**Результат предобработки данных:**
- устранена проблема с неявными дубликатами
- наименования столбцов приведены в соответствие принятым соглашениям (`camel_case`)
- типы данных приведены в соответствие
- устранены опечатки в значениях

Для поиска лучшей модели был применен инструмент `RandomizedSearch` и перебор гиперпараметров для четырех моделей:
- `DecisionTreeClassifier()`
- `KNeighborsClassifier()`
- `LogisticRegression()`
- `SVC()`

Лучшая модель отбиралась по метрике **ROC-AUC**. Лучшей моделью оказалась `LogisticRegression()` с `L1-регуляризацией`.

- Метрика ROC-AUC на кросс-валидации: **0.91**
- Метрика ROC-AUC на тестовой выборке: **0.85**

###  Рекомендации:

Для дополнительного исследования был взят сегмент **Группа клиентов с высокой вероятностью снижения покупательской активности и наиболее высокой прибыльностью**. Показатели признаков данной группы были проанализированы в сравнении с группой клиентов с **низкой** вероятностью снижения покупательской активности. Важность признаков изучена с помощью SHAP-значений для обученной модели. По результатам данной работы можно сформулировать следующие возможные пути повышения покупательской активности:

1. Повышать количество маркетинговых коммуникаций.
2. Напоминать о наличии неоплаченных товаров в корзине.
3. Чаще показывать карточки товара в категории **Мелкая бытовая техника и электроника**.

Проанализировав графики обоих сегментов выяснилось, что покупательская активность чаще снижается, чем в общем датафрейме, а если точнее, то в общей выборке в 38% случаев покупательская активность снизилась, а в самых популярных категориях Товаря для детей и Домашний текстиль покупательская активность снизилась в 44% и 40% случаев соответственно.

## Увеличить покупательскую активность в данных категориях покупателей можно следующими методами:

Для категории "Товары для детей" можно проводить сезонные распродажы, к примеру, к началу учебного года. Так же можно реализовать программу бонусов за покупки, делать дополнительные скидки в праздники и таким образом покупательская активность может возрасти.
С категорией "Домашний текстиль" почти тоже самое, можно проводить распродажы в зависимости от сезона и так же предоставлять скидки, например, на наборы товаров, чтобы заинтересовать клиентов покупать большее количество товаров.
