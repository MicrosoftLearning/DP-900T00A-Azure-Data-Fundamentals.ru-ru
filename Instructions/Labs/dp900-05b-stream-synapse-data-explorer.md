---
lab:
  title: "Знакомство с Azure\_Synapse Data\_Explorer"
  module: Explore fundamentals of real-time analytics
---

# <a name="explore-azure-synapse-data-explorer"></a>Знакомство с Azure Synapse Data Explorer

В этом упражнении вы будете использовать обозреватель данных Azure Synapse Data Explorer для анализа данных временных рядов.

Выполнение этого задания займет около **25** минут.

## <a name="before-you-start"></a>Перед началом работы

Вам потребуется [подписка Azure](https://azure.microsoft.com/free) с доступом уровня администратора.

## <a name="provision-a-synapse-analytics-workspace"></a>Создание рабочей области Synapse Analytics

> **Совет**. Если у вас все еще есть рабочая область Azure Synapse из предыдущего упражнения, пропустите этот раздел и сразу перейдите к **[Созданию пула Data Explorer](#create-a-data-explorer-pool)** .

1. Войдите на портал Azure по адресу [https://portal.azure/com](https://portal.azure.com?azure-portal=true), используя учетные данные, связанные с вашей подпиской Azure.

    >                 **Примечание**. Убедитесь, что работаете в каталоге, содержащем вашу подписку. Он указан в правом верхнем углу под идентификатором пользователя. В противном случае нажмите значок пользователя и переключите каталог.

1. На портале Azure на **домашней** странице используйте значок **&#65291; Создать ресурс**, чтобы создать новый ресурс.
1. Выполните поиск по запросу *Azure Synapse Analytics* и создайте хранилище **Azure Synapse Analytics** с приведенными ниже параметрами.
    - **Подписка**. *Ваша подписка Azure*
        - **Группа ресурсов** — *создайте новую группу ресурсов с подходящим именем, например "synapse-rg".*
        - **Управляемая группа ресурсов** — *введите подходящее имя, например "synapse-managed-rg".*
    - **Имя рабочей области** — *введите уникальное имя рабочей области, например "synapse-ws-<vashe_imya>".*
    - **Регион** — *выберите любой доступный регион.*
    - **Выбор Data Lake Storage 2-го поколения** — из подписки.
        - **Имя учетной записи** — *создайте новую учетную запись с уникальным именем, например "datalake<vashe_imya>".*
        - **Имя файловой системы** — *создайте новую файловую систему с уникальным именем, например "fs<vashe_imya>".*

    >                 **Примечание**. Для рабочей области Synapse Analytics требуются две группы ресурсов в подписке Azure: одна для ресурсов, явно создаваемых вами, а другая — для управляемых ресурсов, используемых службой. Для нее также необходима учетная запись хранения Data Lake, в которой она будет хранить данные, скрипты и другие артефакты.

1. После ввода этих сведений выберите **Просмотр и создание**, а затем выберите **Создать**, чтобы создать рабочую область.
1. Дождитесь создания рабочей области. Это займет около пяти минут.
1. После завершения развертывания перейдите к созданной группе ресурсов и обратите внимание, что она содержит рабочую область Synapse Analytics и учетную запись хранения Data Lake.
1. Выберите рабочую область Synapse и на странице **Обзор** в карточке **Открыть Synapse Studio** выберите **Открыть**, чтобы открыть Synapse Studio на новой вкладке браузера. Synapse Studio — это веб-интерфейс, с помощью которого можно использовать рабочую область Synapse Analytics.
1. В левой части Synapse Studio нажмите на значок **&rsaquo;&rsaquo;** , чтобы развернуть меню. В нем содержатся различные страницы Synapse Studio, которые вы будете использовать для управления ресурсами и выполнения задач аналитики данных.

## <a name="create-a-data-explorer-pool"></a>Создание пула Data Explorer

1. В Synapse Studio выберите страницу **Управление**.
1. Перейдите на вкладку **Пулы Data Explorer**, а затем используйте значок **&#65291; Создать**, чтобы создать новый пул со следующими параметрами:
    - **Имя пула Data Explorer**: dxpool
    - **Рабочая нагрузка**: оптимизированная для вычислений
    - **Размер**: очень маленький (2 ядра)
1. Выберите **Далее: Дополнительные параметры >** и включите **Прием потоковой передачи**. Это позволит Data Explorer принимать новые данные из источника потоковой передачи, например из Центров событий Azure.
1. Выберите **Проверить и создать**, чтобы создать пул Data Explorer, а затем дождитесь его развертывания (это может занять 15 минут или более). Состояние изменится с *Создание* на *Готово*.

## <a name="create-a-database-and-ingest-data"></a>Создание базы данных и прием данных

1. В Synapse Studio выберите страницу **Данные**.
1. Убедитесь, что выбрана вкладка **Рабочая область**, и при необходимости щелкните значок **&#8635;** в левом верхнем углу страницы, чтобы обновить представление и отобразить **Базы данных Data Explorer**.
1. Разверните **Базы данных Data Explorer** и убедитесь, что в списке указан пул **dxpool**.
1. На панели **Данные** используйте значок **&#65291;** , чтобы создать в пуле **dxpool** новую **базу данных Data Explorer** с именем **iot-data**.
1. Пока ожидается создание базы, скачайте файл **devices.csv** по адресу [https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/data/devices.csv](https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/data/devices.csv?azure-portal=true) и сохраните его в любой папке на локальном компьютере.
1. В Synapse Studio дождитесь создания базы данных, если это необходимо, а затем в меню **...** для новой базы данных **iot-data** выберите **Открыть в Azure Data Explorer**.
1. На новой вкладке браузера, содержащей Azure Data Explorer, на вкладке **Данные** выберите **Принять новые данные**.
1. На странице **Назначение** выберите следующие параметры:
    - **Кластер**: *пул Data Explorer **dxpool** в рабочей области Azure Synapse*.
    - **База данных**: iot-data
    - **Таблица**: создание новой таблицы с именем **devices**
1. Выберите **Далее: источник** и на странице **источник** выберите следующие параметры:
    - **Тип источника**: файл
    - **Файлы**: Загрузите файл **devices.csv** с локального компьютера.
1. Выберите **Далее: Схема** и на странице **Схема** убедитесь, что следующие параметры заданы верно.
    - **Тип сжатия**: без сжатия
    - **Формат данных**: CSV
    - **Пропускать первую запись**: выбрано
    - **Сопоставление**: devices_mapping
1. Убедитесь, что типы данных столбца правильно определены как *время (DateTime)*, *устройство (строка)* и *значение (Long)*). Затем нажмите кнопку **Далее: начать прием**.
1. По завершении приема нажмите кнопку **Закрыть**.
1. В Azure Data Explorer на вкладке **Запрос** убедитесь, что выбрана база данных **iot-data**, а затем на панели запроса введите следующий запрос.

    ```kusto
    devices
    ```

1. На панели инструментов нажмите **&#9655; Запуск**, чтобы выполнить запрос, и просмотрите результаты, которые должны выглядеть примерно так:

    | время; | Устройство | Значение |
    | --- | --- | --- |
    | 2022-01-01T00:00:00Z | Dev1 | 7 |
    | 2022-01-01T00:00:01Z | Dev2 | 4 |
    | ... | ... | ... |

    Если результаты такие же, вы успешно создали таблицу **Устройства** из данных в файле.

    >                 **Совет**. В этом примере вы импортировали из файла лишь небольшой объем пакетных данных, что подходит для целей этого упражнения. На практике можно использовать Data Explorer для анализа больших объемов данных, а так как вы включили прием потоковой передачи, можно также настроить Data Explorer для приема данных в таблицу из источника потоковой передачи, такого как Центры событий Azure.

## <a name="use-kusto-query-language-to-query-the-table-in-synapse-studio"></a>Использование языка запросов Kusto для запроса таблицы в Synapse Studio

1. Закройте в браузере вкладку Azure Data Explorer и вернитесь на вкладку Synapse Studio.
1. На странице **Данные** разверните базу данных **iot-data** и папку **Tables (таблицы)** в ней. Затем в меню **...** для таблицы **Devices (устройства)** выберите **новый KQL-скрипт** > ** Принимать 1000 строк**.
1. Проверьте созданный запрос и его результаты. Он должен содержать следующий код:

    ```kusto
    devices
    | take 1000
    ```

    Результаты запроса содержат первые 1000 строк данных.

1. Измените запрос следующим образом:

    ```kusto
    devices
    | where Device == 'Dev1'
    ```

1. Нажмите **&#9655; Запуск**, чтобы выполнить запрос. Затем просмотрите результаты, которые должны содержать только строки для устройства *Dev1*.

1. Измените запрос следующим образом:

    ```kusto
    devices
    | where Device == 'Dev1'
    | where Time > datetime(2022-01-07)
    ```

1. Выполните запрос и проверьте результаты, которые должны содержать только строки для устройства *Dev1* позже чем 7 января 2022 г.

1. Измените запрос следующим образом:

    ```kusto
    devices
    | where Time between (datetime(2022-01-01 00:00:00) .. datetime(2022-07-01 23:59:59))
    | summarize AvgVal = avg(Value) by Device
    | sort by Device asc
    ```

1. Выполните запрос и проверьте результаты, которые должны содержать среднее значение устройства, записанное между 1 января и 7 января 2022 г. в порядке возрастания имени устройства.

1. Закройте вкладку запроса KQL, отменив изменения.

## <a name="delete-azure-resources"></a>Удаление ресурсов Azure

Теперь, когда вы завершили изучение Azure Synapse Analytics, вы должны удалить созданные ресурсы, чтобы избежать ненужных затрат на Azure.

1. Закройте вкладку браузера Synapse Studio, не сохраняя изменений, и вернитесь на портал Azure.
1. На **домашней** странице портала Azure выберите **Группы ресурсов**.
1. Выберите группу ресурсов для рабочей области Synapse Analytics (не управляемую группу ресурсов) и убедитесь, что в ней есть рабочая область Synapse, учетная запись хранения и пул Data Explorer для вашей рабочей области (если вы выполнили предыдущее упражнение, она также будет содержать пул Spark).
1. В верхней части страницы **Обзор** группы ресурсов выберите **Удалить группу ресурсов**.
1. Введите имя группы ресурсов, чтобы подтвердить ее удаление, и выберите **Удалить**.

    Через несколько минут рабочая область Azure Synapse и связанная с ней управляемая рабочая область будут удалены.