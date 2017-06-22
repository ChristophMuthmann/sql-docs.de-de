---
title: MSSQL_ENG003724 | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG003724 error
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d97300f400557643da18e81201136649d629b681
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqleng003724"></a>MSSQL_ENG003724
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|3724|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Das %1!s! von '%3!s!' (%2!s!) ist nicht möglich, da das Objekt für die Replikation verwendet wird.|  
  
## <a name="explanation"></a>Erklärung  
 Wenn Sie Objekte in einer Datenbank replizieren, werden diese Objekte in der **sysarticles** -Systemtabelle (bei Momentaufnahmen- und Transaktionsveröffentlichungen) bzw. **sysmergearticles** (bei Mergeveröffentlichungen) als repliziert gekennzeichnet. Dieser Fehler wird ausgelöst, wenn Sie versuchen, ein repliziertes Objekt zu löschen.  
  
## <a name="user-action"></a>Benutzeraktion  
 Stellen Sie vor dem Löschen sicher, dass das Datenbankobjekt nicht repliziert ist. Beispiel:  
  
-   Tritt der Fehler in der Veröffentlichungsdatenbank auf, löschen Sie den Artikel aus der Veröffentlichung, bevor Sie das Objekt löschen. Weitere Informationen finden Sie unter [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
-   Tritt der Fehler in der Abonnementdatenbank auf, löschen Sie das Abonnement, bevor Sie das Objekt löschen. Weitere Informationen finden Sie unter [Veröffentlichungen abonnieren](../../relational-databases/replication/subscribe-to-publications.md). Bei Abonnements für Transaktionsreplikationen besteht die Möglichkeit, nicht gleich die gesamte Veröffentlichung zu löschen, sondern nur das Abonnement eines einzelnen Artikels zu löschen. Weitere Informationen finden Sie unter [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md).  
  
 Falls dieser Fehler in einer Datenbank auftritt, die nicht repliziert wird, führen Sie [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) aus, um sicherzustellen, dass die Objekte in der Datenbank nicht als repliziert hervorgehoben sind.  
  
## <a name="see-also"></a>Siehe auch  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
