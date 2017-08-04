---
title: Verwendung von SQL Server-Features und Funktionen | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7cbfb4ef-1e61-4e65-9fe0-ed5adfb43415
caps.latest.revision: 3
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 66fe9487c8b7d2189d69917fc81226a4f698af7c
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>WideWorldImportersDW Verwendung von SQL Server-Features und Funktionen
WideWorldImportersDW dient zum Großteil der wichtigsten Funktionen von SQL Server zu präsentieren, die für Data Warehouse- und Analysen geeignet sind. Im folgenden wird eine Liste der SQL Server-Features und Funktionen und eine Beschreibung, wie sie in WideWorldImportersDW verwendet werden.

## <a name="polybase"></a>PolyBase

[Gilt für SQL Server (2016 und höher)]

PolyBase dient zum Kombinieren von Umsatzdaten aus WideWorldImportersDW mit einem öffentlichen DataSet zu demografischen Daten, um zu verstehen, welche Städte von für eine weitere Erweiterung der Verkäufe sein könnten.

Um die Verwendung von PolyBase in der Beispieldatenbank zu aktivieren, stellen Sie sicher, dass es installiert ist, und führen Sie die folgende gespeicherte Prozedur in der Datenbank:

    EXEC [Application].[Configuration_ApplyPolybase]

Dadurch wird eine externe Tabelle erstellt `dbo.CityPopulationStatistics` , die auf eine öffentliche Daten Gruppe mit Auffüllung Daten für Städte in den USA gehostet, die im Azure-Blob-Speicher verweist. Es wird empfohlen, den Code in der gespeicherten Prozedur, um den Konfigurationsvorgang zu verstehen, zu überprüfen. Wenn Sie hosten Ihre eigenen Daten im Azure-Blob-Speicher und von allgemeinen öffentlichen Zugriff schützen möchten, müssen Sie zusätzliche Konfigurationsschritte durchführen. Die folgende Abfrage gibt die Daten aus diesem externen DataSet zurück:

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

Um zu verstehen, welche Städte von für eine weitere Erweiterung sein könnten, die folgende Abfrage prüft die Wachstumsrate des Städte, und gibt die ersten 100 größten Orten mit erheblichen Vergrößerung und Wide World Importers verfügt, in denen nicht über eine sales Präsenz. Die Abfrage umfasst einen Join zwischen der Remotetabelle `dbo.CityPopulationStatistics` und die lokale Tabelle `Dimension.City`, und einen Filter, die im Zusammenhang mit der lokalen Tabelle `Fact.Sales`.

    WITH PotentialCities
    AS
    (
        SELECT cps.CityName,
               cps.StateProvinceCode,
               MAX(cps.LatestRecordedPopulation) AS PopulationIn2016,
               (MAX(cps.LatestRecordedPopulation) - MIN(cps.LatestRecordedPopulation)) * 100.0
                   / MIN(cps.LatestRecordedPopulation) AS GrowthRate
        FROM dbo.CityPopulationStatistics AS cps
        WHERE cps.LatestRecordedPopulation IS NOT NULL
        AND cps.LatestRecordedPopulation <> 0
        GROUP BY cps.CityName, cps.StateProvinceCode
    ),
    InterestingCities
    AS
    (
        SELECT DISTINCT pc.CityName,
                        pc.StateProvinceCode,
                        pc.PopulationIn2016,
                        FLOOR(pc.GrowthRate) AS GrowthRate
        FROM PotentialCities AS pc
        INNER JOIN Dimension.City AS c
        ON pc.CityName = c.City
        WHERE GrowthRate > 2.0
        AND NOT EXISTS (SELECT 1 FROM Fact.Sale AS s WHERE s.[City Key] = c.[City Key])
    )
    SELECT TOP(100) CityName, StateProvinceCode, PopulationIn2016, GrowthRate
    FROM InterestingCities
    ORDER BY PopulationIn2016 DESC;

## <a name="clustered-columnstore-indexes"></a>Gruppierte Columnstore-Indizes

(Vollständige Version des Beispiels)

Gruppierte columnstore-Indizes (CCI) sind mit alle Faktentabellen verwendet, um den Speicherplatzbedarf verringern und die abfrageleistung. Bei Verwendung von CCI verwendet der Basis Speicher für den Faktentabellen Komprimierung der Spalte.

Nicht gruppierte Indizes werden zusätzlich zu den gruppierten columnstore-Index verwendet, um die primary key- und foreign Key-Einschränkungen zu ermöglichen. Diese Einschränkungen wurden hinzugefügt, aus einer Fülle von Vorsicht - ETL-Prozess Datenquellen die Daten aus der Datenbank "wideworldimporters", mit Einschränkungen zum Erzwingen der Integrität. Entfernen von primären und foreign Key-Einschränkungen und deren unterstützende Indizes würde den Speicher der Faktentabellen zu verkleinern.

**Datengröße**

Die Beispieldatenbank eingeschränkter Datengröße zum Herunterladen und installieren Sie das Beispiel zu vereinfachen. Allerdings würde die tatsächliche Leistungsvorteile von columnstore-Indizes finden Sie ein größeres DataSet verwenden möchten.

Sie können die folgende Anweisung zum Vergrößern Ausführen der `Fact.Sales` Tabelle durch eine andere 12 Millionen Zeilen mit Beispieldaten einfügen. Diese Zeilen werden alle für das Jahr 2012 eingefügt, dass keine Störungen mit ETL-Prozess vorhanden ist.

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

Diese Anweisung dauert etwa 5 Minuten ausgeführt. Um mehr als 12 Millionen Zeilen einzufügen, übergeben Sie die gewünschte Anzahl von Zeilen, die als Parameter dieser gespeicherten Prozedur eingefügt.

Um die abfrageleistung mit und ohne Columnstore zu vergleichen, können Sie löschen und/oder erstellen Sie den gruppierten columnstore-Index neu.

So löschen Sie den Index:

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

Um erneut zu erstellen:

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>Partitionierung

(Vollständige Version des Beispiels)

Größe der Daten in einem Data Warehouse kann sehr groß werden. Aus diesem Grund ist es die bewährte Methode, die Verwendung der Partitionierung zum Verwalten der Speicherung von die großen Tabellen in der Datenbank.

Alle von der größeren Faktentabellen sind nach Jahr aufgeteilt. Die einzige Ausnahme ist `Fact.Stock Holdings`, dies ist kein datumsbasierte und verfügt über eingeschränkten Datengröße verglichen mit den anderen Faktentabellen.

Wird für alle partitionierten Tabellen verwendete Partitionsfunktion `PF_Date`, und das Partitionsschema verwendeten `PS_Date`.

## <a name="in-memory-oltp"></a>In-Memory OLTP

(Vollständige Version des Beispiels)

WideWorldImportersDW verwendet SCHEMA_ONLY-Tabellen für das staging-Tabellen. Alle `Integration.` * `_Staging` Tabellen sind SCHEMA_ONLY Speicheroptimierte Tabellen.

Der Vorteil, dass SCHEMA_ONLY-Tabellen ist, dass sie nicht angemeldet sind, und Zugriff auf die Festplatte ist nicht erforderlich. Dies verbessert die Leistung des ETL-Prozesses. Da diese Tabellen nicht angemeldet sind, werden Sie in ihren Inhalt verloren, wenn ein Fehler auftritt. Die Datenquelle ist jedoch weiterhin verfügbar, damit ETL-Prozess einfach neu gestartet werden kann, wenn ein Fehler auftritt.

