---
title: "Azure 資料庫移轉服務預覽概觀 | Microsoft Docs"
description: "Azure 資料庫移轉服務的概觀，此服務能從許多資料庫來源提供無縫移轉到 Azure 資料平台。"
services: database-migration
author: HJToland3
ms.author: jtoland
manager: 
ms.reviewer: 
ms.service: database-migration
ms.workload: data-services
ms.topic: article
ms.date: 12/13/2017
ms.openlocfilehash: 2aae105b7454209131db79c60d74740ce97c21ce
ms.sourcegitcommit: ded74961ef7d1df2ef8ffbcd13eeea0f4aaa3219
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2018
---
# <a name="what-is-the-azure-database-migration-service-preview"></a>什麼是 Azure 資料庫移轉服務預覽？
Azure 資料庫移轉服務是一個完全受控的服務，能夠從多個資料庫來源無縫移轉到 Azure 資料平台，將停機時間降到最低。 服務目前處於公開預覽，開發重點放在下列工作：

- 可靠性和效能。
- 反覆新增來源目標組。
- 持續投資無衝突的移轉。

## <a name="use-familiar-tools"></a>使用熟悉的工具
Azure 資料庫移轉服務整合我們現有工具和服務的某些功能。  它提供客戶全方位、高可用性的解決方案。 服務會使用[資料移轉小幫手](http://aka.ms/dma)來產生評估報表，提供建議以引導您在移轉之前完成所需的變更。 由您自行決定，是否要執行任何所需的補救。 當您準備好要開始移轉程序時，Azure 資料庫移轉服務會執行所有相關聯的步驟。 移轉程序會善用 Microsoft 決定的最佳做法，因此您可以放心地移轉專案。

## <a name="regional-availability-during-public-preview"></a>公開預覽期間的區域可用性
公開預覽版本的 Azure 資料庫移轉服務目前可在下列區域使用：
- 美國東部
- 美國中南部
- 美國西部
- 巴西南部
- 西歐
- 北歐
- 東南亞
- 印度西部

## <a name="next-steps"></a>後續步驟
- [使用 Azure 入口網站建立 Azure 資料庫移轉服務的執行個體](quickstart-create-data-migration-service-portal.md)。
- [將 SQL Server 移轉到 Azure SQL Database](tutorial-sql-server-to-azure-sql.md)。
- [使用 Azure 資料庫移轉服務的必要條件概觀](pre-reqs.md)。
- [使用 Azure 資料庫移轉服務的相關常見問題集](faq.md)。
