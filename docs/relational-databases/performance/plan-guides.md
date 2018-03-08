---
title: Planhinweislisten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-plan-guides
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TEMPLATE plan guide
- SQL plan guides
- OPTIMIZE FOR query hint
- RECOMPILE query hint
- OBJECT plan guide
- plan guides [SQL Server], about plan guides
- OPTION clause
- plan guides [SQL Server]
- USE PLAN query hint
ms.assetid: bfc97632-c14c-4768-9dc5-a9c512f6b2bd
caps.latest.revision: "52"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a0414a27a14e937e7c58ca6ba74de3b6bfd6a2b0
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="plan-guides"></a>Planhinweislisten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mit Planhinweislisten können Sie die Leistung von Abfragen optimieren, wenn Sie den Text der eigentlichen Abfrage in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nicht direkt ändern möchten oder können. Planhinweislisten beeinflussen die Abfrageoptimierung, indem Abfragehinweise oder ein fester Abfrageplan an die Abfragen angefügt werden. Die Verwendung von Planhinweislisten bietet sich z. B. an, wenn eine kleine Teilmenge von Abfragen in der Datenbankanwendung eines Drittanbieters nicht erwartungsgemäß funktioniert. In der Planhinweisliste geben Sie die Transact-SQL-Anweisung an, die optimiert werden soll, sowie entweder eine OPTION-Klausel mit den zu verwendenden Abfragehinweisen oder einen spezifischen Abfrageplan, der für die Optimierung der Abfrage verwendet werden soll. Wenn die Abfrage ausgeführt wird, vergleicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Transact-SQL-Anweisung mit der Planhinweisliste und fügt der Abfrage entweder zur Laufzeit die OPTION-Klausel hinzu oder verwendet den angegebenen Abfrageplan.  
  
 Die maximale Anzahl der erstellbaren Planhinweislisten ist lediglich durch die verfügbaren Systemressourcen begrenzt. Planhinweislisten sollten jedoch nur begrenzt für unternehmenswichtige Abfragen verwendet werden, deren Leistung verbessert oder stabilisiert werden soll. Planhinweislisten sollten nicht verwendet werden, um die überwiegende Abfragelast einer bereitgestellten Anwendung zu beeinflussen.  
  
> [!NOTE]  
>  Planhinweislisten können nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md). Planhinweislisten sind in jeder Edition sichtbar. Sie können auch in allen Versionen eine Datenbank anfügen, die Planhinweislisten enthält. Planhinweislisten bleiben beim Wiederherstellen oder Anfügen einer Datenbank in einer aktualisierten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erhalten.  
  
## <a name="types-of-plan-guides"></a>Typen von Planhinweislisten  
 Die folgenden Typen von Planhinweislisten können erstellt werden.  
  
 ### <a name="object-plan-guide"></a>OBJECT-Planhinweisliste  
 OBJECT-Planhinweislisten dienen zum Abgleich von Abfragen, die im Kontext von gespeicherten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Prozeduren, benutzerdefinierten Skalarfunktionen, benutzerdefinierten Tabellenwertfunktionen mit mehreren Anweisungen und von DML-Triggern ausgeführt werden.  
  
 Angenommen, die folgende gespeicherte Prozedur, die den `@Country_region`-Parameter annimmt, existiert in einer Datenbankanwendung, die in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank bereitgestellt wird:  
  
```sql  
CREATE PROCEDURE Sales.GetSalesOrderByCountry (@Country_region nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h, Sales.Customer AS c,   
        Sales.SalesTerritory AS t  
    WHERE h.CustomerID = c.CustomerID  
        AND c.TerritoryID = t.TerritoryID  
        AND CountryRegionCode = @Country_region  
END;  
```  
  
 Gehen Sie weiterhin davon aus, dass diese gespeicherte Prozedur kompiliert und für `@Country_region = N'AU'` (Australien) optimiert wurde. Aus Australien kommen jedoch nur relativ wenige Bestellungen. Wenn die Abfrage mit Parameterwerten für Länder oder Regionen mit mehr Bestellungen ausgeführt wird, verringert dies die Leistung. Da die meisten Bestellungen aus den USA kommen, würde ein für `@Country_region = N'US'` generierter Abfrageplan wahrscheinlich eine bessere Leistung für alle möglichen Werte des `@Country_region` -Parameters erbringen.  
  
 Sie könnten dieses Problem lösen, indem Sie die gespeicherte Prozedur so ändern, dass der Abfrage der `OPTIMIZE FOR` -Abfragehinweis hinzugefügt wird. Da sich die gespeicherte Prozedur jedoch in einer bereitgestellten Anwendung befindet, können Sie den Code der Anwendung nicht direkt ändern. Stattdessen können Sie in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank die folgende Planhinweisliste erstellen.  
  
```sql  
sp_create_plan_guide   
@name = N'Guide1',  
@stmt = N'SELECT *FROM Sales.SalesOrderHeader AS h,  
        Sales.Customer AS c,  
        Sales.SalesTerritory AS t  
        WHERE h.CustomerID = c.CustomerID   
            AND c.TerritoryID = t.TerritoryID  
            AND CountryRegionCode = @Country_region',  
@type = N'OBJECT',  
@module_or_batch = N'Sales.GetSalesOrderByCountry',  
@params = NULL,  
@hints = N'OPTION (OPTIMIZE FOR (@Country_region = N''US''))';  
```  
  
 Wenn die in der `sp_create_plan_guide` -Anweisung angegebene Abfrage ausgeführt wird, wird sie vor der Optimierung so geändert, dass sie die `OPTIMIZE FOR (@Country = N''US'')` -Klausel enthält.  
  
 ### <a name="sql-plan-guide"></a>SQL-Planhinweisliste  
 SQL-Planhinweislisten dienen zum Abgleich von Abfragen, die im Kontext von eigenständigen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen und -Batches, die nicht Teil eines Datenbankobjekts sind, ausgeführt werden. SQL-basierte Planhinweislisten können auch zum Abgleich von Abfragen verwendet werden, die in einer bestimmten Form parametrisiert werden. SQL-Planhinweislisten werden für eigenständige [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen und -Batches verwendet. Diese Anweisungen werden von einer Anwendung häufig mithilfe der gespeicherten Systemprozedur [sp_executesql](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md) übermittelt. Betrachten Sie beispielsweise den folgenden eigenständigen Batch:  
  
```sql  
SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC;  
```  
  
 Um zu verhindern, dass ein paralleler Ausführungsplan für diese Abfrage generiert wird, erstellen Sie die folgende Planhinweisliste und legen den `MAXDOP` -Abfragehinweis im `1` -Parameter auf `@hints` fest.  
  
```sql  
sp_create_plan_guide   
@name = N'Guide2',   
@stmt = N'SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC',  
@type = N'SQL',  
@module_or_batch = NULL,   
@params = NULL,   
@hints = N'OPTION (MAXDOP 1)';  
```  
  
> [!IMPORTANT]  
>  Die für das `@module_or_batch` -Argument und das `@params` -Argument der `sp_create_plan guide` -Anweisung angegebenen Werte müssen mit dem Text übereinstimmen, der in der Abfrage übermittelt wird. Weitere Informationen finden Sie unter [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md) -Argument und das [Verwenden von SQL Server Profiler zum Erstellen und Testen von Planhinweislisten](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md)nicht direkt ändern möchten oder können.  
  
 SQL-Planhinweislisten können auch für Abfragen erstellt werden, die in derselben Form parametrisiert werden, wenn die PARAMETERIZATION-Datenbankoption mithilfe von SET auf FORCED festgelegt wird oder wenn eine TEMPLATE-Planhinweisliste erstellt wird, die eine parametrisierte Abfrageklasse angibt.  
  
 ### <a name="template-plan-guide"></a>TEMPLATE (Planhinweisliste)  
 Eine TEMPLATE-Planhinweisliste zur Übereinstimmung mit eigenständigen Abfragen, die in einer angegebenen Form parametrisiert werden. Diese Planhinweislisten werden verwendet, um die aktuelle PARAMETERIZATION-Datenbankoption für eine bestimmte Abfrageklasse zu überschreiben.  
  
 Sie können eine TEMPLATE-Planhinweisliste in folgenden Situationen erstellen:  
  
-   Die Datenbankoption PARAMETERIZATION ist auf FORCED festgelegt, es gibt aber Abfragen, die nach den Regeln der [einfachen Parametrisierung](../../relational-databases/query-processing-architecture-guide.md#SimpleParam) kompiliert werden sollen.  
  
-   Die Datenbankoption PARAMETERIZATION ist auf SIMPLE festgelegt (die Standardeinstellung), für eine Klasse von Abfragen soll aber eine [erzwungene Parametrisierung](../../relational-databases/query-processing-architecture-guide.md#ForcedParam) versucht werden.  
  
## <a name="plan-guide-matching-requirements"></a>Voraussetzungen für den Planhinweislistenabgleich  
 Planhinweislisten beziehen sich auf die Datenbank, in der sie erstellt werden. Daher können nur die Planhinweislisten gegen die Abfrage geprüft werden, die in der zum Zeitpunkt der Ausführung einer Abfrage aktuellen Datenbank vorhanden sind. Beispiel: Wenn [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] die aktuelle Datenbank ist und die folgende Abfrage ausgeführt wird:  
  
 ```sql
 SELECT FirstName, LastName FROM Person.Person;
 ```  
  
 Dann können nur in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank vorhandene Planhinweislisten mit dieser Abfrage verglichen werden. Wenn jedoch [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] die aktuelle Datenbank ist und die folgenden Anweisungen ausgeführt werden:  
  
 ```sql
 USE DB1; 
 SELECT FirstName, LastName FROM Person.Person;
 ```  
  
 Dann können nur in `DB1` vorhandene Planhinweislisten mit dieser Abfrage verglichen werden, weil die Abfrage im Kontext von `DB1`ausgeführt wird.  
  
 Bei SQL- und TEMPLATE-basierten Planhinweislisten vergleicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Werte der Argumente @module_or_batch und @params mit einer Abfrage, indem die beiden Werte Zeichen für Zeichen verglichen werden. Das bedeutet, dass Sie den Text genau so bereitstellen müssen, wie er von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im tatsächlichen Batch empfangen wird.  
  
 Wenn @type = 'SQL' und @module_or_batch auf NULL gesetzt wird, wird der Wert von @module_or_batch auf den Wert von @stmt festgelegt. Dies bedeutet, dass der Wert für *statement_text* Zeichen für Zeichen in exakt dem gleichen Format bereitgestellt werden muss, in dem er an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]übermittelt wird. Es findet keine interne Konvertierung zur Vereinfachung dieses Abgleichs statt.  
  
 Wenn für eine Anweisung sowohl eine reguläre Planhinweisliste (SQL oder OBJECT) als auch eine TEMPLATE-Planhinweisliste gelten können, wird nur die reguläre Planhinweisliste verwendet.  
  
> [!NOTE]  
>  Der Batch, der die Anweisung enthält, für die Sie eine Planhinweisliste erstellen wollen, darf keine USE *database* -Anweisung enthalten.  
  
## <a name="plan-guide-effect-on-the-plan-cache"></a>Auswirkungen von Planhinweislisten auf den Plancache  
 Wenn Sie eine Planhinweisliste für ein Modul erstellen, wird der Abfrageplan für dieses Modul aus dem Plancache entfernt. Wenn Sie eine Planhinweisliste des Typs OBJECT oder SQL für einen Batch erstellen, wird der Abfrageplan für einen Batch mit demselben Hashwert entfernt. Wenn Sie eine Planhinweisliste des Typs TEMPLATE erstellen, werden alle Batches mit einer Anweisung aus dem Plancache in dieser Datenbank entfernt.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Task|Thema|  
|----------|-----------|  
|Beschreibt, wie eine Planhinweisliste erstellt wird.|[Erstellen einer neuen Planhinweisliste](../../relational-databases/performance/create-a-new-plan-guide.md)|  
|Beschreibt, wie eine Planhinweisliste für parametrisierte Abfragen erstellt wird.|[Erstellen einer Planhinweisliste für parametrisierte Abfragen](../../relational-databases/performance/create-a-plan-guide-for-parameterized-queries.md)|  
|Beschreibt, wie das Abfrageparametrisierungs-Verhalten mit Planhinweislisten gesteuert wird.|[Angeben des Abfrageparametrisierungsverhaltens mithilfe von Planhinweislisten](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)|  
|Beschreibt, wie ein fester Abfrageplan in eine Planhinweisliste eingeschlossen wird.|[Anwenden eines festen Abfrageplans auf eine Planhinweisliste](../../relational-databases/performance/apply-a-fixed-query-plan-to-a-plan-guide.md)|  
|Beschreibt, wie Abfragehinweise in einer Planhinweisliste angegeben werden.|[Anfügen von Abfragehinweisen an eine Planhinweisliste](../../relational-databases/performance/attach-query-hints-to-a-plan-guide.md)|  
|Beschreibt, wie Planhinweislisten-Eigenschaften angezeigt werden.|[Anzeigen der Eigenschaften der Planhinweisliste](../../relational-databases/performance/view-plan-guide-properties.md)|  
|Beschreibt, wie SQL Server Profiler zum Erstellen und Testen von Testplanhinweislisten verwendet wird.|[Verwenden von SQL Server Profiler zum Erstellen und Testen von Planhinweislisten](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md)|  
|Beschreibt, wie Planhinweislisten überprüft werden.|[Überprüfen von Planhinweislisten nach einem Upgrade](../../relational-databases/performance/validate-plan-guides-after-upgrade.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)   
 [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md)  
  
  
