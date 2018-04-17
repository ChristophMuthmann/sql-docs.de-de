---
title: Sp_table_privileges (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_table_privileges
- sp_table_privileges_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_table_privileges
ms.assetid: 0512e688-4fc0-4557-8dc8-016672c1e3fe
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2eb872a8ca079bbde96ad3667d687618cba7414a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sptableprivileges-transact-sql"></a>sp_table_privileges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Liste der Tabellenberechtigungen (beispielsweise INSERT, DELETE, UPDATE, SELECT, REFERENCES) für die angegebene Tabelle oder Tabellen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_table_privileges [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @table_name=] '*Table_name*"  
 Die Tabelle zum Zurückgeben von Kataloginformationen. *TABLE_NAME* ist **Nvarchar (**384**)**, hat keinen Standardwert. Mustervergleiche mit Platzhalterzeichen werden unterstützt.  
  
 [ @table_owner=] '*Table_owner*"  
 Der Tabellenbesitzer für die Tabelle zum Zurückgeben von Kataloginformationen. *Table_owner*ist **Nvarchar (**384**)**, hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden unterstützt. Wenn der Besitzer nicht angegeben ist, werden die Standardregeln für die Sichtbarkeit von Tabellen des zugrunde liegenden DBMS angewendet.  
  
 Wenn der aktuelle Benutzer diese Tabelle mit dem angegebenen Namen besitzt, werden die Spalten einer Tabelle zurückgegeben. Wenn *Besitzer* nicht angegeben wird und der aktuelle Benutzer keine Tabelle mit dem angegebenen *Namen*, sucht Sie dieses Verfahren für eine Tabelle mit dem angegebenen *Table_name* im Besitz der der Datenbankbesitzer. Falls vorhanden, werden die Spalten dieser Tabelle zurückgegeben.  
  
 [ @table_qualifier=] '*Table_qualifier*"  
 Der Name des Tabellenqualifizierers. *TABLE_QUALIFIER* ist **Sysname**, hat den Standardwert NULL. Verschiedene DBMS-Produkte unterstützen eine dreiteilige Namensgebung für Tabellen (*qualifier.owner.name*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt diese Spalte den Datenbanknamen dar. Bei anderen Produkten stellt sie den Servernamen der Datenbankumgebung für die Tabelle dar.  
  
 [ @fUsePattern=] '*fUsePattern*"  
 Bestimmt, ob der Unterstrich (_), Prozentzeichen (%), und Klammern ([oder]) Zeichen als Platzhalterzeichen interpretiert werden. Gültige Werte sind 0 (Mustervergleich ist deaktiviert) und 1 (Mustervergleich ist aktiviert). *fUsePattern* ist vom Datentyp **bit**. Der Standardwert ist 1.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|Tabelle der Name des Prozedurqualifizierers. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt diese Spalte den Datenbanknamen dar. Dieses Feld kann den Wert NULL annehmen.|  
|TABLE_OWNER|**sysname**|Name des Tabellenbesitzers. Dieses Feld gibt immer einen Wert zurück.|  
|table_name|**sysname**|Tabellenname. Dieses Feld gibt immer einen Wert zurück.|  
|GRANTOR|**sysname**|Der Datenbankbenutzername, der dem aufgelisteten GRANTEE Berechtigungen für TABLE_NAME erteilt hat. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist diese Spalte stets mit dem TABLE_OWNER identisch. Dieses Feld gibt immer einen Wert zurück. Zudem kann die GRANTOR-Spalte entweder der Datenbankbesitzer (TABLE_OWNER) oder ein Benutzer sein, dem der Datenbankbesitzer mithilfe der WITH GRANT OPTION-Klausel in der GRANT-Anweisung die Berechtigung erteilt hat.|  
|GRANTEE|**sysname**|Der Datenbank-Benutzername, dem vom aufgeführten GRANTOR Berechtigungen für TABLE_NAME erteilt wurden. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], enthält diese Spalte immer einen Datenbankbenutzer aus der Ansicht sys.database_principalssystem. Dieses Feld gibt immer einen Wert zurück.|  
|PRIVILEGE|**sysname**|Eine der verfügbaren Tabellenberechtigungen. Tabellenberechtigungen können folgende Werte annehmen (bzw. auch andere Werte, die von der Datenquelle bei der Definition der Implementierung unterstützt werden):<br /><br /> SELECT = GRANTEE kann Daten aus einer oder mehreren Spalten abrufen.<br /><br /> INSERT = GRANTEE kann in einer oder mehreren Spalten Daten für neue Zeilen bereitstellen.<br /><br /> UPDATE = GRANTEE kann vorhandene Daten in einer oder mehreren Spalten ändern.<br /><br /> DELETE = GRANTEE kann Zeilen aus der Tabelle entfernen.<br /><br /> REFERENCES = der Berechtigte (GRANTEE) kann bei einer Primär-/Fremdschlüssel-Beziehung auf eine Spalte in einer Fremdschlüsseltabelle verweisen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Primär-/Fremdschlüsselbeziehungen über Tabelleneinschränkungen definiert.<br /><br /> Der dem GRANTEE durch ein bestimmtes Tabellenprivileg erteilte Aktionsbereich ist datenquellenabhängig. Beispielsweise kann der GRANTEE mit dem UPDATE-Privileg alle Spalten in einer Tabelle für eine Datenquelle aktualisieren, während er für eine andere Datenquelle nur die Spalten aktualisieren kann, für die der GRANTOR das UPDATE-Privileg besitzt.|  
|IS_GRANTABLE|**sysname**|Zeigt an, ob der GRANTEE anderen Benutzern Berechtigungen erteilen darf (oft als "Berechtigung mit Recht zum Erteilen" bezeichnet). Dieses Feld kann die Werte YES, NO oder NULL annehmen. Ein unbekannter Wert (oder NULL-Wert) verweist auf eine Datenquelle, für die die "Berechtigung mit Recht zum Erteilen" nicht anwendbar ist.|  
  
## <a name="remarks"></a>Hinweise  
 Die gespeicherte Prozedur sp_table_privileges entspricht SQLTablePrivileges in ODBC. Die zurückgegebenen Ergebnisse sind nach TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME und PRIVILEGE sortiert.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigung für das Schema.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Privileginformationen zu allen Tabellen zurückgegeben, deren Namen mit dem Wort `Contact` beginnen.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_table_privileges   
   @table_name = 'Contact%';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für Kataloginformationen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
