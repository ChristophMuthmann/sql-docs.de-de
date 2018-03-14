---
title: Nicht-SQL Server-Verleger | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- heterogeneous database replication, non-SQL Server Publishers
- non-SQL Server Publishers
- heterogeneous data sources, non-SQL Server Publishers
- Publishers [SQL Server replication], Oracle
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 023c87eaf832a80fea4675a0fbf595b963ebe27e
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="non-sql-server-publishers"></a>Nicht-SQL Server-Verleger  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Es ist möglich, Daten aus Quellen außerhalb von[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] zu veröffentlichen und so die Daten in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]zu konsolidieren. Mit[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] können Sie Momentaufnahme- oder Transaktionsdaten abonnieren, die aus einer Oracle-Datenbank veröffentlicht werden. Weitere Informationen zum Veröffentlichen mit Oracle finden Sie unter [Veröffentlichungen mit Oracle (Übersicht)](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt die folgenden heterogenen Szenarien für die Transaktions- und Momentaufnahmereplikation:  
  
-   Veröffentlichen von Daten aus [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] an Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Abonnenten.  

-   Beim Veröffentlichen von Daten an und von Oracle bestehen folgende Einschränkungen:  
  | |2016 oder früher |2017 oder höher |
  |-------|-------|--------|
  |Replikation von Oracle |Wird nur für Oracle 10g oder früher unterstützt |Wird nur für Oracle 10g oder früher unterstützt |
  |Replikation zu Oracle |Bis Oracle 12c |Nicht unterstützt |


 Die heterogene Replikation an Nicht-SQL Server-Abonnenten ist veraltet. Das Veröffentlichen mit Oracle ist veraltet. Um Daten zu verschieben, erstellen Sie Lösungen mit Change Data Capture und [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Das Veröffentlichen von Daten aus Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbanken eignet sich ideal für die folgenden Szenarien:  
  
|Szenario|Description|  
|--------------|-----------------|  
|Bereitstellungen von[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework-Anwendungen|Führen Sie die Entwicklung mit [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] durch, und arbeiten Sie dabei mit Daten, die aus einer Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank repliziert wurden.|  
|Datawarehousing-Stagingserver|Sorgen Sie dafür, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Stagingdatenbanken stets synchron mit der Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank sind.|  
|Migration nach [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Testen Sie Ihre Anwendung in Echtzeit mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , und replizieren Sie dabei die Änderungen am Quellsystem. Wechseln Sie endgültig zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , wenn Sie mit der Migration zufrieden sind.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Heterogeneous Database Replication](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  
