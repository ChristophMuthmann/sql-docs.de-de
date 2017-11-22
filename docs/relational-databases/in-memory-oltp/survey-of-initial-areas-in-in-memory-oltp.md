---
title: "Schnellstart 1: In-Memory-OLTP-Technologien für höhere Transact-SQL-Leistung | Microsoft Dokumentation"
ms.custom: 
ms.date: 09/05/2017"
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1c25a164-547d-43c4-8484-6b5ee3cbaf3a
caps.latest.revision: "31"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ee66a454da8bfdc23e9beb382c0ac22939268e80
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="survey-of-initial-areas-in-in-memory-oltp"></a>Überblick des Anfangsbereichs in In-Memory OLTP
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  
Dieser Artikel ist für Entwickler konzipiert, die schnell die Grundlagen der In-Memory-OLTP-Leistungsmerkmale von Microsoft SQL Server und der Azure SQL-Datenbank lernen möchten.  
  
Dieser Artikel bietet für In-Memory-OLTP Folgendes:  
  
- Eine kurze Erklärung der Funktionen  
- Core-Codebeispiele, die die Funktionen implementieren  
  
  
SQL Server und die SQL-Datenbank haben nur geringfügige Unterschiede bei ihrer Unterstützung der In-Memory-Technologien.  
  
  
In der Praxis verwenden Blogger für die In-Memory-OLTP-Funktionen auch den Begriff *Hekaton*.  
  
  
<a name="benefits-of-in-memory-features-21a"></a>  
  
## <a name="benefits-of-in-memory-features"></a>Vorteile der In-Memory-Funktionen  
  
SQL Server bietet In-Memory-Funktionen, die die Leistung von vielen Anwendungssystemen erheblich verbessern können. In diesem Abschnitt werden die häufigsten unkomplizierten Aspekte beschrieben.  
  
  
### <a name="features-for-oltp-online-transactional-processing"></a>Funktionen für OLTP (Online Transactional Processing – Onlinetransaktionsverarbeitung)  
  
  
Systeme, die eine große Anzahl von SQL INSERT-Anweisungen gleichzeitig verarbeiten müssen, sind eine ausgezeichnete Wahl für die OLTP-Funktionen.  
  
- Unsere Vergleichtests zeigen, dass Verbesserungen der Geschwindigkeit um das 5- bis 20-fache möglich sind, wenn die In-Memory-Funktionen angewendet werden.  
  
  
Systeme, die hohe Berechnungen in Transact-SQL ausführen, sind eine ausgezeichnete Wahl.  
  
- Eine gespeicherte Prozedur, die für hohe Berechnungen vorgesehen ist, kann bis zu 99-mal schneller ausgeführt werden.  
  
  
Sie können sich später die folgenden Artikel ansehen, die Demonstrationen der Leistungsgewinne durch In-Memory-OLTP bieten:  
  
- [Demo: Leistungsverbesserungen von In-Memory-OLTP](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md) bietet eine kleine Demonstration der größeren potenziellen Leistungsgewinne.  
- [Sample Database for In-Memory-OLTP](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md) (Beispieldatenbank für In-Memory-OLTP) bietet eine genauere Erläuterung.  
  
  
  
### <a name="features-for-operational-analytics"></a>Funktionen für die operative Analyse  
  
In-Memory-Analyse bezieht sich auf SQL SELECT-Anweisungen, die in der Regel Transaktionsdaten durch Inklusion einer GROUP BY-Klausel aggregieren. Der Indextyp heißt *columnstore* und ist ein wesentlicher Bestandteil der operativen Analyse.  
  
Es gibt zwei wichtige Szenarios:  
  
- *Operative Analyseprozesse im Batchmodus* verweist auf Aggregationsprozesse, die entweder nach den Geschäftsstunden ausgeführt werden oder auf sekundärer Hardware, die über Kopien der Transaktionsdaten verfügt.  
  - [Azure SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-what-is/) bezieht sich auch auf operative Analyseprozesse, die im Batchmodus ausgeführt werden.  
- *Operative Echtzeitanalyse* verweist auf Aggregationsprozesse, die entweder während der Geschäftsstunden ausgeführt werden oder auf der primären Hardware, die für Transaktionsarbeitsauslastung verwendet wird.  
  
  
Dieser Artikel fokussiert sich auf OLTP und nicht auf Analyseaufgaben. Informationen darüber, wie Columnstore-Indizes Analytics auf SQL überträgt, finden Sie unter:  
  
- [Erste Schritte mit Columnstore für operative Echtzeitanalyse](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
- [Beschreibung von Columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-overview.md)  
  
  
> [!NOTE]
> Ein zwei-Minuten-Video zu den In-Memory-Funktionen finden Sie unter [Azure SQL Database - In-Memory Technologies](http://channel9.msdn.com/Blogs/Windows-Azure/Azure-SQL-Database-In-Memory-Technologies)(Azure SQL-Datenbank – In-Memory-Technologien) Das Video ist von Dezember 2015.  


### <a name="columnstore"></a>columnstore

Eine Reihe exzellenter Blogbeiträge erklärt Ihnen aus verschiedenen Blickwinkeln Columnstore-Indizes auf leicht verständliche Art und Weise. In den meisten dieser Beiträge wird auch das von Columnstore unterstützte Konzept der operativen Echtzeitanalyse genauer beschrieben.  Diese Beiträge wurden im März 2016 von Sunil Agarwal, Program Manager bei Microsoft, verfasst.

#### <a name="real-time-operational-analytics"></a>Operative Echtzeitanalyse

1. [Real-Time Operational Analytics Using In-Memory Technology (Operative Echtzeitanalyse mit In-Memory-Technologie)](https://blogs.technet.microsoft.com/dataplatforminsider/2015/12/09/real-time-operational-analytics-using-in-memory-technology/)
2. [Real-Time Operational Analytics – Overview nonclustered columnstore index (NCCI) (Operative Echtzeitanalyse – Überblick über den nicht gruppierten Columnstore-Index [Nonclustered Columnstore Index, NCCI])](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-using-nonclustered-columnstore-index/)
3. [Real-Time Operational Analytics: Simple example using nonclustered clustered columnstore index (NCCI) in SQL Server 2016 (Operative Echtzeitanalyse: Einfaches Beispiel mit Verwendung des gruppierten/nicht gruppierten Columnstore-Index [Nonclustered Columnstore Index, NCCI] in SQL Server 2016)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-simple-example-using-nonclustered-clustered-columnstore-index-ncci/)
4. [Real-Time Operational Analytics: DML operations and nonclustered columnstore index (NCCI) in SQL Server 2016 (Operative Echtzeitanalyse: DML-Operationen und nicht gruppierter Columnstore-Index [Nonclustered Columnstore Index, NCCI] in SQL Server 2016)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/04/real-time-operational-analytics-dml-operations-and-nonclustered-columnstore-index-ncci-in-sql-server-2016/)
5. [Real-Time Operational Analytics: Filtered nonclustered columnstore index (NCCI) (Operative Echtzeitanalyse: Gefilterter, nicht gruppierter Columnstore-Index [Nonclustered Columnstore Index, NCCI])](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-filtered-nonclustered-columnstore-index-ncci/)
6. [Real-Time Operational Analytics: Compression Delay Option for Nonclustered Columnstore Index (NCCI) (Operative Echtzeitanalyse: Die Option Kompressionsverzögerung für einen nicht gruppierten Columnstore-Index [Nonclustered Columnstore Index, NCCI])](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-for-nonclustered-columnstore-index-ncci/)
7. [Real-Time Operational Analytics: Compression Delay option with NCCI and the performance (Operative Echtzeitanalyse: Performance des nicht gruppierten Columnstore-Index [Nonclustered Columnstore Index, NCCI] mit aktivierter Option „Kompressionsverzögerung“)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-with-ncci-and-the-performance/)
8. [Real-Time Operational Analytics: Memory-Optimized Tables and Columnstore Index (Operative Echtzeitanalyse: Speicheroptimierte Tabellen und der Columnstore-Index)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/real-time-operational-analytics-memory-optimized-table-and-columnstore-index/)

#### <a name="defragment-a-columnstore-index"></a>Defragmentieren eines Columnstore-Index

1. [Columnstore Index Defragmentation using REORGANIZE Command (Defragmentieren des Columnstore-Index mithilfe des Befehls REORGANIZE)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)
2. [Columnstore Index Merge Policy for REORGANIZE (Zusammenführungsrichtlinie für REORGANIZE des Columnstore-Index)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)

#### <a name="bulk-importation-of-data"></a>Ausführen eines Massenimports von Daten

1. [Clustered Column Store: Bulk Load (Gruppierter Columnstore-Index: Massenladen)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2014/07/27/clustered-column-store-index-bulk-loading-the-data/)
2. [Clustered Columnstore Index: Data Load Optimizations – Minimal Logging (Gruppierter Columnstore-Index: Optimieren des Ladens von Daten – Minimale Protokollierung)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/10/clustered-columnstore-index-data-load-optimizations-minimal-logging/)
3. [Clustered Columnstore Index: Data Load Optimizations – Parallel Bulk Import (Gruppierter Columnstore-Index: Optimieren des Ladens von Daten – Paralleles Massenladen)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/28/clustered-columnstore-index-parallel-bulk-import/)





<a name="features-on-in-memory-oltp-13b"></a>  
  
## <a name="features-of-in-memory-oltp"></a>Funktionen von In-Memory-OLTP  
  
Betrachten wir nun die wichtigsten Funktionen von In-Memory-OLTP.  
  
  
#### <a name="memory-optimized-tables"></a>Speicheroptimierte Tabellen  
  
Das T-SQL-Schlüsselwort MEMORY_OPTIMIZED in der CREATE TABLE-Anweisung zeigt wie eine Tabelle erstellt wird, um im aktiven Arbeitsspeicher zu existieren, anstatt auf dem Datenträger.  
  
  
Eine [speicheroptimierte Tabelle](../../relational-databases/in-memory-oltp/memory-optimized-tables.md) hat eine Darstellung von sich selbst im aktiven Arbeitsspeicher und eine sekundäre Kopie auf dem Datenträger.  
  
- Die Kopie auf dem Datenträger ist für die routinemäßige Wiederherstellung nach einem Herunterfahren und anschließendem Neustart des Servers oder der Datenbank. Diese In-Memory-plus-Datenträger-Dualität ist vollständig unsichtbar für Sie und Ihren Code.  
  
  
#### <a name="natively-compiled-modules"></a>Nativ kompilierte Module  
  
Das T-SQL-Schlüsselwort NATIVE_COMPILATION in der CREATE PROCEDURE-Anweisung zeigt, wie eine nativ kompilierte gespeicherte Prozedur erstellt wird. Die T-SQL-Anweisungen werden jedes Mal bei der ersten Verwendung der nativen Prozedur in Computercode kompiliert, wenn die Datenbank erneut online gestellt wird. Die T-SQL-Anweisungen erdulden nicht länger das langsame Interpretieren jeder Anweisung.  
  
- Es kann vorkommen, dass diese Kompilierung (nativ) nur 1 % der Zeit benötigt, die für eine interpretierte gespeicherte Prozedur benötigt wird.  
  
  
Ein natives Modul kann nur speicheroptimierte Tabellen verweisen. Sie kann keine datenträgerbasierten Tabellen verweisen.  
  
Es gibt drei Arten von nativ kompilierten Modulen:  
  
- [Nativ kompilierte gespeicherte Prozeduren](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
- Nativ kompilierte benutzerdefinierte Funktionen (UDFs), die skalare sind.  
- Nativ kompilierte Trigger.  
  
  
#### <a name="availability-in-azure-sql-database"></a>Verfügbarkeit in Azure SQL-Datenbank  
  
In-Memory-OLTP und Columnstore sind in Azure SQL-Datenbank verfügbar. Weitere Informationen finden Sie unter [Optimieren der Leistung mithilfe von In-Memory-Technologien in SQL-Datenbank](https://docs.microsoft.com/azure/sql-database/sql-database-in-memory).
  
  
<a name="ensure-compatibility-level-gteq-130-99c"></a>  
  
## <a name="1-ensure-compatibility-level--130"></a>1. Sicherstellen, dass der Kompabilitätsgrad >= 130 ist  
  
  
Dieser Abschnitt beginnt mit einer Sequenz von nummerierten Abschnitten, die zusammen die Transact-SQL-Syntax veranschaulicht, die Sie verwenden können, um In-Memory-OLTP-Funktionen zu implementieren.  
  
  
Zuerst ist es wichtig, dass Ihre Datenbank auf einen Kompatibilitätsgrad von mindestens 130 festgelegt ist. Als Nächstes wird der T-SQL-Code verwendet, um den aktuellen Kompatibilitätsgrad anzuzeigen, auf den Ihre aktuelle Datenbank festgelegt ist.  
  
  
  
  
  
    SELECT d.compatibility_level  
        FROM sys.databases as d  
        WHERE d.name = Db_Name();  
  
  
  
  
Danach wird der T-SQL-Code verwendet, um den Grad wenn nötig zu aktualisieren.  
  
  
  
  
    ALTER DATABASE CURRENT  
        SET COMPATIBILITY_LEVEL = 130;  
  
  
  
  
<a name="elevate-to-snapshot-26n"></a>  
  
## <a name="2-elevate-to-snapshot"></a>2. Erhöhen auf Momentaufnahme  
  
  
Wenn eine Transaktion jeweils eine datenträgerbasierte Tabelle und eine speicheroptimierte Tabelle einschließt, nennen wir dies eine *containerübergreifende Transaktion*. In einer solchen Transaktion ist es wichtig, dass der speicheroptimierte Teil der Transaktion auf der Transaktionsisolationsstufe namens SNAPSHOT ausgeführt wird.  
  
Um diese Stufe für speicheroptimierte Tabellen in einer containerübergreifenden Transaktion zuverlässig zu erzwingen, [ändern Sie Ihre Datenbankeinstellung](../../t-sql/statements/alter-database-transact-sql-set-options.md) durch das Ausführen der folgenden T-SQL.  
  
  
  
  
    ALTER DATABASE CURRENT  
        SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;  
  
  
  
  
<a name="create-an-optimized-filegroup-24r"></a>  
  
## <a name="3-create-an-optimized-filegroup"></a>3. Erstellen einer optimierten FILEGROUP  
  
  
Auf Microsoft SQL Server müssen Sie vor der Erstellung einer speicheroptimierten Tabelle zunächst eine FILEGROUP erstellen und für diese die Angabe CONTAINS MEMORY_OPTIMIZED_DATA vornehmen. Die FILEGROUP wird Ihrer Datenbank zugewiesen. Einzelheiten dazu finden Sie unter:  
  
- [Die speicheroptimierte FILEGROUP](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)  
  
  
Auf Azure SQL-Datenbank können und brauchen Sie keine solche FILEGROUP erstellen.  

Das folgende T-SQL-Beispielskript aktiviert eine Datenbank für In-Memory-OLTP und konfiguriert alle empfohlene Einstellungen. Es funktioniert mit SQL Server und Azure SQL-Datenbank: [enable-in-memory-oltp.sql](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql).

Beachten Sie, dass nicht alle Features von SQL Server für Datenbanken mit einer MEMORY_OPTIMIZED_DATA-Dateigruppe unterstützt werden. Weitere Informationen zu den Einschränkungen finden Sie unter [Nicht unterstützte SQL Server-Funktionen für In-Memory OLTP](unsupported-sql-server-features-for-in-memory-oltp.md).
  
<a name="create-a-memory-optimized-table-26y"></a>  
  
## <a name="4-create-a-memory-optimized-table"></a>4. Erstellen einer speicheroptimierten Tabelle  
  
Das entscheidende Transact-SQL-Schlüsselwort ist das MEMORY_OPTIMIZED-Schlüsselwort.  
  
  
  
  
    CREATE TABLE dbo.SalesOrder  
    (  
        SalesOrderId   integer        not null  IDENTITY  
            PRIMARY KEY NONCLUSTERED,  
        CustomerId     integer        not null,  
        OrderDate      datetime       not null  
    )  
        WITH  
            (MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_AND_DATA);  
  
  
  
  
Die Transact-SQL-INSERT und SELECT-Anweisungen für eine speicheroptimierte Tabelle sind die gleichen wie für eine normale Tabelle.  
  
#### <a name="alter-table-for-memory-optimized-tables"></a>ALTER TABLE für speicheroptimierte Tabellen  
  
ALTER TABLE...ADD/DROP können eine Spalte aus einer speicheroptimierten Tabelle oder einem Index hinzufügen oder entfernen.  
  
- CREATE INDEX und DROP INDEX können nicht für speicheroptimierte Tabellen ausgeführt werden. Verwenden Sie stattdessen ALTER TABLE... ADD/DROP INDEX.  
- Weitere Informationen finden Sie unter [Ändern von speicheroptimierten Tabellen](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md).  
  
  
#### <a name="plan-your-memory-optimized-tables-and-indexes"></a>Planen Sie Ihre speicheroptimierten Tabellen und Indizes.  
  
  
- [Indizes für speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)  
- [Von In-Memory-OLTP nicht unterstützte Transact-SQL-Konstrukte](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
  
<a name="create-a-natively-compiled-stored-procedure-native-proc-29u"></a>  
  
## <a name="5-create-a-natively-compiled-stored-procedure-native-proc"></a>5. Erstellen einer nativ kompilierten, gespeicherten Prozedur (native Prozedur)  
  
  
Das entscheidende Schlüsselwort ist NATIVE_COMPILATION.  
  
  
  
  
    CREATE PROCEDURE ncspRetrieveLatestSalesOrderIdForCustomerId  
        @_CustomerId   INT  
        WITH  
            NATIVE_COMPILATION,  
            SCHEMABINDING  
    AS  
    BEGIN ATOMIC  
        WITH  
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
            LANGUAGE = N'us_english')  
      
        DECLARE @SalesOrderId int, @OrderDate datetime;  
      
        SELECT TOP 1  
                @SalesOrderId = s.SalesOrderId,  
                @OrderDate    = s.OrderDate  
            FROM dbo.SalesOrder AS s  
            WHERE s.CustomerId = @_CustomerId  
            ORDER BY s.OrderDate DESC;  
      
        RETURN @SalesOrderId;  
    END;  
  
  
  
  
Das Schlüsselwort SCHEMABINDING bedeutet, dass die Tabellen in der nativen Prozedur nicht gelöscht werden können, es sei denn, die native Prozedur wird zuvor gelöscht. Weitere Informationen finden Sie unter [Erstellen systemintern kompilierter gespeicherter Prozeduren](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md).  
  
Beachten Sie, dass Sie keine nativ kompilierte gespeicherte Prozedur erstellen müssen, um auf eine speicheroptimierte Tabelle zuzugreifen. Sie können auf speicheroptimierte Tabellen auch von herkömmlich gespeicherten Prozeduren und Ad-hoc-Batches verweisen.
  
<a name="execute-the-native-proc-31e"></a>  
  
## <a name="6-execute-the-native-proc"></a>6. Ausführen der nativen Prozedur  
  
  
Füllen Sie die Tabelle mit zwei Zeilen mit Daten auf.  
  
  
  
  
    INSERT into dbo.SalesOrder  
            ( CustomerId, OrderDate )  
        VALUES  
            ( 42, '2013-01-13 03:35:59' ),  
            ( 42, '2015-01-15 15:35:59' );  
  
  
  
  
Dann folgt ein EXECUTE-Aufruf auf die systemintern kompilierte gespeicherte Prozedur.  
  
  
  
  
    DECLARE @LatestSalesOrderId int, @mesg nvarchar(128);  
      
    EXECUTE @LatestSalesOrderId =  
        ncspRetrieveLatestSalesOrderIdForCustomerId 42;  
      
    SET @mesg = CONCAT(@LatestSalesOrderId,  
        ' = Latest SalesOrderId, for CustomerId = ', 42);  
    PRINT @mesg;  
      
    -- Here is the actual PRINT output:  
    -- 2 = Latest SalesOrderId, for CustomerId = 42  
  
  
  
  
<a name="guide-to-the-documentation-and-next-steps-32w"></a>  
  
### <a name="guide-to-the-documentation-and-next-steps"></a>Anleitung zur Dokumentation und nächste Schritte  
  
  
Die vorhergehenden, einfachen Beispiele bieten Ihnen eine Grundlage zum Erlernen der erweiterten Funktionen von In-Memory-OLTP. Die folgenden Abschnitte sind eine Anleitung für die speziellen Überlegungen, die Sie möglicherweise kennen sollten, und wo Sie die Details von diesen finden können.  
  
  
  
<a name="how-do-in-memory-oltp-features-work-so-much-faster-33v"></a>  
  
## <a name="how-in-memory-oltp-features-work-so-much-faster"></a>So arbeiten In-Memory-OLTP-Funktionen so viel schneller  
  
  
In den folgenden Unterabschnitten wird kurz beschrieben, wie die In-Memory-OLTP-Funktionen intern arbeiten, um verbesserte Leistung zu bieten.  
  
  
<a name="how-do-memory-optimized-tables-perform-faster-34q"></a>  
  
### <a name="how-memory-optimized-tables-perform-faster"></a>So werden speicheroptimierte Tabellen schneller ausgeführt  
  
  
**Dualer Aufbau:** Eine speicheroptimierte Tabelle ist dual aufgebaut; eine Darstellung im aktiven Arbeitsspeicher, und die andere auf der Festplatte. Jede Transaktion wird in beiden Versionen der Tabelle committet. Transaktionen arbeiten gegen die Darstellung des viel schnelleren aktiven Arbeitsspeichers. Speicheroptimierte Tabellen profitieren von der höheren Geschwindigkeit des aktiven Arbeitsspeichers im Vergleich zum Datenträger. Darüber hinaus erlaubt die höhere Agilität des aktiven Speichers die Verwendung einer komplexeren, auf Geschwindigkeit optimierten Tabellenstruktur. Zusätzlich ist die erweiterte Struktur seitenlos, wodurch der Mehraufwand sowie der Konflikt von Latches und Spinlocks vermieden werden.  
  
  
**Keine Sperren:** Die speicheroptimierte Tabelle basiert auf einem *optimistischen* Ansatz für die konkurrierenden Ziele der Datenintegrität gegenüber Parallelität und hohem Durchsatz. Während der Transaktion platziert die Tabelle keine Sperren auf keiner Version der aktualisierten Zeilen von Daten. Diese kann im Konflikte erheblich in einigen Systemen mit hohem Volumen reduzieren.  
  
  
**Zeilenversionen:** Anstelle von Sperren fügt die speicheroptimierte Tabelle eine neue Version einer aktualisierten Zeile in die Tabelle selbst ein, nicht in „tempdb“. Die ursprüngliche Zeile wird beibehalten, nachdem für die Transaktion ein Commit ausgeführt wurde. Während der Transaktion können andere Prozesse die ursprüngliche Version der Zeile lesen.  
  
- Wenn mehrere Versionen einer Zeile für eine datenträgerbasierte Tabelle erstellt werden, werden Zeilenversionen vorübergehend in „tempdb“ gespeichert.  
  
  
**Weniger Protokollierung:** Die Versionen der Zeilen vor und nach der Aktualisierung werden in der speicheroptimierten Tabelle gespeichert. Das Zeilenpaar stellt einen Großteil der Informationen bereit, die normalerweise in die Protokolldatei geschrieben werden. Dadurch kann das System weniger Informationen in das Protokoll schreiben und auch nicht so häufig. Die Transaktionsintegrität wird nichtsdestotrotz sichergestellt.  
  
  
<a name="how-do-native-procs-perform-faster-35x"></a>  
  
### <a name="how-native-procs-perform-faster"></a>So werden native Prozeduren schneller ausgeführt  
  
Konvertieren einer regulär interpretierten, gespeicherten Prozedur in eine nativ kompilierte gespeicherte Prozedur reduziert erheblich die Anzahl der Anweisungen, die während der Laufzeit ausgeführt wird.  
  
  
<a name="trade-offs-of-in-memory-features-36j"></a>  
  
## <a name="trade-offs-of-in-memory-features"></a>Vor- und Nachteile von In-Memory-Funktionen  
  
  
Wie es in der Informatik üblich ist, sind die durch In-Memory-Funktionen bereitgestellte Leistungsgewinne ein Kompromiss. Die bessere Funktionen bringen Vorteile mit sich, die bedeutender als die zusätzlichen Kosten für die Funktion sind. Umfassende Hinweise zu den Vor- und Nachteilen finden Sie unter:

- [Planen der Übernahme von In-Memory-OLTP-Funktionen in SQL Server](../../relational-databases/in-memory-oltp/plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)

Im Rest dieses Abschnitts werden einige der wichtigsten Aspekte hinsichtlich Planung und Vor- und Nachteilen aufgelistet.
  
<a name="trade-offs-of-memory-optimized-tables-37d"></a>  
  
### <a name="trade-offs-of-memory-optimized-tables"></a>Vor- und Nachteile von speicheroptimierten Tabellen  
  
  
**Schätzen Sie den Arbeitsspeicher:** Sie müssen die Menge des aktiven Arbeitsspeichers schätzen, den Ihre speicheroptimierte Tabelle verbrauchen wird. Ihr Computersystem muss über ausreichend Kapazität zum Hosten einer speicheroptimierten Tabelle verfügen. Einzelheiten dazu finden Sie unter:  
  
- [Überwachung und Fehlerbehebung für die Arbeitsspeicherauslastung](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)  
- [Schätzen der Arbeitsspeicheranforderungen speicheroptimierter Tabellen](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)  
- [Tabellen- und Zeilengröße in speicheroptimierten Tabellen](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
  
**Partitionieren Sie Ihre große Tabelle:** Eine Möglichkeit, den Bedarf an großer Menge aktiven Arbeitsspeichers zu decken, ist das Partitionieren Ihrer große Tabelle in Teile im Arbeitsspeicher, *die heiße* Datenzeilen enthalten, verglichen mit *kalte, alte* Datenzeilen, die auf der Festplatte gespeichert werden (z.B. Aufträge, die vollständig ausgeliefert und abgeschlossen wurden). Diese Partitionierung ist ein manueller Prozess von Entwurf und Implementierung. Weitere Informationen:  
  
- [Partitionierung auf Anwendungsebene](../../relational-databases/in-memory-oltp/application-level-partitioning.md)  
- [Anwendungsmuster zur Partitionierung von speicheroptimierten Tabellen](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)  
  
  
<a name="trade-offs-of-native-procs-38p"></a>  
  
### <a name="trade-offs-of-native-procs"></a>Vor-und Nachteile von nativen Prozeduren  
  
  
- Eine nativ kompilierte gespeicherte Prozedur kann nicht auf datenträgerbasierte Tabellen zugreifen. Eine native Prozedur kann nur auf speicheroptimierte Tabellen zugreifen.  
- Wenn eine native Prozedur zum ersten Mal ausgeführt wird, nachdem der Server oder die Datenbank zuletzt wieder online geschaltet wurde, muss die native Prozedur einmalig neu kompiliert werden. Dies führt zu einer Verzögerung, bevor die native Prozedur mit der Ausführung beginnt.  
  
  
<a name="advanced-considerations-for-memory-optimized-tables-39n"></a>  
  
## <a name="advanced-considerations-for-memory-optimized-tables"></a>Zusätzliche Überlegungen zu speicheroptimierten Tabellen  
  
  
[Indizes für speicheroptimierten Tabellen](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md) unterscheiden sich in einigen Punkten von Indizes in Tabellen auf herkömmlichen Datenträgern.  
  
- [Hashindizes](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) sind nur für speicheroptimierte Tabellen verfügbar.  
  
  
Sie müssen planen, um sicherzustellen, dass genügend aktiver Speicher für Ihre geplante speicheroptimierte Tabelle und ihre Indizes vorhanden sein wird. Weitere Informationen:  
  
- [Erstellen und Verwalten von Speicher für speicheroptimierte Objekte](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
Eine speicheroptimierte Tabelle kann mit DURABILITY = SCHEMA_ONLY deklariert werden:  
  
- Diese Syntax weist das System an, alle Daten aus der speicheroptimierten Tabelle zu verwerfen, wenn die Datenbank offline geschaltet wird. Nur die Tabellendefinition wird beibehalten.  
- Wenn die Datenbank wieder online geschaltet wird, wird die speicheroptimierte Tabelle ohne Daten zurück in den aktiven Arbeitsspeicher geladen.  
- SCHEMA_ONLY-Tabellen können eine übergeordnete [Alternative zu #temporären Tabellen](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md) in tempdb darstellen, wenn tausende Zeilen involviert sind.  
  
  
Tabellenvariablen können auch als speicheroptimiert deklariert werden. Weitere Informationen:  
  
- [Schnellere temporäre Tabellen und Tabellenvariablen durch Speicheroptimierung](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)  
  
  
  
<a name="advanced-considerations-for-natively-compiled-modules-40k"></a>  
  
## <a name="advanced-considerations-for-natively-compiled-modules"></a>Zusätzliche Überlegungen zu nativ kompilierten Modulen  
  
  
Die Typen von nativ kompilierten Modulen, die über Transact-SQL verfügbar sind, sind:  
  
- Systemintern kompilierte gespeicherte Prozeduren (native Prozeduren).  
- Nativ kompilierte [benutzerdefinierte Skalarfunktionen](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
- Nativ kompilierte Trigger (native Trigger).  
  - Nur Trigger, die nativ kompiliert werden, sind für speicheroptimierte Tabellen zulässig.  
- Nativ kompilierte [Tabellenwertfunktionen](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md).  
  - [Improving temp table and table variable performance using memory optimization (Verbesserung der temporären Tabelle und Tabellenvariablenleistung mithilfe der Speicheroptimierung)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/21/improving-temp-table-and-table-variable-performance-using-memory-optimization/)  
  
  
Eine nativ kompilierte benutzerdefinierte Funktion (UDF) wird schneller ausgeführt als eine interpretierte UDF. Hier sind einige Punkte, die bei UDFs zu beachten sind:  
  
- Wenn T-SQL-SELECT eine UDF verwendet, wird die UDF immer einmal pro zurückgegebener Zeile aufgerufen.  
  - UDFs werden nie Inline ausgeführt, und stattdessen immer aufgerufen.  
  - Die Ersparnis ist durch das Kompilieren ist weniger ausschlaggebend als der für alle UDFs inhärente Aufwand für wiederholte Aufrufe.  
  - Dennoch ist der Mehraufwand für UDF-Aufrufe im Praktischen oft akzeptabel.  
  
Testdaten und Erläuterung zur Leistung von nativen UDFs finden Sie unter:  
  
  - [Soften the RBAR impact with Native Compiled UDFs in SQL Server 2016 (Weichzeichnen der RBAR Wirkung mit nativ kompilierten UDFs in SQL Server 2016)](https://blogs.msdn.microsoft.com/sqlcat/2016/02/17/soften-the-rbar-impact-with-native-compiled-udfs-in-sql-server-2016/)  
  - Der [tolle Blogbeitrag von Gail Shaw](http://sqlinthewild.co.za/index.php/2016/01/12/natively-compiled-user-defined-functions/)von Januar 2016.  
  
  
<a name="documentation-guide-for-memory-optimized-tables-41z"></a>  
  
## <a name="documentation-guide-for-memory-optimized-tables"></a>Dokumentationshandbuch für speicheroptimierte Tabellen  
  
  
Hier sind Links zu anderen Artikeln über spezielle Überlegungen zu speicheroptimierten Tabellen:  
  
- [Migrieren zu In-Memory-OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  - [Bestimmen, ob eine Tabelle oder eine gespeicherte Prozedur zu In-Memory-OLTP portiert werden soll](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)  
  - Der Transaktionsleistungs-Analysebericht in SQL Server Management Studio hilft Ihnen zu bewerten, ob In-Memory-OLTP die Leistung Ihrer Datenbankanwendungen verbessern wird.  
  - Verwenden Sie den [Ratgeber für die Speicheroptimierung](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md) , um die datenträgerbasierte Datenbanktabelle zu In-Memory-OLTP zu migrieren.   
- [Sichern und Wiederherstellen speicheroptimierter Tabellen](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  - Der von speicheroptimierten Tabellen genutzte Speicher kann wesentlich größer als die belegte Arbeitsspeicherkapazität sein, was sich auf die Größe der Datenbanksicherung auswirkt.  
- [Transaktionen mit speicheroptimierten Tabellen](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)  
  - Enthält Informationen zur Wiederholungslogik in T-SQL für Transaktionen in speicheroptimierten Tabellen.  
- [Transact-SQL-Unterstützung für In-Memory-OLTP](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  - Unterstützte und nicht unterstützte T-SQL-Funktionen und Datentypen für speicheroptimierte Tabellen und native Prozeduren.  
- Der Artikel[Bind a Database with Memory-Optimized Tables to a Resource Pool](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)(eine Datenbank mithilfe speicheroptimierter Tabellen an einen Ressourcenpool binden) erläutert einen optionalen erweiterten Aspekt.  
  
  
  
<a name="documentation-guide-for-native-procs-42b"></a>  
  
## <a name="documentation-guide-for-native-procs"></a>Dokumentationshandbuch für native Prozeduren  

Im folgenden Artikel und dessen untergeordneten Artikel im Inhaltsverzeichnis sind die Details zu nativ kompilierten gespeicherten Prozeduren aufgeführt.

- [Nativ kompilierte gespeicherte Prozeduren](natively-compiled-stored-procedures.md)
  
<a name="related-links-43f"></a>  
  
## <a name="related-links"></a>Verwandte Links  
  
- Ursprünglicher Artikel: [In-Memory-OLTP (Arbeitsspeicheroptimierung)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
Hier finden Sie Artikel, die Code zum Veranschaulichen der Leistungsverbesserungen bieten, die Sie mit In-Memory-OLTP erreichen können.  
  
- [Demo: Leistungsverbesserungen von In-Memory-OLTP](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md) bietet eine kleine Demonstration der größeren potenziellen Leistungsgewinne.  
- [Sample Database for In-Memory-OLTP](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md) (Beispieldatenbank für In-Memory-OLTP) bietet eine genauere Erläuterung.  
