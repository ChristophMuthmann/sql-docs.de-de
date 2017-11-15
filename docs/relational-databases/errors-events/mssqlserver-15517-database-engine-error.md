---
title: MSSQLSERVER_15517 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 15517 (Database Engine error)
ms.assetid: f94287f5-129f-4c52-9d34-62b996088001
caps.latest.revision: "5"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: b8a41aab607e1fcdcdb413278630c8b7a63f5642
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver15517"></a>MSSQLSERVER_15517
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|15517|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SEC_CANNOTEXECUTEASUSER|  
|Meldungstext|Die Ausführung als Datenbankprinzipal ist nicht möglich, weil der Prinzipal „*principal*“ nicht vorhanden ist, für diesen Typ von Prinzipal kein Identitätswechsel möglich ist, oder Sie nicht die erforderliche Berechtigung haben.|  
  
## <a name="user-action"></a>Benutzeraktion  
Verwenden Sie den Namen eines vorhandenen Prinzipals, oder rufen Sie die IMPERSONATE-Berechtigung für den betreffenden Prinzipal ab.  
  
15517 kann zudem nach dem Anfügen und Wiederherstellen einer Datenbank durch eine Person auftreten, die nicht mit dem ursprünglichen Datenbankbesitzer identisch ist. Ändern Sie zum Beheben dieses Fehlers den db_owner in eine Anmeldung auf Ihrem Server, indem Sie den folgenden Befehl ausführen:  
  
```  
ALTER AUTHORIZATION ON DATABASE:: DBName TO [NewLogin]  
```  
  
## <a name="see-also"></a>Siehe auch  
[In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
