---
title: dm_exec_query_optimizer_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_optimizer_info_TSQL
- dm_exec_query_optimizer_info
- sys.dm_exec_query_optimizer_info_TSQL
- sys.dm_exec_query_optimizer_info
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_optimizer_info dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9e
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cf54ff13623d2ca2e523fd8db3afde8bb2be3367
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexecqueryoptimizerinfo-transact-sql"></a>sys.dm_exec_query_optimizer_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt ausführliche Statistiken zur Ausführung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageoptimierers zurück. Diese Sicht können Sie beim Optimieren einer Arbeitsauslastung verwenden, um Probleme oder Verbesserungen bei der Abfrageoptimierung zu identifizieren. Sie können beispielsweise anhand der Gesamtanzahl der Optimierungen, des Wertes für die verstrichene Zeit und des Endkostenwertes die Abfrageoptimierungen der aktuellen Arbeitsauslastung und sämtliche während des Optimierungsvorgangs beobachteten Änderungen vergleichen. Einige Leistungsindikatoren stellen Daten bereit, die nur für die interne Diagnose von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relevant sind. Diese Leistungsindikatoren sind als "Internal only" gekennzeichnet.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_exec_query_optimizer_info**.  
  
|Name|Datentyp|Description|  
|----------|---------------|-----------------|  
|**Leistungsindikator**|**nvarchar(4000)**|Name des Statistikereignisses des Abfrageoptimierers.|  
|**occurrence**|**bigint**|Anzahl der Vorkommen von Optimierungsereignissen für diesen Leistungsindikator.|  
|**value**|**float**|Durchschnittlicher Eigenschaftswert pro Ereignisvorkommen.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
    
## <a name="remarks"></a>Hinweise  
 **dm_exec_query_optimizer_info** enthält die folgenden Eigenschaften (Leistungsindikatoren). Alle Vorkommenwerte sind kumulativ und werden beim Neustarten des Systems auf 0 festgelegt. Alle Werte für Wertfelder werden beim Neustarten des Systems auf NULL festgelegt. Alle Wertspaltenwerte, die einen Durchschnitt angeben, verwenden den Vorkommenwert aus derselben Zeile als Nenner bei der Berechnung des Durchschnitts. Alle abfrageoptimierungen werden gemessen, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bestimmt die Änderungen an **Dm_exec_query_optimizer_info**, einschließlich beide Benutzer und systemgenerierten Abfragen. Ausführung eines bereits zwischengespeicherten Plans ändert sich nicht auf die Werte in **Dm_exec_query_optimizer_info**nur Optimierungen sind von Bedeutung.  
  
|Leistungsindikator|Vorkommen|Wert|  
|-------------|----------------|-----------|  
|optimizations|Gesamtzahl der Optimierungen.|Nicht verfügbar|  
|elapsed time|Gesamtzahl der Optimierungen.|Durchschnittlich verstrichene Zeit pro Optimierung einer einzelnen Anweisung (Abfrage), in Sekunden.|  
|final cost|Gesamtzahl der Optimierungen.|Durchschnittliche geschätzte Kosten für einen optimierten Plan in internen Kosteneinheiten.|  
|trivial plan|Nur intern|Nur intern|  
|Tasks|Nur intern|Nur intern|  
|no plan|Nur intern|Nur intern|  
|Suche 0|Nur intern|Nur intern|  
|search 0 time|Nur intern|Nur intern|  
|0 Aufgaben suchen|Nur intern|Nur intern|  
|Suche 1|Nur intern|Nur intern|  
|Suche 1 Zeit|Nur intern|Nur intern|  
|Suche 1 Aufgaben|Nur intern|Nur intern|  
|search 2|Nur intern|Nur intern|  
|search 2 time|Nur intern|Nur intern|  
|search 2 tasks|Nur intern|Nur intern|  
|Stufe 0 auf Stufe 1 erhöhen|Nur intern|Nur intern|  
|gain stage 1 to stage 2|Nur intern|Nur intern|  
|timeout|Nur intern|Nur intern|  
|memory limit exceeded|Nur intern|Nur intern|  
|insert stmt|Anzahl der für INSERT-Anweisungen ausgeführten Optimierungen.|Nicht verfügbar|  
|delete stmt|Anzahl der für DELETE-Anweisungen ausgeführten Optimierungen.|Nicht verfügbar|  
|update stmt|Anzahl der für UPDATE-Anweisungen ausgeführten Optimierungen.|Nicht verfügbar|  
|contains subquery|Anzahl der Optimierungen für eine Abfrage, die mindestens eine Unterabfrage enthält.|Nicht verfügbar|  
|unnest failed|Nur intern|Nur intern|  
|Tabellen|Gesamtzahl der Optimierungen.|Gesamtzahl der Tabellen, auf die pro optimierte Abfrage verwiesen wird.|  
|hints|Häufigkeit, mit der ein Hinweis angegeben wurde. Zu diesen Hinweisen gehören die Abfragehinweise JOIN, GROUP, UNION und FORCE ORDER, die SET-Option FORCE PLAN sowie Joinhinweise.|Nicht verfügbar|  
|order hint|Häufigkeit, mit der ein FORCE ORDER-Hinweis angegeben wurde.|Nicht verfügbar|  
|join hint|Häufigkeit, mit der der Joinalgorithmus von einem Joinhinweis erzwungen wurde.|Nicht verfügbar|  
|view reference|Häufigkeit, mit der in einer Abfrage auf eine Sicht verwiesen wurde.|Nicht verfügbar|  
|remote query|Anzahl der Optimierungen, bei denen die Abfrage auf mindestens eine Remotedatenquelle verwiesen hat, wie z. B. auf eine Tabelle mit einem vierteiligen Namen oder ein OPENROWSET-Ergebnis.|Nicht verfügbar|  
|maximum DOP|Gesamtzahl der Optimierungen.|Durchschnittlicher effektiver MAXDOP-Wert für einen optimierten Plan. Standardmäßig wird durch effektive MAXDOP bestimmt die **Max. Grad an Parallelität** Serverkonfiguration aus, und kann für eine bestimmte Abfrage durch den Wert des MAXDOP-Abfragehinweises überschrieben werden.|  
|maximum recursion level|Anzahl der Optimierungen, bei denen mit dem Abfragehinweis eine höhere MAXRECURSION-Ebene als 0 angegeben wurde.|Durchschnittliche MAXRECURSION-Ebene in Optimierungen, bei denen mit dem Abfragehinweis eine maximale Rekursionsebene angegeben wurde.|  
|indexed views loaded|Nur intern|Nur intern|  
|indexed views matched|Anzahl der Optimierungen, bei denen für mindestens eine indizierte Sicht eine Übereinstimmung gefunden wurde.|Durchschnittliche Anzahl der übereinstimmenden Sichten.|  
|indexed views used|Anzahl der Optimierungen, bei denen nach dem Abgleich mindestens eine indizierte Sicht im Ausgabeplan verwendet wird.|Durchschnittliche Anzahl der verwendeten Sichten.|  
|indexed views updated|Anzahl der Optimierungen einer DML-Anweisung, die einen Plan erstellen, von dem mindestens eine indizierte Sicht verwaltet wird.|Durchschnittliche Anzahl der verwalteten Sichten.|  
|dynamic cursor request|Anzahl der Optimierungen, in denen eine Anforderung nach dynamischen Cursorn angegeben wurde.|Nicht verfügbar|  
|fast forward cursor request|Anzahl der Optimierungen, in denen eine Anforderung nach schnellen Vorwärtscursorn angegeben wurde.|Nicht verfügbar|  
|merge stmt|Anzahl der für MERGE-Anweisungen ausgeführten Optimierungen.|Nicht verfügbar|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-viewing-statistics-on-optimizer-execution"></a>A. Anzeigen von Statistiken zur Ausführung von Optimierern  
 Wie sehen die aktuellen Statistiken zur Ausführung des Abfrageoptimierers für diese [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz aus?  
  
```  
SELECT * FROM sys.dm_exec_query_optimizer_info;  
```  
  
### <a name="b-viewing-the-total-number-of-optimizations"></a>B. Anzeigen der Gesamtzahl von Optimierungen  
 Wie viele Optimierungen werden ausgeführt?  
  
```  
SELECT occurrence AS Optimizations FROM sys.dm_exec_query_optimizer_info  
WHERE counter = 'optimizations';  
```  
  
### <a name="c-average-elapsed-time-per-optimization"></a>C. Durchschnittliche verstrichene Zeit pro Optimierung  
 Wie lange dauert eine Optimierung im Durchschnitt?  
  
```  
SELECT ISNULL(value,0.0) AS ElapsedTimePerOptimization  
FROM sys.dm_exec_query_optimizer_info WHERE counter = 'elapsed time';  
```  
  
### <a name="d-fraction-of-optimizations-that-involve-subqueries"></a>D. Anteil der Optimierungen mit Unterabfragen  
 Wie hoch liegt der Anteil der optimierten Abfragen mit einer Unterabfrage?  
  
```  
SELECT (SELECT CAST (occurrence AS float) FROM sys.dm_exec_query_optimizer_info WHERE counter = 'contains subquery') /  
       (SELECT CAST (occurrence AS float)   
        FROM sys.dm_exec_query_optimizer_info WHERE counter = 'optimizations')  
        AS ContainsSubqueryFraction;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Ausführung dynamische Verwaltungssichten und-Funktionen im Zusammenhang &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


