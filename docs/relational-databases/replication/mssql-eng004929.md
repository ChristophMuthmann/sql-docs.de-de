---
title: MSSQL_ENG004929 | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
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
- MSSQL_ENG004929 error
ms.assetid: 1d9b1d88-1fbf-4089-b392-687d3b0220ca
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 63ec3f2d7704e0cc1e84cc07be51883277de4b3b
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="mssqleng004929"></a>MSSQL_ENG004929
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|4929|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Das %1!s!-Objekt '%2!s!' kann nicht geändert werden, da es für die Replikation veröffentlicht wird.|  
  
## <a name="explanation"></a>Erklärung  
 Dieser Fehler tritt normalerweise auf, wenn Sie versuchen, die PRIMARY KEY-Einschränkung einer Tabelle zu löschen, die für die Transaktionsreplikation veröffentlicht wird. Die Transaktionsreplikation erfordert einen Primärschlüssel für jede veröffentlichte Tabelle. Aus diesem Grund kann die Einschränkung nicht gelöscht werden.  
  
## <a name="user-action"></a>Benutzeraktion  
 Um die Einschränkung zu löschen, löschen Sie zunächst den der Tabelle zugeordneten Artikel. Weitere Informationen finden Sie unter [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md). Falls dieser Fehler in einer Datenbank auftritt, die nicht repliziert wird, führen Sie [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) aus, um sicherzustellen, dass die Objekte in der Datenbank nicht als repliziert hervorgehoben sind.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
