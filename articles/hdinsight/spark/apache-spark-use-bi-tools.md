---
title: "在 Azure HDInsight 上使用資料視覺效果工具的 Spark BI | Microsoft Docs"
description: "透過 HDInsight 叢集上的 Apache Spark BI 使用分析的資料視覺效果工具"
keywords: "apache spark bi, spark bi, spark 資料視覺效果, spark 商業智慧"
services: hdinsight
documentationcenter: 
author: mumian
manager: cgronlun
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2017
ms.author: jgao
ms.openlocfilehash: 074415ba50ecdb1799093a3ead3bdd22fd02cc15
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a>使用資料視覺效果工具搭配 Azure HDInsight 的 Apache Spark BI

了解如何使用 [Microsoft Power BI](http://powerbi.microsoft.com) 和 [Tableau](http://www.tableau.com) \(英文\) 在 Azure HDInsight 上對 Apache Spark 叢集中的資料進行視覺化。

## <a name="prerequisites"></a>先決條件

* **完成[在 HDInsight 中的 Spark 叢集上執行互動式查詢](./apache-spark-load-data-run-query.md)**一文。
* **Power BI**：[Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/) 與 [Power BI 試用訂用帳戶](https://app.powerbi.com/signupredirect?pbi_source=web) (選擇性)。
* **Tableau**：[Tableau Desktop](http://www.tableau.com/products/desktop) \(英文\) 與 [Microsoft Spark ODBC 驅動程式](http://go.microsoft.com/fwlink/?LinkId=616229) \(英文\)。


## <a name="hivetable"></a>驗證資料

您在[上一個教學課程](apache-spark-load-data-run-query.md)中建立的 Jupyter Notebook 包含可建立 `hvac` 資料表的程式碼。 本資料表根據的是 **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv** 上所有 HDInsight Spark 叢集上的可用 CSV 檔案。 使用下列程序來驗證資料。

1. 從 Jupyter Notebook 貼上下列程式碼，然後按下 **SHIFT + ENTER** 鍵。 該程式碼會驗證資料表是否存在。

    ```PySpark
    %%sql
    SHOW TABLES
    ```

    輸出看起來如下：

    ![顯示 Spark 中的資料表](./media/apache-spark-use-bi-tools/show-tables.png)

    如果在開始本教學課程之前關閉 Notebook，則會清除 `hvactemptable`，因此其不會包含在輸出中。
    從 BI 工具只可以存取儲存在中繼存放區的 Hive 資料表 (在 **isTemporary** 資料行下表示為 **False**)。 在此教學課程中，您會連線到您所建立的 **hvac** 資料表。

2. 將以下程式碼貼入空白儲存格，然後按下 **SHIFT + ENTER** 鍵。 該程式碼會驗證資料表中的資料。

    ```PySpark
    %%sql
    SELECT * FROM hvac LIMIT 10
    ```

    輸出看起來如下：

    ![顯示 Spark 中 hvac 資料表的資料列](./media/apache-spark-use-bi-tools/select-limit.png)

3. 從 Notebook 的 [檔案] 功能表中，按一下 [關閉並終止]。 關閉 Notebook 來釋放資源。 















## <a name="powerbi"></a>使用 Power BI

在本節中，您會使用 Power BI 從 Spark 叢集資料建立視覺效果、報表及儀表板。 

### <a name="create-a-report-in-power-bi-desktop"></a>在 Power BI Desktop 中建立報表
使用 Spark 的第一步是連接到 Power BI Desktop 中的叢集，從叢集載入資料，並根據該資料建立基本視覺效果。

> [!NOTE]
> 本文中所示範的連接器目前為預覽版本。 請透過 [Power BI 社群](https://community.powerbi.com/) \(英文\) 網站或 [Power BI Ideas](https://ideas.powerbi.com/forums/265200-power-bi-ideas) \(英文\) 提供您的意見反應。

1. 開啟 [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/)。
1. 按一下 [首頁] 索引標籤中的 [取得資料]，然後按一下 [更多]。

    ![將資料從 HDInsight Apache Spark 送入 Power BI Desktop](./media/apache-spark-use-bi-tools/hdinsight-spark-power-bi-desktop-get-data.png "將資料從 Apache Spark BI 送入 Power BI")


2. 在搜尋方塊中輸入 `Spark`，選取 [Azure HDInsight Spark (搶鮮版 (Beta))]，然後按一下 [連線]。

    ![將資料從 Apache Spark BI 送入 Power BI](./media/apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "將資料從 Apache Spark BI 送入 Power BI")

3. 輸入您的叢集 URL (格式為 `mysparkcluster.azurehdinsight.net`)，選取 [DirectQuery]，然後按一下 [確定]。

    您可以搭配 Spark 使用任一種資料連線模式。 如果您使用 DirectQuery，變更會反映在報表中，而不需重新整理整個資料集。 如果您是匯入資料，則必須重新整理資料集，才能看到變更。 如需如何使用以及該在何時使用 DirectQuery 的詳細資訊，請參閱[使用 Power BI 中的 DirectQuery](https://powerbi.microsoft.com/documentation/powerbi-desktop-directquery-about/)。 

4. 輸入 HDInsight 登入帳戶資訊，然後按一下 [連線]。 預設帳戶名稱為 *admin*。

5. 選取 `hvac` 資料表，等待查看資料的預覽，然後按一下 [載入]。

    ![Spark 叢集使用者名稱和密碼](./media/apache-spark-use-bi-tools/apache-spark-bi-select-table.png "Spark 叢集使用者名稱和密碼")

    Power BI Desktop 擁有連線至 Spark 叢集以及從 `hvac` 資料表載入資料所需的資訊。 資料表及其資料行會顯示在 [欄位] 窗格中。  請參閱下列螢幕擷取畫面：

6. 將每棟建築物之目標溫度和實際溫度間的差異視覺化： 

    1. 在 [視覺效果] 窗格中，選取 [區域圖]。 
    2. 將 [BuildingID] 欄位拖曳至 [軸]，並將 [ActualTemp] 和 [TargetTemp] 欄位拖曳至 [值]。

        ![使用 Apache Spark BI 建立 Spark 資料視覺效果](./media/apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "使用 Apache Spark BI 建立 Spark 資料視覺效果")

        圖表看起來如下：

        ![使用 Apache Spark BI 建立 Spark 資料視覺效果](./media/apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "使用 Apache Spark BI 建立 Spark 資料視覺效果")

        根據預設，視覺效果會顯示 **ActualTemp** 和 **TargetTemp** 的總和。 在 [視覺效果] 窗格中，按一下 [ActualTemp] 與 [TargetTemp] 旁的向下箭頭，您會看到已選取 [總和]。

    3. 在 [視覺效果] 窗格中，按一下 [ActualTemp] 與 [TargetTemp] 旁的向下箭頭，選取 [平均值] 以取得每棟建築物之實際溫度與目標溫度的平均值。

        ![使用 Apache Spark BI 建立 Spark 資料視覺效果](./media/apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "使用 Apache Spark BI 建立 Spark 資料視覺效果")

        您的資料視覺效果應該類似於螢幕擷取畫面中的視覺效果。 在視覺效果上移動游標可取得相關資料的工具提示。

        ![使用 Apache Spark BI 建立 Spark 資料視覺效果](./media/apache-spark-use-bi-tools/apache-spark-bi-area-graph-sum.png "使用 Apache Spark BI 建立 Spark 資料視覺效果")

7. 按一下 [檔案]，然後 [儲存]，並輸入檔案名稱 `BuildingTemperature.pbix`。 

### <a name="publish-the-report-to-the-power-bi-service-optional"></a>將報告發佈至 Power BI 服務 (選用)

Power BI 服務可讓您跨組織共用報表和儀表板。 在本節中，您會首次發佈資料集和報表。 然後，您會將報表釘選到儀表板。 儀表板通常用於強調報告中的資料子集；您的報告中只有一個視覺效果，但逐步了解下列步驟仍很有幫助。

1. 開啟 Power BI Desktop。
2. 在 [首頁] 索引標籤上，按一下 [發佈]。

    ![從 Power BI Desktop 發佈](./media/apache-spark-use-bi-tools/apache-spark-bi-publish.png "從 Power BI Desktop 發佈")

2. 選取要發佈您的資料集和報告的目標工作區，然後按一下 [選取]。 在下列映像中，已選取預設值 [我的工作區]。

    ![選取要發佈資料集和報表的目標工作區](./media/apache-spark-use-bi-tools/apache-spark-bi-select-workspace.png "選取要發佈資料集和報表的目標工作區") 

3. 成功發佈之後，按一下 [在 Power BI 中開啟 'BuildingTemperature.pbix']。

    ![發佈成功，按一下以輸入認證](./media/apache-spark-use-bi-tools/apache-spark-bi-publish-success.png "發佈成功，按一下以輸入認證") 

4. 在 Power BI 服務中，按一下 [輸入認證]。

    ![在 Power BI 服務中輸入認證](./media/apache-spark-use-bi-tools/apache-spark-bi-enter-credentials.png "在 Power BI 服務中輸入認證")

5. 按一下 [編輯認證]。

    ![在 Power BI 服務中編輯認證](./media/apache-spark-use-bi-tools/apache-spark-bi-edit-credentials.png "在 Power BI 服務中編輯認證")

6. 輸入 HDInsight 登入帳戶資訊，然後按一下 [登入]。 預設帳戶名稱為 *admin*。

    ![登入 Spark 叢集](./media/apache-spark-use-bi-tools/apache-spark-bi-sign-in.png "登入 Spark 叢集")

7. 在左側窗格中，移至 [工作區] > [我的工作區] > [報表]，然後按一下 [BuildingTemperature]。

    ![左側窗格中報告下列出的報表](./media/apache-spark-use-bi-tools/apache-spark-bi-service-left-pane.png "左側窗格中報表下列出的報告")

    您也應該會看到 [BuildingTemperature] 列於左側窗格中 [資料集] 底下。

    現在您在 Power BI Desktop 中建立的視覺效果已可於 Power BI 服務中使用。 

8. 將游標暫留在視覺效果上，然後按一下右上角的釘選圖示。

    ![Power BI 服務中的報告](./media/apache-spark-use-bi-tools/apache-spark-bi-service-report.png "Power BI 服務中的報告")

9. 選取 [新的儀表板]，輸入名稱 `Building temperature`，然後按一下 [釘選]。

    ![釘選到新的儀表板](./media/apache-spark-use-bi-tools/apache-spark-bi-pin-dashboard.png "釘選到新的儀表板")

10. 在報告中，按一下 [移至儀表板]。 

您的視覺效果已釘選至儀表板 - 您可以將其他視覺效果新增至報告，並將其釘選至相同的儀表板。 如需關於報告與儀表板的詳細資訊，請參閱 [Power BI 中的報告](https://powerbi.microsoft.com/documentation/powerbi-service-reports/)和 [Power BI 中的儀表板](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)。

## <a name="tableau"></a>使用 Tableau Desktop 

> [!NOTE]
> 本節只適用於在 Azure HDInsight 中建立的 Spark 1.5.2 叢集。
>
>

1. 在執行本 Apache Spark BI 教學課程的電腦上安裝 [Tableau Desktop](http://www.tableau.com/products/desktop)。

2. 確保這部電腦也也安裝 Microsoft Spark ODBC 驅動程式。 您可以前往 [這裡](http://go.microsoft.com/fwlink/?LinkId=616229)來安裝驅動程式。

1. 啟動 Tableau Desktop。 在左窗格上可連線的伺服器清單中，按一下 [Spark SQL] 。 如果左窗格沒有預設列出 Spark SQL，您可以按一下 [更多伺服器] 來尋找它。
2. 在 Spark SQL 連線對話方塊中，提供螢幕擷取畫面中所示的值，然後按一下 [確定]。

    ![連線至 Apache Spark BI 的叢集](./media/apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "連線至 Apache Spark BI 的叢集")

    您必須先在電腦上安裝 [Microsoft Spark ODBC 驅動程式](http://go.microsoft.com/fwlink/?LinkId=616229)，驗證下拉式清單中才會出現 **Microsoft Azure HDInsight 服務**。
3. 在下一個畫面中，按一下 [結構描述] 下拉式清單的 [尋找] 圖示，然後按一下 [預設]。

    ![尋找 Apache Spark BI 的結構描述](./media/apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "尋找 Apache Spark BI 的結構描述")
4. 對於 [資料表] 欄位，再次按一下 [尋找] 圖示以列出叢集中所有可用的 Hive 資料表。 您應該會看到自己先前使用 Notebook 建立的 **hvac** 資料表。

    ![尋找 Apache Spark BI 的資料表](./media/apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "尋找 Apache Spark BI 的資料表")
5. 將資料表拖放到右側頂端的方塊。 Tableau 會匯入資料，並以紅色方塊反白顯示結構描述。

    ![將資料表新增至 Apache Spark BI 的 Tableau](./media/apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "將資料表新增至 Apache Spark BI 的 Tableau")
6. 按一下左下方的 [Sheet1]  索引標籤。 針對每個日期，製作出顯示所有建築物之平均目標溫度和實際溫度的視覺效果。 請把 [日期] 和 [建築物識別碼] 拖放到 [資料行] 中，然後將 [實際溫度]/[目標溫度] 拖放到 [資料列] 中。 請選取 [標記] 下方的 [區域]，以使用 Spark 資料視覺效果的區域對應圖。

     ![新增 Spark 資料視覺效果的欄位](./media/apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "新增 Spark 資料視覺效果的欄位")
7. 根據預設，溫度欄位以彙總形式顯示。 如果想要改為顯示平均溫度，您可以從下拉式清單操作，如下列螢幕擷取畫面所示：

    ![採取 Spark 資料視覺效果的平均溫度](./media/apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "採取 Spark 資料視覺效果的平均溫度")

8. 您也可以將溫度對應加諸在其他對應之上，凸顯目標溫度和實際溫度之間的差異。 將滑鼠游標移至區域圖下半部的角落，直到控點形狀出現為止 (如紅色圓圈所標示)。 把對應圖拖曳到另一個對應圖的頂端，然後在您看到紅色圓圈中所示的形狀時，放開滑鼠按鍵。

    ![合併 Spark 資料視覺效果的對應圖](./media/apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "合併 Spark 資料視覺效果的對應圖")

     資料視覺效果應會變更，如底下螢幕擷取畫面所示：

    ![Spark 資料視覺效果的 Tableau 輸出](./media/apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Spark 資料視覺效果的 Tableau 輸出")
9. 按一下 [儲存]  以儲存工作表。 您可以建立儀表板，並在儀表板中加入一個或多個工作表。

## <a name="next-steps"></a>後續步驟

到目前為止，您學會了如何建立叢集、建立 Spark 資料框架來查詢資料，然後從 BI 工具中存取該資料。 您現在可以看看如何管理叢集資源，以及對在 HDInsight Spark 叢集中執行的工作進行偵錯的指示。

* [在 Azure HDInsight 中管理 Apache Spark 叢集的資源](apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](apache-spark-job-debugging.md)

