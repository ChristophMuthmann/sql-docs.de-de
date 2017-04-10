---
title: "M&#246;gliche Medienfehler w&#228;hrend der Sicherung und Wiederherstellung (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Medienfehler [SQL Server]"
  - "CONTINUE_AFTER_ERROR (Option)"
  - "Fehler [SQL Server], Sicherungen"
  - "Sicherungen [SQL Server], Fehler"
  - "RESTORE VERIFYONLY-Anweisung"
  - "Sicherungsmedien [SQL Server], Fehlerverwaltung"
  - "Seitenprüfsummen [SQL Server]"
  - "Sicherungsprüfsummen [SQL Server]"
  - "Sichern [SQL Server], Medienfehler"
  - "RESTORE-Anweisung, Medienfehler"
  - "NO_CHECKSUM (Option)"
  - "Prüfsummen [SQL Server]"
ms.assetid: 83a27b29-1191-4f8d-9648-6e6be73a9b7c
caps.latest.revision: 37
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 36
---
# M&#246;gliche Medienfehler w&#228;hrend der Sicherung und Wiederherstellung (SQL Server)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] haben Sie die Möglichkeit, trotz erkannter Fehler eine Datenbank wiederherzustellen. Ein wichtiger neuer Fehlererkennungsmechanismus ist die optionale Erstellung einer Sicherungsprüfsumme, die von einem Sicherungsvorgang erstellt und von einem Wiederherstellungsvorgang überprüft wird. Sie können steuern, ob vom Vorgang auf Fehler geprüft wird, und ob der Vorgang beim Auftreten eines Fehlers beendet oder fortgesetzt wird. Wenn eine Sicherung eine Sicherungsprüfsumme enthält, kann mithilfe von RESTORE- und RESTORE VERIFYONLY-Anweisungen auf Fehler hin geprüft werden.  
  
> [!NOTE]  
>  Gespiegelte Sicherungen bieten bis zu fünf Kopien (Spiegel) eines Mediensatzes, womit alternative Kopien für die Wiederherstellung zur Verfügung gestellt werden, die durch beschädigte Medien ausgelöst wurden. Weitere Informationen finden Sie unter [Gespiegelte Sicherungsmediensätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md).  
  
 **In diesem Thema:**  
  
-   [Sicherungsprüfsummen](#BckChecksums)  
  
-   [Antwort auf Fehler bei der Seitenprüfsumme während einer Sicherung oder eines Wiederherstellungsvorgangs](#ResponsetoPageChecksumErrors)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="BckChecksums"></a> Sicherungsprüfsummen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden drei Prüfsummentypen unterstützt: eine Prüfsumme auf Seiten, eine Prüfsumme in Protokollblöcken und eine Sicherungsprüfsumme. Beim Generieren einer Sicherungsprüfsumme wird von BACKUP überprüft, ob die aus der Datenbank gelesenen Daten mit Prüfsummen oder Indikatoren für zerrissene Seiten konsistent sind, die möglicherweise in der Datenbank vorhanden sind.  
  
 Von der BACKUP-Anweisung wird optional eine Sicherungsprüfsumme auf dem Sicherungsdatenstrom berechnet. Wenn Seitenprüfsummen oder Informationen zu zerrissenen Seiten auf einer gegebenen Seite vorhanden sind, wird von BACKUP während der Seitensicherung die Prüfsumme, der Status für zerrissene Seiten und die Seiten-ID für die Seite überprüft. Beim Erstellen einer Sicherungsprüfsumme werden von Sicherungsvorgängen keine Prüfsummen zu Seiten hinzugefügt. Seiten werden so gesichert, wie sie in der Datenbank vorgefunden werden, und bleiben durch die Sicherung unverändert.  
  
 Wegen des Verwaltungsaufwands für das Überprüfen und Generieren von Prüfsummen stellen Sicherungsprüfsummen die potenzielle Gefahr einer Leistungseinbuße dar. Sowohl die Arbeitsauslastung als auch der Sicherungsdurchsatz können davon betroffen sein. Deshalb ist die Verwendung von Sicherungsprüfsummen optional. Wenn Sie sich für das Generieren von Prüfsummen während einer Sicherung entscheiden, behalten Sie den dadurch hervorgerufenen CPU-Verwaltungsaufwand genauso im Auge wie die Auswirkungen auf nebenläufige Arbeitsauslastungen für das System.  
  
 Von BACKUP wird in keinem Fall die Quellenseite auf dem Datenträger oder der Inhalt einer Seite verändert.  
  
 Wenn Sicherungsprüfsummen aktiviert werden, führt ein Sicherungsvorgang die folgenden Schritte aus:  
  
1.  Vor dem Schreiben einer Seite auf das Sicherungsmedium werden vom Sicherungsvorgang die Informationen auf Seitenebene überprüft (Seitenprüfsumme oder Erkennen zerrissener Seiten), soweit vorhanden. Wenn keines vorhanden ist, kann die Seite nicht von der Sicherung überprüft werden. Nicht überprüfte Seiten werden unverändert übernommen. Der Inhalt wird zur Gesamtsicherungsprüfsumme hinzugefügt.  
  
     Wenn vom Sicherungsvorgang während der Überprüfung ein Seitenfehler festgestellt wird, tritt bei der Sicherung ein Fehler auf.  
  
    > [!NOTE]  
    >  Weitere Informationen zu Seitenprüfsummen und dem Erkennen von zerrissenen Seiten finden Sie in der PAGE_VERIFY-Option der ALTER DATABASE-Anweisung. Weitere Informationen zu dieser Einstellung finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md).  
  
2.  Unabhängig davon, ob Seitenprüfsummen vorhanden sind, generiert BACKUP eine separate Sicherungsprüfsumme für den Sicherungsdatenstrom. Bei den Wiederherstellungsvorgängen kann optional die Sicherungsprüfsumme verwendet werden, um zu überprüfen, ob die Sicherung beschädigt ist. Die Sicherungsprüfsumme wird auf den Sicherungsmedien gespeichert, nicht in den Datenbankseiten. Die Sicherungsprüfsumme kann bei der Wiederherstellung optional verwendet werden.  
  
3.  Der Sicherungssatz erhält die Markierung, dass er Sicherungsprüfsummen enthält (in der **has_backup_checksums**-Spalte von **msdb..backupset**). Weitere Informationen finden Sie unter [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md).  
  
 Wenn bei einem Sicherungsvorgang auf dem Sicherungsmedium Sicherungsprüfsummen vorhanden sind, werden standardmäßig die Sicherungsprüfsummen und Seitenprüfsummen von RESTORE- und RESTORE VERIFYONLY-Anweisungen überprüft. Wenn keine Sicherungsprüfsummen vorhanden sind, werden beide Wiederherstellungsvorgänge ohne Überprüfung fortgesetzt, weil ohne Sicherungsprüfsumme vom Wiederherstellungsvorgang keine Seitenprüfsummen verlässlich überprüft werden können.  
  
## Antwort auf Fehler bei der Seitenprüfsumme während einer Sicherung oder eines Wiederherstellungsvorgangs  
 Nach dem Auftreten eines Fehlers bei der Seitenprüfsumme treten beim BACKUP- oder RESTORE-Vorgang standardmäßig Fehler auf, und ein RESTORE VERIFYONLY-Vorgang wird fortgesetzt. Sie können jedoch steuern, ob ein angegebener Vorgang fehlerhaft ist, wenn ein Fehler gefunden wird, oder ob er weiterhin so gut wie möglich fortgesetzt wird.  
  
 Wenn ein BACKUP-Vorgang nach dem Finden von Fehler fortgesetzt wird, werden vom Vorgang die folgenden Schritte ausgeführt:  
  
1.  Der Sicherungssatz auf dem Sicherungsmedium wird als fehlerhaft markiert, und die Seite wird in der **suspect_pages**-Tabelle in der **msdb**-Datenbank nachverfolgt. Weitere Informationen finden Sie unter [suspect_pages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md).  
  
2.  Der Fehler wird im SQL Server-Fehlerprotokoll protokolliert.  
  
3.  Der Sicherungssatz wird mit diesem Fehlertyp in der **is_damaged**-Spalte von **msdb.backupset** markiert. Weitere Informationen finden Sie unter [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md).  
  
4.  Es wird eine Meldung ausgegeben, dass die Sicherung erfolgreich generiert wurde, aber Seitenfehler enthält.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So aktivieren oder deaktivieren Sie Sicherungsprüfsummen**  
  
-   [Aktivieren oder deaktivieren von Sicherungsprüfsummen während der Sicherung oder Wiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
 **So steuern Sie die Antwort auf einen Fehler während eines Sicherungsvorgangs**  
  
-   [Angeben, ob ein Sicherungs- oder Wiederherstellungsvorgang fortgesetzt wird, nachdem ein Fehler festgestellt wurde &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify if backup or restore continues or stops after error.md)  
  
## Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Gespiegelte Sicherungsmediensätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../Topic/RESTORE%20VERIFYONLY%20\(Transact-SQL\).md)  
  
  