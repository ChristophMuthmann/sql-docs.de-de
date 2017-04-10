---
title: "Nicht-SQL Server-Verleger | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Heterogene Datenbankreplikation, Nicht-SQL Server-Verleger"
  - "Nicht-SQL Server-Verleger"
  - "Heterogene Datenquellen, Nicht-SQL Server-Verleger"
  - "Verleger [SQL Server-Replikation], Oracle"
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Nicht-SQL Server-Verleger
  Veröffentlichen von Daten aus nicht[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Quellen können Sie beim Konsolidieren der Daten in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] können Sie Momentaufnahme- oder Transaktionsdaten abonnieren, die aus einer Oracle-Datenbank veröffentlicht werden. Weitere Informationen zum Veröffentlichen von Oracle finden Sie unter [Oracle-Veröffentlichung Überblick](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
 Die heterogene Replikation an Nicht-SQL Server-Abonnenten ist veraltet. Das Veröffentlichen mit Oracle ist veraltet. Um Daten zu verschieben, erstellen Sie Lösungen mit Change Data Capture und [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Das Veröffentlichen von Daten aus Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datenbanken eignet sich ideal für die folgenden Szenarien:  
  
|Szenario|Beschreibung|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework-Anwendungen|Führen Sie die Entwicklung mit [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] durch, und arbeiten Sie dabei mit Daten, die aus einer Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datenbank repliziert wurden.|  
|Datawarehousing-Stagingserver|Behalten Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mit einem nicht-synchronisiert Stagingdatenbanken[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbank.|  
|Migration nach [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Testen Sie Ihre Anwendung in Echtzeit mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , und replizieren Sie dabei die Änderungen am Quellsystem. Wechseln Sie endgültig zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , wenn Sie mit der Migration zufrieden sind.|  
  
## Siehe auch  
 [Heterogene Datenbankreplikation](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  