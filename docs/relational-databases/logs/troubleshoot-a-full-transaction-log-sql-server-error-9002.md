---
title: Problembehandlung bei vollen Transaktionsprotokollen (SQL Server-Fehler 9002) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: logs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-transaction-log
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], full
- troubleshooting [SQL Server], full transaction log
- 9002 (Database Engine error)
- transaction logs [SQL Server], truncation
- backing up transaction logs [SQL Server], full logs
- transaction logs [SQL Server], full log
- full transaction logs [SQL Server]
ms.assetid: 0f23aa84-475d-40df-bed3-c923f8c1b520
caps.latest.revision: 59
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Active
ms.openlocfilehash: f4c82de87a706d4c4f80ae4502c7fe554910ef7f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="troubleshoot-a-full-transaction-log-sql-server-error-9002"></a>Problembehandlung bei vollen Transaktionsprotokollen (SQL Server-Fehler 9002)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema werden mögliche Lösungen für volle Transaktionsprotokolle erörtert und Vermeidungsstrategien vorgeschlagen. 
  
  Wenn das Transaktionsprotokoll voll ist, wird von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] der **Fehler 9002**ausgegeben. Das Protokoll kann sich füllen, wenn die Datenbank online ist oder wiederhergestellt wird. Wenn das Protokoll gefüllt wird, während die Datenbank online ist, bleibt die Datenbank online, sie kann aber nur gelesen und nicht aktualisiert werden. Wird das Protokoll während einer Wiederherstellung gefüllt, wird die Datenbank von [!INCLUDE[ssDE](../../includes/ssde-md.md)] als RESOURCE PENDING (ausstehende Ressource) markiert. In beiden Fällen ist eine Aktion seitens des Benutzers erforderlich, um Speicherplatz im Protokoll verfügbar zu machen.  
  
## <a name="responding-to-a-full-transaction-log"></a>Mögliche Vorgehensweisen bei einem vollen Transaktionsprotokoll  
 Die richtige Reaktion auf ein volles Transaktionsprotokoll hängt zum Teil davon ab, aufgrund welcher Bedingungen das Protokoll gefüllt wurde. 
 
 Mithilfe der Spalten **log_reuse_wait** und **log_reuse_wait_desc** der **sys.database**-Katalogsicht können Sie feststellen, wodurch eine Protokollkürzung verhindert wurde. Weitere Informationen finden Sie unter [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md). Eine Beschreibung von Faktoren, die eine Protokollkürzung verzögern können, finden Sie unter [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
> **WICHTIG!**  
>  Wenn sich die Datenbank zu dem Zeitpunkt, als der Fehler 9002 auftrat, gerade im Wiederherstellungsmodus befand, müssen Sie nach Behebung des Problems die Datenbank mithilfe von [ALTER DATABASE *database_name* SET ONLINE](../../t-sql/statements/alter-database-transact-sql-set-options.md) wiederherstellen.  
  
 Alternativ sind als Reaktion auf ein volles Transaktionsprotokoll auch folgende Aktionen möglich:  
  
-   Sichern des Protokolls.  
  
-   Freigeben von Speicherplatz, damit das Protokoll automatisch vergrößert werden kann.  
  
-   Verschieben der Protokolldatei auf einen Datenträger mit ausreichendem Speicherplatz.  
  
-   Vergrößern einer Protokolldatei.  
  
-   Hinzufügen einer Protokolldatei auf einem anderen Datenträger.  
  
-   Abschließen oder Abbrechen einer Transaktion mit langer Ausführungszeit.  
  
 Diese Alternativen werden in den folgenden Abschnitten erläutert. Wählen Sie diejenige Aktion aus, die sich am besten für Ihre Situation eignet.  
  
## <a name="back-up-the-log"></a>Sichern des Protokolls  
 Falls bei Verwendung des vollständigen oder massenprotokollierten Wiederherstellungsmodells das Transaktionsprotokoll nicht vor kurzem gesichert wurde, kann durch die Sicherung eine Protokollkürzung verhindert werden. Wenn das Protokoll noch nie gesichert wurde, müssen Sie **zwei Protokollsicherungen erstellen** , damit das Protokoll von [!INCLUDE[ssDE](../../includes/ssde-md.md)] bis zu dem Punkt abgeschnitten werden kann, an dem die letzte Sicherung erfolgte. Durch Kürzen des Protokolls wird Speicherplatz für neue Protokolldatensätze freigegeben. Sichern Sie das Protokoll in kürzeren Abständen, damit es nicht wieder so schnell aufgefüllt wird.  
  
 **So erstellen Sie eine Transaktionsprotokollsicherung**  
  
> **WICHTIG**  
>  Wenn die Datenbank beschädigt ist, gehen Sie unter [Protokollfragmentsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
-   [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
### <a name="freeing-disk-space"></a>Freigeben von Speicherplatz  
 Möglicherweise können Sie durch Löschen oder Verschieben anderer Dateien Speicherplatz auf dem Datenträger freigeben, das die Transaktionsprotokolldatei für die Datenbank enthält. Aufgrund des freigegebenen Speicherplatzes kann die Protokolldatei dann durch den Wiederherstellungsmechanismus automatisch vergrößert werden.  
  
### <a name="move-the-log-file-to-a-different-disk"></a>Verschieben der Protokolldatei auf einen anderen Datenträger  
 Wenn Sie auf dem Datenträger, auf dem die Protokolldatei aktuell gespeichert ist, nicht genügend Speicherplatz freigeben können, können Sie die Datei auf einen anderen Datenträger mit ausreichendem Speicherplatz verschieben.  
  
> **WICHTIG!** Protokolldateien sollten unter keinen Umständen in komprimierten Dateisystemen gespeichert werden.  
  
 **Verschieben einer Protokolldatei**  
  
-   [Verschieben von Datenbankdateien](../../relational-databases/databases/move-database-files.md)  
  
### <a name="increase-log-file-size"></a>Erhöhen der Größe der Protokolldatei  
 Wenn auf dem Protokolldatenträger Speicherplatz vorhanden ist, können Sie die Protokolldatei vergrößern. Die maximale Größe für Protokolldateien beträgt zwei Terabyte (TB) pro Protokolldatei.  
  
 **Erhöhen der Dateigröße**  
  
 Wenn die automatische Vergrößerung deaktiviert ist, die Datenbank online ist und auf dem Datenträger ausreichend Speicherplatz verfügbar ist, führen Sie einen der folgenden Schritte aus:  
  
-   Erhöhen Sie die Dateigröße manuell, um die Datei einmalig um einen bestimmten Wert zu vergrößern.  
  
-   Aktivieren Sie die automatische Vergrößerung, indem Sie mit der ALTER DATABASE-Anweisung für die Option FILEGROWTH ein Vergrößerungsinkrement ungleich Null festlegen.  
  
> **HINWEIS:** Erhöhen Sie in beiden Fällen den MAXSIZE-Wert, wenn die aktuelle Größenbeschränkung erreicht wurde.  
  
### <a name="add-a-log-file-on-a-different-disk"></a>Hinzufügen einer Protokolldatei auf einem anderen Datenträger  
 Fügen Sie der Datenbank mithilfe von ALTER DATABASE <database_name> ADD LOG FILE eine neue Protokolldatei auf einem anderen Datenträger hinzu, auf dem ausreichend Speicherplatz vorhanden ist.  
  
 **Hinzufügen einer Protokolldatei**  
  
-   [Hinzufügen von Daten- oder Protokolldateien zu einer Datenbank](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)  
## <a name="complete-or-kill-a-long-running-transaction"></a>Abschließen oder Abbrechen einer Transaktion mit langer Ausführungszeit
### <a name="discovering-long-running-transactions"></a>Ermitteln von Transaktionen mit langer Ausführungszeit
Eine Transaktion mit sehr langer Ausführungszeit kann zum Auffüllen des Transaktionsprotokolls führen. Verwenden Sie eine der folgenden Optionen, um nach lang andauernden Transaktionen zu suchen:
 - **[sys.dm_tran_database_transactions](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md).**
Diese dynamische Verwaltungssicht gibt Informationen zu Transaktionen auf Datenbankebene zurück. Bei einer lang andauernden Transaktion gehören der Zeitpunkt des ersten Protokolldatensatzes [(database_transaction_begin_time)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md), der aktuelle Status der Transaktion [(database_transaction_state)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)und die Protokollfolgenummer [(Log Sequence Number, LSN)](../backup-restore/recover-to-a-log-sequence-number-sql-server.md) des ersten Datensatzes im Transaktionsprotokoll [(database_transaction_begin_lsn)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)zu den Spalten von besonderem Interesse.

 - **[DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md).**
Mithilfe dieser Anweisung können Sie die Benutzer-ID des Transaktionsbesitzers identifizieren. Auf diese Weise können Sie die Quelle der Transaktion ermitteln und die Transaktion ordnungsgemäß beenden (durch ein Commit anstelle eines Rollbacks).

### <a name="kill-a-transaction"></a>Abbrechen einer Transaktion
Manchmal müssen Sie den Prozess einfach nur beenden. Möglicherweise müssen Sie dazu die [KILL](../../t-sql/language-elements/kill-transact-sql.md) -Anweisung verwenden. Verwenden Sie diese Anweisung jedoch sehr vorsichtig, besonders wenn gerade kritische Prozesse ausgeführt werden, die Sie nicht abbrechen möchten. Weitere Informationen finden Sie unter [KILL (Transact-SQL)](../../t-sql/language-elements/kill-transact-sql.md).

## <a name="see-also"></a>Siehe auch  
[KB-Supportartikel – Ein Transaktionsprotokoll wächst unerwartet in SQL Server oder wird voll](https://support.microsoft.com/en-us/kb/317375) [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Verwalten der Größe der Transaktionsprotokolldatei](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)   
 [Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [sp_add_log_file_recover_suspect_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql.md)  
  
  
