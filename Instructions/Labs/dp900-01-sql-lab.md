---
lab:
  title: Изучение Базы данных SQL Azure
  module: Explore relational data in Azure
---

# <a name="explore-azure-sql-database"></a>Изучение Базы данных SQL Azure

В этом упражнении вы подготовите к работе ресурс базы данных SQL Azure в подписке Azure, а затем используете SQL для запроса таблиц в реляционной базе данных.

Выполнение этого задания займет около **15** минут.

## <a name="before-you-start"></a>Перед началом работы

Вам потребуется [подписка Azure](https://azure.microsoft.com/free) с доступом уровня администратора.

## <a name="provision-an-azure-sql-database-resource"></a>Подготовка ресурса "База данных SQL Azure"

1. In the <bpt id="p1">[</bpt>Azure portal<ept id="p1">](https://portal.azure.com?azure-portal=true)</ept>, select <bpt id="p2">**</bpt>&amp;#65291; Create a resource<ept id="p2">**</ept> from the upper left-hand corner and search for <bpt id="p3">*</bpt>Azure SQL<ept id="p3">*</ept>. Then in the resulting <bpt id="p1">**</bpt>Azure SQL<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.

1. Просмотрите доступные параметры Azure SQL, а затем в области **Базы данных SQL** убедитесь, что выбран пункт **Отдельная база данных**, и нажмите **Создать**.

    ![Снимок экрана портала Azure со страницей Azure SQL.](images//azure-sql-portal.png)

1. На странице **Создание Базы данных SQL** введите следующие значения.
    - **Подписка**: Выберите подписку Azure.
    - **Группа ресурсов**: создайте новую группу ресурсов с именем по своему выбору.
    - **Имя базы данных**: *AdventureWorks*
    - <bpt id="p1">**</bpt>Server<ept id="p1">**</ept>:  Select <bpt id="p2">**</bpt>Create new<ept id="p2">**</ept> and create a new server with a unique name in any available location. Use <bpt id="p1">**</bpt>SQL authentication<ept id="p1">**</ept> and specify your name as the server admin login and a suitably complex password (remember the password - you'll need it later!)
    - **Нужно ли использовать эластичный пул SQL?**: *Нет*
    - **Вычисления + хранилище**: оставьте без изменений
    - **Избыточность хранилища резервных копий**: выберите *локально избыточное хранилище резервных копий*.

1. On the <bpt id="p1">**</bpt>Create SQL Database<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Next :Networking &gt;<ept id="p2">**</ept>, and on the <bpt id="p3">**</bpt>Networking<ept id="p3">**</ept> page, in the <bpt id="p4">**</bpt>Network connectivity<ept id="p4">**</ept> section, select <bpt id="p5">**</bpt>Public endpoint<ept id="p5">**</ept>. Then select <bpt id="p1">**</bpt>Yes<ept id="p1">**</ept> for both options in the <bpt id="p2">**</bpt>Firewall rules<ept id="p2">**</ept> section to allow access to your database server from Azure services and your current client IP address.

1. Нажмите **Далее: Безопасность >** и выберите для параметра **Включить Microsoft Defender для SQL** значение **Не сейчас**.

1. Нажмите **Далее: Дополнительные параметры >** и на вкладке **Дополнительные параметры** задайте для параметра **Использовать существующие данные** значение **Пример** (будет создан образец базы данных, который можно изучить позже).

1. Щелкните **Просмотр и создание**, а затем нажмите кнопку **Создать**, чтобы создать базу данных SQL Azure.

1. Wait for deployment to complete. Then go to the resource that was deployed, which should look like this:

    ![Снимок экрана портала Azure со страницей базы данных SQL.](images//sql-database-portal.png)

1. В области в левой части страницы выберите **Редактор запросов (предварительная версия)**, а затем войдите с именем и паролем администратора, указанными вами для вашего сервера.
    
    *Если отображается сообщение об ошибке, что IP-адрес клиента не разрешен, нажмите ссылку **Список разрешений IP...** в конце сообщения, чтобы разрешить доступ, и повторите попытку входа (ранее вы добавили клиентский IP-адрес вашего компьютера в правила брандмауэра, но редактор запросов может подключаться с другого адреса в зависимости от конфигурации сети).*
    
    Редактор запросов выглядит следующим образом:
    
    ![Снимок экрана портала Azure с редактором запросов.](images//query-editor.png)

1. Разверните папку **Таблицы**, чтобы просмотреть таблицы в базе данных.

1. В области **Query 1** введите следующий код SQL:

    ```sql
    SELECT * FROM SalesLT.Product;
    ```

1. Нажмите кнопку **&#9655; Запуск** над запросом, чтобы выполнить его и просмотреть результаты, которые должны включать все столбцы для всех строк в таблице **SalesLT.Product**, как показано здесь:

    ![Снимок экрана портала Azure с редактором запросов и результатами запроса.](images//sql-query-results.png)

1. Замените инструкцию SELECT следующим кодом, а затем нажмите **&#9655; Запуск**, чтобы выполнить новый запрос и просмотреть результаты (которые включают только столбцы **ProductID**, **Name**, **ListPrice** и **ProductCategoryID**):

    ```sql
    SELECT ProductID, Name, ListPrice, ProductCategoryID
    FROM SalesLT.Product;
    ```

1. Теперь попробуйте выполнить следующий запрос, который использует соединение для получения имени категории из таблицы **SalesLT.ProductCategory**:

    ```sql
    SELECT p.ProductID, p.Name AS ProductName,
            c.Name AS Category, p.ListPrice
    FROM SalesLT.Product AS p
    JOIN [SalesLT].[ProductCategory] AS c
        ON p.ProductCategoryID = c.ProductCategoryID;
    ```

1. Закройте панель редактора запросов, отменяя внесенные изменения.

> **Совет**. Когда вы завершите знакомство с Базой данных SQL Azure, созданную в этом упражнении группу ресурсов можно удалить.
