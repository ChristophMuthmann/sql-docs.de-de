---
title: Nicht-SQL Server-Verleger | Microsoft-Dokumentation
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
- heterogeneous database replication, non-SQL Server Publishers
- non-SQL Server Publishers
- heterogeneous data sources, non-SQL Server Publishers
- Publishers [SQL Server replication], Oracle
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 72a1a8c69a7c18f02da6439af94fefffe73a03a3
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="non-sql-server-publishers"></a>Nicht-SQL Server-Verleger
  Es ist möglich, Daten aus Quellen außerhalb von[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] zu veröffentlichen und so die Daten in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]zu konsolidieren. Mit[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] können Sie Momentaufnahme- oder Transaktionsdaten abonnieren, die aus einer Oracle-Datenbank veröffentlicht werden. Weitere Informationen zum Veröffentlichen mit Oracle finden Sie unter [Veröffentlichungen mit Oracle (Übersicht)](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
 Die heterogene Replikation an Nicht-SQL Server-Abonnenten ist veraltet. Das Veröffentlichen mit Oracle ist veraltet. Um Daten zu verschieben, erstellen Sie Lösungen mit Change Data Capture und [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Das Veröffentlichen von Daten aus Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbanken eignet sich ideal für die folgenden Szenarien:  
  
|Szenario|Beschreibung|  
|--------------|-----------------|  
|Bereitstellungen von[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework-Anwendungen|Führen Sie die Entwicklung mit [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] durch, und arbeiten Sie dabei mit Daten, die aus einer Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank repliziert wurden.|  
|Datawarehousing-Stagingserver|Sorgen Sie dafür, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Stagingdatenbanken stets synchron mit der Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank sind.|  
|Migration nach [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Testen Sie Ihre Anwendung in Echtzeit mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , und replizieren Sie dabei die Änderungen am Quellsystem. Wechseln Sie endgültig zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , wenn Sie mit der Migration zufrieden sind.|  
  
## <a name="see-also"></a>Siehe auch  
 [Heterogeneous Database Replication](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  
