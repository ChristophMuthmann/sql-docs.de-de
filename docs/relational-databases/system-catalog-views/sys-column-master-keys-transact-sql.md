---
title: column_master_keys (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- column_master_key_definitions_TSQL
- column_master_key_definitions
- sys.column_master_key_definitions_TSQL
- sys.column_master_key_definitions
- column_master_keys_TSQL
- column_master_keys
- sys.column_master_keys_TSQL
- sys.column_master_keys
dev_langs: TSQL
helpviewer_keywords:
- sys.column_master_key_definitions catalog view
- sys.column_master_keys catalog view
ms.assetid: fbec2efa-5fe9-4121-9b34-60497b0b2aca
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e22e052d88c339828e0a7e5d6f5803bc04b30925
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="syscolumnmasterkeys-transact-sql"></a>sys.column_master_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Datenbank-Hauptschlüssel, der hinzugefügt wird, mithilfe der [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) Anweisung. Jede Zeile stellt einen einzelnen spaltenhauptschlüssel (CMK).  
    
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Der Name des CMK.|  
|**column_master_key_id**|**int**|ID der Hauptschlüssel der Spalte.|  
|**create_date**|**datetime**|Datum, an dem spaltenhauptschlüssel erstellt wurde.|  
|**modify_date**|**datetime**|Datum, an dem spaltenhauptschlüssel zuletzt geändert wurde.|  
|**key_store_provider_name**|**sysname**|Name des Anbieters für die spaltenhauptschlüsselspeicher, die den CMK enthält. Zulässige Werte sind:<br /><br /> MSSQL_CERTIFICATE_STORE – Wenn der spaltenspeicher für den Hauptschlüssel einem Zertifikatspeicher gespeichert ist.<br /><br /> Eine einen benutzerdefinierten Wert, wenn der spaltenspeicher für den Hauptschlüssel eines benutzerdefinierten Typs ist.|  
|**key_path**|**nvarchar(4000)**|Eine Spalte speicherspezifischen Pfad des Hauptschlüssels des Schlüssels. Das Format des Pfads, hängt von der Spalte Hauptschlüssel Speichertyp ab. Beispiel:<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> Der Entwickler für eine benutzerdefinierte spaltenhauptschlüsselspeicher, ist dafür verantwortlich zu definieren ein Schlüsselpfad für die benutzerdefinierte spaltenhauptschlüsselspeicher ist.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **VIEW ANY COLUMN MASTER KEY** Berechtigung.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Always Encrypted &#40;Datenbankmodul&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
  
  
