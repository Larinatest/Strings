# Домашнее задание к занятию «Строки и массивы»

## Цель задания

1. Научиться использовать циклы для работы с массивами.

## Инструкция к заданию

1. Скачайте и установите профессиональный редактор кода [Intellij Idea Community Version](https://www.jetbrains.com/idea/download/).
1. Откройте IDEA и [создайте и настройте новый Maven-проект](QA_Maven_Idea_Create.md). Под каждую задачу следует создавать отдельный проект, если обратное не сказано в условии.
2. Создайте пустой репозиторий на GitHub и свяжите его с папкой вашего проекта, а не с какой-либо другой.
3. Правильно настройте репозиторий в плане `.gitignore`. Проигнорируйте папки `.idea` и `target` (раньше была `out`) и `.iml`-файл — их в репозитории быть не должно.
4. Выполните в IDEA требуемую задачу согласно условию.
5. Проверьте соблюдение [правил форматирования кода](QA_Java_Idea_Format.md).
6. Убедитесь, что при запуске `mvn clean test` все тесты запускаются, проходят, а сборка завершается успешно.
7. Закоммитьте и отправьте в репозиторий содержимое папки проекта.

## Задание 1

Статистика — очень важный компонент любого бизнеса. У вас есть набор данных о продажах конкретного предприятия по месяцам: `[8, 15, 13, 15, 17, 20, 19, 20, 7, 14, 14, 18]`. Компании могут быть крупными, продажи могут быть до 5 млрд в месяц.

Программисты все заняты, и вам поручили написать небольшой сервис, который умеет по предоставленному ему массиву месячных продаж рассчитывать:
* сумму всех продаж;
* среднюю сумму продаж в месяц;
* номер месяца, в котором был пик продаж, то есть осуществлены продажи на максимальную сумму*;
* номер месяца, в котором был минимум продаж, то есть осуществлены продажи на минимальную сумму*;
* количество месяцев, в которых продажи были ниже среднего (см. п.2);
* количество месяцев, в которых продажи были выше среднего (см. п.2).

Примечание: в вашем задании нужно найти последний месяц, соответствующий условиям.

Сервис должен представлять собой один класс с шестью методами — по методу на пункт. Входные данные для расчёта сервис должен принимать в параметрах своих методов. Обратите внимание, что написанный класс должен уметь работать с любыми корректными значениями в массиве продаж, а приведённый выше набор — это лишь пример данных для ваших тестов на методы создаваемого класса.

Метод ниже считает номер месяца минимальных продаж. 
Логика его такова: заводим переменную `minMonth` для хранения номера ячейки в массиве того месяца, в котором были минимальные продажи среди всех уже просмотренных.
Изначально мы никакие ещё не просмотрели, потому запишем туда номер 0.
Будем циклом поочерёдно смотреть месяцы продаж, перебирая все номера ячеек.
Если мы смотрим на месяц, в котором продажи меньше, чем в том, который мы помним как минимальный из просмотренных ранее, то считаем теперь этот рассматриваемый месяц минимальным и присваиваем в `minMonth` значение `i`.
И так до конца массива продаж, тогда после цикла в `minMonth` у нас будет лежать номер месяца минимальных продаж.
Останется только один момент: мы нумеровали месяцы с нуля, так как в массивах ячейки нумеруются с нуля, потому, отдавая ответ, нам надо прибавить 1.

```java
    public int minSales(long[] sales) {
        int minMonth = 0; // номер месяца с минимальными продажами среди просмотренных ранее

        for (int i = 0; i < sales.length; i++) {
            if (sales[i] <= sales[minMonth]) { // значит, в рассматриваемом i-м месяце продаж меньше
                minMonth = i; // запомним его как минимальный
            }
        }

        return minMonth + 1; // месяца нумеруются с 1, а индексы массива с 0, нужно сдвинуть ответ на 1
    }
```

Вам необходимо
1. Создать Maven-проект, в котором в package `ru.netology.stats` будет класс `StatsService` с необходимыми методами, сами придумайте им говорящие названия.
1. Написать на каждый метод по одному автотесту, который проверяет правильность работы на тестовых данных.
1. Убедиться, что ваши автотесты работают и проходят.

------

## Правила приёма работы

Прикреплена одна ссылка на публичный репозиторий с решением задачи.
