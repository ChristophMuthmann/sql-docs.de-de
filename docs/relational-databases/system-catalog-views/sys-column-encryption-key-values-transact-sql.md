---
title: Sys. column_encryption_key_values (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- column_encryption_key_values
- column_encryption_key_values_TSQL
- sys.column_encryption_key_values
- sys.column_encryption_key_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_key_values catalog view
ms.assetid: 440875ab-b0e9-4966-8c16-01503558fedd
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 776e6e8ecf9e6ce79d2f1f72a01acfd5af268448
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syscolumnencryptionkeyvalues-transact-sql"></a>Sys. column_encryption_key_values (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu verschlüsselten Werten der Spalte Verschlüsselungsschlüssel (CEKs) erstellt, die entweder mit der [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) oder [ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)Anweisung. Jede Zeile stellt einen Wert, der einen CEK, mit einem spaltenhauptschlüssel (CMK) verschlüsselt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|Die ID des CEK in der Datenbank.|  
|**column_master_key_id**|**int**|ID der Hauptschlüssel der Spalte, die zum Verschlüsseln des Wert des CEK verwendet wurde.|  
|**encrypted_value**|**varbinary(8000)**|Mit den CMK im Column_master_key_id angegebenen verschlüsselten CEK-Wert.|  
|**encryption_algorithm_name**|**sysname**|Der Name eines Algorithmus zum Verschlüsseln des CEK-Wert.<br /><br /> Der Name des Verschlüsselungsalgorithmus, der zum Verschlüsseln des Werts verwendet wird. Der Algorithmus für die Systemanbieter muss **RSA_OAEP**.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **VIEW ANY COLUMN ENCRYPTION KEY** Berechtigung.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_master_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Always Encrypted &#40;Datenbankmodul&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
  
