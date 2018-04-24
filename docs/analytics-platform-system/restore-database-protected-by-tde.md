---
title: Wiederherstellen einer Datenbank durch TDE - Parallel Data Warehouse geschützt | Microsoft Docs
description: Verwenden Sie die folgenden Schritte zum Wiederherstellen einer Datenbank, die mithilfe von transparente datenverschlüsselung in Parallel Data Warehouse Analytics Platform System verschlüsselt wird.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a791d4110dc70c506025f8f11fb06b9ba2e5dcb3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>Stellen Sie eine durch TDE in Parallel Data Warehouse geschützte Datenbank wieder her
Verwenden Sie die folgenden Schritte zum Wiederherstellen einer Datenbank, die mit transparenter datenverschlüsselung verschlüsselt wird.  
  
Die [Transparent Data Encryption verwenden](transparent-data-encryption.md#using-tde) Beispiel enthält Code zum Aktivieren von TDE auf die `AdventureWorksPDW2012` Datenbank. Im folgende Code wird, beispielsweise durch eine Sicherung der Datenbank auf dem ursprünglichen Analytics Platform System (APS)-Gerät erstellen und dann wiederherstellen, das Zertifikat und die Datenbank auf einer anderen Einheit fortgesetzt.  
  
Der erste Schritt ist zum Erstellen einer Sicherung der Quelldatenbank.  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
Vorbereiten der neuen SQL Server PDW TDE durch einen Hauptschlüssel erstellen, Aktivieren der Verschlüsselung und Erstellen von Netzwerkanmeldeinformationen.  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
Die letzten beiden Schritten erstellen Sie das Zertifikat mithilfe der Sicherungen aus der ursprünglichen SQL Server PDW neu. Verwenden Sie das Kennwort, das Sie beim Erstellen der Sicherung des Zertifikats verwendet.  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert  
    FROM FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'   
    WITH PRIVATE KEY (FILE = '\\SECURE_SERVER\cert\MyServerCert.key',   
    DECRYPTION BY PASSWORD = '<password>');  
  
RESTORE DATABASE AdventureWorksPDW2012   
    FROM DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>Siehe auch  
[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)  
[CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md) 
[Sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[ZERTIFIKAT ERSTELLEN](../t-sql/statements/create-certificate-transact-sql.md)  
[STELLEN SIE DIE DATENBANK WIEDER HER.](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  
