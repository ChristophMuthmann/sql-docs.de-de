---
title: "Aktualisiert – Dokumentation zu relationalen Datenbanken | Microsoft-Dokumentation"
description: "Zeigen Sie Codeausschnitte von aktualisierten Inhalten in der zuletzt geänderten Dokumentation zu relationale Datenbanken an."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.openlocfilehash: 1fbc7affa833eb34b6e13e28b229d47ac0b05a5c
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Neu und zuletzt aktualisiert: Dokumentation zu relationalen Datenbanken



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates*: &nbsp; **28.09.2017** &nbsp; – bis – &nbsp; **02.12.2017**
- *Themenbereich:* &nbsp; **Relationale Datenbanken**




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Verwenden des SSMS XEvent Profilers](extended-events/use-the-ssms-xe-profiler.md)
2. [Import Flat File to SQL Wizard (Assistent zum Importieren von Flatfiles in SQL)](import-export/import-flat-file-wizard.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [tempdb-Datenbank](#TitleNum_1)
2. [Handbuch zur Architektur der Speicherverwaltung](#TitleNum_2)
3. [Statistik](#TitleNum_3)
4. [sp_server_diagnostics (Transact-SQL)](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-tempdb-databasedatabasestempdb-databasemd"></a>1. &nbsp; [tempdb-Datenbank](databases/tempdb-database.md)

*Aktualisiert: 20.11.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 121.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5c8bb5f9c40625aaf955295e5b5d03e4257e6c6b 337555ea28f4c3fdd6b78f1bfb4d62607a6bf92d  (PR=4039  ,  Filename=tempdb-database.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=ef1fa818beea435f58986af3379853dc28f5efd8) -->



**Optimieren der Leistung von tempdb**

 Die Größe und die physische Platzierung der tempdb-Datenbank können sich auf die Leistung eines Systems auswirken. Wurde für tempdb beispielsweise eine zu kleine Größe definiert, muss bei jedem Neustart der ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)]-Instanz möglicherweise ein Teil der Verarbeitungslast des Systems dafür aufgewendet werden, die tempdb-Datenbank automatisch auf den Umfang zu vergrößern, der zum Unterstützen der anfallenden Arbeitsauslastung erforderlich ist.

 Verwenden Sie möglichst [database instant file initialization--../../relational-databases/databases/database-instant-file-initialization.md), um die Leistung der Vorgänge zur Datendateivergrößerung zu verbessern.

 Weisen Sie allen tempdb-Dateien im Voraus Speicherplatz zu, indem Sie die Dateigröße auf einen Wert festlegen, der hoch genug ist, um der typischen Arbeitsauslastung in der Umgebung gerecht zu werden. Dadurch verhindern Sie, dass die tempdb-Datenbank zu häufig vergrößert wird, was zu Leistungseinbußen führen kann. Für die tempdb-Datenbank sollte die automatische Vergrößerung festgelegt werden, jedoch nur für den Fall eines zusätzlichen Speicherplatzbedarfs für nicht geplante Ausnahmen.

 Datendateien sollten in jeder [filegroup--../../relational-databases/databases/database-files-and-filegroups.md#filegroups) die gleiche Größe haben, weil in ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] ein Algorithmus mit proportionalem Füllen verwendet wird, in dem Zuteilungen in Dateien mit mehr Platz bevorzugt werden. Ein Aufteilen von tempdb in mehrere Datendateien gleicher Größe bietet einen hohen Grad an paralleler Effizienz in Vorgängen, in denen tempdb verwendet wird.

 Legen Sie das Inkrement für die Dateivergrößerung auf eine sinnvolle Größe fest, sodass der Zuwachs der tempdb-Datenbank nicht zu gering ausfällt. Wenn der Dateizuwachs im Vergleich zur Anzahl der Daten, die in die tempdb-Datenbank geschrieben werden, zu gering ist, muss tempdb möglicherweise ständig vergrößert werden. Dies beeinträchtigt die Leistung.

 Um die aktuelle Größe von tempdb und die aktuellen Größenzuwachsparameter zu überprüfen, führen Sie die folgende Abfrage aus:
```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeinMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-memory-management-architecture-guidememory-management-architecture-guidemd"></a>2. &nbsp; [Handbuch zur Architektur der Speicherverwaltung](memory-management-architecture-guide.md)

*Aktualisiert: 28.11.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Zurück](#TitleNum_1) | [Weiter](#TitleNum_3))

<!-- Source markdown line 75.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 dd47431ca47eab16af40e41adaeeaf3fc5fb7461 445f013af3bdad65dd3eaf837db7f744b43e8f97  (PR=4113  ,  Filename=memory-management-architecture-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=28cccac53767db70763e5e705b8cc59a83c77317) -->



In früheren Versionen von SQL Server (..!NCLUDE-NotShown--ssVersion2005--../includes/ssversion2005-md.md)], ..!NCLUDE-NotShown--ssKatmai--../includes/ssKatmai-md.md)] und ..!NCLUDE-NotShown--ssKilimanjaro--../includes/ssKilimanjaro-md.md)]) gibt es fünf unterschiedliche Mechanismen zur Speicherbelegung:
-  **Einzelseitenbelegung (Single-page Allocator, SPA)**, die im ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)]-Prozess nur Speicherbelegungen umfasst, die kleiner als oder gleich 8 KB sind. Die Konfigurationsoptionen *Max. Serverarbeitsspeicher (MB)* und *Min. Serverarbeitsspeicher (MB)* bestimmten die Grenzen des vom SPA verbrauchten physischen Arbeitsspeichers. Der Pufferpool bildete zugleich den Mechanismus für SPA und den größten Verbraucher für Einzelseitenbelegungen.
-  **Mehrseitenbelegung (Multi-Page Allocator, MPA)**, für Speicherbelegungen, die mehr als 8 KB erfordern.
-  **CLR-Belegung**, einschließlich des SQL CLR-Heaps und dessen globaler Belegungen, die während der CLR-Initialisierung erstellt werden.
-  Speicherbelegungen für **[thread stacks--../relational-databases/memory-management-architecture-guide.md#stacksizes)** im ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)]-Prozess.
-  **Direkte Windows-Belegungen (Direct Windows allocations, DWA)** für Speicherbelegungsanforderungen, die direkt an Windows gerichtet sind. Dazu gehören die Windows-Heapnutzung und direkte virtuelle Belegungen von Modulen, die in den ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)]-Prozess geladen werden. Beispiele für solche Speicherbelegungsanforderungen beinhalten Belegungen von DLLs erweiterter gespeicherter Prozeduren, Objekte, die mithilfe von Automatisierungsprozeduren (sp_OA-Aufrufen) erstellt werden, und Belegungen von verknüpften Serveranbietern.

Seit ..!NCLUDE-NotShown--ssSQL11--../includes/sssql11-md.md)] sind alle Einzelseitenbelegungen, Mehrseitenbelegungen und CLR-Belegungen in einer **Seitenbelegung beliebiger Größe** konsolidiert, die in den Speichergrenzwerten enthalten ist, die durch die Konfigurationsoptionen *Max. Serverarbeitsspeicher (MB)* und *Min. Serverarbeitsspeicher (MB)* gesteuert werden. Diese Änderung ermöglichte eine genauere Dimensionierung für alle Arbeitsspeicheranforderungen, die vom ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)]-Speicher-Manager verarbeitet werden.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-statisticsstatisticsstatisticsmd"></a>3. &nbsp; [Statistik](statistics/statistics.md)

*Aktualisiert: 27.11.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Zurück](#TitleNum_2) | [Weiter](#TitleNum_4))

<!-- Source markdown line 48.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1dbe3bd6fdfcd27cf4a597cac5a4a09821b51ba7 971cfccf75fbc8842a0ef020a2bc93992c5f4ad9  (PR=4087  ,  Filename=statistics.md  ,  Dirpath=docs\relational-databases\statistics\  ,  MergeCommitSha40=9fbe5403e902eb996bab0b1285cdade281c1cb16) -->



> [!NOTE]
> Histogramme in ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] werden nur für eine einzelne Spalte oder die erste Spalte aus der Gruppe der Schlüsselspalten des Statistik-Objekts erstellt.

Zum Erstellen des Histogramms sortiert der Abfrageoptimierer die Spaltenwerte, berechnet die Anzahl der Werte, die den einzelnen unterschiedlichen Spaltenwerten entsprechen, und aggregiert die Spaltenwerte dann in maximal 200 zusammenhängenden Histogrammschritten. Jeder Histogrammschritt umfasst einen Bereich von Spaltenwerten gefolgt von einem oberen Spaltengrenzwert. Der Bereich enthält alle möglichen Spaltenwerte zwischen den Begrenzungswerten, ohne die Begrenzungswerte selbst. Der niedrigste der sortierten Spaltenwerte ist der obere Grenzwert für den ersten Histogrammschritt.

Ausführlicher formuliert heißt das, ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] erstellt das **Histogramm** aus den sortierten Spaltenwerten in drei Schritten:

- **Initialisierung des Histogramms:** Im ersten Schritt wird eine Wertesequenz verarbeitet, die am Anfang der sortierten Menge beginnt, und bis zu 200 Werte von *range_high_key*, *equal_rows*, *range_rows*, und *distinct_range_rows* werden erfasst (*range_rows* und *distinct_range_rows* sind während dieses Schritts immer 0). Der erste Schritt ist abgeschlossen, wenn alle Eingaben erschöpft sind oder 200 Werte gefunden wurden.
- **Scannen mit Bucketzusammenführung:** Jeder zusätzliche Wert aus der führenden Spalte des Statistikschlüssels wird im zweiten Schritt in sortierter Reihenfolge verarbeitet. Jeder nachfolgende Wert wird entweder zum letzten Bereich hinzugefügt, oder es wird am Ende ein neuer Bereich erstellt (dies ist möglich, da die Eingabewerte sortiert sind). Wenn ein neuer Bereich erstellt wird, wird ein Paar der vorhandenen benachbarten Bereiche zu einem einzelnen Bereich reduziert. Dieses Bereichspaar wird ausgewählt, um den Verlust von Informationen zu minimieren. Diese Methode verwendet einen Algorithmus für die *maximale Differenz*, um die Anzahl von Schritten im Histogramm zu minimieren und gleichzeitig die Differenz zwischen den Begrenzungswerten zu maximieren. Die Anzahl von Schritten nach dem Reduzieren von Bereichen bleibt in diesem Schritt bei 200.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-spserverdiagnostics-transact-sqlsystem-stored-proceduressp-server-diagnostics-transact-sqlmd"></a>4. &nbsp; [sp_server_diagnostics (Transact-SQL)](system-stored-procedures/sp-server-diagnostics-transact-sql.md)

*Aktualisiert: 21.11.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Zurück](#TitleNum_3))

<!-- Source markdown line 157.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d0d97efbb0b16638d0120af9ac5e66ec3bcfa391 b98735ec26a091f8c8c58ca1790243be7942e038  (PR=4052  ,  Filename=sp-server-diagnostics-transact-sql.md  ,  Dirpath=docs\relational-databases\system-stored-procedures\  ,  MergeCommitSha40=45e4efb7aa828578fe9eb7743a1a3526da719555) -->



Die nachstehende Beispielabfrage liest die Zusammenfassungsausgabe aus der Tabelle:
```sql
SELECT create_time,
       component_name,
       state_desc
FROM SpServerDiagnosticsResult;
```

Die nachstehende Beispielabfrage liest einige Bestandteile der ausführlichen Ausgabe aus jeder Komponente in der Tabelle:
```sql
-- system
select data.value('(/system/@systemCpuUtilization)[1]','bigint') as 'System_CPU',
   data.value('(/system/@sqlCpuUtilization)[1]','bigint') as 'SQL_CPU',
   data.value('(/system/@nonYieldingTasksReported)[1]','bigint') as 'NonYielding_Tasks',
   data.value('(/system/@pageFaults)[1]','bigint') as 'Page_Faults',
   data.value('(/system/@latchWarnings)[1]','bigint') as 'Latch_Warnings',
   data.value('(/system/@BadPagesDetected)[1]','bigint') as 'BadPages_Detected',
   data.value('(/system/@BadPagesFixed)[1]','bigint') as 'BadPages_Fixed'
from SpServerDiagnosticsResult
where component_name like 'system'
go

-- Resource Monitor
select data.value('(./Record/ResourceMonitor/Notification)[1]', 'VARCHAR(max)') AS [Notification],
    data.value('(/resource/memoryReport/entry[@description=''Working Set'']/@value)[1]', 'bigint')/1024 AS [SQL_Mem_in_use_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Paging File'']/@value)[1]', 'bigint')/1024 AS [Avail_Pagefile_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Physical Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_Physical_Mem_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Virtual Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_VAS_MB],
    data.value('(/resource/@lastNotification)[1]','varchar(100)') as 'LastNotification',
    data.value('(/resource/@outOfMemoryExceptions)[1]','bigint') as 'OOM_Exceptions'
from SpServerDiagnosticsResult
where component_name like 'resource'
go

-- Nonpreemptive waits
```







## <a name="similar-articles"></a>Ähnliche Artikel

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [Neu + Aktualisiert (3+14): Dokumente zu **Advanced Analytics für SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [New + Updated (1+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (1+0): Analysis Services für SQL-Dokumente)](../analysis-services/new-updated-analysis-services.md)
- [Neu + Aktualisiert (87+0): Dokumente zu **Analyseplattformsystem für SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neu + Aktualisiert (5+4): Dokumente zu **Herstellen einer Verbindung mit SQL**](../connect/new-updated-connect.md)
- [Neu + Aktualisiert (0+1): Dokumente zum **Datenbankmodul für SQL**](../database-engine/new-updated-database-engine.md)
- [Neu + Aktualisiert (2+2):Dokumente zu **Integration Services für SQL**](../integration-services/new-updated-integration-services.md)
- [Neu + Aktualisiert (10+9): Dokumente zu **Linux für SQL**](../linux/new-updated-linux.md)
- [Neu + Aktualisiert (2+4): Dokumente zu **Relationale Datenbanken für SQL**](../relational-databases/new-updated-relational-databases.md)
- [Neu + Aktualisiert (4+2): Dokumente zu **Reporting Services für SQL**](../reporting-services/new-updated-reporting-services.md)
- [Neu + Aktualisiert (0+1): Dokumente zu **Beispiele für SQL**](../sample/new-updated-sample.md)
- [Neu + Aktualisiert (21+0): Dokumente zu **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neu + Aktualisiert (5+1): Dokumente zu **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [New + Updated (0+1): **SQL Server Data Tools (SSDT)** docs (Neu + Aktualisiert (0+1): SQL Server Data Tools-Dokumente (SSDT))](../ssdt/new-updated-ssdt.md)
- [Neu + Aktualisiert (1+0): Dokumente zu **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [New + Updated (0+1): **SQL Server Management Studio (SSMS)** docs (Neu + Aktualisiert (0+1): SQL Server Management Studio-Dokumente (SSMS))](../ssms/new-updated-ssms.md)
- [Neu + Aktualisiert (0+2): Dokumente zu **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [Neu + Aktualisiert (0+0): Dokumente zu **Data Migration Assistant (DMA) für SQL**](../dma/new-updated-dma.md)
- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [Neu + Aktualisiert (0+0): Dokumentation zu **Tools für SQL**](../tools/new-updated-tools.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)


