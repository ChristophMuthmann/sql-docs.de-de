---
title: Was ist neu in SQLServer 2017 | Microsoft Docs
ms.custom: 
ms.date: 06/19/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: aa08b5e7de9bb317fd781a98ee5d829431b92df6
ms.openlocfilehash: 66c9bc4f2cba20076c357d27fdfacbc767a94c5c
ms.contentlocale: de-de
ms.lasthandoff: 06/23/2017

---
# <a name="what39s-new-in-sql-server-2017"></a>Was ist neu in SQLServer 2017
SQL Server-2017 stellt einen wichtigen Schritt bei, dass SQL Server eine Plattform, die Sie Ihre Auswahl Entwicklungssprachen, Datentypen, lokal und in der Cloud und Betriebssystemen erhalten, durch das Kombinieren von der Leistungsfähigkeit von SQL Server für Linux, Linux-basierte Docker-Containern und Windows dar.

In diesem Thema wird ein Überblick über die Neuigkeiten in der aktuellen Community Technical Preview (CTP) Version und Links zu detailliertere was neue Informationen für bestimmte Feature-Bereiche ist.

![info_tip](../sql-server/media/info-tip.png) Führen Sie SQL Server unter Linux aus! Weitere Informationen finden Sie in den folgenden Themen:
-  [Neuigkeiten für SQL Server-2017 unter Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-whats-new)
-  [Dokumentation zu SQL Server unter Linux](https://docs.microsoft.com/sql/linux/)


**Probieren Sie es aus:**    
   -   [![Download aus dem Evaluation Center](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) **[herunterladen den SQL Server 2017 Community Technology Preview](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="whats-new-in-sql-server-2017-ctp-21-may-2017"></a>Was ist neu in CTP für SQL Server 2017 2.1 (Mai 2017)
### <a name="sql-server-database-engine"></a>SQL Server-Datenbankmodul  
- Eine neue DMF [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md), eingeführt, um zusammenfassende Ebene Attribute und Informationen zu den Transaktionsprotokolldateien verfügbar zu machen; dies ist hilfreich für die Überwachung der Integrität des Transaktionsprotokolls ist.  
- Dieser CTP-Version enthält Fehlerbehebungen und leistungsverbesserungen für das Datenbankmodul.
- Eine ausführliche Liste der 2017 CTP-Verbesserungen in der vorherigen CTP-Versionen finden Sie unter [Neuigkeiten in SQL Server-2017 (Datenbankmodul)](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- SQL Server Reporting Services ist nicht mehr verfügbar ist, mithilfe von SQL Server Setup zum Zeitpunkt der CTP-Version 2.1 installiert.
- Kommentare sind jetzt für Berichte verfügbar. Kommentare können Sie Perspektive an, was in einem Bericht hinzufügen und die Zusammenarbeit mit anderen Personen in Ihrer Organisation. Sie können auch die Anlagen mit Ihren Kommentar einschließen.
- Ausführlichere Informationen zu Neuigkeiten in SSRS, einschließlich Details aus früheren Versionen, finden Sie unter [Neues bei Reporting Services](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md). 
- Weitere Informationen zu Power BI-Berichtsserver, finden Sie unter [erste Schritte mit Power BI-Berichtsserver](https://powerbi.microsoft.com/documentation/reportserver-get-started/).

### <a name="sql-server-machine-learning-services"></a>SQL Server-Machine Learning-Dienste
- Es sind keine neuen Machine Learning-Services-Funktionen in dieser CTP-Version.
- Ausführlichere Machine Learning Services was neue Informationen, einschließlich Details aus vorherigen CTPs finden Sie unter [Neuigkeiten in SQL Server-Machine Learning-Services](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).  

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)
- Diese CTP enthält keine neuen SSAS-Funktionen.  
- Ausführliche Informationen zu Verbesserungen und Fehlerbehebungen in dieser Version finden Sie unter [Neuigkeiten in SQL Server 2017 Analysis Services](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md).  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
-   Sie können nun die **Use32BitRuntime** Parameter.
-   Die Leistung der Protokollierung wurde verbessert.
- Ausführlichere SSIS was neue Informationen, einschließlich Details aus vorherigen CTPs finden Sie unter [Neuigkeiten in SQL Server 2017 Integration Services](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md).  

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="whats-new-in-sql-server-2017-ctp-20-april-2017"></a>Was ist neu in SQL Server 2017 CTP 2.0 (April 2017)
### <a name="sql-server-database-engine"></a>SQL Server-Datenbankmodul
- **Fortsetzbare onlineindexneuerstellung**. Fortsetzbare onlineneuerstellung von Indizes können Sie zum Fortsetzen eines Vorgangs zur onlineindexneuerstellung aus, in denen er nach einem Fehler beendet. Angenommen, ein Failover auf ein Replikat oder nicht genügend Speicherplatz Situation. Sie können auch unterbrechen und spätere Wiederaufnahme einen Vorgang zur onlineindexneuerstellung. Sie möchten z. B. vorübergehend Systemressourcen, um eine hohe Priorität Task auszuführen, oder führen Sie die indexneuerstellung in einem anderen Miniatous-Fenster aus, wenn die verfügbaren Wartungsfenster ist zu kurz für eine große Tabelle freizugeben. Schließlich benötigt fortsetzbar onlineneuerstellung von Indizes nicht signifikante Protokollspeicherplatz, der ermöglicht Ihnen, Abschneiden des Protokolls durchzuführen, während der fortsetzbar Neuerstellungsvorgang ausgeführt wird. Finden Sie unter [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) und [Richtlinien für Onlineindexvorgänge](../relational-databases/indexes/guidelines-for-online-index-operations.md).
- **IDENTITY_CACHE-Option für ALTER DATABASE SCOPED CONFIGURATION**. ALTER DATABASE SCOPED CONFIGURATION T-SQL-Anweisung wurde eine neue Option IDENTITY_CACHE hinzugefügt. Wenn diese Option auf OFF festgelegt ist, können Lücken in den Werten von Identity-Spalten vermieden werden, im Fall ein Servers wird unerwartet neu gestartet oder ein Failover zu einem sekundären Server. Finden Sie unter [ALTER ausgelegte DATENBANKKONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).  
- CLR verwendet (Code Access Security, CAS) in .NET Framework, das als Sicherheitsgrenze nicht mehr unterstützt wird. Erstellt mit einer CLR-Assembly `PERMISSION_SET = SAFE` möglicherweise Zugriff auf externe Systemressourcen, nicht verwalteten Code aufrufen und Abrufen der Sysadmin-Berechtigungen. Beginnend mit [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)], wird ein `sp_configure` Option namens `clr strict security` wurde eingeführt, um die Sicherheit der CLR-Assemblys zu verbessern. `clr strict security`ist standardmäßig aktiviert, und behandelt `SAFE` und `EXTERNAL_ACCESS` Assemblys als wäre sie gekennzeichneten `UNSAFE`. Die `clr strict security` Option kann deaktiviert werden, um Abwärtskompatibilität zu gewährleisten, aber nicht empfohlen wird. Microsoft empfiehlt, alle Assemblys mit einem Zertifikat oder asymmetrischen Schlüssel mit einem entsprechenden Anmeldenamen, die erteilt wurden signiert werden `UNSAFE ASSEMBLY` -Berechtigung in der master-Datenbank. Weitere Informationen finden Sie unter [strikte Sicherheit der CLR](../database-engine/configure-windows/clr-strict-security.md).  
- Funktionen zur Modellierung von m: n-Beziehungen im Diagramm anzeigen. Dies bietet neue [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) Syntax zum Erstellen von Knoten und Rahmentabellen und das Schlüsselwort [Übereinstimmung](../t-sql/queries/match-sql-graph.md) für Abfragen. Weitere Informationen finden Sie unter [Graph Verarbeitung mit SQL Server-2017](../relational-databases/graphs/sql-graph-overview.md).   
- Automatische Optimierung ist ein datenbankfeature, das einen Einblick in die Abfrage potenzielle Leistungsprobleme bereitstellt, kann diese Lösungen empfohlen und automatisch beheben Probleme identifiziert. Automatische Optimierung [!INCLUDE[ssnoversion](../includes/ssnoversion.md)], Sie werden benachrichtigt, sobald ein mögliches Leistungsproblem erkannt wird, und ermöglicht das Anwenden von korrekturmaßnahmen oder ermöglicht die [!INCLUDE[ssde](../includes/ssde-md.md)] automatisch zu beheben von Leistungsproblemen. Weitere Informationen finden Sie unter [Automatische Optimierung](../relational-databases/automatic-tuning/automatic-tuning.md).  
-   Batch-Modus Adaptive Beitreten zur Verbesserung der Qualität des Abfrageplans (unter 140 Db-Kompatibilität).
-   Verschachtelte Ausführung für T-SQL-Tabellenwertfunktionen mit mehreren Anweisungen zur Verbesserung der Qualität des Abfrageplans (unter 140 Db-Kompatibilität).
- Der Abfragespeicher überwacht jetzt außerdem Wait Stats zusammenfassende Informationen. Nachverfolgen von Statistiken wartevorgangskategorien pro Abfrage im Abfragespeicher ermöglicht das Potenzial der Leistung, Problembehandlung, sogar noch stärker einen Einblick in die Arbeitsleistung zu und seine Engpässe Beibehaltung der Abfragespeicher bietet folgende Vorteile bietet.
- DTC-Unterstützung für AlwaysOn-Verfügbarkeitsgruppen für alle datenbankübergreifende Transaktionen zwischen Datenbanken, die Teil der verfügbarkeitsgruppe, einschließlich für Datenbanken, die Teil derselben Instanz sind. Weitere Informationen finden Sie unter [Transaktionen - AlwaysOn-Verfügbarkeitsgruppen und Datenbankspiegelung](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)
- Eine neue Spalte **Modified_extent_page_count** wird in eingeführt [dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md) zum Nachverfolgen von differenzielle Änderungen in jeder einzelnen Datenbankdatei an der Datenbank.
- [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) unterstützt jetzt das Laden einer Tabellenstatus in einer anderen Dateigruppe als eine Standarddateigruppe, der den Benutzer mithilfe der **ON** Schlüsselwort.
- SQL Server-Setup unterstützt bis zu angeben der anfänglichen Tempdb-Dateigröße **256 GB (262.144 MB)** pro Datei mit einer Warnung, wenn die Dateigröße auf Wert größer als festgelegt ist **1 GB** und IFI nicht aktiviert ist.
- Eine neue dynamische Ansicht (DMV) [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md) wurde eingeführt, um die Verwendung von Version Store pro Datenbank überwachen.
- Eine neue DMV [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) wurde eingeführt, um die DBCC LOGINFO ähnelt VLF-Informationen verfügbar machen.
- Temporale Tabellen mit systemversionsverwaltung unterstützen jetzt CASCADE DELETE- und UPDATE CASCADE.
- Diese CTP enthält Fehlerbehebungen für das Datenbankmodul.
- Eine ausführliche Liste der 2017 CTP-Verbesserungen in der vorherigen CTP-Versionen finden Sie unter [Neuigkeiten in SQL Server-2017 (Datenbankmodul)](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).   

### <a name="sql-server-machine-learning-services"></a>SQL Server-Machine Learning-Dienste
- SQL Server R Services hat einen neuen Namen ein, um Unterstützung für die Sprache Python in CTP 2.0 widerzuspiegeln. SQL Server Machine Learning-Services (Datenbankintern) können jetzt ein R oder Python-Skripts in SQL Server ausgeführt wird. Oder installieren Sie Microsoft Machine Learning-Server (eigenständig) zum Bereitstellen und Nutzen von R und Python-Modelle, die keine SQL Server erfordern. 
- Beide Plattformen gehören neue MicrosoftML Algorithmen für verteilte maschinelles lernen und die neueste Version von Microsoft R (Version 9.1.0).
- Weitere Informationen finden Sie unter [Neuigkeiten für Machine Learning](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-2017-ctp-14-march-2017"></a>Neuigkeiten in SQL Server 2017 CTP 1.4 (März 2017)
### <a name="sql-server-database-engine"></a>SQL Server-Datenbankmodul
- Diese CTP enthält keine neuen Funktionen des Datenbankmoduls.
- Diese CTP enthält Fehlerbehebungen für das Datenbankmodul.
- Eine ausführliche Liste der 2017 CTP-Verbesserungen in der vorherigen CTP-Versionen finden Sie unter [Neuigkeiten in SQL Server-2017 (Datenbankmodul)](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).

### <a name="sql-server-r-services"></a>SQL Server R Services
- Diese CTP enthält keine neuen R Services-Funktionen.
- Ausführlichere Informationen zu neuen Funktionen für R Services, einschließlich Details zu früheren CTPs, finden Sie unter [Neues in SQL Server R Services](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md).  

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- Diese CTP enthält keine neuen SSRS-Funktionen.
- Ausführlichere Informationen zu Neuigkeiten in SSRS, einschließlich Details aus früheren Versionen, finden Sie unter [Neues bei Reporting Services](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md). 

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)
- Diese CTP enthält keine neuen SSAS-Funktionen.  
- Weitere Details, einschließlich für Analysis Services in der neuesten Preview-Versionen von SSDT und SSMS Neuigkeiten finden Sie unter [Neuigkeiten in Analysis Services 2017](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md).  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
- Diese CTP enthält keine neuen SSIS-Funktionen.
- Ausführlichere SSIS was neue Informationen, einschließlich Details aus vorherigen CTPs finden Sie unter [Neuigkeiten in Integration Services 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md).  

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-2017-ctp-13-february-2017"></a>Neues in CTP für SQL Server 2017 1.3 (Version von Februar 2017)
### <a name="sql-server-database-engine"></a>SQL Server-Datenbankmodul
- Indirekte Prüfpunkte für die Leistungsverbesserung
- Verfügbarkeitsgruppen mit weniger Clusterunterstützung wurden hinzugefügt.
- Die Einstellungen des Minimum Replikat-Commits der Verfügbarkeitsgruppen wurden hinzugefügt.
- Verfügbarkeitsgruppen funktionieren jetzt auch über Windows-Linux, um OS-übergreifende Migrationen und Tests zu ermöglichen.
- Temporale Tabellen Aufbewahrungsrichtlinie für die Unterstützung hinzugefügt. Weitere Informationen finden Sie unter [verwalten Beibehaltung von Verlaufsdaten in Temporalen Tabellen mit Systemversionsverwaltung](../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md#using-temporal-history-retention-policy-approach).
- Neue DMV SYS.DM_DB_STATS_HISTOGRAM
- Online nicht gruppierten Columnstore-index erstellen und Neuerstellen verfügen über zusätzliche Unterstützung
- Fünf neue dynamische Verwaltungsansichten, um Informationen zum Linux-Prozess zurückzugeben. Weitere Informationen finden Sie unter [Linux-Prozess dynamische Verwaltungssichten](../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md).   
- [Sys.dm_db_stats_histogram (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) wird zum Untersuchen von Statistiken hinzugefügt.

### <a name="sql-server-analysis-services-ssas-ctp-13"></a>SQL Server Analysis Services (SSAS) (CTP 1.3)
- Codierungshinweise: eine erweiterte Funktion, die zur Optimierung der Verarbeitung (Datenaktualisierung) von großen tabellarischen InMemory-Modellen verwendet wird. Weitere Informationen finden Sie unter [Neuigkeiten in Analysis Services 2017](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md). 


![horizontal_bar](../sql-server/media/horizontal-bar.png)

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Kontaktaufnahme mit dem SQL Server-Entwicklungsteam 
- [Stapelüberlauf (tag sql-server)](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN-Foren](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect: Meldung von Programmfehlern und Vorschlagen von Features](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit: Allgemeine Diskussion zu R](https://www.reddit.com/r/SQLServer/)

## <a name="see-also"></a>Siehe auch    
- ![Anmerkungen zu dieser Version](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) [Versionsanmerkungen zu SQL Server 2017](../sql-server/sql-server-2017-release-notes.md). 
- [Von den Editionen unterstützte Funktionen](https://msdn.microsoft.com/library/cc645993.aspx)
- [Hardware- und Softwareanforderungen für die Installation](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
- [SQL Server-Installations-Assistent](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
- [Installieren von SQLServer-Wartungsupdates](http://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)
 
 ![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)

