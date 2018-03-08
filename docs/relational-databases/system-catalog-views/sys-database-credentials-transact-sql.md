---
title: Sys. database_credentials (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.database_credentials
- sys.database_credentials_TSQL
- database_credentials
- database_credentials_TSQL
helpviewer_keywords: sys.database_credentials catalog view
ms.assetid: 796322df-e62a-45bf-b519-89e1d521abce
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc6e8fe546412d4549c0724b34e434994ffa744d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatabasecredentials-transact-sql"></a>Sys. database_credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Gibt eine Zeile für jede Datenbank begrenzt Anmeldeinformationen in der Datenbank.  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) stattdessen.    
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|Die ID der datenbankweite Anmeldeinformationen. Ist in der Datenbank eindeutig.|  
|name|**sysname**|Name der Datenbank, begrenzt Anmeldeinformationen. Ist in der Datenbank eindeutig.|  
|credential_identity|**nvarchar(4000)**|Name der zu verwendenden Identität. In der Regel ist dies ein Windows-Benutzer. Er muss nicht eindeutig sein.|  
|create_date|**datetime**|Zeitpunkt, zu dem die datenbankbezogenen Anmeldeinformationen erstellt wurde.|  
|modify_date|**datetime**|Der Zeitpunkt, zu dem die datenbankbezogenen Anmeldeinformationen zuletzt geändert wurde.|  
|target_type|**nvarchar(100)**|Typ der Datenbank im Bereich einer Anmeldeinformationen aus. Gibt NULL für die Datenbank beschränkt Anmeldeinformationen.|  
|target_id|**int**|Die ID des Objekts, das die datenbankbezogenen Anmeldeinformationen zugeordnet ist. Gibt 0 zurück, für die Datenbank beschränkt, Anmeldeinformationen|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die `CONTROL`-Berechtigung für die Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Anmeldeinformationen &#40; Datenbankmodul &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [Erstellen Sie die Datenbank ausgelegte CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE ausgelegte CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE ausgelegte CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
