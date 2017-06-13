---
title: "Nach der Migration Überprüfung und Optimierung Handbuch | Microsoft Docs"
ms.custom: 
ms.date: 5/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- post-migration validation and optimization
- guide, post-migration validation and optimization
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
caps.latest.revision: 3
author: pelopes
ms.author: harinid
manager: 
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: d81eabfa1bdb5736bbf6f53ed34c2e1ac157e782
ms.contentlocale: de-de
ms.lasthandoff: 05/25/2017

---
# <a name="post-migration-validation-and-optimization-guide"></a>Nach der Migration Überprüfung und Optimization Guide
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]POST Migration Schritt ist sehr wichtig für das Abgleichen Genauigkeit der Daten und die Vollständigkeit sowie Aufdecken von Leistungsproblemen bei der arbeitsauslastung.

# <a name="common-performance-scenarios"></a>Allgemeine Leistungsszenarien 
Im folgenden sind einige der allgemeinen leistungsszenarien gefunden, die nach der Migration zu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Plattform und deren Behebung. Hierzu gehören auch Szenarios, die auf Specifdic [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration (ältere Versionen auf neuere Versionen) als auch foreign-Plattform (z. B. Oracle, DB2, MySQL und Sybase) [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration.

## <a name="Parameter Sniffing"></a>Sensitivität für die parameterermittlung

**Gilt für:** Foreign-Plattform (z. B. Oracle, DB2, MySQL und Sybase) [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration.

> [!NOTE]
> Für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migrationen, wenn dieses Problem in der Quelle vorhanden waren [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Migration auf eine neuere Version des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] als-wird dieses Szenario nicht berücksichtigen. 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]kompiliert die Abfragepläne für gespeicherte Prozeduren mithilfe der Ermittlung die Eingabeparameter an der ersten Kompilierung, generieren einen Plan parametrisierten und wiederverwendet werden, optimiert für, die Verteilung von Daten eingegeben. Auch wenn keine gespeicherten Prozeduren werden die meisten Anweisungen Generieren von trivialen Pläne parametrisiert werden. Nachdem Sie ein Plan zuerst zwischengespeichert wird, wird eine spätere Ausführung eine zuvor zwischengespeicherte Plan zugeordnet.
Ein mögliches Problem tritt auf, wenn es sich bei dieser ersten Kompilierung nicht die am häufigsten verwendeten Sätze von Parametern für die üblichen arbeitsauslastung verwendet haben kann. Bei anderen Parametern wird desselben Ausführungsplans ineffizient.

### <a name="steps-to-resolve"></a>Schritte zum Beheben

1.    Verwenden der `RECOMPILE` Hinweis. Ein Plan wird berechnet, jedes Mal, wenn jeder Parameterwert angepasst.
2.    Schreiben Sie die gespeicherte Prozedur zur Verwendung der Option `(OPTIMIZE FOR(<input parameter> = <value>))`. Entscheiden Sie, welcher Wert verwendet, die am besten entspricht die meisten der relevanten arbeitsauslastung, erstellen und verwalten einen Plan, der für den parametrisierten Wert effiziente wird.
3.    Schreiben Sie die gespeicherte Prozedur mithilfe von lokalen Variablen in der Prozedur. Nun verwendet der Optimierer density_vector für Einschätzung, was im gleichen Plan unabhängig vom Wert Parameters.
4.    Schreiben Sie die gespeicherte Prozedur zur Verwendung der Option `(OPTIMIZE FOR UNKNOWN)`. Dieselbe Wirkung wie die Verwendung der lokalen Variablen Technik.
5.    Schreiben Sie die Abfrage zum Verwenden des Hinweis `DISABLE_PARAMETER_SNIFFING`. Identisch Effekt wie die Verwendung der lokalen Variablen Technik von völlig deaktiviert die parameterermittlung, es sei denn, `OPTION(RECOMPILE)`, `WITH RECOMPILE` oder `OPTIMIZE FOR <value>` verwendet wird.

> [!TIP] 
> Nutzen der Vorteile der [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] planen Analyse schnell zu identifizieren, wenn dies ein Problem ist. Weitere Informationen zur Verfügung [hier](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-query-performance-troubleshooting-made-easier/).

## <a name="Missing indexes"></a>Fehlende Indizes

**Gilt für:** Foreign Plattform (z. B. Oracle, DB2, MySQL und Sybase) und [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration.

Falsche oder fehlende Indizes bewirkt, dass zusätzliche e/a-, die zu zusätzlichen Arbeitsspeicher führt und CPU-verschwendet wird. Dies kann da Arbeitslast Profil geändert hat, wie die Verwendung von Indexentwurf andere Prädikate, vorhandene wird ungültig gemacht. Details zu einer schlechten Indizierungsstrategie oder Änderungen bei der Arbeitsauslastungsprofil gehören:
-   Suchen Sie nach doppelt redundante, selten verwendet und nicht vollständig verwendeten Indizes.
-   Besondere Sorgfalt mit nicht verwendeten Indizes mit Updates.

### <a name="steps-to-resolve"></a>Schritte zum Beheben

1.    Nutzen Sie den grafischen Ausführungsplan nach fehlenden Index verweisen.
2.    Indizieren von generierten Vorschläge [Datenbankmodul-Optimierungsratgeber](../tools/dta/tutorial-database-engine-tuning-advisor.md).
3.    Nutzen der Vorteile der [fehlende Indizes DMV](../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) oder über die [Dashboard der SQL Server-Leistung](https://www.microsoft.com/en-us/download/details.aspx?id=29063).
4.    Nutzen Sie bereits vorhandene Skripts, die vorhandenen DMVs verwenden können, um einen Einblick in alle fehlenden, doppelten, redundante, selten verwendeten und nicht vollständig verwendeten Indizes, sondern auch bereitzustellen, wenn alle Verweise von Index mit dem Hinweis/hartcodiert vorhandenen Prozeduren und Funktionen in der Datenbank ist. 

> [!TIP] 
> Beispiele für solche bereits vorhandene Skripts [Indexerstellung](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Creation) und [Indexinformationen](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Information). 

## <a name="Inability to use predicates"></a>Nicht funktionierenden Prädikate zum Filtern von Daten

**Gilt für:** Foreign Plattform (z. B. Oracle, DB2, MySQL und Sybase) und [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration.

> [!NOTE]
> Für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migrationen, wenn dieses Problem in der Quelle vorhanden waren [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Migration auf eine neuere Version des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] als-wird dieses Szenario nicht berücksichtigen.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Der Abfrageoptimierer kann nur Informationen berücksichtigen, die zum Zeitpunkt der Kompilierung bekannt ist. Wenn eine arbeitsauslastung Prädikate, die nur zum Zeitpunkt der Ausführung bekannt sein kann abhängt, wird das Potenzial für schlechter Planauswahl erhöht. Für einen Plan höherer Qualität Prädikate muss **SARGable**, oder **S**uchen **Arg**u stornierende**können**.

Einige Beispiele für nicht-Prädikate:
-   Implizite datenkonvertierungen, wie z. B. VARCHAR, NVARCHAR oder INT varchar. Suchen Sie nach der Common Language Runtime CONVERT_IMPLICIT Warnungen in die tatsächliche Ausführungspläne. Konvertieren von einem Typ in einen anderen kann auch einem Genauigkeitsverlust führen.
-   Komplexe unbestimmt Ausdrücke wie z. B. `WHERE UnitPrice + 1 < 3.975`, aber nicht `WHERE UnitPrice < 320 * 200 * 32`.
-   Ausdrücke, die mithilfe von Funktionen, wie z. B. `WHERE ABS(ProductID) = 771` oder`WHERE UPPER(LastName) = 'Smith'`
-   Zeichenfolgen mit einem führenden Platzhalterzeichen, wie z. B. `WHERE LastName LIKE '%Smith'`, aber nicht `WHERE LastName LIKE 'Smith%'`.

### <a name="steps-to-resolve"></a>Schritte zum Beheben

1. Deklarieren Sie Variablen/Parameter immer als das vorgesehene Ziel [Datentyp](../t-sql/data-types/data-types-transact-sql.md). 
  -   Dazu kann gehören, vergleichen alle benutzerdefinierten Code-Konstrukt, das in der Datenbank (z. B. gespeicherte Prozeduren, benutzerdefinierte Funktionen oder Sichten) in Bezug auf Systemtabellen gespeichert ist, die Informationen zu Datentypen, die in der zugrunde liegenden Tabellen verwendeten enthalten (z. B. [sys.columns](../relational-databases/system-catalog-views/sys-columns-transact-sql.md)).
2. Wenn nicht der gesamte Code in den früheren Zustand zu durchlaufen, klicken Sie dann für den gleichen Zweck ändern Sie den Datentyp für die Tabelle entsprechend der Deklaration einer Variablen/Parameter.
3. Grund, die Nützlichkeit von den folgenden Konstrukten:
  -   Fungiert als Prädikate verwendet wird.
  -   Platzhaltersuchen;
  -   Komplexe Ausdrücke, die basierend auf Einspaltig Daten – bewerten die Notwendigkeit, stattdessen persistente berechnete Spalten erstellen indiziert werden können;

> [!NOTE] 
> Alle oben genannten Programmaticaly möglich.

## <a name="Table Valued Functions"></a>Verwendung von Tabellenwertfunktionen (mit mehreren Anweisungen Vs Inline)

**Gilt für:** Foreign Plattform (z. B. Oracle, DB2, MySQL und Sybase) und [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration.

> [!NOTE]
> Für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migrationen, wenn dieses Problem in der Quelle vorhanden waren [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Migration auf eine neuere Version des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] als-wird dieses Szenario nicht berücksichtigen.

Tabellenwertfunktionen zurückgeben einen Table-Datentyp, der eine Alternative zum Ansichten werden kann. Während der Sichten in einer einzelnen beschränkt sind `SELECT` -Anweisung, benutzerdefinierte Funktionen zusätzliche Anweisungen, die ermöglichen, weitere Logik als Sichten enthalten.

> [!IMPORTANT] 
> Da die Ausgabetabelle von einem MSTVF (mit mehreren Anweisungen Tabellenwertfunktion) nicht zum Zeitpunkt der Kompilierung erstellt wird die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Abfrageoptimierer stützt sich auf Heuristik und keine tatsächliche Netzwerkstatistiken, um die Zeile Einschätzung zu bestimmen. Auch wenn die Basistabellen Indizes hinzugefügt werden, ist dies nicht sehr helfen. Für MSTVFs [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwendet einen festen Schätzung 1 für die Anzahl der Zeilen von einer MSTVF zurückgegeben werden soll (beginnend mit [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] behobene Schätzung ist 100 Zeilen).

### <a name="steps-to-resolve"></a>Schritte zum Beheben
1.    Wenn die Tabellenwertfunktion mit mehreren Anweisungen nur einzelne Anweisung Inline TVF konvertiert wird.

    ```tsql
    CREATE FUNCTION dbo.tfnGetRecentAddress(@ID int)
    RETURNS @tblAddress TABLE
    ([Address] VARCHAR(60) NOT NULL)
    AS
    BEGIN
      INSERT INTO @tblAddress ([Address])
      SELECT TOP 1 [AddressLine1]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    RETURN
    END
    ```
    Aktion 

    ```tsql
    CREATE FUNCTION dbo.tfnGetRecentAddress_inline(@ID int)
    RETURNS TABLE
    AS
    RETURN (
      SELECT TOP 1 [AddressLine1] AS [Address]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    )
    ```

2.    Wenn komplexere, sollten erwägen Sie, Zwischenergebnisse gespeichert in speicheroptimierten Tabellen oder temporären Tabellen zu verwenden.

##  <a name="Additional_Reading"></a> Zusätzliches Lesematerial  
 [Bewährte Methoden für den Abfragespeicher](../relational-databases/performance/best-practice-with-the-query-store.md)  
[Speicheroptimierte Tabellen](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
[Benutzerdefinierte Funktionen](../relational-databases/user-defined-functions/user-defined-functions.md)  
[Tabellenvariablen und Zeile Einschätzung - Teil 1](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/11/30/table-variables-and-row-estimations-part-1/)  
[Tabellenvariablen und Zeile Einschätzung - Teil 2](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/12/09/table-variables-and-row-estimations-part-2/)  
[Des Zwischenspeicherns von Ausführungsplänen und Wiederverwendung](../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)

