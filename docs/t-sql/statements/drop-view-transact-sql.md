---
title: DROP VIEW (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4ed2dc16e20179981985cc52812c8dbc44c0624b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="drop-view-transact-sql"></a>DROP VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
 *IF EXISTS*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]).|  
  
 Löscht die Sicht nur, wenn diese bereits vorhanden ist.  
  
 *schema_name*  
 Ist der Name des Schemas, zu dem die Sicht gehört.  
  
 *view_name*  
 Ist der Name der zu entfernenden Sicht.  
  
## <a name="remarks"></a>Remarks  
 Wenn Sie eine Sicht löschen, werden die Definition der Sicht sowie weitere Informationen zur Sicht aus dem Systemkatalog entfernt. Alle Berechtigungen für die Sicht werden ebenfalls gelöscht.  
  
 Eine mithilfe von DROP TABLE gelöschte Sicht in einer Tabelle muss explizit mit DROP VIEW gelöscht werden.  
  
 Beim Ausführen in einer indizierten Sicht löscht DROP VIEW automatisch alle Indizes der Sicht. Verwenden Sie [sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md), um alle Indizes in einer Sicht anzuzeigen.  
  
 Wenn eine Abfrage über eine Sicht durchgeführt wird, überprüft [!INCLUDE[ssDE](../../includes/ssde-md.md)], ob alle Datenbankobjekte, auf die in der Anweisung verwiesen wird, vorhanden sind, ob sie im Kontext der Anweisung gültig sind und ob Datenänderungsanweisungen gegen die Regeln der Datenintegrität verstoßen. Schlägt eine Überprüfung fehl, wird eine Fehlermeldung zurückgegeben. Andernfalls wird die Aktion in eine Aktion für die zugrunde liegende Tabelle bzw. Tabellen übersetzt. Haben sich die zugrunde liegenden Tabellen oder Sichten seit der ursprünglichen Erstellung der Sicht geändert, kann es hilfreich sein, die Sicht zu löschen und neu zu erstellen.  
  
 Weitere Informationen zum Bestimmen von Abhängigkeiten für einen bestimmten Trigger finden Sie unter [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md).  
  
 Weitere Informationen zum Anzeigen des Sichttexts finden Sie unter [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **CONTROL**-Berechtigung für die Sicht, die **ALTER**-Berechtigung für das Schema, das die Sicht enthält, oder die Mitgliedschaft in der festen Serverrolle **db_ddladmin**.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-drop-a-view"></a>A. Löschen einer Sicht  
 Im folgenden Beispiel wird die `Reorder`-Sicht entfernt.  
  
```  
DROP VIEW dbo.Reorder ;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
 
