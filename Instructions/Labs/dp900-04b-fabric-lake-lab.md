---
lab:
  title: Изучение аналитики данных в Microsoft Fabric
  module: Explore fundamentals of large-scale data analytics
---

# Изучение аналитики данных в Microsoft Fabric

В этом упражнении вы изучите прием данных и аналитику в Microsoft Fabric Lakehouse.

Выполнение этого задания займет около **25** минут.

> **Примечание.** Для выполнения этого упражнения потребуется лицензия Microsoft Fabric. Дополнительные сведения о том, как включить бесплатную пробную лицензию Fabric, см. в статье [Начало работы с Fabric](https://learn.microsoft.com/fabric/get-started/fabric-trial). Для этого вам понадобится *учебная* или *рабочая* учетная запись Microsoft. Если у вас ее нет, вы можете [зарегистрироваться для пробной версии Microsoft Office 365 E3 или более поздней версии](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans).

## Создание рабочей области

Прежде чем работать с данными в Fabric, создайте рабочую область с включенной пробной версией Fabric.

1. Войдите в [Microsoft Fabric](https://app.fabric.microsoft.com) по адресу `https://app.fabric.microsoft.com`.
2. В строке меню слева выберите **Рабочие области** (значок выглядит как ).
3. Создайте рабочую область с выбранным именем, выбрав режим лицензирования в разделе **Дополнительно**, который включает возможности Fabric (*пробная версия*, *premium* или *Fabric*).
4. Когда откроется новая рабочая область, она должна быть пустой.

    ![Снимок экрана: пустая рабочая область в Power BI.](./images/new-workspace.png)

## Создание озера данных

Теперь, когда у вас есть рабочая область, пришло время переключиться на интерфейс *Инжиниринг данных* на портале и создать хранилище в озере данных для ваших файлов данных.

1. В нижней левой части портала перейдите к интерфейсу **Инжиниринг данных**.

    ![Снимок экрана: меню переключателя интерфейса.](./images/fabric-switcher.png)

    Домашняя страница инжиниринга данных содержит плитки для создания часто используемых ресурсов инжиниринга данных.

2. На домашней странице **Инжиниринг данных** создайте новое **Озеро данных** с выбранным именем.

    Через минуту или около того будет создано новое озеро данных:

    ![Снимок экрана: новое озеро данных.](./images/new-lakehouse.png)

3. Просмотрите новое озеро данных и обратите внимание, что **Панель обозревателя озера данных** слева позволяет просматривать таблицы и файлы в озере данных:
    - Папка **Таблицы** содержит таблицы, которые можно запрашивать с помощью SQL. Таблицы в озере Microsoft Fabric основаны на формате файла с открытым кодом *Delta Lake*, часто используемом в Apache Spark.
    - Папка **Файлы** содержит файлы данных в хранилище OneLake для озера данных, которые не связаны с управляемыми таблицами Delta. Вы также можете создать *ярлыки* в этой папке, чтобы ссылаться на данные, которые хранятся во внешней памяти.

    В настоящее время в озере данных нет таблиц или файлов.

## Прием данных

Простой способ приема данных — использовать действие **Копировать данные** в конвейере, чтобы извлечь данные из источника и скопировать их в файл в озере данных.

1. На **Домашней странице** вашего озера в меню **Получить данные** выберите **Создать новый конвейер данных** и создайте новый конвейер данных с именем **Ingest Sales Data**.
1. В мастере **копирования данных** на странице **Выбор источника данных** выберите образец набора данных **Модель данных розничной торговли от Wide World Importers**.

    ![Снимок экрана: Выберите страницу источника данных.](./images/choose-data-source.png)

1. Нажмите кнопку **Далее** и просмотрите таблицы в источнике данных на странице **Подключение к источнику данных**.
1. Выберите таблицу **dimension_stock_item**, содержащую записи о продуктах. Затем нажмите кнопку **Далее**, чтобы перейти на страницу **Выбор назначения данных**.
1. На странице **Выбор назначения данных** выберите существующее озеро данных. Затем выберите **Далее**.
1. Задайте следующие параметры назначения данных и нажмите кнопку **Далее**:
    - **Корневая папка**: Таблицы
    - **Загрузка параметров**: загрузка в новую таблицу
    - **Название таблицы назначения**: dimension_stock_item
    - **Сопоставления столбцов**: *оставьте эту настройку по умолчанию как есть*
    - **Включить раздел**: *Не выбрано*
1. На странице**Просмотреть и сохранить** убедитесь, что выбран параметр **Немедленно начать передачу данных** и нажмите кнопку **Сохранить и запустить**.

    Создается новый конвейер, содержащий действие **Копировать данные**, как показано ниже:

    ![Снимок экрана: конвейер с действием Копировать данные.](./images/copy-data-pipeline.png)

    При запуске конвейера можно отслеживать его состояние на панели **Вывод** в разделе конструктора конвейеров. Используйте значок **↻** (*Обновить*), чтобы обновить состояние, и дождитесь успешного удаления.

1. В строке меню концентратора слева выберите озеро данных.
1. На **домашней** странице на **Панели обозревателя озера данных** разверните **Таблицы** и убедитесь, что таблица **dimension_stock_item** создана.

    > **Примечание**. Если новая таблица указана как *неопознанная*, нажмите кнопку **Обновить** на панели инструментов озера данных, чтобы обновить представление.

1. Выберите таблицу **dimension_stock_item**, чтобы просмотреть ее содержимое.

    ![Снимок экрана: таблица dimension_stock_item.](./images/dimProduct.png)

## Запрос данных в озере данных

Теперь, когда вы получили данные в таблицу в озере данных, вы можете использовать SQL для его запроса.

1. В правом верхнем углу страницы Lakehouse перейдите в **конечную точку** аналитики SQL для озера.

    ![Снимок экрана: меню конечной точки аналитики SQL.](./images/endpoint-switcher.png)

1. На панели инструментов выберите **Новый SQL-запрос**. Введите в редактор запросов следующий код SQL:

    ```sql
    SELECT Brand, COUNT(StockItemKey) AS Products
    FROM dimension_stock_item
    GROUP BY Brand
    ```

1. Нажмите кнопку **▷ Выполнить**, чтобы запустить запрос и просмотреть результаты, которые должны показать, что в каждом из них есть две позиции бренда (*Н/Д* и *Northwind*), а также отобразить количество продуктов по каждой позиции.

    ![Снимок экрана: SQL-запрос.](./images/sql-query.png)

## Визуализация данных в озере данных

Microsoft Fabric lakehouse упорядочивает все таблицы в семантической модели данных, которую можно использовать для создания визуализаций и отчетов.

1. В нижней левой части страницы на панели **Обозреватель** выберите вкладку **Модель**, чтобы просмотреть модель данных для таблиц в озере данных (в этом случае есть только одна таблица).

    ![Снимок экрана: страница модели в озере данных Fabric.](./images/fabric-model.png)

1. На панели инструментов выберите **Новый отчет**, чтобы открыть новую вкладку браузера, содержащую конструктор отчетов Power BI.
1. В конструкторе отчетов:
    1. На панели **Данные** разверните таблицу **dimension_stock_item** и выберите поля **Brand** и **StockItemKey**.
    1. На панели **Визуализация** выберите визуализацию **Линейчатой диаграммы с накоплением** (это первая из них). Затем убедитесь, что **ось Y** содержит поле **Brand**, и измените агрегирование на **оси X** на **Count**, чтобы оно содержало поле **Count of StockItemKey**. Наконец, измените размер визуализации на холсте отчета, чтобы заполнить доступное пространство.

        ![Снимок экрана: отчет Power BI](./images/fabric-report.png)

    > **Совет**: Значки **>>** можно использовать для скрытия панелей конструктора отчетов, чтобы увидеть отчет более четко.

1. В меню **Файл** выберите **Сохранить**, чтобы сохранить отчет как **Отчет о количестве бренда** в рабочей области Fabric.

    Теперь вы можете закрыть вкладку браузера, содержащую отчет, и вернуться в свое озеро данных. Отчет можно найти на странице рабочей области на портале Microsoft Fabric.

## Очистка ресурсов

По окончании изучения Microsoft Fabric можно удалить рабочую область, созданную для этого упражнения.

1. На панели слева выберите значок рабочей области, чтобы просмотреть все содержащиеся в ней элементы.
2. В меню **...** на панели инструментов выберите **Параметры рабочей области**.
3. В разделе **Другие** выберите **Удалить эту рабочую область**.
