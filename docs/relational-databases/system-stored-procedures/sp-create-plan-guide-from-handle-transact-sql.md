---
title: Sp_create_plan_guide_from_handle (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_create_plan_guide_from_handle_TSQL
- sp_create_plan_guide_from_handle
dev_langs: TSQL
helpviewer_keywords: sp_create_plan_guide_from_handle
ms.assetid: 02cfb76f-a0f9-4b42-a880-1c3e7d64fe41
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e61fdefeb38dcf011241cecaadd525b0a527b30
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spcreateplanguidefromhandle-transact-sql"></a>sp_create_plan_guide_from_handle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine oder mehrere Planhinweislisten aus einem Abfrageplan im Plancache. Sie können diese gespeicherte Prozedur verwenden, um sicherzustellen, dass der Abfrageoptimierer einen bestimmten Abfrageplan für eine bestimmte Abfrage verwendet. Weitere Informationen zu Planhinweislisten finden Sie unter [Planhinweislisten](../../relational-databases/performance/plan-guides.md).  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_create_plan_guide_from_handle [ @name = ] N'plan_guide_name'  
    , [ @plan_handle = ] plan_handle  
    , [ [ @statement_start_offset = ] { statement_start_offset | NULL } ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @name =] N'*Plan_guide_name*"  
 Der Name der Planhinweisliste. Die Gültigkeit der Namen von Planhinweislisten beschränkt sich auf die aktuelle Datenbank. *Plan_guide_name* muss den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md) und kann nicht gestartet werden mit dem Nummernzeichen (#). Die maximale Länge des *Plan_guide_name* beträgt 124 Zeichen.  
  
 [ @plan_handle =] *Plan_handle*  
 Identifiziert einen Batch im Plancache. *plan_handle* ist **varbinary(64)** *Plan_handle* abgerufen werden kann, aus der [Sys. dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) -verwaltungssicht.  
  
 [ @statement_start_offset =] { *Statement_start_offset* | NULL}]  
 Identifiziert die Anfangsposition der Anweisung innerhalb des Batches des angegebenen *Plan_handle*. *Statement_start_offset* ist **Int**, hat den Standardwert NULL.  
  
 Der anweisungsoffset entspricht der Spalte Statement_start_offset in der [Sys. dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) -verwaltungssicht.  
  
 Wenn NULL angegeben ist oder kein Anweisungsoffset angegeben ist, wird eine Planhinweisliste für jede Anweisung im Batch unter Verwendung des Abfrageplans für das angegebene Planhandle erstellt. Die daraus resultierenden Planhinweislisten entsprechen den Planhinweislisten, die mit dem USE PLAN-Abfragehinweis die Verwendung eines bestimmten Plans erzwingen.  
  
## <a name="remarks"></a>Hinweise  
 Planhinweislisten können nicht für alle Anweisungstypen erstellt werden. Wenn für eine Anweisung im Batch keine Planhinweisliste erstellt werden kann, ignoriert die gespeicherte Prozedur die Anweisung und fährt mit der nächsten Anweisung im Batch fort. Wenn eine Anweisung mehrfach im selben Batch vorkommt, wird der Plan für das letzte Vorkommen aktiviert, und die vorherigen Pläne für die Anweisung werden deaktiviert. Wenn in einer Planhinweisliste keine Anweisungen im Batch verwendet werden können, wird Fehler 10532 ausgegeben, und die Anweisung schlägt fehl. Es wird empfohlen, das Planhandle immer aus der dynamischen Verwaltungssicht sys.dm_exec_query_stats abzurufen, um das Auftreten dieses Fehlers zu verhindern.  
  
> [!IMPORTANT]  
>  sp_create_plan_guide_from_handle erstellt Planhinweislisten auf der Basis von Plänen, wie sie im Plancache angezeigt werden. Das bedeutet, dass der Batchtext, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen und XML-Showplan Zeichen für Zeichen (einschließlich aller an die Abfrage übergebenen Literalwerte) aus dem Plancache in die resultierende Planhinweisliste übertragen werden. Diese Textzeichenfolgen enthalten möglicherweise vertrauliche Informationen, die dann in den Metadaten der Datenbank gespeichert werden. Benutzer mit entsprechenden Berechtigungen können diese Informationen mithilfe der plan_guides-Katalogsicht anzeigen und die **Eigenschaften der Planhinweisliste** im Dialogfeld [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Um sicherzustellen, dass vertrauliche Informationen nicht über eine Planhinweisliste offen gelegt werden, wird empfohlen, die aus dem Plancache erstellten Planhinweislisten zu überprüfen.  
  
## <a name="creating-plan-guides-for-multiple-statements-within-a-query-plan"></a>Erstellen von Planhinweislisten für mehrere Anweisungen innerhalb eines Abfrageplans  
 sp_create_plan_guide_from_handle entfernt (wie sp_create_plan_guide) den Abfrageplan für den Zielbatch oder das Zielmodul aus dem Plancache. Dies geschieht, um sicherzustellen, dass alle Benutzer die neue Planhinweisliste verwenden. Beim Erstellen einer Planhinweisliste für mehrere Anweisungen innerhalb eines einzelnen Abfrageplans können Sie das Entfernen des Plans aus dem Cache verzögern, indem Sie alle Planhinweislisten in einer expliziten Transaktion erstellen. Bei Verwendung dieser Methode bleibt der Plan so lange im Cache, bis die Transaktion abgeschlossen ist und eine Planhinweisliste für jede angegebene Anweisung erstellt ist. Siehe Beispiel B.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung. Außerdem sind einzelne Berechtigungen für jede Planhinweisliste erforderlich, die unter Verwendung von sp_create_plan_guide_from_handle erstellt wird. Zum Erstellen einer Planhinweisliste vom Typ erfordert SERVEROBJEKT ALTER-Berechtigung für das Objekt verwiesen wird. Zum Erstellen einer Planhinweisliste vom Typ SQL oder TEMPLATE wird die ALTER-Berechtigung für die aktuelle Datenbank benötigt. Um den Typ der erstellten Planhinweislistentyp zu bestimmen, führen Sie die folgende Abfrage aus:  
  
```  
SELECT cp.plan_handle, sql_handle, st.text, objtype   
FROM sys.dm_exec_cached_plans AS cp  
JOIN sys.dm_exec_query_stats AS qs ON cp.plan_handle = qs.plan_handle  
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS st;  
```  
  
 Untersuchen Sie in der Zeile mit der Anweisung, für die Sie die Planhinweisliste erstellen, die `objtype`-Spalte im Resultset. Der Wert `Proc` gibt an, dass die Planhinweisliste den Typ OBJECT hat. Andere Werte, wie z. B. `AdHoc` oder `Prepared`, geben an, dass die Planhinweisliste den Typ SQL hat.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-plan-guide-from-a-query-plan-in-the-plan-cache"></a>A. Erstellen einer Planhinweisliste aus einem Abfrageplan im Plancache  
 Im folgenden Beispiel wird eine Planhinweisliste für eine einzelne SELECT-Anweisung erstellt, indem ein Abfrageplan aus dem Plancache angegeben wird. In diesem Beispiel wird zuerst eine einfache `SELECT`-Anweisung ausgeführt, für die die Planhinweisliste erstellt werden soll. Der Plan für diese Abfrage wird unter Verwendung der dynamischen Verwaltungssichten `sys.dm_exec_sql_text` und `sys.dm_exec_text_query_plan` untersucht. Anschließend wird die Planhinweisliste für die Abfrage erstellt, indem der Abfrageplan in dem Plancache angegeben wird, der der Abfrage zugeordnet ist. Die abschließende Anweisung in dem Beispiel überprüft, dass die Planhinweisliste vorhanden ist.  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT WorkOrderID, p.Name, OrderQty, DueDate  
FROM Production.WorkOrder AS w   
JOIN Production.Product AS p ON w.ProductID = p.ProductID  
WHERE p.ProductSubcategoryID > 4  
ORDER BY p.Name, DueDate;  
GO  
-- Inspect the query plan by using dynamic management views.  
SELECT * FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(sql_handle)  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset) AS qp  
WHERE text LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
GO  
-- Create a plan guide for the query by specifying the query plan in the plan cache.  
DECLARE @plan_handle varbinary(64);  
DECLARE @offset int;  
SELECT @plan_handle = plan_handle, @offset = qs.statement_start_offset  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS st  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset) AS qp  
WHERE text LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
  
EXECUTE sp_create_plan_guide_from_handle   
    @name =  N'Guide1',  
    @plan_handle = @plan_handle,  
    @statement_start_offset = @offset;  
GO  
-- Verify that the plan guide is created.  
SELECT * FROM sys.plan_guides  
WHERE scope_batch LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
GO  
```  
  
### <a name="b-creating-multiple-plan-guides-for-a-multistatement-batch"></a>B. Erstellen von mehreren Planhinweislisten für einen Batch mit mehreren Anweisungen  
 Im folgenden Beispiel wird eine Planhinweisliste für zwei Anweisungen innerhalb eines Batches mit mehreren Anweisungen erstellt. Die Planhinweislisten werden innerhalb einer expliziten Transaktion erstellt, damit der Abfrageplan für den Batch erst dann aus dem Plancache entfernt wird, nachdem die erste Planhinweisliste erstellt wurde. Im Beispiel wird zuerst ein Batch mit mehreren Anweisungen ausgeführt. Der Plan für den Batch wird unter Verwendung der dynamischen Verwaltungssichten untersucht. Beachten Sie, dass eine Zeile für jede Anweisung im Batch zurückgegeben wird. Anschließend wird eine Planhinweisliste für die erste und die dritte Anweisung in dem Batch durch Angabe des `@statement_start_offset`-Parameters erstellt. Die abschließende Anweisung in dem Beispiel überprüft, dass die Planhinweislisten vorhanden sind.  
  
 [!code-sql[PlanGuides#Create_From_Handle2](../../relational-databases/system-stored-procedures/codesnippet/tsql/sp-create-plan-guide-fro_1.sql)]  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Sys. dm_exec_query_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [Planhinweislisten](../../relational-databases/performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [Sys. dm_exec_sql_text &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [Sys. dm_exec_text_query_plan &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)   
 [Sp_control_plan_guide &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
  
  
