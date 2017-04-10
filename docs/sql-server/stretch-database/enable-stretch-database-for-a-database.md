---
title: "Aktivieren von Stretch-Datenbank f&#252;r eine Datenbank | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "08/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-server-stretch-database"
ms.suite: ""
ms.technology: 
  - "dbe-stretch"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Stretch-Datenbank, Datenbank aktivieren"
  - "Aktivieren der Datenbank für Stretch-Datenbank"
ms.assetid: 37854256-8c99-4566-a552-432e3ea7c6da
caps.latest.revision: 70
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 69
---
# Aktivieren von Stretch-Datenbank f&#252;r eine Datenbank
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Wählen Sie zum Konfigurieren einer vorhandenen Datenbank für Stretch-Datenbank **Aufgaben | Stretch | Aktivieren** aus, damit in SQL Server Management Studio für eine Datenbank der Assistent zum **Aktivieren der Datenbank für Stretch** geöffnet wird. Sie können alternativ Transact-SQL verwenden, um Stretch-Datenbank für eine Datenbank zu aktivieren.  
  
 Wenn Sie **Aufgaben | Stretch | Aktivieren** für eine bestimmte Tabelle auswählen und die Datenbank noch nicht für Stretch-Datenbank aktiviert haben, konfiguriert der Assistent die Datenbank für Stretch-Datenbank und ermöglicht es Ihnen, gleichzeitig Tabellen auszuwählen. Führen Sie die Schritte in diesem Thema statt der Schritte in [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)aus.  
  
 Um Stretch-Datenbank auf einer Datenbank oder für eine Tabelle zu aktivieren, benötigen Sie „db_owner“-Berechtigungen. Um Stretch-Datenbank auf einer Datenbank zu aktivieren, benötigen Sie außerdem CONTROL DATABASE-Berechtigungen.  

 >   [!NOTE] Wenn Sie Stretch-Datenbank später deaktivieren, sollten Sie daran denken, dass durch die Deaktivierung von Stretch-Datenbank für eine Tabelle oder Datenbank das Remoteobjekt nicht gelöscht wird. Wenn Sie die Remotetabelle oder Remotedatenbank löschen möchten, müssen Sie sie mithilfe des Azure-Verwaltungsportals löschen. Die Remoteobjekte erzeugen weiterhin Azure-Kosten, bis Sie die Objekte manuell löschen. 
 
## Vor dem Beginn  
  
-   Bevor Sie eine Datenbank für Stretch konfigurieren, empfiehlt es sich, den Stretch-Datenbankratgeber auszuführen, um für Stretch geeignete Datenbanken und Tabellen zu identifizieren. Der Stretch-Datenbankratgeber ermittelt auch Blockierungsprobleme. Weitere Informationen finden Sie unter [Identifizieren von Datenbanken und Tabellen für Stretch-Datenbank durch Ausführen des Ratgebers für Stretch-Datenbank](../../sql-server/stretch-database/stretch database databases and tables - stretch database advisor.md).  
  
-   Lesen Sie auch [Limitations for Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md) (Einschränkungen für Stretch-Datenbank).  
  
-   Stretch-Datenbank migriert Daten zu Azure. Daher benötigen Sie ein Azure-Konto und ein Abonnement für die Abrechnung. [Klicken Sie hier](http://azure.microsoft.com/en-us/pricing/free-trial/), um sich ein Azure-Konto einzurichten.  
  
-   Erhalten Sie die erforderlichen Informationen zu Verbindungen und Anmeldungen, um einen neuen Azure-Server zu erstellen oder einen vorhandenen Azure-Server auszuwählen.  
  
##  <a name="EnableTSQLServer"></a> Voraussetzung: Aktivieren Sie Stretch-Datenbank auf dem Server.  
 Bevor Sie Stretch-Datenbank für eine Datenbank oder Tabelle aktivieren können, müssen Sie es auch auf dem lokalen Server aktivieren. Dieser Vorgang erfordert die Berechtigung „Systemadministrator“ oder „Severadministrator“.  
  
-   Wenn Sie über die erforderlichen Administratorberechtigungen verfügen, konfiguriert der Assistent zum **Aktivieren der Datenbank für Stretch** den Server für Stretch.  
  
-   Wenn Sie nicht über die erforderlichen Berechtigungen verfügen, muss ein Administrator die Option manuell durch Ausführen von **sp_configure** aktivieren, bevor Sie den Assistenten ausführen. Alternativ muss ein Administrator den Assistenten ausführen.  
  
 Führen Sie zum manuellen Aktivieren von Stretch-Datenbank auf dem Server **sp_configure** aus, und aktivieren Sie die Option **remote data archive**. Im folgenden Beispiel wird die Option **remote data archive** aktiviert, indem ihr Wert auf 1 festgelegt wird.  
  
```  
EXEC sp_configure 'remote data archive' , '1';  
GO

RECONFIGURE;  
GO  
```  
  
 Weitere Informationen finden Sie unter [Configure the remote data archive Server Configuration Option](../../database-engine/configure-windows/configure-the-remote-data-archive-server-configuration-option.md) (Konfigurieren der Serverkonfigurationsoption „Remotedatenarchiv“) und [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
##  <a name="Wizard"></a> Verwenden des Assistenten zum Aktivieren von Stretch-Datenbank auf einer Datenbank  
 Weitere Informationen über den Assistenten zum Aktivieren einer Datenbank für Stretch, einschließlich der von Ihnen einzugebenden Informationen und der zu treffenden Entscheidungen, finden Sie unter [Get started by running the Enable Database for Stretch Wizard](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md) (Erste Schritte durch Ausführen des Assistenten zum Aktivieren von Stretch).  
  
##  <a name="EnableTSQLDatabase"></a> Verwenden von Transact-SQL zum Aktivieren von Stretch-Datenbank auf einer Datenbank  
 Bevor Sie Stretch-Datenbank für einzelne Tabellen aktivieren können, müssen Sie es auf der Datenbank aktivieren.  
  
 Um Stretch-Datenbank auf einer Datenbank oder für eine Tabelle zu aktivieren, benötigen Sie „db_owner“-Berechtigungen. Um Stretch-Datenbank auf einer Datenbank zu aktivieren, benötigen Sie außerdem CONTROL DATABASE-Berechtigungen.  
  
1.  Bevor Sie beginnen, wählen Sie einen vorhandenen Azure-Server für die Daten, die Stretch-Datenbank migrieren soll, oder erstellen Sie einen neuen Azure-Server.  
  
2.  Erstellen Sie auf dem Azure-Server eine Firewallregel mit dem IP-Adressbereich von SQL Server, der SQL Server die Kommunikation mit dem Remoteserver ermöglicht.  

    Sie können die erforderlichen Werte problemlos finden und die Firewallregel erstellen, indem Sie versuchen, über den Objekt-Explorer in SQL Server Management Studio (SSMS) eine Verbindung mit dem Azure-Server herzustellen. SSMS unterstützt Sie beim Erstellen der Regel, indem das folgende Dialogfeld geöffnet wird, das die erforderlichen IP-Adresswerte bereits enthält.
    
    ![Firewallregel für Stretch](../../sql-server/stretch-database/media/firewall-rule-for-stretch.png)
  
3.  Um eine SQL Server-Datenbank für Stretch-Datenbank zu konfigurieren, benötigt die Datenbank einen Datenbank-Hauptschlüssel. Der Datenbank-Hauptschlüssel sichert die Anmeldeinformationen, die Stretch-Datenbank für die Verbindung mit der Remotedatenbank verwendet. Nachstehend finden Sie ein Beispiel, in dem ein neuer Datenbank-Hauptschlüssel erstellt wird.  
  
    ```tsql  
    USE <database>; 
    GO  
  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD='<password>'; 
    GO
    ```  
    Weitere Informationen zum Datenbank-Hauptschlüssel finden Sie unter [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) und [Erstellen eines Datenbank-Hauptschlüssels](../../relational-databases/security/encryption/create-a-database-master-key.md).
    
4.  Wenn Sie eine Datenbank für Stretch-Datenbank konfigurieren, müssen Sie Anmeldeinformationen für Stretch-Datenbank bereitstellen, die für die Kommunikation zwischen dem lokalen SQL Server und dem Remoteserver in Azure verwendet werden. Hierfür stehen zwei Möglichkeiten zur Verfügung:  
  
    -   Sie können die Anmeldeinformationen eines Administrators angeben.  
  
        -   Wenn Sie Stretch-Datenbank durch Ausführen des Assistenten aktivieren, können Sie daraufhin die Anmeldeinformationen erstellen.  
  
        -   Wenn Sie Stretch-Datenbank durch Ausführen von **ALTER DATABASE** aktivieren möchten, müssen Sie die Anmeldeinformationen manuell erstellen, bevor Sie **ALTER DATABASE** zur Aktivierung von Stretch-Datenbank ausführen. 
        
        Nachstehend finden Sie ein Beispiel, in dem neue Anmeldeinformationen erstellt werden.
  
        ```tsql  
        CREATE DATABASE SCOPED CREDENTIAL <db_scoped_credential_name>  
            WITH IDENTITY = '<identity>' , SECRET = '<secret>' ;
        GO   
        ```  

         Weitere Informationen zu Anmeldeinformationen finden Sie unter[CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md). Zum Erstellen von Anmeldeinformationen ist die ALTER ANY CREDENTIAL-Berechtigung erforderlich.  

    -   Sie können ein Verbunddienstkonto verwenden, damit SQL Server mit dem Azure-Remoteserver kommunizieren kann, wenn alle der folgenden Bedingungen zutreffen.  
  
        -   Das Dienstkonto, unter dem die SQL Server-Instanz ausgeführt wird, ist ein Domänenkonto.  
  
        -   Das Domänenkonto gehört zu einer Domäne, deren Active Directory mit Azure Active Directory verbunden ist.  
  
        -   Der Azure-Remoteserver wird konfiguriert, um die Azure Active Directory-Authentifizierung zu unterstützen.  
  
        -   Das Dienstkonto, unter dem die SQL Server-Instanz ausgeführt wird, muss auf dem Azure-Remoteserver als ein dbmanager- oder sysadmin-Konto konfiguriert worden sein.  
  
5.  Um eine Datenbank für Stretch-Datenbank zu konfigurieren, führen Sie den Befehl ALTER DATABASE aus.  
  
    1.  Stellen Sie für das SERVER-Argument den Namen eines vorhandenen Azure-Servers bereit, einschließlich des Namensteils `.database.windows.net`, z.B. `MyStretchDatabaseServer.database.windows.net`.  
  
    2.  Stellen Sie vorhandene Administratoranmeldeinformationen mit dem Argument CREDENTIAL bereit, oder geben Sie FEDERATED_SERVICE_ACCOUNT = ON an. Das folgende Beispiel veranschaulicht eine vorhandene Anmeldeinformationen.  
  
    ```tsql  
    ALTER DATABASE <database name>  
        SET REMOTE_DATA_ARCHIVE = ON  
            (  
                SERVER = '<server_name>' ,  
                CREDENTIAL = <db_scoped_credential_name>  
            ) ;  
    GO
    ```  
  
## Nächste Schritte  
-   Aktivieren zusätzlicher Tabellen mithilfe des Artikels[Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) .  
  
-   [Überwachung und Problembehandlung bei der Datenmigration &#40;Stretch-Datenbank&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) zum Anzeigen des Status der Datenmigration.  
  
-   [Anhalten und Fortsetzen der Datenmigration &#40;Stretch-Datenbank&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
-   [Verwalten und Problembehandlung von Stretch-Datenbank](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
-   [Sichern von Stretch-aktivierten Datenbanken](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
  
-   [Restore Stretch-enabled databases (Wiederherstellen von für die Streckung aktivierten Datenbanken)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
## Siehe auch  
 [Identifizieren von Datenbanken und Tabellen für Stretch-Datenbank durch Ausführen des Ratgebers für Stretch-Datenbank](../../sql-server/stretch-database/stretch database databases and tables - stretch database advisor.md)   
 [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)  
  
  