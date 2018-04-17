---
title: Sys. database_principals (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- database_principals
- database_principals_TSQL
- sys.database_principals
- sys.database_principals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_principals catalog view
ms.assetid: 8cb239e9-eb8c-4109-9cec-0d35de95fa0e
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d6d3cd64336d3374e74e5df05310e2e337ded062
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdatabaseprincipals-transact-sql"></a>sys.database_principals (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für jeden Sicherheitsprinzipal in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Der Name des Prinzipals, der innerhalb der Datenbank eindeutig ist.|  
|**principal_id**|**int**|Die ID des Prinzipals, die innerhalb der Datenbank eindeutig ist.|  
|**type**|**char(1)**|Prinzipaltyp:<br /><br /> A = Anwendungsrolle<br /><br /> C = Einem Zertifikat zugeordneter Benutzer<br /><br /> E = externen Benutzer aus Azure Active Directory<br /><br /> G = Windows-Gruppe<br /><br /> K = Einem asymmetrischen Schlüssel zugeordneter Benutzer<br /><br /> R = Datenbankrolle<br /><br /> S = SQL-Benutzer<br /><br /> U = Windows-Benutzer<br /><br /> X = externe Gruppe von Azure Active Directory-Gruppe oder Anwendungen|  
|**type_desc**|**nvarchar(60)**|Beschreibung des Prinzipaltyps.<br /><br /> APPLICATION_ROLE<br /><br /> CERTIFICATE_MAPPED_USER<br /><br /> EXTERNAL_USER<br /><br /> WINDOWS_GROUP<br /><br /> ASYMMETRIC_KEY_MAPPED_USER<br /><br /> DATABASE_ROLE<br /><br /> SQL_USER<br /><br /> WINDOWS_USER<br /><br /> EXTERNAL_GROUPS|  
|**default_schema_name**|**sysname**|Name, der verwendet werden, wenn SQL-Namen ein Schemas nicht angegeben wird. NULL für Prinzipale, die nicht vom Typ S, U oder A sind.|  
|**create_date**|**datetime**|Der Zeitpunkt, zu dem der Prinzipal erstellt wurde.|  
|**modify_date**|**datetime**|Der Zeitpunkt, zu dem der Prinzipal zum letzten Mal geändert wurde.|  
|**owning_principal_id**|**int**|ID des Prinzipals, der der Besitzer dieses Prinzipals ist. Alle Prinzipale außer Datenbankrollen müssen im Besitz **Dbo**.|  
|**SID**|**varbinary(85)**|Sicherheits-ID (SID) des Prinzipals.  NULL für SYS und INFORMATION SCHEMAS.|  
|**is_fixed_role**|**bit**|Falls 1, stellt diese Zeile einen Eintrag für eine der festen Datenbankrollen dar: db_owner, db_accessadmin, db_datareader, db_datawriter, db_ddladmin, db_securityadmin, db_backupoperator, db_denydatareader oder db_denydatawriter.|  
|**authentication_type**|**int**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt den Authentifizierungstyp an. Im folgenden sind die möglichen Werte und deren Beschreibungen.<br /><br /> 0: keine Authentifizierung<br />1: Instanz-Authentifizierung<br />2: Datenbankauthentifizierung<br />3: Windows-Authentifizierung|  
|**authentication_type_desc**|**nvarchar(60)**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Beschreibung des Authentifizierungstyps. Im folgenden sind die möglichen Werte und deren Beschreibungen.<br /><br /> NONE: Keine Authentifizierung<br />-Instanz: Instanzauthentifizierung<br />: Datenbankauthentifizierung Datenbank<br />WINDOWS: Windows-Authentifizierung|  
|**default_language_name**|**sysname**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt die Standardsprache für diesen Prinzipal an.|  
|**default_language_lcid**|**int**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt die Standard-LCID für diesen Prinzipal an.|  
|**allow_encrypted_value_modifications**|**bit**|**Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Verhindert bei Massenkopiervorgängen kryptografische Metadatenüberprüfungen auf dem Server. Dies ermöglicht es dem Benutzer zum Massenkopieren von Daten zwischen Tabellen oder Datenbanken ohne Entschlüsselung der Daten mit Always Encrypted verschlüsselt. Der Standardwert ist OFF. |      
  
## <a name="remarks"></a>Hinweise  
 Die *PasswordLastSetTime* Eigenschaften sind in allen unterstützten Konfigurationen von SQL Server verfügbar, aber die anderen Eigenschaften sind nur verfügbar, wenn SQL Server auf WindowsServer 2003 oder höher und CHECK_POLICY und CHECK_ ausgeführt wird Ablauf aktiviert sind. Finden Sie unter [Kennwortrichtlinie](../../relational-databases/security/password-policy.md) für Weitere Informationen.  
  
## <a name="permissions"></a>Berechtigungen  
 Jeder Benutzer kann den eigenen Benutzernamen, die Systembenutzer und die festen Datenbankrollen anzeigen. Zum Anzeigen anderer Benutzer ist ALTER ANY USER oder eine Berechtigung für den Benutzer erforderlich. Zum Anzeigen benutzerdefinierter Rollen ist ALTER ANY ROLE oder die Mitgliedschaft in der Rolle erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-listing-all-the-permissions-of-database-principals"></a>A: Auflisten aller Berechtigungen von Datenbankprinzipalen  
 Mit der folgenden Abfrage werden die Berechtigungen aufgelistet, die Datenbankprinzipalen ausdrücklich gewährt oder verweigert wurden.  
  
> [!IMPORTANT]  
>  Die Berechtigungen von festen Datenbankrollen werden nicht in sys.database_permissions aufgeführt. Daher können Datenbankprinzipale über zusätzliche Berechtigungen verfügen, die hier nicht aufgeführt werden.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="b-listing-permissions-on-schema-objects-within-a-database"></a>G. Auflisten von Berechtigungen für Schemaobjekte in einer Datenbank  
 Die folgende Abfrage verknüpft sys.database_principals und sys.database_permissions mit sys.objects und sys.schemas, um Berechtigungen aufzulisten, die bestimmten Schemaobjekten gewährt oder verweigert wurden.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="c-listing-all-the-permissions-of-database-principals"></a>"C:" Auflisten aller Berechtigungen von datenbankprinzipalen  
 Mit der folgenden Abfrage werden die Berechtigungen aufgelistet, die Datenbankprinzipalen ausdrücklich gewährt oder verweigert wurden.  
  
> [!IMPORTANT]  
>  Die Berechtigungen der festen Datenbankrollen erscheinen nicht im `sys.database_permissions`. Daher können Datenbankprinzipale über zusätzliche Berechtigungen verfügen, die hier nicht aufgeführt werden.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="d-listing-permissions-on-schema-objects-within-a-database"></a>D: Auflisten der Berechtigungen für Schemaobjekte in einer Datenbank  
 Die folgende Abfrage Joins `sys.database_principals` und `sys.database_permissions` auf `sys.objects` und `sys.schemas` beim Auflisten der Berechtigungen, die bestimmten Schemaobjekten erteilt oder verweigert.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Eigenständige Datenbankbenutzer - machen Sie Ihre Datenbank portabel](../../relational-databases/security/contained-database-users-making-your-database-portable.md)   
 [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)  
  
  


