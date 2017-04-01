---
title: "Schnellere tempor&#228;re Tabellen und Tabellenvariablen durch Speicheroptimierung | Microsoft Docs"
ms.custom: ""
ms.date: "01/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 38512a22-7e63-436f-9c13-dde7cf5c2202
caps.latest.revision: 20
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 19
---
# Schnellere tempor&#228;re Tabellen und Tabellenvariablen durch Speicheroptimierung
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  
Wenn Sie temporäre Tabellen, Tabellenvariablen oder Tabellenwertparameter verwenden, sollten Sie die Konvertierungen auf Speicheroptimierte Tabellen und Tabellenvariablen zur Verbesserung der Leistung nutzen. Die Codeänderungen sind normalerweise minimal.  
  
Dieser Artikel beschreibt:  
  
- Szenarios, die für die Konvertierung zu In-Memory sprechen.  
- Technische Schritte für die Implementierung der Konvertierungen zu In-Memory.  
- Erforderliche Komponenten vor der Konvertierung zu In-Memory.  
- Ein Codebeispiel, das die Leistungsvorteile der Speicheroptimierung hervorhebt.
  
  
## A. Grundlagen von speicheroptimierten Tabellenvariablen  
  
Eine speicheroptimierte Tabellenvariable ist höchst effizient bei der Verwendung des gleichen speicheroptimierten Algorithmus und der gleichen Datenstrukturen, die von speicheroptimierten Tabellen verwendet werden. Die Effizienz wird maximiert, wenn innerhalb eines nativ kompilierten Moduls auf die Tabellenvariable zugegriffen werden kann.  
  
  
Eine speicheroptimierte Tabellenvariable:  
  
- Wird nur im Arbeitsspeicher gespeichert und verfügt über keine Komponente auf dem Datenträger.  
- Umfasst keine E/A-Aktivität.  
- Umfasst keine tempdb-Nutzung oder -Konflikte.  
- Kann an eine gespeicherte Prozedur als ein Tabellenwertparameter (TVP) übergeben werden.  
- Benötigt mindestens einen Index, entweder einen Hashindex oder einen nicht gruppierten Index.  
  - Für einen Hash-Index sollte die Bucketanzahl idealerweise auf einen Wert zwischen der einfachen und doppelten Anzahl von Indexschlüsselwerten festgelegt werden. Ein zu hoher Wert (ein bis zu zehnfacher Wert) stellt in der Regel aber auch kein Problem dar. Weitere Informationen finden Sie unter [Indexes for Memory-Optimized Tables](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md) (Indizes für speicheroptimierte Tabellen).  

  
  
#### Objekttypen  
  
In-Memory-OLTP stellt die folgenden Objekte bereit, die für speicheroptimierte temporäre Tabellen und Tabellenvariablen verwendet werden können.  
  
- Speicheroptimierte Tabellen  
  - Durability = SCHEMA_ONLY  
- Speicheroptimierte Tabellenvariablen  
  - Muss in zwei Schritten (statt inline) deklariert werden:  
    - `CREATE TYPE my_type AS TABLE ...;` , dann  
    - `DECLARE @mytablevariable my_type;`.  
  
  
## B. Szenario: Ersetzen von globaler tempd &#x23;&#x23;table  
  
Angenommen, Sie verfügen über die folgende globale temporäre Tabelle.  
  
  
  
  
    CREATE TABLE ##tempGlobalB  
    (  
        Column1   INT   NOT NULL ,  
        Column2   NVARCHAR(4000)  
    );  
  
  
  
  
Ersetzen Sie die globale temporäre Tabelle mit der folgenden speicheroptimierten Tabelle, für die DURABILITY = SCHEMA_ONLY festgelegt wurde.  
  
  
  
  
    CREATE TABLE dbo.soGlobalB  
    (  
        Column1   INT   NOT NULL   INDEX ix1 NONCLUSTERED,  
        Column2   NVARCHAR(4000)  
    )  
        WITH  
            (MEMORY_OPTIMIZED = ON,  
            DURABILITY        = SCHEMA_ONLY);  
  
  
  
  
#### B.1 Schritte  
  
Die folgenden Schritte beschreiben die Konvertierung von globalen temporären Tabellen zu SCHEMA_ONLY.  
  
  
1. Erstellen Sie einmalig die **dbo.soGlobalB**-Tabelle, so wie Sie es auch auf einer herkömmlichen Tabelle auf einem Datenträger machen würden.  
2. Entfernen Sie aus Transact-SQL den Block zum Erstellen der Tabelle **&#x23;&#x23;tempGlobalB**.  
3. Ersetzen Sie in T-SQL alle Erwähnungen von **&#x23;&#x23;tempGlobalB** mit **dbo.soGlobalB**.  
  
  
## C. Szenario: Ersetzen der tempd &#x23;Sitzungstabelle  
  
Die erforderlichen Schritte zum Ersetzen einer Sitzung temporäre Tabelle umfassen zusätzliches T-SQL als für die globale temporäre Tabelle Szenario. Zusätzliches T-SQL bedeutet glücklicherweise nicht, dass mehr Arbeit für die Ausführung der Konvertierung nötig ist.  
  
Angenommen, Sie verfügen über die folgende temporäre Sitzungstabelle.  
  
  
  
  
    CREATE TABLE #tempSessionC  
    (  
        Column1   INT   NOT NULL ,  
        Column2   NVARCHAR(4000)  
    );  
  
  
  
  
Erstellen Sie zunächst die folgende Tabellenwertfunktion zum Filtern nach **@@spid**. Die Funktion kann von allen SCHEMA_ONLY-Tabellen verwendet werden, die Sie aus temporären Sitzungstabellen konvertieren.  
  
  
  
  
    CREATE FUNCTION dbo.fn_SpidFilter(@SpidFilter smallint)  
        RETURNS TABLE  
        WITH SCHEMABINDING , NATIVE_COMPILATION  
    AS  
        RETURN  
            SELECT 1 AS fn_SpidFilter  
                WHERE @SpidFilter = @@spid;  
  
  
  
  
Zweitens: Erstellen der SCHEMA_ONLY-Tabelle sowie eine Sicherheitsrichtlinie für die Tabelle ein.  
  
  
Beachten Sie, dass jede speicheroptimierte Tabelle mindestens einen Index besitzen muss.  
  
- Für die Tabelle dbo.soSessionC ist ein HASH-Index möglicherweise die bessere Wahl, wenn wir den geeigneten BUCKET_COUNT-Wert berechnen. Verwenden wir der Einfachheit halber einen NONCLUSTERED-Index.  
  
  
  
  
    CREATE TABLE dbo.soSessionC  
    (  
        Column1     INT         NOT NULL,  
        Column2     NVARCHAR(4000)  NULL,  
  
        SpidFilter  SMALLINT    NOT NULL   DEFAULT (@@spid),  
  
        INDEX ix_SpidFiler NONCLUSTERED (SpidFilter),  
        --INDEX ix_SpidFilter HASH  
        --    (SpidFilter) WITH (BUCKET_COUNT = 64),  
          
        CONSTRAINT CHK_soSessionC_SpidFilter  
            CHECK ( SpidFilter = @@spid ),  
    )  
        WITH  
            (MEMORY_OPTIMIZED = ON,  
             DURABILITY = SCHEMA_ONLY);  
    go  
  
  
    CREATE SECURITY POLICY dbo.soSessionC_SpidFilter_Policy  
        ADD FILTER PREDICATE dbo.fn_SpidFilter(SpidFilter)  
        ON dbo.soSessionC  
        WITH (STATE = ON);  
    go  
  
  
  
  
Drittens: Im allgemeinen T-SQL-Code:  
  
1. Löschen Sie alle CREATE TABLE-Anweisungen für die alte temporäre Sitzungstabelle.  
2. Ersetzen Sie den alten Tabellennamen mit dem neuen Namen:  
  - _Alt:_ &#x23;tempSessionC  
  - _Neu:_ dbo.soSessionC  
  
  
  
## D. Szenario: Eine Tabellenvariable kann die WITH-Klausel MEMORY_OPTIMIZED=ON enthalten.  
  
  
Eine herkömmliche Tabellenvariable stellt eine Tabelle in der tempdb-Datenbank dar. Für eine schnellere Leistung können Sie den Speicher Ihrer Tabellenvariable optimieren.  
  
Hier ist das T-SQL für eine herkömmliche Tabellenvariablen. Der Bereich endet, wenn der Batch oder die Sitzung beendet wird.  
  
  
  
  
    DECLARE @tvTableD TABLE  
        ( Column1   INT   NOT NULL ,  
          Column2   CHAR(10) );  
  
  
  
  
#### D.1 Konvertieren von Inline zu Explicit  
  
Die vorherigen Syntax soll die Tabellenvariable *inline* erstellen. Die Inline-Syntax unterstützt keine Speicheroptimierung. Lassen Sie uns also die Inline-Syntax zur Explicit-Syntax für TYPE konvertieren.  
  
*Bereich:* Die TYPE-Definition, die vom ersten „go“-unterteilten Batch erstellt wurde, bleibt auch nach dem Herunterfahren und Neustart des Servers bestehen. Nach dem ersten „go“-unterteilten Batch, bleibt die deklarierte Tabelle „@tvTableC“ nur bis zum nächsten „go“-unterteilten Batch bestehen und bis der Batch endet.  
  
  
  
  
    CREATE TYPE dbo.typeTableD  
        AS TABLE  
        (  
            Column1  INT   NOT NULL ,  
            Column2  CHAR(10)  
        );  
    go  
          
    SET NoCount ON;  
    DECLARE @tvTableD dbo.typeTableD  
    ;  
    INSERT INTO @tvTableD (Column1) values (1), (2)  
    ;  
    SELECT * from @tvTableD;  
    go  
  
  
  
  
#### D.2 Konvertieren einer explizit auf dem Datenträger gespeicherten Tabellenvariable in eine speicheroptimierte Tabellenvariable  
  
Es befindet sich keine speicheroptimierte Tabellenvariable in tempdb. Die Speicheroptimierung führt zu einer Zunahme der Geschwindigkeit, die zehnmal schneller ist oder sogar noch schneller.  
  
Die Konvertierung in eine speicheroptimierte Tabelle erfolgt in nur einem Schritt. Erweitern Sie die explizite Erstellung von TYPE, sodass Sie folgendermaßen aussieht, was hinzufügt:  
  
- Ein Index. Jede speicheroptimierte Tabelle muss mindestens einen Index haben.  
- MEMORY_OPTIMIZED = ON.  
  
  
  
  
    CREATE TYPE dbo.typeTableD  
        AS TABLE  
        (  
            Column1  INT   NOT NULL   INDEX ix1,  
            Column2  CHAR(10)  
        )  
        WITH  
            (MEMORY_OPTIMIZED = ON);  
  
  
  
  
Fertig.  
  
  
## E. FILEGROUP als Voraussetzung für SQL Server  
  
Wenn Sie speicheroptimierte Funktionen auf Microsoft SQL Server verwenden möchten, muss Ihre Datenbank über FILEGROUP verfügen, die mit **MEMORY_OPTIMIZED_DATA** deklariert ist.  
  
- In der Azure SQL-Datenbank ist die Erstellung von FILEGROUP nicht nötig.  
  
  
*Voraussetzung:* Der folgende Transact-SQL-Code für FILEGROUP ist eine Voraussetzung für die langen T-SQL-Codebeispiele in späteren Abschnitten dieses Artikels.  
  
1. Verwenden Sie SSMS.exe oder ein anderes Tool, das T-SQL übermitteln kann.  
2. Fügen Sie den T-SQL-Beispielcode FILEGROUP in SSMS ein.  
3. Bearbeiten Sie das T-SQL, um die bestimmten Namen und Verzeichnispfade wie gewünscht zu ändern.  
  - Alle Verzeichnisse im Wert FILENAME müssen bereits vorhanden sein, außer die unterste Ebene im Verzeichnis.  
4. Führen Sie das bearbeitete T-SQL aus.  
  - Es ist nicht nötig, die FILEGROUP von T-SQL mehrmals auszuführen, auch wenn Sie wiederholt den T-SQL-Geschwindigkeitsvergleich des nächsten Unterbereichs anpassen und erneut ausführen.  
  
  
  
 
  
    ALTER DATABASE InMemTest2  
        ADD FILEGROUP FgMemOptim3  
            CONTAINS MEMORY_OPTIMIZED_DATA;  
    go  
    ALTER DATABASE InMemTest2  
        ADD FILE  
        (  
            NAME = N'FileMemOptim3a',  
            FILENAME = N'C:\DATA\FileMemOptim3a'  
                     --  C:\DATA\    preexisted.  
        )  
        TO FILEGROUP FgMemOptim3;  
    go  
  
  
Das folgende Skript erstellt eine Dateigruppe für Sie und konfiguriert empfohlene Datenbankeinstellungen: [enable-in-memory-oltp.sql](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql)
  
Weitere Informationen zu `ALTER DATABASE ... ADD` FILE und FILEGROUP finden Sie unter:  
  
- [ALTER DATABASE-Optionen Datei und Dateigruppe (Transact-SQL)](ALTER%20DATABASE%20File%20and%20Filegroup%20Options%20(Transact-SQL).xml)  
- [Die speicheroptimierte Dateigruppe](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)    
  
  
## F. Schnelltest zum Beweisen der Verbesserung der Geschwindigkeit  
  
  
Dieser Abschnitt enthält Transact-SQL-Code, der ausgeführt werden kann, um zu vergleichen, welcher Geschwindigkeitszuwachs bei INSERT-DELETE durch die Verwendung speicheroptimierter Tabellen erreicht werden kann. Der Code besteht aus zwei Hälften, die nahezu identisch sind. In der ersten Hälfte ist der Tabellentyp jedoch speicheroptimiert.  
  
Der Vergleichstest dauert ca. 7 Sekunden. So führen Sie das Beispiel aus:  
  
1. *Voraussetzung:* Sie müssen bereits FILEGROUP T-SQL aus dem vorherigen Abschnitt ausgeführt haben.  
2. Führen Sie das folgende T-SQL-INSERT-DELETE-Skript aus.  
  - Beachten Sie die 'GO 5001'-Anweisung, die T-SQL 5001-mal übermittelt. Sie können die Anzahl anpassen und den Vorgang erneut ausführen.  
  
Wenn Sie das Skript in einer Azure SQL-Datenbank ausführen, stellen Sie sicher, dass Sie es auf einem virtuellen Computer in der gleichen Region ausführen.
  
  
    PRINT ' ';  
    PRINT '---- Next, memory-optimized, faster. ----';  
  
    DROP TYPE IF EXISTS dbo.typeTableC_mem;  
    go  
    CREATE TYPE dbo.typeTableC_mem  -- !!  Memory-optimized.  
         AS TABLE  
         (  
              Column1  INT NOT NULL INDEX ix1,  
              Column2  CHAR(10)  
         )  
         WITH  
              (MEMORY_OPTIMIZED = ON);  
    go  
    DECLARE @dateString_Begin nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_Begin, '  = Begin time, _mem.');  
    go  
    SET NoCount ON;  
    DECLARE @tvTableC dbo.typeTableC_mem;  -- !!  
  
    INSERT INTO @tvTableC (Column1) values (1), (2);  
    INSERT INTO @tvTableC (Column1) values (3), (4);  
    DELETE @tvTableC;  
  
    GO 5001  
  
    DECLARE @dateString_End nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_End, '  = End time, _mem.');  
    go  
    DROP TYPE IF EXISTS dbo.typeTableC_mem;  
    go  
  
    ---- End memory-optimized.  
    -------------------------------------------------  
    ---- Start traditional on-disk.  
  
    PRINT ' ';  
    PRINT '---- Next, tempdb based, slower. ----';  
  
    DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
    go  
    CREATE TYPE dbo.typeTableC_tempdb  -- !!  Traditional tempdb.  
        AS TABLE  
        (  
            Column1  INT NOT NULL ,  
            Column2  CHAR(10)  
        );  
    go  
    DECLARE @dateString_Begin nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_Begin, '  = Begin time, _tempdb.');  
    go  
    SET NoCount ON;  
    DECLARE @tvTableC dbo.typeTableC_tempdb;  -- !!  
  
    INSERT INTO @tvTableC (Column1) values (1), (2);  
    INSERT INTO @tvTableC (Column1) values (3), (4);  
    DELETE @tvTableC;  
  
    GO 5001  
  
    DECLARE @dateString_End nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_End, '  = End time, _tempdb.');  
    go  
    DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
    go  
    ----  
  
    PRINT '---- Tests done. ----';  
  
    go  
  
    /*** Actual output, SQL Server 2016:  
  
    ---- Next, memory-optimized, faster. ----  
    2016-04-20 00:26:58.033  = Begin time, _mem.  
    Beginning execution loop  
    Batch execution completed 5001 times.  
    2016-04-20 00:26:58.733  = End time, _mem.  
  
    ---- Next, tempdb based, slower. ----  
    2016-04-20 00:26:58.750  = Begin time, _tempdb.  
    Beginning execution loop  
    Batch execution completed 5001 times.  
    2016-04-20 00:27:05.440  = End time, _tempdb.  
    ---- Tests done. ----  
    ***/  
  

  
  
  
## G. Vorhersagen von aktiver Arbeitsspeichernutzung  
  
Sie können lernen, wie sie die Bedürfnisse des aktiven Arbeitsspeichers für Ihre speicheroptimierten Tabellen mit den folgenden Ressourcen vorhersagen können:  
  
- [Schätzen der Arbeitsspeicheranforderungen speicheroptimierter Tabellen](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)  
- [Tabellen- und Zeilengröße in speicheroptimierten Tabellen: Beispielrechnung](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
Nicht gruppierte Indizes nutzen für größere Tabellenvariablen mehr Arbeitsspeicher als für speicheroptimierte *Tabellen*. Je größer die Anzahl der Zeilen und der Indexschlüssel, desto größer wird der Unterschied.  
  
Wenn auf die speicheroptimierten Tabellenvariablen nur mit einem exakten Schlüsselwert pro Zugriff zugegriffen wird, sollten Sie eher ein Hashindex als einen nicht gruppierten Index verwenden. Wenn Sie den erforderlichen BUCKET_COUNT-Wert nicht abschätzen können, wäre ein NONCLUSTERED-Index eine gute zweite Wahl.  
  
## H. Siehe auch  
  
- [Speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)
- [Definieren von Dauerhaftigkeit für speicheroptimierte Objekte](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md)  
  
  
  
  
\<!--  
CAPS Title: "Faster temp table and table variable by using memory optimization"  
  
https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/21/improving-temp-table-and-table-variable-performance-using-memory-optimization/  
  
  
[ALTER DATABASE File and Filegroup Options (Transact-SQL)](http://msdn.microsoft.com/library/bb522469.aspx)  
  
[The Memory Optimized Filegroup](http://msdn.microsoft.com/library/dn639109.aspx)  
  
[Resource Governor Resource Pool](http://msdn.microsoft.com/library/hh510189.aspx)  
  
  
[Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx)  
  
[Estimate Memory Requirements for Memory-Optimized Tables](http://msdn.microsoft.com/library/dn282389.aspx)  
  
[Table and Row Size in Memory-Optimized Tables: Example Calculation](http://msdn.microsoft.com/library/dn205318.aspx)  
  
  
[Durability for Memory-Optimized Tables](http://msdn.microsoft.com/library/dn553125.aspx)  
  
[Defining Durability for Memory-Optimized Objects](http://msdn.microsoft.com/library/dn553122.aspx)  
  
[Memory-Optimized Table Variables](http://msdn.microsoft.com/library/dn535766.aspx)  
  
  
GeneMi , 2016-05-02  Monday  18:40pm  
-->  
  
  
  
