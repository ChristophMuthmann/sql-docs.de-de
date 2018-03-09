---
title: MSSQLSERVER_3156 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3156 (Database Engine error)
ms.assetid: 345d8ed4-177e-4ec3-bab3-25d30000e323
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fae24a904f64ca47afba7874148e62bb4ebc2067
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver3156"></a>MSSQLSERVER_3156
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|3156|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|LDDB_CANT_WRITE|  
|Meldungstext|Die Datei '%ls' kann nicht in '%ls' wiederhergestellt werden. Verwenden Sie WITH MOVE, um einen gültigen Speicherort für die Datei zu identifizieren.|  
  
## <a name="explanation"></a>Erklärung  
Mit dieser allgemeinen Meldung werden die logischen oder physischen Dateinamen der Dateien angegeben, die aufgrund eines Problems mit dem angegebenen Speicherort nicht wiederhergestellt werden konnten.  
  
### <a name="possible-causes"></a>Mögliche Ursachen  
Die folgenden Ursachen sind möglich:  
  
-   Möglicherweise müssen Sie auf das angegebene Windows-Verzeichnis zugreifen.  
  
-   Möglicherweise haben Sie den Pfad falsch eingegeben, oder Sie haben einen Pfad angegeben, der nicht vorhanden ist.  
  
-   Der Dateiname wird möglicherweise für eine Datei verwendet, die nicht überschrieben werden kann.  
  
## <a name="user-action"></a>Benutzeraktion  
Suchen Sie in den Fehlerprotokollen nach anderen Meldungen, in denen weitere Details angegeben werden.  
  
Beheben Sie das Problem mit dem angegebenen Speicherort beispielsweise durch das Gewähren von Zugriff, oder verwenden Sie die Option WITH MOVE in Ihrer RESTORE-Anweisung, um die Datei zu verschieben.  
  
## <a name="see-also"></a>Siehe auch  
[Wiederherstellen einer Datenbank an einem neuen Speicherort &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[Wiederherstellen von Dateien an einem neuen Speicherort &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  
