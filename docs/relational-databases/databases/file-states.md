---
title: "Dateistatus | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Wiederherstellung (Dateistatus) [SQL Server]"
  - "Überprüfen des Dateistatus"
  - "Aktueller Dateistatus"
  - "Überprüfen des Dateigruppenstatus"
  - "Dateistatus [SQL Server]"
  - "Online (Dateistatus)"
  - "Offline (Dateistatus) [SQL Server]"
  - "Anzeigen des Dateigruppenstatus"
  - "Anzeigen des Dateistatus"
  - "Fehlerverdächtig (Dateistatus)"
  - "Wird wiederhergestellt (Dateistatus) [SQL Server]"
  - "Aktueller Dateigruppenstatus"
  - "Wiederherstellung ausstehend (Dateistatus) [SQL Server]"
  - "Anzeigen des Dateistatus"
  - "Status [SQL Server], Dateien"
  - "Anzeigen des Dateigruppenstatus"
  - "Veraltet (Dateistatus)"
ms.assetid: b426474d-8954-4df0-b78b-887becfbe8d6
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Dateistatus
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird der Status einer Datenbankdatei unabhängig vom Status der Datenbank verwaltet. Eine Datei befindet sich immer in einem bestimmten Status, wie ONLINE oder OFFLINE. Um den aktuellen Status einer Datei anzuzeigen, verwenden Sie die Katalogsicht [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) oder [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md). Wenn die Datenbank offline ist, kann der Status der Dateien über die [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)-Katalogsicht angezeigt werden.  
  
 Der Status der Dateien in einer Dateigruppe legt die Verfügbarkeit der gesamten Dateigruppe fest. Damit eine Dateigruppe verfügbar ist, müssen alle Dateien in der Dateigruppe online sein. Wenn Sie den aktuellen Status einer Dateigruppe anzeigen möchten, verwenden Sie die [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) -Katalogsicht. Wenn eine Dateigruppe offline ist und Sie versuchen, mit einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung auf die Dateigruppe zuzugreifen, führt dies zu einem Fehler. Wenn der Abfrageoptimierer Abfragepläne für SELECT-Anweisungen erstellt, vermeidet er nicht gruppierte Indizes und indizierte Sichten, die in Offlinedateigruppen gespeichert sind, damit die Anweisungen erfolgreich ausgeführt werden. Enthält die Offlinedateigruppe jedoch den Heap oder gruppierten Index der Zieltabelle, schlagen die SELECT-Anweisungen fehl. Auch alle INSERT-, UPDATE- oder DELETE-Anweisungen, die eine Tabelle mit einem Index in einer Offlinedateigruppe ändern, schlagen fehl.  
  
## Dateistatusdefinitionen  
 Die folgende Tabelle definiert den Dateistatus.  
  
|Status|Definition|  
|-----------|----------------|  
|ONLINE|Die Datei ist für alle Vorgänge verfügbar. Dateien in der primären Dateigruppe sind immer online, wenn die Datenbank selbst online ist. Wenn eine Datei in der primären Dateigruppe nicht online ist, ist die Datenbank nicht online, und der Status der sekundären Dateien ist nicht definiert.|  
|OFFLINE|Die Datei ist nicht für den Zugriff verfügbar und ist möglicherweise nicht auf dem Datenträger vorhanden. Dateien werden durch explizite Benutzeraktionen offline geschaltet und bleiben offline, bis weitere Benutzeraktionen durchgeführt werden.<br /><br /> **\*\* Vorsicht\*\*** Eine Datei sollte nur offline geschaltet werden, wenn sie zwar beschädigt ist, jedoch wiederhergestellt werden kann. Eine offline geschaltete Datei kann nur durch Wiederherstellen der Datei aus der Sicherung erneut online geschaltet werden. Weitere Informationen zum Wiederherstellen einer einzelnen Datei finden Sie unter [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md).|  
|RESTORING|Die Datei wird wiederhergestellt. Dateien gehen aufgrund eines Wiederherstellungsbefehls in den Wiederherstellungsstatus über, der sich auf die gesamte Datei und nicht nur auf eine Seitenwiederherstellung bezieht; sie verbleiben in diesem Status, bis die Wiederherstellung abgeschlossen ist und die Datei wiederhergestellt wurde.|  
|RECOVERY PENDING|Die Wiederherstellung der Datei wurde verschoben. Eine Datei geht automatisch in diesen Status über, weil ein schrittweiser Wiederherstellungsvorgang durchgeführt wird, bei dem die Datei nicht wiederhergestellt wird. Es sind weitere Aktionen durch den Benutzer erforderlich, um den Fehler zu beheben und den Wiederherstellungsvorgang erfolgreich abzuschließen. Weitere Informationen finden Sie unter [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md).|  
|SUSPECT|Die Wiederherstellung der Datei ist während eines Onlinewiederherstellungsvorgangs fehlgeschlagen. Wenn sich die Datei in der primären Dateigruppe befindet, wird die Datenbank ebenfalls als fehlerverdächtig markiert. Anderenfalls gilt nur für die Datei der Status Fehlerverdächtig, und die Datenbank besitzt auch weiterhin den Status online.<br /><br /> Die Datei behält den Status Fehlerverdächtig, bis sie durch eine der folgenden Methoden bereitgestellt wird:<br /><br /> Wiederherstellung<br /><br /> DBCC CHECKDB mit REPAIR_ALLOW_DATA_LOSS|  
|DEFUNCT|Die Datei wurde gelöscht, während sie nicht online war. Alle Dateien in einer Dateigruppe erhalten den Status "defunct", wenn eine Offlinedateigruppe entfernt wird.|  
  
## Verwandte Inhalte  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
 [Datenbankstatus](../../relational-databases/databases/database-states.md)  
  
 [Spiegelungsstatus &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
 [Datenbankdateien und Dateigruppen](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  