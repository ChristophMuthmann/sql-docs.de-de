---
title: "Verwalten der Größe der Transaktionsprotokolldatei | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: logs
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: transaction logs [SQL Server], size management
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: a77aa280acd7a8b6525ac5c17d209b384a7fbed8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="manage-the-size-of-the-transaction-log-file"></a>Verwalten der Größe der Transaktionsprotokolldatei
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Dieses Thema enthält Informationen zum Überwachen der Größe eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Transaktionsprotokolls, Verkleinern des Transaktionsprotokolls, Hinzufügen zu oder Vergrößern einer Transaktionsprotokolldatei, Optimieren der Wachstumsrate des **tempdb**-Transaktionsprotokolls und Steuern des Wachstums einer Transaktionsprotokolldatei.  

  ##  <a name="MonitorSpaceUse"></a> Überwachen der Verwendung von Protokollspeicherplatz  
Überwachen Sie die Verwendung des Protokollspeicherplatzes, indem Sie [DBCC SQLPERF (LOGSPACE)](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql) verwenden. Dieser Befehl gibt Informationen zum derzeit belegten Protokollspeicherplatz zurück und zeigt an, wann das Transaktionsprotokoll abgeschnitten werden muss. Weitere Informationen finden Sie unter [DBCC SQLPERF (Transact-SQL)](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md). Informationen zur aktuellen Größe einer Protokolldatei, ihrer maximalen Größe sowie der für die Datei festgelegten automatischen Vergrößerungsoption können Sie auch den Spalten **size**, **max_size** und **growth** für die betreffende Protokolldatei in **sys.database_files** entnehmen. Weitere Informationen finden Sie unter [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).  
  
**Wichtig!** Vermeiden Sie das Überlasten des Protokolldatenträgers!  

  
##  <a name="ShrinkSize"></a> Verkleinern der Protokolldateigröße  
 Sie müssen zum Reduzieren der physischen Größe einer physischen Protokolldatei die Protokolldatei verkleinern. Dies ist nützlich, wenn Sie wissen, dass eine Transaktionsprotokolldatei nicht verwendeten Speicherplatz enthält. Sie können eine Protokolldatei nur dann verkleinern, wenn die Datenbank online und mindestens eine virtuelle Protokolldatei frei ist. In einigen Fällen ist eine Verkleinerung des Protokolls möglicherweise erst nach der nächsten Protokollkürzung möglich.  
  
> [!NOTE]
>  Faktoren, wie z. B. lang andauernde Transaktionen, die virtuelle Protokolldateien über einen längeren Zeitraum hinweg aktiv halten, können die Protokollverkleinerung einschränken oder sogar gänzlich verhindern. Informationen zu Faktoren, die eine Protokollkürzung verzögern können, finden Sie unter [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
 Beim Verkleinern einer Protokolldatei werden virtuelle Protokolldateien entfernt, die keinen Teil des logischen Protokolls enthalten (d.h. *inaktive virtuelle Protokolldateien*). Beim Verkleinern einer Transaktionsprotokolldatei werden inaktive, virtuelle Protokolldateien vom Ende der Protokolldatei entfernt, um das Protokoll in etwa auf die Zielgröße zu verkleinern.  
  
 **Verkleinern einer Protokolldatei (ohne die Datenbankdateien zu verkleinern)**  
  
-   [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
  
-   [Verkleinern einer Datei](../../relational-databases/databases/shrink-a-file.md)  
  
 **Überwachen der Protokollverkleinerungsereignisse**  
  
-   [Log File Auto Shrink Event Class](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md).  
  
 **Überwachen von Protokollspeicherplatz**  
  
-   [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)  
  
-   [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) (Informationen finden Sie in den Spalten **size**, **max_size** und **growth** für die Protokolldateien.)  
  
> [!NOTE]
>  Sie können festlegen, dass Protokolldateien automatisch verkleinert werden. Es wird jedoch von einer automatischen Verkleinerung abgeraten, und die **autoshrink** -Datenbankeigenschaft ist in den Standardeinstellungen auf FALSE festgelegt. Wenn **autoshrink** auf TRUE festgelegt ist, wird die Größe einer Datei nur dann automatisch verkleinert, wenn mehr als 25 Prozent des Speicherplatzes ungenutzt sind. Die Datei wird entweder auf eine Größe verkleinert, bei der 25 Prozent der Datei aus nicht verwendetem Speicherplatz bestehen, oder auf die ursprüngliche Dateigröße, je nachdem, welcher Wert größer ist. Informationen zum Ändern der Einstellung der der **autoshrink** -Eigenschaft finden Sie unter [Anzeigen oder Ändern der Eigenschaften einer Datenbank](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md). Verwenden Sie die Eigenschaft **AutoShrink** auf der Seite **Optionen** oder alternativ unter [ALTER DATABASE SET-Optionen&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) die Option AUTO_SHRINK.  
  

##  <a name="AddOrEnlarge"></a> Hinzufügen oder Vergrößern einer Protokolldatei  
 Sie können Speicherplatz schaffen, indem Sie entweder die vorhandene Protokolldatei vergrößern (sofern der Speicherplatz dies zulässt) oder der Datenbank eine neue Protokolldatei hinzufügen, wofür normalerweise ein anderer Datenträger verwendet wird.  
  
-   Sie können der Datenbank eine Protokolldatei hinzufügen, indem Sie die ADD LOG FILE-Klausel der ALTER DATABASE-Anweisung verwenden. Durch das Hinzufügen einer Protokolldatei kann das Protokoll vergrößert werden.  
  
-   Sie können die Protokolldatei vergrößern, indem Sie die MODIFY FILE-Klausel der ALTER DATABASE-Anweisung verwenden und die SIZE- und MAXSIZE-Syntax angeben. Weitere Informationen finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
    
  
##  <a name="tempdbOptimize"></a> Optimieren der Größe des tempdb-Transaktionsprotokolls  
 Beim Neustarten einer Serverinstanz wird das Transaktionsprotokoll der **tempdb** -Datenbank auf seine ursprüngliche Größe (vor einer automatischen Größenerweiterung) zurückgesetzt. Dies kann eine Leistungsminderung des **tempdb** -Transaktionsprotokolls zur Folge haben. Der damit verbundene Verwaltungsaufwand lässt sich vermeiden, indem Sie nach dem Starten oder erneuten Starten der Serverinstanz die Größe des **tempdb** -Transaktionsprotokolls erhöhen. Weitere Informationen finden Sie unter [tempdb Database](../../relational-databases/databases/tempdb-database.md).  
  
  
##  <a name="ControlGrowth"></a> Steuern einer Transaktionsprotokolldatei  
 Verwenden Sie die Anweisung [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md), um die Vergrößerung einer Transaktionsprotokolldatei zu verwalten. Beachten Sie Folgendes:  
  
-   Verwenden Sie die Option SIZE, um die aktuelle Dateigröße in KB-, MB-, GB- und TB-Einheiten zu ändern.  
  -   Verwenden Sie die Option FILEGROWTH, um die Vergrößerungsschrittweite zu ändern. Der Wert 0 gibt an, dass die automatische Vergrößerung deaktiviert und kein zusätzlicher Speicherplatz zulässig ist. Die Einstellung der kleinen automatischen Vergrößerungsschrittweite einer Protokolldatei kann ebenfalls die Leistung beeinträchtigen. Die Schrittweite für die Dateivergrößerung sollte für eine Protokolldatei stets groß genug sein, um häufige Erweiterungen zu vermeiden. Die standardmäßige Vergrößerungsschrittweite von 10 Prozent ist hierfür im Allgemeinen gut geeignet.  

Informationen zum Ändern der Eigenschaft für die Dateivergrößerung in einer Protokolldatei finden Sie unter [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md).  
  
-   Verwenden Sie die Option MAXSIZE, um die maximale Größe einer Protokolldatei in KB-, MB-, GB- und TB-Einheiten zu steuern oder die Vergrößerung auf UNLIMITED festzulegen.  
  
  
## <a name="see-also"></a>Siehe auch  
 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [Problembehandlung bei vollen Transaktionsprotokollen (SQL Server-Fehler 9002)](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
  
