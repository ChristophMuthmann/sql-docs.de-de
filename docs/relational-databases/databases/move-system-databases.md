---
title: Verschieben von Systemdatenbanken | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- moving system databases
- disaster recovery [SQL Server], moving database files
- database files [SQL Server], moving
- data files [SQL Server], moving
- tempdb database [SQL Server], moving
- system databases [SQL Server], moving
- scheduled disk maintenace [SQL Server]
- moving databases
- msdb database [SQL Server], moving
- moving database files
- relocating database files
- planned database relocations [SQL Server]
- master database [SQL Server], moving
- model database [SQL Server], moving
- Resource database [SQL Server]
- databases [SQL Server], moving
ms.assetid: 72bb62ee-9602-4f71-be51-c466c1670878
caps.latest.revision: 62
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: a9b177196b7b97b07aafc79095328e1b4f4c9067
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="move-system-databases"></a>Verschieben von Systemdatenbanken
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Systemdatenbanken in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verschoben werden. Das Verschieben von Systemdatenbanken kann in den folgenden Situationen nützlich sein:  
  
-   Bei der Wiederherstellung nach Fehlern. Wenn z. B. die Datenbank aufgrund eines Hardwarefehlers als fehlerverdächtig eingestuft oder heruntergefahren wurde.  
  
-   Bei geplanter Verschiebung.  
  
-   Verschiebung aufgrund planmäßiger Datenträgerwartung.  
  
 Die folgenden Verfahren gelten für das Verschieben von Datenbankdateien innerhalb derselben Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Zum Verschieben einer Datenbank in eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder auf einen anderen Server können Sie den Vorgang [Sichern und Wiederherstellen](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) verwenden.  

 Für die Prozeduren in diesem Thema ist der logische Name der Datenbankdateien erforderlich. Zum Abrufen des Namens führen Sie eine Abfrage für die Namensspalte in der [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) -Katalogsicht aus.  
  
> [!IMPORTANT]  
>  Wenn Sie eine Systemdatenbank verschieben und anschließend die master-Datenbank neu erstellen, müssen Sie die Systemdatenbank erneut verschieben, da bei der Neuerstellung alle Systemdatenbanken an ihrem standardmäßigen Speicherort installiert werden.  

> [!IMPORTANT]  
>  Nach dem Verschieben der Dateien muss das [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Dienstkonto über Zugriffsberechtigungen für die Dateien an ihren neuen Speicherorten verfügen.
    
  
##  <a name="Planned"></a> Prozedur zur geplanten Verschiebung und planmäßigen Datenträgerwartung  
 Zum Verschieben von Systemdatenbankdaten- oder Protokolldateien im Rahmen einer geplanten Verschiebung oder planmäßiger Wartungsarbeiten führen Sie die folgenden Schritte aus: Diese Prozedur gilt für alle Systemdatenbanken mit Ausnahme der master- und Resource-Datenbanken.  
  
1.  Führen Sie für jede zu verschiebende Datei die folgende Anweisung aus.  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name , FILENAME = 'new_path\os_file_name' )  
    ```  
  
2.  Beenden Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , oder fahren Sie das System für die Wartungsarbeiten herunter. Weitere Informationen finden Sie unter [Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
3.  Verschieben Sie die Datei(en) an den neuen Speicherort.  

4.  Starten Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder den Server neu. Weitere Informationen finden Sie unter [Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
5.  Überprüfen Sie die Dateiänderung durch Ausführen der folgenden Abfrage.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
 Wenn die msdb-Datenbank verschoben wurde und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz für [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)konfiguriert ist, führen Sie zusätzlich die folgenden Schritte aus.  
  
1.  Überprüfen Sie mit der folgenden Abfrage, ob [!INCLUDE[ssSB](../../includes/sssb-md.md)] für die msdb-Datenbank aktiviert ist.  
  
    ```  
    SELECT is_broker_enabled   
    FROM sys.databases  
    WHERE name = N'msdb';  
    ```  
  
     Weitere Informationen zum Aktivieren von [!INCLUDE[ssSB](../../includes/sssb-md.md)]finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)verschoben werden.  
  
2.  Überprüfen Sie, ob Datenbank-E-Mail funktionsfähig ist, indem Sie eine Test-E-Mail senden.  
  
##  <a name="Failure"></a> Prozedur zur Wiederherstellung nach Fehlern  
 Wenn eine Datei aufgrund eines Hardwarefehlers verschoben werden muss, müssen Sie die folgenden Schritte ausführen, um die Datei an einen neuen Speicherort zu verschieben: Diese Prozedur gilt für alle Systemdatenbanken mit Ausnahme der master- und Resource-Datenbanken.  
  
> [!IMPORTANT]  
>  Wenn die Datenbank nicht gestartet werden kann, d. h., wenn sie als fehlerverdächtig eingestuft wurde oder sich in einem nicht wiederhergestellten Status befindet, können nur Mitglieder der festen Rolle sysadmin die Datei verschieben.  
  
1.  Beenden Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , wenn sie gestartet ist.  
  
2.  Starten Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz im ausschließlichen Wiederherstellungsmodus der master-Datenbank durch Eingeben der folgenden Befehle an der Eingabeaufforderung. Bei den in diesen Befehlen angegebenen Parametern wird nach Groß- und Kleinschreibung unterschieden. Die Befehle werden nicht ausgeführt, wenn die Parameter nicht wie gezeigt angegeben werden.  
  
    -   Führen Sie für die Standardinstanz (MSSQLSERVER) den folgenden Befehl aus:  
  
        ```  
        NET START MSSQLSERVER /f /T3608
        ```  
  
    -   Führen Sie für eine benannte Instanz den folgenden Befehl aus:  
  
        ```  
        NET START MSSQL$instancename /f /T3608
        ```  
  
     Weitere Informationen finden Sie unter [Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
3.  Verwenden Sie für jede zu verschiebende Datei die **sqlcmd** -Befehle oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , um die folgende Anweisung auszuführen:  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE( NAME = logical_name , FILENAME = 'new_path\os_file_name' )  
    ```  
  
     Weitere Informationen zum Verwenden des **sqlcmd** -Hilfsprogramms finden Sie unter [Verwenden des Hilfsprogramms „sqlcmd“](../../relational-databases/scripting/sqlcmd-use-the-utility.md).  
  
4.  Starten Sie das Hilfsprogramm **sqlcmd** oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
5.  Beenden Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Führen Sie dazu z. B. `NET STOP MSSQLSERVER`aus.  
  
6.  Verschieben Sie die Datei(en) an den neuen Speicherort.  
  
7.  Starten Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]neu. Führen Sie dazu z. B. `NET START MSSQLSERVER`aus.  
  
8.  Überprüfen Sie die Dateiänderung durch Ausführen der folgenden Abfrage.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
##  <a name="master"></a> Verschieben der master-Datenbank  
 Führen Sie die folgenden Schritte aus, um die master-Datenbank zu verschieben.  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, auf **Microsoft SQL Server 2005**, auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
2.  Klicken Sie im Knoten **SQL Server-Dienste** mit der rechten Maustaste auf die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (z. B. **SQL Server (MSSQLSERVER)**), und wählen Sie **Eigenschaften**aus.  
  
3.  Klicken Sie im Dialogfeld **Eigenschaften von SQL Server (***Instanzname***)** auf die Registerkarte **Startparameter**.  
  
4.  Wählen Sie im Feld **Vorhandene Parameter** den Parameter „-d“aus, um die Masterdatendatei zu verschieben. Klicken Sie auf **Aktualisieren** , um die Änderung zu speichern.  
  
     Ändern Sie im Feld **Startparameter angeben** den Parameter in den neuen Pfad der Masterdatenbank.  
  
5.  Wählen Sie im Feld **Vorhandene Parameter** den Parameter „-l“aus, um die Masterprotokolldatei zu verschieben. Klicken Sie auf **Aktualisieren** , um die Änderung zu speichern.  
  
     Ändern Sie im Feld **Startparameter angeben** den Parameter in den neuen Pfad der Masterdatenbank.  
  
     Der Parameterwert der Datendatei muss dem `-d` -Parameter und der Wert der Protokolldatei muss dem `-l` -Parameter entsprechen. Im folgenden Beispiel werden die Parameterwerte für den Standardspeicherort der Masterdatendatei dargestellt.  
  
     `-dC:\Program Files\Microsoft SQL Server\MSSQL<version>.MSSQLSERVER\MSSQL\DATA\master.mdf`  
  
     `-lC:\Program Files\Microsoft SQL Server\MSSQL<version>.MSSQLSERVER\MSSQL\DATA\mastlog.ldf`  
  
     Wenn der geplante Speicherort für das Verschieben der Masterdatendatei `E:\SQLData`lautet, werden die Parameterwerte folgendermaßen geändert:  
  
     `-dE:\SQLData\master.mdf`  
  
     `-lE:\SQLData\mastlog.ldf`  
  
6.  Beenden Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , indem Sie mit der rechten Maustaste auf den Instanznamen klicken und **Beenden**auswählen.  
  
7.  Verschieben Sie die Dateien master.mdf und mastlog.ldf an den neuen Speicherort.  
  
8.  Starten Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]neu.  
  
9. Überprüfen Sie die Dateiänderung für die master-Datenbank, indem Sie die folgende Abfrage ausführen.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID('master');  
    GO  
    ```  

10. An diesem Punkt sollte SQL Server normal ausgeführt werden. Microsoft empfiehlt jedoch, auch den Registrierungseintrag unter `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\instance_ID\Setup`anzupassen, wobei *instance_ID* `MSSQL13.MSSQLSERVER`entspricht. Ändern Sie in dieser Struktur den Wert von `SQLDataRoot` in den neuen Pfad. Wenn Sie es versäumen, die Registrierung zu aktualisieren, können Fehler bei Patches und Upgrades auftreten.

  
##  <a name="Resource"></a> Verschieben der Ressourcendatenbank  
 Der Speicherort der Ressourcendatenbank lautet \<*Laufwerk*>:\Programme\Microsoft SQL Server\MSSQL\<Version>.\<*instance_name*>\MSSQL\Binn\\. Die Datenbank kann nicht verschoben werden.  
  
##  <a name="Follow"></a> Nachverfolgung: Nach dem Verschieben aller Systemdatenbanken  
 Wenn Sie alle Systemdatenbanken auf ein neues Laufwerk oder Volume bzw. auf einen anderen Server mit einem anderen Laufwerkbuchstaben verschoben haben, führen Sie die folgenden Updates aus.  
  
-   Ändern Sie den Pfad des SQL Server-Agent-Protokolls. Wenn Sie diesen Pfad nicht aktualisieren, kann SQL Server-Agent nicht gestartet werden.  
  
-   Ändern Sie den Standardspeicherort der Datenbank. Beim Erstellen einer neuen Datenbank kann ein Fehler auftreten, wenn der als Standardspeicherort angegebene Laufwerkbuchstabe und Pfad nicht vorhanden ist.  
  
#### <a name="change-the-sql-server-agent-log-path"></a>Ändern des Pfads des SQL Server-Agent-Protokolls  
  
1.  Erweitern Sie in SQL Server Management Studio im Objekt-Explorer **SQL Server-Agent**.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Fehlerprotokolle** , und klicken Sie auf **Konfigurieren**.  
  
3.  Geben Sie im Dialogfeld **Fehlerprotokolle des SQL Server-Agents konfigurieren** den neuen Speicherort der Datei SQLAGENT.OUT an. Der Standardspeicherort ist C:\Programme\Microsoft SQL Server\MSSQL\<version>.<instance_name>\MSSQL\Log\\.  
  
#### <a name="change-the-database-default-location"></a>Ändern des Standardspeicherorts der Datenbank  
  
1.  Klicken Sie in SQL Server Management Studio im Objekt-Explorer mit der rechten Maustaste auf den SQL Server-Server, und klicken Sie dann auf **Eigenschaften**.  
  
2.  Wählen Sie im Dialogfeld **Servereigenschaften** die Option **Datenbankeinstellungen**aus.  
  
3.  Wechseln Sie unter **Standardspeicherorte für Datenbank**zum neuen Speicherort sowohl für die Daten- als auch die Protokolldatei.  
  
4.  Starten und beenden Sie den SQL Server-Dienst, um die Änderung abzuschließen.  
  
##  <a name="Examples"></a> Beispiele  
  
### <a name="a-moving-the-tempdb-database"></a>A. Verschieben der tempdb-Datenbank  
 Im folgenden Beispiel werden die `tempdb` -Daten- und Protokolldatei im Rahmen einer geplanten Verschiebung an einen neuen Speicherort verschoben.  
  
> [!NOTE]  
>  Da tempdb jedes Mal neu erstellt wird, wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestartet wird, müssen die Daten- und Protokolldateien nicht physisch verschoben werden. Die Dateien werden am neuen Speicherort erstellt, sobald der Dienst in Schritt 3 neu gestartet wird. Bis der Dienst neu gestartet wird, verwendet tempdb weiterhin die Daten und die Protokolldateien des vorhandenen Speicherorts.  
  
1.  Ermitteln Sie die logischen Dateinamen der `tempdb` -Datenbank und ihren aktuellen Speicherort auf dem Datenträger.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'tempdb');  
    GO  
    ```  
  
2.  Ändern Sie den Speicherort der einzelnen Dateien mithilfe von `ALTER DATABASE`.  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = tempdev, FILENAME = 'E:\SQLData\tempdb.mdf');  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = templog, FILENAME = 'F:\SQLLog\templog.ldf');  
    GO  
    ```  
  
3.  Beenden Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und starten Sie sie erneut.  
  
4.  Überprüfen Sie die Dateiänderung.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'tempdb');  
    ```  
  
5.  Löschen Sie die Dateien `tempdb.mdf` und `templog.ldf` am ursprünglichen Speicherort.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ressourcendatenbank](../../relational-databases/databases/resource-database.md)   
 [tempdb-Datenbank](../../relational-databases/databases/tempdb-database.md)   
 [master-Datenbank](../../relational-databases/databases/master-database.md)   
 [msdb-Datenbank](../../relational-databases/databases/msdb-database.md)   
 [model-Datenbank](../../relational-databases/databases/model-database.md)   
 [Verschieben von Benutzerdatenbanken](../../relational-databases/databases/move-user-databases.md)   
 [Verschieben von Datenbankdateien](../../relational-databases/databases/move-database-files.md)   
 [Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Neuerstellen von Systemdatenbanken](../../relational-databases/databases/rebuild-system-databases.md)  
  
  
