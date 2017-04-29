---
title: MSSQLSERVER_2596 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2596 (Database Engine error)
ms.assetid: 49ab892f-8ba3-4ba1-b562-ddf205019802
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 669ad8fa565b39b8a589bf2940b91059d6355bb0
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver2596"></a>MSSQLSERVER_2596
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|2596|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC_DATABASE_IN_READ_ONLY_MODE|  
|Meldungstext|Die REPAIR-Anweisung wurde nicht verarbeitet. Die Datenbank kann nicht im schreibgeschützten Modus sein.|  
  
## <a name="explanation"></a>Erklärung  
Diese Meldung gibt an, dass sich die Datenbank im schreibgeschützten Modus befindet. Reparaturen sind nicht möglich, wenn sich eine Datenbank im schreibgeschützten Modus befindet.  
  
## <a name="user-action"></a>Benutzeraktion  
Legen Sie die Datenbank mithilfe der ALTER DATABASE-Anweisung auf Lese-/Schreibzugriff fest, und führen Sie anschließend den DBCC-Befehl erneut aus.  
  
## <a name="see-also"></a>Siehe auch  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
  

