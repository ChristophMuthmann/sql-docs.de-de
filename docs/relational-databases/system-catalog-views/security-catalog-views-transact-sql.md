---
title: Sicherheitskatalogsichten (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- cryptography [SQL Server], catalog views
- encryption [SQL Server], catalog views
- catalog views [SQL Server], security
- security catalog views [SQL Server]
ms.assetid: 4d5cf1bf-09a7-4ee0-9dbb-5c584750fc67
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0a0959635f522c95af0884ea88a8948b5dbfb697
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="security-catalog-views-transact-sql"></a>Sicherheitskatalogsichten (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sicherheitsinformationen werden in Katalogsichten verfügbar gemacht, die im Hinblick auf Leistung und Nützlichkeit optimiert sind. Verwenden Sie ggf. die folgenden Katalogsichten, um auf Katalogmetadaten zuzugreifen.  
  
## <a name="database-level-views"></a>Sichten auf Datenbankebene  
  
|||  
|-|-|  
|[sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)|[sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) |  
|[sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)|[sys.master_key_passwords](../../relational-databases/system-catalog-views/sys-master-key-passwords-transact-sql.md) |  
|[sys.database_role_members](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)|[sys.user_token](../../relational-databases/system-catalog-views/sys-user-token-transact-sql.md) |  
  
## <a name="server-level-views"></a>Sichten auf Serverebene  
  
|||  
|-|-|  
|[sys.credentials](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)|[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)|  
|[sys.login_token](../../relational-databases/system-catalog-views/sys-login-token-transact-sql.md)|[sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)|  
|[sys.securable_classes](../../relational-databases/system-catalog-views/sys-securable-classes-transact-sql.md)|[sys.sql_logins](../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)|  
|[sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)|[sys.system_components_surface_area_configuration](../../relational-databases/system-catalog-views/sys-system-components-surface-area-configuration-transact-sql.md)|  
  
## <a name="encryption-views"></a>Verschlüsselungssichten  
  
|||  
|-|-|  
|[sys.asymmetric_keys](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md)|[sys.cryptographic_providers](../../relational-databases/system-catalog-views/sys-cryptographic-providers-transact-sql.md)|  
|[sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|[sys.key_encryptions](../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)|  
|[sys.column_encryption_key_values](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)|[sys.openkeys](../../relational-databases/system-catalog-views/sys-openkeys-transact-sql.md)|  
|[column_encryption_keys](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)|[Sys. security_policies &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)|  
|[column_master_key_definitions](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)|[Sys. security_predicates &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)|  
|[sys.crypt_properties](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)|[sys.symmetric_keys](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)|  
  
## <a name="sql-server-audit-views"></a>SQL Server-Überwachungssichten  
  
|||  
|-|-|  
|[sys.server_audits](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)|[sys.server_file_audits](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)|  
|[sys.server_audit_specifications](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)|[sys.server_audit_specifications_details](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)|  
|[sys.database_ audit_specifications](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)|[Sys.audit_database_specification_details](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitscenter für SQL Server-Datenbankmodul und Azure SQL-Datenbank](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [Sicherheitsbezogene dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
