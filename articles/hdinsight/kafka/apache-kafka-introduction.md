---
title: "HDInsight 上的 Apache Kafka 簡介 - Azure | Microsoft Docs"
description: "了解 HDInsight 上的 Apache Kafka：它是什麼、其用途以及到何處尋找範例和入門資訊。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/04/2017
ms.author: larryfr
ms.openlocfilehash: 945b16553d56d5138b17e7768e43a298b310551d
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="introducing-apache-kafka-on-hdinsight"></a>HDInsight 上的 Apache Kafka 簡介

[Apache Kafka](https://kafka.apache.org) 是開放原始碼分散式串流平台，可用來建置即時串流資料管線和應用程式。 Kafka 也提供類似於訊息佇列的訊息代理程式功能，可讓您發佈和訂閱具名資料流。 在 HDInsight 上的 Kafka 為您在 Microsoft Azure 雲端中提供受控、高可調整性和高可用性的服務。

## <a name="why-use-kafka-on-hdinsight"></a>為何使用 HDInsight 上的 Kafka？

Kafka on HDInsight 提供下列功能︰

* __Kafka 運作時間的 99% 服務等級協定 (SLA)__：如需詳細資訊，請參閱 [HDInsight 的 SLA 資訊](https://azure.microsoft.com/support/legal/sla/hdinsight/v1_0/)文件。

* __容錯和機架感知__：Kafka 的設計使用單一維度的機架檢視，適用於某些環境。 不過，在 Azure 等環境中，一個機架會分成兩個維度 - 更新網域 (UD) 和容錯網域 (FD)。 Microsoft 提供一些工具，以確保重新平衡各 UD 和 FD 的 Kafka 資料分割和複本。 

    如需詳細資訊，請參閱[使用 HDInsight 上的 Kafka 確保高可用性](apache-kafka-high-availability.md)文件。

* **與 Azure 受控磁碟整合**：受控磁碟可為 HDInsight 上的 Kafka 所使用的磁碟提供更高的級別和輸送量 (叢集中的每個節點最多 16 TB)。

    如需使用 HDInsight 上的 Kafka 設定受控磁碟的資訊，請參閱[提高 HDInsight 上的 Kafka 延展性](apache-kafka-scalability.md)。

    如需受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟](../../virtual-machines/windows/managed-disks-overview.md)。

* **警示、監視及預測性維護**：Azure Log Analytics 可用於監視 HDInsight 上的 Kafka。 Log Analytics 會呈現虛擬機器層級資訊，例如磁碟和 NIC 計量，以及來自 Kafka 的 JMX 計量。

    如需詳細資訊，請參閱[針對 HDInsight 上的 Kafka 分析記錄](apache-kafka-log-analytics-operations-management.md)。

* **複寫 Kafka 資料**：Kafka 提供 MirrorMaker 公用程式，該公用程式可在 Kafka 叢集之間複寫資料。

    如需使用 MirrorMaker 的詳細資訊，請參閱[透過 HDInsight 上的 Kafka 複寫 Kafka 主題](apache-kafka-mirroring.md)。

* **叢集調整**：HDInsight 可讓您在叢集建立後，變更背景工作節點 (主控 Kafka-broker) 的數目。 隨著工作負載增加而相應增加叢集，或相應減少以降低成本。 您可以從 Azure 入口網站、Azure PowerShell 及其他 Azure 管理介面執行調整。 對於 Kafka，您應該在調整作業完成後重新平衡磁碟分割複本。 重新平衡資料分割可讓 Kafka 利用新的背景工作節點數。

    如需詳細資訊，請參閱[使用 HDInsight 上的 Kafka 確保高可用性](apache-kafka-high-availability.md)文件。

* **發佈-訂閱傳訊模式**︰Kafka 提供生產者 API，可將記錄發佈到 Kafka 主題。 訂閱主題時會使用取用者 API。

    如需詳細資訊，請參閱[開始使用 HDInsight 上的 Kafka](apache-kafka-get-started.md)。

* **串流處理**︰Kafka 通常與 Apache Storm 或 Spark 一起用來處理即時串流。 Kafka 0.10.0.0 (HDInsight 3.5 和 3.6 版) 引進串流 API，讓您不需要 Storm 或 Spark 就能建置串流解決方案。

    如需詳細資訊，請參閱[開始使用 HDInsight 上的 Kafka](apache-kafka-get-started.md)。

* **水平縮放**︰Kafka 可將串流分割給 HDInsight 叢集的各節點。 取用者處理程序可以與個別的資料分割相關聯，在取用記錄時可平衡負載。

    如需詳細資訊，請參閱[開始使用 HDInsight 上的 Kafka](apache-kafka-get-started.md)。

* **依序傳遞**︰在每個資料分割內，記錄會依收到時的順序儲存在串流中。 每個資料分割與一個取用者處理序建立關聯之後，就能保證依序處理記錄。

    如需詳細資訊，請參閱[開始使用 HDInsight 上的 Kafka](apache-kafka-get-started.md)。

## <a name="use-cases"></a>使用案例

* **傳訊**︰Kafka 支援發佈-訂閱傳訊模式，通常作為訊息代理程式。

* **活動追蹤**︰Kafka 能夠依序登載記錄，可用來追蹤和重新建立活動。 例如，網站或應用程式中的使用者動作。

* **彙總**︰您可以利用串流處理來彙總不同串流的資訊，將資訊結合並集中而成為可操作的資料。

* **轉換**︰您可以利用串流處理來結合並充實多個輸入主題的資料，而成為一個或多個輸出主題。

## <a name="architecture"></a>架構

![Kafka 叢集組態](./media/apache-kafka-introduction/kafka-cluster.png)

此圖顯示的典型 Kafka 組態使用取用者群組、資料分割及複寫，提供具有容錯功能的事件平行讀取。 Apache ZooKeeper 是針對並行、有彈性且低延遲的交易而建置，因為它可管理 Kafka 叢集的狀態。 Kafka 會在「主題」中儲存記錄。 記錄是由「產生者」產生，並由「取用者」取用。 產生者會從 Kafka「訊息代理程式」擷取記錄。 HDInsight 叢集中的每個背景工作節點都是 Kafka 訊息代理程式。 系統會為每個取用者建立一個磁碟分割，以允許平行處理串流資料。 複寫用於將磁碟分割分散於各節點，以防止節點 (訊息代理程式) 中斷。 以 *(L)* 表示的磁碟分割是指定之磁碟分割的前端項目。 使用 ZooKeeper 所管理的狀態，可將生產者流量路由傳送至每個節點的前端項目。

每個 Kafka 訊息代理程式都會使用 Azure 受控磁碟。 磁碟數目由使用者定義，每個訊息代理程式最多提供 16 TB 的儲存體。

> [!IMPORTANT]
> Kafka 並不知道 Azure 資料中心的基礎硬體 (機架)。 若要確保基礎硬體的磁碟分割達到適當平衡，請參閱[設定資料的高可用性 (Kafka)](apache-kafka-high-availability.md) 文件。

## <a name="next-steps"></a>後續步驟

使用下列連結以了解如何使用 HDInsight 上的 Apache Kafka：

* [開始使用 HDInsight 上的 Kafka](apache-kafka-get-started.md)

* [使用 MirrorMaker 建立 Apache Kafka on HDInsight 複本](apache-kafka-mirroring.md)

* [使用 Apache Storm 搭配 HDInsight 上的 Kafka](../hdinsight-apache-storm-with-kafka.md)

* [使用 Apache Spark 搭配 Kafka on HDInsight](../hdinsight-apache-spark-with-kafka.md)

* [透過 Azure 虛擬網路連線到 Kafka](apache-kafka-connect-vpn-gateway.md)