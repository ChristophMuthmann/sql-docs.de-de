---
title: "Neuigkeiten in SQL Server vNext (Datenbankmodul) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 42f45b23-6509-45e8-8ee7-76a78f99a920
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# Neuigkeiten in SQL Server vNext (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

**Hinweis:** SQL Server vNext beinhaltet auch die in den SQL Server 2016 Service Packs hinzugefügten Funktionen. Informationen zu diesen Elementen finden Sie unter [Neuigkeiten im Datenbankmodul](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md).

## <a name="sql-server-database-engine-ctp-13"></a>SQL Server-Datenbankmodul (CTP 1.3)
- Indirekte Prüfpunkte für die Leistungsverbesserung
- Verfügbarkeitsgruppen mit weniger Clusterunterstützung wurden hinzugefügt.
- Die Einstellungen des Minimum Replikat-Commits der Verfügbarkeitsgruppen wurden hinzugefügt.
- Verfügbarkeitsgruppen funktionieren jetzt auch über Windows-Linux, um OS-übergreifende Migrationen und Tests zu ermöglichen.
- Temporale Tabellen für den Support der Beibehaltungsrichtlinien wurden hinzugefügt.
- Neue DMV SYS.DM_DB_STATS_HISTOGRAM
- Onlinesupport für die Erstellung und Neuerstellung des nicht geclusterten Columnstore-Index wurde hinzugefügt.
- Fünf neue dynamische Verwaltungsansichten, um Informationen zum Linux-Prozess zurückzugeben. Weitere Informationen finden Sie unter [Linux-Prozess dynamische Verwaltungssichten](../../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md).   
- [Sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) wird zum Untersuchen von Statistiken hinzugefügt.

## <a name="sql-server-database-engine-ctp-12"></a>SQL Server-Datenbankmodul (CTP 1.2)

- Der Datenbankoptimierungsratgebers (DTA), der mit SQL Server Management Studio Version 16.4 freigegeben wurde, verfügt über zusätzliche Optionen, wenn SQL Server 2016 analysiert wird.    
   - Verbesserte Leistung. Weitere Informationen finden Sie unter [Performance Improvements using Database Engine Tuning Advisor (DTA) recommendations (Leistungsverbesserungen mithilfe von Empfehlungen des Datenbankoptimierungsratgebers (DTA))](../../relational-databases/performance/performance-improvements-using-dta-recommendations.md).
   - Die `-fc`-Option, die Empfehlungen für Columnstore-Indizes zulässt. Weitere Informationen finden Sie unter [dta (Hilfsprogramm)](../../tools/dta/dta-utility.md) und [Columnstore index recommendations in Database Engine Tuning Advisor (DTA) (Empfehlungen für Columnstore-Index im Datenbankoptimierungsratgeber (DTA))](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md).  
   - Die `-iq`-Option, die dem DTA erlaubt, eine Arbeitsauslastung aus dem Abfragespeicher zu überprüfen. Weitere Informationen finden Sie unter [Tuning Database Using Workload from Query Store (Datenbankoptimierung mithilfe der Arbeitsauslastung aus dem Abfragespeicher)](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md).
   

## <a name="sql-server-database-engine-ctp-11"></a>SQL Server-Datenbankmodul (CTP 1.1)

<a name="InMemoryBulletsCtp11"/>
- Für InMemory-Funktionen wurden zusätzliche Erweiterungen zu speicheroptimierten Tabellen und nativ kompilierten Funktionen aufgeführt, und Codebeispiele finden Sie im [nachfolgenden Text](#InMemory_CodeSamples):
    - Unterstützung für berechnete Spalten in speicheroptimierten Tabellen und Indizes auf berechneten Spalten.
    - Vollständige Unterstützung für JSON-Funktionen in nativ kompilierten Modulen und CHECK-Einschränkungen.
    - `CROSS APPLY`-Operator in nativ kompilierten Modulen.   
- Die neuen Zeichenfolgenfunktionen [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md), [TRANSLATE](../../t-sql/functions/translate-transact-sql.md) und [TRIM](../../t-sql/functions/trim-transact-sql.md) wurden hinzugefügt.   
- Die `WITHIN GROUP`-Klausel wird nun für die [STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md)-Funktion unterstützt.
- Es wurden zwei neue japanische Sortierungsfamilien (Japanese_Bushu_Kakusu_140 und Japanese_XJIS_140) hinzugefügt, und die Sortierungsoption „Unterscheidung nach Variierungsauswahlzeichen“ (_VSS) wurde für die Verwendung in japanischen Sortierungen hinzugefügt. Einzelheiten dazu finden Sie unter [Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md).   
- Neue Bulk-Access-Optionen ([BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)) ermöglichen den Zugriff auf Daten direkt aus einer Datei, die als CSV-Format angegeben ist, und über die neue `BLOB_STORAGE`-Option von [EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) aus Dateien in Azure Blob Storage.


## <a name="sql-server-database-engine-ctp-10"></a>SQL Server-Datenbankmodul (CTP 1.0)

- Der Datenbank-**KOMPATIBILITÄTSGRAD** 140 wurde hinzugefügt.   Kunden, die diesen Kompatibilitätsgrad ausführen, können die neuesten Sprachfeatures und Verhaltensweisen des Abfrageoptimierers nutzen. Dies schließt Änderungen in den einzelnen von Microsoft veröffentlichten Vorabversionen ein.
- Verbesserte Berechnung der Aktualisierungsschwellenwerte für inkrementelle Statistiken (Kompatibilitätsgrad&140; erforderlich).
- [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) wurde hinzugefügt.
- Wir haben viele Leistungs- und Sprachverbesserungen für Tabellen im Arbeitsspeicher hinzugefügt:
    - `sp_spaceused` wird jetzt für Tabellen im Arbeitsspeicher unterstützt.
    - `sp_rename` wird jetzt für native Module unterstützt.
    - `CASE`-Anweisungen werden jetzt für native Module unterstützt.
    - Die Beschränkung auf 8 Indizes für Tabellen im Arbeitsspeicher wurde aufgehoben.
    - `TOP (N) WITH TIES` wird jetzt in nativen Modulen unterstützt.
    - `ALTER TABLE` für Tabellen im Arbeitsspeicher ist jetzt in manchen Fällen erheblich schneller.
    - Das Wiederholen von Transaktionen erfolgt für Tabellen im Arbeitsspeicher jetzt parallel. Dadurch wird der Zeitaufwand für Failover und in einigen Fällen auch Neustarts erheblich verringert.
    - Prüfpunktdateien im Arbeitsspeicher können jetzt auf Azure Storage gespeichert werden. Dadurch bieten sich für MDF-Dateien ähnliche Möglichkeiten wie für LDF-Dateien, die diese Möglichkeit bereits bieten.
- Gruppierte Columnstore-Indizes unterstützen jetzt LOB-Spalten (nvarchar(max), varchar(max), varbinary(max)).
- Die Aggregatfunktion [STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md) wurde hinzugefügt.  
- Neue Berechtigungen: `DATABASE SCOPED CREDENTIAL` ist jetzt eine Klasse von sicherungfsähigen, unterstützenden `CONTROL`, `ALTER`, `REFERENCES`, `TAKE OWNERSHIP` und `VIEW DEFINITION`-Berechtigungen. `ADMINISTER DATABASE BULK OPERATIONS` ist auf SQL-Datenbanken beschränkt und ist jetzt in `sys.fn_builtin_permissions` sichtbar.   
- Die DMV [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md) wurde hinzugefügt und stellt Systeminformationen sowohl für Windows als auch für Linux bereit.   
- Die Datenbankrollen werden mit R Services für das Verwalten von Berechtigungen erstellt, die Paketen zugeordnet sind. Weitere Informationen finden Sie unter [R-Paketverwaltung für SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md).
 
<a name="InMemory_CodeSamples"/> 
## <a name="code-samples-for-new-in-memory-enhancements"></a>Codebeispiele für neue InMemory-Erweiterungen

Die folgenden Unterabschnitte bieten Transact-SQL-Codebeispiele, die neue InMemory-Funktionen veranschaulichen, welche im vorangegangenen Text in diesem Artikel aufgelistet sind.

Die CTP 1.1-Aufzählung von InMemory finden Sie [hier](#InMemoryBulletsCtp11).

#### <a name="computed-column-in-a-memory-optimized-table"></a>Berechnete Spalte in einer speicheroptimierten Tabelle

Diese CREATE TABLE-Anweisung veranschaulicht die folgenden Funktionen, die im vorhergehenden Text zur CTP 1.1 erwähnt wurden:

- JSON-Check-Einschränkung für eine Spalte
- Neue berechnete Spalten
- Index in einer berechneten Spalten

```tsql
CREATE TABLE Product(
    ProductID  int            PRIMARY KEY NONCLUSTERED,
    Name       nvarchar(400)  NOT NULL,
    Price      float,

    Data      nvarchar(4000)  CONSTRAINT [Data contains JSON]  CHECK (ISJSON(Data)=1),

    MadeIn  AS CAST(JSON_VALUE(Data, '$.MadeIn')            as NVARCHAR(50)) PERSISTED,
    Cost    AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float       ),

    INDEX [idx_Product_MadeIn] NONCLUSTERED (MadeIn)
)
        WITH (MEMORY_OPTIMIZED=ON);
```

#### <a name="cross-apply-and-json-functions"></a>CROSS APPLY und JSON-Funktionen

Diese CREATE PROCEDURE-Anweisung für eine native kompilierte gespeicherte Prozedur veranschaulicht die folgenden Funktionen, die im vorhergehenden Text zur CTP 1.1 erwähnt wurden:

- CROSS APPLY-Operator
- JSON-Funktionen

```tsql
CREATE OR ALTER PROCEDURE ProductList()
    WITH SCHEMABINDING, NATIVE_COMPILATION
as begin
    atomic with (transaction isolation level = snapshot,  language = N'English')

    SELECT
            ProductID, Name, Price, Tags,
            Data,
            JSON_VALUE(Data,'$.MadeIn') AS MadeIn,
            value
        FROM Product
        CROSS APPLY OPENJSON(Data, '$.SalesReasons')
        FOR JSON PATH
end;
```
