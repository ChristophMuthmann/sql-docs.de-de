---
title: "MSSQL_ENG003165 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG003165 (Fehler)"
ms.assetid: 707d33dd-644e-4cc9-ac51-dddd49031530
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG003165
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|3165|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Die %1!s!-Datenbank wurde wiederhergestellt; beim Wiederherstellen/Entfernen der Replikation wurde jedoch ein Fehler erkannt. Die Datenbank ist offline. Weitere Informationen finden Sie im Thema 'MSSQL_ENG003165' in der SQL Server-Onlinedokumentation.|  
  
## Erklärung  
 Dieser Fehler wird ausgelöst, wenn beim Wiederherstellen einer Sicherung für eine replizierte Datenbank ein Problem auftritt.  
  
-   Wenn die Sicherung in dieselbe Datenbank und auf denselben Server wiederhergestellt wird, woher sie stammt, bedeutet der Fehler, dass die Replikationseinstellungen nicht ordnungsgemäß wiederhergestellt werden konnten.  
  
-   Wenn die Sicherung in eine andere Datenbank oder auf einen anderen Server wiederhergestellt wird, bedeutet der Fehler, dass die Repliktionseinstellungen nicht ordnungsgemäß entfernt werden konnten (die Replikationseinstellungen werden bei einer anderen Datenbank oder einem anderen Server standardmäßig entfernt).  
  
 Der Fehler ist vermutlich das Ergebnis einer fehlenden Übereinstimmung zwischen dem Status der wiederhergestellten Datenbank und einer oder mehreren Systemdatenbanken, die Replikationsmetadaten enthalten: **msdb**, **master**oder der Verteilungsdatenbank.  
  
## Benutzeraktion  
 So lösen Sie das Problem:  
  
1.  Führen Sie ALTER DATABASE aus, um die Datenbank offline zu schalten; Beispiel: `ALTER DATABASE AdventureWorks SET ONLINE`. Weitere Informationen finden Sie unter [ALTER DATABASE & #40; Transact-SQL & #41;](../../t-sql/statements/alter-database-transact-sql.md). Wenn Sie die Replikationseinstellungen beibehalten möchten, fahren Sie mit Schritt 2 fort. Andernfalls fahren Sie mit Schritt 3 fort.  
  
2.  Führen Sie [Sp_restoredbreplication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-restoredbreplication-transact-sql.md). Wenn diese gespeicherte Prozedur erfolgreich ausgeführt wird, ist die Wiederherstellung abgeschlossen. Falls die Ausführung nicht erfolgreich verlief, fahren Sie mit Schritt 3 fort.  
  
3.  Führen Sie [Sp_removedbreplication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) Um alle replikationseinstellungen zu entfernen.  
  
     Konfigurieren Sie gegebenenfalls die Replikation neu. Wenn Sie wie empfohlen Skripts für die Replikationstopologie erstellt haben, verwenden Sie Skripts, um die Topologie neu zu konfigurieren.  
  
## Siehe auch  
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Sichern und Wiederherstellen von replizierten Datenbanken](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  