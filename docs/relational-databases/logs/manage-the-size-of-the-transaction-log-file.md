---
title: "Verwalten der Größe der Transaktionsprotokolldatei | Microsoft Docs"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction logs [SQL Server], size management
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 6d75e0e40c5642993cb17b09e421fbfebf40f87a
ms.openlocfilehash: cd1931ef0f77c0a1e31c29833f38c51416e267c8
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="manage-the-size-of-the-transaction-log-file"></a>Verwalten der Größe der Transaktionsprotokolldatei
In diesem Thema wird beschrieben, wie Überwachen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Größe des Transaktionsprotokolls, Verkleinern des Transaktionsprotokolls, hinzufügen oder vergrößern eine Transaktionsprotokolldatei, Optimieren der **Tempdb** Wachstumsrate-Transaktionsprotokolls und Steuern der Vergrößerung einer Transaktionsprotokolldatei.  

  ##  <a name="MonitorSpaceUse"></a> Überwachen der Verwendung von Protokollspeicherplatz  
Überwachen der Verwendung von Protokollspeicherplatz mit [DBCC SQLPERF (LOGSPACE)](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql). Dieser Befehl gibt Informationen zum derzeit belegten Protokollspeicherplatz zurück und zeigt an, wann das Transaktionsprotokoll abgeschnitten werden muss. Weitere Informationen finden Sie unter [DBCC SQLPERF Transact-SQL](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md). Informationen zum aktuellen Größe der Protokolldatei die maximale Größe und die Option "Autogrow" für die Datei, können Sie auch die **Größe**, **Max_size**, und **Wachstum** Spalten für die betreffende Protokolldatei in **Sys. database_files**. Weitere Informationen finden Sie unter [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).  
  
**Wichtig!** Vermeiden Sie das Überlasten des Protokolldatenträgers!  

  
##  <a name="ShrinkSize"></a> Verkleinern der Protokolldateigröße  
 Sie müssen zum Reduzieren der physischen Größe einer physischen Protokolldatei die Protokolldatei verkleinern. Dies ist hilfreich, wenn Sie wissen, dass eine Transaktionsprotokolldatei ungenutzten Speicherplatz enthält. Nur, während die Datenbank online ist und mindestens eine virtuelle Protokolldatei frei ist, können Sie eine Protokolldatei verkleinern. In einigen Fällen ist eine Verkleinerung des Protokolls möglicherweise erst nach der nächsten Protokollkürzung möglich.  
  
> [!NOTE]
>  Faktoren, wie z. B. lang andauernde Transaktionen, die virtuelle Protokolldateien über einen längeren Zeitraum hinweg aktiv halten, können die Protokollverkleinerung einschränken oder sogar gänzlich verhindern. Informationen zu Faktoren, die eine Protokollkürzung verzögern können, finden Sie unter [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
 Beim Verkleinern einer Protokolldatei werden virtuelle Protokolldateien entfernt, die keinen Teil des logischen Protokolls enthalten (d.h. *inaktive virtuelle Protokolldateien*). Wenn eine Transaktionsprotokolldatei verkleinert wird, werden inaktive virtuelle Protokolldateien vom Ende der Protokolldatei, um das Protokoll in etwa die Zielgröße zu verkleinern entfernt.  
  
 **Verkleinern einer Protokolldatei (ohne die Datenbankdateien zu verkleinern)**  
  
-   [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
  
-   [Verkleinern einer Datei](../../relational-databases/databases/shrink-a-file.md)  
  
 **Überwachen der Protokollverkleinerungsereignisse**  
  
-   [Log File Auto Shrink Event Class](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md).  
  
 **Überwachen von Protokollspeicherplatz**  
  
-   [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)  
  
-   [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) (Informationen finden Sie in den Spalten **size**, **max_size** und **growth** für die Protokolldateien.)  
  
> [!NOTE]
>  Sie können Protokolldateien automatisch verkleinert festlegen. Es wird jedoch von einer automatischen Verkleinerung abgeraten, und die **autoshrink** -Datenbankeigenschaft ist in den Standardeinstellungen auf FALSE festgelegt. Wenn **autoshrink** auf TRUE festgelegt ist, wird die Größe einer Datei nur dann automatisch verkleinert, wenn mehr als 25 Prozent des Speicherplatzes ungenutzt sind. Die Datei wird entweder auf eine Größe verkleinert, bei der 25 Prozent der Datei aus nicht verwendetem Speicherplatz bestehen, oder auf die ursprüngliche Dateigröße, je nachdem, welcher Wert größer ist. Informationen zum Ändern der Einstellung der der **autoshrink** -Eigenschaft finden Sie unter [Anzeigen oder Ändern der Eigenschaften einer Datenbank](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md). Verwenden Sie die Eigenschaft **AutoShrink** auf der Seite **Optionen** oder alternativ unter [ALTER DATABASE SET-Optionen&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) die Option AUTO_SHRINK.  
  

##  <a name="AddOrEnlarge"></a> Hinzufügen oder Vergrößern einer Protokolldatei  
 Sie können Speicherplatz gewinnen, indem Sie die vorhandene Protokolldatei vergrößern, (wenn der Speicherplatz dies zulässt) oder durch Hinzufügen einer Protokolldatei in der Datenbank, in der Regel auf einen anderen Datenträger.  
  
-   Sie können der Datenbank eine Protokolldatei hinzufügen, indem Sie die ADD LOG FILE-Klausel der ALTER DATABASE-Anweisung verwenden. Durch das Hinzufügen einer Protokolldatei kann das Protokoll vergrößert werden.  
  
-   Sie können die Protokolldatei vergrößern, indem Sie die MODIFY FILE-Klausel der ALTER DATABASE-Anweisung verwenden und die SIZE- und MAXSIZE-Syntax angeben. Weitere Informationen finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
    
  
##  <a name="tempdbOptimize"></a> Optimieren der Größe des tempdb-Transaktionsprotokolls  
 Beim Neustarten einer Serverinstanz wird das Transaktionsprotokoll der **tempdb** -Datenbank auf seine ursprüngliche Größe (vor einer automatischen Größenerweiterung) zurückgesetzt. Dies kann eine Leistungsminderung des **tempdb** -Transaktionsprotokolls zur Folge haben. Der damit verbundene Verwaltungsaufwand lässt sich vermeiden, indem Sie nach dem Starten oder erneuten Starten der Serverinstanz die Größe des **tempdb** -Transaktionsprotokolls erhöhen. Weitere Informationen finden Sie unter [tempdb Database](../../relational-databases/databases/tempdb-database.md).  
  
  
##  <a name="ControlGrowth"></a> Steuern einer Transaktionsprotokolldatei  
 Verwenden der [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md) Anweisung, um die Vergrößerung einer Transaktionsprotokolldatei zu verwalten. Beachten Sie Folgendes:  
  
-   Verwenden Sie die Option SIZE, um die aktuelle Dateigröße in KB-, MB-, GB- und TB-Einheiten zu ändern.  
  -   Verwenden Sie die Option FILEGROWTH, um die Vergrößerungsschrittweite zu ändern. Der Wert 0 gibt an, dass die automatische Vergrößerung deaktiviert und kein zusätzlicher Speicherplatz zulässig ist. Die Einstellung der kleinen automatischen Vergrößerungsschrittweite einer Protokolldatei kann ebenfalls die Leistung beeinträchtigen. Die Schrittweite für die Dateivergrößerung sollte für eine Protokolldatei stets groß genug sein, um häufige Erweiterungen zu vermeiden. Die standardmäßige Vergrößerungsschrittweite von 10 Prozent ist hierfür im Allgemeinen gut geeignet.  

Informationen zum Ändern der Eigenschaft für die Dateivergrößerung in einer Protokolldatei finden Sie unter [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/ms174269.aspx).  
  
-   Verwenden Sie die Option MAXSIZE, um die maximale Größe einer Protokolldatei in KB-, MB-, GB- und TB-Einheiten zu steuern oder die Vergrößerung auf UNLIMITED festzulegen.  
  
  
## <a name="see-also"></a>Siehe auch  
 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [Problembehandlung bei vollen Transaktionsprotokollen (SQL Server-Fehler 9002)](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
  

