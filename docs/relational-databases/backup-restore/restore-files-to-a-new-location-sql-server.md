---
title: Wiederherstellen von Dateien an einem neuen Speicherort (SQL Server) | Microsoft-Dokumentation
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
- restoring files [SQL Server], how-to topics
- restoring databases [SQL Server], moving
- restoring files [SQL Server], steps
- file restores [SQL Server], how-to topics
- filegroups [SQL Server], restoring
- restoring filegroups [SQL Server]
ms.assetid: b4f4791d-646e-4632-9980-baae9cb1aade
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 212e32ce69ae1b5bef4502227bdc4aafca5e5be2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="restore-files-to-a-new-location-sql-server"></a>Wiederherstellen von Dateien an einem neuen Speicherort (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Sie Dateien in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]auf einem neuen Speicherort wiederherstellen können.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So stellen Sie Dateien an einem neuen Speicherort wieder her mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Nur der Systemadministrator, der die Dateien wiederherstellt, darf zurzeit mit der wiederherzustellenden Datenbank arbeiten.  
  
-   RESTORE ist nicht in einer expliziten oder implizierten Transaktion zulässig.  
  
-   Bevor Sie mit dem vollständigen oder dem massenprotokollierten Wiederherstellungsmodell Dateien wiederherstellen können, müssen Sie das Protokoll der aktiven Transaktion (das sog. Protokollfragment) sichern. Weitere Informationen finden Sie unter [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)wiederherstellen können.  
  
-   Um eine verschlüsselte Datenbank wiederherstellen zu können, muss das Zertifikat oder der asymmetrische Schlüssel verfügbar sein, das oder der zum Verschlüsseln der Datenbank verwendet wurde. Ohne das Zertifikat oder den asymmetrischen Schlüssel kann die Datenbank nicht wiederhergestellt werden. Darum muss das Zertifikat, das zur Verschlüsselung des Verschlüsselungsschlüssels für die Datenbank verwendet wurde, so lange beibehalten werden, wie die Sicherung benötigt wird. Weitere Informationen finden Sie unter [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Ist die wiederherzustellende Datenbank nicht vorhanden, muss der Benutzer über CREATE DATABASE-Berechtigungen verfügen, um RESTORE ausführen zu können. Ist die Datenbank vorhanden, werden RESTORE-Berechtigungen standardmäßig den Mitgliedern der festen Serverrollen **sysadmin** und **dbcreator** sowie dem Besitzer (**dbo**) der Datenbank erteilt (für die Option FROM DATABASE_SNAPSHOT ist die Datenbank immer vorhanden).  
  
 RESTORE-Berechtigungen werden Rollen erteilt, in denen Mitgliedsinformationen immer für den Server verfügbar sind. Da die Mitgliedschaft in einer festen Datenbankrolle nur bei unbeschädigten und zugänglichen Datenbanken geprüft werden kann (was beim Ausführen von RESTORE nicht immer der Fall ist), verfügen Mitglieder der festen Datenbankrolle **db_owner** nicht über RESTORE-Berechtigungen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-restore-files-to-a-new-location"></a>So stellen Sie Dateien an einem neuen Speicherort wieder her  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]her, erweitern Sie diese Instanz und dann **Datenbanken**.  
  
2.  Klicken Sie mit der rechten Maustaste auf die gewünschte Datenbank, zeigen Sie auf **Tasks**, zeigen Sie auf **Wiederherstellen**, und klicken Sie anschließend auf **Dateien und Dateigruppen**.  
  
3.  Geben Sie auf der **Allgemein** im Listenfeld **In Datenbank** die wiederherzustellenden Datenbank ein. Sie können eine neue Datenbank eingeben oder eine vorhandene Datenbank aus der Dropdownliste auswählen. Die Liste umfasst alle Datenbanken auf dem Server, mit Ausnahme der Datenbanken **master** und **tempdb**.  
  
4.  Zum Festlegen von Quelle und Speicherort der wiederherzustellenden Sicherungssätze klicken Sie auf eine der folgenden Optionen:  
  
    -   **Aus Datenbank**  
  
         Geben Sie im Listenfeld einen Datenbanknamen ein. Diese Liste enthält nur Datenbanken, die entsprechend dem Sicherungsverlauf von **msdb** gesichert wurden.  
  
    -   **Von Gerät**  
  
         Klicken Sie auf die Schaltfläche zum Durchsuchen. Wählen Sie im Dialogfeld für das **Angeben der Sicherungsgeräte** einen der im Listenfeld **Sicherungsmedientyp** aufgeführten Medientypen aus. Klicken Sie zum Auswählen von einem oder mehreren Medien für das Listenfeld **Sicherungsmedien** auf **Hinzufügen**.  
  
         Klicken Sie nach dem Hinzufügen der gewünschten Medien zum Listenfeld **Sicherungsmedien** auf **OK** , um zur Seite **Allgemein** zurückzukehren.  
  
5.  Wählen Sie im Raster **Wählen Sie die wiederherzustellenden Sicherungssätze aus** die wiederherzustellenden Sicherungen aus. Mit diesem Raster werden die Sicherungen angezeigt, die für den angegebenen Speicherort verfügbar sind. Standardmäßig wird ein Wiederherstellungsplan vorgeschlagen. Sie können die Auswahl im Raster ändern, um den vorgeschlagenen Wiederherstellungsplan zu überschreiben. Für Sicherungen, die von einer Sicherung abhängig sind, für die die Auswahl aufgehoben wurde, wird die Auswahl automatisch aufgehoben.  
  
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
  
6.  Klicken Sie im Bereich **Seite auswählen** auf die Seite **Optionen** .  
  
7.  Geben Sie im Raster **Datenbankdateien wiederherstellen als** einen neuen Speicherort für die Datei oder die Dateien an, die Sie verschieben möchten.  
  
    |Spaltenkopf|Werte|  
    |-----------------|------------|  
    |**Originaldateiname**|Der vollständige Pfad einer Quellsicherungsdatei.|  
    |**Dateityp**|Gibt den Typ der Daten in der Sicherung an: **Daten**, **Protokoll**oder **Filestream-Daten**. Daten, die in Tabellen enthalten sind, befinden sich in **Daten** -Dateien. Transaktionsprotokolldaten befinden sich in **Protokoll** -Dateien. Blobdaten (Binary Large Object), die im Dateisystem gespeichert werden, befinden sich in **Filestreamdaten** -Dateien.|  
    |**Wiederherstellen als**|Der vollständige Pfad der wiederherzustellenden Datenbankdatei. Um eine neue Wiederherstellungsdatei anzugeben, klicken Sie auf das Textfeld, und bearbeiten Sie den vorgeschlagenen Pfad und Dateinamen. Das Ändern des Pfads oder des Dateinamens in der Spalte **Wiederherstellen als** entspricht der Option MOVE in einer [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE-Anweisung.|  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-restore-files-to-a-new-location"></a>So stellen Sie Dateien an einem neuen Speicherort wieder her  
  
1.  Führen Sie optional die RESTORE FILELISTONLY-Anweisung aus, um Anzahl und Namen der Dateien in der vollständigen Datenbanksicherung zu bestimmen.  
  
2.  Führen Sie die RESTORE DATABASE-Anweisung aus, um die vollständige Datenbanksicherung wiederherzustellen, und geben Sie dabei Folgendes an:  
  
    -   Den Namen der wiederherzustellenden Datenbank.  
  
    -   Das Sicherungsmedium, von dem die vollständige Datenbanksicherung wiederhergestellt wird.  
  
    -   Die MOVE-Klausel für jede Datei, die an einem neuen Speicherort wiederhergestellt werden soll.  
  
    -   Die NORECOVERY-Klausel.  
  
3.  Wenn die Dateien nach dem Erstellen der Sicherung geändert wurden, führen Sie die RESTORE LOG-Anweisung aus, um die Transaktionsprotokollsicherung anzuwenden, und geben Sie Folgendes an:  
  
    -   Den Namen der Datenbank, auf die das zu sichernde Transaktionsprotokoll angewendet wird.  
  
    -   Das Sicherungsmedium, von dem die Transaktionsprotokollsicherung wiederhergestellt wird.  
  
    -   Die NORECOVERY-Klausel, wenn nach der aktuellen Transaktionsprotokollsicherung eine weitere angewendet werden soll. Geben Sie andernfalls die RECOVERY-Klausel an.  
  
         Die gegebenenfalls angewendeten Transaktionsprotokollsicherungen müssen den Zeitpunkt einschließen, zu dem die Dateien und Dateigruppen gesichert wurden.  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 In diesem Beispiel werden zwei der Dateien für die `MyNwind` -Datenbank, die sich ursprünglich auf Laufwerk C befanden, an neuen Speicherorten auf Laufwerk D wiederhergestellt. Zwei Transaktionsprotokolle werden ebenfalls angewendet, um die Datenbank bis zum aktuellen Zeitpunkt wiederherzustellen. Die `RESTORE FILELISTONLY` -Anweisung wird verwendet, um die Anzahl der logischen und physischen Namen der Dateien der Datenbank zu bestimmen, die wiederhergestellt werden.  
  
```tsql  
USE master;  
GO  
-- First determine the number and names of the files in the backup.  
RESTORE FILELISTONLY  
   FROM MyNwind_1;  
-- Restore the files for MyNwind.  
RESTORE DATABASE MyNwind  
   FROM MyNwind_1  
   WITH NORECOVERY,  
   MOVE 'MyNwind_data_1' TO 'D:\MyData\MyNwind_data_1.mdf',   
   MOVE 'MyNwind_data_2' TO 'D:\MyData\MyNwind_data_2.ndf';  
GO  
-- Apply the first transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log1  
   WITH NORECOVERY;  
GO  
-- Apply the last transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log2  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Kopieren von Datenbanken durch Sichern und Wiederherstellen](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [Wiederherstellen von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
  
