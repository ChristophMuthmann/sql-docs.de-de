---
title: "Datenbankspiegelung: Interoperabilität und Koexistenz (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b4f96be2ba6ef11dec1da4bafccaa747ae3e60bb
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>Datenbankspiegelung: Interoperabilität und Koexistenz (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die Datenbankspiegelung kann mit den folgenden Funktionen oder Komponenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden:  
  
-   [AlwaysOn-Failoverclusterinstanzen (SQL Server-Failoverclustering)](../../database-engine/database-mirroring/database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [Change Data Capture (und Änderungsnachverfolgung)](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [Datenbank-Momentaufnahmen](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
-   [Volltextkataloge](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [Protokollversand](../../database-engine/database-mirroring/database-mirroring-and-log-shipping-sql-server.md)  
  
-   [Replikation](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)  
  
 Die Datenbankspiegelung funktioniert nicht in Verbindung mit folgenden Elementen:  
  
-   Datenbankübergreifende Transaktionen/verteilte Transaktionen  
  
     Weitere Informationen dazu, warum solche Transaktionen nicht unterstützt werden, finden Sie unter [Datenbankübergreifende Transaktionen und verteilte Transaktionen für AlwaysOn-Verfügbarkeitsgruppen oder Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
