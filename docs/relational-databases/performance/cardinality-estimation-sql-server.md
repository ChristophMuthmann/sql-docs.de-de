---
title: "Kardinalit&#228;tssch&#228;tzung (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "10/04/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Kardinalitätsschätzung"
  - "CE (Cardinality Estimator, Kardinalitätsschätzung)"
  - "estimating cardinality"
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
caps.latest.revision: 11
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 11
---
# Kardinalit&#228;tssch&#228;tzung (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  
Dieser Artikel veranschaulicht, wie Sie die beste Konfiguration für die Kardinalitätsschätzung (Cardinality Estimation, CE) für Ihr SQL-System bewerten und auswählen. Die meisten Systeme profitieren von der neuesten Kardinalitätsschätzung, da sie die genaueste ist. Die Kardinalitätsschätzung sagt vorher, wie viele Zeilen eine Abfrage wahrscheinlich zurückgibt. Die Vorhersage der Kardinalität wird vom Abfrageoptimierer verwendet, um einen optimalen Abfrageplan zu generieren. In der Regel gilt: Je genauer die Kardinalitätsschätzung ist, desto besser ist der Abfrageplan.  
  
Möglicherweise existiert in Ihrem Anwendungssystem eine wichtige Abfrage, deren Plan während einer neuen Kardinalitätsschätzung in einen langsameren Plan geändert wird. Hier einige Beispiele für eine solche Abfrage:  
  
- Eine OLTP-Abfrage, die so häufig ausgeführt wird, dass oft mehrere Instanzen der Abfrage gleichzeitig ausgeführt werden.  
- Eine SELECT-Anweisung mit erheblicher Aggregation, die während der OLTP-Betriebszeiten ausgeführt wird.  
  
Sie verfügen über Techniken, um eine Abfrage zu identifizieren, die mit der neuen Kardinalitätsschätzung langsamer ausgeführt wird. Und Sie verfügen über Optionen, wie Sie das Leistungsproblem beheben.  
  
  
## Versionen der Kardinalitätsschätzung  
  
 Im Jahr 1998 wurde in Microsoft SQL Server 7.0 ein wichtiges Update der Kardinalitätsschätzung eingeführt, mit dem Kompatibilitätsgrad 70. Spätere Updates mit einem Kompatibilitätsgrad von 120 bzw. 130 erfolgten in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016. Die Updates der Kardinalitätsschätzung für die Kompatibilitätsgrade 120 und 130 umfassen Annahmen und Algorithmen, die für moderne Data Warehousing-Arbeitslasten und OLTP-Prozesse (Online Transaction Processing, Onlinetransaktionsverarbeitung) gut funktionieren.  
  
 **Kompatibilitätsgrad:** Sie können sicherstellen, dass ein bestimmter Grad für Ihre Datenbank gilt, indem Sie den folgenden Transact-SQL-Code für [COMPATIBILITY_LEVEL](ALTER%20DATABASE%20Compatibility%20Level%20\(Transact-SQL\).md) ausführen.  

```tsql  
SELECT ServerProperty('ProductVersion');  
go  
  
ALTER DATABASE <yourDatabase>  
    SET COMPATIBILITY_LEVEL = 130;  
go  
  
SELECT    d.name, d.compatibility_level  
    FROM  sys.databases AS d  
    WHERE d.name = 'yourDatabase';  
go  
```  
  
 In einer SQL Server-Datenbank, die mit Kompatibilitätsgrad 120 eingerichtet wurde, zwingt die Aktivierung des Ablaufverfolgungsflags 9481 das System dazu, die Kardinalitätsschätzung für Kompatibilitätsgrad 70 zu verwenden.  
  
 **Ältere Kardinalitätsschätzung:** In einer SQL Server-Datenbank, die mit Kompatibilitätsgrad 130 eingerichtet wurde, kann eine Kardinalitätsschätzung mit Kompatibilitätsgrad 70 aktiviert werden. Verwenden Sie dazu folgende Transact-SQL-Anweisung für [SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).
  
```tsql  
ALTER DATABASE
    SCOPED CONFIGURATION  
        SET LEGACY_CARDINALITY_ESTIMATION = ON;  
go  
  
SELECT  name, value  
    FROM  sys.database_scoped_configurations  
    WHERE name = 'LEGACY_CARDINALITY_ESTIMATION';  
```  
  
 **Abfragespeicher:** Ab [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 ist der Abfragespeicher ein praktisches Tool zum Untersuchen der Leistung Ihrer Abfragen.  In SQL Server Management Studio (SSMS.exe) wird im **Objekt-Explorer** unterhalb des Knotens Ihrer Datenbank ein Knoten **Abfragespeicher** angezeigt, wenn der Abfragespeicher aktiviert ist.  
  
```tsql  
ALTER DATABASE <yourDatabase>  
    SET QUERY_STORE = ON;  
go  
  
SELECT  
        q.actual_state_desc    AS [actual_state_desc-ofQueryStore],  
        q.desired_state_desc,  
        q.query_capture_mode_desc  
    FROM  
        sys.database_query_store_options  AS q;  
go  
  
ALTER DATABASE <yourDatabase>  
    SET QUERY_STORE CLEAR;  
```  
  
 *Tipp:* Wir empfehlen, jeden Monat die neueste Version von [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx) zu installieren.  
  
 Eine andere Option zum Nachverfolgen der Vorhersagen der Kardinalitätsschätzung ist die Verwendung des erweiterten Ereignisses **query_optimizer_estimate_cardinality**.  Das folgende T-SQL-Codebeispiel wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt. Es schreibt eine XEL-Datei in C:\Temp\ (Sie können den Pfad ändern). Wenn Sie die XEL-Datei in SSMS öffnen, werden die detaillierten Daten in einer von Benutzern gut lesbaren Weise angezeigt.  
  
```tsql  
DROP EVENT SESSION Test_the_CE_qoec_1 ON SERVER;  
go  
  
CREATE EVENT SESSION Test_the_CE_qoec_1  
    ON SERVER  
    ADD EVENT sqlserver.query_optimizer_estimate_cardinality  
    (  
        ACTION (sqlserver.sql_text)  
            WHERE (  
                sql_text LIKE '%yourTable%'  
                and sql_text LIKE '%SUM(%'  
            )  
    )  
    ADD TARGET package0.asynchronous_file_target   
        (SET  
            filename = 'c:\temp\xe_qoec_1.xel',  
            metadatafile = 'c:\temp\xe_qoec_1.xem'  
        );  
go  
  
ALTER EVENT SESSION Test_the_CE_qoec_1  
    ON SERVER  
    STATE = START;  --STOP;  
go  
```  
  
 Informationen zu erweiterten Ereignissen, die speziell auf Azure SQL-Datenbank zugeschnitten sind, finden Sie unter [Erweiterte Ereignisse in SQL-Datenbank](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/).  
  
  
## Schritte für die Bewertung der Version der Kardinalitätsschätzung  
  
 Mit den folgenden Schritten können Sie ermitteln, ob Ihre wichtigsten Abfragen mit der neuesten Kardinalitätsschätzung mit geringerer Leistung ausgeführt werden. In einigen der Schritte wird ein Codebeispiel ausgeführt, das im vorherigen Abschnitt vorgestellt wurde.  
  
1.  Öffnen Sie SSMS. Stellen Sie sicher, dass für Ihre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank der höchste verfügbare Kompatibilitätsgrad festgelegt wurde.  
  
2.  Führen Sie die folgenden vorbereitenden Schritte aus:  
  
    1.  Öffnen Sie SSMS.  
  
    2.  Führen Sie den T-SQL-Code aus, um sicherzustellen, dass für Ihre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank der höchste verfügbare Kompatibilitätsgrad festgelegt wurde.  
  
    3.  Stellen Sie sicher, dass die LEGACY_CARDINALITY_ESTIMATION-Konfiguration Ihrer Datenbank deaktiviert ist.  
  
    4.  Bereinigen Sie Ihren Abfragespeicher (CLEAR). Natürlich müssen Sie auch sicherstellen, dass Ihr Abfragespeicher aktiviert ist.  
  
    5.  Führen Sie diese Anweisung aus: \`SET NoCount OFF;`  
  
3.  Führen Sie diese Anweisung aus: \`SET STATISTICS XML ON;`  
  
4.  Führen Sie Ihre wichtige Abfrage aus.  
  
5.  Beachten Sie im Ergebnisbereich auf der Registerkarte **Meldungen** die tatsächliche Anzahl von betroffenen Zeilen.  
  
6.  Doppelklicken Sie im Ergebnisbereich auf der Registerkarte **Ergebnisse** auf die Zelle, die die Statistik im XML-Format enthält. Es wird ein grafischer Abfrageplan angezeigt.  
  
7.  Klicken Sie mit der rechten Maustaste auf das erste Feld im grafischen Abfrageplan, und klicken Sie dann auf **Eigenschaften**.  
  
8.  Notieren Sie die Werte für die folgenden Eigenschaften, um diese später mit einer anderen Konfiguration vergleichen zu können:  
  
    -   **CardinalityEstimationModelVersion**.  
  
    -   **Geschätzte Anzahl von Zeilen.**.  
  
    -   **Geschätzte E/A-Kosten** sowie einige weitere ähnliche *geschätzte* Eigenschaften, die sich eher auf die tatsächliche Leistung als auf Vorhersagen zur Zeilenanzahl beziehen.  
  
    -   **Logische Operation** und **Physische Operation**. *Parallelität* ist ein guter Wert.  
  
    -   **Tatsächlicher Ausführungsmodus**. *Batch* ist ein guter Wert und besser als *Zeile*.  
  
9. Vergleichen Sie die geschätzte Anzahl von Zeilen mit der tatsächliche Zeilenanzahl. Ist die Kardinalitätsschätzung um 1% oder um 10% ungenau (höher oder niedriger)?  
  
10. Führen Sie diese Anweisung aus: \`SET STATISTICS XML OFF;`  
  
11. Führen Sie den T-SQL-Code aus, um den Kompatibilitätsgrad Ihrer Datenbank um eine Stufe zu senken (z.B. von 130 auf 120).  
  
12. Führen Sie alle Schritte erneut aus, die keine Vorbereitungsschritte sind.  
  
13. Vergleichen Sie die Eigenschaftswerte der Kardinalitätsschätzung der beiden Ausführungen.  
  
    - Ist der Prozentsatz der Ungenauigkeit mit der neuesten Kardinalitätsschätzung geringer als mit der älteren?  
  
14. Vergleichen Sie zum Schluss die verschiedenen Leistungswerte der beiden Ausführungen.  
  
    -   Hat Ihre Abfrage bei den beiden verschiedenen Kardinalitätsschätzungen unterschiedliche Abfragepläne verwendet?  
  
    -   Wurde Ihre Abfrage mit der neuesten Kardinalitätsschätzung langsamer ausgeführt?  
  
    -   Wenn Ihre Abfrage nicht mit der älteren Kardinalitätsschätzung besser und unter einem anderen Plan ausgeführt wird als mit der neuen Schätzung, sollten Sie mit größter Wahrscheinlichkeit die neueste Kardinalitätsschätzung verwenden.  
  
    -   Wenn Ihre Abfrage allerdings mit der älteren Kardinalitätsschätzung unter einem schnelleren Plan ausgeführt wird, sollten Sie erwägen, Ihr System zu zwingen, den schnelleren Plan zu verwenden und die Kardinalitätsschätzung zu ignorieren. Auf diese Weise können Sie die neueste Kardinalitätsschätzung allgemein im System verwenden, für Sonderfälle aber den schnelleren Plan beibehalten.  
  
## Aktivieren des besten Abfrageplans  
  
Nehmen Sie an, dass mit der neuen Kardinalitätsschätzung ein langsamerer Abfrageplan für Ihre Abfrage generiert wird. Für diesen Fall finden Sie hier einige Optionen, mit denen Sie den schnelleren Plan aktivieren können.  
  
Sie können den Kompatibilitätsgrad für Ihre gesamte Datenbank auf einen niedrigeren Wert als den neuesten verfügbaren Grad festlegen.  
  
- Dies aktiviert die ältere Kardinalitätsschätzung, aber damit unterliegen alle Abfragen der älteren und weniger genauen Kardinalitätsschätzung.  
  
- Außerdem können mit einem älteren Kompatibilitätsgrad die hervorragenden Verbesserungen des Abfrageoptimierers nicht genutzt werden.  
  
Sie können LEGACY_CARDINALITY_ESTIMATION verwenden, sodass die gesamte Datenbank die ältere Kardinalitätsschätzung verwendet, die Verbesserungen des Abfrageoptimierers jedoch beibehalten werden.  
  
Die genaueste Steuerung erzielen Sie, indem Sie *erzwingen*, dass das SQL-System den Plan verwendet, der während der Testphase mit der älteren Kardinalitätsschätzung generiert wurde. Nachdem Sie den bevorzugten Plan *angeheftet* haben, können Sie die gesamte Datenbank für die Verwendung des neuesten Kompatibilitätsgrad und der neuesten Kardinalitätsschätzung einrichten. Diese Option wird im nächsten Abschnitt erläutert.  
  
### Erzwingen eines bestimmten Abfrageplans  
  
Der Abfragespeicher bietet verschiedene Möglichkeiten, das System zur Verwendung eines bestimmten Abfrageplans zu zwingen:  
  
- Führen Sie **sp_query_store_force_plan** aus.  
  
- Erweitern Sie in SSMS den Knoten für Ihren **Abfragespeicher**, klicken Sie mit der rechten Maustaste auf **Knoten mit dem höchsten Ressourcenverbrauch**, und klicken Sie dann auf **Knoten mit dem höchsten Ressourcenverbrauch anzeigen**. Es werden die Schaltflächen **Plan erzwingen** und **Erzwingung des Plans aufheben** angezeigt.  
  
 Weitere Informationen zum Abfragespeicher finden Sie unter [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
  
## Beschreibungen der erweiterten Kardinalitätsschätzung  
  
Dieser Abschnitt enthält Beispielabfragen, die von den Erweiterungen der Kardinalitätsschätzung in neueren Versionen profitieren. Hierbei handelt es sich um Hintergrundinformationen, die keine bestimmte Aktion Ihrerseits erfordern.  
  
### Beispiel A. Die Kardinalitätsschätzung berücksichtigt, dass Maximalwerte höher sein können als bei der letzten Erfassung der Statistiken  
  
Angenommen, die Statistiken für OrderTable wurden zuletzt am 30.4.2016 erfasst – der Maximalwert für OrderAddedDate war „2016-04-30“. Bei der Kardinalitätsschätzung für Kompatibilitätsgrad 120 (und höher) wird berücksichtigt, dass Spalten in OrderTable mit *ansteigenden* Daten Werte aufweisen können, die über dem von der Statistik aufgezeichneten Maximalwert liegen. Dies verbessert den Abfrageplan für SQL-SELECT-Anweisungen wie die folgende.  
  
```tsql  
SELECT CustomerId, OrderAddedDate  
    FROM OrderTable  
    WHERE OrderAddedDate >= '2016-05-01';  
```  
  
### Beispiel B. Die Kardinalitätsschätzung berücksichtigt, dass gefilterte Prädikate in der gleichen Tabelle häufig korrelieren.  
  
Die folgende SELECT-Anweisung zeigt gefilterte Prädikate für „Make“ und „Model“. Wir verstehen intuitiv, dass eine Möglichkeit besteht, dass das Modell „Civic“ heißt, wenn die Marke „Honda“ lautet, da Honda den Civic herstellt.  
  
Bei der Kardinalitätsschätzung mit Kompatibilitätsgrad 120 wird berücksichtigt, dass eine Korrelation zwischen den beiden Spalten „Make“ und „Model“ existieren kann, die sich in der gleichen Tabelle befinden. Die Kardinalitätsschätzung kann genauer einschätzen, wie viele Zeilen von der Abfrage zurückgegeben werden, und der Abfrageoptimierer generiert einen besseren Plan.  
  
```tsql  
SELECT Model_Year, Purchase_Price  
    FROM dbo.Cars  
    WHERE  
        Make  = 'Honda'  AND  
        Model = 'Civic';  
```  
  
### Beispiel C. Die Kardinalitätsschätzung geht nicht mehr von einer Korrelation zwischen gefilterten Prädikaten aus verschiedenen Tabellen aus  
  
Umfangreiche neue Untersuchungen moderner Arbeitslasten und tatsächlicher Geschäftsdaten haben ergeben, dass Prädikatfilter aus unterschiedlichen Tabellen üblicherweise nicht korrelieren. In der folgenden Abfrage nimmt die Kardinalitätsschätzung an, dass zwischen „s.type“ und „r.date“ kein Zusammenhang besteht. Daher wird die Anzahl der zurückgegebenen Zeilen niedriger eingeschätzt.  
  
```tsql  
SELECT s.ticket, s.customer, r.store  
    FROM  
                   dbo.Sales    AS s  
        CROSS JOIN dbo.Returns  AS r  
    WHERE  
        s.ticket = r.ticket  AND  
        s.type   = 'toy'     AND  
        r.date   = '2016-05-11';  
```  
  
  
## Siehe auch  
 [Überwachen und Optimieren der Leistung](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
