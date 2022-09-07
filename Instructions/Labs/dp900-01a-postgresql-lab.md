---
lab:
  title: Изучение Базы данных Azure для PostgreSQL
  module: Explore relational data in Azure
---

# <a name="explore-azure-database-for-postgresql"></a>Изучение Базы данных Azure для PostgreSQL

В этом упражнении вы подготовите к работе ресурс "База данных Azure для PostgreSQL" в своей подписке Azure.

Выполнение этого задания займет около **5** минут.

## <a name="before-you-start"></a>Перед началом работы

Вам потребуется [подписка Azure](https://azure.microsoft.com/free) с доступом уровня администратора.

## <a name="provision-an-azure-database-for-postgresql-resource"></a>Подготовка к работе ресурса "База данных Azure для PostgreSQL"

В этом упражнении вы будете подготавливать к работе ресурс "База данных Azure для PostgreSQL".

1. In the Azure portal, select <bpt id="p1">**</bpt>&amp;#65291; Create a resource<ept id="p1">**</ept> from the upper left-hand corner and search for <bpt id="p2">*</bpt>Azure Database for PostgreSQL<ept id="p2">*</ept>. Then in the resulting <bpt id="p1">**</bpt>Azure Database for PostgreSQL<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.

1. Просмотрите доступные варианты Базы данных Azure для PostgreSQL, а затем в области **Гибкий сервер** нажмите **Создать**.

    ![Снимок экрана вариантов развертывания Базы данных Azure для PostgreSQL.](images/postgresql-options.png)

1. На странице **Создание Базы данных SQL** введите следующие значения.
    - **Подписка**: Выберите подписку Azure.
    - **Группа ресурсов**: создайте новую группу ресурсов с именем по своему выбору.
    - **Имя сервера**: введите уникальное имя.
    - **Регион**: выберите регион рядом с вами.
    - **Версия PostgreSQL**: оставьте без изменений.
    - **Тип рабочей нагрузки**: выберите **Разработка**.
    - **Вычисления и хранилище**: оставьте без изменений.
    - **Зона доступности**: оставьте без изменений.
    - **Включить высокий уровень доступности**: оставьте без изменений.
    - **Имя администратора**: введите свое имя.
    - **Пароль** и **Подтверждение пароля**: укажите достаточно сложный пароль.

1. По завершении выберите **Далее: Сеть**.

1. В разделе **Правила брандмауэра** выберите **&#65291; Добавьте текущий IP-адрес клиента**.

1. Щелкните **Просмотр и создание**, а затем нажмите кнопку **Создать**, чтобы создать базу данных PostgreSQL Azure.

1. Wait for deployment to complete. Then go to the resource that was deployed, which should look like this:

    ![Снимок экрана портала Azure со страницей Базы данных Azure для PostgreSQL.](images/postgresql-portal.png)

1. Ознакомьтесь с вариантами управления вашим ресурсом "База данных Azure для PostgreSQL".

> **Совет**. Когда вы завершите знакомство с Базой данных Azure для PostreSQL, созданную в этом упражнении группу ресурсов можно удалить.
