---
lab:
  title: Изучение аналитики в режиме реального времени в Microsoft Fabric
  module: Explore fundamentals of large-scale data analytics
---

# Изучение аналитики в режиме реального времени в Microsoft Fabric

В этом упражнении вы изучите аналитику в режиме реального времени в Microsoft Fabric.

Выполнение этого задания займет около **25** минут.

> **Примечание.** Для выполнения этого упражнения потребуется лицензия Microsoft Fabric. Дополнительные сведения о том, как включить бесплатную пробную лицензию Fabric, см. в статье [Начало работы с Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial). Для этого вам понадобится *учебная* или *рабочая* учетная запись Microsoft. Если у вас ее нет, вы можете [зарегистрироваться для пробной версии Microsoft Office 365 E3 или более поздней версии](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans).

## Создание рабочей области

Прежде чем работать с данными в Fabric, создайте рабочую область с включенной пробной версией Fabric.

1. Войдите в [Microsoft Fabric](https://app.fabric.microsoft.com) по адресу `https://app.fabric.microsoft.com`.
2. В строке меню слева выберите **Рабочие области** (значок выглядит как ).
3. Создайте рабочую область с выбранным именем, выбрав режим лицензирования в разделе **Дополнительно**, который включает возможности Fabric (*пробная версия*, *premium* или *Fabric*).
4. Когда откроется новая рабочая область, она должна быть пустой.

    ![Снимок экрана: пустая рабочая область в Power BI.](./images/new-workspace.png)

## Создание базы данных KQL

Теперь, когда у вас есть рабочая область, можно создать базу данных KQL для хранения данных в режиме реального времени.

1. В нижней левой части портала перейдите к интерфейсу **Аналитика в режиме реального времени**.

    ![Снимок экрана: меню переключателя интерфейса.](./images/fabric-real-time.png)

    Домашняя страница аналитики в режиме реального времени включает плитки для создания часто используемых ресурсов для данных в режиме реального времени

2. На домашней странице аналитики в режиме реального времени создайте новую **базу данных KQL** с выбранным именем.

    ![Снимок экрана: редактор RTA с выделенной выделенной базой данных KQL.](./images/create-kql-db.png)

   Откроется экран панели мониторинга, а затем нажмите кнопку "База данных KQL" в верхней части экрана.

    ![Снимок экрана: новая база данных KQL.](./images/kql-database.png)

    После выбора вы получите диалоговое ***окно "Новая база данных KQL", где вы получите имя базы данных*** KQL.

    ![Снимок экрана: новое диалоговое окно имени базы данных KQL.](./images/name-kql-db.png)

   - присвойте базе данных имя в этом сценарии: `my_kql_db`
   - Нажмите кнопку "Создать", "Создать" ******
  
    Через минуту будет создана новая база данных KQL:

    В настоящее время в базе данных нет таблиц.

## Создание потока событий

Потоки событий предоставляют масштабируемый и гибкий способ приема данных в режиме реального времени из источника потоковой передачи.

1. В строке меню слева выберите **домашнюю** страницу для аналитики в режиме реального времени.
1. На домашней странице выберите плитку, чтобы создать новый **Поток событий** с выбранным именем.

    Через некоторое время отображается визуальный конструктор для потока событий.

    ![Снимок экрана: конструктор Eventstream.](./images/eventstream-designer.png)

    На холсте визуального конструктора показан источник, который подключается к потоку событий, который, в свою очередь, подключен к назначению.

1. На холсте конструктора в списке **Новый источник** выберите **Пример данных**. Затем в области **Пример данных** укажите имя **такси** и выберите пример данных **Желтое такси** (который представляет данные, собранные из поездок на такси). Нажмите кнопку **Добавить**.
1. Под холстом конструктора выберите вкладку **Предварительный просмотр данных**, чтобы просмотреть данные, передаваемые из источника:

    ![Снимок экрана: предварительный просмотр данных Eventstream.](./images/eventstream-preview.png)

1. На холсте конструктора в списке **Новые назначения** выберите **База данных KQL**. Затем на панели **База данных KQL** укажите имя назначения **данные о такси** и выберите рабочую область и базу данных KQL. Затем нажмите **Создать и настроить**.
1. В мастере **Приема данных** на странице **Назначения** выберите **Создать таблицу** и введите имя таблицы **данные о такси**. Затем нажмите **Далее: Источник**.
1. На странице **Источник** просмотрите имя подключения к данным по умолчанию и нажмите **Далее: схема**.
1. На странице **Схема** измените **Формат данных** с TXT на **JSON** и просмотрите предварительный просмотр, чтобы убедиться, что этот формат приводит к нескольким столбцам данных. Затем выберите **Далее: сводка**.
1. На странице **Сводка** подождите, пока будет установлен непрерывный прием, а затем нажмите кнопку **Закрыть**.
1. Убедитесь, что завершенный поток событий выглядит следующим образом:

    ![Скриншот завершенноого Eventstream.](./images/complete-eventstream.png)

## Запрос данных в реальном времени в базе данных KQL

Поток событий постоянно заполняет таблицу в базе данных KQL, что позволяет запрашивать данные в режиме реального времени.

1. В центре меню слева выберите базу данных KQL (или выберите рабочую область и найдите там базу данных KQL).
1. В меню **...** для таблицы **данные о такси** (которая была создана в потоке событий) выберите **Таблица запросов > Записи, принятые за последние 24 часа**.

    ![Снимок экрана: меню таблицы "Запрос" в базе данных KQL.](./images/kql-query.png)

1. Просмотрите результаты запроса, который должен быть запросом KQL, следующим образом:

    ```kql
    ['taxi-data']
    | where ingestion_time() between (now(-1d) .. now())
    ```

    Результаты показывают все записи о такси, полученные из источника потоковой передачи за последние 24 часа.

1. Замените весь код запроса KQL в верхней половине редактора запросов следующим кодом:

    ```kql
    // This query returns the number of taxi pickups per hour
    ['taxi-data']
    | summarize PickupCount = count() by bin(todatetime(tpep_pickup_datetime), 1h)
    ```

1. Используйте кнопку** ▷ Запуск** для запуска запроса и просмотра результатов, которые показывают количество посадок в такси за каждый час.

## Очистка ресурсов

Если вы закончили изучение аналитики в режиме реального времени в Microsoft Fabric, вы можете удалить рабочую область, созданную для этого упражнения.

1. На панели слева выберите значок рабочей области, чтобы просмотреть все содержащиеся в ней элементы.
2. В меню **...** на панели инструментов выберите **Параметры рабочей области**.
3. В разделе **Другие** выберите **Удалить эту рабочую область**.
