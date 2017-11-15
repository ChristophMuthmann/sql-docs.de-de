---
title: MSSQLSERVER_3176 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3176 (Database Engine error)
ms.assetid: 4be24c64-2d52-4cb4-b4d7-36efbe4555b6
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 731f81a6a8c1af6d3efbb1f8af84b5a5f83176c4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver3176"></a>MSSQLSERVER_3176
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|3176|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|LDDB_FILE_CLAIM|  
|Meldungstext|Die Datei '%ls' wird von '%ls'(%d) und '%ls'(%d) beansprucht. Mithilfe der WITH MOVE-Klausel kann nach einer oder mehreren Dateien gesucht werden.|  
  
## <a name="explanation"></a>Erklärung  
Es wird versucht, eine Datei für mehr als einen Zweck zu verwenden.  
  
### <a name="possible-causes"></a>Mögliche Ursachen  
Der Dateiname wird bereits von einer anderen Datenbank verwendet.  
  
## <a name="user-action"></a>Benutzeraktion  
Stellen Sie die Datenbankdateien an einem anderen Speicherort wieder her. Verwenden Sie in einer RESTORE-Anweisung eine WITH MOVE-Klausel, um die einzelnen Dateien zu verschieben. Ändern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] auf der Seite Optionen die Dateispeicherorte im Raster **Datenbankdateien wiederherstellen als** des Dialogfelds **Datenbank wiederherstellen**.  
  
## <a name="see-also"></a>Siehe auch  
[Wiederherstellen einer Datenbank an einem neuen Speicherort &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[Wiederherstellen von Dateien an einem neuen Speicherort &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  
