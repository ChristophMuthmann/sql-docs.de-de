---
title: Erstellen einer differenziellen Datenbanksicherung (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full differential backups [SQL Server]
- database backups [SQL Server], full differential backups
- backing up databases [SQL Server], full differential backups
- backups [SQL Server], creating
ms.assetid: 70f49794-b217-4519-9f2a-76ed61fa9f99
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 72e15006bdae1d2ae6d33a9780b62f17fd88a69b
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-differential-database-backup-sql-server"></a>Erstellen einer differenziellen Datenbanksicherung (SQL Server)
  Erstellen Sie eine differenzielle Datenbanksicherung in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Abschnitte in diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **So erstellen Sie eine differenzielle Datenbanksicherung mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Limitations and restrictions  
  
-   Die BACKUP-Anweisung ist nicht in einer expliziten oder implizierten Transaktion zulässig.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Eine differenzielle Datenbanksicherung kann nur erstellt werden, wenn bereits eine frühere vollständige Datenbanksicherung vorhanden ist. Wenn Ihre Datenbank noch nie gesichert wurde, führen Sie vor dem Erstellen differenzieller Sicherungen zunächst eine vollständige Datenbanksicherung aus. Weitere Informationen finden Sie unter [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Mit zunehmender Größe der differenziellen Sicherungen wird durch das Wiederherstellen einer differenziellen Sicherung der Zeitaufwand zum Wiederherstellen einer Datenbank erheblich erhöht. Sie sollten in regelmäßigen Abständen neue vollständige Sicherungen ausführen, um eine neue differenzielle Basis für die Daten zu erstellen. Sie können z. B. einmal wöchentlich eine vollständige Sicherung der gesamten Datenbank (also eine vollständige Datenbanksicherung) und während der Woche eine regelmäßige Serie von differenziellen Datenbanksicherungen ausführen.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Überprüfen Sie zuerst Ihre Berechtigungen!  
 Mitglieder der festen Serverrolle **sysadmin** und der festen Datenbankrollen **db_owner** und **db_backupoperator** verfügen standardmäßig über BACKUP DATABASE- und BACKUP LOG-Berechtigungen.  
  
 Besitz- und Berechtigungsprobleme im Zusammenhang mit der physischen Datei des Sicherungsmediums beeinträchtigen den Sicherungsvorgang. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss über Lese- und Schreibberechtigungen für das Medium verfügen. Das Konto, unter dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ausgeführt wird, muss Schreibberechtigungen haben. Allerdings prüft die gespeicherte Prozedur [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), die den Systemtabellen einen Eintrag für ein Sicherungsmedium hinzufügt, **nicht** die Dateizugriffsberechtigungen. Berechtigungsprobleme mit der physischen Datei des Sicherungsmediums treten erst zutage, wenn auf die physische Ressource zugegriffen wird, um einen Sicherungs- oder Wiederherstellungsvorgang auszuführen.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio  
  
#### <a name="create-a-differential-database-backup"></a>Erstellen einer differenziellen Datenbanksicherung  
  
1.  Klicken Sie im Objekt-Explorer nach dem Herstellen einer Verbindung mit der entsprechenden Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie den Ordner **Datenbanken**, und wählen Sie dann je nach Datenbank entweder eine Benutzerdatenbank aus, oder erweitern Sie die Option **Systemdatenbanken** , um eine Systemdatenbank auszuwählen.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, zeigen Sie auf **Tasks**, und klicken Sie dann auf **Sichern**. Das Dialogfeld **Datenbank sichern** wird angezeigt.  
  
4.  Überprüfen Sie den Datenbanknamen im Listenfeld **Datenbank** . Sie können optional eine andere Datenbank aus der Liste auswählen.  
  
     Sie können für jedes Wiederherstellungsmodell (vollständig, massenprotokolliert oder einfach) eine differenzielle Sicherung ausführen.  
  
5.  Wählen Sie im Listenfeld **Sicherungstyp** die Option **Differenziell**aus.  
  
    > [!IMPORTANT]  
    >  Stellen Sie sicher, dass das Kontrollkästchen**Kopiesicherung** deaktiviert ist, wenn **Differenziell** ausgewählt ist.  
  
6.  Klicken Sie unter **Sicherungskomponente**auf **Datenbank**.  
  
7.  Akzeptieren Sie entweder den im Textfeld **Name** vorgeschlagenen Standardnamen für den Sicherungssatz, oder geben Sie einen anderen Namen für den Sicherungssatz ein.  
  
8.  Geben Sie optional in das Textfeld **Beschreibung** eine Beschreibung des Sicherungssatzes ein.  
  
9. Geben Sie an, wann der Sicherungssatz ablaufen soll:  
  
    -   Wenn der Sicherungssatz nach einer bestimmten Anzahl von Tagen ablaufen soll, klicken Sie auf **Nach** (die Standardoption), und geben Sie an, nach wie vielen Tagen der Sicherungssatz abläuft. Dieser Wert kann zwischen 0 und 99999 Tagen liegen. Ein Wert von 0 Tagen bedeutet, dass der Sicherungssatz nicht abläuft.  
  
         Der Standardwert wird in der Option **Standardbeibehaltung für Sicherungsmedien (in Tagen)** des Dialogfelds **Servereigenschaften** (Seite**Datenbankeinstellungen** ) festgelegt. Klicken Sie hierzu mit der rechten Maustaste auf den Servernamen im Objekt-Explorer, und wählen Sie Eigenschaften aus. Wählen Sie anschließend die Seite **Datenbankeinstellungen** aus.  
  
    -   Zum Speichern des Sicherungssatzes an einem bestimmten Datum klicken Sie auf **Am**. Geben Sie das Datum ein, an dem der Sicherungssatz abläuft.  
  
10. Wählen Sie den Sicherungszieltyp aus, indem Sie auf **Datenträger** oder **Band**klicken. Um den Pfad für bis zu 64 Datenträger oder Bandlaufwerke auszuwählen, die insgesamt einen einzigen Mediensatz enthalten, klicken Sie auf **Hinzufügen**. Die ausgewählten Pfade werden im Listenfeld **Sichern auf** angezeigt.  
  
     Um einen Sicherungsziel zu entfernen, wählen Sie ihn aus, und klicken Sie auf **Entfernen**. Zum Anzeigen des Inhalts eines Sicherungsziels wählen Sie es aus, und klicken Sie auf **Inhalt**.  
  
11. Zum Anzeigen oder Auswählen der erweiterten Optionen klicken Sie auf **Optionen** im Bereich **Seite auswählen** .  
  
12. Wählen Sie eine Option von **Medium überschreiben** aus, indem Sie auf eine der folgenden Optionen klicken:  
  
    -   **Auf vorhandenen Mediensatz sichern**  
  
         Klicken Sie bei dieser Option entweder auf **An vorhandenen Sicherungssatz anfügen** oder auf **Alle vorhandenen Sicherungssätze überschreiben**. Sie können bei Bedarf das Kontrollkästchen **Mediensatznamen und Ablaufzeit des Sicherungssatzes überprüfen** aktivieren und optional einen Namen in das Textfeld **Mediensatzname** eingeben. Wenn kein Name angegeben wurde, wird ein Mediensatz mit leerem Namen erstellt. Wenn Sie einen Mediensatznamen angeben, wird das Medium (Band oder Datenträger) daraufhin geprüft, ob der tatsächliche Name mit dem hier eingegebenen Namen übereinstimmt.  
  
         Wenn Sie den Mediennamen leer lassen und das Kontrollkästchen aktivieren, um ihn anhand des Mediums zu überprüfen, ist die Prüfung erfolgreich, wenn der Medienname auf dem Medium ebenfalls leer ist.  
  
    -   **Auf neuen Mediensatz sichern und alle vorhandenen Sicherungssätze löschen**  
  
         Geben Sie bei dieser Option einen Namen in das Textfeld **Name für neuen Mediensatz** und optional eine Beschreibung des Mediensatzes in das Textfeld **Beschreibung für neuen Mediensatz** ein.  
  
13. Im Bereich **Zuverlässigkeit** können Sie folgende Optionen aktivieren:  
  
    -   **Sicherung nach dem Abschluss überprüfen**.  
  
    -   **Vor dem Schreiben auf die Medien Prüfsumme bilden**, und optional **Bei Prüfsummenfehler fortsetzen**. Weitere Informationen zu Prüfsummen finden Sie unter [Mögliche Medienfehler während der Sicherung und Wiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
14. Wenn Sie auf ein Bandlaufwerk sichern (gemäß der Konfiguration im Abschnitt **Ziel** der Seite **Allgemein**), ist die Option **Band nach dem Sichern entladen** aktiviert. Wenn Sie auf diese Option klicken, wird die Option **Band vor dem Entladen zurückspulen** aktiviert.  
  
    > [!NOTE]  
    >  Die Optionen im Abschnitt **Transaktionsprotokoll** sind inaktiv, es sei denn, Sie sichern ein Transaktionsprotokoll (wie im Abschnitt **Sicherungstyp** der Seite **Allgemein** angegeben).  
  
15. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] und höheren Versionen wird die [Sicherungskomprimierung](../../relational-databases/backup-restore/backup-compression-sql-server.md). Ob eine Sicherung standardmäßig komprimiert wird, ist vom Wert der Serverkonfigurationsoption **Komprimierungsstandard für Sicherung** abhängig. Sie können jedoch unabhängig von der aktuellen Standardeinstellung auf Serverebene eine Sicherung komprimieren, indem Sie die Option **Sicherung komprimieren**aktivieren, oder die Komprimierung verhindern, indem Sie die Option **Sicherung nicht komprimieren**aktivieren.  
  
     **So zeigen Sie die aktuelle Standardeinstellung für die Sicherungskomprimierung (Option "backup compression default") an**  
  
    -   [Anzeigen oder Konfigurieren der Serverkonfigurationsoption Standardeinstellung für die Sicherungskomprimierung](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
    > [!NOTE]  
    >  Alternativ können Sie den Wartungsplanungs-Assistenten zum Erstellen differenzieller Datenbanksicherungen verwenden.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL  
  
#### <a name="create-a-differential-database-backup"></a>Erstellen einer differenziellen Datenbanksicherung  
  
1.  Führen Sie die BACKUP DATABASE-Anweisung aus, um die differenzielle Datenbanksicherung zu erstellen, und geben Sie dabei Folgendes an:  
  
    -   Den Namen der zu sichernden Datenbank.  
  
    -   Das Sicherungsmedium, auf das die vollständige Datenbanksicherung geschrieben wird.  
  
    -   Die DIFFERENTIAL-Klausel, um anzugeben, dass nur die Abschnitte der Datenbank gesichert werden sollen, die sich nach dem Erstellen der letzten vollständigen Datenbanksicherung geändert haben.  
  
     Die erforderliche Syntax lautet folgendermaßen:  
  
     BACKUP DATABASE *database_name* TO <backup_device> WITH DIFFERENTIAL  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 In diesem Beispiel werden eine vollständige und eine differenzielle Datenbanksicherung für die `MyAdvWorks` -Datenbank erstellt  
  
```tsql  
-- Create a full database backup first.  
BACKUP DATABASE MyAdvWorks   
   TO MyAdvWorks_1   
   WITH INIT;  
GO  
-- Time elapses.  
-- Create a differential database backup, appending the backup  
-- to the backup device containing the full database backup.  
BACKUP DATABASE MyAdvWorks  
   TO MyAdvWorks_1  
   WITH DIFFERENTIAL;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Differenzielle Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)   
 [Sichern von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Wiederherstellen einer differenziellen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-differential-database-backup-sql-server.md)   
 [Wiederherstellen einer Transaktionsprotokollsicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Vollständige Dateisicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)  
  
  
