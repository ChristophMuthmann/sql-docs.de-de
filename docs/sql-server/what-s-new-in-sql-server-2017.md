---
title: Neues in SQL Server 2017 | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
caps.latest.revision: 71
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: db9f087684ae73a0a26cbb8ddedbc00a2651339c
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="whats-new-in-sql-server-2017"></a>Neues in SQL Server 2017
SQL Server 2017 stellt einen wichtigen Schritt dar, um SQL Server zu einer Plattform zu machen, auf der Sie verschiedene Wahlmöglichkeiten haben: Wählen Sie zwischen verschiedenen Entwicklungssprachen und Datentypen, zwischen lokaler Ausführung oder Ausführung in der Cloud sowie zwischen verschiedenen Betriebssystemen, indem die Leistungsfähigkeit von SQL Server für Linux, Linux-basierte Docker-Container und Windows bereitgestellt wird. Dieses Thema fasst die Neuigkeiten für bestimmte Funktionsbereiche in den neuesten Versionen von SQL Server 2017 Release Candidate (RC1, Juli 2017) und Community Technical Preview (CTP) zusammen.

**Probieren Sie es aus:** [Herunterladen von SQL Server 2017 Release Candidate (RC)](http://go.microsoft.com/fwlink/?LinkID=829477)

>**Führen Sie SQL Server unter Linux aus!** Weitere Informationen finden Sie in der [Dokumentation zu SQL Server unter Linux](https://docs.microsoft.com/sql/linux/).

## <a name="latest-release-sql-server-2017-release-candidate-rc2-august-2017"></a>Neueste Version: SQL Server 2017 Release Candidate (RC2, August 2017)
Diese Version enthält Fehlerbehebungen und Leistungsverbesserungen.

### <a name="master-data-services-mds"></a>Master Data Services (MDS)
- Wenn Sie von den folgenden vorherigen Versionen von SQL Server ein Upgrade auf SQL Server 2017 Master Data Services durchführen, können Sie jetzt von einem verbesserten Erlebnis und einer verbesserten Leistung profitieren.
    - SQL Server 2012
    - SQL Server 2014
    - SQL Server 2016

## <a name="sql-server-database-engine"></a>SQL Server-Datenbankmodul  
SQL Server-2017 umfasst viele neue Datenbankmodulfunktionen, Verbesserungen und Leistungsverbesserungen. 
- **CLR-Assemblys** können jetzt einer Positivliste hinzugefügt werden, als Problemumgehung für die in CTP 2.0 beschriebene Funktion `clr strict security`. [sp_add_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md), [sp_drop_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) und [sys.trusted_asssemblies](../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) wurden hinzugefügt, um die Positivliste von vertrauenswürdigen Assemblys zu unterstützen (RC1).  
- **Fortsetzbare Online-Indexneuerstellung** setzt den Vorgang einer Online-Indexneuerstellung dort fort, wo es nach einem Fehler aufgehört hat (z.B. einem Failover in einem Replikat oder nicht genügend Speicherplatz), oder es pausiert und der Vorgang einer Online-Indexneuerstellung wird später fortgeführt. Finden Sie unter [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) und [Richtlinien für Onlineindexvorgänge](../relational-databases/indexes/guidelines-for-online-index-operations.md). (CTP 2.0)
- Mit der Option **IDENTITY_CACHE** für ALTER DATABASE SCOPED CONFIGURATION können Sie Lücken in den Werten von Identitätsspalten vermeiden, wenn ein Server unerwartet neu startet oder ein Failover zu einem sekundären Server ausführt. Finden Sie unter [ALTER ausgelegte DATENBANKKONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). (CTP 2.0)
- Die **Automatische Datenbankoptimierung** bietet einen Einblick in die potentiellen Abfrageleistungsprobleme, empfiehlt Lösungen und kann identifizierte Probleme automatisch beheben. Weitere Informationen finden Sie unter [Automatische Optimierung](../relational-databases/automatic-tuning/automatic-tuning.md). (CTP 2.0)
- Neue **Graph-Datenbankfunktionen** für das Modellieren von m:n-Beziehungen beinhalten die Syntax [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) zum Erstellen von Knoten und Edge-Tabellen und das Schlüsselwort [MATCH](../t-sql/queries/match-sql-graph.md) für Abfragen. Weitere Informationen finden Sie unter [Graph Processing with SQL Server 2017 (Graph-Verarbeitung mit SQL Server-2017)](../relational-databases/graphs/sql-graph-overview.md). (CTP 2.0)
- Eine Option sp_configure mit dem Namen `clr strict security` ist standardmäßig aktiviert, um die Sicherheit der CLR-Assemblys zu verbessern. Weitere Informationen finden Sie unter [CLR strict security (strikte Sicherheit der CLR)](../database-engine/configure-windows/clr-strict-security.md). (CTP 2.0)
- Setup ermöglicht jetzt das Angeben der ersten tempdb-Dateigröße bis zu **256 GB** (262.144 MB) pro Datei, mit einer Warnung, wenn die Dateigröße größer als 1 GB festgelegt ist und IFI nicht aktiviert ist. (CTP 2.0)
- Die Spalte **modified_extent_page_count** in [sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md) verfolgt differenzielle Änderungen in jeder Datenbankdatei und aktiviert dabei intelligente Sicherungslösungen, die eine differenzielle Sicherung oder eine vollständige Sicherung basierend auf dem Prozentsatz der geänderten Seiten in der Datenbank ausführen. (CTP 2.0)
- Die T-SQL-Syntax [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) unterstützt jetzt das Laden einer Tabelle in eine andere Dateigruppe als die Standarddateigruppe des Benutzers mithilfe des **ON**-Schlüsselworts. (CTP 2.0)
- Nun werden datenbankübergreifende Transaktionen zwischen Datenbanken unterstützt, die Teil der **Always On-Verfügbarkeitsgruppe** sind, einschließlich Datenbanken, die Teil derselben Instanz sind. Weitere Informationen finden Sie unter [Transactions - Always On Availability Groups and Database Mirroring (Transaktionen – Always On-Verfügbarkeitsgruppen und Datenbankspiegelung)](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md) (CTP 2.0)
- Die neue Funktionalität der **Verfügbarkeitsgruppen** umfasst die Unterstützung ohne Cluster, die Einstellung der Mindestreplikate für Commitverfügbarkeitsgruppen und betreibssystemübergreifende Migrationen von Windows zu Linux und Tests. (CTP 1.3)
- Neue dynamische Verwaltungssichten:
    - [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md) macht zusammenfassende Ebenenattribute und Informationen zu den Transaktionsprotokolldateien verfügbar. Dies ist hilfreich für die Überwachung der Integrität des Transaktionsprotokolls. (CTP 2.1)
    - [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md) verfolgt die Versionsspeichernutzung pro Datenbank, was für die proaktive Planung der tempdb-Größenanpassung basierend auf der Versionspeichernutzung pro Datenbank hilfreich ist. (CTP 2.0)
    - [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) macht VLF-Informationen verfügbar, um potenzielle Transaktionsprotokollprobleme zu überwachen, davor zu warnen oder diese zu vermeiden. (CTP 2.0)
    - [sys.dm_db_stats_histogram](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) ist eine neue dynamische Verwaltungsansicht zum Untersuchen der Statistiken. (CTP 1.3)
    - **sys.dm_os_host_info** stellt Systeminformationen sowohl für Windows als auch für Linux bereit. (CTP 1.0)
- Der **Datenbankoptimierungsratgeber (DTA)** verfügt über zusätzliche Optionen und eine verbesserte Leistung. (CTP 1.2)
- **In-Memory-Erweiterungen** umfassen auch die Unterstützung für berechnete Spalten in speicheroptimierten Tabellen, die vollständige Unterstützung für JSON-Funktionen in nativ kompilierten Modulen und den CROSS APPLY-Operator in nativ kompilierten Modulen. (CTP 1.1)
- Neue **Zeichenfolgenfunktionen** sind CONCAT_WS, TRANSLATE und TRIM, und WITHIN GROUP wird jetzt für die STRING_AGG-Funktion unterstützt. (CTP 1.1)
- Es gibt neue **Massenzugriffsoptionen** (BULK INSERT und OPENROWSET(Bulk…)) für CSV und Azure-BLOB-Dateien. (CTP 1.1)
- **Speicheroptimierte Objektverbesserungen** umfassen sp_spaceused und die Löschung der acht Indexeinschränkungen für speicheroptimierte Tabellen, sp_rename für speicheroptimierte Tabellen und nativ kompilierte T-SQL-Module und CASE und TOP (N) WITH TIES für nativ kompilierte T-SQL-Module. Speicheroptimierte Dateigruppendateien können jetzt auf Azure Storage gespeichert, gesichert und wiederhergestellt werden. (CTP 1.0)
- **DATABASE SCOPED CREDENTIAL** ist eine neue Klasse der sicherungsfähigen, unterstützenden Berechtigungen CONTROL, ALTER, REFERENCES, TAKE OWNERSHIP und VIEW DEFINITION. ADMINISTER DATABASE BULK OPERATIONS ist jetzt in sys.fn_builtin_permissions sichtbar. (CTP 1.0)
- Die Datenbank **COMPATIBILITY_LEVEL 140** wurde hinzugefügt. (CTP 1.0).  

Weitere Informationen finden Sie unter [What's new in SQL Server 2017 Database Engine (Neues im Datenbankmodul von SQL Server 2017)](~/database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
- Die neue **Scale Out**-Funktion in SSIS weist die folgenden neuen und geänderten Funktionen auf. Weitere Informationen finden Sie unter [What's New in Integration Services in SQL Server 2017 (Neues in Integration Services in SQL Server 2017)](~/integration-services/what-s-new-in-integration-services-in-sql-server-2017.md). (RC1)
    -   Scale Out-Master unterstützt jetzt die hohe Verfügbarkeit.
    -   Die Failoverbehandlung der Ausführungsprotokolle aus Scale-Out-Workern wurde verbessert.
    -   Der Parameter *runincluster* der gespeicherten Prozedur **[catalog].[create_execution]** wird hinsichtlich Konsistenz und Lesbarkeit in *runinscaleout* umbenannt.
    -   Der SSIS-Katalog verfügt über eine neue globale Eigenschaft, um den Standardmodus für das Ausführen von SSIS-Paketen anzugeben.
- In der neuen Funktion **Scale Out** können Sie jetzt den Parameter **Use32BitRuntime** verwenden, wenn Sie die Ausführung auslösen. (CTP 2.1)
- Der Integration Services (SSIS) von SQL Server 2017 unterstützt jetzt auch **SQL Server unter Linux**, und mit einem neuen Paket können Sie die SSIS-Pakete auf Linux über die Befehlszeile ausführen. Weitere Informationen finden Sie unter dem [Blogpost, der die SSIS-Unterstützung für Linux ankündigt](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/). (CTP 2.1)
- Die neue Funktion **Scale Out für SSIS** macht es viel einfacher, SSIS auf mehreren Computern auszuführen. Weitere Informationen finden Sie unter [Integration Services Scale Out (Integration Services Scale Out)](~/integration-services/scale-out/integration-services-ssis-scale-out.md). (CTP 1.0)
- OData-Quelle und der OData-Verbindungs-Manager unterstützen jetzt Verbindungen mit den OData-Feeds von Microsoft Dynamics AX Online und Microsoft Dynamics CRM Online. (CTP 1.0)

Weitere Informationen finden Sie unter [What's New in Integration Services in SQL Server 2017 (Neues in Integration Services in SQL Server 2017)](~/integration-services/what-s-new-in-integration-services-in-sql-server-2017.md).

## <a name="master-data-services-mds"></a>Master Data Services (MDS)
Zusätzlich zu verbesserten Upgradeleistung und -erfahrung beim Upgrade auf SQL Server 2017 MDS wurden folgende Verbesserungen für MDS vorgenommen.
- Sie können sich jetzt die sortierte Liste von Entitäten, Sammlungen und Hierarchien auf der **Explorer-Seite** der Webanwendung anschauen.
- Die Leistung für das Bereitstellen von Millionen von Zeilen mit der entsprechenden gespeicherten Prozedur wurde verbessert.
- Die Leistung beim Erweitern den Ordners **Entitäten** auf der Seite **Gruppen verwalten** zum Zuweisen von Modellberechtigungen wurde verbessert. Die Seite **Gruppen verwalten** befindet sich im Abschnitt **Sicherheit** der Webanwendung. Weitere Informationen zu Leistungsverbesserungen finden Sie unter [https://support.microsoft.com/help/4023865?preview](https://support.microsoft.com/help/4023865?preview). Weitere Informationen zum Zuweisen von Berechtigungen finden Sie unter [Assign Model Object Permissions (Master Data Services) (Zuweisen von Modellobjektberechtigungen (Master Data Services)](../master-data-services/assign-model-object-permissions-master-data-services.md).

## <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS) 
SQL Server Analysis Services 2017 führt zahlreiche Verbesserungen für tabellarische Modelle ein. Dazu gehören:
- Tabellarischer Modus als die Standardinstallationsoption für Analysis Services. (CTP 2.0)
- Sicherheit der Objektebene zum Sichern der Metadaten von tabellarischen Modellen. (CTP 2.0)
- Datumsbeziehungen, um einfach Beziehungen basierend auf Datumsfeldern zu erstellen. (CTP 2.0)
- Neue Datenquellen **Get Data** (Power Query) und die vorhandene Unterstützung der DirectQuery-Datenquellen für M-Abfragen. (CTP 2.0) 
- DAX-Editor für SSDT. (CTP 2.0)
- Codierungshinweise, eine erweiterte Funktion für die Optimierung der Datenaktualisierung von großen tabellarischen In-Memory-Modellen. (CTP 1.3)
- Unterstützung für den **1400 Kompatibilitätsgrad** für tabellarische Modelle. Um neue Tabellenmodellprojekte zu erstellen oder vorhandene Projekte auf den Kompatibilitätsgrad 1400 zu aktualisieren, müssen Sie [SQL Server Data Tools (SSDT) 17.0 RC2](https://go.microsoft.com/fwlink?LinkId=837939) herunterladen und installieren. (CTP 1.1)
- Eine moderne **Get Data**-Erfahrung für tabellarische Modelle mit dem Kompatibilitätsgrad 1400. Weitere Informationen finden Sie unter [Analysis Services-Teamblog](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-2017-on-windows-ctp-1-1-for-analysis-services/). (CTP 1.1)
- Eigenschaft **Elemente ausblenden**, um leere Elemente in unregelmäßigen Hierarchien auszublenden. (CTP 1.1)
- Neue **Detailzeilen**-Endbenutzeraktion, um für aggregierte Informationen **Details anzeigen** zu können. Die Funktionen [SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) und **DETAILROWS** zum Erstellen von Detailzeilenausdrücken. (CTP 1.1)
- Der Operator DAX **IN** für die Angabe mehrerer Werte. (CTP 1.1)

Weitere Informationen finden Sie unter [What's new in SQL Server Analysis Services 2017 (Neues in SQL Server Analysis Services 2017)](~/analysis-services/what-s-new-in-sql-server-analysis-services-2017.md).

## <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
Ab CTP 2.1 kann SSRS nicht mehr über das SQL Server-Setup installiert werden. Wechseln Sie zum Microsoft Download Center, um den [Releasekandidat von Microsoft SQL Server 2017 Reporting Services herunterzuladen](https://www.microsoft.com/download/details.aspx?id=55252). 
- Kommentare sind jetzt für Berichte verfügbar, um Perspektive und Zusammenarbeit mit anderen Benutzern hinzuzufügen. Sie können auch die Anlagen mit Ihren Kommentar einschließen. (CTP 2.1)
- In den neuesten Versionen von Berichts-Generator und SQL Server Data Tools können Sie native DAX-Abfragen für unterstützte Tabellendatenmodelle von SQL Server Analysis Services erstellen, indem Sie die gewünschten Felder in den Abfrage-Designer ziehen und ablegen. Weitere Informationen finden Sie unter [Reporting Services-Blog](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/).

Weitere Informationen finden Sie unter [Neues in SQL Server Reporting Services (SSRS)](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).

## <a name="sql-server-machine-learning-services"></a>SQL Server-Machine Learning-Dienste
SQL Server R Services wurde umbenannt in **SQL Server-Machine Learning-Dienste**, entsprechend der Unterstützung für Python zusätzlich zur R-Programmiersprache. Sie können Machine Learning-Dienste (innerhalb einer Datenbank) zum Ausführen von R- oder Python-Skripts in SQL Server verwenden Alternativ können Sie auch **Machine Learning (eigenständig)** installieren, um R- und Python-Modelle bereitzustellen und zu nutzen, die SQL Server nicht benötigen. 

Entwickler von SQL Server haben jetzt Zugriff auf die umfangreichen ML- und AI-Bibliotheken für Python, die in der Open-Source-Umgebung zusammen mit den neuesten Innovationen von Microsoft zur Verfügung stehen: 

+ **revoscalepy**: Diese Python-Version von RevoScaleR enthält parallele Algorithmen für lineare und logistische Regressionen, Entscheidungsstrukturen, verstärkte Strukturen und zufällige Gesamtstrukturen sowie einen umfangreichen Satz an APIs für die Übertragung und Verschiebung von Daten, Remoterechenkontexte und Datenquellen.

+ **microsoftml**: Dieses moderne Paket von ML-Algorithmen und -Transformationen mit Python-Bindungen enthält tiefgreifende neuronale Netzwerke, schnelle Entscheidungsstrukturen und Entscheidungsgesamtstrukturen sowie hochgradig optimierte Algorithmen für lineare und logistische Regressionen. Darüber hinaus erhalten Sie vorgegebene, auf ResNet-Modellen basierende Modelle, die Sie zur Imageextraktion oder Standpunktanalyse verwenden können.

+ **Operationalisierung von Python mit T-SQL**: Stellen Sie Python-Code ganz leicht mithilfe der gespeicherten Prozedur `sp_execute_external_script` bereit. Profitieren Sie von hervorragender Leistung, indem Sie Daten aus SQL an Python-Prozesse streamen und MPI-Ringparallelisierung verwenden.

+ **Python in Computekontexten von SQL Server**: Datenanalysten und Entwickler können Python-Code remote aus ihrer Entwicklungsumgebung ausführen, um Daten- und Entwicklungsmodelle auszuprobieren, ohne dabei Daten zu verschieben.

Weitere Informationen finden Sie unter [What's new in SQL Server Machine Learning Services (Neues in SQL Server-Machine Learning-Services)](~/advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).

## <a name="next-steps"></a>Nächste Schritte
- Lesen Sie sich den Artikel [Versionsanmerkungen zu SQL Server 2017](sql-server-2017-release-notes.md) durch.
- Finden Sie heraus, was es [Neues in SQL Server 2017 unter Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-whats-new) gibt.
- Lesen Sie sich den Artikel [Neues in SQL Server 2016](what-s-new-in-sql-server-2016.md) durch.

