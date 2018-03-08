---
title: database_scoped_credentials (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.database_scoped_credentials
- sys.database_scoped_credentials_TSQL
- database_scoped_credentials
- database_scoped_credentials_TSQL
helpviewer_keywords: sys.database_scoped_credentials catalog view
ms.assetid: 68e8aa6b-bcdc-42aa-93d8-d498f724c188
caps.latest.revision: "2"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 34db44a8b28ef9441e9bd6214e89ba2ef0e9f41b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatabasescopedcredentials-transact-sql"></a>database_scoped_credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Gibt eine Zeile für jede Datenbank begrenzt Anmeldeinformationen in der Datenbank.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|Die ID der datenbankweite Anmeldeinformationen. Ist in der Datenbank eindeutig.|  
|name|**sysname**|Name der Datenbank, begrenzt Anmeldeinformationen. Ist in der Datenbank eindeutig.|  
|credential_identity|**nvarchar(4000)**|Name der zu verwendenden Identität. In der Regel ist dies ein Windows-Benutzer. Er muss nicht eindeutig sein.|  
|create_date|**datetime**|Zeitpunkt, zu dem die datenbankbezogenen Anmeldeinformationen erstellt wurde.|  
|modify_date|**datetime**|Der Zeitpunkt, zu dem die datenbankbezogenen Anmeldeinformationen zuletzt geändert wurde.|  
|target_type|**nvarchar(100)**|Typ der Datenbank im Bereich einer Anmeldeinformationen aus. Gibt `NULL` für die Datenbank im Bereich einer Anmeldeinformationen.|  
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
  
  
