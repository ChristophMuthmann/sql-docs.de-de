---
title: "Erstellen einer verschlüsselten Sicherung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e29061d3-c2ab-4d98-b9be-8e90a11d17fe
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 42b2038121e0bf9179fefafc89a7b17e3c1585c7
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="create-an-encrypted-backup"></a>Erstellen einer verschlüsselten Sicherung
  Dieses Thema beschreibt die Schritte, die notwendig sind, um eine verschlüsselte Sicherung mit Transact-SQL zu erstellen.  Ein Beispiel zum Verwenden von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]finden Sie unter [Erstellen einer vollständigen Datenbanksicherung (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md). 
  
## <a name="backup-to-disk-with-encryption"></a>Sicherung auf Datenträger mit Verschlüsselung  
 **Voraussetzungen:**  
  
-   Zugriff auf einen lokalen Datenträger oder Speicher mit ausreichendem Speicherplatz, um eine Sicherung der Datenbank zu erstellen.  
  
-   Ein Datenbank-Hauptschlüssel für die Masterdatenbank und ein Zertifikat oder ein asymmetrischer Schlüssel, das bzw. der für die SQL Server-Instanz verfügbar ist. Informationen zu Verschlüsselungsanforderungen und Berechtigungen finden Sie unter [Backup Encryption](../../relational-databases/backup-restore/backup-encryption.md).  
  
 Führen Sie die folgenden Schritte aus, um eine verschlüsselte Sicherung einer Datenbank auf einem lokalen Datenträger zu erstellen. In diesem Beispiel wird eine Benutzerdatenbank mit dem Namen MyTestDB verwendet.  
  
1.  **Erstellen Sie einen Datenbank-Hauptschlüssel der Masterdatenbank:** Wählen Sie ein Kennwort zum Verschlüsseln der Kopie des Hauptschlüssels aus, der in der Datenbank gespeichert wird. Stellen Sie eine Verbindung mit dem Datenbankmodul her, öffnen Sie ein neues Abfragefenster, kopieren Sie das folgende Beispiel, fügen Sie es ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Creates a database master key.   
    -- The key is encrypted using the password "<master key password>"  
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
2.  **Erstellen Sie ein Sicherungszertifikat:** Erstellen Sie ein Sicherungszertifikat in der Masterdatenbank. Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    Use Master  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDB Backup Encryption Certificate';  
    GO  
  
    ```  
  
3.  **Sichern Sie die Datenbank:** Geben Sie den Verschlüsselungsalgorithmus und das Zertifikat an, das verwendet werden soll. Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      COMPRESSION,  
      ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
 Ein Beispiel zum Verschlüsseln einer durch EKM geschützten Sicherung finden Sie unter [Erweiterbare Schlüsselverwaltung mit Azure Key Vault &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
### <a name="backup-to-windows-azure-storage-with-encryption"></a>Sicherung im Windows Azure-Speicher mit Verschlüsselung  
 Wenn Sie eine Sicherung im Windows Azure-Speicher mithilfe der Option **SQL Server-Sicherung über URL** erstellen, sind die Verschlüsselungsschritte die gleichen, aber Sie müssen URL als Ziel und SQL-Anmeldeinformationen verwenden, um sich beim Windows Azure-Speicher zu authentifizieren. Wenn Sie [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] mit Verschlüsselungsoptionen konfigurieren möchten, siehe [Aktivieren der verwalteten SQL Server-Sicherung in Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
 **Voraussetzungen:**  
  
-   Ein Windows-Speicherkonto und ein Container. Weitere Informationen finden Sie weiter oben unter [Lesson 1: Create Windows Azure Storage Objects](http://msdn.microsoft.com/library/74edd1fd-ab00-46f7-9e29-7ba3f1a446c5).  
  
-   Ein Datenbank-Hauptschlüssel für die Masterdatenbank und ein Zertifikat oder ein asymmetrischer Schlüssel in der SQL Server-Instanz. Informationen zu Verschlüsselungsanforderungen und Berechtigungen finden Sie unter [Backup Encryption](../../relational-databases/backup-restore/backup-encryption.md).  
  
1.  **Erstellen Sie SQL Server-Anmeldeinformationen:** Um SQL Server-Anmeldeinformationen zu erstellen, stellen Sie eine Verbindung mit dem Datenbankmodul her, öffnen Sie ein neues Abfragefenster, kopieren Sie das folgende Beispiel, fügen Sie es ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' – this is the name of the storage account you specified when creating a storage account    
    , SECRET = '<storage account access key>' – this should be either the Primary or Secondary Access Key for the storage account  
    ```  
  
2.  **Erstellen Sie einen Datenbank-Hauptschlüssel:** Wählen Sie ein Kennwort zum Verschlüsseln der Kopie des Hauptschlüssels aus, der in der Datenbank gespeichert wird. Stellen Sie eine Verbindung mit dem Datenbankmodul her, öffnen Sie ein neues Abfragefenster, kopieren Sie das folgende Beispiel, fügen Sie es ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
3.  **Erstellen Sie ein Sicherungszertifikat:** Erstellen Sie ein Sicherungszertifikat in der Masterdatenbank. Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE Master;  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDBBackupEncryptCert ';  
    GO  
  
    ```  
  
4.  **Sichern Sie die Datenbank:** Geben Sie den Verschlüsselungsalgorithmus und das Zertifikat an, das verwendet werden soll. Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO URL = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      CREDENTIAL 'mycredential' – this is the name of the credential created in the first step.  
      ,COMPRESSION  
      ,ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
  

