---
title: ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_AUDIT_SPECIFICATION_TSQL
- ALTER DATABASE AUDIT SPECIFICATION
- ALTER_DATABASE_AUDIT_TSQL
- ALTER DATABASE AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER DATABASE AUDIT SPECIFICATION statement
ms.assetid: 85f4e7e6-a330-4de0-9048-64f386ccc314
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 06d58a9ecce3175e021e7db484aeadbe41f3b372
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-audit-specification-transact-sql"></a>ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verändert ein Datenbank-Überwachungsspezifikationsobjekt mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit-Features. Weitere Informationen finden Sie unter [SQL Server Audit &#40;Datenbankmodul&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER DATABASE AUDIT SPECIFICATION audit_specification_name  
{  
    [ FOR SERVER AUDIT audit_name ]  
    [ { { ADD | DROP } (   
           { <audit_action_specification> | audit_action_group_name }   
                )   
      } [, ...n] ]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
<audit_action_specification>::=  
{  
      <action_specification>[ ,...n ] ON [ class :: ] securable   
     BY principal [ ,...n ]   
}  
  
```  
  
## <a name="arguments"></a>Argumente  
 *audit_specification_name*  
 Der Name der Überwachungsspezifikation.  
  
 *audit_name*  
 Der Name der Überwachung auf die diese Spezifikation angewendet wird.  
  
 *audit_action_specification*  
 Der Name von einem oder mehreren überwachbaren Aktionen auf Datenbankebene. Eine Liste der Überwachungsaktionsgruppen finden Sie unter [SQL Server Audit-Aktionsgruppen und-Aktionen](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
 *audit_action_group_name*  
 Name von einer oder mehreren Gruppen von überwachbaren Aktionen auf Datenbankebene. Eine Liste der Überwachungsaktionsgruppen finden Sie unter [SQL Server Audit-Aktionsgruppen und-Aktionen](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
 *Klasse*  
 Klassenname (falls anwendbar) auf dem sicherungsfähigen Element.  
  
 *sicherungsfähiges Element*  
 Tabelle, Sicht oder anderes sicherungsfähiges Element, auf das die Überwachungsaktion oder die Überwachungsaktionsgruppe angewendet werden soll. Weitere Informationen finden Sie unter [Securables](../../relational-databases/security/securables.md).  
  
 *Spalte*  
 Spaltenname (falls anwendbar) auf dem sicherungsfähigen Element.  
  
 *Prinzipal*  
 Name des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prinzipals, auf das die Überwachungsaktion oder die Überwachungsaktionsgruppe angewendet werden soll. Weitere Informationen finden Sie unter [Prinzipale &#40; Datenbankmodul &#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).  
  
 WITH **(** STATE **=** { ON | OFF } **)**  
 Aktiviert oder deaktiviert das Sammeln von Datensätzen durch die Überwachung für diese Überwachungsspezifikation. Statusänderungen der Überwachungsspezifikation müssen außerhalb einer Benutzertransaktion erfolgen und dürfen keine anderen Änderungen in derselben Anweisung enthalten, wenn der Übergang von ON nach OFF stattfindet.  
  
## <a name="remarks"></a>Hinweise  
 Datenbank-Überwachungsspezifikationen sind nicht sicherungsfähige Objekte, die sich in einer gegebenen Datenbank befinden. Sie müssen den Status einer Überwachungsspezifikation auf OFF festlegen, um Änderungen an einer Datenbank-Überwachungsspezifikation stellen festlegen. Wenn ALTER DATABASE AUDIT SPECIFICATION ausgeführt wird während eine Überwachung mit einer anderen Option als STATE=OFF aktiviert ist, erhalten Sie eine Fehlermeldung. Weitere Informationen finden Sie unter [tempdb Database](../../relational-databases/databases/tempdb-database.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer mit der Berechtigung ALTER ANY DATABASE AUDIT können Datenbanküberwachungsspezifikationen ändern und sie an eine beliebige Überwachung binden.  
  
 Nachdem eine datenbanküberwachungsspezifikation erstellt wurde, können sie von Prinzipalen mit die CONTROL SERVER oder Berechtigungen ALTER ANY DATABASE AUDIT, Sysadmin-Konto oder expliziten Zugriff auf die Überwachung verfügen Prinzipale angezeigt werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Datenbanküberwachungsspezifikation namens `HIPPA_Audit_DB_Specification` geändert, die die `SELECT`-Anweisungen des `dbo`-Benutzers für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Überwachung namens `HIPPA_Audit` überwacht.  
  
```  
ALTER DATABASE AUDIT SPECIFICATION HIPPA_Audit_DB_Specification  
FOR SERVER AUDIT HIPPA_Audit  
    ADD (SELECT  
         ON OBJECT::dbo.Table1  
         BY dbo)  
    WITH (STATE = ON);  
GO  
```  
  
 Ein vollständiges Beispiel zum Erstellen einer Überwachung finden Sie unter [SQL Server Audit &#40; Datenbankmodul &#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie die SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [Erstellen Sie die SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [Erstellen Sie DATABASE AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [Sys. fn_get_audit_file &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [Sys. server_audits &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [Sys. server_file_audits &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [server_audit_specifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [server_audit_specification_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [database_audit_specifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [database_audit_specification_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [dm_server_audit_status &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [dm_audit_actions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [Erstellen einer Serverüberwachung und einer Serverüberwachungsspezifikation](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
