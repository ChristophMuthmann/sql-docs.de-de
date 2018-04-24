---
title: Optimieren der JSON-Verarbeitung mit In-Memory-OLTP | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d9c5adb1-3209-4186-bc10-8e41a26f5e57
caps.latest.revision: 3
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3ababc8f8cd05e56c27b6b8d7478aaa5b8b98439
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="optimize-json-processing-with-in-memory-oltp"></a>Optimieren der JSON-Verarbeitung mit In-Memory-OLTP
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

SQL Server- und Azure SQL-Datenbanken ermöglichen die Verwendung von JSON-formatiertem Text. Sie können JSON-Dokumente mithilfe von Standardzeichenfolgenspalten (vom Typ NVARCHAR) in speicheroptimierten Tabellen speichern, um die Leistung der für die Verarbeitung von JSON-Daten verwendeten Abfragen zu verbessern. Beim Speichern von JSON-Daten in speicheroptimierten Tabellen wird die Abfrageleistung durch Nutzung eines ungehinderten Zugriffs auf In-Memory-Daten gesteigert.

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

## <a name="optimize-json-processing-with-additional-in-memory-features"></a>Optimieren der JSON-Verarbeitung mit zusätzlichen In-Memory-Funktionen
Mithilfe der in SQL Server- und Azure SQL-Datenbanken enthaltenen neuen Funktionen können Sie JSON-Funktionen umfassend in bestehende In-Memory-OLTP-Technologien einbinden. Sie haben beispielsweise folgende Möglichkeiten:
 - [Überprüfen Sie die Struktur von JSON-Dokumenten](#validate), die in speicheroptimierten Tabellen gespeicherten sind, mithilfe nativ kompilierter CHECK-Einschränkungen.
 - [Machen Sie in JSON-Dokumenten gespeicherte Werte verfügbar und versehen Sie sie mit einer starken Typisierung](#computedcol). Verwenden Sie hierzu berechnete Spalten.
 - [Indizieren Sie Werte](#index) in JSON-Dokumenten mithilfe von speicheroptimierten Indizes.
 - [Führen Sie für SQL-Abfragen eine native Kompilierung durch](#compile), in denen Werte aus JSON-Dokumenten verwendet werden, oder formatieren Sie Ergebnisse als JSON-Text.

## <a name="validate"></a> Überprüfen von JSON-Spalten
Mithilfe von SQL Server- und Azure SQL-Datenbanken können Sie nativ kompilierte CHECK-Einschränkungen hinzufügen, mit denen der in einer Zeichenfolgenspalte gespeicherte Inhalt von JSON-Dokumenten überprüft werden kann. Mit nativ kompilierten JSON CHECK-Einschränkungen können Sie sicherstellen, dass in Ihren speicheroptimierten Tabellen gespeicherter JSON-Text ordnungsgemäß formatiert wird.

Im folgenden Beispiel wird eine `Product`-Tabelle mit einer JSON-Spalte `Tags` erstellt. Die `Tags`-Spalte weist eine CHECK-Einschränkung auf, die die `ISJSON`-Funktion verwendet, um den JSON-Text in der Spalte zu überprüfen.

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

Sie können zudem die nativ kompilierte CHECK-Einschränkung in vorhandenen Tabellen hinzufügen, die JSON-Spalten enthalten.

```sql
ALTER TABLE xtp.Product
    ADD CONSTRAINT [Data should be JSON]
        CHECK (ISJSON(Data)=1)
```

## <a name="computedcol"></a> Verfügbarmachen von JSON-Werte mithilfe von berechneten Spalten
Mithilfe von berechneten Spalten können Sie Werte aus JSON-Text verfügbar machen und auf diese Werte zugreifen, ohne dass der Wert aus dem JSON-Text erneut abgerufen, erneut ausgewertet und ohne dass die JSON-Struktur erneut analysiert wird. Derartig verfügbar gemachte Werte sind mit einer starken Typisierung versehen und in den berechneten Spalten physisch persistent. Auf JSON-Werte kann mithilfe von permanent berechneten Spalten schneller zugegriffen werden als der direkte Zugriff auf Werte im JSON-Dokument.

Im folgenden Beispiel werden die beiden folgenden Werte aus der JSON `Data`-Spalte verfügbar gemacht:
-   Das Land, in dem ein Produkt hergestellt wird
-   Die Herstellungskosten für das Produkt.

In diesem Beispiel werden die berechneten Spalten `MadeIn` und `Cost` jedes Mal aktualisiert, wenn sich das in der Spalte `Data` gespeicherte JSON-Dokument ändert.

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

## <a name="index"></a> Indexwerte in JSON-Spalten
Bei SQL Server- und Azure SQL-Datenbank können Sie Werte in JSON-Spalten mithilfe von speicheroptimierten Indizes indizieren. Indizierte JSON-Werte müssen wie im vorherigen Beispiel mithilfe von berechneten Spalten verfügbar gemacht und mit einer starken Typisierung versehen werden.

Werte in JSON-Spalten können sowohl mit Standard-NONCLUSTERED- als auch mit HASH-Indizes indiziert werden.
-   Mit NONCLUSTERED-Indizes werden Abfragen optimiert, mit denen Zeilenbereiche nach JSON-Werten ausgewählt werden oder mit denen Ergebnisse nach JSON-Werten sortiert werden.
-   HASH-Indizes optimieren Abfragen, die eine einzelne Zeile oder einige Zeilen auswählen, indem sie einen genauen zu suchenden Wert angeben.

Im folgenden Beispiel wird eine Tabelle erstellt, die JSON-Werte verfügbar macht, indem sie zwei berechnete Spalten verwendet. In dem Beispiel wird ein NONCLUSTERED-Index auf einem JSON-Wert erstellt und ein HASH-Index auf einem anderen.

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

## <a name="compile"></a> Native Kompilierung von JSON-Abfragen
Wenn Ihre Prozeduren, Funktionen und Trigger Abfragen enthalten, die die integrierte JSON-Funktion verwenden, verbessert die native Kompilierung die Leistung dieser Abfragen und vermindert die für deren Ausführung erforderlichen CPU-Zyklen.

Im folgenden Beispiel ist eine nativ kompilierte Prozedur dargestellt, die verschiedene JSON-Funktionen enthält: **JSON_VALUE**, **OPENJSON** und **JSON_MODIFY**.

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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Weitere Informationen zu JSON in SQL Server und Azure SQL-Datenbank  
  
### <a name="microsoft-blog-posts"></a>Microsoft-Blogbeiträge  
  
Spezielle Lösungen, Anwendungsfälle und Empfehlungen finden Sie in den [Blogbeiträgen über die integrierte JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL-Server und in Azure SQL-Datenbank.  

### <a name="microsoft-videos"></a>Microsoft-Videos

Eine visuelle Einführung in die JSON-Unterstützung, die in SQL Server und Azure SQL-Datenbank integriert ist, finden Sie in den folgenden Videos:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
