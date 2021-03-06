---
title: "監視 XTP 記憶體內儲存體 | Microsoft Docs"
description: "估計和監視 XTP 記憶體內儲存體使用量、容量；解決容量錯誤 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2018
ms.author: jodebrui
ms.openlocfilehash: 1e7088e80cc86e3c7cf8ae8ea180d797de613e71
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="monitor-in-memory-oltp-storage"></a>監視記憶體內部 OLTP 儲存體
使用 [記憶體內部 OLTP](sql-database-in-memory.md)時，記憶體最佳化資料表中的資料和資料表變數位於記憶體內部 OLTP 儲存體中。 每個進階服務層都有最大的記憶體內部 OLTP 儲存體大小，如[單一資料庫資源限制](sql-database-resource-limits.md#single-database-storage-sizes-and-performance-levels)與[彈性集區資源限制](sql-database-resource-limits.md#elastic-pool-change-storage-size)所說明。 一旦超過此限制，插入和更新作業就可能會開始失敗，並出現錯誤 41823 (適用於獨立資料庫) 和錯誤 41840 (適用於彈性集區)。 屆時您需要將資料刪除以回收記憶體，或將資料庫的效能層級升級。

## <a name="determine-whether-data-fits-within-the-in-memory-oltp-storage-cap"></a>判斷資料是否在記憶體內部 OLTP 儲存容量上限內
判斷不同進階服務層的儲存體上限。 請參閱[單一資料庫資源限制](sql-database-resource-limits.md#single-database-storage-sizes-and-performance-levels)和[彈性集區資源限制](sql-database-resource-limits.md#elastic-pool-change-storage-size)。

估計記憶體最佳化資料表的記憶體需求，其方式如同在 Azure SQL Database 中估計 SQL Server 的記憶體需求。 花幾分鐘時間在 [MSDN](https://msdn.microsoft.com/library/dn282389.aspx) 上檢閱該文章。

資料表和資料表變數資料列以及索引，都會計入最大的使用者資料大小。 此外，ALTER TABLE 需要足夠的空間來建立新版的完整資料表及其索引。

## <a name="monitoring-and-alerting"></a>監視和警示
您可以在 [Azure 入口網站](https://portal.azure.com/)中，透過效能層的儲存體上限百分比來監視記憶體內部儲存體使用情形： 

1. 在 [資料庫] 刀鋒視窗上，找出 [資源使用率方塊] 並按一下 [編輯]。
2. 選取計量 `In-Memory OLTP Storage percentage`。
3. 若要新增警示，請按一下 [資源使用率] 方塊以開啟 [計量] 刀鋒視窗，然後按一下 [新增警示]。

或使用下列查詢來顯示記憶體內部儲存體使用率：

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-in-memory-oltp-storage-situations---errors-41823-and-41840"></a>更正記憶體內部 OLTP 儲存體不足之狀況 - 錯誤 41823 和 41840
在資料庫中達到記憶體內部 OLTP 儲存體上限時，會造成 INSERT、UPDATE、ALTER 和 CREATE 作業失敗，並出現錯誤訊息 41823 (適用於獨立資料庫) 或錯誤 41840 (適用於彈性集區)。 這兩個錯誤都會造成使用中的交易中止。

錯誤訊息 41823 和 41840 表示經記憶體最佳化的資料表以及資料庫或集區中的資料表變數，已達到記憶體內部 OLTP 儲存體大小的上限。

若要解決此錯誤，您可以：

* 從記憶體最佳化資料表中刪除資料，可能會將資料卸載至傳統、以磁碟為基礎的資料表；或者，
* 將服務層升級至具有足夠記憶體內部記憶體的服務層，以便儲存您需要保留在記憶體最佳化資料表中的資料。

> [!NOTE] 
> 在極少數的情況下，41823 和 41840 錯誤可能是暫時性的，這表示可用的記憶體內部 OLTP 儲存體是足夠的，重試此作業即可成功。 因此，建議您除了監視整體可用的記憶體內部 OLTP 儲存體，也要在首次遇到 41823 或 41840 錯誤時進行重試。 如需重試邏輯的詳細資訊，請參閱[記憶體內部 OLTP 的衝突偵測和重試邏輯](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables#conflict-detection-and-retry-logic)。

## <a name="next-steps"></a>後續步驟
如需監視指引，請參閱[使用動態管理檢視監視 Azure SQL Database](sql-database-monitoring-with-dmvs.md)。
