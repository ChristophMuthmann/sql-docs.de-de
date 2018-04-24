---
title: Mögliche Medienfehler während der Sicherung und Wiederherstellung (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- media errors [SQL Server]
- CONTINUE_AFTER_ERROR option
- errors [SQL Server], backups
- backups [SQL Server], errors
- RESTORE VERIFYONLY statement
- backup media [SQL Server], error management
- page checksums [SQL Server]
- backup checksums [SQL Server]
- backing up [SQL Server], media errors
- RESTORE statement, media errors
- NO_CHECKSUM option
- checksums [SQL Server]
ms.assetid: 83a27b29-1191-4f8d-9648-6e6be73a9b7c
caps.latest.revision: 37
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 69fa1e87c12541a507eb1970e1728a7548d1bb8c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="possible-media-errors-during-backup-and-restore-sql-server"></a>Mögliche Medienfehler während der Sicherung und Wiederherstellung (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] haben Sie die Möglichkeit, trotz erkannter Fehler eine Datenbank wiederherzustellen. Ein wichtiger neuer Fehlererkennungsmechanismus ist die optionale Erstellung einer Sicherungsprüfsumme, die von einem Sicherungsvorgang erstellt und von einem Wiederherstellungsvorgang überprüft wird. Sie können steuern, ob vom Vorgang auf Fehler geprüft wird, und ob der Vorgang beim Auftreten eines Fehlers beendet oder fortgesetzt wird. Wenn eine Sicherung eine Sicherungsprüfsumme enthält, kann mithilfe von RESTORE- und RESTORE VERIFYONLY-Anweisungen auf Fehler hin geprüft werden.  
  
> [!NOTE]  
>  Gespiegelte Sicherungen bieten bis zu fünf Kopien (Spiegel) eines Mediensatzes, womit alternative Kopien für die Wiederherstellung zur Verfügung gestellt werden, die durch beschädigte Medien ausgelöst wurden. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Gespiegelte Sicherungsmediensätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)noch nicht kennen.  
  
  
##  <a name="BckChecksums"></a> Sicherungsprüfsummen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden drei Prüfsummentypen unterstützt: eine Prüfsumme auf Seiten, eine Prüfsumme in Protokollblöcken und eine Sicherungsprüfsumme. Beim Generieren einer Sicherungsprüfsumme wird von BACKUP überprüft, ob die aus der Datenbank gelesenen Daten mit Prüfsummen oder Indikatoren für zerrissene Seiten konsistent sind, die möglicherweise in der Datenbank vorhanden sind.  
  
 Von der BACKUP-Anweisung wird optional eine Sicherungsprüfsumme auf dem Sicherungsdatenstrom berechnet. Wenn Seitenprüfsummen oder Informationen zu zerrissenen Seiten auf einer gegebenen Seite vorhanden sind, wird von BACKUP während der Seitensicherung die Prüfsumme, der Status für zerrissene Seiten und die Seiten-ID für die Seite überprüft. Beim Erstellen einer Sicherungsprüfsumme werden von Sicherungsvorgängen keine Prüfsummen zu Seiten hinzugefügt. Seiten werden so gesichert, wie sie in der Datenbank vorgefunden werden, und bleiben durch die Sicherung unverändert.  
  
 Wegen des Verwaltungsaufwands für das Überprüfen und Generieren von Prüfsummen stellen Sicherungsprüfsummen die potenzielle Gefahr einer Leistungseinbuße dar. Sowohl die Arbeitsauslastung als auch der Sicherungsdurchsatz können davon betroffen sein. Deshalb ist die Verwendung von Sicherungsprüfsummen optional. Wenn Sie sich für das Generieren von Prüfsummen während einer Sicherung entscheiden, behalten Sie den dadurch hervorgerufenen CPU-Verwaltungsaufwand genauso im Auge wie die Auswirkungen auf nebenläufige Arbeitsauslastungen für das System.  
  
 Von BACKUP wird in keinem Fall die Quellenseite auf dem Datenträger oder der Inhalt einer Seite verändert.  
  
 Wenn Sicherungsprüfsummen aktiviert werden, führt ein Sicherungsvorgang die folgenden Schritte aus:  
  
1.  Vor dem Schreiben einer Seite auf das Sicherungsmedium werden vom Sicherungsvorgang die Informationen auf Seitenebene überprüft (Seitenprüfsumme oder Erkennen zerrissener Seiten), soweit vorhanden. Wenn keines vorhanden ist, kann die Seite nicht von der Sicherung überprüft werden. Nicht überprüfte Seiten werden unverändert übernommen. Der Inhalt wird zur Gesamtsicherungsprüfsumme hinzugefügt.  
  
     Wenn vom Sicherungsvorgang während der Überprüfung ein Seitenfehler festgestellt wird, tritt bei der Sicherung ein Fehler auf.  
  
    > [!NOTE]  
    >  Weitere Informationen zu Seitenprüfsummen und dem Erkennen von zerrissenen Seiten finden Sie in der PAGE_VERIFY-Option der ALTER DATABASE-Anweisung. Weitere Informationen zu dieser Einstellung finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
2.  Unabhängig davon, ob Seitenprüfsummen vorhanden sind, generiert BACKUP eine separate Sicherungsprüfsumme für den Sicherungsdatenstrom. Bei den Wiederherstellungsvorgängen kann optional die Sicherungsprüfsumme verwendet werden, um zu überprüfen, ob die Sicherung beschädigt ist. Die Sicherungsprüfsumme wird auf den Sicherungsmedien gespeichert, nicht in den Datenbankseiten. Die Sicherungsprüfsumme kann bei der Wiederherstellung optional verwendet werden.  
  
3.  Der Sicherungssatz erhält die Markierung, dass er Sicherungsprüfsummen enthält (in der **has_backup_checksums** -Spalte von **msdb..backupset**). Weitere Informationen finden Sie unter [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md).  
  
 Wenn bei einem Sicherungsvorgang auf dem Sicherungsmedium Sicherungsprüfsummen vorhanden sind, werden standardmäßig die Sicherungsprüfsummen und Seitenprüfsummen von RESTORE- und RESTORE VERIFYONLY-Anweisungen überprüft. Wenn keine Sicherungsprüfsummen vorhanden sind, werden beide Wiederherstellungsvorgänge ohne Überprüfung fortgesetzt, weil ohne Sicherungsprüfsumme vom Wiederherstellungsvorgang keine Seitenprüfsummen verlässlich überprüft werden können.  
  
## <a name="response-to-page-checksum-errors-during-a-backup-or-restore-operation"></a>Antwort auf Fehler bei der Seitenprüfsumme während einer Sicherung oder eines Wiederherstellungsvorgangs  
 Nach dem Auftreten eines Fehlers bei der Seitenprüfsumme treten beim BACKUP- oder RESTORE-Vorgang standardmäßig Fehler auf, und ein RESTORE VERIFYONLY-Vorgang wird fortgesetzt. Sie können jedoch steuern, ob ein angegebener Vorgang fehlerhaft ist, wenn ein Fehler gefunden wird, oder ob er weiterhin so gut wie möglich fortgesetzt wird.  
  
 Wenn ein BACKUP-Vorgang nach dem Finden von Fehler fortgesetzt wird, werden vom Vorgang die folgenden Schritte ausgeführt:  
  
1.  Der Sicherungssatz auf dem Sicherungsmedium wird als fehlerhaft markiert, und die Seite wird in der **suspect_pages**-Tabelle in der **msdb**-Datenbank nachverfolgt. Weitere Informationen finden Sie unter [suspect_pages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md).  
  
2.  Der Fehler wird im SQL Server-Fehlerprotokoll protokolliert.  
  
3.  Der Sicherungssatz wird mit diesem Fehlertyp in der **is_damaged** -Spalte von **msdb.backupset**markiert. Weitere Informationen finden Sie unter [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md).  
  
4.  Es wird eine Meldung ausgegeben, dass die Sicherung erfolgreich generiert wurde, aber Seitenfehler enthält.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So aktivieren oder deaktivieren Sie Sicherungsprüfsummen**  
  
-   [Aktivieren oder deaktivieren von Sicherungsprüfsummen während der Sicherung oder Wiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
 **So steuern Sie die Antwort auf einen Fehler während eines Sicherungsvorgangs**  
  
-   [Angeben, ob ein Sicherungs- oder Wiederherstellungsvorgang fortgesetzt wird, nachdem ein Fehler festgestellt wurde &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Gespiegelte Sicherungsmediensätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
  
