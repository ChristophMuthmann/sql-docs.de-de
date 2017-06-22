---
title: Wiederherstellen von Dateien und Dateigruppen (SQL Server) | Microsoft-Dokumentation
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
- sql13.swb.restorefilesandfilegrps.general.f1
- sql13.swb.bselectfilegrpsfiles.f1
- sql13.swb.restorefilesandfilegrps.options.f1
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], restoring files and filegroups
- restoring [SQL Server], files
ms.assetid: 72603b21-3065-4b56-8b01-11b707911b05
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f0bc8f28aa966b39b9b5c78d681458d6bf25f84f
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="restore-files-and-filegroups-sql-server"></a>Wiederherstellen von Dateien und Dateigruppen (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Sie Daten und Dateigruppen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]wiederherstellen können.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
-   [Sicherheit](#Security)  
  
-   **So stellen Sie Dateien und Dateigruppen wieder her mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Nur der mit der Wiederherstellung der Dateien und Dateigruppen betraute Systemadministrator darf zurzeit mit der wiederherzustellenden Datenbank arbeiten.  
  
-   RESTORE ist nicht in einer expliziten oder implizierten Transaktion zulässig.  
  
-   Die Datei muss im Rahmen des Modells der einfachen Wiederherstellung zu einer schreibgeschützten Dateigruppe gehören.  
  
-   Bevor Sie mit dem vollständigen oder dem massenprotokollierten Wiederherstellungsmodell Dateien wiederherstellen können, müssen Sie das Protokoll der aktiven Transaktion (das sog. Protokollfragment) sichern. Weitere Informationen finden Sie unter [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)wiederherstellen können.  
  
-   Um eine verschlüsselte Datenbank wiederherstellen zu können, muss das Zertifikat oder der asymmetrische Schlüssel verfügbar sein, das oder der zum Verschlüsseln der Datenbank verwendet wurde. Ohne das Zertifikat oder den asymmetrischen Schlüssel kann die Datenbank nicht wiederhergestellt werden. Darum muss das Zertifikat, das zur Verschlüsselung des Verschlüsselungsschlüssels für die Datenbank verwendet wurde, so lange beibehalten werden, wie die Sicherung benötigt wird. Weitere Informationen finden Sie unter [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Ist die wiederherzustellende Datenbank nicht vorhanden, muss der Benutzer über CREATE DATABASE-Berechtigungen verfügen, um RESTORE ausführen zu können. Ist die Datenbank vorhanden, werden RESTORE-Berechtigungen standardmäßig den Mitgliedern der festen Serverrollen **sysadmin** und **dbcreator** sowie dem Besitzer (**dbo**) der Datenbank erteilt (für die Option FROM DATABASE_SNAPSHOT ist die Datenbank immer vorhanden).  
  
 RESTORE-Berechtigungen werden Rollen erteilt, in denen Mitgliedsinformationen immer für den Server verfügbar sind. Da die Mitgliedschaft in einer festen Datenbankrolle nur geprüft werden kann, wenn die Datenbank unbeschädigt ist und auf sie zugegriffen werden kann, was beim Ausführen von RESTORE nicht immer der Fall ist, verfügen Mitglieder der festen Datenbankrolle **db_owner** nicht über RESTORE-Berechtigungen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-restore-files-and-filegroups"></a>So stellen Sie Dateien und Dateigruppen wieder her  
  
1.  Stellen Sie eine Verbindung mit der entsprechenden Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]her, und klicken Sie danach im Objekt-Explorer auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Datenbanken**. Wählen Sie je nach Datenbank entweder eine Benutzerdatenbank aus, oder erweitern Sie **Systemdatenbanken**, und wählen Sie eine Systemdatenbank aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, zeigen Sie auf **Tasks**, und klicken Sie dann auf **Wiederherstellen**.  
  
4.  Klicken Sie auf **Dateien und Dateigruppen**. Daraufhin wird das Dialogfeld **Dateien und Dateigruppen wiederherstellen** geöffnet.  
  
5.  Geben Sie auf der **Allgemein** im Listenfeld **In Datenbank** die wiederherzustellenden Datenbank ein. Sie können eine neue Datenbank eingeben oder eine vorhandene Datenbank aus der Dropdownliste auswählen. Die Liste umfasst alle Datenbanken auf dem Server, mit Ausnahme der Datenbanken **master** und **tempdb**.  
  
6.  Zum Festlegen von Quelle und Speicherort der wiederherzustellenden Sicherungssätze klicken Sie auf eine der folgenden Optionen:  
  
    -   **Aus Datenbank**  
  
         Geben Sie im Listenfeld einen Datenbanknamen ein. Diese Liste enthält nur Datenbanken, die entsprechend dem Sicherungsverlauf von **msdb** gesichert wurden.  
  
    -   **Von Gerät**  
  
         Klicken Sie auf die Schaltfläche zum Durchsuchen. Wählen Sie im Dialogfeld für das Angeben der Sicherungsgeräte **** einen der im Listenfeld **Sicherungsmedientyp** aufgeführten Medientypen aus. Klicken Sie zum Auswählen von einem oder mehreren Medien für das Listenfeld **Sicherungsmedien** auf **Hinzufügen**.  
  
         Klicken Sie nach dem Hinzufügen der gewünschten Medien zum Listenfeld **Sicherungsmedien** auf **OK** , um zur Seite **Allgemein** zurückzukehren.  
  
7.  Wählen Sie im Raster **Wählen Sie die wiederherzustellenden Sicherungssätze aus** die wiederherzustellenden Sicherungen aus. Mit diesem Raster werden die Sicherungen angezeigt, die für den angegebenen Speicherort verfügbar sind. Standardmäßig wird ein Wiederherstellungsplan vorgeschlagen. Sie können die Auswahl im Raster ändern, um den vorgeschlagenen Wiederherstellungsplan zu überschreiben. Für Sicherungen, die von einer Sicherung abhängig sind, für die die Auswahl aufgehoben wurde, wird die Auswahl automatisch aufgehoben.  
  
    |Spaltenkopf|Werte|  
    |-----------------|------------|  
    |**Wiederherstellen**|Die aktivierten Kontrollkästchen zeigen die wiederherzustellenden Sicherungssätze an.|  
    |**Name**|Name des Sicherungssatzes.|  
    |**Dateityp**|Gibt den Typ der Daten in der Sicherung an: **Daten**, **Protokoll**oder **Filestream-Daten**. Daten, die in Tabellen enthalten sind, befinden sich in **Daten** -Dateien. Transaktionsprotokolldaten befinden sich in **Protokoll** -Dateien. Blobdaten (Binary Large Object), die im Dateisystem gespeichert werden, befinden sich in **Filestreamdaten** -Dateien.|  
    |**Typ**|Der Typ der ausgeführten Sicherung: **Vollständig**, **Differenziell**oder **Transaktionsprotokoll**.|  
    |**Server**|Name der Instanz des Datenbankmoduls, durch die der Sicherungsvorgang ausgeführt wurde.|  
    |**Logischer Name der Datei**|Der logische Name der Datei.|  
    |**Datenbank**|Name der an der Sicherungsoperation beteiligten Datenbank.|  
    |**Startdatum**|Datum und Uhrzeit des Sicherungsbeginns, entsprechend den Ländereinstellungen des Clients.|  
    |**Beendigungsdatum**|Datum und Uhrzeit des Endes des Sicherungsvorgangs, entsprechend den Ländereinstellungen des Clients.|  
    |**Größe**|Größe des Sicherungssatzes in Byte.|  
    |**Benutzername**|Name des Benutzers, der den Sicherungsvorgang ausgeführt hat.|  
  
8.  Klicken Sie auf der Seite **Seite auswählen** auf **Optionen**, um die erweiterten Optionen anzuzeigen und auszuwählen.  
  
9. Im Bereich **Wiederherstellungsoptionen** können Sie Ihren Anforderungen entsprechend aus den folgenden Optionen auswählen.  
  
     **Als Dateigruppe wiederherstellen**  
     Zeigt an, dass eine komplette Dateigruppe wiederhergestellt wird.  
  
     **Vorhandene Datenbank überschreiben**  
     Legt fest, dass beim Wiederherstellungsvorgang alle vorhandenen Datenbanken und die dazugehörigen Dateien überschrieben werden, selbst wenn bereits eine Datenbank oder Datei mit demselben Namen vorhanden ist.  
  
     Das Auswählen dieser Option entspricht der Verwendung der Option REPLACE in einer [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE-Anweisung.  
  
     **Bestätigung vor Wiederherstellen jeder einzelnen Sicherung**  
     Fordert bei jedem Sicherungssatz eine Bestätigung vom Benutzer, bevor mit der Wiederherstellung begonnen wird.  
  
     Diese Option ist insbesondere dann hilfreich, wenn Sie Bänder für verschiedene Mediensätze wechseln müssen, beispielsweise wenn der Server nur ein Bandgerät besitzt.  
  
     **Zugriff auf die wiederhergestellte Datenbank einschränken**  
     Gestattet nur Mitgliedern von **db_owner**, **dbcreator**oder **sysadmin**, auf die wiederhergestellte Datenbank zuzugreifen.  
  
     Das Auswählen dieser Option entspricht der Verwendung der Option RESTRICTED_USER in einer [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE-Anweisung.  
  
10. Optional: Sie können die Datenbank an einem neuen Speicherort wiederherstellen, indem Sie im Raster **Datenbankdateien wiederherstellen als** für jede Datei ein neues Wiederherstellungsziel angeben.  
  
    |Spaltenkopf|Werte|  
    |-----------------|------------|  
    |**Originaldateiname**|Der vollständige Pfad einer Quellsicherungsdatei.|  
    |**Dateityp**|Gibt den Typ der Daten in der Sicherung an: **Daten**, **Protokoll**oder **Filestream-Daten**. Daten, die in Tabellen enthalten sind, befinden sich in **Daten** -Dateien. Transaktionsprotokolldaten befinden sich in **Protokoll** -Dateien. Blobdaten (Binary Large Object), die im Dateisystem gespeichert werden, befinden sich in **Filestreamdaten** -Dateien.|  
    |**Wiederherstellen als**|Der vollständige Pfad der wiederherzustellenden Datenbankdatei. Um eine neue Wiederherstellungsdatei anzugeben, klicken Sie auf das Textfeld, und bearbeiten Sie den vorgeschlagenen Pfad und Dateinamen. Das Ändern des Pfads oder des Dateinamens in der Spalte **Wiederherstellen als** entspricht der Option MOVE in einer [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE-Anweisung.|  
  
11. Die Optionen im Bereich **Wiederherstellungsstatus** bestimmen den Status der Datenbank nach dem Wiederherstellungsvorgang.  
  
     **Datenbank betriebsbereit belassen, indem für Transaktionen ohne Commit ein Rollback ausgeführt wird. Zusätzliche Transaktionsprotokolle können nicht wiederhergestellt werden. (RESTORE WITH RECOVERY)**  
     Stellt die Datenbank wieder her. Dies ist das Standardverhalten. Wählen Sie diese Option nur aus, wenn Sie alle benötigten Sicherungen jetzt wiederherstellen möchten. Diese Option entspricht der Angabe von WITH RECOVERY in einer [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE-Anweisung.  
  
     **Datenbank nicht betriebsbereit belassen und kein Rollback für Transaktionen ohne Commit ausführen. Zusätzliche Transaktionsprotokolle können wiederhergestellt werden. (RESTORE WITH NORECOVERY)**  
     Belässt die Datenbank im Wiederherstellungsstatus. Um die Datenbank wiederherzustellen, müssen Sie eine weitere Wiederherstellung mithilfe der vorangegangenen Option RESTORE WITH RECOVERY ausführen (siehe oben). Diese Option entspricht der Angabe von WITH NORECOVERY in einer [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE-Anweisung.  
  
     Wenn Sie diese Option auswählen, ist die Option **Replikationseinstellungen beibehalten** nicht verfügbar.  
  
     **Datenbank im schreibgeschützten Modus belassen. Transaktionen ohne Commit werden rückgängig gemacht, die Rückgängigaktionen werden jedoch in einer Standbydatei gespeichert, sodass die Auswirkungen der Wiederherstellung umgekehrt werden können. (RESTORE WITH STANDBY)**  
     Belässt die Datenbank in einem Standbystatus. Diese Option entspricht der Angabe von WITH STANDBY in einer [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE-Anweisung.  
  
     Bei Auswahl dieser Option müssen Sie eine Standbydatei angeben.  
  
     **Rollback-Rückgängigdatei**  
     Geben Sie im Textfeld **Rollback-Rückgängigdatei** einen Namen für die Standbydatei an. Diese Option ist erforderlich, wenn Sie die Datenbank im schreibgeschützten Modus belassen (RESTORE WITH STANDBY).  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-restore-files-and-filegroups"></a>So stellen Sie Dateien und Dateigruppen wieder her  
  
1.  Führen Sie die RESTORE DATABASE-Anweisung aus, um die Datei- und Dateigruppensicherung wiederherzustellen, und geben Sie dabei Folgendes an:  
  
    -   Den Namen der wiederherzustellenden Datenbank.  
  
    -   Das Sicherungsmedium, von dem die vollständige Datenbanksicherung wiederhergestellt wird.  
  
    -   Die FILE-Klausel für jede wiederherzustellende Datei.  
  
    -   Die FILEGROUP-Klausel für jede wiederherzustellende Dateigruppe.  
  
    -   Die NORECOVERY-Klausel. Wenn die Dateien nach dem Erstellen der Sicherung nicht geändert wurden, geben Sie die RECOVERY-Klausel an.  
  
2.  Wenn die Dateien nach dem Erstellen der Sicherung geändert wurden, führen Sie die RESTORE LOG-Anweisung aus, um die Transaktionsprotokollsicherung anzuwenden, und geben Sie Folgendes an:  
  
    -   Den Namen der Datenbank, auf die das zu sichernde Transaktionsprotokoll angewendet wird.  
  
    -   Das Sicherungsmedium, von dem die Transaktionsprotokollsicherung wiederhergestellt wird.  
  
    -   Die NORECOVERY-Klausel, wenn nach der aktuellen Transaktionsprotokollsicherung eine weitere angewendet werden soll. Geben Sie andernfalls die RECOVERY-Klausel an.  
  
         Die gegebenenfalls angewendeten Transaktionsprotokollsicherungen müssen den Zeitpunkt, zu dem die Dateien und Dateigruppen gesichert wurden, bis hin zum Protokollende abdecken (es sei denn, ALLE Datenbankdateien werden wiederhergestellt).  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 In diesem Beispiel werden die Dateien und Dateigruppen der `MyDatabase` -Datenbank wiederhergestellt. Zur Wiederherstellung der Datenbank zur aktuellen Zeit werden zwei Transaktionsprotokolle übernommen.  
  
```tsql  
USE master;  
GO  
-- Restore the files and filesgroups for MyDatabase.  
RESTORE DATABASE MyDatabase  
   FILE = 'MyDatabase_data_1',  
   FILEGROUP = 'new_customers',  
   FILE = 'MyDatabase_data_2',  
   FILEGROUP = 'first_qtr_sales'  
   FROM MyDatabase_1  
   WITH NORECOVERY;  
GO  
-- Apply the first transaction log backup.  
RESTORE LOG MyDatabase  
   FROM MyDatabase_log1  
   WITH NORECOVERY;  
GO  
-- Apply the last transaction log backup.  
RESTORE LOG MyDatabase  
   FROM MyDatabase_log2  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [Sichern von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)   
 [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Wiederherstellen einer Transaktionsprotokollsicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
