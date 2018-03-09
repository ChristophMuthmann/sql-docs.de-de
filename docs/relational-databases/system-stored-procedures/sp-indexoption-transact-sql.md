---
title: Sp_indexoption (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_indexoption
- sp_indexoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_indexoption
ms.assetid: 75f836be-d322-4a53-a45d-25bee6b42a52
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8b5b63c7f76695853ab216aee1aaab63a3139cc2
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="spindexoption-transact-sql"></a>sp_indexoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Legt Werte für Sperrenoptionen für benutzerdefinierte gruppierte und nicht gruppierte Indizes oder Tabellen ohne gruppierten Index fest.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] wählt automatisch zwischen Sperren auf Seitenebene, Zeilenebene und Tabellenebene aus. Sie müssen diese Optionen nicht manuell festlegen. **Sp_indexoption** für erfahrene Benutzer, die mit Bestimmtheit wissen, der immer ein bestimmter Typ von Sperre ist die entsprechende bereitgestellt wird.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]Verwenden Sie stattdessen [ALTER INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-index-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_indexoption [ @IndexNamePattern = ] 'table_or_index_name'   
    , [ @OptionName = ] 'option_name'   
    , [ @OptionValue = ] 'value'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@IndexNamePattern=**] **"***Table_or_index_name***"**  
 Der qualifizierte oder nicht qualifizierte Name einer benutzerdefinierten Tabelle oder eines benutzerdefinierten Indexes. *Table_or_index_name* ist **nvarchar(1035)**, hat keinen Standardwert. Anführungszeichen sind nur erforderlich, wenn ein qualifizierter Index- oder Tabellenname angegeben wird. Bei Angabe eines voll gekennzeichneten Tabellennamens (einschließlich eines Datenbanknamens) muss der Datenbankname der Name der aktuellen Datenbank sein. Wenn ein Tabellenname ohne Index angegeben wird, wird der angegebene Optionswert für alle Indizes dieser Tabelle und für die Tabelle selbst, falls kein gruppierter Index vorhanden ist, festgelegt.  
  
 [  **@OptionName =**] **"***Option_name***"**  
 Ein Indexoptionsname. *Option_name* ist **varchar(35)**, hat keinen Standardwert. *Option_name* kann einen der folgenden Werte aufweisen.  
  
|value|Description|  
|-----------|-----------------|  
|**AllowRowLocks**|Mit TRUE sind Zeilensperren beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Zeilensperren verwendet werden. Mit FALSE werden keine Zeilensperren verwendet. Der Standardwert ist TRUE.|  
|**AllowPageLocks**|Mit TRUE sind Seitensperren beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Seitensperren verwendet werden. Mit FALSE werden keine Seitensperren verwendet. Der Standardwert ist TRUE.|  
|**DisAllowRowLocks**|Mit TRUE werden keine Zeilensperren verwendet. Mit FALSE sind Zeilensperren beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Zeilensperren verwendet werden.|  
|**DisAllowPageLocks**|Mit TRUE werden keine Seitensperren verwendet. Mit FALSE sind Seitensperren beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Seitensperren verwendet werden.|  
  
 [  **@OptionValue =**] **"***Wert***"**  
 Gibt an, ob die *Option_name* Einstellung ist aktiviert (TRUE, ON, Yes oder 1) oder deaktiviert (FALSE, OFF, No oder 0). *Wert* ist **varchar(12)**, hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder größer als 0 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 XML-Indizes werden nicht unterstützt. Wenn Sie einen XML-Index angeben oder einen Tabellennamen ohne Indexnamen angeben und die Tabelle einen XML-Index enthält, wird für die Anweisung ein Fehler gemeldet. Verwenden Sie zum Festlegen dieser Optionen [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) stattdessen.  
  
 Verwenden Sie zum Anzeigen der aktuellen Zeilen- und Seitensperren Eigenschaften [INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md) oder [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) -Katalogsicht angezeigt.  
  
-   Zeilen-, Seiten- und Sperren auf Tabellenebene sind zulässig, wenn der Zugriff auf den Index bei **AllowRowLocks** = "true" oder **DisAllowRowLocks** = "false", und **AllowPageLocks** = "true" oder  **DisAllowPageLocks** = "false". Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] wählt die geeignete Sperre aus und kann die Sperre von einer Zeilen- oder Seitensperre auf eine Tabellensperre ausweiten.  
  
 Nur eine Sperre auf Tabellenebene ist zulässig, wenn der Zugriff auf den Index bei **AllowRowLocks** = FALSE oder **DisAllowRowLocks** = "true" und **AllowPageLocks** = FALSE oder  **DisAllowPageLocks** = "true".  
  
 Wenn ein Tabellenname ohne Index angegeben wird, werden die Einstellungen auf alle Indizes dieser Tabelle angewendet. Wenn die zugrunde liegende Tabelle keinen gruppierten Index aufweist (d. h., es handelt sich um einen Heap), werden die Einstellungen wie folgt angewendet:  
  
-   Wenn **AllowRowLocks** oder **DisAllowRowLocks** werden auf "true" oder "false" festgelegt, wird die Einstellung, die dem Heap angewendet, und alle zugehörigen nicht gruppierten Indizes.  
  
-   Wenn **AllowPageLocks** Option auf "true" festgelegt ist oder **DisAllowPageLocks** festgelegt ist auf "false", die Einstellung angewendet wird, auf den Heap und alle zugehörigen nicht gruppierten Indizes.  
  
-   Wenn **AllowPageLocks** Option ist "false" festgelegt oder **DisAllowPageLocks** ist auf "true" festgelegt, wird vollständig die Einstellung, die nicht gruppierten Indizes angewendet. Das heißt, alle Seitensperren sind für die nicht gruppierten Indizes nicht zulässig. Auf dem Heap sind nur freigegebene Sperren (S), Updatesperren (U) und exklusive Sperren (X) für die Seite nicht zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] kann weiterhin eine beabsichtigte Seitensperre (IS, IU oder IX) für interne Zwecke abrufen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-setting-an-option-on-a-specific-index"></a>A. Festlegen einer Option auf einen bestimmten Index  
 Im folgende Beispiel lässt Seitensperren nicht zu, auf die `IX_Customer_TerritoryID` index für die `Customer` Tabelle.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_indexoption N'Sales.Customer.IX_Customer_TerritoryID',  
    N'disallowpagelocks', TRUE;  
```  
  
### <a name="b-setting-an-option-on-all-indexes-on-a-table"></a>B. Festlegen einer Option auf alle Indizes in einer Tabelle  
 Im folgenden Beispiel werden Zeilensperren für alle Indizes der `Product`-Tabelle nicht zugelassen. Die `sys.indexes`-Katalogsicht wird vor und nach dem Ausführen der gespeicherten Prozedur `sp_indexoption` abgefragt, um die Ergebnisse der Anweisung anzuzeigen.  
  
```sql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
-- Set the disallowrowlocks option on the Product table.   
EXEC sp_indexoption N'Production.Product',  
    N'disallowrowlocks', TRUE;  
GO  
--Verify the row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
```  
  
### <a name="c-setting-an-option-on-a-table-with-no-clustered-index"></a>C. Festlegen einer Option für eine Tabelle ohne gruppierten Index  
 Im folgenden Beispiel werden Seitensperren für eine Tabelle ohne gruppierten Index (ein Heap) nicht zugelassen. Die `sys.indexes` -Katalogsicht wird abgefragt, vor und nach der `sp_indexoption` Prozedur wird ausgeführt, um die Ergebnisse der Anweisung anzuzeigen.  
  
```sql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options of the table.   
SELECT OBJECT_NAME (object_id) AS [Table], type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
-- Set the disallowpagelocks option on the table.   
EXEC sp_indexoption DatabaseLog,  
    N'disallowpagelocks', TRUE;  
GO  
--Verify the row and page lock settings of the table.  
SELECT OBJECT_NAME (object_id) AS [Table], allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
