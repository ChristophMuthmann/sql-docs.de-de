---
title: "Sichern des Transaktionsprotokolls bei beschädigter Datenbank (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [SQL Server], damaged
- backing up [SQL Server]. damaged database
- transaction log backups [SQL Server], damaged databases
ms.assetid: 9b8873cc-df54-4336-ab9b-8f525132c2b0
caps.latest.revision: "29"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 99d8836c970ffac99f3468176132a48522aa7df6
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="back-up-the-transaction-log-when-the-database-is-damaged-sql-server"></a>Sichern des Transaktionsprotokolls bei beschädigter Datenbank (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Sie ein Transaktionsprotokoll in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] sichern können, wenn die Datenbank beschädigt ist.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
     [Security](#Security)  
  
-   **Sichern des Transaktionsprotokolls bei beschädigter Datenbank mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Die BACKUP-Anweisung ist nicht in einer expliziten oder implizierten Transaktion zulässig.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Im Allgemeinen müssen Sie für eine Datenbank, die entweder das vollständige oder das massenprotokollierte Wiederherstellungsmodell verwendet, das Protokollfragment sichern, bevor Sie mit der Wiederherstellung der Datenbank beginnen. Vor dem Ausführen eines Failovers einer Protokollversandkonfiguration sollten Sie ebenfalls das Protokollfragment der primären Datenbank sichern. Das Sichern des Protokollfragments als abschließende Protokollsicherung vor dem Wiederherstellen der Datenbank vermeidet den Datenverlust nach einem Fehler. Weitere Informationen zu Sicherungen des Protokollfragments finden Sie unter [Protokollfragmentsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Mitglieder der festen Serverrolle **sysadmin** und der festen Datenbankrollen **db_owner** und **db_backupoperator** verfügen standardmäßig über BACKUP DATABASE- und BACKUP LOG-Berechtigungen.  
  
 Besitz- und Berechtigungsprobleme im Zusammenhang mit der physischen Datei des Sicherungsmediums können den Sicherungsvorgang beeinträchtigen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss über Lese- und Schreibberechtigungen für das Medium verfügen. Das Konto, unter dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ausgeführt wird, muss Schreibberechtigungen haben. Allerdings prüft die gespeicherte Prozedur [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), die den Systemtabellen einen Eintrag für ein Sicherungsmedium hinzufügt, nicht die Dateizugriffsberechtigungen. Solche Probleme mit der physischen Datei des Sicherungsmediums treten möglicherweise erst auf, wenn auf die physische Ressource zugegriffen wird, um einen Sicherungs- oder Wiederherstellungsvorgang auszuführen.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-back-up-the-tail-of-the-transaction-log"></a>So sichern Sie das Transaktionsprotokollfragment  
  
1.  Klicken Sie im Objekt-Explorer nach dem Herstellen einer Verbindung mit der entsprechenden Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Datenbanken**, und wählen Sie je nach Datenbank eine Benutzerdatenbank aus, oder erweitern Sie **Systemdatenbanken** , und wählen Sie eine Systemdatenbank aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, zeigen Sie auf **Tasks**, und klicken Sie anschließend auf **Sichern**. Das Dialogfeld **Datenbank sichern** wird angezeigt.  
  
4.  Überprüfen Sie den Datenbanknamen im Listenfeld **Datenbank** . Sie können optional eine andere Datenbank aus der Liste auswählen.  
  
5.  Überprüfen Sie, ob als Wiederherstellungsmodell entweder **FULL** oder **BULK_LOGGED**ausgewählt wurde.  
  
6.  Wählen Sie im Listenfeld **Sicherungstyp** den Eintrag **Transaktionsprotokoll**aus.  
  
7.  Lassen Sie **Nur Sicherung kopieren** deaktiviert.  
  
8.  Akzeptieren Sie im Bereich **Sicherungssatz** entweder den im Textfeld **Name** vorgeschlagenen Standardnamen für den Sicherungssatz, oder geben Sie einen anderen Namen für den Sicherungssatz ein.  
  
9. Geben Sie im Textfeld **Beschreibung** eine Beschreibung für die Sicherung des Protokollfragments ein.  
  
10. Geben Sie an, wann der Sicherungssatz ablaufen soll:  
  
    -   Wenn der Sicherungssatz nach einer bestimmten Anzahl von Tagen ablaufen soll, klicken Sie auf **Nach** (die Standardoption), und geben Sie an, nach wie vielen Tagen der Sicherungssatz abläuft. Dieser Wert kann zwischen 0 und 99999 Tagen liegen. Ein Wert von 0 Tagen bedeutet, dass der Sicherungssatz nicht abläuft.  
  
         Der Standardwert wird im Dialogfeld **Servereigenschaften** (Seite **Datenbankeinstellungen** ) über die Option**Standardbeibehaltung für Sicherungsmedien (in Tagen)** festgelegt. Klicken Sie zum Zugreifen auf dieses Dialogfeld im Objekt-Explorer mit der rechten Maustaste auf den Servernamen, und wählen Sie „Eigenschaften“ aus. Wählen Sie anschließend die Seite **Datenbankeinstellungen** aus.  
  
    -   Zum Speichern des Sicherungssatzes an einem bestimmten Datum klicken Sie auf **Am**. Geben Sie das Datum ein, an dem der Sicherungssatz abläuft.  
  
11. Wählen Sie den Sicherungszieltyp aus, indem Sie auf **Datenträger** oder **Band**klicken. Klicken Sie auf **Hinzufügen**, um die Pfade von bis zu 64 Datenträgern oder Bandlaufwerken, die einen einzelnen Mediensatz enthalten, auszuwählen. Die ausgewählten Pfade werden im Listenfeld **Sichern auf** angezeigt.  
  
     Um einen Sicherungsziel zu entfernen, wählen Sie ihn aus, und klicken Sie auf **Entfernen**. Zum Anzeigen des Inhalts eines Sicherungsziels wählen Sie es aus, und klicken Sie auf **Inhalt**.  
  
12. Wählen Sie auf der Seite **Optionen** eine Option von **Medium überschreiben** aus, indem Sie auf eine der folgenden Optionen klicken:  
  
    -   **Auf vorhandenen Mediensatz sichern**  
  
         Klicken Sie bei dieser Option entweder auf **An vorhandenen Sicherungssatz anfügen** oder auf **Alle vorhandenen Sicherungssätze überschreiben**.  
  
         Sie können bei Bedarf das Kontrollkästchen **Mediensatznamen und Ablaufzeit des Sicherungssatzes überprüfen** aktivieren, damit beim Sicherungsvorgang das Datum und die Uhrzeit überprüft werden, an dem bzw. zu der der Mediensatz und der Sicherungssatz ablaufen.  
  
         Geben Sie optional einen Namen im Textfeld **Mediensatzname** ein. Wenn kein Name angegeben wurde, wird ein Mediensatz mit leerem Namen erstellt. Wenn Sie einen Mediensatznamen angeben, wird überprüft, ob der tatsächliche Name des Mediums (Band oder Datenträger) mit dem eingegebenen Namen übereinstimmt.  
  
         Wenn Sie den Mediennamen leer lassen und das Kontrollkästchen aktivieren, um ihn anhand des Mediums zu überprüfen, ist die Prüfung erfolgreich, wenn der Medienname auf dem Medium ebenfalls leer ist.  
  
    -   **Auf neuen Mediensatz sichern und alle vorhandenen Sicherungssätze löschen**  
  
         Geben Sie bei dieser Option einen Namen in das Textfeld **Name für neuen Mediensatz** und optional eine Beschreibung des Mediensatzes in das Textfeld **Beschreibung für neuen Mediensatz** ein.  
  
     Weitere Informationen über Mediensätze finden Sie unter [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
13. Im Bereich **Zuverlässigkeit** können Sie folgende Optionen aktivieren:  
  
    -   **Sicherung nach dem Abschluss überprüfen**.  
  
    -   **Vor dem Schreiben auf die Medien Prüfsumme bilden**  
  
    -   **Bei Prüfsummenfehler fortfahren**  
  
     Weitere Informationen finden Sie unter [Mögliche Medienfehler während der Sicherung und Wiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
14. Aktivieren Sie im Abschnitt **Transaktionsprotokoll** die Option **Protokollfragment sichern und Datenbank im Wiederherstellungsstatus belassen**.  
  
     Dies entspricht dem Angeben der folgenden [BACKUP](../../t-sql/statements/backup-transact-sql.md) -Anweisung:  
  
     `BACKUP LOG <database_name> TO <backup_device> WITH NORECOVERY`  
  
    > [!IMPORTANT]  
    >  Zur Wiederherstellungszeit wird im Dialogfeld „Datenbank wiederherstellen“ der Typ einer Protokollfragmentsicherung als **Transaktionsprotokoll (Nur Kopie)**angezeigt.  
  
15. Wenn Sie auf ein Bandlaufwerk sichern (gemäß der Konfiguration im Abschnitt **Ziel** der Seite **Allgemein** ), ist die Option **Band nach dem Sichern entladen** aktiviert. Wenn Sie auf diese Option klicken, wird die Option **Band vor dem Entladen zurückspulen** aktiviert.  
  
16. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] und höheren Versionen wird die [Sicherungskomprimierung](../../relational-databases/backup-restore/backup-compression-sql-server.md). Ob eine Sicherung standardmäßig komprimiert wird, ist abhängig vom Wert der Serverkonfigurationsoption **backup-compression default** . Sie können jedoch unabhängig von der aktuellen Standardeinstellung auf Serverebene eine Sicherung komprimieren, indem Sie die Option **Sicherung komprimieren**aktivieren, oder die Komprimierung verhindern, indem Sie die Option **Sicherung nicht komprimieren**aktivieren.  
  
     **So zeigen Sie die aktuelle Standardeinstellung für die Sicherungskomprimierung (Option "backup compression default") an**  
  
    -   [Anzeigen oder Konfigurieren der Serverkonfigurationsoption Standardeinstellung für die Sicherungskomprimierung](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-a-backup-of-the-currently-active-transaction-log"></a>So erstellen Sie eine Sicherung des aktuell aktiven Transaktionsprotokolls  
  
1.  Führen Sie die BACKUP LOG-Anweisung aus, um das aktuell aktive Transaktionsprotokoll zu sichern, und geben Sie dabei Folgendes an:  
  
    -   Den Namen der Datenbank, zu der das zu sichernde Transaktionsprotokoll gehört.  
  
    -   Das Sicherungsmedium, auf das die Transaktionsprotokollsicherung geschrieben wird.  
  
    -   Die NO_TRUNCATE-Klausel.  
  
         Mit dieser Klausel ist ein Sichern des aktiven Teils des Transaktionsprotokolls auch dann möglich, wenn nicht auf die Datenbank zugegriffen werden kann. Voraussetzung hierfür ist allerdings, dass auf die Transaktionsprotokolldateien zugegriffen werden kann und diese unbeschädigt sind.  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
  
> [!NOTE]  
>  In diesem Beispiel wird [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]verwendet, das das einfache Wiederherstellungsmodell verwendet. Um Protokollsicherungen zu ermöglichen, wurde für die Datenbank vor dem Erstellen einer vollständigen Datenbanksicherung die Verwendung des vollständigen Wiederherstellungsmodells festgelegt. Weitere Informationen finden Sie unter [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
 In diesem Beispiel wird das derzeit aktive Transaktionsprotokoll bei einer beschädigten oder nicht erreichbaren Datenbank gesichert, sofern das Transaktionsprotokoll unbeschädigt und erreichbar ist.  
  
```scr  
BACKUP LOG AdventureWorks2012  
   TO MyAdvWorks_FullRM_log1  
   WITH NO_TRUNCATE;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Wiederherstellen einer Transaktionsprotokollsicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [Wiederherstellen einer SQL Server-Datenbank zu einem Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [Datenbank sichern &#40;Seite 'Sicherungsoptionen'&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)   
 [Datenbank sichern &#40;Seite Allgemein&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)   
 [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Dateiwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Dateiwiederherstellungen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)  
  
  
