---
title: 'Beispiel: Einrichten einer Datenbankspiegelung mit Windows-Authentifizierung (T-SQL) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- Windows authentication [SQL Server]
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: 35800769-aede-4aac-b077-0e0e487e302f
caps.latest.revision: 41
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d5fafa948d63eae3402e6d5b14587170f3675a56
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="example-setting-up-database-mirroring-using-windows-authentication-transact-sql"></a>Beispiel: Einrichten der Datenbankspiegelung mithilfe der Windows-Authentifizierung (Transact-SQL)
  In diesem Beispiel werden sämtliche Schritte erläutert, die für die Erstellung einer Datenbank-Spiegelungssitzung mit einem Zeugen mithilfe der Windows-Authentifizierung erforderlich sind. In den Beispielen in diesem Thema wird [!INCLUDE[tsql](../../includes/tsql-md.md)]verwendet. Beachten Sie Folgendes: Anstelle der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Schritte können Sie für die Einrichtung von Datenbankspiegelungen den Assistenten zum Konfigurieren der Sicherheit für die Datenbankspiegelung verwenden. Weitere Informationen finden Sie unter [Einrichten einer Datenbank-Spiegelungssitzung mithilfe der Windows-Authentifizierung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md).  
  
## <a name="prerequisite"></a>Voraussetzung  
 In diesem Beispiel wird die **AdventureWorks** -Beispieldatenbank verwendet, in der standardmäßig das einfache Wiederherstellungsmodell zum Einsatz kommt. Um diese Datenbank für die Datenbankspiegelung verwenden zu können, muss sie dahin gehend geändert werden, dass das vollständige Wiederherstellungsmodell verwendet wird. Verwenden Sie zu diesem Zweck in [!INCLUDE[tsql](../../includes/tsql-md.md)] die ALTER DATABASE-Anweisung wie folgt:  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks   
SET RECOVERY FULL;  
GO  
```  
  
 Informationen zum Ändern von Wiederherstellungsmodellen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] finden Sie unter [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank und die CREATE ENDPOINT-Berechtigung oder die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel sind die beiden Partner und der Zeuge die standardmäßigen Serverinstanzen auf drei Computersystemen. Von den drei Serverinstanzen wird dieselbe Windows-Domäne ausgeführt, das (als Dienststartkonto verwendete) Benutzerkonto für die Zeugenserverinstanz im Beispiel weicht jedoch ab.  
  
 In der folgenden Tabelle finden Sie eine Zusammenfassung der in diesem Beispiel verwendeten Werte.  
  
|Rolle bei der ersten Spiegelung|Hostsystem|Domänenbenutzerkonto|  
|----------------------------|-----------------|-------------------------|  
|Prinzipal|PARTNERHOST1|*\<MeineDomäne>\\<dbBenutzername\>*|  
|Spiegel|PARTNERHOST5|*\<MeineDomäne>\\<dbBenutzername\>*|  
|Zeuge|WITNESSHOST4|*\<EineDomäne>\\<ZeugeBenutzer\>*|  
  
1.  Erstellen Sie einen Endpunkt auf der Prinzipalserverinstanz (Standardinstanz auf PARTNERHOST1).  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=PARTNER)  
    GO  
    --Partners under same domain user; login already exists in master.  
    --Create a login for the witness server instance,  
    --which is running as Somedomain\witnessuser:  
    USE master ;  
    GO  
    CREATE LOGIN [Somedomain\witnessuser] FROM WINDOWS ;  
    GO  
    -- Grant connect permissions on endpoint to login account of witness.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Somedomain\witnessuser];  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
2.  Erstellen Sie einen Endpunkt auf der Spiegelserverinstanz (Standardinstanz auf PARTNERHOST5).  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
    --Partners under same domain user; login already exists in master.  
    --Create a login for the witness server instance,  
    --which is running as Somedomain\witnessuser:  
    USE master ;  
    GO  
    CREATE LOGIN [Somedomain\witnessuser] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account of witness.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Somedomain\witnessuser];  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
3.  Erstellen Sie einen Endpunkt auf der Zeugenserverinstanz (Standardinstanz auf WITNESSHOST4).  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=WITNESS)  
    GO  
    --Create a login for the partner server instances,  
    --which are both running as Mydomain\dbousername:  
    USE master ;  
    GO  
    CREATE LOGIN [Mydomain\dbousername] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
4.  Erstellen Sie die Spiegeldatenbank. Weitere Informationen finden Sie unter [Vorbereiten einer Spiegeldatenbank auf die Spiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)verwendet.  
  
5.  Legen Sie auf der Spiegelserverinstanz auf PARTNERHOST5 die Serverinstanz auf PARTNERHOST1 als Partner fest (hierdurch wird sie zur ersten Prinzipalserverinstanz).  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET PARTNER =   
        'TCP://PARTNERHOST1.COM:7022'  
    GO  
    ```  
  
6.  Legen Sie auf der Prinzipalserverinstanz auf PARTNERHOST1 die Serverinstanz auf PARTNERHOST5 als Partner fest (hierdurch wird sie zur ersten Spiegelserverinstanz).  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://PARTNERHOST5.COM:7022'  
    GO  
    ```  
  
7.  Legen Sie auf dem Prinzipalserver den Zeugen fest (der sich auf WITNESSHOST4 befindet).  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET WITNESS =   
        'TCP://WITNESSHOST4.COM:7022'  
    GO  
    ```  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Vorbereiten einer Spiegeldatenbank auf die Spiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [Starten des Assistenten zum Konfigurieren der Sicherheit für die Datenbankspiegelung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
-   [Einrichten der TRUSTWORTHY-Eigenschaft für eine Spiegeldatenbank &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)  
  
-   [Ermöglichen des Verwendens von Zertifikaten für ausgehende Verbindungen für einen Datenbankspiegelungs-Endpunkt &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
-   [Ermöglichen des Verwendens von Zertifikaten für eingehende Verbindungen für einen Datenbankspiegelungs-Endpunkt &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Beispiel: Einrichten der Datenbankspiegelung mithilfe von Zertifikaten &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Der Datenbankspiegelungs-Endpunkt &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Transportsicherheit für Datenbankspiegelung und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Verwalten von Metadaten beim Bereitstellen einer Datenbank auf einer anderen Serverinstanz &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [Sicherheitscenter für SQL Server-Datenbankmodul und Azure SQL-Datenbank](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  

