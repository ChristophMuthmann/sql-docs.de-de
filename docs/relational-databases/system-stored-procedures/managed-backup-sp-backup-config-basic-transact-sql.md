---
title: managed_backup. sp_backup_config_basic (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_backup_config_basic_TSQL
- sp_backup_config_basic
- managed_backup.sp_backup_config_basic
- managed_backup.sp_backup_config_basic_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_basic
- sp_backup_config_basic
ms.assetid: 3ad73051-ae9a-4e41-a889-166146e5508f
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 51507869caef7a8738381881f22f6cf9f1005144
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="managedbackupspbackupconfigbasic-transact-sql"></a>managed_backup. sp_backup_config_basic (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Konfiguriert die [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] grundlegende Einstellungen für eine bestimmte Datenbank oder für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Dieses Verfahren kann für eigene zum Erstellen einer grundlegenden verwalteten Sicherung Konfigurations aufgerufen werden. Jedoch, wenn Sie erweiterte Funktionen oder einen benutzerdefinierten Zeitplan hinzufügen möchten, zunächst konfigurieren Sie diese Einstellungen mithilfe von [sp_backup_config_advanced &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) und [managed_backup.sp_ Backup_config_schedule &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) vor dem Aktivieren der verwalteten Sicherung mit diesem Verfahren.  
   
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="Arguments"></a> Argumente  
 @enable_backup  
 Aktiviert oder deaktiviert [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] für die angegebene Datenbank. Die @enable_backup ist **BIT**. Erforderlicher Parameter beim Konfigurieren von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] für die erste Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Wenn Sie ein vorhandenes ändern [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] Konfiguration dieser Parameter ist optional. Alle nicht angegebenen Konfigurationswerte werden in diesem Fall ihre vorhandene Werte beibehalten.  
  
 @database_name  
 Der Name der Datenbank zum Aktivieren der verwalteten Sicherung in einer bestimmten Datenbank.  
  
 @container_url  
 Eine URL, der den Speicherort der Sicherung angibt. Wenn @credential_name NULL ist, diese URL wird die URL ein shared Access Signature (SAS) zu einem blobcontainer im Azure-Speicher und die Sicherungen verwenden die neue Sicherungsfunktion Block-Blob. Weitere Informationen finden Sie [Verständnis SAS](http://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/). Wenn @credential_name angegeben wird, dies ist eine Speicherkonto-URL und die Sicherungen verwenden, die als veraltet markierte Sicherungsfunktion Seite Blob.  
  
> [!NOTE]  
>  Nur eine SAS-URL wird für diesen Parameter zu diesem Zeitpunkt unterstützt.  
  
 @retention_days  
 Die Beibehaltungsdauer für die Sicherungsdateien in Tagen. Die @storage_url ist "int". Dies ist ein erforderlicher Parameter, beim Konfigurieren von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] zum ersten Mal auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Beim Ändern der [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] Konfiguration dieser Parameter ist optional. Wenn der Parameter nicht angegeben ist, werden die vorhandenen Konfigurationswerte beibehalten.  
  
 @credential_name  
 Der Name der SQL-Anmeldeinformationen, der zur Authentifizierung beim Windows Azure-Speicherkonto verwendet wird. @credentail_name ist **SYSNAME**. Wenn angegeben, wird die Sicherung ein Seiten-Blob gespeichert. Wenn dieser Parameter NULL ist, wird die Sicherung als Block-Blob gespeichert werden. Seiten-Blob-Sicherung ist veraltet, damit sie mit der neuen Block-BLOB-backup-Funktionalität bevorzugt wird. Bei Verwendung zum Ändern der [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]-Konfiguration ist dieser Parameter optional. Wenn nicht angegeben, werden die vorhandenen Konfigurationswerte beibehalten.  
  
> [!WARNING]  
>  Die **@credential_name** Parameter ist zu diesem Zeitpunkt nicht unterstützt. Nur Sicherung in block von Blob wird unterstützt, die erfordert, dass dieser Parameter gleich NULL sein.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in **Db_backupoperator** -Datenbankrolle mit **ALTER ANY CREDENTIAL** Berechtigungen und **EXECUTE** Berechtigungen für **Sp_delete_ Backuphistory** gespeicherte Prozedur.  
  
## <a name="examples"></a>Beispiele  
 Sie können den Container des Speicherkontos und die SAS-URL erstellen, mit der neuesten Azure PowerShell-Befehle. Im folgenden Beispiel erstellt einen neuen Container, Mycontainer, im Speicherkonto Mystorageaccount und klicken Sie dann eine SAS-URL für ihn mit vollen Berechtigungen erhält.  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 Im folgenden Beispiel wird [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] für die Instanz von SQL Server, die es ausgeführt wird, setzt die Aufbewahrungsrichtlinie auf 30 Tage, setzt Sie das Ziel auf einen Container namens "Mycontainer" in einem Speicherkonto mit dem Namen "Mystorageaccount".  
  
```Transact-SQL 
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=1  
                ,@container_url = 'https://mystorageaccount.blob.core.windows.net/mycontainer'  
                ,@retention_days=30;   
GO  
  
```
  
 Im folgenden Beispiel wird [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] für die Instanz von SQL Server deaktiviert, in der es ausgeführt wird.  
  
```Transact-SQL  
Use msdb;  
Go  
EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=0;  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
