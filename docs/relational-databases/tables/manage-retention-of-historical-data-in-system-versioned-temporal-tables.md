---
title: Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7925ebef-cdb1-4cfe-b660-a8604b9d2153
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 41c64af6ffe805d6b0b92ffde0c7057a7cd2abca
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="manage-retention-of-historical-data-in-system-versioned-temporal-tables"></a>Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Durch temporale Tabellen mit Systemversionsverwaltung kann die Verlaufstabelle die Datenbank stärker vergrößern als reguläre Tabellen, insbesondere in den folgenden Situationen:  
  
-   Sie behalten Verlaufsdaten für eine langen Zeitraum bei.  
  
-   Ihr Muster für Datenänderungen erfordert umfangreiche Aktualisierungen oder Löschungen.  
  
 Eine große und ständig wachsende Verlaufstabelle kann zu einem Problem werden, sowohl aufgrund der reinen Speicherkosten als auch durch Leistungsbeeinträchtigungen aufgrund von temporalen Abfragen. Daher ist die Entwicklung einer Datenbeibehaltungsrichtlinie für die Verwaltung von Daten in der Verlaufstabelle ein wichtiger Aspekt der Planung und Verwaltung des Lebenszyklus aller temporalen Tabellen.  
  
## <a name="data-retention-management-for-history-table"></a>Verwaltung der Datenbeibehaltung für die Verlaufstabelle  
 Das Verwalten der Datenbeibehaltung für temporale Tabellen beginnt damit, die Beibehaltungsdauer für jede temporale Tabelle zu bestimmen. Ihrer Beibehaltungsrichtlinie sollte in den meisten Fällen als Teil der Geschäftslogik der Anwendung betrachtet werden, die die temporalen Tabellen verwendet. Für Anwendungen in Datenüberwachungs- und Zeitreiseszenarien gelten beispielsweise feste Anforderungen dafür, wie lange Verlaufsdaten für Onlineabfragen verfügbar sein müssen.  
  
 Nachdem Sie die Beibehaltungsdauer bestimmt haben, ist der nächste Schritt, einen Plan für die Verwaltung von Verlaufsdaten zu entwickeln. Dazu gehört, wie und wo Sie Verlaufsdaten speichern und wie Sie Verlaufsdaten löschen, die älter sind, als die Beibehaltungsanforderungen vorsehen. Die folgenden vier Ansätze für das Verwalten von Verlaufsdaten in der temporalen Verlaufstabelle stehen Ihnen zur Verfügung:  
  
-   [Stretch Database](https://msdn.microsoft.com/library/mt637341.aspx#using-stretch-database-approach)  
  
-   [Tabellenpartitionierung](https://msdn.microsoft.com/library/mt637341.aspx#using-table-partitioning-approach)  
  
-   [Benutzerdefiniertes Bereinigungsskript](https://msdn.microsoft.com/library/mt637341.aspx#using-custom-cleanup-script-approach)  

-   [Beibehaltungsrichtlinie](https://msdn.microsoft.com/library/mt637341.aspx#using-temporal-history-retention-policy-approach)  

 Bei jedem dieser Ansätze basiert die Logik für die Migration oder Bereinigung von Verlaufsdaten auf der Spalte, die dem Ende der Dauer in der aktuellen Tabelle entspricht. Der Wert für das Ende der Dauer für jede Zeile bestimmt den Moment, an dem die Zeilenversion „geschlossen“ wird, an dem sie also in die Verlaufstabelle aufgenommen wird. Beispielsweise gibt die Bedingung `SysEndTime < DATEADD (DAYS, -30, SYSUTCDATETIME ())` an, dass Verlaufsdaten, die älter als einen Monat sind, aus der Verlaufstabelle entfernt oder verschoben werden müssen.  
  
> **HINWEIS:**  In den Beispielen in diesem Thema wird dieses [Beispiel für eine temporale Tabelle](creating-a-system-versioned-temporal-table.md)verwendet.  
  
## <a name="using-stretch-database-approach"></a>Verwenden des Ansatzes mit Stretch-Datenbank  
  
> **HINWEIS:**  Der Ansatz mit Stretch-Datenbank kann nur für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verwendet werden, aber nicht für [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 [Stretch-Datenbank](../../sql-server/stretch-database/stretch-database.md) in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] migriert die Verlaufsdaten transparent zu Azure. Zur Erhöhung der Sicherheit können Sie Daten während der Übertragung mit der SQL Server-Funktion [Always Encrypted](https://msdnstage.redmond.corp.microsoft.com/library/mt163865.aspx) verschlüsseln. Darüber hinaus können Sie zum Schutz Ihrer Daten [Sicherheit auf Zeilenebene](../../relational-databases/security/row-level-security.md) und andere erweiterte SQL Server-Sicherheitsfeatures für eine temporale Datenbank und Stretch-Datenbank verwenden.  
  
 Mit Stretch Database können Sie für einige oder alle Ihrer temporalen Verlaufstabellen ein Stretching auf Azure durchführen, und SQL Server verschiebt Verlaufsdaten im Hintergrund nach Azure. Durch die Aktivierung von Stretch für eine Verlaufstabelle ändert sich die Interaktion mit der temporalen Tabelle im Hinblick auf Datenänderungen und temporale Abfragen nicht.  
  
-   **Strecken der gesamten Verlaufstabelle:** Konfigurieren Sie Stretch-Datenbank für die gesamte Verlaufstabelle, wenn das wichtigste Szenario die Datenüberwachung in einer Umgebung mit häufigen Datenänderungen und relativ seltenen Abfragen von Verlaufsdaten ist.  Verwenden Sie diesen Ansatz also, wenn die Leistung temporaler Abfragen nicht entscheidend ist. In diesem Fall kann die von Azure bereitgestellte Kosteneffizienz interessant sein.   
    Beim Stretching der gesamten Verlaufstabelle können Sie den Stretch-Assistenten oder Transact-SQL verwenden. Beispiele für beides sind weiter unten aufgeführt.  
  
-   **Strecken eines Teils der Verlaufstabelle:** Konfigurieren Sie Stretch-Datenbank nur für einen Teil der Verlaufstabelle, um die Leistung zu verbessern, wenn Ihr wichtigstes Szenario in erster Linie das Abfragen aktueller Verlaufsdaten beinhaltet, Sie aber die Option zum Abfragen älterer Verlaufsdaten bei Bedarf beibehalten möchten, solange diese Daten remote zu geringeren Kosten gespeichert werden. Mit Transact-SQL erreichen Sie dies, indem Sie eine Prädikatfunktion angeben, um die Zeilen auszuwählen, die aus der Verlaufstabelle migriert werden, statt alle Zeilen zu migrieren.  Wenn Sie mit temporalen Tabellen arbeiten, ist es in der Regel sinnvoll, Daten basierend auf einer Zeitbedingung zu verschieben (d. h. basierend auf dem Alter der Zeilenversion in der Verlaufstabelle).    
    Wenn Sie eine deterministische Prädikatfunktion verwenden, können Sie einen Teil des Verlaufs in derselben Datenbank zusammen mit den aktuellen Daten behalten, während der Rest zu Azure migriert wird.    
    Beispiele und Informationen zu Einschränkungen finden Sie unter [Auswählen zu migrierender Zeilen mithilfe einer Filterfunktion (Stretch-Datenbank)](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md) Da nicht deterministische Funktionen nicht gültig sind, wenn Sie Verlaufsdaten in der Form eines gleitendes Fensters übertragen möchten, müssten Sie die Definition der Inlineprädikatfunktion regelmäßig ändern, damit das Fenster von Zeilen, das Sie lokal speichern, im Hinblick auf das Alter konstant ist. Mit einem gleitenden Fenster können Sie Verlaufsdaten, die älter als ein Monat sind, kontinuierlich nach Azure verschieben. Ein Beispiel dieses Ansatzes ist weiter unten dargestellt.  
  
> **HINWEIS:** Stretch-Datenbank migriert Daten zu Azure. Daher benötigen Sie ein Azure-Konto und ein Abonnement für die Abrechnung. Um ein kostenloses Azure-Testkonto zu erhalten, melden Sie sich für eine [einmonatige kostenlose Testversion](https://azure.microsoft.com/pricing/free-trial/)an.  
  
 Sie können eine temporale Verlaufstabelle für Stretch mit dem Stretch-Assistenten oder Transact-SQL konfigurieren, und Sie können eine temporale Verlaufstabelle für Stretch aktivieren, wenn die Systemversionsverwaltung auf **ON**festgelegt ist. Ein Stretching der aktuellen Tabelle ist nicht zulässig, da es nicht sinnvoll ist, für die aktuelle Tabelle ein Stretching durchzuführen.  
  
### <a name="using-the-stretch-wizard-to-stretch-the-entire-history-table"></a>Verwenden des Stretch-Assistenten für ein Stretching der gesamten Verlaufstabelle  
 Die einfachste Methode für Anfänger ist, den Stretch-Assistenten zu verwenden, um Stretch für die gesamte Datenbank zu aktivieren. Wählen Sie dann die temporale Verlaufstabelle im Stretch-Assistenten aus (in diesem Beispiel wird davon ausgegangen, dass Sie die Department-Tabelle als eine temporale Tabelle mit Systemversionsverwaltung in einer ansonsten leeren Datenbank konfiguriert haben). In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]können Sie nicht mit der rechten Maustaste auf die temporale Verlaufstabelle selbst klicken und dann auf „Stretch“ klicken.  
  
1.  Klicken Sie mit der rechten Maustaste auf die Datenbank, und zeigen Sie auf **Aufgaben**, zeigen Sie auf **Stretch**, und klicken Sie dann auf **Aktivieren** , um den Assistenten zu starten.  
  
2.  Aktivieren Sie im Fenster **Tabellen auswählen** das Kontrollkästchen für die temporale Verlaufstabelle, und klicken Sie auf „Weiter“.  
  
     ![Auswählen der Verlaufstabelle auf der Seite „Tabellen auswählen“](../../relational-databases/tables/media/stretch-wizard-2-for-temporal.png "Auswählen der Verlaufstabelle auf der Seite „Tabellen auswählen“")  
  
3.  Geben Sie im Fenster **Azure konfigurieren** Ihre Anmeldeinformationen an. Melden Sie sich bei Microsoft Azure an, oder registrieren Sie sich für ein Konto. Wählen Sie das zu verwendende Abonnement und die Azure-Region aus. Erstellen Sie dann einen neuen Server, oder wählen Sie einen vorhandenen Server aus. Klicken Sie auf **Weiter**.  
  
     ![Erstellen neuer Azure-Server – Stretch-Datenbank-Assistent](../../relational-databases/tables/media/stretch-wizard-4.png "Erstellen neuer Azure-Server – Stretch-Datenbank-Assistent")  
  
4.  Geben Sie im Fenster **Sichere Anmeldeinformationen** ein Kennwort für den Datenbankhauptschlüssel an, um Ihre Anmeldeinformationen für die SQL Server-Quelldatenbank zu schützen, und klicken Sie dann auf „Weiter“.  
  
     ![Sichere Anmeldeinformationenseite des Stretch-Datenbank-Assistenten](../../relational-databases/tables/media/stretch-wizard-6.png "Sichere Anmeldeinformationenseite des Stretch-Datenbank-Assistenten")  
  
5.  Geben Sie im Fenster **IP-Adresse auswählen** den IP-Adressbereich für Ihre SQL Server-Instanz an, um Ihrem Azure-Server die Kommunikation mit SQL Server zu ermöglichen (bei Auswahl eines vorhandenen Servers, für den bereits eine Firewallregel vorhanden ist, klicken Sie hier einfach auf „Weiter“, um die vorhandene Firewallregel zu verwenden). Klicken Sie auf **Weiter** dann auf **Fertig stellen**, um Stretch Database zu aktivieren und ein Stretching für die temporale Verlaufstabelle durchzuführen.  
  
     ![Wählen der IP-Adressseite des Stretch-Datenbank-Assistenten](../../relational-databases/tables/media/stretch-wizard-7.png "Wählen der IP-Adressseite des Stretch-Datenbank-Assistenten")  
  
6.  Überprüfen Sie nach Abschluss des Assistenten, ob die Datenbank erfolgreich für Stretch aktiviert wurde. Beachten Sie die Symbole im Objekt-Explorer, die angeben, dass für die Datenbank ein Stretching durchgeführt wurde.  
  
> **HINWEIS:** Wenn das Aktivieren der Datenbank für Stretch fehlschlägt, überprüfen Sie das Fehlerprotokoll. Ein häufiger Fehler ist eine fehlerhafte Konfiguration der Firewallregel.  
  
 Siehe auch:  
  
-   [Aktivieren von Stretch-Datenbank für eine Datenbank](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)  
  
-   [Erste Schritte durch Ausführen des Assistenten zum Aktivieren von Stretch für eine Datenbank](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)  
  
-   [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
### <a name="using-transact-sql-to-stretch-the-entire-history-table"></a>Verwenden von Transact-SQL zum Durchführen eines Stretchings der gesamten Verlaufstabelle  
 Sie können alternativ Transact-SQL verwenden, um die Streckung für den lokalen Server zu aktivieren, und [Stretch-Datenbank für eine Datenbank zu aktivieren](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md). Sie können dann  [Transact-SQL verwenden, um Stretch-Datenbank für eine Tabelle zu aktivieren](https://msdn.microsoft.com/library/mt605115.aspx#Anchor_1). Führen Sie mit einer Datenbank, die zuvor für Stretch Database aktiviert wurde, das folgende Transact-SQL-Skript aus, um für eine vorhandene temporale Verlaufstabelle mit Systemversionsverwaltung ein Stretching durchzuführen:  
  
```  
ALTER TABLE <history table name>   
SET (REMOTE_DATA_ARCHIVE = ON (MIGRATION_STATE = OUTBOUND));  
```  
  
### <a name="using-transact-sql-to-stretch-a-portion-of-the-history-table"></a>Verwenden von Transact-SQL zum Durchführen eines Stretchings für einen Teil der Verlaufstabelle  
 Um nur für einen Teil der Verlaufstabelle ein Stretching durchzuführen, erstellen Sie zunächst eine [Inlineprädikatfunktion](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md). In diesem Beispiel gehen wir davon aus, dass Sie zum ersten Mal am 1. Dezember 2015 die Inlineprädikatfunktion konfiguriert haben und dass für alle Verlaufsdaten, die vor dem 1. November 2015 gespeichert wurden, ein Stretching auf Azure durchgeführt werden soll. Um dies zu erreichen, erstellen Sie zunächst die folgende Funktion:  
  
```  
CREATE FUNCTION dbo.fn_StretchBySystemEndTime20151101(@systemEndTime datetime2)   
RETURNS TABLE   
WITH SCHEMABINDING    
AS    
RETURN SELECT 1 AS is_eligible   
  WHERE @systemEndTime < CONVERT(datetime2, '2015-11-01T00:00:00', 101) ;  
```  
  
 Als Nächstes verwenden Sie das folgende Skript, um das Filterprädikat der Verlaufstabelle hinzuzufügen und den Migrationsstatus auf OUTBOUND festzulegen und so eine prädikatbasierte Datenmigration für die Verlaufstabelle zu aktivieren.  
  
```  
ALTER TABLE <history table name>   
SET (   
        REMOTE_DATA_ARCHIVE = ON   
                (   
                        FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20151101 (SysEndTime)  
                                , MIGRATION_STATE = OUTBOUND   
                )  
        )   
;  
```  
  
 Um ein gleitendes Fenster beizubehalten, muss die Prädikatfunktion täglich exakt sein (ändern Sie also die Filterzeilenbedingung jeden Tag um einen Tag). Das folgende Skript ist das Skript, dass Sie am 2. Dezember 2015 ausführen müssten:  
  
```  
BEGIN TRAN  
           /*(1) Create new predicate function definition */  
        CREATE FUNCTION dbo.fn_StretchBySystemEndTime20151102(@systemEndTime datetime2)  
        RETURNS TABLE  
        WITH SCHEMABINDING   
        AS   
        RETURN SELECT 1 AS is_eligible  
               WHERE @systemEndTime < CONVERT(datetime2,'2015-11-02T00:00:00', 101)  
        GO  
  
        /*(2) Set the new function as filter predicate */  
        ALTER TABLE <history table name>  
        SET   
        (  
               REMOTE_DATA_ARCHIVE = ON  
               (  
                       FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20151102(SysEndTime),  
                       MIGRATION_STATE = OUTBOUND  
               )  
        )   
COMMIT ;  
```  
  
 Verwenden Sie den SQL Server-Agent oder einen anderen Planungsmechanismus, damit eine gültige Definition der Prädikatfunktion immer sichergestellt ist.  
  
## <a name="using-table-partitioning-approach"></a>Verwenden des Ansatzes mit Tabellenpartitionierung  
 Die[Tabellenpartitionierung](../partitions/create-partitioned-tables-and-indexes.md) kann bewirken, dass sich große Tabellen besser verwalten und skalieren lassen. Wenn Sie den Ansatz mit Tabellenpartitionierung verwenden, können Sie Verlaufstabellenpartitionen nutzen, um eine angepasste Datenbereinigung oder Offlinearchivierung basierend auf einer Zeitbedingung zu implementieren. Durch Tabellenpartitionierung erhalten Sie über die Partitionsentfernung auch Leistungsvorteile beim Abfragen von temporalen Tabellen für einen Teil des Datenverlaufs.  
  
 Mit der Tabellenpartitionierung können Sie den Ansatz mit einem gleitenden Fenster implementieren, um den ältesten Teil der Verlaufsdaten aus der Verlaufstabelle zu verschieben und die Größe des beibehaltenen Teils im Hinblick auf das Alter konstant zu halten. So verwalten Sie die Daten in der Verlaufstabelle entsprechend der erforderlichen Beibehaltungsdauer. Der Vorgang des Austauschens von Daten aus der Verlaufstabelle wird unterstützt, wenn SYSTEM_VERSIONING auf ON festgelegt ist. Dies bedeutet, dass ein Teil der Verlaufsdaten bereinigt werden kann, ohne ein Wartungsfenster einzurichten oder normale Arbeitsauslastungen zu blockieren.  
  
> **HINWEIS:** Für einen Partitionswechsel muss der gruppierte Index für die Verlaufstabelle am Partitionierungsschema ausgerichtet werden („SysEndTime“ muss enthalten sein). Die vom System erstellte Standardverlaufstabelle enthält einen gruppierten Index, der die Spalten „SysEndTime“ und „SysStartTime“ aufweist. Dies ist optimal für die Partitionierung, das Einfügen neuer Daten und normale temporale Abfragen. Weitere Informationen finden Sie unter [Temporal Tables](../../relational-databases/tables/temporal-tables.md).  
  
 Für den Ansatz mit einem gleitenden Fenster müssen Sie zwei Sätze von Aufgaben ausführen:  
  
-   Eine Partitionierungskonfigurationsaufgabe  
  
-   Aufgaben für die wiederholte Partitionswartung  
  
 Zur Veranschaulichung gehen wir davon aus, dass wir Verlaufsdaten für sechs Monate beibehalten möchten und dass die Daten der einzelnen Monate jeweils in einer separaten Partition gespeichert werden sollen. Außerdem nehmen wir an, dass wir im September 2015 die Systemversionsverwaltung aktiviert haben.  
  
 Mit einer Partitionierungskonfigurationsaufgabe wird die erste Partitionierungskonfiguration für die Verlaufstabelle erstellt. In diesem Beispiel würden wir eine Anzahl von Partitionen erstellen, die der Größe des gleitenden Fensters entspricht (in Monaten). Zusätzlich wird eine leere Partition vorbereitet (dies wird weiter unten erläutert). Mit dieser Konfiguration wird sichergestellt, dass das System neue Daten ordnungsgemäß speichern kann, wenn die Aufgabe für die wiederholte Partitionswartung das erste Mal ausgeführt wird. Zudem ist gewährleistet, dass wir Partitionen mit Daten nicht unterteilen, um teure Datenbewegungen zu vermeiden. Sie sollten diese Aufgabe mit Transact-SQL und dem weiter unten aufgeführten Beispielskript ausführen.  
  
 Die folgende Abbildung zeigt die erste Partitionierungskonfiguration, mit der Daten von 6 Monaten beibehalten werden.  
  
 ![Partitionierung](../../relational-databases/tables/media/partitioning.png "Partitionierung")  
  
> **HINWEIS:** Unter „Überlegungen zur Leistung bei der Tabellenpartitionierung“ weiter unten finden Sie Informationen zu Leistungseinbußen bei der Verwendung von RANGE LEFT oder RANGE RIGHT beim Konfigurieren der Partitionierung.  
  
 Beachten Sie, dass die untere bzw. die obere Grenze bei der ersten bzw. der letzten Partition „offen“ ist, um sicherzustellen, dass für jede neue Zeile eine Zielpartition vorhanden ist, unabhängig vom Wert in der Partitionierungsspalte.   
Im Laufe der Zeit werden neue Zeilen in der Verlaufstabelle in höhere Partitionen aufgenommen. Wenn die 6. Partition gefüllt wird, haben wir die vorgesehene Beibehaltungsdauer erreicht. Dies ist der Zeitpunkt, an dem die Aufgabe für die wiederholte Partitionswartung zum ersten Mal gestartet wird (sie muss in regelmäßigen Abständen ausgeführt werden, in diesem Beispiel einmal pro Monat).  
  
 Die folgende Abbildung veranschaulicht die Aufgabe für die wiederholte Partitionswartung (die genauen Schritte werden im Folgenden erläutert).  
  
 ![Partitionierung2](../../relational-databases/tables/media/partitioning2.png "Partitionierung2")  
  
 Die genauen Schritte für die Aufgabe für die wiederholte Partitionswartung:  
  
1.  SWITCH OUT: Erstellen Sie eine Stagingtabelle, und wechseln Sie dann eine Partition zwischen der Verlaufstabelle und der Stagingtabelle. Verwenden Sie dazu die Anweisung [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) mit dem Argument SWITCH PARTITION (siehe Beispiel „C. Wechseln von Partitionen zwischen Tabellen“).  
  
    ```  
    ALTER TABLE <history table> SWITCH PARTITION 1 TO <staging table>  
    ```  
  
     Nach dem Partitionswechsel können Sie optional die Daten aus der Stagingtabelle archivieren und dann die Stagingtabelle löschen oder kürzen, damit Sie vorbereitet sind, wenn Sie diese Aufgabe für die wiederholte Partitionswartung das nächste Mal ausführen müssen.  
  
2.  MERGE RANGE: Führen Sie die leere Partition 1 mit der Partition 2 zusammen. Verwenden Sie dazu [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md) mit MERGE RANGE (siehe Beispiel B). Durch Entfernen der untersten Grenze mit dieser Funktion führen Sie effektiv die leere Partition 1 mit der ehemaligen Partition 2 zusammen, sodass eine neue Partition 1 entsteht. Bei den anderen Partitionen werden ebenfalls die Ordinalzahlen geändert.  
  
3.  SPLIT RANGE: Erstellen Sie eine neue leere Partition 7. Verwenden Sie dazu [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md) mit SPLIT RANGE (siehe Beispiel A). Durch das Hinzufügen einer neuen oberen Grenze mit dieser Funktion erstellen Sie effektiv eine separate Partition für den kommenden Monat.  
  
### <a name="use-transact-sql-to-create-partitions-on-history-table"></a>Verwenden von Transact-SQL zum Erstellen von Partitionen in der Verlaufstabelle  
 Verwenden Sie das Transact-SQL-Skript im folgenden Codefenster, um die Partitionsfunktion und das Partitionsschema zu erstellen, und erstellen Sie den gruppierten Indexes so neu, dass die Partitionierung am Partitionsschema und den Partitionen ausgerichtet ist. In diesem Beispiel erstellen wir ein gleitendes Fenster für sechs Monate mit monatlichen Partitionen ab September 2015.  
  
```  
BEGIN TRANSACTION  
  
        /*Create partition function*/  
        CREATE PARTITION FUNCTION [fn_Partition_DepartmentHistory_By_SysEndTime] (datetime2(7))   
                    AS RANGE LEFT FOR VALUES   
                                (N'2015-09-30T23:59:59.999'  
                                , N'2015-10-31T23:59:59.999'  
                                , N'2015-11-30T23:59:59.999'  
                                , N'2015-12-31T23:59:59.999'  
                                , N'2016-01-31T23:59:59.999'  
                                , N'2016-02-29T23:59:59.999')  
  
        /*Create partition scheme*/  
        CREATE PARTITION SCHEME [sch_Partition_DepartmentHistory_By_SysEndTime]   
                        AS PARTITION [fn_Partition_DepartmentHistory_By_SysEndTime]   
                        TO ([PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY])  
  
        /*Re-create index to be partition-aligned with the partitioning schema*/  
        CREATE CLUSTERED INDEX [ix_DepartmentHistory] ON [dbo].[DepartmentHistory]  
        (  
                    [SysEndTime] ASC,  
                    [SysStartTime] ASC  
        )  
            WITH   
                        (PAD_INDEX = OFF  
                        , STATISTICS_NORECOMPUTE = OFF  
                        , SORT_IN_TEMPDB = OFF  
                        , DROP_EXISTING = ON  
                        , ONLINE = OFF  
                        , ALLOW_ROW_LOCKS = ON  
                        , ALLOW_PAGE_LOCKS = ON  
                        , DATA_COMPRESSION = PAGE)  
            ON [sch_Partition_DepartmentHistory_By_SysEndTime] ([SysEndTime])  
  
COMMIT TRANSACTION;  
  
```  
  
### <a name="using-transact-sql-to-maintain-partitions-in-sliding-window-scenario"></a>Verwenden von Transact-SQL zum Verwalten von Partitionen im Szenario mit gleitendem Fenster  
 Verwenden Sie das Transact-SQL-Skript im folgenden Codefenster, um Partitionen im Szenario mit gleitendem Fenster zu verwalten. In diesem Beispiel lagern wir die Partition für September 2015 mit MERGE RANGE aus und fügen dann eine neue Partition für März 2016 mit SPLIT RANGE hinzu.  
  
```  
BEGIN TRANSACTION  
  
         /*(1)  Create staging table */  
         CREATE TABLE [dbo].[staging_DepartmentHistory_September_2015]  
        (  
                 [DeptID] [int] NOT NULL  
                 , [DeptName] [varchar](50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL  
                 , [ManagerID] [int] NULL  
                 ,  [ParentDeptID] [int] NULL  
                 ,  [SysStartTime] [datetime2](7) NOT NULL  
                 ,  [SysEndTime] [datetime2](7) NOT NULL  
         ) ON [PRIMARY]  
         WITH  
         (  
              DATA_COMPRESSION = PAGE  
         )  
  
         /*(2) Create index on the same filegroups as the partition that will be switched out*/  
         CREATE CLUSTERED INDEX [ox_staging_DepartmentHistory_September_2015]    
         ON [dbo].[staging_DepartmentHistory_September_2015]  
         (  
                  [SysEndTime] ASC,  
                  [SysStartTime] ASC  
         )  
      WITH   
          (  
               PAD_INDEX = OFF  
               , SORT_IN_TEMPDB = OFF  
               , DROP_EXISTING = OFF  
               , ONLINE = OFF  
               , ALLOW_ROW_LOCKS = ON  
               , ALLOW_PAGE_LOCKS = ON  
          )   
         ON [PRIMARY]  
  
         /*(3) Create constraints matching the partition that will be switched out*/  
         ALTER TABLE [dbo].[staging_DepartmentHistory_September_2015]  WITH CHECK   
               ADD  CONSTRAINT [chk_staging_DepartmentHistory_September_2015_partition_1]   
                    CHECK  ([SysEndTime]<=N'2015-09-30T23:59:59.999')  
         ALTER TABLE [dbo].[staging_DepartmentHistory_September_2015]   
               CHECK CONSTRAINT [chk_staging_DepartmentHistory_September_2015_partition_1]  
  
         /*(4) Switch partition to staging table*/  
         ALTER TABLE [dbo].[DepartmentHistory]   
         SWITCH PARTITION 1 TO [dbo].[staging_DepartmentHistory_September_2015]   
         WITH (WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 MINUTES, ABORT_AFTER_WAIT = NONE))  
  
         /*(5) [Commented out] Optionally archive the data and drop staging table  
         INSERT INTO [ArchiveDB].[dbo].[DepartmentHistory]   
         SELECT * FROM [dbo].[staging_DepartmentHistory_September_2015];  
         DROP TABLE [dbo].[staging_DepartmentHIstory_September_2015];  
         */  
  
         /*(6) merge range to move lower boundary one month ahead*/  
         ALTER PARTITION FUNCTION [fn_Partition_DepartmentHistory_By_SysEndTime]()   
               MERGE RANGE(N'2015-09-30T23:59:59.999')  
  
         /*(7) Create new empty partition for "April and after" by creating new boundary point and specifying NEXT USED file group*/  
         ALTER PARTITION SCHEME [sch_Partition_DepartmentHistory_By_SysEndTime] NEXT USED [PRIMARY]  
         ALTER PARTITION FUNCTION [fn_Partition_DepartmentHistory_By_SysEndTime]() SPLIT RANGE(N'2016-03-31T23:59:59.999')  
  
COMMIT TRANSACTION  
  
```  
  
 Sie können das obige Skript etwas ändern und im regelmäßigen monatlichen Wartungsprozess verwenden:  
  
1.  Erstellen Sie in Schritt (1) eine neue Stagingtabelle für den Monat, den Sie entfernen möchten (Oktober wäre der nächste in unserem Beispiel).  
  
2.  Erstellen Sie in Schritt (3) eine CHECK-Einschränkung, die dem Monat entspricht, dessen Daten Sie entfernen möchten: `[SysEndTime]<=N'2015-10-31T23:59:59.999'` für die Oktober-Partition.  
  
3.  Ändern Sie in Schritt (4) Partition 1 in die neu erstellte Stagingtabelle.  
  
4.  Ändern Sie in Schritt (6) die Partitionsfunktion durch Zusammenführen der unteren Grenze: `MERGE RANGE(N'2015-10-31T23:59:59.999'` nach dem Auslagern der Daten für Oktober.  
  
5.  Teilen Sie in Schritt (7) die Partitionsfunktion durch Erstellen der neuen oberen Grenze: `SPLIT RANGE (N'2016-04-30T23:59:59.999'` nach dem Auslagern der Daten für Oktober.  
  
 Die optimale Lösung wäre jedoch, regelmäßig ein generisches Transact-SQL-Skript auszuführen, das die entsprechende Aktion monatlich ohne Skriptänderungen durchführen kann. Es ist möglich, das oben angeführte Skript zu verallgemeinern, um die bereitgestellten Parameter zu bearbeiten (die untere Grenze, die zusammengeführt werden muss, und die neue Grenze, die durch Teilen der Partition erstellt wird). Um zu vermeiden, dass jeden Monat Stagingtabellen erstellt werden, können Sie eine Stagingtabelle im Voraus erstellen und wiederverwenden, indem Sie die CHECK-Einschränkung entsprechend der Partition ändern, die ausgelagert wird. Sehen Sie sich die folgenden Seiten an, um Ideen für [die vollständige Automatisierung eines gleitenden Fensters](https://msdn.microsoft.com/library/aa964122.aspx) mithilfe eines Transact-SQL-Skripts zu bekommen.  
  
### <a name="performance-considerations-with-table-partitioning"></a>Überlegungen zur Leistung bei der Tabellenpartitionierung  
 Es ist äußerst wichtig, MERGE und SPLIT RANGE-Vorgänge durchzuführen, um das Verschieben von Daten zu vermeiden, da dies einen erheblichen Verarbeitungsaufwand verursachen kann. Weitere Informationen finden Sie unter [Ändern einer Partitionsfunktion](../../relational-databases/partitions/modify-a-partition-function.md). Verwenden Sie dazu RANGE LEFT statt RANGE RIGHT, wenn Sie [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md) verwenden.  
  
 Lassen Sie mich zuerst visuell die Bedeutung der Optionen RANGE LEFT und RANGE RIGHT erläutern:  
  
 ![Partitionierung3](../../relational-databases/tables/media/partitioning3.png "Partitionierung3")  
  
 Beim Definieren einer Partitionsfunktion als RANGE LEFT sind die angegebenen Werte die oberen Grenzen der Partitionen. Wenn Sie RANGE RIGHT verwenden, sind die angegebenen Werte die unteren Grenzen der Partitionen. Wenn Sie den MERGE RANGE-Vorgang verwenden, um eine Grenze aus der Definition der Partitionsfunktion zu entfernen, entfernt die zugrunde liegende Implementierung auch die Partition, die die Grenze enthält. Wenn diese Partition nicht leer ist, werden Daten in die Partition verschoben, die das Ergebnis des MERGE RANGE-Vorgangs ist.  
  
 Im Szenario mit gleitendem Fenster entfernen wir immer die unterste Partitionsgrenze.  
  
-   RANGE LEFT-Fall: Im RANGE LEFT-Fall gehört die unterste Partitionsgrenze zu Partition 1, die leer ist (nach dem Auslagern der Partition), sodass MERGE RANGE keine Datenverschiebungen verursacht.  
  
-   RANGE RIGHT-Fall: Im RANGE RIGHT-Fall gehört die unterste Partitionsgrenze zu Partition 2, die nicht leer ist, da wir davon ausgehen, dass Partition 1 durch Auslagern geleert wurde. In diesem Fall entstehen durch MERGE RANGE Datenverschiebungen (Daten von Partition 2 werden in Partition 1 verschoben). Um dies zu vermeiden, muss RANGE RIGHT im Szenario mit gleitendem Fenster eine Partition 1 aufweisen, die immer leer ist. Dies bedeutet, wenn wir RANGE RIGHT verwenden, sollten wir eine zusätzliche Partition im Vergleich mit dem RANGE LEFT-Fall erstellen und verwalten.  
  
 Fazit: Die Verwendung von RANGE LEFT in einer gleitenden Partition ist viel einfacher für die Partitionsverwaltung und vermeidet Datenverschiebungen. Das Definieren der Partitionsgrenzen mit RANGE RIGHT ist jedoch etwas einfacher, da Sie sich nicht um Probleme mit dem datetime-Zeittakt kümmern müssen.  
  
## <a name="using-custom-cleanup-script-approach"></a>Verwenden des Ansatzes mit einem benutzerdefiniertem Bereinigungsskript  
 In Fällen, in denen Stretch-Datenbank und Tabellenpartitionierung keine geeigneten Optionen sind, besteht der dritte Ansatz darin, die Daten mit dem benutzerdefinierten Bereinigungsskript aus der Verlaufstabelle zu löschen. Das Löschen von Daten aus einer Verlaufstabelle ist nur möglich, wenn **SYSTEM_VERSIONING = OFF**gilt. Um Dateninkonsistenz zu vermeiden, führen Sie die Bereinigung während des Wartungsfensters (wenn Arbeitsauslastungen, bei denen Daten geändert werden, nicht aktiv sind) oder innerhalb einer Transaktion (sodass andere Arbeitsauslastungen blockiert sind) durch.  Dieser Vorgang erfordert die **CONTROL** -Berechtigung für aktuelle Tabellen und Verlaufstabellen.  
  
 Um reguläre Anwendungen und Benutzerabfragen in möglichst geringem Umfang zu blockieren, löschen Sie Daten in kleineren Blöcken mit einer Verzögerung, wenn Sie das Bereinigungsskript innerhalb einer Transaktion ausführen. Es gibt zwar keine optimale Größe für jeden zu löschenden Datenblock für alle Szenarien, aber das Löschen von mehr als 10.000 Zeilen in einer einzigen Transaktion kann erhebliche Auswirkungen haben.  
  
 Die Bereinigungslogik ist für jede temporale Tabelle identisch, sodass relativ einfach eine Automatisierung über eine generische gespeicherte Prozedur möglich ist. Sie können die regelmäßige Ausführung dieser gespeicherten Prozedur für jede Tabelle planen, für die Sie den Datenverlauf einschränken möchten.  
  
 Das folgende Diagramm veranschaulicht, wie Ihre Bereinigungslogik für eine einzelne Tabelle strukturiert sein sollte, um die Auswirkungen auf die aktiven Arbeitsauslastungen zu verringern.  
  
 ![CustomCleanUpScriptDiagram](../../relational-databases/tables/media/customcleanupscriptdiagram.png "CustomCleanUpScriptDiagram")  
  
 Im Folgenden finden Sie einige allgemeine Richtlinien für die Implementierung des Prozesses. Planen Sie eine tägliche Ausführung der Bereinigungslogik, und wenden Sie sie auf alle temporalen Tabellen an, für die eine Datenbereinigung erforderlich ist. Verwenden Sie den SQL Server-Agent oder ein anderes Tool, um diesen Prozess zu planen:  
  
-   Löschen Sie Verlaufsdaten in allen temporalen Tabellen. Beginnen Sie dabei mit den ältesten Zeilen, und arbeiten Sie sich in mehrere Iterationen in kleinen Blöcken zu den letzten Zeilen vor. Vermeiden Sie das Löschen aller Zeilen in einer einzigen Transaktion, wie in der Abbildung weiter oben gezeigt.  
  
-   Implementieren Sie jede Iteration als Aufruf der generischen gespeicherten Prozedur, die einen Teil der Daten aus der Verlaufstabelle entfernt (diese Prozedur ist im Codebeispiel weiter unten dargestellt).  
  
-   Berechnen Sie jedes Mal, wenn Sie den Prozess aufrufen, wie viele Zeilen Sie für eine einzelne temporale Tabelle löschen müssen. Basierend darauf und auf der Anzahl der Iterationen müssen Sie dynamisch Teilungspunkte für jeden Prozeduraufruf bestimmen.  
  
-   Planen Sie eine Verzögerung zwischen Iterationen für eine einzelne Tabelle ein, um die Auswirkungen auf die Anwendungen zu reduzieren, die auf die temporale Tabelle zugreifen.  
  
 Eine gespeicherte Prozedur, die die Daten für eine einzelne temporale Tabelle löscht, kann wie der folgende Codeausschnitt aussehen (prüfen Sie diesen Code sorgfältig, und passen Sie ihn an, bevor Sie ihn in Ihrer Umgebung anwenden):  
  
```  
DROP PROCEDURE IF EXISTS sp_CleanupHistoryData;  
GO  
  
CREATE PROCEDURE sp_CleanupHistoryData  
         @temporalTableSchema sysname  
       , @temporalTableName sysname  
       , @cleanupOlderThanDate datetime2  
AS  
    DECLARE @disableVersioningScript nvarchar(max) = '';  
    DECLARE @deleteHistoryDataScript nvarchar(max) = '';  
    DECLARE @enableVersioningScript nvarchar(max) = '';  
  
DECLARE @historyTableName sysname    
DECLARE @historyTableSchema sysname    
DECLARE @periodColumnName sysname    
  
/*Generate script to discover history table name and end of period column for given temporal table name*/  
EXECUTE sp_executesql   
    N'SELECT @hst_tbl_nm = t2.name, @hst_sch_nm = s.name, @period_col_nm = c.name  
        FROM sys.tables t1   
           JOIN sys.tables t2 on t1.history_table_id = t2.object_id  
        JOIN sys.schemas s on t2.schema_id = s.schema_id  
            JOIN sys.periods p on p.object_id = t1.object_id  
           JOIN sys.columns c on p.end_column_id = c.column_id and c.object_id = t1.object_id  
                  WHERE   
                 t1.name = @tblName and s.name = @schName'  
                , N'@tblName sysname  
                , @schName sysname  
                , @hst_tbl_nm sysname OUTPUT  
                , @hst_sch_nm sysname OUTPUT  
                , @period_col_nm sysname OUTPUT'  
                , @tblName = @temporalTableName  
                , @schName = @temporalTableSchema  
                , @hst_tbl_nm = @historyTableName OUTPUT  
                , @hst_sch_nm = @historyTableSchema OUTPUT  
                , @period_col_nm = @periodColumnName OUTPUT   
  
IF @historyTableName IS NULL OR @historyTableSchema IS NULL OR @periodColumnName IS NULL  
    THROW 50010, 'History table cannot be found. Either specified table is not system-versioned temporal or you have provided incorrect argument values.', 1  
  
/*Generate 3 statements that will run inside a transaction: SET SYSTEM_VERSIONING = OFF, DELETE FROM history_table, SET SYSTEM_VERSIONING = ON */  
SET @disableVersioningScript =  @disableVersioningScript + 'ALTER TABLE [' + @temporalTableSchema + '].[' + @temporalTableName + '] SET (SYSTEM_VERSIONING = OFF)'  
SET @deleteHistoryDataScript =  @deleteHistoryDataScript + ' DELETE FROM  [' + @historyTableSchema + '].[' + @historyTableName + ']   
     WHERE ['+ @periodColumnName + '] < ' + '''' + convert(varchar(128), @cleanupOlderThanDate, 126) +  ''''   
SET @enableVersioningScript =  @enableVersioningScript + ' ALTER TABLE [' + @temporalTableSchema + '].[' + @temporalTableName + ']   
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = [' + @historyTableSchema + '].[' + @historyTableName + '], DATA_CONSISTENCY_CHECK = OFF )); '   
  
BEGIN TRAN  
    EXEC (@disableVersioningScript);  
    EXEC (@deleteHistoryDataScript);  
    EXEC (@enableVersioningScript);  
COMMIT;  
```  

## <a name="using-temporal-history-retention-policy-approach"></a>Verwenden eines Ansatzes für temporale Verlaufsbeibehaltungsrichtlinien
> **HINWEIS:** Der Ansatz mit der Richtlinie zur Beibehaltung temporaler Verlaufsdaten kann bei [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] und SQL Server 2017 ab Version CTP 1.3 verwendet werden.  

Die Beibehaltung temporaler Verlaufsdaten kann auf den einzelnen Tabellenebenen konfiguriert werden, sodass Benutzer flexible Ablaufrichtlinien erstellen können. Das Anwenden der temporalen Beibehaltung ist einfach: Sie erfordert nur einen Parameter, der bei der Tabellenerstellung oder einer Schemaänderung festgelegt werden muss.

Nachdem Sie Beibehaltungsrichtlinien festgelegt haben, überprüft Azure SQL-Datenbank in regelmäßigen Abständen, ob Zeilen mit Verlaufsdaten existieren, die für die automatische Datenbereinigung infrage kommen. Die Ermittlung übereinstimmender Zeilen und ihre Entfernung aus der Verlaufstabelle erfolgen transparent mithilfe eines vom System geplanten und ausgeführten Hintergrundtasks. Die Ablaufbedingungen für die Zeilen der Verlaufstabelle werden basierend auf der Spalte überprüft, die das Ende des SYSTEM_TIME-Zeitraums repräsentiert. Wenn die Beibehaltungsdauer beispielsweise auf sechs Monate festgelegt ist, erfüllen die für die Bereinigung infrage kommenden Zeilen folgende Bedingung:
```
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
```
Im vorherigen Beispiel sind wir davon ausgegangen, dass die Spalte „ValidTo“ dem Ende des SYSTEM_TIME-Zeitraums entspricht.
### <a name="how-to-configure-retention-policy"></a>Wie werden Beibehaltungsrichtlinien konfiguriert?
Bevor Sie die Aufbewahrungsrichtlinie für eine temporale Tabelle konfigurieren, überprüfen Sie zunächst, ob die Beibehaltung temporaler Verlaufsdaten auf Datenbankebene aktiviert ist:
```
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
```
Das Datenbankflag **Is_temporal_history_retention_enabled** ist standardmäßig auf „ON“ festgelegt, aber Benutzer können dies mit der Anweisung ALTER DATABASE ändern. Es wird ebenfalls nach einer Point-In-Time-Wiederherstellung auf OFF festgelegt. Um die Bereinigung der Beibehaltung temporaler Verlaufsdaten in Ihrer Datenbank zu aktivieren, führen Sie folgende Anweisung aus:
```
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
```
Die Beibehaltungsrichtlinien werden während der Tabellenerstellung konfiguriert, indem ein Wert für den Parameter HISTORY_RETENTION_PERIOD angegeben wird:
```
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
```
Sie können den Beibehaltungszeitraum mithilfe verschiedener Zeiteinheiten angeben: DAYS, WEEKS, MONTHS, und YEARS. Wenn HISTORY_RETENTION_PERIOD weggelassen wird, wird von einer unbegrenzten (INFINITE) Beibehaltung ausgegangen. Sie können das Schlüsselwort INFINITE auch explizit verwenden.
In manchen Szenarios sollten Sie die Beibehaltung erst nach der Tabellenerstellung konfigurieren oder den zuvor konfigurierten Wert ändern. Verwenden Sie für diesen Fall die Anweisung ALTER TABLE:
```
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
```
Zum Prüfen des aktuellen Status der Beibehaltungsrichtlinie verwenden Sie die folgende Abfrage, die das Flag für die Aktivierung der temporalen Beibehaltung auf Datenbankebene mit den Beibehaltungszeiträumen für die einzelnen Tabellen verknüpft:
```
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
```
### <a name="how-sql-database-deletes-aged-rows"></a>Wie löscht SQL-Datenbank veraltete Zeilen?
Der Bereinigungsprozess hängt vom Indexlayout der Verlaufstabelle ab. Zu beachten ist, dass eine Richtlinie für die begrenzte Beibehaltung *nur für Verlaufstabellen mit einem gruppierten Index (B-Struktur oder Columnstore) konfiguriert werden können*. Es wird ein Hintergrundtask erstellt, um die Bereinigung veralteter Daten für alle temporalen Tabellen mit begrenztem Beibehaltungszeitraum auszuführen. Die Bereinigungslogik für den gruppierten Index für Rowstore (B-Struktur) löscht die veralteten Zeilen in kleineren Blöcken (max. 10K), was die Belastung des Datenbankprotokolls und des E/A-Subsystems minimiert. Die Bereinigungslogik verwendet zwar den benötigten B-Strukturindex, jedoch kann die Löschreihenfolge der Zeilen, die den Beibehaltungszeitraum übersteigen, nicht sicher garantiert werden. *Verwenden Sie in Ihren Anwendungen daher keine Abhängigkeit von der Bereinigungsreihenfolge*.

Der Bereinigungstask für den gruppierten Columnstore entfernt ganze Zeilengruppen auf einmal (die üblicherweise jeweils 1 Mio. Reihen enthalten). Dies ist sehr effizient, vor allem wenn Verlaufsdaten mit einer hohen Geschwindigkeit generiert werden.

![Gruppierte Columnstore-Beibehaltung](../../relational-databases/tables/media/cciretention.png "gruppierte Columnstore-Beibehaltung")

Die hervorragende Datenkompression und die effiziente Beibehaltungsbereinigung machen den gruppierten Columnstore-Index zur perfekten Lösung für Szenarios, bei denen Ihre Workload in kürzester Zeit eine große Menge an Verlaufsdaten generiert. Dieses Muster ist typisch für intensive Transaktionsverarbeitungs-Workloads, die temporale Tabellen verwenden, um die Änderungsnachverfolgung und -überwachung, Trendanalysen oder die Erfassung von IoT-Daten durchzuführen.

Weitere Details finden Sie unter: [Verwalten von Verlaufsdaten in temporalen Tabellen mit Beibehaltungsrichtlinien](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-temporal-tables-retention-policy).

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Systemkonsistenzprüfungen von temporalen Tabellen](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Partitionierung mit temporären Tabellen](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Überlegungen und Einschränkungen zu temporalen Tabellen](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Sicherheit bei temporale Tabellen](../../relational-databases/tables/temporal-table-security.md)   
 [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Metadatenansichten und Funktionen für temporale Tabellen](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
