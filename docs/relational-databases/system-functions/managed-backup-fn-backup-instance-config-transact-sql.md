---
title: managed_backup.fn_backup_instance_config (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_backup_instance_config
- smart_admin.fn_backup_instance_config_TSQL
- fn_backup_instance_config_TSQL
- smart_admin.fn_backup_instance_config
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_backup_instance_config
- fn_backup_instance_config
ms.assetid: 2382a547-c0c9-4e1d-87c9-d8526192eb5a
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bad83cf900e1946612eb1065e4e413760c84d76f
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="managedbackupfnbackupinstanceconfig-transact-sql"></a>managed_backup.fn_backup_instance_config (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Gibt 1 Zeile mit den [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]-Standardkonfigurationseinstellungen für die SQL Server-Instanz zurück.  
  
 Verwenden Sie diese gespeicherte Prozedur, um die aktuellen [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]-Standardkonfigurationseinstellungen für die Instanz von SQL Server zu überprüfen oder zu bestimmen.  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
managed_backup.fn_backup_db_config ()  
```  
  
##  <a name="Arguments"></a> Argumente  
 Keine  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|is_smart_backup_enabled|INT|Zeigt 1 an, wenn [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] aktiviert ist, und 0, wenn [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] deaktiviert ist.|  
|credential_name|SYSNAME|Verwendete Standard SQL-Anmeldeinformationen für die Authentifizierung beim Speicher.|  
|retention_days|INT|Die auf Instanzebene festgelegte Standardbeibehaltungsdauer.|  
|storage_url|NVARCHAR(1024)|Die standardmäßige, auf Instanzebene festgelegte Speicherkonto-URL.|  
|encryption_algorithm|SYSNAME|Der Name des Verschlüsselungsalgorithmus. Wird auf NULL festgelegt, wenn keine Verschlüsselung angegeben ist.|  
|encryptor_type|NVARCHAR(32)|Der verwendete Verschlüsselungstyp: Zertifikat oder Asymmetrischer Schlüssel. Wird auf NULL festgelegt werden, wenn es keine Verschlüsselung angegeben ist.|  
|encryptor_name|SYSNAME|Der Name des Zertifikats oder des asymmetrischen Schlüssels. Wird auf NULL festgelegt, wenn kein Name angegeben ist.|  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Db_backupoperator** Datenbankrolle mit **ALTER ANY CREDENTIAL** Berechtigungen. Der Benutzer sollte nicht verweigert werden **VIEW ANY DEFINITION** Berechtigungen.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt die [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]-Standardkonfigurationseinstellungen für die Instanz zurück, auf der es ausgeführt wird:  
  
```  
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_instance_config ();  
  
```  
  
  
