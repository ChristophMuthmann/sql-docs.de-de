---
title: Datenbankkatalog | Microsoft Docs
ms.prod: world-wide-importers
ms.prod_service: sql-non-specified
ms.service: samples
ms.component: 
ms.technology: samples
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5ed65e42-527a-45e7-9a91-7179e892652e
caps.latest.revision: "2"
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 16606144dfc216d1da57386e97ee02b43691252b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="wideworldimportersdw-database-catalog"></a>Datenbankkatalog WideWorldImportersDW
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Erläuterungen für Schemas, Tabellen und gespeicherten Prozeduren in der Datenbank WideWorldImportersDW. 

Die WideWorldImportersDW-Datenbank ist für Datawarehousing und analytischen Verarbeitung verwendet. Transaktionsdaten zur und Verkäufe in der Datenbank "wideworldimporters" generiert und in die Datenbank mit WideWorldImportersDW geladen ist ein **tägliche ETL-Prozess**.

Die Daten in WideWorldImportersDW spiegelt daher die Daten in "wideworldimporters", aber die Tabellen anders angeordnet sind. WideWorldImportersDW wird verwendet, während "wideworldimporters" ein herkömmliches normalisiertes Schemas verfügt, die [Sternschema](https://wikipedia.org/wiki/Star_schema) Ansatz für den Tabellenentwurf. Neben den Tabellen Fakten- und Dimensionstabellen umfasst die Datenbank eine Reihe von Stagingtabellen, die verwendet werden, in die ETL-Prozess.

## <a name="schemas"></a>Schemas

Die verschiedenen Typen von Tabellen sind in drei Schemas organisiert.

|Schema|Description|
|-----------------------------|---------------------|
|Dimension|Dimensionstabellen.|
|Fakt|Faktentabellen.|  
|Integration|Staging-Tabellen und andere Objekte, die für ETL erforderlich sind.|  

## <a name="tables"></a>Tabellen

Die Dimensions- und Faktentabellen Tabellen sind unten aufgeführt. Die Tabellen im Schema Integration nur für ETL-Prozess verwendet werden und sind nicht aufgeführt.

### <a name="dimension-tables"></a>Dimensionstabellen

WideWorldImportersDW hat die folgenden Dimensionstabellen. Die Beschreibung umfasst die Beziehung mit den Quelltabellen in der Datenbank "wideworldimporters".

|Tabelle|Quelltabellen|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|Customer|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|Datum|Neue Tabelle mit Informationen zu Daten, einschließlich des Geschäftsjahres (basierend auf dem 1. November Geschäftsjahres starten).|
|Employee|`Application.People`.|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|Lieferanten|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`.|
|TransactionType|`Application.TransactionTypes`.|

### <a name="fact-tables"></a>Faktentabellen

WideWorldImportersDW hat die folgenden Faktentabellen. Die Beschreibung umfasst die Beziehung mit den Quelltabellen in der Datenbank "wideworldimporters" als auch die Klassen Analytics ist/Bericht erstattet Abfragen, die jede Faktentabelle in der Regel mit verwendet wird.

|Tabelle|Quelltabellen|Beispiel-Analysen|
|-----------------------------|---------------------|---------------------|
|Order|`Sales.Orders`und`Sales.OrderLines`|Sales Personen, Auswahl/Packer Produktivität, und wählen Sie die Aufträge auf Zeit. Darüber hinaus wenig stock Situationen zu Aufträgen zurück.|
|Ausverkauf|`Sales.Invoices`und`Sales.InvoiceLines`|Sales Datumsangaben, Lieferdaten, Rentabilität, mit der Zeit, Rentabilität vom Verkäufer.|
|Bestellung|`Purchasing.PurchaseOrderLines`|Erwarteten und tatsächlichen Lieferzeiten|
|Transaction|`Sales.CustomerTransactions`und`Purchasing.SupplierTransactions`|Messen von Problem Datumsangaben im Vergleich zur Finalisierung verfolgt Datumsangaben und Mengen.|
|Datenverschiebung|`Warehouse.StockTransactions`|-Bewegungen, die über die Zeit.|
|Vordefinierte Betrieb|`Warehouse.StockItemHoldings`|Verfügbare Lagerbestände und Wert.|

## <a name="stored-procedures"></a>Gespeicherte Prozeduren

Die gespeicherten Prozeduren werden in erster Linie für ETL-Prozess und Konfigurationszwecken verwendet.

Alle Erweiterungen des Beispiels werden empfohlen, mit der `Reports` Schema für Reporting Services-Berichte und die `PowerBI` Schema für Power BI den Zugriff.

### <a name="application-schema"></a>Anwendungsschema

Diese Prozeduren werden zum Konfigurieren des Beispiels verwendet. Sie werden verwendet, zum Anwenden von Funktionen der Enterprise Edition auf die standard Edition-Version des Beispiels, die PolyBase hinzufügen und neue Ausgangswerte zuzuweisen und ETL.

|Verfahren|Zweck|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|Wendet die Partitionierung und columnstore-Indizes für Faktentabellen.|
|Configuration_ConfigureForEnterpriseEdition|Wendet die Partitionierung, Columnstore-Index und in-Memory.|
|Configuration_EnableInMemory|Ersetzt die Stagingtabellen für die Integration mit SCHEMA_ONLY-Tabellen zum Verbessern der Leistung von ETL.|
|Configuration_ApplyPolybase|Konfiguriert eine externe Datenquelle, Dateiformat und Tabelle.|
|Configuration_PopulateLargeSaleTable|Enterprise Edition Änderungen übernommen, und füllt anschließend eine größere Menge an Daten für das Kalenderjahr 2012 als zusätzliche Verlauf.|
|Configuration_ReseedETL|Vorhandene Daten entfernt und neu gestartet wird der ETL-Ausgangswerte. Dies ermöglicht die OLAP-Datenbank für das streckungsschema an entsprechend der aktualisierte Zeilen in der OLTP-Datenbank.|

### <a name="integration-schema"></a>Integration Schema

In der ETL-Prozess verwendete Prozeduren fallen in den folgenden Kategorien:
- Hilfsprozeduren für ETL-Paket - alle Get * Prozeduren.
- Prozeduren, die von der ETL-Paket verwendet werden, für die Migration von bereitgestellten Daten in die Data Warehouse-Tabellen - alle migrieren * Prozeduren.
- `PopulateDateDimensionForYear`-Akzeptiert ein Jahr und stellt sicher, dass alle Datumsangaben für dieses Jahr, in aufgefüllt werden der `Dimension.Date` Tabelle.

### <a name="sequences-schema"></a>Sequenzen-Schema

Verfahren zum Konfigurieren von Sequenzen in der Datenbank.

|Verfahren|Zweck|
|-----------------------------|---------------------|
|ReseedAllSequences|Ruft die Prozedur `ReseedSequenceBeyondTableValue` für alle Sequenzen.|
|ReseedSequenceBeyondTableValue|Verwendet, um den nächsten Sequenzwert hinter dem Wert in einer beliebigen Tabelle neu zu positionieren, die die gleiche Sequenz verwendet. (Z. B. eine `DBCC CHECKIDENT` Identity-Spalten entsprechendes für Sequenzen jedoch auf potenziell mehrere Tabellen.)|
