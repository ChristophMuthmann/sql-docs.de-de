---
title: Heterogene Datenbankreplikation | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- heterogeneous database replication, about heterogeneous database replication
- replication [SQL Server], heterogeneous database replication
- heterogeneous database replication
ms.assetid: 3fd983ad-e206-45db-9054-417c9b5bb815
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6eee43a7755f2e018a7ed4e9f822983b03b7181a
ms.lasthandoff: 04/11/2017

---
# <a name="heterogeneous-database-replication"></a>Heterogene Datenbankreplikation
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt die folgenden heterogenen Szenarien für die Transaktions- und Momentaufnahmereplikation:  
  
-   Veröffentlichen von Daten aus Oracle in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Veröffentlichen von Daten aus [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] an Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Abonnenten.  
  
 Die heterogene Replikation an Nicht-SQL Server-Abonnenten ist veraltet. Das Veröffentlichen mit Oracle ist veraltet. Um Daten zu verschieben, erstellen Sie Lösungen mit Change Data Capture und [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="publishing-data-from-oracle"></a>Veröffentlichen von Daten aus Oracle  
 Mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] können Sie Daten aus Oracle mit einem Großteil der Funktionen und ebenso einfach veröffentlichen wie bei der Momentaufnahme- und Transaktionsreplikation in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Das Veröffentlichen von Daten aus Oracle eignet sich ideal für die folgenden Szenarien:  
  
|Szenario|Beschreibung|  
|--------------|-----------------|  
|Bereitstellungen von[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework-Anwendungen|Führen Sie die Entwicklung mit [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] durch, und arbeiten Sie dabei mit Daten, die aus einer Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank repliziert wurden.|  
|Datawarehousing-Stagingserver|Sorgen Sie dafür, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Stagingdatenbanken stets synchron mit der Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank sind.|  
|Migration nach [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Testen Sie Ihre Anwendung in Echtzeit mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , und replizieren Sie dabei die Änderungen am Quellsystem. Wechseln Sie endgültig zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , wenn Sie mit der Migration zufrieden sind.|  
  
 Weitere Informationen finden Sie unter [Veröffentlichungen mit Oracle (Übersicht)](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
## <a name="publishing-data-to-non-sql-server-subscribers"></a>Veröffentlichen von Daten für Nicht-SQL Server-Abonnenten  
 Die folgenden Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbanken werden als Abonnenten für Momentaufnahme- und Transaktionsveröffentlichungen unterstützt:  
  
-   Oracle für alle Plattformen, die durch Oracle unterstützt werden  
  
-   IBM DB2 für AS400, MVS, Unix, Linux und Windows.  
  
 Weitere Informationen finden Sie unter [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
  
