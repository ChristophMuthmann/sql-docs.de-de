---
title: Optimieren der JSON-Verarbeitung mit In-Memory-OLTP | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d9c5adb1-3209-4186-bc10-8e41a26f5e57
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4e0331c288665fd9f69444d0d14366dfa69a668f
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="optimize-json-processing-with-in-memory-oltp"></a>Optimieren der JSON-Verarbeitung mit In-Memory-OLTP
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

SQL Server- und Azure SQL-Datenbanken ermöglichen die Verwendung von JSON-formatiertem Text. Sie können JSON-Dokumente mithilfe von standardmäßigen Zeichenfolgenspalten (vom Typ NVARCHAR) in speicheroptimierten Tabellen speichern, um die Leistung der für die Verarbeitung von JSON-Daten verwendeten OLTP-Abfragen zu verbessern.

## <a name="store-json-in-memory-optimized-tables"></a>Speichern von JSON-Daten in speicheroptimierten Tabellen
Im folgenden Beispiel wird eine speicheroptimierte `Product`-Tabelle mit zwei JSON-Spalten, `Tags` und `Data`, erstellt:

```sql
CREATE SCHEMA xtp;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED, --standard column
    Name nvarchar(400) NOT NULL, --standard column
    Price float, --standard column

    Tags nvarchar(400),--json stored in string column
    Data nvarchar(4000) --json stored in string column

) WITH (MEMORY_OPTIMIZED=ON);
```
Beim Speichern von JSON-Daten in speicheroptimierten Tabellen wird die Abfrageleistung durch Nutzung eines ungehinderten Zugriffs auf In-Memory-Daten gesteigert.

## <a name="optimize-json-with-additional-in-memory-features"></a>Optimieren von JSON-Daten mit zusätzlichen In-Memory-Funktionen
Mithilfe der in SQL Server- und Azure SQL-Datenbanken enthaltenen neuen Funktionen können Sie JSON-Funktionen umfassend in bestehende In-Memory-OLTP-Technologien einbinden. Sie haben beispielsweise folgende Möglichkeiten:
 - Überprüfen Sie die Struktur von in speicheroptimierten Tabellen gespeicherten JSON-Dokumenten mithilfe nativ kompilierter CHECK-Einschränkungen.
 - Machen Sie in JSON-Dokumenten gespeicherte Werte verfügbar und versehen Sie sie mit einer starken Typisierung. Verwenden Sie hierzu berechnete Spalten.
 - Indizieren Sie Werte in JSON-Dokumenten mithilfe von speicheroptimierten Indizes.
 - Führen Sie für SQL-Abfragen, in denen Werte aus JSON-Dokumenten verwendet werden, eine native Kompilierung durch, oder formatieren Sie Ergebnisse als JSON-Text.

## <a name="validate-json-columns"></a>Überprüfen von JSON-Spalten
Mithilfe von SQL Server- und Azure SQL-Datenbanken können Sie wie im folgenden Beispiel nativ kompilierte CHECK-Einschränkungen hinzufügen, mit denen der in einer Zeichenfolgenspalte gespeicherte Inhalt von JSON-Dokumenten überprüft werden kann.

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Tags nvarchar(400)
            CONSTRAINT [Tags should be formatted as JSON]
                CHECK (ISJSON(Tags)=1),
    Data nvarchar(4000)

) WITH (MEMORY_OPTIMIZED=ON);
```

Die nativ kompilierte CHECK-Einschränkung kann in vorhandenen Tabellen hinzugefügt werden, die JSON-Spalten enthalten:

```sql
ALTER TABLE xtp.Product
    ADD CONSTRAINT [Data should be JSON]
        CHECK (ISJSON(Data)=1)
```

Mit nativ kompilierten JSON CHECK-Einschränkungen können Sie sicherstellen, dass in Ihren speicheroptimierten Tabellen gespeicherter JSON-Text ordnungsgemäß formatiert wird.

## <a name="expose-json-values-using-computed-columns"></a>JSON-Werte mithilfe von berechneten Spalten verfügbar machen
Mithilfe von berechneten Spalten können Sie Werte aus JSON-Text verfügbar machen und auf diese Werte zugreifen, ohne die Ausdrücke, mit denen ein Wert aus dem JSON-Text abgerufen wird, erneut auszuwerten und ohne die JSON-Struktur erneut zu analysieren. Verfügbar gemachte Werte sind mit einer starken Typisierung versehen und in den berechneten Spalten physisch persistent. Auf JSON-Werte kann mithilfe von permanent berechneten Spalten schneller zugegriffen werden als auf Werte im JSON-Dokument.

Im folgenden Beispiel werden die beiden folgenden Werte aus der JSON `Data`-Spalte verfügbar gemacht:
-   Das Land, in dem ein Produkt hergestellt wird.
-   Die Herstellungskosten für das Produkt.

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float)

) WITH (MEMORY_OPTIMIZED=ON);
```

Die berechneten Spalten `MadeIn` und `Cost` werden jedes Mal aktualisiert, wenn sich das in der Spalte `Data` gespeicherte JSON-Dokument ändert.

## <a name="index-values-in-json-columns"></a>Indexwerte in JSON-Spalten
Bei SQL Server- und Azure SQL-Datenbanken können Sie Werte in JSON-Spalten mithilfe von speicheroptimierten Indizes indizieren. Indizierte JSON-Werte müssen wie im folgenden Beispiel mithilfe von berechneten Spalten verfügbar gemacht und mit einer starken Typisierung versehen werden.

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float) PERSISTED,

    INDEX [idx_Product_MadeIn] NONCLUSTERED (MadeIn)

) WITH (MEMORY_OPTIMIZED=ON)

ALTER TABLE Product
    ADD INDEX [idx_Product_Cost] NONCLUSTERED HASH(Cost)
        WITH (BUCKET_COUNT=20000)
```
Werte in JSON-Spalten können sowohl mit standardmäßigen NONCLUSTERED- als auch mit HASH-Indizes indiziert werden.
-   Mit NONCLUSTERED-Indizes werden Abfragen optimiert, mit denen Zeilenbereiche nach JSON-Werten ausgewählt werden oder mit denen Ergebnisse nach JSON-Werten sortiert werden.
-   HASH-Indizes zeigen eine optimale Leistung, wenn eine einzelne Zeile oder wenige Zeilen durch Angabe des exakten Suchwerts abgerufen werden.

## <a name="native-compilation-of-json-queries"></a>Native Kompilierung von JSON-Abfragen
Durch die native Kompilierung von Transact-SQL-Prozeduren, -Funktionen und -Triggern, die Abfragen mit JSON-Funktionen enthalten, wird die Abfrageleistung gesteigert und die zum Ausführen der Prozeduren erforderlichen CPU-Zyklen werden reduziert. Im folgenden Beispiel ist eine nativ kompilierte Prozedur dargestellt, die verschiedene JSON-Funktionen enthält: JSON_VALUE, OPENJSON und JSON_MODIFY.

```sql
CREATE PROCEDURE xtp.ProductList(@ProductIds nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    SELECT ProductID,Name,Price,Data,Tags, JSON_VALUE(data,'$.MadeIn') AS MadeIn
    FROM xtp.Product
        JOIN OPENJSON(@ProductIds)
            ON ProductID = value

END;

CREATE PROCEDURE xtp.UpdateProductData(@ProductId int, @Property nvarchar(100), @Value nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    UPDATE xtp.Product
    SET Data = JSON_MODIFY(Data, @Property, @Value)
    WHERE ProductID = @ProductId;

END
```

## <a name="next-steps"></a>Nächste Schritte
JSON-Daten in nativen In-Memory-OLTP-Modulen bedeuten für die in SQL Server und Azure SQL-Datenbanken integrierte JSON-Funktion eine deutliche Leistungssteigerung.

Weitere Informationen zu den Kernszenarios für die Verwendung von JSON finden Sie in den folgenden Ressourcen:

-   [TechNet-Blog](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
-   [MSDN-Dokumentation](https://msdn.microsoft.com/library/dn921897.aspx)
-   [Channel 9-Video](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

Informationen zu verschiedenen Szenarios zur Integration von JSON in Ihre Anwendung finden Sie in den folgenden Ressourcen:
-   Sehen Sie sich die Demos in diesem [Channel 9-Video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) an.
-   In den [JSON-Blogbeiträgen](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) finden Sie Szenarios für Ihren Anwendungsfall.
-   In unserem [GitHub-Repository](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/json/) finden Sie entsprechende Beispiele.


