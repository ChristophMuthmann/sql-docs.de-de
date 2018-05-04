---
title: Sys. database_credentials (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.database_credentials
- sys.database_credentials_TSQL
- database_credentials
- database_credentials_TSQL
helpviewer_keywords:
- sys.database_credentials catalog view
ms.assetid: 796322df-e62a-45bf-b519-89e1d521abce
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ce7ab8708f1bfb8cdb141c32971a477cfbafe64d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatabasecredentials-transact-sql"></a>Sys. database_credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Gibt eine Zeile für jede Datenbank begrenzt Anmeldeinformationen in der Datenbank.  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwendung [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) stattdessen.    
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|Die ID der datenbankweite Anmeldeinformationen. Ist in der Datenbank eindeutig.|  
|name|**sysname**|Name der Datenbank, begrenzt Anmeldeinformationen. Ist in der Datenbank eindeutig.|  
|credential_identity|**nvarchar(4000)**|Name der zu verwendenden Identität. In der Regel ist dies ein Windows-Benutzer. Er muss nicht eindeutig sein.|  
|create_date|**datetime**|Zeitpunkt, zu dem die datenbankbezogenen Anmeldeinformationen erstellt wurde.|  
|modify_date|**datetime**|Der Zeitpunkt, zu dem die datenbankbezogenen Anmeldeinformationen zuletzt geändert wurde.|  
|target_type|**Nvarchar(100)**|Typ der Datenbank im Bereich einer Anmeldeinformationen aus. Gibt NULL für die Datenbank beschränkt Anmeldeinformationen.|  
|target_id|**int**|Die ID des Objekts, das die datenbankbezogenen Anmeldeinformationen zugeordnet ist. Gibt 0 zurück, für die Datenbank beschränkt, Anmeldeinformationen|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die `CONTROL`-Berechtigung für die Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Anmeldeinformationen &#40;Datenbank-Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
