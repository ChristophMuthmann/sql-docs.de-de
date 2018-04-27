---
title: Aktivieren von Stretch Database für eine Datenbank | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: stretch-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Stretch Database, enabling database
- enabling database for Stretch Database
ms.assetid: 37854256-8c99-4566-a552-432e3ea7c6da
caps.latest.revision: 70
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b977d38ef82901ddb6431e63a360545c7380f27d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="enable-stretch-database-for-a-database"></a>Enable Stretch Database for a database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Wählen Sie zum Konfigurieren einer vorhandenen Datenbank für Stretch Database **Aufgaben | Stretch | Aktivieren** aus, damit in SQL Server Management Studio für eine Datenbank der Assistent zum **Aktivieren der Datenbank für Stretch** geöffnet wird. Sie können alternativ Transact-SQL verwenden, um Stretch Database für eine Datenbank zu aktivieren.  
  
 Wenn Sie **Aufgaben | Stretch | Aktivieren** für eine bestimmte Tabelle auswählen und die Datenbank noch nicht für Stretch Database aktiviert haben, konfiguriert der Assistent die Datenbank für Stretch Database und ermöglicht es Ihnen, gleichzeitig Tabellen auszuwählen. Führen Sie die Schritte in diesem Artikel statt der Schritte in [Aktivieren von Stretch Database für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) aus.  
  
 Um Stretch Database für eine Datenbank oder eine Tabelle zu aktivieren, benötigen Sie „db_owner“-Berechtigungen. Um Stretch Database für eine Datenbank zu aktivieren, benötigen Sie außerdem CONTROL DATABASE-Berechtigungen.  

 >   [!NOTE]
 > Wenn Sie Stretch Database später deaktivieren, sollten Sie daran denken, dass durch die Deaktivierung von Stretch Database für eine Tabelle oder Datenbank das Remoteobjekt nicht gelöscht wird. Wenn Sie die Remotetabelle oder Remotedatenbank löschen möchten, müssen Sie sie mithilfe des Azure-Verwaltungsportals löschen. Die Remoteobjekte erzeugen weiterhin Azure-Kosten, bis Sie die Objekte manuell löschen. 
 
## <a name="before-you-get-started"></a>Vor dem Beginn  
  
-   Bevor Sie eine Datenbank für Stretch konfigurieren, empfiehlt es sich, den Stretch Database-Ratgeber auszuführen, um für Stretch geeignete Datenbanken und Tabellen zu identifizieren. Der Stretch Database-Ratgeber ermittelt auch Blockierungsprobleme. Weitere Informationen finden Sie unter [Identifizieren von Datenbanken und Tabellen für Stretch Database durch Ausführen des Ratgebers für Stretch Database](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md).  
  
-   Lesen Sie auch [Limitations for Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md)(Einschränkungen für Stretch-Datenbank).  
  
-   Stretch Database migriert Daten zu Azure. Daher benötigen Sie ein Azure-Konto und ein Abonnement für die Abrechnung. [Klicken Sie hier](http://azure.microsoft.com/en-us/pricing/free-trial/), um sich ein Azure-Konto einzurichten.  
  
-   Erhalten Sie die erforderlichen Informationen zu Verbindungen und Anmeldungen, um einen neuen Azure-Server zu erstellen oder einen vorhandenen Azure-Server auszuwählen.  
  
##  <a name="EnableTSQLServer">
            </a> Voraussetzung: Aktivieren Sie Stretch Database auf dem Server.  
 Bevor Sie Stretch Database für eine Datenbank oder Tabelle aktivieren können, müssen Sie es auch auf dem lokalen Server aktivieren. Dieser Vorgang erfordert die Berechtigung „Systemadministrator“ oder „Severadministrator“.  
  
-   Wenn Sie über die erforderlichen Administratorberechtigungen verfügen, konfiguriert der Assistent zum **Aktivieren der Datenbank für Stretch** den Server für Stretch.  
  
-   Wenn Sie nicht über die erforderlichen Berechtigungen verfügen, muss ein Administrator die Option manuell durch Ausführen von **sp_configure** aktivieren, bevor Sie den Assistenten ausführen. Alternativ muss ein Administrator den Assistenten ausführen.  
  
 Führen Sie zum manuellen Aktivieren von Stretch Database auf dem Server **sp_configure** aus, und aktivieren Sie die Option **remote data archive** . Im folgenden Beispiel wird die Option **remote data archive** aktiviert, indem ihr Wert auf 1 festgelegt wird.  
  
```sql
EXEC sp_configure 'remote data archive' , '1';  
GO

RECONFIGURE;  
GO  
```  
  
 Weitere Informationen finden Sie unter [Configure the remote data archive Server Configuration Option](../../database-engine/configure-windows/configure-the-remote-data-archive-server-configuration-option.md) (Konfigurieren der Serverkonfigurationsoption „Remotedatenarchiv“) und [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
##  <a name="Wizard">
            </a> Verwenden des Assistenten zum Aktivieren von Stretch Database für eine Datenbank  
 Weitere Informationen über den Assistenten zum Aktivieren einer Datenbank für Stretch, einschließlich der von Ihnen einzugebenden Informationen und der zu treffenden Entscheidungen, finden Sie unter [Get started by running the Enable Database for Stretch Wizard](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)(Erste Schritte durch Ausführen des Assistenten zum Aktivieren von Stretch).  
  
##  <a name="EnableTSQLDatabase">
            </a> Verwenden von Transact-SQL zum Aktivieren von Stretch Database für eine Datenbank  
 Bevor Sie Stretch Database für einzelne Tabellen aktivieren können, müssen Sie es auf der Datenbank aktivieren.  
  
 Um Stretch Database für eine Datenbank oder eine Tabelle zu aktivieren, benötigen Sie „db_owner“-Berechtigungen. Um Stretch Database für eine Datenbank zu aktivieren, benötigen Sie außerdem CONTROL DATABASE-Berechtigungen.  
  
1.  Bevor Sie beginnen, wählen Sie einen vorhandenen Azure-Server für die Daten, die Stretch Database migrieren soll, oder erstellen Sie einen neuen Azure-Server.  
  
2.  Erstellen Sie auf dem Azure-Server eine Firewallregel mit dem IP-Adressbereich von SQL Server, der SQL Server die Kommunikation mit dem Remoteserver ermöglicht.  

    Sie können die erforderlichen Werte problemlos finden und die Firewallregel erstellen, indem Sie versuchen, über den Objekt-Explorer in SQL Server Management Studio (SSMS) eine Verbindung mit dem Azure-Server herzustellen. SSMS unterstützt Sie beim Erstellen der Regel, indem das folgende Dialogfeld geöffnet wird, das die erforderlichen IP-Adresswerte bereits enthält.
    
    ![Firewallregel für Stretch](../../sql-server/stretch-database/media/firewall-rule-for-stretch.png)
  
3.  Um eine SQL Server-Datenbank für Stretch Database zu konfigurieren, benötigt die Datenbank einen Datenbank-Hauptschlüssel. Der Datenbank-Hauptschlüssel sichert die Anmeldeinformationen, die Stretch Database für die Verbindung mit der Remotedatenbank verwendet. Nachstehend finden Sie ein Beispiel, in dem ein neuer Datenbank-Hauptschlüssel erstellt wird.  
  
    ```sql  
    USE <database>; 
    GO  
  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD='<password>'; 
    GO
    ```  
    Weitere Informationen zum Datenbank-Hauptschlüssel finden Sie unter [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) und [Erstellen eines Datenbank-Hauptschlüssels](../../relational-databases/security/encryption/create-a-database-master-key.md).
    
4.  Wenn Sie eine Datenbank für Stretch Database konfigurieren, müssen Sie Anmeldeinformationen für Stretch Database bereitstellen, die für die Kommunikation zwischen dem lokalen SQL Server und dem Remoteserver in Azure verwendet werden. Hierfür stehen zwei Möglichkeiten zur Verfügung:  
  
    -   Sie können die Anmeldeinformationen eines Administrators angeben.  
  
        -   Wenn Sie Stretch Database durch Ausführen des Assistenten aktivieren, können Sie daraufhin die Anmeldeinformationen erstellen.  
  
        -   Wenn Sie Stretch Database durch Ausführen von **ALTER DATABASE**aktivieren möchten, müssen Sie die Anmeldeinformationen manuell erstellen, bevor Sie **ALTER DATABASE** zur Aktivierung von Stretch Database ausführen. 
        
        Nachstehend finden Sie ein Beispiel, in dem neue Anmeldeinformationen erstellt werden.
  
        ```sql  
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
  
5.  Um eine Datenbank für Stretch Database zu konfigurieren, führen Sie den Befehl ALTER DATABASE aus.  
  
    1.  Stellen Sie für das SERVER-Argument den Namen eines vorhandenen Azure-Servers bereit, einschließlich des Namensteils `.database.windows.net` , z.B. `MyStretchDatabaseServer.database.windows.net`.  
  
    2.  Stellen Sie vorhandene Administratoranmeldeinformationen mit dem Argument CREDENTIAL bereit, oder geben Sie FEDERATED_SERVICE_ACCOUNT = ON an. Das folgende Beispiel veranschaulicht eine vorhandene Anmeldeinformationen.  
  
    ```sql  
    ALTER DATABASE <database name>  
        SET REMOTE_DATA_ARCHIVE = ON  
            (  
                SERVER = '<server_name>' ,  
                CREDENTIAL = <db_scoped_credential_name>  
            ) ;  
    GO
    ```  
  
## <a name="next-steps"></a>Nächste Schritte  
-   Aktivieren zusätzlicher Tabellen mithilfe des Artikels[Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) .  
  
-   [Überwachung und Problembehandlung bei der Datenmigration &#40;Stretch-Datenbank&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) zum Anzeigen des Status der Datenmigration.  
  
-   [Anhalten und Fortsetzen der Datenmigration &#40;Stretch-Datenbank&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
-   [Verwalten und Problembehandlung von Stretch-Datenbank](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
-   [Sichern von Stretch-aktivierten Datenbanken](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
  
-   [Restore Stretch-enabled databases (Wiederherstellen von für die Streckung aktivierten Datenbanken)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Identifizieren von Datenbanken und Tabellen für Stretch Database durch Ausführen des Ratgebers für Stretch Database](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)   
 [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
