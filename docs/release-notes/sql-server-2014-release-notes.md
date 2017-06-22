---
title: SQL Server 2014 Release Notes | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-server-2014
ms.technology: server-general
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf4c4922-80b3-4be3-bf71-228247f97004
caps.latest.revision: 100
author: byham
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0ca391c25a462a5f30d6a9bc51b4541f77adfd48
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-2014-release-notes"></a>SQL Server 2014 Release Notes
In diesem Dokument mit Versionsanmerkungen werden bekannte Probleme beschrieben, mit denen Sie sich vertraut machen sollten, bevor Sie mit der Installation oder Fehlerbehebung von [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]beginnen.  
  
## <a name="top"></a>Inhalt  
[1.0 Vor der Installation](#BeforeInstall)  
  
[2.0 Produktdokumentation](#ProdDoc)  
  
[3.0 Datenbankmodul](#DBEngine)  
  
[4.0 Reporting Services](#SSRS)  
  
[5.0 SQL Server 2014 auf Microsoft Azure Virtual Machines](#AzureVM)  
  
[6.0 Analysis Services](#SSAS)  
  
[7.0 Data Quality Services](#DQS)  
  
[8.0 Upgrade Advisor](#UA)  
  
## <a name="BeforeInstall"></a>1.0 Vor der Installation  
  
### <a name="11-limitations-and-restrictions-in-sql-server-2014-rtm"></a>1.1 Einschränkungen in SQL Server 2014 RTM  
  
#### <a name="111-general-limitations-and-restrictions"></a>1.1.1 Allgemeine Einschränkungen  
  
1.  Upgrades von SQL Server 2014 CTP 1 auf SQL Server 2014 RTM werden NICHT unterstützt.  
  
2.  Die parallele Installation von SQL Server 2014 CTP 1 und SQL Server 2014 RTM wird NICHT unterstützt.  
  
3.  Das Anfügen einer SQL Server 2014 CTP 1-Datenbank an SQL Server 2014 RTM bzw. das Wiederherstellen einer solchen Datenbank in SQL Server 2014 RTM wird NICHT unterstützt.  
  
**Problemumgehung:** Keine  
  
#### <a name="12-considerations-for-upgrading-sql-server-2014-ctp-2-to-sql-server-2014-rtm-and-downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>1.2 Überlegungen zu Upgrades von SQL Server 2014 CTP 2 auf SQL Server 2014 RTM und zu Downgrades von SQL Server 2014 RTM auf SQL Server 2014 CTP 2  
  
#### <a name="121-upgrading-from-sql-server-2014-ctp-2-to-sql-server-rtm-is-fully-supported"></a>1.2.1 Upgrades von SQL Server 2014 CTP 2 auf SQL Server RTM werden vollständig unterstützt  
Sie haben insbesondere folgende Möglichkeiten:  
  
1.  Anfügen einer SQL Server 2014-CTP 2-Datenbank an eine Instanz von SQL Server 2014 RTM.  
  
2.  Wiederherstellen einer Datenbanksicherung, die unter SQL Server 2014 CTP 2 erstellt wurde, auf einer Instanz von SQL Server 2014 RTM.  
  
3.  Direktes Upgrade auf SQL Server 2014 RTM.  
  
4.  Paralleles Upgrade auf SQL Server 2014 RTM. Bevor Sie das parallele Upgrade initiieren, müssen Sie in den manuellen Failovermodus wechseln. Ausführliche Informationen finden Sie unter [Upgrade und Update von Verfügbarkeitsgruppenservern bei minimaler Downtime und minimalem Datenverlust](http://msdn.microsoft.com/library/dn178483.aspx) .  
  
5.  Daten, die durch die in SQL Server 2014 CTP 2 installierten Transaktionsleistungs-Sammlungssätze gesammelt werden, können von SQL Server Management Studio in SQL Server 2014 RTM nicht angezeigt werden und umgekehrt. Verwenden Sie SQL Server Management Studio in SQL Server 2014 CTP 2, um Daten anzuzeigen, die von dem in SQL Server 2014 CTP 2 installierten Sammlungssatz gesammelt wurden, und verwenden Sie SQL Server Management Studio in SQL Server 2014 RTM, um Daten anzuzeigen, die von dem in SQL Server 2014 RTM installierten Sammlungssatz gesammelt wurden.  
  
### <a name="122-downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>1.2.2 Downgrade von SQL Server 2014 RTM auf SQL Server 2014 CTP 2  
Dieser Vorgang wird nicht unterstützt.  
  
**Problemumgehung:** Es gibt keine Problemumgehung für das Downgrade. Es empfiehlt sich, die Datenbank vor einem Upgrade auf SQL Server 2014 RTM zu sichern.  
  
![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../release-notes/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“")[Nach oben](#top)  
  
## <a name="13-incorrect-version-of-streaminsight-client-on-sql-server-2014-mediaisocab"></a>1.3 Falsche Version von StreamInsight Client bei SQL Server 2014-Medien/ISO/CAB  
Die falsche Version von StreamInsight.msi und StreamInsightClient.msi befindet sich unter folgendem Pfad auf SQL Server-Media/ISO/CAB (StreamInsight\\\<Architecture\>\\\<Language ID\>).  
  
**Problemumgehung:** Laden Sie die richtige Version von der [SQL Server 2014 Feature Pack-Downloadseite](http://go.microsoft.com/fwlink/?LinkID=306709)herunter, und installieren Sie sie.  
  
## <a name="ProdDoc"></a>2.0 Produktdokumentation  
  
### <a name="21-report-builder-content-is-not-available-in-some-languages"></a>2.1 Inhalte zum Berichts-Generator sind nicht in allen Sprachen verfügbar  
**Problem:** In den folgenden Sprachen sind keine Informationen zum Berichts-Generator verfügbar.  
  
-   Griechisch (el-GR)  
  
-   Norwegisch (Bokmal) (nb-NO)  
  
-   Finnisch (fi-FI)  
  
-   Dänisch (da-DK)  
  
In [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]waren die Inhalte in Form einer mit dem Produkt gelieferten CHM-Datei auch in diesen Sprachen verfügbar. Da die CHM-Dateien nicht mehr im Produktlieferumfang enthalten sind, stehen Inhalte zum Berichts-Generator nur auf MSDN zur Verfügung. Diese Sprachen werden von MSDN nicht unterstützt. Der Berichts-Generator wurde auch aus TechNet entfernt und ist in diesen unterstützten Sprachen nicht mehr verfügbar.  
  
**Problemumgehung:** Keine  
  
### <a name="22-powerpivot-content-is-not-available-in-some-languages"></a>2.2 PowerPivot-Inhalte sind in manchen Sprachen nicht verfügbar  
**Problem:** In den folgenden Sprachen sind keine Informationen zu PowerPivot verfügbar.  
  
-   Griechisch (el-GR)  
  
-   Norwegisch (Bokmal) (nb-NO)  
  
-   Finnisch (fi-FI)  
  
-   Dänisch (da-DK)  
  
-   Tschechisch (cs-CZ)  
  
-   Ungarisch (hu-HU)  
  
-   Niederländisch (Niederlande) (nl-NL)  
  
-   Polnisch (pl-PL)  
  
-   Schwedisch (sv-SE)  
  
-   Türkisch (tr-TR)  
  
-   Portugiesisch (Portugal) (pt-PT)  
  
In [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]waren diese Inhalte in TechNet in diesen Sprachen verfügbar. Die Inhalte wurden aus TechNet entfernt und sind in diesen unterstützten Sprachen nicht mehr verfügbar.  
  
**Problemumgehung:** Keine  
  
![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../release-notes/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“")[Nach oben](#top)  
  
## <a name="DBEngine"></a>3.0 Datenbankmodul  
  
### <a name="31-changes-made-for-standard-edition-in-sql-server-2014-rtm"></a>3.1 Änderungen an der Standard Edition in SQL Server 2014 RTM  
SQL Server 2014 Standard weist die folgenden Änderungen auf:  
  
-   Die Pufferpoolerweiterungsfunktion unterstützt die Verwendung einer maximalen Größe, die bis zu viermal so groß wie der konfigurierte Arbeitsspeicher sein kann.  
  
-   Der maximale Arbeitsspeicher wurde von 64 GB auf 128 GB erweitert.  
  
### <a name="32-in-memory-oltp-issues"></a>3.2 Probleme bei In-Memory OLTP  
  
#### <a name="321-memory-optimization-advisor-flags-default-constraints-as-incompatible"></a>3.2.1 Der Ratgeber für die Speicheroptimierung kennzeichnet Standardeinschränkungen als inkompatibel  
**Problem:** Der Ratgeber für die Speicheroptimierung in SQL Server Management Studio kennzeichnet alle Standardeinschränkungen als inkompatibel. In einer speicheroptimierten Tabelle werden nicht alle Standardeinschränkungen unterstützt. Der Ratgeber unterscheidet nicht zwischen unterstützten und nicht unterstützten Typen von Standardeinschränkungen. Zu den unterstützten Standardeinschränkungen gehören alle Konstanten, Ausdrücke und integrierten Funktionen, die innerhalb systemintern kompilierter gespeicherter Prozeduren unterstützt werden. Die Liste der in systemintern kompilierten gespeicherten Prozeduren unterstützten Funktionen finden Sie unter [Unterstützte Konstrukte in systemintern kompilierten gespeicherten Prozeduren](http://msdn.microsoft.com/library/dn452279(v=sql.120).aspx).  
  
**Problemumgehung:** Wenn Sie den Ratgeber verwenden möchten, um Blockierungen zu identifizieren, sollten Sie die kompatiblen Standardeinschränkungen ignorieren. Um den Ratgeber für die Speicheroptimierung zum Migrieren von Tabellen zu verwenden, die über kompatible Standardeinschränkungen, aber keine anderen Blockierungen verfügen, führen Sie folgende Schritte aus:  
  
1.  Entfernen Sie die Standardeinschränkungen aus der Tabellendefinition.  
  
2.  Lassen Sie vom Ratgeber ein Migrationsskript für die Tabelle generieren.  
  
3.  Fügen Sie die Standardeinschränkungen wieder in das Migrationsskript ein.  
  
4.  Führen Sie das Migrationsskript aus.  
  
#### <a name="322-informational-message-file-access-denied-incorrectly-reported-as-an-error-in-the-sql-server-2014-error-log"></a>3.2.2 Die Informationsmeldung "Kein Zugriff auf Datei" wird im Fehlerprotokoll von SQL Server 2014 fälschlicherweise als Fehler gemeldet  
**Problem:** Beim Neustart eines Servers, der Datenbanken mit speicheroptimierten Tabellen enthält, kann im Fehlerprotokoll von SQL Server 2014 folgende Art von Fehlermeldungen angezeigt werden:  
  
```  
[ERROR]Unable to delete file C:\Program Files\Microsoft SQL   
Server\....old.dll. This error may be due to a previous failure to unload   
memory-optimized table DLLs.  
```  
  
Diese Meldung dient tatsächlich nur zu Informationszwecken und erfordert keine Benutzeraktion.  
  
**Problemumgehung:** Keine Diese Meldung dient zu Informationszwecken.  
  
#### <a name="323-missing-index-details-incorrectly-report-included-columns-for-memory-optimized-table"></a>3.2.3 In den Details zu fehlenden Indizes sind fälschlicherweise eingeschlossene Spalten für eine speicheroptimierte Tabelle angegeben  
**Problem:** Wenn in SQL Server 2014 ein fehlender Index für eine Abfrage einer speicheroptimierten Tabelle erkannt wird, wird in SHOWPLAN_XML sowie in den DMVs zu fehlenden Indizes, z. B. sys.dm_db_missing_index_details, ein fehlender Index gemeldet. In einigen Fällen enthalten die Details zu fehlenden Indizes eingeschlossene Spalten. Da alle Spalten mit allen Indizes für speicheroptimierte Tabellen implizit eingeschlossen werden, ist es nicht zulässig, eingeschlossene Spalten mit speicheroptimierten Indizes explizit anzugeben.  
  
**Problemumgehung:** Geben Sie bei Indizes für speicheroptimierte Tabellen keine INCLUDE-Klausel an.  
  
#### <a name="324-missing-index-details-omit-missing-indexes-if-a-hash-index-exists-but-is-not-suitable-for-the-query"></a>3.2.4 In den Details zu fehlendem Indizes werden fehlende Indizes ausgelassen, wenn ein Hashindex vorhanden, für die Abfrage aber nicht geeignet ist  
**Problem:** Wenn für Spalten einer speicheroptimierten Tabelle ein HASH-Index vorhanden ist, auf den in einer Abfrage verwiesen wird, der für die Abfrage jedoch nicht verwendet werden kann, wird von SQL Server 2014 in SHOWPLAN_XML und in der sys.dm_db_missing_index_details-DMV nicht immer ein fehlender Index gemeldet.  
  
Insbesondere, wenn eine Abfrage Gleichheitsprädikate enthält, die eine Teilmenge der Indexschlüsselspalten umfassen, oder wenn die Abfrage Ungleichheitsprädikate enthält, die die Indexschlüsselspalten umfassen, kann der HASH-Index in seiner ursprünglichen Form nicht verwendet werden. Um die Abfrage effizient auszuführen, wäre ein anderer Index erforderlich.  
  
**Problemumgehung:** Sofern Sie Hashindizes verwenden, sollten Sie die Abfragen und Abfragepläne daraufhin überprüfen, ob die Abfragen von Index Seek-Vorgängen für eine Teilmenge des Indexschlüssels oder für Ungleichheitsprädikate profitieren könnten. Wenn Sie eine Suche für eine Teilmenge des Indexschlüssels ausführen müssen, verwenden Sie einen NONCLUSTERED-Index. Alternativ verwenden Sie einen HASH-Index für exakt die Spalten, in denen gesucht werden soll. Wenn eine Suche für ein Ungleichheitsprädikat ausgeführt werden muss, verwenden Sie einen NONCLUSTERED-Index anstelle eines HASH-Indexes.  
  
#### <a name="325-failure-when-using-a-memory-optimized-table-and-memory-optimized-table-variable-in-the-same-query-if-the-database-option-readcommittedsnapshot-is-set-to-on"></a>3.2.5 Bei Verwendung einer speicheroptimierten Tabelle und einer speicheroptimierten Tabellenvariable in derselben Abfrage tritt ein Fehler auf, wenn die Datenbankoption READ_COMMITTED_SNAPSHOT auf ON festgelegt ist  
**Problem:** Wenn die Datenbankoption READ_COMMITTED_SNAPSHOT auf ON festgelegt ist und Sie sowohl auf eine speicheroptimierte Tabelle als auch auf eine speicheroptimierte Tabellenvariable in derselben Anweisung außerhalb des Kontexts einer Benutzertransaktion zugreifen, kann folgende Fehlermeldung ausgegeben werden:  
  
```  
Msg 41359  
A query that accesses memory optimized tables using the READ COMMITTED  
isolation level, cannot access disk based tables when the database option  
READ_COMMITTED_SNAPSHOT is set to ON. Provide a supported isolation level  
for the memory optimized table using a table hint, such as WITH (SNAPSHOT).  
```  
  
**Problemumgehung:** Verwenden Sie entweder den WITH (SNAPSHOT)-Tabellenhinweis mit der Tabellenvariablen, oder legen Sie die Datenbankoption MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT auf ON fest. Verwenden Sie dazu folgende Anweisung:  
  
```  
ALTER DATABASE CURRENT   
SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
```  
  
#### <a name="326-procedure-and-query-execution-statistics-for-natively-compiled-stored-procedures-record-worker-time-in-multiples-of-1000"></a>3.2.6 In den Prozedur- und Abfrageausführungsstatistiken für systemintern kompilierte gespeicherte Prozeduren wird worker_time in Vielfachen von 1.000 aufgezeichnet  
**Problem:** Nachdem Sie die Sammlung von Prozedur- oder Abfrageausführungsstatistiken für systemintern kompilierte gespeicherte Prozeduren unter Verwendung von sp_xtp_control_proc_exec_stats oder sp_xtp_control_query_exec_stats aktiviert haben, stellen Sie fest, dass *_worker_time in den DMVs sys.dm_exec_procedure_stats und sys.dm_exec_query_stats in Vielfachen von 1000 angegeben wird. Für Abfrageausführungen, die unter 500 Mikrosekunden liegen, wird unter worker_time der Wert 0 angegeben.  
  
**Problemumgehung:** Keine Bei Abfragen in systemintern kompilierten gespeicherten Prozeduren, die über eine kurze Ausführungsdauer verfügen, sollten Sie sich nicht auf den in den DMVs zu Ausführungsstatistiken angegebenen worker_time-Wert verlassen.  
  
#### <a name="327-error-with-showplanxml-for-natively-compiled-stored-procedures-that-contain-long-expressions"></a>3.2.7 SHOWPLAN_XML-Fehler bei systemintern kompilierten gespeicherten Prozeduren, die lange Ausdrücke enthalten  
**Problem:** Wenn eine systemintern kompilierte gespeicherte Prozedur einen langen Ausdruck enthält und Sie die SHOWPLAN_XML für die Prozedur entweder mit der T-SQL-Option SET SHOWPLAN_XML ON oder mit der Option „Geschätzten Ausführungsplan anzeigen“ in Management Studio abrufen, kann folgender Fehler auftreten:  
  
```  
Msg 41322. MAT/PIT export/import encountered a failure for memory  
optimized table or natively compiled stored procedure with object ID  
278292051 in database ID 6. The error code was  
0xc00cee81.  
```  
  
**Problemumgehung:** Es werden zwei Problemumgehungen empfohlen:  
  
1.  Fügen Sie dem Ausdruck Klammern hinzu, wie im folgenden Beispiel veranschaulicht:  
  
    Verwenden Sie anstelle von  
  
    ```  
    SELECT @v0 + @v1 + @v2 + ... + @v199  
    ```  
  
    beispielsweise  
  
    ```  
    SELECT((@v0 + ... + @v49) + (@v50 + ... + @v99)) + ((@v100 + ... + @v149) + (@v150 + ... + @v199))  
    ```  
  
2.  Erstellen Sie eine zweite Prozedur mit einem leicht vereinfachten Ausdruck. Für den Showplan sollte die allgemeine Form des Plans identisch sein. Verwenden Sie anstelle von  
  
    ```  
    SELECT @v0 +@v1 +@v2 +...+@v199  
    ```  
  
    beispielsweise  
  
    ```  
    SELECT @v0 +@v1  
    ```  
  
#### <a name="328-using-a-string-parameter-or-variable-with-datepart-and-related-functions-in-a-natively-compiled-stored-procedure-results-in-an-error"></a>3.2.8 Die Verwendung eines Zeichenfolgenparameters oder einer Variablen mit DATEPART und zugehörigen Funktionen in einer systemintern kompilierten gespeicherten Prozedur führt zu einem Fehler  
**Problem:** Wenn Sie einen Parameter oder eine Variable, der oder die einen Zeichenfolgendatentyp wie „(var)char“ oder „n(var)char“ aufweist, mit den integrierten Funktionen DATEPART, DAY, MONTH und YEAR innerhalb einer systemintern kompilierten gespeicherten Prozedur verwenden, wird eine Fehlermeldung mit dem Hinweis angezeigt, dass der Datentyp „datetimeoffset“ bei systemintern kompilierten gespeicherten Prozeduren nicht unterstützt wird.  
  
**Problemumgehung:** Weisen Sie den Zeichenfolgenparameter oder die Variable einer neuen Variablen des datetime2-Typs zu, und verwenden Sie diese Variable in der Funktion DATEPART, DAY, MONTH oder YEAR. Beispiel:  
  
```  
DECLARE @d datetime2 = @string  
DATEPART(weekday, @d)  
```  
  
#### <a name="329-native-compilation-advisor-flags-delete-from-clauses-incorrectly"></a>3.2.9 DELETE FROM-Klauseln werden vom Ratgeber für systeminterne Kompilierung falsch gekennzeichnet  
**Problem:** DELETE FROM-Klauseln innerhalb einer gespeicherten Prozedur werden vom Ratgeber für systeminterne Kompilierung fälschlicherweise als inkompatibel gekennzeichnet.  
  
**Problemumgehung:** Keine  
  
### <a name="33-register-through-ssms-adds-dac-meta-data-with-mismatched-instance-ids"></a>3.3 Bei der Registrierung über SSMS werden DAC-Metadaten mit nicht übereinstimmenden Instanz-IDs hinzugefügt  
**Problem:** Beim Registrieren oder Löschen eines Datenschichtanwendungspakets (DACPAC) über SQL Server Management Studio werden die sysdac*-Tabellen nicht ordnungsgemäß aktualisiert, um einem Benutzer das Abfragen des DACPAC-Verlaufs für die Datenbank zu ermöglichen.  Die „instance_id“ für „sysdac_history_internal“ und „sysdac_instances_internal“ stimmen nicht überein und ermöglichen keinen JOIN-Vorgang.  
  
**Problemumgehung:** Dieses Problem wird mit der Feature Pack-Umverteilung des [Data-Tier Application Framework](https://www.microsoft.com/download/details.aspx?id=42295)behoben.  Nach dem Anwenden des Updates verwenden alle neuen Verlaufseinträge den in der Tabelle „sysdac_instances_internal“ für „instance_id“ aufgelisteten Wert.  
  
Wenn das Problem mit nicht übereinstimmenden instance_id-Werten bei Ihnen bereits besteht, ist die einzige Möglichkeit zum Korrigieren der nicht übereinstimmenden Werte, als Benutzer mit Schreibberechtigungen eine Verbindung zur MSDB-Datenbank herzustellen und die instance_id-Werte so zu aktualisieren, dass sie übereinstimmen.  Wenn mehrere Registrierungs- und Deregistrierungsereignisse der gleichen Datenbank aufgetreten sind, müssen Sie möglicherweise den Datums-/Uhrzeitstempel überprüfen, um festzustellen, welche Datensätze mit den aktuellen instance_id-Werten übereinstimmen.  
  
1.  Stellen Sie in SQL Server Management Studio unter Verwendung einer Anmeldung, die über Updateberechtigungen für MSDB verfügt, eine Verbindung mit dem Server her.  
  
2.  Öffnen Sie eine neue Abfrage unter Verwendung der MSDB-Datenbank.  
  
3.  Führen Sie diese Abfrage aus, um alle Ihre aktiven DAC-Instanzen anzuzeigen.  Suchen Sie die zu berichtigende Instanz, und notieren Sie die „instance_id“:  
  
    `select * from` sysdac_instances_internal  
  
4.  Führen Sie die folgende Abfrage aus, um alle Verlaufseinträge anzuzeigen:  
  
    `select * from` sysdac_history_internal  
  
5.  Identifizieren Sie die Zeilen, die der korrigierten Instanz entsprechen sollten.  
  
6.  Aktualisieren Sie den sysdac_history_internal.instance_id-Wert auf den in Schritt 3 notierten Wert (aus der sysdac_instances_internal-Tabelle):  
  
    `update` sysdac_history_internal `set` instance_id = '\<Wert aus Schritt 3\>' `where` \<Ausdruck, der den zu aktualisierenden Zeilen entspricht\>  
  
![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../release-notes/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“")[Nach oben](#top)  
  
## <a name="SSRS"></a>4.0 Reporting Services  
  
### <a name="41-the-sql-server-2012-reporting-services-native-mode-report-server-cannot-run-side-by-side-with-sql-server-2014-reporting-services-sharepoint-components"></a>4.1 Der SQL Server 2012 Reporting Services-Berichtsserver im einheitlichen Modus kann nicht parallel mit SharePoint-Komponenten von SQL Server 2014 Reporting Services ausgeführt werden  
**Problem:** Der Windows-Dienst [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] im einheitlichen Modus „SQL Server Reporting Services“ (ReportingServicesService.exe) kann nicht gestartet werden, wenn auf demselben Server SharePoint-Komponenten von [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] installiert sind.  
  
**Problemumgehung:** Deinstallieren Sie SharePoint-Komponenten von [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , und starten Sie den Windows-Dienst "Microsoft SQL Server 2012 Reporting Services" neu.  
  
**Weitere Informationen**  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Der einheitliche Modus kann nicht parallel mit folgenden Produkten ausgeführt werden:  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Add-In für SharePoint-Produkte  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Gemeinsamer SharePoint-Dienst  
  
Die parallele Installation verhindert, dass der Windows-Dienst [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (einheitlicher Modus) gestartet wird. Im Windows-Ereignisprotokoll werden Fehlermeldungen wie die Folgenden angezeigt:  
  
```  
Log Name:   Application  
Source:          Report Server (<SQL instance ID>)  
Event ID:        117  
Task Category:   Startup/Shutdown  
Level:           Error  
Keywords:        Classic  
Description:     The report server database is an invalid version.  
  
Log Name:      Application  
Source:        Report Server (<SQL instance ID>)  
Event ID:      107  
Task Category: Management  
Level:         Error  
Keywords:      Classic  
Description:   Report Server (DENALI) cannot connect to the report server database.  
```  
  
Weitere Informationen finden Sie unter [Tipps &amp; Tricks und Problembehandlung für SQL Server 2014 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=391254).  
  
### <a name="42-required-upgrade-order-for-multi-node-sharepoint-farm-to-sql-server-2014-reporting-services"></a>4.2 Das Upgrade einer SharePoint-Farm mit mehreren Knoten auf SQL Server 2014 Reporting Services erfordert eine bestimmte Reihenfolge  
**Problem:** Das Rendern von Berichten in einer Farm mit mehreren Knoten schlägt fehl, wenn Instanzen des gemeinsamen SharePoint-Diensts für [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] vor allen Instanzen des [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Add-Ins für SharePoint-Produkte aktualisiert werden.  
  
**Problemumgehung:** In einer SharePoint-Farm mit mehreren Knoten:  
  
1.  Aktualisieren Sie zuerst alle Instanzen des [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Add-Ins für SharePoint-Produkte.  
  
2.  Aktualisieren Sie dann alle Instanzen des gemeinsamen SharePoint-Diensts für [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
Weitere Informationen finden Sie unter [Tipps, Tricks und Problembehandlung für SQL Server 2014 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=391254).  
  
![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../release-notes/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“")[Nach oben](#top)  
  
## <a name="AzureVM"></a>5.0 SQL Server 2014 RTM auf Microsoft Azure Virtual Machines  
  
### <a name="51-the-add-azure-replica-wizard-returns-an-error-when-configuring-an-availability-group-listener-in-windows-azure"></a>5.1 Der Assistent zum Hinzufügen von Azure-Replikaten gibt beim Konfigurieren eines Verfügbarkeitsgruppenlisteners in Windows Azure einen Fehler zurück  
**Problem:** Wenn eine Verfügbarkeitsgruppe über einen Listener verfügt, gibt der Assistent zum Hinzufügen von Azure-Replikaten beim Versuch, den Listener in Windows Azure zu konfigurieren, einen Fehler zurück.  
  
Das liegt daran, dass Verfügbarkeitsgruppenlistenern in jedem Subnetz, das Verfügbarkeitsgruppenreplikate hostet, eine IP-Adresse zugewiesen werden muss. Dies gilt auch für das Azure-Subnetz.  
  
**Problemumgehung:**  
  
1.  Weisen Sie dem Verfügbarkeitsgruppenlistener auf der Seite Listener eine freie statische IP-Adresse im Azure-Subnetz zu, das das Verfügbarkeitsgruppenreplikat hostet.  
  
    Auf diese Weise kann der Assistent das Replikat in Windows Azure endgültig hinzufügen.  
  
2.  Nachdem der Assistent beendet ist, müssen Sie die Konfiguration des Listeners in Windows Azure, wie in [Listener-Konfiguration für AlwaysOn-Verfügbarkeitsgruppen in Windows Azure](http://msdn.microsoft.com/library/dn376546.aspx)beschrieben, abschließen.  
  
![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../release-notes/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“")[Nach oben](#top)  
  
## <a name="SSAS"></a>6.0 Analysis Services  
  
### <a name="61-msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2010-new-farm-configured-with-sql-server-2014"></a>Für eine neue SharePoint 2010-Farm, die mit SQL Server 2014 konfiguriert ist, muss 6.1 MSOLAP. 5 heruntergeladen, installiert und registriert werden  
**Problem:**  
  
-   Bei einer SharePoint 2010-Farm, die mit einer SQL Server 2014 RTM-Bereitstellung konfiguriert ist, können PowerPivot-Arbeitsmappen keine Verbindung mit Datenmodellen herstellen, da der Anbieter, auf den in der Verbindungszeichenfolge verwiesen wird, nicht installiert ist.  
  
**Problemumgehung:**  
  
1.  Laden Sie den MSOLAP.5-Anbieter aus dem [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Pack herunter. Installieren Sie den Anbieter auf den Anwendungsservern, auf denen Excel Services ausgeführt wird. Weitere Informationen finden Sie im Abschnitt "Microsoft Analysis Services OLE DB Provider für Microsoft SQL Server 2012 SP1" im [Microsoft SQL Server 2012 SP1 Feature Pack](http://www.microsoft.com/download/details.aspx?id=35580).  
  
2.  Registrieren Sie MSOLAP.5 als vertrauenswürdigen Anbieter bei SharePoint Excel Services. Weitere Informationen finden Sie unter [Hinzufügen von MSOLAP.5 als vertrauenswürdigen Datenanbieter in Excel Services](http://technet.microsoft.com/library/hh758436.aspx).  
  
**Weitere Informationen**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] enthält MSOLAP.6. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] - und [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssGemini](../includes/ssgemini-md.md)] -Arbeitsmappen verwenden MSOLAP.5. Wenn MSOLAP.5 auf dem Computer, auf dem Excel Services ausgeführt werden, nicht installiert ist, können die Datenmodelle von Excel Services nicht geladen werden.  
  
### <a name="62-msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2013-new-farm-configured-with-sql-server-2014"></a>6.2 Für eine neue SharePoint 2013-Farm, die mit SQL Server 2014 konfiguriert ist, muss MSOLAP.5 heruntergeladen, installiert und registriert werden  
**Problem:**  
  
-   Bei einer SharePoint 2013-Farm, die mit einer [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] -Bereitstellung konfiguriert ist, können Excel-Arbeitsmappen, die auf den MSOLAP.5-Anbieter verweisen, keine Verbindung mit tabellarischen Datenmodellen herstellen, da der Anbieter, auf den in der Verbindungszeichenfolge verwiesen wird, nicht installiert ist.  
  
**Problemumgehung:**  
  
1.  Laden Sie den MSOLAP.5-Anbieter aus dem [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Pack herunter. Installieren Sie den Anbieter auf den Anwendungsservern, auf denen Excel Services ausgeführt wird. Weitere Informationen finden Sie im Abschnitt "Microsoft Analysis Services OLE DB Provider für Microsoft SQL Server 2012 SP1" im [Microsoft SQL Server 2012 SP1 Feature Pack](http://www.microsoft.com/download/details.aspx?id=35580).  
  
2.  Registrieren Sie MSOLAP.5 als vertrauenswürdigen Anbieter bei SharePoint Excel Services. Weitere Informationen finden Sie unter [Hinzufügen von MSOLAP.5 als vertrauenswürdigen Datenanbieter in Excel Services](http://technet.microsoft.com/library/hh758436.aspx).  
  
**Weitere Informationen**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] enthält MSOLAP.6. PowerPivot-Arbeitsmappen aus SQL Server 2014 verwenden jedoch MSOLAP.5. Wenn MSOLAP.5 auf dem Computer, auf dem Excel Services ausgeführt werden, nicht installiert ist, können die Datenmodelle von Excel Services nicht geladen werden.  
  
### <a name="63-corrupt-data-refresh-schedules"></a>6.3 Beschädigte Zeitpläne zur Datenaktualisierung  
**Problem:**  
  
-   Sie aktualisieren einen Aktualisierungszeitplan, und der Zeitplan wird beschädigt und unbrauchbar.  
  
**Problemumgehung:**  
  
1.  Deaktivieren Sie in Microsoft Excel die benutzerdefinierten erweiterten Eigenschaften. Weitere Informationen finden Sie im Abschnitt "Problemumgehung" des folgenden Knowledge Base-Artikels: [2927748 KB](http://support.microsoft.com/kb/2927748).  
  
**Weitere Informationen**  
  
-   Wenn Sie einen Zeitplan zur Datenaktualisierung für eine Arbeitsmappe aktualisieren und die serialisierte Länge des Aktualisierungszeitplans geringer als der ursprüngliche Zeitplan ist, wird die Puffergröße nicht ordnungsgemäß aktualisiert, und die neuen Zeitplaninformationen werden mit den alten Zeitplaninformationen zusammengeführt, wodurch der Zeitplan beschädigt wird.  
  
![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../release-notes/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“")[Nach oben](#top)  
  
## <a name="DQS"></a>7.0 Data Quality Services  
  
### <a name="71-no-cross-version-support-for-data-quality-services-in-master-data-services"></a>7.1 Data Quality Services werden in Master Data Services nicht versionsübergreifend unterstützt  
**Problem:** Die folgenden Szenarien werden nicht unterstützt:  
  
-   Master Data Services 2014, gehostet in einer Datenbank des SQL Server-Datenbankmoduls in SQL Server 2012 mit installierten Data Quality Services 2012  
  
-   Master Data Services 2012, gehostet in einer Datenbank des SQL Server-Datenbankmoduls in SQL Server 2014 mit installierten Data Quality Services 2014.  
  
**Problemumgehung:** Master Data Services, die Datenbank des Datenbankmoduls und Data Quality Services müssen dieselbe Version aufweisen.  
  
![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../release-notes/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“")[Nach oben](#top)  
  
## <a name="UA"></a>8.0 Probleme bei Upgrade Advisor  
  
### <a name="81--sql-server-2014-upgrade-advisor-reports-irrelevant-upgrade-issues-for-sql-server-reporting-services"></a>8.1 SQL Server 2014 Upgrade Advisor meldet irrelevante Upgradeprobleme für SQL Server Reporting Services  
**Problem:** Der im Lieferumfang von SQL Server 2014 enthaltene SQL Server Upgrade Advisor (SSUA) meldet bei der Analyse eines SQL Server Reporting Services-Servers fälschlicherweise mehrere Fehler.  
  
**Problemumgehung:** Dieses Problem wurde im SQL Server Upgrade Advisor, der im [SQL Server 2014 Feature Pack für SSUA](http://go.microsoft.com/fwlink/?LinkID=306709)verfügbar ist, behoben.  
  
### <a name="82--sql-server-2014-upgrade-advisor-reports-an-error-when-analyzing-sql-server-integration-services-server"></a>8.2 SQL Server 2014 Upgrade Advisor meldet bei der Analyse eines SQL Server Integration Services-Servers einen Fehler  
**Problem:** Der mit den SQL Server 2014-Medien ausgelieferte SQL Server Upgrade Advisor (SSUA) meldet einen Fehler beim Analysieren eines SQL Server Integration Services-Servers.  Fehler, der dem Benutzer angezeigt wird:  
  
```  
The installed version of Integration Services does not support Upgrade Advisor.   
The assembly information is "Microsoft.SqlServer.ManagedDTS, Version=11.0.0.0,   
Culture=neutral, PublicKeyToken=89845dcd8080cc91  
```  
  
**Problemumgehung:** Dieses Problem wurde im SQL Server Upgrade Advisor, der im [SQL Server 2014 Feature Pack für SSUA](http://go.microsoft.com/fwlink/?LinkID=306709)verfügbar ist, behoben.  
  
![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../release-notes/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“")[Nach oben](#top)  
  

