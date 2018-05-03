---
title: HAS_PERMS_BY_NAME (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- HAS_PERMS_BY_NAME
- HAS_PERMS_BY_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- current permission status
- checking permission status
- verifying permission status
- testing permissions
- HAS_PERMS_BY_NAME function
ms.assetid: eaf8cc82-1047-4144-9e77-0e1095df6143
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4189de226a768914621be0a99d6d2a5b757c7236
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="haspermsbyname-transact-sql"></a>HAS_PERMS_BY_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Wertet die gültige Berechtigung des aktuellen Benutzers für ein sicherungsfähiges Element aus. Eine verwandte Funktion ist [fn_my_permissions](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HAS_PERMS_BY_NAME ( securable , securable_class , permission    
    [ , sub-securable ] [ , sub-securable_class ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *securable*  
 Der Name des sicherungsfähigen Elements. Wenn das sicherungsfähige Element der Server selbst ist, sollte dieser Wert auf NULL festgelegt werden. *securable* ist ein Skalarausdruck vom Typ **sysname**. Es gibt keinen Standardwert.  
  
 *securable_class*  
 Der Name der Klasse des sicherungsfähigen Elements, für das die Berechtigung getestet wird. *securable_class* ist ein Skalarausdruck vom Typ **nvarchar(60)**.  
  
 In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] muss das securable_class-Argument auf einen der folgenden Werte festgelegt werden: **DATABASE**, **OBJECT**, **ROLE**, **SCHEMA** oder **USER**.  
  
 *permission*  
 Ein Skalarausdruck ungleich NULL vom Datentyp **sysname**, der den zu überprüfenden Berechtigungsnamen darstellt. Es gibt keinen Standardwert. Der Berechtigungsname ANY ist ein Platzhalter.  
  
 *sub-securable*  
 Ein optionaler Skalarausdruck vom Typ **sysname**, der den Namen der sicherungsfähigen untergeordneten Entität darstellt, mit der die Berechtigung getestet wird. Die Standardeinstellung ist NULL.  
  
> [!NOTE]  
>  In den Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dürfen in untergeordneten sicherungsfähigen Elementen keine eckigen Klammern in der Form **'[***sub name***]'** verwendet werden. Verwenden Sie stattdessen **'***sub name***'**.  
  
 *sub-securable_class*  
 Ein optionaler Skalarausdruck vom Datentyp **nvarchar(60)**, der die Klasse der sicherungsfähigen untergeordneten Entität darstellt, für die die Berechtigung getestet wird. Die Standardeinstellung ist NULL.  
  
 Das sub-securable_class-Argument ist in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] nur gültig, wenn das securable_class-Argument auf **OBJECT** festgelegt ist. Wenn das securable_class-Argument auf **OBJECT** festgelegt ist, muss das sub-securable_class-Argument auf **COLUMN** festgelegt werden.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
 Gibt NULL zurück, wenn die Abfrage einen Fehler erzeugt.  
  
## <a name="remarks"></a>Remarks  
 Diese integrierte Funktion testet, ob der aktuelle Prinzipal eine bestimmte gültige Berechtigung für ein bestimmtes sicherungsfähiges Element aufweist. HAS_PERMS_BY_NAME gibt 1 zurück, wenn der Benutzer über eine gültige Berechtigung für das sicherungsfähige Element verfügt, 0, wenn der Benutzer über keine gültige Berechtigung für das sicherungsfähige Element verfügt, und NULL, wenn die sicherungsfähige Klasse oder die Berechtigung nicht gültig ist. Bei einer gültigen Berechtigung kann es sich um Folgendes handeln:  
  
-   Eine Berechtigung, die dem Prinzipal direkt gewährt und nicht verweigert wurde.  
  
-   Eine Berechtigung, die durch eine Berechtigung auf höherer Ebene des Prinzipals impliziert wird und nicht verweigert wird.  
  
-   Eine Berechtigung, die einer Rolle oder Gruppe erteilt wird, der der Prinzipal als Mitglied angehört, und nicht verweigert wird.  
  
-   Eine Berechtigung einer Rolle oder Gruppe, der der Prinzipal als Mitglied angehört, und die nicht verweigert wird.  
  
 Die Berechtigungsauswertung erfolgt immer im Sicherheitskontext des Aufrufers. Wenn Sie bestimmen möchten, ob ein anderer Benutzer eine gültige Berechtigung aufweist, benötigt der Aufrufer die IMPERSONATE-Berechtigung für diesen Benutzer.  
  
 Für Entitäten auf Schemaebene werden ein-, zwei- oder dreiteilige Namen akzeptiert, die ungleich NULL sind. Für Entitäten auf Datenbankebene ist ein einteiliger Name zulässig, wobei ein NULL-Wert für "aktuelle Datenbank" steht. Für den Server selbst ist ein NULL-Wert (steht für "aktueller Server") erforderlich. Mit dieser Funktion können keine Berechtigungen auf einem Verbindungsserver oder für einen Windows-Benutzer überprüft werden, für den kein Prinzipal auf Serverebene erstellt wurde.  
  
 Die folgende Abfrage gibt eine Liste integrierter sicherungsfähiger Klassen zurück:  
  
```  
SELECT class_desc FROM sys.fn_builtin_permissions(default);  
```  
  
 Die folgenden Sortierungen werden verwendet:  
  
-   Aktuelle Datenbanksortierung: auf Datenbankebene sicherungsfähige Elemente einschließlich sicherungsfähiger Elemente, die nicht in einem Schema enthalten sind; ein- oder zweiteilige sicherungsfähige Elemente mit Schemabereich; Zieldatenbanken, falls ein dreiteiliger Name verwendet wird.  
  
-   master-Datenbanksortierung: auf Serverebene sicherungsfähige Elemente.  
  
-   'ANY' wird für Überprüfungen auf Spaltenebene nicht unterstützt. Sie müssen die entsprechende Berechtigung angeben.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-do-i-have-the-server-level-view-server-state-permission"></a>A. Habe ich die VIEW SERVER STATE-Berechtigung auf Serverebene?  
  
**Gilt für** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT HAS_PERMS_BY_NAME(null, null, 'VIEW SERVER STATE');  
```  
  
### <a name="b-am-i-able-to-impersonate-server-principal-ps"></a>B. Kann ich die IMPERSONATE-Anweisung für den Ps-Serverprinzipal ausführen?  
  
**Gilt für** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT HAS_PERMS_BY_NAME('Ps', 'LOGIN', 'IMPERSONATE');  
```  
  
### <a name="c-do-i-have-any-permissions-in-the-current-database"></a>C. Habe ich Berechtigungen in der aktuellen Datenbank?  
  
```  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'ANY');  
```  
  
### <a name="d-does-database-principal-pd-have-any-permission-in-the-current-database"></a>D. Hat der Pd-Datenbankprinzipal Berechtigungen in der aktuellen Datenbank?  
 Angenommen, der Aufrufer hat die IMPERSONATE-Berechtigung für den `Pd`-Prinzipal.  
  
```  
EXECUTE AS user = 'Pd'  
GO  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'ANY');  
GO  
REVERT;  
GO  
```  
  
### <a name="e-can-i-create-procedures-and-tables-in-schema-s"></a>E. Kann ich Prozeduren und Tabellen im S-Schema erstellen?  
 Für das folgende Beispiel ist die `ALTER`-Berechtigung in `S` und die `CREATE PROCEDURE`-Berechtigung für die Datenbank und entsprechend für Tabellen erforderlich.  
  
```  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'CREATE PROCEDURE')  
    & HAS_PERMS_BY_NAME('S', 'SCHEMA', 'ALTER') AS _can_create_procs,  
    HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'CREATE TABLE') &  
    HAS_PERMS_BY_NAME('S', 'SCHEMA', 'ALTER') AS _can_create_tables;  
```  
  
### <a name="f-which-tables-do-i-have-select-permission-on"></a>F. Für welche Tabellen habe ich die SELECT-Berechtigung?  
  
```  
SELECT HAS_PERMS_BY_NAME  
(QUOTENAME(SCHEMA_NAME(schema_id)) + '.' + QUOTENAME(name),   
    'OBJECT', 'SELECT') AS have_select, * FROM sys.tables  
```  
  
### <a name="g-do-i-have-insert-permission-on-the-salesperson-table-in-adventureworks2012"></a>G. Verfüge ich über die INSERT-Berechtigung für die SalesPerson-Tabelle in AdventureWorks2012?  
 Im folgenden Beispiel wird von `AdventureWorks2012` als aktuellem Datenbankkontext ausgegangen und ein zweiteiliger Name verwendet.  
  
```  
SELECT HAS_PERMS_BY_NAME('Sales.SalesPerson', 'OBJECT', 'INSERT');  
```  
  
 Im folgenden Beispiel wird von keinem aktuellen Datenbankkontext ausgegangen und ein dreiteiliger Name verwendet.  
  
```  
SELECT HAS_PERMS_BY_NAME('AdventureWorks2012.Sales.SalesPerson',   
    'OBJECT', 'INSERT');  
```  
  
### <a name="h-which-columns-of-table-t-do-i-have-select-permission-on"></a>H. Für welche Spalten der T-Tabelle habe ich die SELECT-Berechtigung?  
  
```  
SELECT name AS column_name,   
    HAS_PERMS_BY_NAME('T', 'OBJECT', 'SELECT', name, 'COLUMN')   
    AS can_select   
    FROM sys.columns AS c   
    WHERE c.object_id=object_id('T');  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [Berechtigungshierarchie &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
  
  
