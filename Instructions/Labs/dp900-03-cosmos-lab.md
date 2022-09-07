---
lab:
  title: "Изучение возможностей Azure Cosmos\_DB"
  module: Explore fundamentals of Azure Cosmos DB
---
# <a name="explore-azure-cosmos-db"></a>Изучение возможностей Azure Cosmos DB

В этом упражнении вы подготовите к работе базу данных Azure Cosmos DB в подписке Azure, а также изучите различные способы ее использования для хранения нереляционных данных.

Выполнение этого задания займет около **15** минут.

## <a name="before-you-start"></a>Перед началом работы

Вам потребуется [подписка Azure](https://azure.microsoft.com/free) с доступом уровня администратора.

## <a name="create-a-cosmos-db-account"></a>Создание учетной записи Azure Cosmos DB

To use Cosmos DB, you must provision a Cosmos DB account in your Azure subscription. In this exercise, you'll provision a Cosmos DB account that uses the core (SQL) API.

1. In the Azure portal, select <bpt id="p1">**</bpt>+ Create a resource<ept id="p1">**</ept> at the top left, and search for <bpt id="p2">*</bpt>Azure Cosmos DB<ept id="p2">*</ept>.  In the results, select <bpt id="p1">**</bpt>Azure Cosmos DB<ept id="p1">**</ept> and select  <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.
1. В плитке **Основной (SQL) — рекомендовано** выберите **Создать**.
1. Введите приведенные ниже сведения и нажмите кнопку **Проверка и создание**.
    - <bpt id="p1">**</bpt>Subscription<ept id="p1">**</ept>: If you're using a sandbox, select <bpt id="p2">*</bpt>Concierge Subscription<ept id="p2">*</ept>. Otherwise, select your Azure subscription.
    - **Группа ресурсов**: если вы используете песочницу, выберите существующую группу ресурсов (с именем вида *learn-xxxx…* ). В противном случае создайте новую группу с именем по вашему выбору.
    - **Имя учетной записи**: введите уникальное имя.
    - **Location**: выберите любое из рекомендованных расположений
    - **Режим производительности**: подготовленная пропускная способность
    - **Применить скидку бесплатной категории**: выберите "Применить", если доступно
    - **Ограничение общей пропускной способности учетной записи**: не выбрано
1. После проверки конфигурации выберите **Создать**.
1. Wait for deployment to complete. Then go to the deployed resource.

## <a name="create-a-sample-database"></a>Создание образца базы данных

*На протяжении всей процедуры закрывайте любые советы, отображаемые на портале*.

1. На странице новой учетной записи Cosmos DB выберите на панели слева **Обозреватель данных**.
1. На странице **Обозреватель данных** щелкните **Launch quick start** (Запустить быстрый запуск).
1. На вкладке **Создать контейнер** просмотрите предварительно заполненные параметры для примера базы данных и щелкните **ОК**.
1. Отслеживайте состояние на панели в нижней части экрана, пока не будет создана база данных **SampleDB** и контейнер **SampleContainer** (это может занять около минуты).

## <a name="view-and-create-items"></a>Просмотр и создание элементов

1. In the Data Explorer page, expand the <bpt id="p1">**</bpt>SampleDB<ept id="p1">**</ept> database and the <bpt id="p2">**</bpt>SampleContainer<ept id="p2">**</ept> container, and select <bpt id="p3">**</bpt>Items<ept id="p3">**</ept> to see a list of items in the container. The items represent addresses, each with a unique id and other properties.
1. Выберите любой из элементов в списке, чтобы просмотреть представление JSON данных элемента.
1. В верхней части страницы выберите **Создать элемент**, чтобы создать новый пустой элемент.
1. Измените JSON для нового элемента, как показано ниже, а затем нажмите кнопку **Сохранить**.

    ```json
    {
        "address": "1 Any St.",
        "id": "123456789"
    }
    ```

1. После сохранения нового элемента обратите внимание, что дополнительные свойства метаданных добавляются автоматически.

## <a name="query-the-database"></a>Выполнение запросов к базе данных

1. На странице **Обозреватель данных** щелкните значок **Новый запрос SQL**.
1. В редакторе запросов SQL проверьте запрос по умолчанию (`SELECT * FROM c`) и нажмите кнопку `SELECT * FROM c`.
1. Проверьте результаты, включая полное представление JSON всех элементов.
1. Измените запрос следующим образом:

    ```sql
    SELECT c.id, c.address
    FROM c
    WHERE CONTAINS(c.address, "Any St.")
    ```

1. Нажмите кнопку **Выполнить запрос**, чтобы выполнить измененный запрос и просмотреть его результаты, в том числе сущности JSON для всех элементов, у которых поле **адреса** содержит строку текста "Any St.".
1. Закройте редактор запросов SQL, отменив изменения.

    You've seen how to create and query JSON entities in a Cosmos DB database by using the data explorer interface in the Azure portal. In a real scenario, an application developer would use one of the many programming language specific software development kits (SDKs) to call the core (SQL) API and work with data in the database.

> **Совет**. Когда вы завершите знакомство с Azure Cosmos DB, созданную в этом упражнении группу ресурсов можно удалить.
