---
title: Sp_column_privileges (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_TSQL
- sp_column_privileges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges
ms.assetid: a3784301-2517-4b1d-bbd9-47404483fad0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f930dc96633f526259dccf89f7fb592a4f9caf10
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spcolumnprivileges-transact-sql"></a>sp_column_privileges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu Spaltenprivilegien für eine einzelne Tabelle in der aktuellen Umgebung zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_column_privileges [ @table_name = ] 'table_name'   
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @column_name = ] 'column' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @table_name=] '*Table_name*"  
 Die Tabelle zum Zurückgeben von Kataloginformationen. *TABLE_NAME* ist **Sysname**, hat keinen Standardwert. Mustervergleiche mit Platzhalterzeichen werden nicht unterstützt.  
  
 [ @table_owner=] '*Table_owner*"  
 Der Besitzer der Tabelle, die zum Zurückgeben von Kataloginformationen verwendet wird. *Table_owner* ist **Sysname**, hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden nicht unterstützt. Wenn *Table_owner* nicht angegeben wird, gelten die Standardregeln für die Sichtbarkeit von Tabellen des zugrunde liegenden Datenbank-Managementsystem (DBMS).  
  
 Wenn der aktuelle Benutzer eine Tabelle mit dem angegebenen Namen besitzt, werden die Spalten dieser Tabelle zurückgegeben. Wenn *Table_owner* nicht angegeben wird und der aktuelle Benutzer keine Tabelle mit dem angegebenen *Table_name*, sp_column nach für eine Tabelle mit dem angegebenen *Table_name* gehören dem Datenbankbesitzer. Sofern eine solche Tabelle vorhanden ist, werden die Spalten dieser Tabelle zurückgegeben.  
  
 [ @table_qualifier=] '*Table_qualifier*"  
 Der Name des Tabellenqualifizierers. *TABLE_QUALIFIER* ist *Sysname*, hat den Standardwert NULL. Verschiedene DBMS-Produkte unterstützen eine dreiteilige Namensgebung für Tabellen (*Qualifizierer***.** *Besitzer***.** *Namen*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt diese Spalte den Datenbanknamen dar. Bei anderen Produkten stellt sie den Servernamen der Datenbankumgebung für die Tabelle dar.  
  
 [ @column_name=] '*Spalte*"  
 Eine einzelne Spalte, die verwendet wird, wenn nur eine Spalte mit Kataloginformationen empfangen wird. *Spalte* ist **Nvarchar (**384**)**, hat den Standardwert NULL. Wenn *Spalte* ist nicht angegeben ist, werden alle Spalten zurückgegeben. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], *Spalte* dar, der den Namen der Spalte in der sys.columns-Tabelle aufgeführt. *Spalte* kann mithilfe von Platzhalterzeichen Mustervergleich DBMS-spezifische Platzhalterzeichen enthalten. Für eine optimale Interoperabilität sollte der Gatewayclient nur einen ISO-Standardmustervergleich voraussetzen (die Platzhalterzeichen % und _).  
  
## <a name="result-sets"></a>Resultsets  
 Sp_column_privileges entspricht SQLColumnPrivileges in ODBC. Die zurückgegebenen Ergebnisse sind nach den Spalten TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME, COLUMN_NAME und PRIVILEGE sortiert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|Tabelle der Name des Prozedurqualifizierers. Dieses Feld kann den Wert NULL annehmen.|  
|TABLE_OWNER|**sysname**|Name des Tabellenbesitzers. Dieses Feld gibt immer einen Wert zurück.|  
|TABLE_NAME|**sysname**|Tabellenname. Dieses Feld gibt immer einen Wert zurück.|  
|COLUMN_NAME|**sysname**|Der Name der Spalte für jede Spalte des zurückgegebenen TABLE_NAME. Dieses Feld gibt immer einen Wert zurück.|  
|GRANTOR|**sysname**|Der Datenbank-Benutzername, der dem als GRANTEE aufgeführten Prinzipal Berechtigungen für die mit COLUMN_NAME angegebene Spalte erteilt hat. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist diese Spalte stets mit dem TABLE_OWNER identisch. Dieses Feld gibt immer einen Wert zurück.<br /><br /> Die GRANTOR-Spalte kann entweder der Datenbankbesitzer (TABLE_OWNER) oder ein anderer Benutzer sein, dem die Berechtigungen vom Datenbankbesitzer mithilfe der WITH GRANT OPTION-Klausel in der GRANT-Anweisung erteilt wurden.|  
|GRANTEE|**sysname**|Der Datenbank-Benutzername, dem der als GRANTOR aufgeführte Prinzipal Berechtigungen für die mit COLUMN_NAME angegebene Spalte erteilt hat. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält diese Spalte immer einen Datenbankbenutzer aus der sysusers-Tabelle. Dieses Feld gibt immer einen Wert zurück.|  
|PRIVILEGE|**Varchar (**32**)**|Eine der verfügbaren Spaltenberechtigungen. Spaltenberechtigungen können folgende Werte annehmen (oder auch andere Werte, die von der Datenquelle bei der Definition der Implementierung unterstützt werden):<br /><br /> SELECT = der Berechtigte (GRANTEE) kann Daten für die Spalten abrufen.<br /><br /> INSERT = der Berechtigte (GRANTEE) kann Daten für diese Spalten bereitstellen, wenn neue Zeilen (von diesem GRANTEE) in die Tabelle eingefügt werden.<br /><br /> UPDATE = der Berechtigte (GRANTEE) kann vorhandene Daten in der Spalte ändern.<br /><br /> REFERENCES = der Berechtigte (GRANTEE) kann bei einer Primär-/Fremdschlüssel-Beziehung auf eine Spalte in einer Fremdschlüsseltabelle verweisen. Primär-/Fremdschlüssel-Beziehungen werden mithilfe von Tabelleneinschränkungen definiert.|  
|IS_GRANTABLE|**Varchar (**3**)**|Zeigt an, ob der Berechtigte (GRANTEE) anderen Benutzern Berechtigungen erteilen darf (bekannt als "Berechtigung mit Recht zum Erteilen"). Dieses Feld kann die Werte YES, NO oder NULL annehmen. Ein unbekannter Wert (oder NULL-Wert) verweist auf eine Datenquelle, für die die "Berechtigung mit Recht zum Erteilen" nicht zutreffend ist.|  
  
## <a name="remarks"></a>Hinweise  
 Bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Berechtigungen mit der GRANT-Anweisung erteilt und mit der REVOKE-Anweisung aufgehoben.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigung für das Schema.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zum Spaltenprivileg für eine bestimmte Spalte zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_column_privileges @table_name = 'Employee'   
    ,@table_owner = 'HumanResources'  
    ,@table_qualifier = 'AdventureWorks2012'  
    ,@column_name = 'SalariedFlag';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
