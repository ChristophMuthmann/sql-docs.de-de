---
title: "Dateiwiederherstellungen (einfaches Wiederherstellungsmodell) | Microsoft Docs"
ms.custom: ""
ms.date: "03/24/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Dateiwiederherstellungen [SQL Server]"
  - "Einfaches Wiederherstellungsmodell [SQL Server]"
  - "Wiederherstellen von Dateien [SQL Server], Transact-SQL-Wiederherstellungssequenz"
  - "Wiederherstellen von Dateien [SQL Server]"
  - "Wiederherstellungssequenz in Transact-SQL"
  - "Wiederherstellen von Dateien [SQL Server], einfaches Wiederherstellungsmodell"
  - "Dateiwiederherstellung [SQL Server], einfaches Wiederherstellungsmodell"
  - "Dateiwiederherstellung [SQL Server], Transact-SQL-Wiederherstellungssequenz"
ms.assetid: b6d07386-7c6f-4cc6-be32-93289adbd3d6
caps.latest.revision: 57
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 56
---
# Dateiwiederherstellungen (einfaches Wiederherstellungsmodell)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Dieses Thema betrifft nur Datenbanken, die auf dem einfachen Wiederherstellungsmodell basieren und mindestens eine schreibgeschützte sekundäre Dateigruppe enthalten.  
  
 Das Ziel einer Dateiwiederherstellung besteht darin, eine oder mehrere beschädigte Dateien wiederherzustellen, ohne dabei die gesamte Datenbank wiederherstellen zu müssen. Beim einfachen Wiederherstellungsmodell werden Dateisicherungen nur für schreibgeschützte Dateien unterstützt. Die primäre Dateigruppe und die sekundären Dateigruppen mit Lese-/Schreibzugriff werden immer zusammen wiederhergestellt (durch Wiederherstellen einer Datenbank- oder Teilsicherung).  
  
 Für die Dateiwiederherstellung sind folgende Szenarien möglich:  
  
-   Offlinedateiwiederherstellung  
  
     Bei einer *Offlinedateiwiederherstellung*ist die Datenbank offline, während die beschädigten Dateien oder Dateigruppen wiederhergestellt werden. Am Ende der Wiederherstellungssequenz wird die Datenbank wieder online geschaltet.  
  
     Offlinewiederherstellungen werden von allen Editionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unterstützt.  
  
-   Onlinedateiwiederherstellung  
  
     Bei einer *Onlinedateiwiederherstellung*bleibt die Datenbank online, wenn die Datenbank während einer Dateiwiederherstellung online ist. Dateigruppen, in denen eine Datei wiederhergestellt wird, sind während des Wiederherstellungsvorgangs jedoch offline. Sobald die Dateien einer Offlinedateigruppe wiederhergestellt sind, wird die Dateigruppe automatisch wieder online geschaltet.  
  
     Informationen zur Unterstützung von Onlinewiederherstellungen von Seiten und Dateien finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md). Weitere Informationen zur Onlinewiederherstellung finden Sie unter [Onlinewiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md).  
  
    > [!TIP]  
    >  Wenn Sie die Datenbank für eine Dateiwiederherstellung offline schalten möchten, tun Sie dies vor dem Starten der Wiederherstellungssequenz, indem Sie die folgende [ALTER DATABASE](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)-Anweisung ausführen: ALTER DATABASE *Datenbankname* SET OFFLINE.  
  
 **In diesem Thema:**  
  
-   [Übersicht über Datei- und Dateigruppenwiederherstellung mit dem einfachen Wiederherstellungsmodell](#Overview)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="Overview"></a> Übersicht über Datei- und Dateigruppenwiederherstellung mit dem einfachen Wiederherstellungsmodell  
 Ein Dateiwiederherstellungsszenario besteht aus einer einzelnen Wiederherstellungssequenz, bei der die geeigneten Daten kopiert, ein Rollforward ausgeführt und die Daten anschließend wiederhergestellt werden:  
  
1.  Jede beschädigte Datei wird von der letzten Dateisicherung wiederhergestellt.  
  
2.  Für jede wiederhergestellte Datei wird die letzte differenzielle Dateisicherung und dann die Datenbank wiederhergestellt.  
  
### Transact-SQL-Schritte für die Dateiwiederherstellungssequenz (einfaches Wiederherstellungsmodell)  
 In diesem Abschnitt werden die grundlegenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-[RESTORE](../Topic/RESTORE%20\(Transact-SQL\).md)-Optionen für eine einfache Dateiwiederherstellungssequenz erläutert. Hierfür unwichtige Syntax und Informationen werden ausgelassen.  
  
 Die Wiederherstellungssequenz enthält nur zwei [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen. Mit der ersten Anweisung wird unter Verwendung von WITH NORECOVERY eine sekundäre Datei (Datei `A`) wiederhergestellt. Im zweiten Vorgang werden unter Verwendung von WITH RECOVERY zwei weitere Dateien (`B` und `C`) von einem anderen Sicherungsmedium wiederhergestellt:  
  
1.  RESTORE DATABASE *Datenbank* FILE **=***Name_von_Datei_A*  
  
     FROM *Dateisicherung_von_Datei_A*  
  
     WITH NORECOVERY**;**  
  
2.  RESTORE DATABASE *Datenbank* FILE **=*** Name_von_Datei_B***, ***Name_von_Datei_C*  
  
     FROM *Dateisicherung_der_Dateien_B_und_C*  
  
     WITH RECOVERY**;**  
  
### Beispiele  
  
-   [Beispiel: Onlinewiederherstellung einer schreibgeschützten Datei &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Beispiel: Offlinewiederherstellung der primären Dateigruppe und einer weiteren Dateigruppe &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So stellen Sie Dateien und Dateigruppen wieder her**  
  
-   [Wiederherstellen von Dateien und Dateigruppen über vorhandene Dateien &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Wiederherstellen von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Wiederherstellen von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Restore.SqlRestore-Methode (Server)](../Topic/SqlRestore%20Method.md) (SMO)  
  
## Siehe auch  
 [Sicherung und Wiederherstellung: Interoperabilität und Koexistenz &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [Differenzielle Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Vollständige Dateisicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [Vollständige Datenbankwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  