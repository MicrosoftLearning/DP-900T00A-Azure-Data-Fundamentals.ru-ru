---
lab:
  title: Изучение аналитики в режиме реального времени в Microsoft Fabric
  module: Explore fundamentals of large-scale data analytics
---

# Изучение аналитики в режиме реального времени в Microsoft Fabric

В этом упражнении вы изучите аналитику в режиме реального времени в Microsoft Fabric.

Выполнение этого задания займет около **25** минут.

> **Примечание**. Для выполнения этого упражнения вам потребуется лицензия Microsoft Fabric. Дополнительные сведения о том, как включить бесплатную пробную лицензию Fabric, см. в статье [Начало работы с Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial) . Для этого вам потребуется *учебная* или *рабочая* учетная запись Майкрософт. Если у вас ее нет, вы можете [зарегистрироваться для получения пробной версии Microsoft Office 365 E3 или более поздней версии](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans).

## Создание рабочей области

Перед работой с данными в Fabric создайте рабочую область с включенной пробной версией Fabric.

1. Войдите в [Microsoft Fabric](https://app.fabric.microsoft.com) по адресу `https://app.fabric.microsoft.com`.
2. В строке меню слева выберите **Рабочие области** (значок похож на &#128455;).
3. Создайте рабочую область с выбранным именем, выбрав режим лицензирования в разделе **Дополнительно** , который включает емкость Fabric (*Пробная версия*, *Премиум* или *Структура*).
4. Когда откроется новая рабочая область, она должна быть пустой.

    ![Снимок экрана: пустая рабочая область в Power BI.](./images/new-workspace.png)

## Создание базы данных KQL

Теперь, когда у вас есть рабочая область, можно создать базу данных KQL для хранения данных в режиме реального времени.

1. В левом нижнем углу портала перейдите к **интерфейсу Аналитика в режиме реального времени**.

    ![Снимок экрана: меню переключателя взаимодействия.](./images/fabric-real-time.png)

    Домашняя страница аналитики в режиме реального времени содержит плитки для создания часто используемых ресурсов для анализа данных в режиме реального времени.

2. На домашней странице аналитики в режиме реального времени создайте базу **данных KQL** с выбранным именем.

    Через минуту или около того будет создана новая база данных KQL:

    ![Снимок экрана: новая база данных KQL.](./images/kql-database.png)

    В настоящее время в базе данных нет таблиц.

## Создание потока событий

Потоки событий предоставляют масштабируемый и гибкий способ приема данных в режиме реального времени из источника потоковой передачи.

1. В строке меню слева выберите **домашнюю** страницу для аналитики в режиме реального времени.
1. На домашней странице выберите плитку, чтобы создать поток **событий** с выбранным именем.

    Через некоторое время отобразится визуальный конструктор для потока событий.

    ![Снимок экрана: конструктор Eventstream.](./images/eventstream-designer.png)

    На холсте визуального конструктора показан источник, который подключается к потоку событий, который, в свою очередь, подключен к месту назначения.

1. На холсте конструктора в списке **Новый источник** для источника выберите **Пример данных**. Затем в области **Пример данных** укажите имя **taxis** и выберите образец данных **Yellow Taxi** (который представляет данные, собранные из поездок в такси). Нажмите кнопку **Добавить**.
1. Под холстом конструктора выберите вкладку **Предварительный просмотр данных** , чтобы просмотреть данные, передаваемые из источника:

    ![Снимок экрана: предварительный просмотр данных Eventstream.](./images/eventstream-preview.png)

1. На холсте конструктора в списке **Новое назначение** для назначения выберите **база данных KQL**. Затем в области **базы данных KQL** укажите имя назначения **taxi-data** и выберите свою рабочую область и базу данных KQL. Затем выберите **Создать и настроить**.
1. В **мастере приема данных** на странице **Назначение** выберите **Создать таблицу** и введите имя таблицы **taxi-data**. Затем выберите **Далее: источник**.
1. На странице **Источник** просмотрите имя подключения к данным по умолчанию и выберите **Далее: схема**.
1. На странице **Схема** измените **формат данных** с TXT на **JSON** и просмотрите предварительный просмотр, чтобы убедиться, что этот формат приводит к нескольким столбцам данных. Затем выберите **Далее: сводка**.
1. На странице **Сводка** дождитесь установки непрерывного приема и нажмите кнопку **Закрыть**.
1. Убедитесь, что завершенный поток событий выглядит следующим образом:

    ![Снимок экрана: завершенный поток событий.](./images/complete-eventstream.png)

## Запрос данных в режиме реального времени в базе данных KQL

Поток событий постоянно заполняет таблицу в базе данных KQL, что позволяет запрашивать данные в режиме реального времени.

1. В центре меню слева выберите базу данных KQL (или рабочую область и найдите там базу данных KQL).
1. В меню **...** для таблицы **taxi-data** (созданной потоком событий) выберите **Таблица запросов > Записи, принятые за последние 24 часа**.

    ![Снимок экрана: меню таблицы запроса в базе данных KQL.](./images/kql-query.png)

1. Просмотрите результаты запроса, который должен быть KQL-запросом, как показано ниже:

    ```kql
    ['taxi-data']
    | where ingestion_time() between (now(-1d) .. now())
    ```

    Результаты показывают все записи такси, полученные из источника потоковой передачи за последние 24 часа.

1. Замените весь код запроса KQL в верхней части редактора запросов следующим кодом:

    ```kql
    // This query returns the number of taxi pickups per hour
    ['taxi-data']
    | summarize PickupCount = count() by bin(tpep_pickup_datetime, 1h)
    ```

1. Используйте ** кнопку&#9655; Выполнить** , чтобы выполнить запрос и просмотреть результаты, в которых отображается количество пикапов такси за каждый час.

## Очистка ресурсов

Если вы завершили изучение аналитики в режиме реального времени в Microsoft Fabric, вы можете удалить рабочую область, созданную для этого упражнения.

1. На панели слева щелкните значок рабочей области, чтобы просмотреть все содержащиеся в ней элементы.
2. В меню **...** на панели инструментов выберите **Параметры рабочей области**.
3. В разделе **Другое** выберите **Удалить эту рабочую область**.