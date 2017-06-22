---
title: Skalierbarkeit | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/27/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a4891c57-56bb-49f4-9bb5-f11b745279e5
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5ab43ba6b6a27fa46b5214a60063c5df3f5496f4
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="scalability"></a>Skalierbarkeit
  In SQL Server 2016 wurde die Skalierbarkeit der Speicherung auf Datenträgern für speicheroptimierte Tabellen verbessert.  
  
-   **Mehrere Threads zur dauerhaften Speicherung speicheroptimierter Tabellen**  
  
     In der vorherigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gab es einen einzigen Offline-Prüfpunktthread, der das Transaktionsprotokoll auf Änderungen an speicheroptimierten Tabellen überprüft und diese dauerhaft in Prüfpunktdateien gespeichert hat (z.B. Daten- und Änderungsdateien). Eine größere Anzahl von Kernen konnte zur Überlastung des einzelnen Offline-Prüfpunktthreads führen.  
  
     In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]sind mehrere gleichzeitig ausgeführte Threads dafür zuständig, Änderungen an speicheroptimierten Tabellen dauerhaft zu speichern.  
  
-   **Multithread-Wiederherstellung**  
  
     In der vorherigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erfolgte die Protokollanwendung im Rahmen eines Wiederherstellungsvorgangs mit einem einzigen Thread. In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]werden mehrere Threads für die Protokollanwendung verwendet.  
  
-   **Zusammenführungsvorgang**  
  
     Der Zusammenführungsvorgang wird jetzt mit mehreren Threads durchgeführt.  
  
-   **Dynamische Verwaltungssichten**  
  
     [sys.dm_db_xtp_checkpoint_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-stats-transact-sql.md) und [sys.dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) wurden in erheblichem Umfang geändert.  
  
 Die manuelle Zusammenführung wurde deaktiviert, da durch die Verwendung mehrerer Threads davon auszugehen ist, dass die Last bewältigt wird.  
  
 Das In-Memory-OLTP-Modul verwenden weiterhin eine speicheroptimierte Dateigruppe, die auf FILESTREAM basiert. Die einzelnen Dateien in der Dateigruppe wurden jedoch von FILESTREAM entkoppelt. Diese Dateien werden vollständig vom In-Memory OLTP-Modul verwaltet (beispielsweise hinsichtlich der Erstellung, Löschung und Speicherbereinigung). [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) wird nicht unterstützt.  
  
  

