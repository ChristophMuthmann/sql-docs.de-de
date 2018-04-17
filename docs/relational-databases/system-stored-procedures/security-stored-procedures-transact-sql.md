---
title: Gespeicherte Sicherheitsprozeduren (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
dev_langs:
- TSQL
helpviewer_keywords:
- system stored procedures [SQL Server], security
- stored procedures [SQL Server], security
- security [SQL Server], stored procedures
ms.assetid: 62b72907-7e95-4c97-9891-0c45d5b678ce
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b894dd2099e41a2a0718cd443c079444cc18d475
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="security-stored-procedures-transact-sql"></a>Gespeicherte Sicherheitsprozeduren (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt die folgenden gespeicherten Systemprozeduren, die zum Verwalten der Sicherheit verwendet werden. Einige dieser gespeicherten Prozeduren sind veraltet, jedoch weiterhin zur Unterstützung der Abwärtskompatibilität zur Verfügung. In den Themen für veraltete Prozeduren wird der jeweilige Ersatz aufgeführt.  

|||  
|-|-|  
[Sys.sp_add_trusted_assembly]( sys-sp-add-trusted-assembly-transact-sql.md) |[Sp_addapprole](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md) (veraltet)|
|[sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)|[sp_addlinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)
|[Sp_addlogin](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md) (veraltet) |[Sp_addremotelogin](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md) (veraltet)
|[Sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md) (veraltet) |[Sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) (veraltet)
|[Sp_addserver](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md) (veraltet) |[Sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md) (veraltet)
|[Sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md) (veraltet) |[Sp_approlepassword](../../relational-databases/system-stored-procedures/sp-approlepassword-transact-sql.md) (veraltet)
|[sp_audit_write](../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md) |[sp_change_users_login](../../relational-databases/system-stored-procedures/sp-change-users-login-transact-sql.md)
|[sp_changedbowner](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md) |[Sp_changeobjectowner](../../relational-databases/system-stored-procedures/sp-changeobjectowner-transact-sql.md) (veraltet)
|[sp_control_dbmasterkey_password](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md) |[Sp_dbfixedrolepermission](../../relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql.md) (veraltet)
|[Sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) (veraltet) |[Sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md) (veraltet)
|[Sp_denylogin](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md) (veraltet) |[sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)
|[Sp_dropalias](../../relational-databases/system-stored-procedures/sp-dropalias-transact-sql.md) (veraltet) |[sys.sp_drop_trusted_assembly]( sys-sp-drop-trusted-assembly-transact-sql.md) |
|[Sp_dropapprole](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md) (veraltet) |[sp_droplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md) |
|[Sp_droplogin](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md) (veraltet) |[Sp_dropremotelogin](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md) (veraltet) |
|[Sp_droprole](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md) (veraltet) |[Sp_droprolemember](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) (veraltet) |
|[sp_dropserver](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md) |[Sp_dropsrvrolemember](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md) (veraltet) |
|[Sp_dropuser](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md) (veraltet) |[Sp_grantdbaccess](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md) (veraltet) |
|[Sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md) (veraltet) |[sp_helpdbfixedrole](../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md) |
|[sp_helplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-helplinkedsrvlogin-transact-sql.md) |[sp_helplogins](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md) |
|[sp_helpntgroup](../../relational-databases/system-stored-procedures/sp-helpntgroup-transact-sql.md) |[Sp_helpremotelogin](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md) (veraltet) |
|[sp_helprole](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md) |[sp_helprolemember](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) |
|[Sp_helprotect](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md) (veraltet) |[sp_helpsrvrole](../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md) |
|[sp_helpsrvrolemember](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md) |[Sp_helpuser](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md) (veraltet) |
|[sp_migrate_user_to_contained](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)|[sp_MShasdbaccess](../../relational-databases/system-stored-procedures/sp-mshasdbaccess-transact-sql.md) |
|[Sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md) (veraltet)|[sp_refresh_parameter_encryption](../../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) |
|[Sp_remoteoption](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md) (veraltet)|[Sp_revokedbaccess](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md) (veraltet) |
|[Sp_revokelogin](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md) (veraltet)|[sp_setapprole](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md) |
|[Sp_srvrolepermission](../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md) (veraltet)|[sp_testlinkedserver](../../relational-databases/system-stored-procedures/sp-testlinkedserver-transact-sql.md) |
|[sp_unsetapprole](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md) |[sp_validatelogins](../../relational-databases/system-stored-procedures/sp-validatelogins-transact-sql.md) |
|[sp_xp_cmdshell_proxy_account](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md) | |

 
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
