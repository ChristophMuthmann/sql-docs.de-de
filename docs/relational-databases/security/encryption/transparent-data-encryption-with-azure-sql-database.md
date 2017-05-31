---
title: "Transparente Datenverschlüsselung in Azure SQL-Datenbank | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
- MSDN content
- MSDN - SQL DB
ms.date: 09/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TDE, SQL Database
- encryption (SQL Database), TDE
- Transparent Data Encryption, SQL Database
ms.assetid: 0bf7e8ff-1416-4923-9c4c-49341e208c62
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1c607015f1ead5b19d4c32c5bac62eb624b0578b
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>Transparente Datenverschlüsselung in Azure SQL-Datenbank
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx_md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] Die transparente Datenverschlüsselung unterstützt Maßnahmen zum Schutz vor bösartigen Aktivitäten, indem sie die Verschlüsselung und Entschlüsselung der Datenbank in Echtzeit sowie der ihr zugeordneten Sicherheitskopien und der Transaktionsprotokolle in Ruhephasen vornimmt, ohne Änderungen an der Anwendung zu erfordern.  
  
 TDE verschlüsselt den Speicher einer gesamten Datenbank mithilfe eines symmetrischen Schlüssels, der als Verschlüsselungsschlüssel für die Datenbank bezeichnet wird. In [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] ist der Datenbank-Verschlüsselungsschlüssel durch ein integriertes Serverzertifikat geschützt. Das integrierte Serverzertifikat ist für jeden [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] -Server eindeutig. Wenn sich eine Datenbank in einer GeoDR-Beziehung befindet, ist sie auf jedem Server durch einen anderen Schlüssel geschützt. Wenn zwei Datenbanken mit dem gleichen Server verbunden sind, verwenden sie das gleiche integrierte Zertifikat. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] tauscht diese Zertifikate mindestens alle 90 Tage automatisch untereinander. Eine allgemeine Beschreibung von TDE finden Sie unter [Transparente Datenverschlüsselung &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md).  
  
 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] unterstützt die Integration des Azure-Schlüsseltresors mit TDE nicht. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] kann bei der Ausführung auf einem virtuellen Azure-Computer einen asymmetrischen Schlüssel aus dem Schlüsseltresor verwenden. Weitere Informationen finden Sie im Thema [Erweiterbare Schlüsselverwaltung mit Azure Key Vault &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
##  <a name="Permissions"></a> Berechtigungen  
 Um TDE über das Azure-Portal mithilfe der REST-API oder mithilfe von PowerShell zu konfigurieren, müssen Sie als Azure-Besitzer, Azure-Mitwirkender oder SQL-Sicherheitsmanager verbunden sein.  
  
 Zum Konfigurieren von TDE mithilfe von [!INCLUDE[tsql](../../../includes/tsql-md.md)] müssen folgende Voraussetzungen erfüllt sein:  
  
-   Zum Ausführen der Anweisung ALTER DATABASE mit der Option SET ist die Mitgliedschaft in der Rolle **dbmanager** erforderlich.  
  
##  <a name="Preview"></a> Aktivieren von TDE in einer Datenbank mithilfe des Portals  
  
1.  Suchen Sie das Azure-Portal unter [https://portal.azure.com](https://portal.azure.com) auf, und melden Sie sich mit Ihrem Azure-Administrator- oder Mitwirkendenkonto an.  
  
2.  Klicken Sie auf dem linken Banner auf **DURCHSUCHEN**, und klicken Sie dann auf **SQL-Datenbanken**.  
  
3.  Klicken Sie auf Ihre Benutzerdatenbank, während **SQL-Datenbanken** im linken Bereich ausgewählt ist.  
  
4.  Klicken Sie auf dem Datenbankblatt auf **Alle Einstellungen**.  
  
5.  Klicken Sie auf dem Blatt **Einstellungen** auf die Kachel **Transparente Datenverschlüsselung** , um das Blatt **Transparente Datenverschlüsselung** zu öffnen.  
  
6.  Schieben Sie auf dem Blatt **Datenverschlüsselung** den Schalter **Datenverschlüsselung** auf **Ein**, und klicken Sie anschließend auf **Speichern** (oben auf der Seite), um die Einstellung zu übernehmen. Der **Verschlüsselungsstatus** ist eine ungefähre Angabe zum Fortschritt der transparenten Datenverschlüsselung.  
  
     ![SQL-Datenbank TDE Start Verschlüsselung](../../../relational-databases/security/encryption/media/sqldb-tde-encrypt.png "SQL Database TDE Start Encryption")  
  
     Sie können den Verlauf der Verschlüsselung aber auch überwachen, indem Sie die Verbindung mit [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] mithilfe eines Abfragetools wie [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] als Datenbankbenutzer mit der Berechtigung **DATENBANKSTATUS ANZEIGEN** herstellen. Fragen Sie die **encryption_state** -Spalte der Sicht [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) ab.  
  
##  <a name="Encrypt"></a> Aktivieren von TDE für [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] mithilfe von Transact-SQL  
 TDE wird wie folgt aktiviert.  
  
###  <a name="TsqlProcedure"></a>  
  
1.  Stellen Sie eine Verbindung mit der Datenbank mithilfe eines Kontos her, das ein Administratorkonto oder ein Mitglied der Rolle **dbmanager** in der Masterdatenbank ist.  
  
2.  Führen Sie die folgenden Anweisungen aus, um die Datenbank zu entschlüsseln.  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;  
    GO  
    ```  
  
3.  Um den Verlauf der Verschlüsselung auf [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]zu überwachen, können Datenbankbenutzer mit der Berechtigung **VIEW DATABASE STATE** die Spalte **encryption_state** der Sicht [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) abfragen.  
  
##  <a name="EncryptPS"></a> Aktivieren und Deaktivieren von TDE für [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] mithilfe von PowerShell  
 Mithilfe von Azure PowerShell können Sie den folgenden Befehl ausführen, um TDE ein- oder auszuschalten. Sie müssen eine Verbindung Ihres Kontos mit dem PS-Fenster herstellen, bevor Sie den Befehl ausführen. Passen Sie die Parameter `ServerName`, `ResourceGroupName`und `DatabaseName` des Beispiels an Ihre Werte an. Weitere Informationen zu PowerShell finden Sie unter [Installieren und Konfigurieren von Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).  
  
> [!NOTE]  
>  Zum Fortfahren müssen Sie Azure PowerShell Version 1.0 installieren und konfigurieren. Version 0.9.8 kann zwar noch verwendet werden, wurde aber als veraltet markiert und erfordert mit dem Befehl `PS C:\> Switch-AzureMode -Name AzureResourceManager` einen Wechsel zu den AzureResourceManager-Cmdlets.  
  
###  <a name="PSlProcedure"></a>  
  
1.  Zum Aktivieren von TDE geben Sie den TDE-Status zurück und zeigen die Veschlüsselungsaktivität an.  
  
    ```  
    PS C:\> Set-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"  
  
    PS C:\> Get-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    PS C:\> Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
    ```  
  
     Bei Verwendung von Version 0.9.8 müssen Sie die Befehle Set-AzureSqlDatabaseTransparentDataEncryption, Get-AzureSqlDatabaseTransparentDataEncryption und Get-AzureSqlDatabaseTransparentDataEncryptionActivity verwenden.  
  
2.  So deaktivieren Sie TDE:  
  
    ```  
    PS C:\> Set-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"  
  
    ```  
  
     Bei Verwendung von Version 0.9.8 müssen Sie den Befehl Set-AzureSqlDatabaseTransparentDataEncryption verwenden.  
  
##  <a name="Decrypt"></a> Entschlüsseln Sie eine mithilfe von TDE geschützte Datenbank auf [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]  
  
#### <a name="to-disable-tde-by-using-the-azure-portal"></a>So deaktivieren Sie TDE mithilfe des Azure-Portals  
  
1.  Suchen Sie das Azure-Portal unter [https://portal.azure.com](https://portal.azure.com) auf, und melden Sie sich mit Ihrem Azure-Administrator- oder Mitwirkendenkonto an.  
  
2.  Klicken Sie auf dem linken Banner auf **DURCHSUCHEN**, und klicken Sie dann auf **SQL-Datenbanken**.  
  
3.  Klicken Sie auf Ihre Benutzerdatenbank, während **SQL-Datenbanken** im linken Bereich ausgewählt ist.  
  
4.  Klicken Sie auf dem Datenbankblatt auf **Alle Einstellungen**.  
  
5.  Klicken Sie auf dem Blatt **Einstellungen** auf die Kachel **Transparente Datenverschlüsselung** , um das Blatt **Transparente Datenverschlüsselung** zu öffnen.  
  
6.  Schieben Sie auf dem Blatt **Transparente Datenverschlüsselung** den Schalter **Datenverschlüsselung** auf **Aus**, und klicken Sie anschließend auf **Speichern** (oben auf der Seite), um die Einstellung zu übernehmen. Der **Verschlüsselungsstatus** zeigt annähernd den Status der transparenten Datenentschlüsselung an.  
  
     Sie können den Verlauf der Entschlüsselung aber auch überwachen, indem Sie die Verbindung mit [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] mithilfe eines Abfragetools wie [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] als Datenbankbenutzer mit der Berechtigung **DATENBANKSTATUS ANZEIGEN** herstellen. Fragen Sie die **encryption_state** -Spalte der Sicht [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) ab.  
  
#### <a name="to-disable-tde-by-using-transact-sql"></a>So deaktivieren Sie TDE mithilfe von Transact-SQL  
  
1.  Stellen Sie eine Verbindung mit der Datenbank mithilfe eines Kontos her, das ein Administratorkonto oder ein Mitglied der Rolle **dbmanager** in der Masterdatenbank ist.  
  
2.  Führen Sie die folgenden Anweisungen aus, um die Datenbank zu entschlüsseln.  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;  
    GO  
    ```  
  
3.  Um den Verlauf der Verschlüsselung auf [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]zu überwachen, können Datenbankbenutzer mit der Berechtigung **VIEW DATABASE STATE** die Spalte **encryption_state** der Sicht [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) abfragen.  
  
##  <a name="Working"></a> Verschieben einer durch TDE geschützten Datenbank auf [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]  
 Für Vorgänge in Azure brauchen Datenbanken nicht entschlüsselt zu werden. Die TDE-Einstellungen für die Quelldatenbank oder die primäre Datenbank werden transparent an das Ziel vererbt. Dazu gehören auch Vorgänge, die dieses beinhalten:  
  
-   Geowiederherstellung  
  
-   Self-Service-Point-In-Time-Wiederherstellung  
  
-   Wiederherstellung einer gelöschten Datenbank  
  
-   Aktive Georeplikation  
  
-   Erstellen einer Datenbankkopie  
  
 Beim Exportieren einer durch TDE geschützten Datenbank mithilfe der Funktion „Datenbank exportieren“ im [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] -Portal oder im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Import- und -Export-Assistenten werden die exportierten Datenbankinhalte nicht verschlüsselt. Diese exportierten Inhalte werden in unverschlüsselten BACPAC-Dateien gespeichert. Achten Sie darauf, die BACPAC-Dateien in geeigneter Weise zu schützen und TDE zu aktivieren, sobald der Import der neuen Datenbank abgeschlossen ist. 
 
 Wenn die BACPAC-Datei z. B. von einem lokalen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]exportiert wird, erfolgt keine automatische Verschlüsselung des importierten Inhalts der neuen Datenbank. Wenn die BACPAC-Datei von einem [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] auf einen lokalen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]exportiert wird, erfolgt ebenfalls keine automatische Verschlüsselung der neuen Datenbank.  
 
 Die einzige Ausnahme ist beim Exportieren in und von [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] – TDE wird in der neuen Datenbank aktiviert, aber die BACPAC-Datei selbst wird weiterhin nicht verschlüsselt.
  
## <a name="related-sql-server-topic"></a>Verwandte SQL Server-Themen  
 [Aktivieren von TDE in SQL Server mithilfe von EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Transparente Datenverschlüsselung &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)  
  
  

