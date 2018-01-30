---
title: "Verwalten der Größe der Transaktionsprotokolldatei | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/05/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: logs
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction logs [SQL Server], size management
- manage log size
- log size, manage
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 58cbe590d16bba9d74f41dc7499b563a2e0b2499
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="manage-the-size-of-the-transaction-log-file"></a>Verwalten der Größe der Transaktionsprotokolldatei
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Dieses Thema enthält Informationen zum Überwachen der Größe eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Transaktionsprotokolls, Verkleinern des Transaktionsprotokolls, Hinzufügen zu oder Vergrößern einer Transaktionsprotokolldatei, Optimieren der Wachstumsrate des **tempdb**-Transaktionsprotokolls und Steuern des Wachstums einer Transaktionsprotokolldatei.  

##  <a name="MonitorSpaceUse"></a>Überwachen der Belegung des Protokollspeicherplatzes  
Überwachen Sie mithilfe von [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md) die Belegung des Protokollspeicherplatzes. Diese DMV gibt Informationen zum derzeit belegten Protokollspeicherplatz zurück und zeigt an, wann das Transaktionsprotokoll abgeschnitten werden muss. 

Informationen zur aktuellen Größe einer Protokolldatei, ihrer maximalen Größe sowie der für die Datei festgelegten automatischen Vergrößerungsoption können Sie auch den Spalten **size**, **max_size** und **growth** für die betreffende Protokolldatei in [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) entnehmen.  
  
> [!IMPORTANT]
> Achten Sie darauf, den Protokolldatenträger nicht zu überlasten. Stellen Sie sicher, dass der Protokollspeicher den [IOPS](http://wikipedia.org/wiki/IOPS)-Anforderungen und Anforderungen an niedrige Latenzen für Ihre Transaktionslast gerecht wird. 
  
##  <a name="ShrinkSize"></a> Verkleinern der Protokolldateigröße  
 Sie müssen zum Reduzieren der physischen Größe einer physischen Protokolldatei die Protokolldatei verkleinern. Dies ist nützlich, wenn Sie wissen, dass eine Transaktionsprotokolldatei nicht verwendeten Speicherplatz enthält. Sie können eine Protokolldatei nur dann verkleinern, wenn die Datenbank online und mindestens eine [virtuelle Protokolldatei (Virtual Log File, VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) verfügbar ist. In einigen Fällen ist eine Verkleinerung des Protokolls möglicherweise erst nach der nächsten Protokollkürzung möglich.  
  
> [!NOTE]
> Faktoren, wie z.B. Transaktionen mit langer Laufzeit, die [VLFs](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) über einen längeren Zeitraum hinweg aktiv halten, können die Protokollverkleinerung einschränken oder sogar gänzlich verhindern. Weitere Informationen finden Sie unter [Faktoren, die die Protokollkürzung verzögern können](../../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation).  
  
Beim Verkleinern einer Protokolldatei werden [VLFs](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) entfernt, die keinen Teil des logischen Protokolls enthalten (d.h. *inaktive VLFs*). Beim Verkleinern einer Transaktionsprotokolldatei werden inaktive VLFs vom Ende der Protokolldatei entfernt, um das Protokoll in etwa auf die Zielgröße zu verkleinern. 

> [!IMPORTANT]
> Berücksichtigen Sie vor dem Verkleinern des Transaktionsprotokolls die [Faktoren, die die Protokollkürzung verzögern können](../../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation). Wenn der Speicherplatz nach einer Protokollverkleinerung wieder benötigt wird, vergrößert sich das Transaktionsprotokoll wieder und führt bei der Protokollvergrößerung infolgedessen zu einem Leistungsoverhead. Weitere Informationen finden Sie in diesem Thema unter [Empfehlungen](#Recommendations).
  
 **Verkleinern einer Protokolldatei (ohne die Datenbankdateien zu verkleinern)**  
  
-   [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
  
-   [Verkleinern einer Datei](../../relational-databases/databases/shrink-a-file.md)  
  
 **Überwachen der Protokollverkleinerungsereignisse**  
  
-   [Log File Auto Shrink Event Class](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md).  
  
 **Überwachen von Protokollspeicherplatz**  
  
-   [sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)  
  
-   [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) (Informationen finden Sie in den Spalten **size**, **max_size** und **growth** für die Protokolldateien.)  
  
##  <a name="AddOrEnlarge"></a> Hinzufügen oder Vergrößern einer Protokolldatei  
Sie können Speicherplatz schaffen, indem Sie entweder die vorhandene Protokolldatei vergrößern (sofern der Speicherplatz dies zulässt) oder der Datenbank eine neue Protokolldatei hinzufügen, wofür normalerweise ein anderer Datenträger verwendet wird. Eine Transaktionsprotokolldatei ist ausreichend, es sei denn, der Protokollspeicherplatz und der Speicherplatz auf dem Volume, auf dem die Protokolldatei gespeichert ist, sind ausgeschöpft.   
  
-   Sie können der Datenbank eine Protokolldatei hinzufügen, indem Sie die `ADD LOG FILE`-Klausel der `ALTER DATABASE`-Anweisung verwenden. Durch das Hinzufügen einer Protokolldatei kann das Protokoll vergrößert werden.  
-   Um die Protokolldatei zu vergrößern, verwenden Sie die `MODIFY FILE`-Klausel der `ALTER DATABASE`-Anweisung unter Angabe der Syntax `SIZE` und `MAXSIZE`. Weitere Informationen finden Sie unter [ALTER DATABASE-Optionen FILE und FILEGROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  

Weitere Informationen finden Sie in diesem Thema unter [Empfehlungen](#Recommendations).
    
##  <a name="tempdbOptimize"></a> Optimieren der Größe des tempdb-Transaktionsprotokolls  
 Beim Neustarten einer Serverinstanz wird das Transaktionsprotokoll der **tempdb** -Datenbank auf seine ursprüngliche Größe (vor einer automatischen Größenerweiterung) zurückgesetzt. Dies kann eine Leistungsminderung des **tempdb** -Transaktionsprotokolls zur Folge haben. 
 
 Der damit verbundene Verwaltungsaufwand lässt sich vermeiden, indem Sie nach dem Starten oder erneuten Starten der Serverinstanz die Größe des **tempdb** -Transaktionsprotokolls erhöhen. Weitere Informationen finden Sie unter [tempdb Database](../../relational-databases/databases/tempdb-database.md).  
  
##  <a name="ControlGrowth"></a> Steuern einer Transaktionsprotokolldatei  
 Sie können die [ALTER DATABASE-Optionen FILE und FILEGROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)-Anweisung verwenden, um die Vergrößerung einer Transaktionsprotokolldatei zu steuern. Beachten Sie Folgendes:  
  
-   Verwenden Sie die Option `SIZE`, um die aktuelle Dateigröße in KB-, MB-, GB- und TB-Einheiten zu ändern.  
-   Verwenden Sie die Option `FILEGROWTH`, um das Vergrößerungsinkrement zu ändern. Der Wert 0 gibt an, dass die automatische Vergrößerung deaktiviert und kein zusätzlicher Speicherplatz zulässig ist.  
-   Verwenden Sie die Option `MAXSIZE`, um die maximale Größe einer Protokolldatei in KB-, MB-, GB- und TB-Einheiten zu steuern oder die Vergrößerung auf UNLIMITED festzulegen.  

Weitere Informationen finden Sie in diesem Thema unter [Empfehlungen](#Recommendations).

## <a name="Recommendations"></a> Empfehlungen
Es folgen einige allgemeine Empfehlungen für die Arbeit mit Transaktionsprotokolldateien:

-   Das mit der Option `FILEGROWTH` festgelegte automatische Vergrößerungsinkrement (autogrow) des Transaktionsprotokolls muss groß genug sein, um den Anforderungen der Workloadtransaktionen immer einen Schritt voraus sein. Die Schrittweite für die Dateivergrößerung sollte für eine Protokolldatei stets groß genug sein, um häufige Erweiterungen zu vermeiden. Ein guter Anhaltspunkt für die korrekte Anpassung der Größe eines Transaktionsprotokolls ist die Überwachung der Menge der Protokolldaten, die in folgenden Zeiträumen belegt werden:
    -  Die Zeit, die erforderlich ist, um eine vollständige Sicherung durchzuführen, da Protokollsicherungen erst nach Beendigung der vollständigen Sicherung durchgeführt werden können
    -  Die Zeit, die für die umfangreichsten Vorgänge zur Indexwartung erforderlich ist
    -  Die Zeit, die für die Ausführung des größten Batches in einer Datenbank erforderlich ist

-   Wenn Sie die Option `FILEGROWTH` **autogrow** für Daten- und Protokolldateien festlegen, kann es empfehlenswert sein, diese anstelle von **percentage** in **size** festzulegen, um eine bessere Steuerung der Wachstumsrate zu ermöglichen, da der Prozentsatz eine stetig steigende Zahl darstellt.
    -  Beachten Sie, dass erweiterte Protokollwachstumszeiten von entscheidender Bedeutung sind, da für Transaktionsprotokolle nicht die [schnelle Dateiinitialisierung](../../relational-databases/databases/database-instant-file-initialization.md) verwendet werden kann. 
    -  Als bewährte Methode sollten Sie für Transaktionsprotokolle den Wert der Option `FILEGROWTH` nicht auf über 1.024 MB festlegen. Die Standardwerte für die Option `FILEGROWTH` lauten wie folgt:  
  
      |Versionsoptionen|Standardwerte|  
      |-------------|--------------------|  
      |Seit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Daten: 64 MB, Protokolldateien: 64 MB|  
      |Seit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Daten: 1 MB, Protokolldateien: 10 %|  
      |Vor [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Daten: 10 %, Protokolldateien: 10 %|  

-   Ein kleines Vergrößerungsinkrement könnte dazu führen, dass zu viele kleine [VLFs](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) generiert werden und die Leistung beeinträchtigt wird. Informationen darüber, wie Sie die optimale VLF-Verteilung für die aktuelle Größe des Transaktionsprotokolls aller Datenbanken in einer bestimmten Instanz sowie die benötigten Wachstumsinkremente zum Erreichen der erforderlichen Größe ermitteln, finden Sie in [diesem Skript](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs).

-   Ein großes Vergrößerungsinkrement könnte dazu führen, dass wenige große [VLFs](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) generiert werden und darüber hinaus die Leistung beeinträchtigt. Informationen darüber, wie Sie die optimale VLF-Verteilung für die aktuelle Größe des Transaktionsprotokolls aller Datenbanken in einer bestimmten Instanz sowie die benötigten Wachstumsinkremente zum Erreichen der erforderlichen Größe ermitteln, finden Sie in [diesem Skript](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs). 

-   Auch bei aktiviertem autogrow-Inkrement können Sie eine Meldung erhalten, dass das Transaktionsprotokoll voll ist, wenn es nicht schnell genug wachsen kann, um die Anforderungen Ihrer Abfrage zu erfüllen. Weitere Informationen zum Ändern des Vergrößerungsinkrements finden Sie unter [ALTER DATABASE-Optionen FILE und FILEGROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).

-   Durch die Verwaltung von mehreren Protokolldateien in einer Datenbank wird die Leistung in keiner Weise verbessert, da die Transaktionsprotokolldateien nicht wie Datendateien eine [proportionale Füllung](../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill) in derselben Dateigruppe durchführen.  

-   Für Protokolldateien kann eine automatische Verkleinerung durchgeführt werden. Dies wird jedoch **nicht empfohlen**, und die Datenbankeigenschaft **auto_shrink** ist standardmäßig auf FALSE festgelegt. Wenn **auto_shrink** auf TRUE festgelegt ist, wird die Größe einer Datei nur dann automatisch verkleinert, wenn mehr als 25 Prozent des Speicherplatzes ungenutzt sind. 
    -   Die Datei wird entweder auf eine Größe verkleinert, bei der 25 Prozent der Datei aus nicht verwendetem Speicherplatz bestehen, oder auf die ursprüngliche Dateigröße, je nachdem, welcher Wert größer ist. 
    -   Informationen zum Ändern der Einstellung der **auto_shrink**-Eigenschaft finden Sie unter [Anzeigen oder Ändern der Eigenschaften einer Datenbank](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md) und [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). 
  
## <a name="see-also"></a>Siehe auch  
[BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
[Problembehandlung bei vollen Transaktionsprotokollen &#40;SQL Server-Fehler 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)    
[Transaktionsprotokollsicherungen – Handbuch zur Architektur und Verwaltung von Transaktionsprotokollen in SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Backups)    
[Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)    
[ALTER DATABASE-Optionen FILE und FILEGROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)
