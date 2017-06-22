---
title: "Datenbank wiederherstellen (Seite „Optionen“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.restoredb.options.f1
ms.assetid: 9a75d48b-c25f-40f3-8ea1-32cfa8211754
caps.latest.revision: 68
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 698c8658d2a3d6779a8800c23e5c508351a05d12
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="restore-database-options-page"></a>Datenbank wiederherstellen (Seite Optionen)
  Verwenden Sie im Dialogfeld **Datenbank wiederherstellen** die Seite **Optionen** , um das Verhalten und das Ergebnis des Wiederherstellungsvorgangs zu ändern.  
  
 **So verwenden Sie SQL Server Management Studio zum Wiederherstellen einer Datenbanksicherung**  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [Definieren eines logischen Sicherungsmediums für ein Bandlaufwerk &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  Wenn Sie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]einen Wiederherstellungstask angeben, können Sie ein entsprechendes [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript generieren, das die RESTORE-Anweisungen für diesen Wiederherstellungsvorgang enthält. Zum Generieren des Skripts klicken Sie auf **Skript** , und wählen Sie dann ein Ziel für das Skript aus. Informationen zur RESTORE-Syntax finden Sie unter [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
## <a name="options"></a>Datenbank wiederherstellen  
  
### <a name="restore-options"></a>Wiederherstellungsoptionen  
 Verwenden Sie die Optionen des Bereichs **Wiederherstellungsoptionen** , um die Aspekte des Verhaltens des Wiederherstellungsvorgangs zu ändern.  
  
 **Vorhandene Datenbank überschreiben (WITH REPLACE)**  
 Beim Wiederherstellungsvorgang werden die Dateien jeder Datenbank überschrieben, die derzeit den Datenbanknamen verwendet, den Sie im Dialogfeld **Wiederherstellen in**auf der Seite [Allgemein](../../relational-databases/backup-restore/restore-database-general-page.md) im Feld **In Datenbank** angeben. Die Dateien der vorhandenen Datenbank werden sogar dann überschrieben, wenn Sie die Sicherungen von einer anderen Datenbank im vorhandenen Datenbanknamen wiederherstellen. Das Auswählen dieser Option entspricht der Verwendung der Option REPLACE in einer [RESTORE](../../t-sql/statements/restore-statements-arguments-transact-sql.md) -Anweisung ([!INCLUDE[tsql](../../includes/tsql-md.md)]).  
  
> [!CAUTION]  
>  Verwenden Sie diese Option nur nach sorgfältiger Überlegung. Weitere Informationen finden Sie unter [RESTORE-Argumente &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 **Replikationseinstellungen beibehalten (WITH KEEP_REPLICATION)**  
 Behält die Replikationseinstellungen bei, wenn eine veröffentlichte Datenbank auf einem Server wiederhergestellt wird, auf dem die Datenbank nicht erstellt wurde. Diese Option ist nur relevant, wenn die Datenbank beim Erstellen der Sicherung repliziert wurde.  
  
 Diese Option ist nur in Verbindung mit der Option **Datenbank betriebsbereit belassen, indem für Transaktionen ohne Commit ein Rollback ausgeführt wird** (wird in der Tabelle weiter unten beschrieben) verfügbar, die der Wiederherstellung einer Sicherungskopie mit der Option RECOVERY entspricht.  
  
 Das Auswählen dieser Option entspricht der Verwendung der Option KEEP_REPLICATION in einer [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) -Anweisung.  
  
 Weitere Informationen finden Sie unter [Sichern und Wiederherstellen von replizierten Datenbanken](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).  
  
 **Zugriff auf die wiederhergestellte Datenbank einschränken (WITH RESTRICTED_USER)**  
 Macht die wiederhergestellte Datenbank nur Mitgliedern von **db_owner**, **dbcreator**oder **sysadmin**verfügbar.  
  
 Das Auswählen dieser Option entspricht der Verwendung der Option RESTRICTED_USER in einer RESTORE-Anweisung.  
  
### <a name="recovery-state"></a>Wiederherstellungsstatus  
 Zum Bestimmen des Status der Datenbank nach dem Wiederherstellungsvorgang müssen Sie eine der Optionen des Bereichs **Wiederherstellungsstatus** angeben.  
  
 **RESTORE WITH RECOVERY**  
 Stellt die Datenbank nach der Wiederherstellung der im Raster **Wiederherzustellende Sicherungssätze**auf der Seite [Allgemein](../../relational-databases/backup-restore/restore-database-general-page.md)ausgewählten letzten Sicherung wieder her. Dies ist die Standardoption und entspricht der Angabe von WITH RECOVERY in einer [RESTORE](../../t-sql/statements/restore-statements-arguments-transact-sql.md) -Anweisung ([!INCLUDE[tsql](../../includes/tsql-md.md)]).  
  
> [!NOTE]  
>  Wählen Sie diese Option beim vollständigen Wiederherstellungsmodell oder beim massenprotokollierten Wiederherstellungsmodell nur dann aus, wenn Sie alle Protokolldateien jetzt wiederherstellen.  
  
 **RESTORE WITH NORECOVERY**  
 Belässt die Datenbank im Wiederherstellungsstatus. Auf diese Weise können Sie zusätzliche Sicherungen im aktuellen Wiederherstellungspfad wiederherstellen. Zum Wiederherstellen der Datenbank müssen Sie mithilfe der Option RESTORE WITH RECOVERY (siehe vorherige Option) einen Wiederherstellungsvorgang ausführen.  
  
 Diese Option entspricht der Angabe von WITH NORECOVERY in einer RESTORE-Anweisung.  
  
 Wenn Sie diese Option auswählen, ist die Option **Replikationseinstellungen beibehalten** nicht verfügbar.  
  
 **RESTORE WITH STANDBY**  
 Belässt die Datenbank in einem Standbystatus, in dem die Datenbank für den eingeschränkten schreibgeschützten Zugriff verfügbar ist. Diese Option entspricht der Angabe von WITH STANDBY in einer RESTORE-Anweisung.  
  
 Zum Auswählen dieser Option ist die Angabe einer Standbydatei im Textfeld **Standbydatei** erforderlich. Mithilfe der Standbydatei können die Auswirkungen der Wiederherstellung rückgängig gemacht werden.  
  
 **Standbydatei**  
 Gibt eine Standbydatei an. Sie können nach der Standbydatei suchen oder den Pfadnamen direkt in das Textfeld eingeben.  
  
### <a name="tail-log-backup"></a>Sicherung des Protokollfragments  
 Ermöglicht es Ihnen festzulegen, dass eine Sicherung des Protokollfragments mit der Datenbankwiederherstellung ausgeführt wird.  
  
 **Erstellen der Sicherung des Protokollfragments vor dem Wiederherstellen**  
 Aktivieren Sie dieses Kontrollkästchen, um festzulegen, dass eine Sicherung des Protokollfragments ausgeführt werden soll.  
  
> [!NOTE]  
>  Wenn der Zeitpunkt, den Sie im Dialogfeld [Sicherungszeitachse](../../relational-databases/backup-restore/backup-timeline.md) ausgewählt haben, eine Sicherung des Protokollfragments erfordert, wird dieses Kontrollkästchen aktiviert, und es ist keine Bearbeitung möglich.  
  
 **Sicherungsdatei**  
 Gibt eine Sicherungsdatei für das Protokollfragment an. Sie können nach der Sicherungsdatei suchen oder den Namen direkt in das Textfeld eingeben.  
  
### <a name="server-connections"></a>Serververbindungen  
 Ermöglicht es Ihnen, vorhandene Datenbankverbindungen zu schließen.  
  
 **Bestehende Verbindungen schließen**  
 Bei Wiederherstellungsvorgängen treten möglicherweise Fehler auf, wenn aktive Verbindungen zur Datenbank bestehen. Aktivieren Sie die Option **Bestehende Verbindungen schließen** , um sicherzustellen, dass alle aktiven Verbindungen zwischen [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] und der Datenbank geschlossen werden. Durch die Aktivierung dieses Kontrollkästchens wechselt die Datenbank in einen Einzelbenutzermodus, bevor Wiederherstellungsvorgänge ausgeführt werden. Außerdem wird dadurch die Datenbank auf einen Multibenutzermodus festgelegt, wenn der Vorgang abgeschlossen ist.  
  
### <a name="prompt"></a>Eingabeaufforderung  
 **Bestätigung vor Wiederherstellen jeder einzelnen Sicherung**  
 Gibt an, dass nach der Wiederherstellung der einzelnen Sicherungen das Dialogfeld **Wiederherstellung fortsetzen** angezeigt wird, um anzufragen, ob Sie die Wiederherstellungssequenz fortsetzen möchten. In diesem Dialogfeld werden der Name des nächsten Mediensatzes (wenn bekannt) und der Name sowie die Beschreibung des nächsten Sicherungssatzes angezeigt.  
  
 Mithilfe dieser Option können Sie eine Wiederherstellungssequenz nach der Wiederherstellung einer beliebigen Sicherung anhalten. Diese Option ist insbesondere dann hilfreich, wenn Sie Bänder für verschiedene Mediensätze wechseln müssen, z. B. wenn der Server nur über ein Bandmedium verfügt. Klicken Sie auf **OK**, wenn der Vorgang fortgesetzt werden soll.  
  
 Sie können eine Wiederherstellungssequenz unterbrechen, indem Sie auf **Nein**klicken. Dadurch wird die Datenbank im Wiederherstellungsstatus belassen. Sie können die Wiederherstellungssequenz ggf. später fortsetzen, indem Sie die nächste Sicherung gemäß der Beschreibung im Dialogfeld **Wiederherstellung fortsetzen** fortsetzen. Die Prozedur zum Wiederherstellen der nächsten Sicherung ist wie folgt davon abhängig, ob sie Daten oder ein Transaktionsprotokoll enthält:  
  
-   Wenn die nächste Sicherung eine vollständige oder differenzielle Sicherung ist, verwenden Sie den Task **Datenbank wiederherstellen** erneut.  
  
-   Handelt es sich bei der nächsten Sicherung um eine Dateisicherung, verwenden Sie den Task **Dateien und Dateigruppen wiederherstellen**. Weitere Informationen finden Sie unter [Wiederherstellen von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md).  
  
-   Wenn die nächste Sicherung eine Protokollsicherung ist, verwenden Sie den Task **Transaktionsprotokoll wiederherstellen** . Informationen zum Fortsetzen einer Wiederherstellungssequenz durch Wiederherstellen eines Transaktionsprotokolls finden Sie unter [Wiederherstellen einer Transaktionsprotokollsicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md).  
  
## <a name="see-also"></a>Siehe auch  
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Wiederherstellung einer Sicherung von einem Medium &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)   
 [Wiederherstellen einer Transaktionsprotokollsicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Datenbank wiederherstellen &#40;Seite „Allgemein“&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)  
  
  
