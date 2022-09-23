---
lab:
  title: "Изучение основ визуализации данных с помощью Power\_BI"
  module: Explore fundamentals of data visualization
---

# <a name="explore-fundamentals-of-data-visualization-with-power-bi"></a>Изучение основ визуализации данных с помощью Power BI

В этом упражнении вы будете использовать Microsoft Power BI Desktop для создания модели данных и отчета, содержащего интерактивные визуализации данных.

Выполнение этого задания займет около **20** минут.

## <a name="before-you-start"></a>Перед началом работы

Вам потребуется [подписка Azure](https://azure.microsoft.com/free) с доступом уровня администратора.

### <a name="install-power-bi-desktop"></a>Установка Power BI Desktop

Если Microsoft Power BI Desktop еще не установлен на компьютере на основе Windows, его можно скачать и установить бесплатно.

1. Скачайте установщик Power BI Desktop отсюда: [https://aka.ms/power-bi-desktop](https://aka.ms/power-bi-desktop?azure-portal=true).
1. When the file has downloaded, open it, and use the setup wizard to install Power BI Desktop on your computer. This insatllation may take a few minutes.

## <a name="import-data"></a>Импорт данных

1. Open Power BI Desktop. The application interface should look similar to this:

    ![Снимок начального экрана Power BI Desktop.](images/power-bi-start.png)

    Теперь все готово для импорта данных для отчета.

1. На экране приветствия Power BI Desktop выберите **Получить данные**, а затем в списке источников данных выберите **Интернет**, а затем — **Подключить**.

    ![Снимок экрана с выбором Интернета в качестве источника данных Power BI.](images/web-source.png)

1. В диалоговом окне **Из Интернета** введите следующий URL-адрес и нажмите кнопку **OK**.

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/customers.csv
    ```

1. В диалоговом окне "Доступ к веб-содержимому" выберите **Подключить**.

1. Verify that the URL opens a dataset containing customer data, as shown below. Then select <bpt id="p1">**</bpt>Load<ept id="p1">**</ept> to load the data into the data model for your report.

    ![Снимок экрана с набором клиентских данных в Power BI.](images/customers.png)

1. В главном окне Power BI Desktop в меню "Данные" выберите **Получение данных**, а затем — **Интернет**:

    ![Снимок экрана с меню "Получение данных" в Power BI.](images/get-data.png)

1. В диалоговом окне **Из Интернета** введите следующий URL-адрес и нажмите кнопку **OK**.

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/products.csv
    ```

1. В диалоговом окне выберите **Загрузить**, чтобы загрузить данные о продуктах из этого файла в модель данных.

1. Повторите предыдущие три шага, чтобы импортировать третий набор данных, содержащий данные о заказах, по следующему URL-адресу:

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/orders.csv
    ```

## <a name="explore-a-data-model"></a>Изучение модели данных

В модель данных загружены три таблицы импортированных данных, которые теперь можно исследовать и уточнять.

1. In Power BI Desktop, on the left-side edge, select the <bpt id="p1">**</bpt>Model<ept id="p1">**</ept> tab, and then arrange the tables in the model so you can see them. You can hide the panes on the right side by using the <bpt id="p1">**</bpt><ph id="ph1">&gt;&gt;</ph><ept id="p1">**</ept> icons:

    ![Снимок экрана с вкладкой "Модель" в Power BI.](images/model-tab.png)

1. В таблице **orders** выберите поле **Revenue**, а затем на панели **Свойства** задайте для свойства **Формат** значение **Валюта**.

    ![Снимок экрана Power BI с указанием формата "Валюта" для поля Revenue.](images/revenue-currency.png)

    Это обеспечит отображение значений дохода как валюты в визуализациях отчета.

1. In the products table, right-click the <bpt id="p1">**</bpt>Category<ept id="p1">**</ept> field (or open its <bpt id="p2">**</bpt><ph id="ph1">&amp;vellip;</ph><ept id="p2">**</ept> menu) and select <bpt id="p3">**</bpt>Create hierarchy<ept id="p3">**</ept>. This step creates a hierarchy named <bpt id="p1">**</bpt>Category Hierarchy<ept id="p1">**</ept>. You may need to expand or scroll in the <bpt id="p1">**</bpt>products<ept id="p1">**</ept> table to see this - you can also see it in the <bpt id="p2">**</bpt>Fields<ept id="p2">**</ept> pane:

    ![Снимок экрана Power BI с добавлением иерархии категорий.](images/category-hierarchy.png)

1. In the products table, right-click the <bpt id="p1">**</bpt>ProductName<ept id="p1">**</ept> field (or open its <bpt id="p2">**</bpt><ph id="ph1">&amp;vellip;</ph><ept id="p2">**</ept> menu) and select <bpt id="p3">**</bpt>Add to hierarchy<ept id="p3">**</ept><ph id="ph2"> &gt; </ph><bpt id="p4">**</bpt>Category Hierarchy<ept id="p4">**</ept>. This adds the <bpt id="p1">**</bpt>ProductName<ept id="p1">**</ept> field to the hierarchy you created previously.
1. In the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, right-click <bpt id="p2">**</bpt>Category Hierarchy<ept id="p2">**</ept> (or open its <bpt id="p3">**</bpt>...<ept id="p3">**</ept> menu) and select <bpt id="p4">**</bpt>Rename<ept id="p4">**</ept>. Then rename the hierarchy to <bpt id="p1">**</bpt>Categorized Product<ept id="p1">**</ept>.

    ![Снимок экрана с переименованием иерархии в Power BI.](images/rename-hierarchy.png)

1. У левого края выберите вкладку **Данные**, а затем в области **Поля** выберите таблицу **customers**.
1. Выберите заголовок столбца **City**, а затем задайте для его свойства **Категория данных** значение **City**:

    ![Снимок экрана с заданием категории данных в Power BI.](images/data-category.png)

    Это обеспечит интерпретацию значений в этом столбце как названий городов, что может быть полезно, если предполагается добавление визуализаций карт.

## <a name="create-a-report"></a>Создание отчета

Now you're almost ready to create a report. First you need to check some settings to ensure all visualizations are enabled.

1. On the <bpt id="p1">**</bpt>File<ept id="p1">**</ept> menu, select <bpt id="p2">**</bpt>Options and Settings<ept id="p2">**</ept>. Then select <bpt id="p1">**</bpt>Options<ept id="p1">**</ept>, and in the <bpt id="p2">**</bpt>Security<ept id="p2">**</ept> section, ensure that <bpt id="p3">**</bpt>Use Map and Filled Map visuals<ept id="p3">**</ept> is enabled and select <bpt id="p4">**</bpt>OK<ept id="p4">**</ept>.

    ![Снимок экрана с заданием свойства "Использование визуальных элементов карты и картограммы" в Power BI.](images/set-options.png)

    Этот параметр обеспечит возможность включения визуализаций карт в отчеты.

1. У левого края выберите вкладку **Отчет** и просмотрите интерфейс конструктора отчетов.

    ![Снимок экрана с вкладкой отчета в Power BI.](images/report-tab.png)

1. In the ribbon, above the report design surface, select <bpt id="p1">**</bpt>Text Box<ept id="p1">**</ept> and add a text box containing the text <bpt id="p2">**</bpt>Sales Report<ept id="p2">**</ept> to the report. Format the text to make it bold with a font size of 32.

    ![Снимок экрана с добавлением текстового поля в Power BI.](images/text-box.png)

1. После загрузки файла откройте его и используйте мастер установки, чтобы установить Power BI Desktop на компьютере.

    ![Снимок экрана с добавлением таблицы классифицируемых продуктов в отчет Power BI.](images/categorized-products-table.png)

1. Установка может занять несколько минут.

    The revenue is formatted as currency, as you specified in the model. However, you didn't specify the number of decimal places, so the values include fractional amounts. It won't matter for the visualizations you're going to create, but you could go back to the <bpt id="p1">**</bpt>Model<ept id="p1">**</ept> or <bpt id="p2">**</bpt>Data<ept id="p2">**</ept> tab and change the decimal places if you wish.

    ![Снимок экрана с таблицей классифицируемых продуктов и дохода в отчете.](images/revenue-column.png)

1. With the table still selected, in the <bpt id="p1">**</bpt>Visualizations<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>Stacked column chart<ept id="p2">**</ept> visualization. The table is changed to a column chart showing revenue by category.

    ![Снимок экрана гистограммы с накоплением для классифицируемых продуктов и дохода в отчете.](images/stacked-column-chart.png)

1. Откройте Power BI Desktop.

    ![Снимок экрана гистограммы с детализацией для просмотра продуктов в категории.](images/drill-down.png)

1. Интерфейс приложения должен выглядеть следующим образом:
1. Select a blank area of the report, and then in the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>Quantity<ept id="p2">**</ept> field in the <bpt id="p3">**</bpt>orders<ept id="p3">**</ept> table and the <bpt id="p4">**</bpt>Category<ept id="p4">**</ept> field in the <bpt id="p5">**</bpt>products<ept id="p5">**</ept> table. This step results in another column chart showing sales quantity by product category.
1. Выбрав новую гистограмму, в области **Визуализации** выберите **Круговая диаграмма**, а затем измените размер диаграммы и поместите ее рядом с диаграммой дохода по категориям.

    ![Снимок экрана с круговой диаграммой объема продаж по категориям.](images/category-pie-chart.png)

1. Select a blank area of the report, and then in the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>City<ept id="p2">**</ept> field in the <bpt id="p3">**</bpt>customers<ept id="p3">**</ept> table and then select the <bpt id="p4">**</bpt>Revenue<ept id="p4">**</ept> field in the <bpt id="p5">**</bpt>orders<ept id="p5">**</ept> table. This results in a map showing sales revenue by city. Rearrange and resize the visualizations as needed:

    ![Снимок экрана с картой, показывающей доход по городам.](images/revenue-map.png)

1. In the map, note that you can drag, double-click, use a mouse-wheel, or pinch and drag on a touch screen to interact. Then select a specific city, and note that the other visualizations in the report are modified to highlight the data for the selected city.

    ![Снимок экрана с картой, показывающей доход по городам, и выделенными данными для выбранного города.](images/selected-data.png)

1. On the <bpt id="p1">**</bpt>File<ept id="p1">**</ept> menu, select <bpt id="p2">**</bpt>Save<ept id="p2">**</ept>. Then save the file with an appropriate .pbix file name. You can open the file and explore data modeling and visualization further at your leisure.

Если у вас есть подписка на [службу Power BI](https://www.powerbi.com/?azure-portal=true), вы можете войти в свою учетную запись и опубликовать отчет в рабочей области Power BI. 
