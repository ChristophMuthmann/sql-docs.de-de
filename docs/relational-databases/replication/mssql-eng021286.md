---
title: MSSQL_ENG021286 | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG021286 error
ms.assetid: b63620b7-1c6d-46f7-90ea-3a8e99af8de4
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3e5b8c5b4f737d0abe9f8c250bdba72d791c2788
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="mssqleng021286"></a>MSSQL_ENG021286
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|21286|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Die %1!s!-Konflikttabelle ist nicht vorhanden.|  
  
## <a name="explanation"></a>Erklärung  
 Dieser Fehler wird ausgelöst, wenn es für einen Artikel in [sysmergearticles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) keine Konflikttabelle gibt. Der Fehler kann bei dem Versuch auftreten, einer Tabelle, die für die Mergereplikation veröffentlicht wurde, eine Spalte hinzuzufügen oder aber eine Spalte aus der Tabelle zu entfernen.  
  
## <a name="user-action"></a>Benutzeraktion  
 Führen Sie [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) für die Datenbank mit der fehlenden Konflikttabelle aus, um sich zu vergewissern, dass keine Probleme mit der Datenkonsistenz bestehen.  
  
 Wenn die Konflikttabelle auf einem Abonnenten fehlt, sollten Sie das Abonnement löschen und es dann gänzlich neu erstellen. Fehlt die Konflikttabelle auf einem Verleger, empfiehlt es sich, alle Abonnements und die Veröffentlichung zu löschen und dann die Veröffentlichung und alle Abonnements neu zu erstellen. Weitere Informationen finden Sie unter [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md) und [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
