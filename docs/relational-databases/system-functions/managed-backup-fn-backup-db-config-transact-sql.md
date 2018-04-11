---
title: managed_backup.fn_backup_db_config (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_backup_db_config
- smart_admin.fn_backup_db_config_TSQL
- fn_backup_db_config
- fn_backup_db_config_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_backup_db_config
- fn_backup_db_config
ms.assetid: 7c755d8a-64dd-44b2-be5e-735d30758900
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d18a24bdf8021fd27df0ec51e4937e80ae9c0516
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="managedbackupfnbackupdbconfig-transact-sql"></a>managed_backup.fn_backup_db_config (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Gibt keine, eine oder mehrere Zeilen mit [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]-Konfigurationseinstellungen zurück. Gibt eine Zeile für die angegebene Datenbank oder die Informationen für alle Datenbanken zurück, die auf der Instanz mit [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] konfiguriert sind.  
  
 Verwenden Sie diese gespeicherte Prozedur, um die aktuellen [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]-Konfigurationseinstellungen für eine Datenbank oder alle Datenbanken in einer SQL Server-Instanz zu überprüfen oder zu ermitteln.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
managed_backup.fn_backup_db_config (‘database_name’ | ‘’ | NULL)  
```  
  
##  <a name="Arguments"></a> Argumente  
 @db_name  
 Der Name der Datenbank. Die @db_name Parameter ist **SYSNAME**. Wenn eine leere Zeichenfolge oder ein NULL-Wert an diesen Parameter übergeben wird, werden die Informationen über alle Datenbanken in der SQL Server-Instanz zurückgegeben.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|db_name|SYSNAME|Datenbankname.|  
|db_guid|UNIQUEIDENTIFIER|Ein Bezeichner, der die Datenbank eindeutig identifiziert.|  
|is_availability_database|BIT|Gibt an, ob die Datenbank einer Verfügbarkeitsgruppe angehört. Der Wert 1 gibt an, dass die Datenbank eine Verfügbarkeitsdatenbank ist, der Wert 0, dass dies nicht der Fall ist.|  
|is_dropped|BIT|Der Wert 1 gibt an, dass es sich um eine gelöschte Datenbank handelt.|  
|credential_name|SYSNAME|Der Name der SQL-Anmeldeinformationen, der zur Authentifizierung beim Speicherkonto verwendet wird. Ein NULL-Wert gibt an, dass keine SQL-Anmeldeinformationen festgelegt sind.|  
|retention_days|INT|Die aktuelle Beibehaltungsdauer in Tagen. Ein NULL-Wert gibt an, dass [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] nie für diese Datenbank konfiguriert wurde.|  
|is_smart_backup_enabled|INT|Gibt an, ob [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] derzeit für diese Datenbank aktiviert ist. Der Wert 1 gibt an, dass [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] derzeit aktiviert ist, der Wert 0 gibt an, dass [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] für diese Datenbank deaktiviert ist.|  
|storage_url|NVARCHAR(1024)|Die URL des Speicherkontos.|  
|Encryption_algorithm|NCHAR(20)|Gibt den aktuellen Verschlüsselungsalgorithmus zurück, der beim Verschlüsseln der Sicherung verwendet werden soll.|  
|Encryptor_type|NCHAR(15)|Gibt die Verschlüsselungseinstellung zurück: Zertifikat oder Asymmetrischer Schlüssel.|  
|Encryptor_name|NCHAR(max_length_of_cert/asymm_key_name)|Der Name des Zertifikats oder des asymmetrischen Schlüssels.|  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Db_backupoperator** Datenbankrolle mit **ALTER ANY CREDENTIAL** Berechtigungen. Der Benutzer sollte nicht verweigert werden **VIEW ANY DEFINITION** Berechtigungen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]-Konfiguration für "TestDB" zurückgegeben.  
  
 Wählen Sie für jeden Codeausschnitt "tsql" im Sprachattributfeld aus.  
  
```  
Use msdb  
GO  
SELECT * FROM managed_backup.fn_backup_db_config('TestDB')  
```  
  
 Im folgenden Beispiel wird die [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]-Konfiguration für alle Datenbanken in der Instanz von SQL Server zurückgegeben, für die sie ausgeführt wird.  
  
```  
Use msdb  
GO  
SELECT * FROM managed_backup.fn_backup_db_config (NULL)  
```  
  
  
