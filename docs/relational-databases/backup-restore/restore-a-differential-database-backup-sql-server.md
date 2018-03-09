---
title: Wiederherstellen einer differenziellen Datenbanksicherung (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full differential backups [SQL Server]
- restoring databases [SQL Server], full differential backups
- database backups [SQL Server], full differential backups
- database restores [SQL Server], full differential backups
- backing up databases [SQL Server], full differential backups
ms.assetid: 0dd971a4-ee38-4dd3-9f30-ef77fc58dd11
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d5a965b04e6c09bfe067b3894cac0591fefd0247
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="restore-a-differential-database-backup-sql-server"></a>Wiederherstellen einer differenziellen Datenbanksicherung (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Sie in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] eine differenzielle Datenbanksicherung mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]wiederherstellen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Security](#Security)  
  
-   **So stellen Sie eine differenzielle Datenbanksicherung wieder her, und zwar mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   RESTORE ist nicht in einer expliziten oder implizierten Transaktion zulässig.  
  
-   Sicherungen, die mit aktuelleren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt werden, können in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nicht wiederhergestellt werden.  
  
-   In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]können Sie eine Benutzerdatenbank von einer Datenbanksicherung wiederherstellen, die mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder einer höheren Version erstellt wurde.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Im vollständigen oder im massenprotokollierten Wiederherstellungsmodell muss das Protokoll der aktiven Transaktion (wird als Protokollfragment bezeichnet) gesichert werden, bevor eine Datenbank wiederhergestellt werden kann. Weitere Informationen finden Sie unter [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)bezeichnet) gesichert werden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Ist die wiederherzustellende Datenbank nicht vorhanden, muss der Benutzer über CREATE DATABASE-Berechtigungen verfügen, um RESTORE ausführen zu können. Ist die Datenbank vorhanden, werden RESTORE-Berechtigungen standardmäßig den Mitgliedern der festen Serverrollen **sysadmin** und **dbcreator** sowie dem Besitzer (**dbo**) der Datenbank erteilt (für die Option FROM DATABASE_SNAPSHOT ist die Datenbank immer vorhanden).  
  
 RESTORE-Berechtigungen werden Rollen erteilt, in denen Mitgliedsinformationen immer für den Server verfügbar sind. Da die Mitgliedschaft in einer festen Datenbankrolle nur bei unbeschädigten und zugänglichen Datenbanken geprüft werden kann (was beim Ausführen von RESTORE nicht immer der Fall ist), verfügen Mitglieder der festen Datenbankrolle **db_owner** nicht über RESTORE-Berechtigungen.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-restore-a-differential-database-backup"></a>So stellen Sie eine differenzielle Datenbanksicherung wieder her  
  
1.  Stellen Sie eine Verbindung mit der entsprechenden Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]her, und klicken Sie danach im Objekt-Explorer auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Datenbanken**. Wählen Sie je nach Datenbank entweder eine Benutzerdatenbank aus, oder erweitern Sie **Systemdatenbanken**, und wählen Sie eine Systemdatenbank aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, zeigen Sie auf **Tasks**und **Wiederherstellung**, und klicken Sie anschließend auf **Datenbank**.  
  
4.  Legen Sie Quelle und Speicherort der wiederherzustellenden Sicherungssätze auf der Seite **Allgemein** mithilfe des Abschnitts **Quelle** fest. Wählen Sie eine der folgenden Optionen aus:  
  
    -   **Datenbank**  
  
         Wählen Sie die wiederherzustellende Datenbank aus der Dropdownliste aus. Die Liste enthält nur Datenbanken, die entsprechend dem Sicherungsverlauf von **msdb** gesichert wurden.  
  
    > [!NOTE]  
    >  Wenn die Sicherung von einem anderen Server abgerufen wird, verfügt der Zielserver über keine Sicherungsverlaufsinformationen für die angegebene Datenbank. Wählen Sie in diesem Fall **Sicherungsmedium** aus, um die wiederherzustellende Datei oder das Medium manuell anzugeben.  
  
    -   **Sicherungsmedium**  
  
         Klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), um das Dialogfeld **Sicherungsmedien auswählen** zu öffnen. Wählen Sie im Feld **Sicherungsmedientyp** einen der aufgeführten Medientypen aus. Wenn Sie ein oder mehrere Medien für das Feld **Sicherungsmedien** auswählen möchten, klicken Sie auf **Hinzufügen**.  
  
         Klicken Sie nach dem Hinzufügen der gewünschten Medien zum Listenfeld **Sicherungsmedien** auf **OK** , um zur Seite **Allgemein** zurückzukehren.  
  
         Wählen Sie im Listenfeld **Quelle: Sicherungsmedium: Datenbank** den Namen der Datenbank aus, die wiederhergestellt werden soll.  
  
         **Hinweis** Diese Liste ist nur verfügbar, wenn **Sicherungsmedium** ausgewählt wird. Nur Datenbanken mit Sicherungen auf dem ausgewählten Medium stehen zur Verfügung.  
  
5.  Im Abschnitt **Ziel** wird das Feld **Datenbank** automatisch mit dem Namen der Datenbank aufgefüllt, die wiederhergestellt werden soll. Geben Sie zum Ändern des Datenbanknamens den neuen Namen ins Feld **Datenbank** ein.  
  
    > [!NOTE]  
    >  Klicken Sie zum Anhalten der Wiederherstellung zu einem bestimmten Zeitpunkt auf **Zeitachse** , um auf das Dialogfeld **Sicherungszeitachse** zuzugreifen. Hilfe zum Beenden einer Wiederherstellung der Datenbank zu einem bestimmten Zeitpunkt finden Sie unter [Wiederherstellen einer SQL Server-Datenbank zu einem Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
6.  Wählen Sie im Raster **Wiederherzustellende Sicherungssätze** die Sicherungen durch die differenzielle Sicherung aus, die Sie wiederherstellen möchten.  
  
     Weitere Informationen zu den Spalten des Rasters **Wiederherzustellende Sicherungssätze** finden Sie unter [Datenbank wiederherstellen &#40;Seite „Allgemein“&#41;](../../relational-databases/backup-restore/restore-database-general-page.md).  
  
7.  Auf der Seite **Optionen** im Bereich **Wiederherstellungsoptionen** können Sie entsprechend Ihren Anforderungen die folgenden Optionen auswählen:  
  
    -   **Vorhandene Datenbank überschreiben (WITH REPLACE)**  
  
    -   **Replikationseinstellungen beibehalten (WITH KEEP_REPLICATION)**  
  
    -   **Bestätigung vor Wiederherstellen jeder einzelnen Sicherung**  
  
    -   **Zugriff auf die wiederhergestellte Datenbank einschränken (WITH RESTRICTED_USER)**  
  
     Weitere Informationen zu diesen Optionen finden Sie unter [Datenbank wiederherstellen &#40;Seite „Optionen“&#41;](../../relational-databases/backup-restore/restore-database-options-page.md).  
  
8.  Aktivieren Sie eine Option für das Feld **Wiederherstellungsstatus** . In diesem Feld wird der Status der Datenbank nach dem Wiederherstellungsvorgang bestimmt.  
  
    -   **RESTORE WITH RECOVERY** ist das Standardverhalten, das die Datenbank betriebsbereit belässt, indem für Transaktionen ohne Commit ein Rollback ausgeführt wird. Zusätzliche Transaktionsprotokolle können nicht wiederhergestellt werden. Wählen Sie diese Option nur aus, wenn Sie alle benötigten Sicherungen jetzt wiederherstellen möchten.  
  
    -   **RESTORE WITH NORECOVERY** belässt die Datenbank nicht betriebsbereit und führt kein Rollback für Transaktionen ohne Commit aus. Zusätzliche Transaktionsprotokolle können wiederhergestellt werden. Die Datenbank kann erst verwendet werden, wenn sie wiederhergestellt wurde.  
  
    -   **RESTORE WITH STANDBY** belässt die Datenbank im schreibgeschützten Modus. Diese Option macht Transaktionen rückgängig, für die noch kein Commit ausgeführt wurde, speichert die Umkehraktionen aber in einer Standbydatei, damit die Auswirkungen der Wiederherstellung rückgängig gemacht werden können.  
  
     Beschreibungen der Optionen für den Bereich finden Sie unter [Datenbank wiederherstellen &#40;Seite Optionen&#41;](../../relational-databases/backup-restore/restore-database-options-page.md).  
  
9. Wiederherstellungsvorgänge schlagen fehl, wenn aktive Verbindungen zur Datenbank bestehen. Aktivieren Sie die Option **Bestehende Verbindungen schließen** , um sicherzustellen, dass alle aktiven Verbindungen zwischen [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] und der Datenbank geschlossen werden.  
  
10. Wählen Sie **Bestätigung vor Wiederherstellen jeder einzelnen Sicherung** aus, wenn Sie zwischen jedem Wiederherstellungsvorgang zur Bestätigung aufgefordert werden möchten. Dies ist in der Regel nur bei großen Datenbanken und bei der gewünschten Überwachung des Status des Wiederherstellungsvorgangs erforderlich.  
  
11. Optional können Sie die Seite **Dateien** verwenden, um die Datenbank an einem neuen Speicherort wiederherzustellen. Hilfe zum Verschieben einer Datenbank finden Sie unter [Wiederherstellen einer Datenbank an einem neuen Speicherort &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md).  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-restore-a-differential-database-backup"></a>So stellen Sie eine differenzielle Datenbanksicherung wieder her  
  
1.  Führen Sie die RESTORE DATABASE-Anweisung mit der NORECOVERY-Klausel aus, um die vollständige Datenbanksicherung wiederherzustellen, die der differenziellen Datenbanksicherung vorausging. Weitere Informationen finden Sie unter [Vorgehensweise: Wiederherstellen einer vollständigen Sicherung](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
2.  Führen Sie die RESTORE DATABASE-Anweisung aus, um die differenzielle Datenbanksicherung wiederherzustellen, und geben Sie dabei Folgendes an:  
  
    -   Den Namen der Datenbank, auf die die differenzielle Datenbanksicherung angewendet werden soll.  
  
    -   Das Sicherungsmedium, von dem die differenzielle Datenbanksicherung wiederhergestellt wird.  
  
    -   Die NORECOVERY-Klausel, wenn Transaktionsprotokollsicherungen vorliegen, die nach Wiederherstellung der differenziellen Datenbanksicherung angewendet werden müssen. Andernfalls geben Sie die RECOVERY-Klausel an.  
  
3.  Beim vollständigen oder massenprotokollierten Wiederherstellungsmodell wird die Datenbank bei einer differenziellen Datenbankwiederherstellung in dem Status wiederhergestellt, in dem sie sich zum Zeitpunkt der Fertigstellung der differenziellen Datenbanksicherung befand. Um die Datenbank im Status zum Zeitpunkt des Fehlers wiederherzustellen, müssen Sie alle Transaktionsprotokollsicherungen anwenden, die nach der letzten differenziellen Datenbanksicherung erstellt wurden. Weitere Informationen finden Sie unter [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
  
#### <a name="a-restoring-a-differential-database-backup"></a>A. Wiederherstellen einer differenziellen Datenbanksicherung  
 In diesem Beispiel werden eine Datenbanksicherung und eine differenzielle Datenbanksicherung der `MyAdvWorks` -Datenbank wiederhergestellt.  
  
```sql  
-- Assume the database is lost, and restore full database,   
-- specifying the original full database backup and NORECOVERY,   
-- which allows subsequent restore operations to proceed.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH NORECOVERY;  
GO  
-- Now restore the differential database backup, the second backup on   
-- the MyAdvWorks_1 backup device.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH FILE = 2,  
   RECOVERY;  
GO  
```  
  
#### <a name="b-restoring-a-database-differential-database-and-transaction-log-backup"></a>B. Wiederherstellen einer Datenbank-, einer differenziellen Datenbank- und einer Transaktionsprotokollsicherung  
 In diesem Beispiel werden eine Datenbanksicherung, eine differenzielle Datenbanksicherung und eine Transaktionsprotokollsicherung der `MyAdvWorks` -Datenbank wiederhergestellt.  
  
```sql  
-- Assume the database is lost at this point. Now restore the full   
-- database. Specify the original full database backup and NORECOVERY.  
-- NORECOVERY allows subsequent restore operations to proceed.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH NORECOVERY;  
GO  
-- Now restore the differential database backup, the second backup on   
-- the MyAdvWorks_1 backup device.  
RESTORE DATABASE MyAdvWorks  
   FROM MyAdvWorks_1  
   WITH FILE = 2,  
   NORECOVERY;  
GO  
-- Now restore each transaction log backup created after  
-- the differential database backup.  
RESTORE LOG MyAdvWorks  
   FROM MyAdvWorks_log1  
   WITH NORECOVERY;  
GO  
RESTORE LOG MyAdvWorks  
   FROM MyAdvWorks_log2  
   WITH RECOVERY;  
GO  
```  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Erstellen einer differenziellen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [Wiederherstellen einer Transaktionsprotokollsicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Differenzielle Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
