---
title: Aktualisiert - relationale Datenbanken Docs | Microsoft Docs
description: "Aktualisierter Inhalt in zuletzt geänderten Dokumentation für relationale Datenbanken Codeausschnitte anzeigen"
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
ms.date: 07/17/2017
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 71203bfa7cb4dcd06cc14ad8e49e5bc1113f8605
ms.openlocfilehash: 519fbd2bc596112dbb1c662d76e4aeeb230ffc36
ms.contentlocale: de-de
ms.lasthandoff: 07/19/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Neue und zuletzt aktualisiert: relationale Datenbanken Docs



Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates*: &nbsp; **23.5.2017** &nbsp; -bis- &nbsp; **17.7.2017**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **relationalen Datenbanken**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [SQL Server In-Memory OLTP Internals for SQL Server 2016 (Merkmale von SQL Server In-Memory-OLTP für SQL Server 2016)](in-memory-oltp/sql-server-in-memory-oltp-internals-for-sql-server-2016.md)
2. [Adaptive query processing in SQL databases (Adaptive Abfrageverarbeitung in SQL-Datenbanken)](performance/adaptive-query-processing.md)
3. [Guide to enhancing privacy and addressing GDPR requirements with the Microsoft SQL platform (Anleitung zur Verbesserung des Datenschutzes und zur Erfüllung von GDPR-Anforderung mit der SQL-Plattform von Microsoft)](security/microsoft-sql-and-the-gdpr-requirements.md)
4. [sys.pdw_replicated_table_cache_state (Transact-SQL)](system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql.md)
5. [sys.trusted_assemblies (Transact-SQL)](system-catalog-views/sys-trusted-assemblies-transact-sql.md)
6. [sys.dm_exec_query_parallel_workers (Transact-SQL)](system-dynamic-management-views/sys-dm-exec-query-parallel-workers-transact-sql.md)
7. [sys.sp_add_trusted_assembly (Transact-SQL)](system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)
8. [sys.sp_drop_trusted_assembly (Transact-SQL)](system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md)




&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact Liste von Artikeln, die vor kurzem aktualisiert

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszüge

Dieser Abschnitt zeigt die Auszüge von Updates, die vom Artikel, die vor kurzem eine große Aktualisierung aufgetreten sind.

Die hier angezeigten Auszüge werden getrennt vom richtigen semantische kontextabhängig angezeigt. Darüber hinaus wird manchmal ein Auszug vom wichtige Markdown-Syntax getrennt, die sie in den tatsächlichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Die Auszüge können nur Sie wissen, ob Ihre Interessen dauert rechtfertigen, klicken Sie auf, und besuchen den tatsächlichen Artikel.

Kopieren Sie für diese und andere Gründe Code nicht von diesen verwendet, und nehmen Sie nicht als genaue Wahrheit alle Textauszug. Besuchen Sie stattdessen den tatsächlichen Artikel aus.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-altering-memory-optimized-tablesin-memory-oltpaltering-memory-optimized-tablesmd"></a>1. &nbsp; [Ändern von speicheroptimierten Tabellen](in-memory-oltp/altering-memory-optimized-tables.md)

*Aktualisiert: 23.6.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 82.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 8359700b5db24838f1bb273526794c2865bbbe11 41d77cf0bbcf53a1b64d6524a24e5736c5a073da  (PR=2171  ,  Filename=altering-memory-optimized-tables.md  ,  Dirpath=docs\relational-databases\in-memory-oltp\  ,  MergeCommitSha40=7d2dbe0bdc4cbd05f11eacf938b35a9c35ace2e7) -->



**Protokollieren von ALTER TABLE bei speicheroptimierten Tabellen**

Bei einer speicheroptimierten Tabelle werden die meisten ALTER TABLE-Szenarios nun parallel ausgeführt und tragen zu einer Optimierung der Schreibvorgänge in das Transaktionsprotokoll bei. Zur Optimierung werden nur die Metadatenänderungen in das Transaktionsprotokoll geschrieben. Die folgenden ALTER TABLE-Vorgänge werden als Singlethread ausgeführt und sind nicht protokolloptimiert.

Die Singlethreadvorgänge schreiben in diesem Fall den gesamten Inhalt der geänderten Tabelle in das Transaktionsprotokoll. Im Folgenden finden Sie eine Liste der Singlethread-Vorgänge:

- Ändern oder Hinzufügen einer Spalte, um einen LOB-Typ (Large Object) zu verwenden: nvarchar(max), varchar(max) oder varbinary(max).

- Hinzufügen oder Löschen eines Columnstore-Indexes.

- Fast alles, das „[off-row column--../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)“ betrifft.

    - Sorgen Sie dafür, dass eine Spalte in der Zeile aus der Zeile verschoben wird.

    - Sorgen Sie dafür, dass eine Spalte außerhalb der Zeile in die Zeile verschoben wird.

    - Erstellen Sie eine neue Spalte außerhalb der Zeile.

    - *Ausnahme:* Ein Verlängern einer bereits zeilenüberragenden Spalte wird in der optimierten Weise protokolliert. 
  




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-table-and-row-size-in-memory-optimized-tablesin-memory-oltptable-and-row-size-in-memory-optimized-tablesmd"></a>2. &nbsp; [Tabellen- und Zeilengröße in speicheroptimierten Tabellen](in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)

*Aktualisiert: 22.6.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Zurück](#TitleNum_1) | [Weiter](#TitleNum_3))

<!-- Source markdown line 114.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 27ce0fa2e7bb464f9c3d6e32dd195de3b79abfcd 0a3cacd86024e2b734704ffd37e55ca0b17a0c94  (PR=2163  ,  Filename=table-and-row-size-in-memory-optimized-tables.md  ,  Dirpath=docs\relational-databases\in-memory-oltp\  ,  MergeCommitSha40=fe6de2b16b9792a5399b1c014af72a2a5ee52377) -->



 
  
 Die Berechnung von [row body size] wird in der folgenden Tabelle erläutert.  
  
 Es gibt zwei verschiedene Berechnungen für die Zeilentextgröße: die berechnete Größe und die tatsächliche Größe:  
  
-   Die berechnete Größe, bezeichnet mit [computed row body size], wird verwendet, um festzustellen, ob die Zeilengrößeneinschränkung von 8.060 Bytes überschritten wird.  
  
-   Die tatsächliche Größe, bezeichnet mit [actual row body size], ist die tatsächliche Speichergröße des Zeilentexts im Arbeitsspeicher und in den Prüfpunktdateien.  
  
 [computed row body size] und [actual row body size] werden ähnlich berechnet. Der einzige Unterschied ist die Berechnung der Größe von (n)varchar(i)- und varbinary(i)-Spalten, wie unten in der folgenden Tabelle dargestellt. Bei der berechneten Zeilentextgröße wird die deklarierte Größe *i* als Größe der Spalte verwendet, während für die tatsächliche Zeilentextgröße die tatsächliche Größe der Daten verwendet wird.  
  
 In der folgenden Tabelle wird die Berechnung der Zeilentextgröße beschrieben, die wie folgt angegeben wird: [actual row body size] = SUM([size of shallow types]) + 2 + 2 * [number of deep type columns].  
  
|Abschnitt|Größe|Kommentare|  
|-------------|----------|--------------|  
|Spalten flacher Typen|SUM([Größe flacher Typen]) Die Größe (in Bytes) der einzelnen Typen lautet wie folgt:<br /><br /> **Bit**: 1<br /><br /> **Tinyint**: 1<br /><br /> **Smallint**: 2<br /><br /> **Int**: 4<br /><br /> **Real**: 4<br /><br /> **Smalldatetime**: 4<br /><br /> **Smallmoney**: 4<br /><br /> **Bigint**: 8<br /><br /> **Datetime**: 8<br /><br /> **Datetime2**: 8<br /><br /> **Float**: 8<br /><br /> **Money**: 8<br /><br /> **Numeric** (Genauigkeit <=18): 8<br /><br /> **Time**: 8<br /><br /> **Numeric** (Genauigkeit >18): 16<br /><br /> **Uniqueidentifier**: 16||  
|Auffüllung flacher Spalten|Folgende Werte sind möglich:<br /><br /> 1, wenn Spalten tiefer Typen vorhanden sind und die gesamte Datengröße der flachen Spalten eine ungerade Zahl darstellt.<br /><br /> 0 andernfalls|Tiefe Typen sind die Typen (var)binary und (n)(var)char.|  




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-post-migration-validation-and-optimization-guidepost-migration-validation-and-optimization-guidemd"></a>3. &nbsp; [Handbuch für die Überprüfung und Optimierung nach der Migration](post-migration-validation-and-optimization-guide.md)

*Aktualisiert: 21.6.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Zurück](#TitleNum_2) | [Weiter](#TitleNum_4))

<!-- Source markdown line 27.  ms.author= "harinid".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 faa2e3dd8be3aeb475bf8c7f71617ebf17969892 f2760dfecda10baeb121929b72a4d8164e81185b  (PR=2126  ,  Filename=post-migration-validation-and-optimization-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=dcbeda6b8372b358b6497f78d6139cad91c8097c) -->



Im folgenden sind einige der häufigsten Leistungsszenarios aufgelistet, die nach der Migration zu [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)]-Plattform auftreten, und wie sie behoben werden können. Darunter sind Szenarios, die für die Migration von [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] zu [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] spezifisch sind (von einer älteren zu einer neueren Version) sowie von einer fremdem Plattform (z.B. Oracle, DB2, MySQL und Sybase) zu [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)].

**<a name="CEUpgrade"></a> Abfrageregressionen aufgrund einer Änderung in der CE-Version**


**Gilt für** die Migration von [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] zu [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)].

Wenn Sie von einer älteren Version von [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] zu [!INCLUDE[ssSQL14--../includes/sssql14-md.md)] oder neuer migrieren und [database compatibility level--../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) auf die aktuellste Version aktualisieren, kann es sein, dass eine Workload Leistung einbüßt.

Seit [!INCLUDE[ssSQL14--../includes/sssql14-md.md)] sind daher alle Änderungen des Abfrageoptimierers an den neuesten Datenbank-Kompatibilitätsgrad gebunden, sodass Pläne nicht sofort im Moment des Upgrades geändert werden, sondern erst, wenn ein Benutzer die Datenbankoption `COMPATIBILITY_LEVEL` auf die neuste aktualisiert. Diese Möglichkeit gibt Ihnen in Kombination mit dem Abfragespeicher ein großes Maß an Kontrolle über die Abfrageleistung im Upgradeprozess. 

Weitere Informationen zu Änderungen des Abfrageoptimierers, der in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] eingeführt wurde, finden Sie unter [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator (Optimieren Ihrer Abfragepläne mit der Kardinalitätsschätzung von SQL Server 2014)](http://msdn.microsoft.com/library/dn673537.aspx).




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-sysquerystoreplan-transact-sqlsystem-catalog-viewssys-query-store-plan-transact-sqlmd"></a>4. &nbsp; [sys.query_store_plan (Transact-SQL)](system-catalog-views/sys-query-store-plan-transact-sql.md)

*Aktualisiert: 5.6.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Vorherige](#TitleNum_3))

<!-- Source markdown line 58.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1b77e34309ba7033578b3c82ed83c8c2fbc93e24 ce4ade9ab906c35cb87068a1fb91c4e1d7549aac  (PR=1940  ,  Filename=sys-query-store-plan-transact-sql.md  ,  Dirpath=docs\relational-databases\system-catalog-views\  ,  MergeCommitSha40=1d363db8e8bd0e1460cdea3c3a7add68e48714c9) -->



**Einschränkungen des Erzwingens von Plänen**

Der Abfragedatenspeicher verfügt über eine Mechanismus, der den Abfrageoptimierer dazu zwingen kann, einen bestimmten Ausführungsplan zu verwenden. Es gibt allerdings Einschränkungen, die dazu führen können, dass das Erzwingen eines Plans verhindert wird. 

Erstens, wenn der Plan die folgenden Konstruktionen enthält:
* INSERT BULK-Anweisung
* INSERT BULK-Anweisung
* einen Verweis auf eine externe Tabelle
* eine verteilte Abfrage oder Volltextvorgänge
* globale Abfragen 
* Cursor
* eine ungültige Sternverknüpfungsspezifikation 

Zweitens, wenn Objekte, von denen der Plan anhängig ist, nicht mehr zur Verfügung stehen:
* eine Datenbank (wenn die Datenbank, aus der der Plan kommt, nicht mehr existiert)
* ein Index (nicht mehr vorhanden oder deaktiviert)

Und drittens, bei Problemen mit dem Plan selbst:
* Er darf nicht abgefragt werden.
* Der Abfrageoptimierer hat die Zahl an zulässigen Vorgängen überschritten.
* Die XML des Plans ist ungültig formuliert.





<a name="similars2"/>

&nbsp;

## <a name="similar-articles"></a>Ähnliche Artikel

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen, innerhalb des gleichen GitHub-Repository: [MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/).

<!--  20170717-1101  -->

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [New + Updated (4+4): **Advanced Analytics for SQL** docs (Neu + Aktualisiert (4+4): Dokumentation zu Erweiterten Analytics für SQL)](../advanced-analytics/new-updated-advanced-analytics.md)
- [New + Updated (2+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (2+0): Dokumentation zu Analysis Services für SQL)](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (1+2): **Connect to SQL** docs (Neu + Aktualisiert (1+2): Dokumentation zur Herstellung einer Verbindung mit SQL)](../connect/new-updated-connect.md)
- [New + Updated (6+0): **Database Engine for SQL** docs (Neu + Aktualisiert (6+0): Dokumentation zum Datenbankmodul für SQL)](../database-engine/new-updated-database-engine.md)
- [New + Updated (13+2): **Linux for SQL** docs (Neu + Aktualisiert (13+2): Dokumentation zu Linux für SQL)](../linux/new-updated-linux.md)
- [New + Updated (1+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (1+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (1+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (1+0): Dokumentation zu Open Database Connectivity für SQL)](../odbc/new-updated-odbc.md)
- [New + Updated (8+4): **Relational Databases for SQL** docs (Neu + Aktualisiert (8+4): Dokumentation zu relationale Datenbanken für SQL)](../relational-databases/new-updated-relational-databases.md)
- [New + Updated (2+2): **Microsoft SQL Server** docs (Neu + Aktualisiert (2+2): Dokumentation zu Microsoft SQL Server)](../sql-server/new-updated-sql-server.md)
- [New + Updated (0+1) : **SQL Server Management Studio (SSMS)** docs (Neu + Aktualisiert (0+1): Dokumentation zu SQL Server Management Studio (SSMS))](../ssms/new-updated-ssms.md)
- [New + Updated (1+0): **Transact-SQL** docs (Neu + Aktualisiert (1+0): Dokumentation zu Transact-SQL)](../t-sql/new-updated-t-sql.md)
- [New + Updated (1+0): **Tools for SQL** docs (Neu + Aktualisiert (1+0): Dokumentation zu Tools für SQL)](../tools/new-updated-tools.md)


#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Integration Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu SSIS für SQL)](../integration-services/new-updated-integration-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [New + Updated (0+0): **Reporting Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Reporting Services für SQL)](../reporting-services/new-updated-reporting-services.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../sample/new-updated-sample.md)
- [New + Updated (0+0): **SQL Server Data Tools (SSDT)** docs (Neu + Aktualisiert (0+0): Dokumentation zu SQL Server Data Tools (SSDT))](../ssdt/new-updated-ssdt.md)
- [New + Updated (0+0): **SQL Server Migration Assistant (SSMA)** docs (Neu + Aktualisiert (0+0): SQL Server Migration Assistant-Dokumente (SSMA))](../ssma/new-updated-ssma.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)


&nbsp;


