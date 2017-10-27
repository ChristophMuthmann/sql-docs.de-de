---
title: Bestimmen, ob eine Tabelle oder eine gespeicherte Prozedur zu In-Memory OLTP portiert werden soll | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 08/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analyze, Migrate, Report
- AMR
ms.assetid: c1ef96f1-290d-4952-8369-2f49f27afee2
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: b18d5078244bf83d8820bf3f03039ac120287f8a
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp"></a>Bestimmen, ob eine Tabelle oder eine gespeicherte Prozedur zu In-Memory OLTP portiert werden soll
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Mit dem Bericht zur Transaktionsleistungsanalyse in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] können Sie einschätzen, ob In-Memory-OLTP die Leistung Ihrer Datenbankanwendung verbessern kann. Der Bericht gibt darüber hinaus an, welchen Arbeitsaufwand Sie leisten müssen, um In-Memory-OLTP in Ihrer Anwendung zu aktivieren. Nachdem Sie eine datenträgerbasierte Tabelle identifiziert haben, die Sie zur Verwendung von In-Memory-OLTP portieren, können Sie die Tabellenmigration mit dem [Ratgeber für die Speicheroptimierung](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md)vereinfachen. In ähnlicher Weise unterstützt Sie der [Ratgeber für native Kompilierung](../../relational-databases/in-memory-oltp/native-compilation-advisor.md) bei der Portierung einer gespeicherten Prozedur in eine nativ kompilierte gespeicherte Prozedur. Weitere Informationen zu Migrationsmethoden finden Sie unter [In-Memory-OLTP − Allgemeine Arbeitsauslastungsmuster und Überlegungen zur Migration](https://msdn.microsoft.com/library/dn673538.aspx).  
  
 Der Bericht zur Transaktionsleistungsanalyse wird direkt gegen die Produktionsdatenbank oder eine Testdatenbank ausgeführt, deren aktive Arbeitsauslastung der Arbeitsauslastung der Produktion ähnelt.  
  
 Die Bericht- und die Migrationsratgeber helfen Ihnen, die folgenden Aufgaben auszuführen:  
  
-   Analysieren Sie Ihre Arbeitsauslastung, um Hotspots zu ermitteln, bei denen In-Memory OLTP potenziell zu einer Leistungsverbesserung beitragen kann. Der Bericht zur Transaktionsleistungsanalyse empfiehlt Tabellen und gespeicherte Prozeduren, die von der Konvertierung in In-Memory-OLTP am meisten profitieren würden.  
  
-   Hilfe bei der Planung und Durchführung der Migration zu In-Memory OLTP. Der Migrationspfad von einer datenträgerbasierten Tabelle zu einer speicheroptimierten Tabelle kann zeitaufwendig sein. Mit dem Ratgeber für die Speicheroptimierung können Sie Inkompatibilitäten in Ihrer Tabelle identifizieren, die Sie entfernen müssen, bevor Sie die Tabelle zu In-Memory OLTP verschieben. Der Ratgeber für die Speicheroptimierung gibt außerdem Aufschluss über die Auswirkungen, die die Migration einer Tabelle zu einer speicheroptimierten Tabelle auf Ihre Anwendung haben wird.  
  
     Sie können ermitteln, ob Ihre Anwendung von In-Memory OLTP profitieren würde. Außerdem können Sie OLTP verwenden, um die Migration zu In-Memory OLTP zu planen und um einige Ihrer Tabellen und gespeicherten Prozeduren zu In-Memory OLTP zu migrieren.  
  
    > [!IMPORTANT]  
    >  Die Leistung eines Datenbanksystems hängt von verschiedenen Faktoren ab, die jedoch nicht alle durch den Transaktionsleistungssammler beobachtet und gemessen werden können. Daher gewährleistet der Transaktionsleistungsanalysebericht nicht, dass die tatsächlichen Leistungssteigerungen den ggf. getroffenen Vorhersagen entsprechen.  
  
 Der Bericht zur Transaktionsleistungsanalyse und die Migrationsratgeber werden im Rahmen von SQL Server Management Studio (SSMS) installiert, wenn Sie bei der Installation von **Verwaltungstools – Einfach** oder **Verwaltungstools – Erweitert** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]auswählen, oder wenn Sie [SQL Server Management Studio herunterladen](https://msdn.microsoft.com/library/mt238290.aspx).    
  
## <a name="transaction-performance-analysis-reports"></a>Berichte zur Transaktionsleistungsanalyse  
 Sie können Berichte zur Transaktionsleistungsanalyse erstellen, indem Sie im **Objekt-Explorer** mit der rechten Maustaste auf die Datenbank klicken und nacheinander **Berichte**, **Standardberichte**und **Übersicht der Transaktionsleistungsanalyse**auswählen. Die Datenbank muss eine aktive oder eine kurz zuvor ausgeführte Arbeitsauslastung aufweisen, damit ein aussagekräftiger Analysebericht erstellt werden kann.  
  
### <a name="tables"></a>Tabellen
  
 Der Detailbericht für eine Tabelle umfasst drei Abschnitte:  
  
-   Abschnitt zur Scanstatistik  
  
     Dieser Abschnitt enthält eine einzelne Tabelle mit den Statistiken, die zu Scans für die Datenbanktabelle gesammelt wurden. Folgende Spalten sind enthalten:  
  
    -   Prozent der Gesamtzahl der Zugriffe. Der Prozentsatz der Scans und Suchvorgänge für diese Tabelle im Verhältnis zur Aktivität für die gesamte Datenbank. Je höher der Prozentsatz, desto stärker wird die Tabelle im Vergleich zu anderen Tabellen in der Datenbank verwendet.  
  
    -   Statistik zu Suchläufen/Bereichsscans. In dieser Spalte wird die Anzahl der Punktsuchen und Bereichsscans (Indexscans und Tabellenscans) aufgeführt, die während der Profilerstellung für die Tabelle durchgeführt wurden. Der Durchschnitt je Transaktion beruht auf einer Schätzung.  
    
-   Abschnitt zur Konfliktstatistik  
  
     Dieser Abschnitt enthält eine Tabelle mit den Konflikten für die Datenbanktabelle. Weitere Informationen zu Datenbanklatches und -sperren finden Sie unter „Sperrenarchitektur“. Es gibt folgende Spalten:  
  
    -   Prozent der Gesamtwartevorgänge. Der Prozentsatz der Latch- und Sperrenwartevorgänge für diese Datenbanktabelle im Verhältnis zur Aktivität für die Datenbank. Je höher der Prozentsatz, desto stärker wird die Tabelle im Vergleich zu anderen Tabellen in der Datenbank verwendet.  
  
    -   Latchstatistik. In diesen Spalten wird die Anzahl der Latchwartevorgänge bei Abfragen, die diese Tabelle betreffen, aufgeführt. Weitere Informationen zu Latches finden Sie unter „Latching“. Je höher diese Zahl ist, desto mehr Latchkonflikte treten für die Tabelle auf.  
  
    -   Sperrenstatistik. In dieser Gruppe von Spalten wird die Anzahl der Sperrenerhalt- und -wartevorgänge für Seiten bei Abfragen, die diese Tabelle betreffen, aufgeführt. Weitere Informationen zu Sperren finden Sie unter „Grundlegendes zu Sperren in SQL Server“. Je höher die Anzahl der Wartevorgänge ist, desto mehr Sperrenkonflikte treten für die Tabelle auf.  
  
-   Abschnitt zu Migrationsproblemen  
  
     Dieser Abschnitt enthält eine Tabelle, die angibt, wie schwierig es ist, diese Datenbanktabelle in eine speicheroptimierte Tabelle zu konvertieren. Je höher die Schwierigkeitsbewertung, desto schwieriger ist die Konvertierung der Tabelle. Ausführliche Informationen zum Konvertieren dieser Datenbanktabelle erhalten Sie im Ratgeber für die Speicheroptimierung.  
  
Scan- und Konfliktstatistiken für den Tabellendetailbericht werden aus „sys.dm_db_index_operational_stats“ (Transact-SQL) gesammelt und aggregiert.  

### <a name="stored-procedures"></a>Gespeicherte Prozeduren

 Eine gespeicherte Prozedur mit hoher CPU-Zeit im Verhältnis zur verstrichenen Zeit ist ein Kandidat für die Migration. Der Bericht zeigt alle Tabellenverweise an, da systemintern kompilierte gespeicherte Prozeduren nur auf speicheroptimierte Tabellen verweisen können. Das kann den Migrationsaufwand weiter erhöhen.  
  
 Der Detailbericht für eine gespeicherte Prozedur umfasst zwei Abschnitte:  
  
-   Abschnitt zur Ausführungsstatistik  
  
     Dieser Abschnitt enthält eine Tabelle mit den Statistiken, die zur Ausführung der gespeicherten Prozedur gesammelt wurden. Es gibt folgende Spalten:  
  
    -   Cachezeit. Die Zwischenspeicherungsdauer des Ausführungsplans. Wenn die gespeicherte Prozedur aus dem Plancache entfernt und wieder hinzugefügt wird, werden Zeiten für jeden Cache angegeben.  
  
    -   Gesamte CPU-Zeit. Die gesamte CPU-Zeit, die die gespeicherte Prozedur während der Profilerstellung genutzt hat. Je höher diese Zahl ist, desto mehr CPU-Leistung hat die gespeicherte Prozedur genutzt.  
  
    -   Gesamtausführungszeit. Die Gesamtdauer der Ausführungszeit, die die gespeicherte Prozedur während der Profilerstellung genutzt hat. Je höher die Differenz zwischen dieser Zahl und der CPU-Zeit ist, desto weniger effizient nutzt die gespeicherte Prozedur die CPU.  
  
    -   Cachefehler gesamt. Die Anzahl der Cachefehler (Lesevorgänge aus dem physischen Speicher), die durch die Ausführung der gespeicherten Prozedur während der Profilerstellung verursacht wurden.  
  
    -   Ausführungsanzahl. Gibt an, wie oft diese gespeicherte Prozedur während der Profilerstellung ausgeführt wurde.  
  
-   Abschnitt zu Tabellenverweisen  
  
     Dieser Abschnitt enthält eine Tabelle mit den Tabellen, auf die diese gespeicherte Prozedur verweist. Vor dem Konvertieren der gespeicherten Prozedur in eine systemintern kompilierte gespeicherte Prozedur müssen alle diese Tabellen in speicheroptimierte Tabellen konvertiert werden, und sie müssen auf demselben Server und in derselben Datenbank verbleiben.  
  
 Die Ausführungsstatistik für den Detailbericht zu gespeicherten Prozeduren wird aus „sys.dm_exec_procedure_stats“ (Transact-SQL) gesammelt und aggregiert. Die Verweise werden aus „sys.sql_expression_dependencies“ (Transact-SQL) abgerufen.  
  
 Verwenden Sie den Ratgeber für native Kompilierung, um Details zum Konvertieren einer gespeicherten Prozedur in eine nativ kompilierte gespeicherte Prozedur anzuzeigen.  
  
## <a name="generating-in-memory-oltp-migration-checklists"></a>Prüflisten für die In-Memory-OLTP-Migration erstellen  
 Prüflisten für die Migration identifizieren alle Funktionen einer Tabelle oder gespeicherten Prozedur, die nicht mit speicheroptimierten Tabellen oder nativ kompilierten gespeicherten Prozeduren unterstützt werden. Die Speicheroptimierung und der native Kompilierungsratgeber können eine Prüfliste für eine einzelne datenträgerbasierte Tabelle oder mit T-SQL interpretierte gespeicherte Prozedur. Es besteht außerdem die Möglichkeit, Prüflisten für die Migration mehrerer Tabellen und gespeicherter Prozeduren in einer Datenbank zu generieren.  
  
 Sie können in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Migrationsprüfliste mithilfe des Befehls **Prüflisten für die Migration zum In-Memory-OLTP erstellen** oder mithilfe von PowerShell generieren.  
  
**So generieren Sie eine Migrationsprüfliste über die Benutzeroberfläche**  
  
1.  Klicken Sie im **Objekt-Explorer**mit der rechten Maustaste auf eine Datenbank, die nicht die Systemdatenbank ist. Klicken Sie auf **Aufgaben**und anschließend auf **Prüflisten für die Migration zum In-Memory-OLTP erstellen**.  
  
2.  Klicken Sie im Dialogfeld „Prüflisten für die Migration zum In-Memory-OLTP erstellen“ auf „Weiter“, um zur Seite **Optionen für die Prüflistenerstellung konfigurieren** zu navigieren. Führen Sie auf dieser Seite die folgenden Aktionen aus.  
  
    1.  Geben Sie einen Ordnerpfad in das Feld **Prüfliste speichern in** ein.  
  
    2.  Überprüfen Sie, ob **Prüflisten für bestimmte Tabellen und gespeicherte Prozeduren erstellen** ausgewählt ist.  
  
    3.  Erweitern Sie im Auswahlbereich die Knoten **Tabelle** und **Gespeicherte Prozedur** .  
  
    4.  Wählen Sie einige Objekte im Auswahlbereich aus.  
  
3.  Klicken Sie auf **Weiter** , und bestätigen Sie, dass die Liste der Aufgaben Ihren Einstellungen auf der Seite **Optionen für die Prüflistenerstellung konfigurieren** entspricht.  
  
4.  Klicken Sie auf **Fertig stellen**, und bestätigen Sie, dass die Migrationsprüflistenberichte nur für die von Ihnen ausgewählten Objekte generiert wurden.  
  
 Sie können die Genauigkeit der Berichte überprüfen, indem Sie sie mit den Berichten vergleichen, die von den Tools „Speicheroptimierungsratgeber“ und „Ratgeber für native Kompilierung“ erstellt wurden. Weitere Informationen finden Sie unter [Ratgeber für die Speicheroptimierung](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md) und [Ratgeber für native Kompilierung](../../relational-databases/in-memory-oltp/native-compilation-advisor.md).  
  
**So generieren Sie eine Migrationsprüfliste mithilfe von SQL Server PowerShell**  
  
1.  Klicken Sie im **Objekt-Explorer**auf eine Datenbank und anschließend auf **PowerShell starten**. Überprüfen Sie, ob die folgende Eingabeaufforderung angezeigt wird.  
  
    ```  
    PS SQLSERVER: \SQL\{Instance Name}\DEFAULT\Databases\{two-part DB Name}>  
    ```  
  
2.  Geben Sie den folgenden Befehl ein.  
  
    ```  
    Save-SqlMigrationReport –FolderPath “<folder_path>”  
    ```  
  
3.  Überprüfen Sie Folgendes.  
  
    -   Der Ordnerpfad wird erstellt, wenn er noch nicht existiert.  
  
    -   Der Migrationsprüflistenbericht wird für alle Tabellen und gespeicherten Prozeduren in der Datenbank generiert. Er befindet sich an dem durch „folder_path“ angegebenen Speicherort.  
  
**So generieren Sie eine Migrationsprüfliste mithilfe von Windows PowerShell**  
  
1.  Starten Sie eine Windows PowerShell-Sitzung mit erhöhten Rechten.  
  
2.  Geben Sie die folgenden Befehle ein. Das Objekt kann entweder eine Tabelle oder eine gespeicherte Prozedur sein.  
  
    ```  
    [System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.SMO')  
  
    ```  
  
    ```  
    Save-SqlMigrationReport –Server "<instance_name>" -Database "<db_name>" -FolderPath "<folder_path1>"  
  
    ```  
  
    ```  
    Save-SqlMigrationReport –Server "<instance_name>" -Database "<db_name>" -Object <object_name> -FolderPath "<folder_path2>"  
  
    ```  
  
3.  Überprüfen Sie Folgendes.  
  
    -   Ein Migrationsprüflistenbericht wird für alle Tabellen und gespeicherten Prozeduren in der Datenbank generiert. Er befindet sich an dem durch „folder_path“ angegebenen Speicherort.  
  
    -   Ein Migrationsprüflistenbericht für <Objekt_Name> ist der einzige Bericht an dem von „folder_path2“ angegebenen Speicherort.  
  
## <a name="see-also"></a>Siehe auch  
 [Migrieren zu In-Memory OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  

