---
title: DROP VIEW (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_VIEW_TSQL
- DROP VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- dropping views
- DROP VIEW statement
- deleting views
- indexed views [SQL Server], removing
- views [SQL Server], removing
- removing views
ms.assetid: 03cea355-e39c-46e1-b7db-8832038669dd
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8dedeff21f56659d0cc55eef2d133a1ecbe0f63e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-view-transact-sql"></a>DROP VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entfernt eine oder mehrere Sichten aus der aktuellen Datenbank. DROP VIEW kann in indizierten Sichten ausgeführt werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP VIEW [ IF EXISTS ] [ schema_name . ] view_name [ ...,n ] [ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP VIEW [ schema_name . ] view_name   
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *IF VORHANDEN IST*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]). |  
  
 Bedingt löscht die Ansicht nur, wenn sie bereits vorhanden ist.  
  
 *schema_name*  
 Ist der Name des Schemas, zu dem die Sicht gehört.  
  
 *view_name*  
 Ist der Name der zu entfernenden Sicht.  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie eine Sicht löschen, werden die Definition der Sicht sowie weitere Informationen zur Sicht aus dem Systemkatalog entfernt. Alle Berechtigungen für die Sicht werden ebenfalls gelöscht.  
  
 Eine mithilfe von DROP TABLE gelöschte Sicht in einer Tabelle muss explizit mit DROP VIEW gelöscht werden.  
  
 Beim Ausführen in einer indizierten Sicht löscht DROP VIEW automatisch alle Indizes der Sicht. Verwenden Sie zum Anzeigen aller Indizes für eine Sicht [Sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md).  
  
 Wenn eine Abfrage über eine Sicht durchgeführt wird, überprüft [!INCLUDE[ssDE](../../includes/ssde-md.md)], ob alle Datenbankobjekte, auf die in der Anweisung verwiesen wird, vorhanden sind, ob sie im Kontext der Anweisung gültig sind und ob Datenänderungsanweisungen gegen die Regeln der Datenintegrität verstoßen. Schlägt eine Überprüfung fehl, wird eine Fehlermeldung zurückgegeben. Andernfalls wird die Aktion in eine Aktion für die zugrunde liegende Tabelle bzw. Tabellen übersetzt. Haben sich die zugrunde liegenden Tabellen oder Sichten seit der ursprünglichen Erstellung der Sicht geändert, kann es hilfreich sein, die Sicht zu löschen und neu zu erstellen.  
  
 Weitere Informationen zum Bestimmen von Abhängigkeiten für eine bestimmte Sicht finden Sie unter [sql_dependencies &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md).  
  
 Weitere Informationen zum Anzeigen der Ansicht finden Sie unter [Sp_helptext &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert **Steuerelement** Berechtigung für die Sicht **ALTER** Berechtigung für das Schema, enthält die Sicht oder die Mitgliedschaft in der **Db_ddladmin** festen Serverrolle "".  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-drop-a-view"></a>A. Löschen Sie eine Sicht  
 Im folgenden Beispiel wird die `Reorder`-Sicht entfernt.  
  
```  
DROP VIEW dbo.Reorder ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Verwenden Sie &#40; Transact-SQL &#41;](../../t-sql/language-elements/use-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
 

