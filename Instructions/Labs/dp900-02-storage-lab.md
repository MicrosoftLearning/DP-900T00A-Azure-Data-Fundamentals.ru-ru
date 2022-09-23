---
lab:
  title: "Изучение нереляционных данных в службе хранилища\_Azure"
  module: Explore Azure Storage for non-relational data
---

# <a name="explore-non-relational-data-in-azure-with-azure-storage"></a>Изучение нереляционных данных в службе хранилища Azure

В этом упражнении вы подготовите к работе учетную запись службы хранилища Azure в подписке Azure, а также изучите различные способы ее использования для хранения данных.

Выполнение этого задания займет около **15** минут.

## <a name="before-you-start"></a>Перед началом работы

Вам потребуется [подписка Azure](https://azure.microsoft.com/free) с доступом уровня администратора.

## <a name="provision-an-azure-storage-account"></a>Подготовка учетной записи службы хранилища Azure

Первый шаг при использовании службы хранилища Azure — подготовка учетной записи службы хранилища Azure в подписке Azure.

1. Если вы еще этого не сделали, войдите на [портал Azure](https://portal.azure.com?azure-portal=true).
1. On the Azure portal home page, select <bpt id="p1">**</bpt>&amp;#65291; Create a resource<ept id="p1">**</ept> from the upper left-hand corner and search for <bpt id="p2">*</bpt>Storage account<ept id="p2">*</ept>. Then in the resulting <bpt id="p1">**</bpt>Storage account<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.
1. В мастере **Создание учетной записи хранения** введите приведенные ниже значения:
    - <bpt id="p1">**</bpt>Subscription<ept id="p1">**</ept>: If you're using a sandbox, select <bpt id="p2">*</bpt>Concierge Subscription<ept id="p2">*</ept>. Otherwise, select your Azure subscription.
    - **Группа ресурсов**: если вы используете песочницу, выберите существующую группу ресурсов (с именем вида *learn-xxxx…* ). В противном случае создайте новую группу с именем по вашему выбору.
    - **Служба хранилища имя учетной записи**: введите уникальное имя для учетной записи хранения, используя буквы и цифры в нижнем регистре.
    - **Регион**: выберите любое доступное расположение.
    - **Производительность**: *стандартная*
    - **Избыточность**: *выберите Локально избыточное хранилище (LRS)*

1. Select <bpt id="p1">**</bpt>Next: Advanced &gt;<ept id="p1">**</ept> and view the advanced configuration options. In particular, note that this is where you can enable hierarchical namespace to support Azure Data Lake Storage Gen2. Leave this option <bpt id="p1">**</bpt><bpt id="p2">&lt;u&gt;</bpt>unselected<ept id="p2">&lt;/u&gt;</ept><ept id="p1">**</ept> (you'll enable it later), and then select <bpt id="p3">**</bpt>Next: Networking &gt;<ept id="p3">**</ept> to view the networking options for your storage account.
1. Select <bpt id="p1">**</bpt>Next: Data protection &gt;<ept id="p1">**</ept> and then in the <bpt id="p2">**</bpt>Recovery<ept id="p2">**</ept> section, <bpt id="p3">&lt;u&gt;</bpt>de<ept id="p3">&lt;/u&gt;</ept>select all of the <bpt id="p4">**</bpt>Enable soft delete...<ept id="p4">**</ept> options. These options retain deleted files for subsequent recovery, but can cause issues later when you enable hierarchical namespace.
1. Листайте оставшиеся страницы, нажимая **Далее >** и не меняя параметры по умолчанию, а затем на странице **Проверка и создание** дождитесь подтверждения своих настроек и выберите **Создать**. Ваша учетная запись хранения Azure будет создана.
1. Wait for deployment to complete. Then go to the resource that was deployed.

## <a name="explore-blob-storage"></a>Исследуйте хранилище BLOB-объектов

Теперь, когда у вас есть учетная запись службы хранилища Azure, можно создать контейнер для данных BLOB-объектов.

1. Скачайте JSON-файл [product1.json](https://aka.ms/product1.json?azure-portal=true) из `https://aka.ms/product1.json` и сохраните его на компьютере (его можно сохранить в любой папке — вы сможете отправить его в хранилище BLOB-объектов позже).

    *Если JSON-файл отображается в браузере, сохраните страницу как **product1.json**.*

1. На странице контейнера хранилища на портале Azure слева в разделе **Хранилище данных** выберите **Контейнеры**.
1. На странице **Контейнеры** выберите **&#65291; Контейнер** и добавьте новый контейнер с именем **data** и уровнем общего доступа **Частный (без анонимного доступа)** .
1. После создания контейнера **data** убедитесь, что он указан на странице **Контейнеры**.
1. In the pane on the left side, in the top section, select **Storage browser **. This page provides a browser-based interface that you can use to work with the data in your storage account.
1. На странице обозревателя хранилища выберите **Контейнеры BLOB-объектов** и убедитесь, что контейнер **data** присутствует в списке.
1. Выберите контейнер **data** и обратите внимание, что он пуст.
1. Выберите **&#65291; Добавить каталог** и прочтите сведения о папках, прежде чем создавать новый каталог с именем **products**.
1. В обозревателе хранилища убедитесь, что содержимое только что созданной папки **products** отображается в текущем представлении. Вверху страницы должна быть цепочка навигации **Контейнеры BLOB-объектов > data > products**.
1. В навигационной цепочка выберите **data** для переключения в контейнер **data** и обратите внимание, что она <u>не</u> содержит папку **Products**.

    Folders in blob storage are virtual, and only exist as part of the path of a blob. Since the <bpt id="p1">**</bpt>products<ept id="p1">**</ept> folder contained no blobs, it isn't really there!

1. Нажмите кнопку **&#10514; Отправить**, чтобы открыть панель **Отправить BLOB-объект**.
1. In the <bpt id="p1">**</bpt>Upload blob<ept id="p1">**</ept> panel, select the <bpt id="p2">**</bpt>product1.json<ept id="p2">**</ept> file you saved on your local computer previously. Then in the <bpt id="p1">**</bpt>Advanced<ept id="p1">**</ept> section, in the <bpt id="p2">**</bpt>Upload to folder<ept id="p2">**</ept> box, enter <bpt id="p3">**</bpt>product_data<ept id="p3">**</ept> and select the <bpt id="p4">**</bpt>Upload<ept id="p4">**</ept> button.
1. Закройте панель **Загрузка BLOB-объектов**, если она еще открыта, и убедитесь, что в контейнере **data** создана **product_data** виртуальная папка.
1. Выберите папку **product_data** и убедитесь, что она содержит отправленный BLOB-объект **product1.json**.
1. В левой части в разделе **Хранилище данных** выберите **Контейнеры**.
1. Откройте контейнер **data** и убедитесь, что в списке указана созданная папка **product_data**.
1. Select the <bpt id="p1">**</bpt>&amp;#x2027;&amp;#x2027;&amp;#x2027;<ept id="p1">**</ept> icon at the right-end of the folder, and note that it doesn't display any options. Folders in a flat namespace blob container are virtual, and can't be managed.
1. Используйте значок **X** в правом верхнем углу страницы **data**, чтобы закрыть страницу и вернуться на страницу **Контейнеры**.

## <a name="explore-azure-data-lake-storage-gen2"></a>Знакомство с Azure Data Lake Storage 2-го поколения

Azure Data Lake Store Gen2 support enables you to use hierarchical folders to organize and manage access to blobs. It also enables you to use Azure blob storage to host distributed file systems for common big data analytics platforms.

1. Скачайте JSON-файл [product2.json](https://aka.ms/product2.json?azure-portal=true) из `https://aka.ms/product2.json` и сохраните его на компьютере в той же папке, в которой ранее загружалось приложение **product1.json**. Вы сможете отправить его в хранилище BLOB-объектов позже.
1. С левой стороны страницы портала Azure для учетной записи хранения прокрутите экран вниз до раздела **Параметры** и выберите **Обновление Data Lake 2-го поколения**.
1. На главной странице портала Azure нажмите **&#65291; Создать ресурс** в верхнем левом углу и найдите *Учетную запись хранения*.
1. После завершения обновления в верхней части области слева выберите **Обозреватель хранилища** и вернитесь к корню контейнера BLOB-объектов **data**, который по-прежнему содержит папку **product_data**.
1. Выберите папку **product_data** и убедитесь, что она все еще содержит файл **product1.json**, который вы загрузили ранее.
1. Нажмите кнопку **&#10514; Отправить**, чтобы открыть панель **Отправить BLOB-объект**.
1. Затем на полученной странице **Службы хранилища учетной записи** выберите **Создать**.
1. Закройте панель **Отправить BLOB-объект**, если она еще открыта, и убедитесь, что в папке **product_data** теперь есть файл **product2.json**.
1. В левой части в разделе **Хранилище данных** выберите **Контейнеры**.
1. Откройте контейнер **data** и убедитесь, что в списке указана созданная папка **product_data**.
1. Щелкните значок **&#x2027;&#x2027;&#x2027;** с правого края папки и обратите внимание, что при включенном иерархическом пространстве имен можно выполнять задачи настройки на уровне папки, в том числе переименование папок и задание разрешений.
1. Используйте значок **X** в правом верхнем углу страницы **data**, чтобы закрыть страницу и вернуться на страницу **Контейнеры**.

## <a name="explore-azure-files"></a>Обзор Файлов Azure

Служба Файлов Azure предоставляет способ создания облачных файловых ресурсов.

1. На странице контейнера хранилища на портале Azure слева в разделе **Хранилище данных** выберите **Общие папки**.
1. На странице "Общие папки" выберите **&#65291; Общая папка** и добавьте новый файловый ресурс с именем **files** и уровнем **оптимизации для транзакций**.
1. В **Общих папках** откройте новую **общую папку**.
1. At the top of the page, select <bpt id="p1">**</bpt>Connect<ept id="p1">**</ept>. Then in the <bpt id="p1">**</bpt>Connect<ept id="p1">**</ept> pane, note that there are tabs for common operating systems (Windows, Linux, and macOS) that contain scripts you can run to connect to the shared folder from a client computer.
1. Закройте панель **Подключение**, а затем закройте страницу **files**, чтобы вернуться на страницу **Общих файловых ресурсов** для вашей учетной записи хранения Azure.

## <a name="explore-azure-tables"></a>Знакомство с Таблицами Azure

Таблицы Azure предоставляют хранилище "ключ/значение" для приложений, которые должны хранить значения данных, но не нуждаются в полной функциональности и структуре реляционной базы данных.

1. На странице контейнера хранилища на портале Azure слева в разделе **Хранилище данных** выберите **Таблицы**.
1. На странице **Таблицы** выберите **&#65291; Таблица** и создайте новую таблицу с именем **products**.
1. После создания таблицы **products** в верхней части области слева выберите **Обозреватель хранилища**.
1. В обозревателе хранилища выберите **Таблицы** и убедитесь, что таблица **products** указана в списке.
1. Выберите таблицу **products**.
1. На странице **products** выберите **&#65291; Добавление сущности**.
1. На панели **Добавить сущность** введите следующие значения ключей:
    - **PartitionKey**: 1
    - **RowKey**: 1
1. Выберите **Добавить свойство** и создайте новое свойство со следующими значениями:

    |Имя свойства | Тип | Значение |
    | ------------ | ---- | ----- |
    | Название | Строка | Мини-приложение |

1. Добавьте второе свойство со следующими значениями:

    |Имя свойства | Тип | Значение |
    | ------------ | ---- | ----- |
    | Цена | Double | 2,99 |

1. Нажмите кнопку **Вставить**, чтобы вставить строку для новой сущности в таблицу.
1. В обозревателе хранилища убедитесь, что строка была добавлена в таблицу **Products** и что был создан столбец **timestamp** для указания времени последнего изменения строки.
1. Добавьте еще одну сущность в таблицу **Products** со следующими свойствами:

    |Имя свойства | Тип | Значение |
    | ------------ | ---- | ----- |
    | PartitionKey | Строка | 1 |
    | RowKey | Строковый тип | 2 |
    | Имя | Строка | Kniknak |
    | Цена | Double | 1,99 |
    | Поставки прекращены | Логическое | Да |

1. После вставки новой сущности убедитесь, что в таблице показана строка, содержащая неподдерживаемый продукт.

    You have manually entered data into the table using the storage browser interface. In a real scenario, application developers can use the Azure Storage Table API to build applications that read and write values to tables, making it a cost effective and scalable solution for NoSQL storage.

> **Совет**. Когда вы завершите знакомство со службой хранилища Azure, созданную в этом упражнении группу ресурсов можно удалить.
