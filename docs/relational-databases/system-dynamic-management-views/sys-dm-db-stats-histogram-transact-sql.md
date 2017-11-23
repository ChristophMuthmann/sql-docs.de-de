---
title: Sys.dm_db_stats_histogram (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.dm_db_stats_histogram
- sys.dm_db_stats_histogram_TSQL
- dm_db_stats_histogram
- dm_db_stats_histogram_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_stats_histogram dynamic management function
ms.assetid: 1897fd4a-8d51-461e-8ef2-c60be9e563f2
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 93aec7a71f3522114bc9ef6c2d19edaccaac2e57
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysdmdbstatshistogram-transact-sql"></a>Sys.dm_db_stats_histogram (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Gibt das statistikhistogramm für das angegebene Datenbankobjekt (Tabelle oder indizierte Sicht) in der aktuellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank. Ähnlich wie `DBCC SHOW_STATISTICS WITH HISTOGRAM`.

> [!NOTE] 
> Diese DMF steht ab [!INCLUDE[ssSQL15](../../includes/ssSQL15-md.md)] SP1 CU2

## <a name="syntax"></a>Syntax  
  
```  
sys.dm_db_stats_histogram (object_id, stats_id)  
```  
  
## <a name="arguments"></a>Argumente  
 *object_id*  
 ID des Objekts in der aktuellen Datenbank, für die Eigenschaften einer der enthaltenen Statistiken angefordert werden. *object_id* ist **int**.  
  
 *stats_id*  
 ID der Statistik für die angegebene *object_id*. Die Statistik-ID kann aus der dynamischen Verwaltungssicht [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) abgerufen werden. *stats_id* ist **int**.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|object_id |**int**|ID des Objekts (Tabelle oder indizierte Sicht), für das die Eigenschaften des Statistikobjekts zurückgegeben werden sollen.|  
|stats_id |**int**|Die ID des Statistikobjekts. Diese ist innerhalb der Tabelle oder indizierten Sicht eindeutig. Weitere Informationen finden Sie unter [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md).|  
|step_number |**int** |Die Anzahl der Schritte im Histogramm. |
|range_high_key |**sql_variant** |Oberer Spaltengrenzwert für einen Histogrammschritt. Der Spaltenwert wird auch als Schlüsselwert bezeichnet.|
|RANGE_ROWS |**real** |Geschätzte Anzahl von Zeilen, deren Spaltenwerte innerhalb eines Histogrammschritts liegen, ohne den oberen Grenzwert. |
|equal_rows |**real** |Geschätzte Anzahl von Zeilen, deren Spaltenwerte der Obergrenze des Histogrammschritts entsprechen. |
|DISTINCT_RANGE_ROWS |**bigint** |Geschätzte Anzahl von Zeilen mit einem unterschiedlichen Spaltenwert innerhalb eines Histogrammschritts ohne den oberen Grenzwert. |
|average_range_rows |**real** |Durchschnittliche Anzahl von Zeilen mit doppelten Spaltenwerten in einem Histogrammschritt, ohne den oberen Grenzwert (`RANGE_ROWS / DISTINCT_RANGE_ROWS` für `DISTINCT_RANGE_ROWS > 0`). |
  
 ## <a name="remarks"></a>Hinweise  
 
 Das Resultset für `sys.dm_db_stats_histogram` gibt Informationen ähnlich `DBCC SHOW_STATISTICS WITH HISTOGRAM` und weist daneben `object_id`, `stats_id`, und `step_number`.

 Da die Spalte `range_high_key` ist eine Sql_variant-Daten geben, müssen Sie möglicherweise verwenden `CAST` oder `CONVERT` , wenn ein Prädikat Vergleich mit eine Zeichenfolgenkonstante ist.

### <a name="histogram"></a>Histogramm
  
 Ein Histogramm misst die Häufigkeit des Vorkommens für jeden unterschiedlichen Wert in einem Dataset. Der Abfrageoptimierer berechnet ein Histogramm für die Spaltenwerte in der ersten Schlüsselspalte des Statistikobjekts und wählt die Spaltenwerte aus, indem statistische Zeilenstichproben entnommen werden oder indem ein vollständiger Scan aller Zeilen in der Tabelle oder Sicht ausgeführt wird. Wenn das Histogramm anhand einer Gruppe von Zeilenstichproben erstellt wird, handelt es sich bei der gespeicherten Gesamtzahl von Zeilen und unterschiedlichen Werten um Schätzungen, die keine ganzen Zahlen sein müssen.  
  
 Zum Erstellen des Histogramms sortiert der Abfrageoptimierer die Spaltenwerte, berechnet die Anzahl der Werte, die den einzelnen unterschiedlichen Spaltenwerten entsprechen, und aggregiert die Spaltenwerte dann in maximal 200 zusammenhängenden Histogrammschritten. Jeder Schritt umfasst einen Bereich von Spaltenwerten gefolgt von einem oberen Spaltengrenzwert. Der Bereich enthält alle möglichen Spaltenwerte zwischen den Begrenzungswerten, ohne die Begrenzungswerte selbst. Der niedrigste der sortierten Spaltenwerte ist der obere Grenzwert für den ersten Histogrammschritt.  
  
 Das folgende Diagramm zeigt ein Histogramm mit sechs Schritten. Der Bereich links vom ersten oberen Grenzwert ist der erste Schritt.  
  
 ![](../../relational-databases/system-dynamic-management-views/media/a0ce6714-01f4-4943-a083-8cbd2d6f617a.gif "a0ce6714-01f4-4943-a083-8cbd2d6f617a")  
  
 Für jeden Histogrammschritt gilt:  
  
-   Fett formatierte Zeile stellt den oberen Grenzwert (*Range_high_key*) und wie oft der Wartetyp tritt auf (*Equal_rows*)  
  
-   Der einfarbige Bereich links *Range_high_key* stellt den Bereich der Spaltenwerte und die durchschnittliche Anzahl von jedem Spaltenwert tritt auf (*Average_range_rows*). Die *Average_range_rows* für das Histogramm ersten Schritt ist immer 0.  
  
-   Gepunktete Linien stellen die als Stichprobe entnommenen Werte, die zum Schätzen der Gesamtanzahl der unterschiedlichen Werte im Bereich (*Distinct_range_rows*) und die Gesamtzahl der Werte im Bereich (*Range_rows*). Der Abfrageoptimierer verwendet *Range_rows* und *Distinct_range_rows* berechnet *Average_range_rows* und der als Stichprobe entnommenen Werte werden nicht gespeichert.  
  
 Der Abfrageoptimierer definiert die Histogrammschritte gemäß ihrer statistischen Bedeutung. Dabei wird ein Algorithmus für die maximale Differenz verwendet, um die Anzahl der Schritte im Histogramm zu minimieren und gleichzeitig die Differenz zwischen den Begrenzungswerten zu maximieren. Die maximale Anzahl von Schritten ist 200. Die Anzahl von Histogrammschritten kann geringer sein als die Anzahl unterschiedlicher Werte, auch bei Spalten mit weniger als 200 Grenzpunkten. Beispielsweise kann eine Spalte mit 100 unterschiedlichen Werten ein Histogramm mit weniger als 100 Grenzpunkten aufweisen.  
  
## <a name="permissions"></a>Berechtigungen  

Erfordert, dass der Benutzer über SELECT-Berechtigungen für Statistikspalten verfügt, Besitzer der Tabelle oder Mitglied der festen Serverrolle `sysadmin`, der festen Datenbankrolle `db_owner` oder der festen Datenbankrolle `db_ddladmin` ist.

## <a name="examples"></a>Beispiele  

### <a name="a-simple-example"></a>A. Einfaches Beispiel    
Das folgende Beispiel erstellt und füllt eine einfache Tabelle. Klicken Sie dann erstellt Statistiken für die `Country_Name` Spalte.

```tsql
CREATE TABLE Country
(Country_ID int IDENTITY PRIMARY KEY,
Country_Name varchar(120) NOT NULL);
INSERT Country (Country_Name) VALUES ('Canada'), ('Denmark'), ('Iceland'), ('Peru');

CREATE STATISTICS Country_Stats  
    ON Country (Country_Name) ;  
```   
Der Primärschlüssel belegt `stat_id` Nummer 1, daher rufen `sys.dm_db_stats_histogram` für `stat_id` Nummer 2, für das statistikhistogramm Zurückgeben der `Country` Tabelle.    
```tsql     
SELECT * FROM sys.dm_db_stats_histogram(OBJECT_ID('Country'), 2);
```


### <a name="b-useful-query"></a>B. Praktische Abfrage:   
```tsql  
SELECT hist.step_number, hist.range_high_key, hist.range_rows, 
    hist.equal_rows, hist.distinct_range_rows, hist.average_range_rows
FROM sys.stats AS s
CROSS APPLY sys.dm_db_stats_histogram(s.[object_id], s.stats_id) AS hist
WHERE s.[name] = N'<statistic_name>';
```

### <a name="c-useful-query"></a>C. Praktische Abfrage:
Das folgende Beispiel wählt aus Tabelle `Country` mit einem Prädikat für Spalte `Country_Name`.

```tsql  
SELECT * FROM Country 
WHERE Country_Name = 'Canada';
```

Im folgenden Beispiel wird die zuvor erstellte Statistik für Tabelle prüft `Country` und `Country_Name` für den Abgleich des Prädikats in der obigen Abfrage Histogrammschritt.

```tsql  
SELECT ss.name, ss.stats_id, shr.steps, shr.rows, shr.rows_sampled, 
    shr.modification_counter, shr.last_updated, sh.range_rows, sh.equal_rows
FROM sys.stats ss
INNER JOIN sys.stats_columns sc 
    ON ss.stats_id = sc.stats_id AND ss.object_id = sc.object_id
INNER JOIN sys.all_columns ac 
    ON ac.column_id = sc.column_id AND ac.object_id = sc.object_id
CROSS APPLY sys.dm_db_stats_properties(ss.object_id, ss.stats_id) shr
CROSS APPLY sys.dm_db_stats_histogram(ss.object_id, ss.stats_id) sh
WHERE ss.[object_id] = OBJECT_ID('Country') 
    AND ac.name = 'Country_Name'
    AND sh.range_high_key = CAST('Canada' AS CHAR(8));
```
  
## <a name="see-also"></a>Siehe auch  

[DBCC SHOW_STATISTICS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
[Objektbezogene dynamische Verwaltungssichten und-Funktionen (Transact-SQL)](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)  
[Sys. dm_db_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)  
