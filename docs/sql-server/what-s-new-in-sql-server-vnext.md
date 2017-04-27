---
title: Neues in SQL Server vNext | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-vnext
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
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f4a9065cccb31a8ee71e142aeba054addd6c4a5d
ms.lasthandoff: 04/11/2017

---
# <a name="what39s-new-in-sql-server-vnext"></a>Neues in SQL Server vNext
SQL Server vNext stellt einen wichtigen Schritt dar, um SQL Server zu einer Plattform zu machen, auf der Sie verschiedene Wahlmöglichkeiten haben: Wählen Sie zwischen verschiedenen Entwicklungssprachen und Datentypen, zwischen lokaler Ausführung und Ausführung in der Cloud sowie zwischen verschiedenen Betriebssystemen, indem die Leistungsfähigkeit von SQL Server für Linux, Linux-basierte Docker-Container und Windows bereitgestellt wird.

Dieses Thema gibt einen Überblick über die neuesten Funktionen der aktuellsten CTP-Version (Community Technical Preview). Ferner finden Sie hier für bestimmte Funktionsbereiche Links zu ausführlicheren Informationen über die neuen Funktionen.

![info_tip](../sql-server/media/info-tip.png) Führen Sie SQL Server unter Linux aus! Weitere Informationen finden Sie in den folgenden Themen:
-  [What's new for SQL Server vNext on Linux (Neues in SQL Server vNext unter Linux)](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-whats-new)
-  [Dokumentation zu SQL Server unter Linux](https://docs.microsoft.com/en-us/sql/linux/)


**Probieren Sie es aus:**    
   -   [![Download from Evaluation Center](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) **[Download the SQL Server vNext Community Technology Preview](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="whats-new-in-sql-server-vnext-ctp-14-march-2017"></a>Neues in SQL Server vNext CTP 1.4 (März 2017)
### <a name="sql-server-database-engine"></a>SQL Server-Datenbankmodul
- Diese CTP enthält keine neuen Funktionen des Datenbankmoduls.
- Diese CTP enthält Fehlerbehebungen für das Datenbankmodul.
- Eine ausführliche Liste der Verbesserungen von vNext CTP finden Sie unter [Neuigkeiten in SQL Server vNext (Datenbankmodul)](../database-engine/configure-windows/what-s-new-in-sql-server-vnext-database-engine.md).

### <a name="sql-server-r-services"></a>SQL Server R Services
- Diese CTP enthält keine neuen R Services-Funktionen.
- Ausführlichere Informationen zu neuen Funktionen für R Services, einschließlich Details zu früheren CTPs, finden Sie unter [Neues in SQL Server R Services](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md).  

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- Diese CTP enthält keine neuen SSRS-Funktionen.
- Ausführlichere Informationen zu Neuigkeiten in SSRS, einschließlich Details aus früheren Versionen, finden Sie unter [Neues bei Reporting Services](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md). 

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)
- Diese CTP enthält keine neuen SSAS-Funktionen.  
- Weitere Informationen zu Neuerungen in Analysis Services in der aktuellsten Vorschauversion von SSDT und SSMS finden Sie unter [Neues in SQL Server Analysis Services vNext](../analysis-services/what-s-new-in-sql-server-analysis-services-vnext.md).  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
- Diese CTP enthält keine neuen SSIS-Funktionen.
- Ausführlichere Informationen zu neuen SSIS-Funktionen, einschließlich Details aus früheren CTPs, finden Sie unter [What's New in Integration Services vNext (Neues in Integration Services vNext)](../integration-services/what-s-new-in-integration-services-in-sql-server-vnext.md).  

### <a name="master-data-services-mds"></a>Master Data Services (MDS)
- Diese CTP enthält keine neuen Master Data Services-Funktionen.

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-vnext-ctp-13-february-2017"></a>Neues in SQL Server vNext CTP 1.3 (Februar 2017)
### <a name="sql-server-database-engine"></a>SQL Server-Datenbankmodul
- Indirekte Prüfpunkte für die Leistungsverbesserung
- Verfügbarkeitsgruppen mit weniger Clusterunterstützung wurden hinzugefügt.
- Die Einstellungen des Minimum Replikat-Commits der Verfügbarkeitsgruppen wurden hinzugefügt.
- Verfügbarkeitsgruppen funktionieren jetzt auch über Windows-Linux, um OS-übergreifende Migrationen und Tests zu ermöglichen.
- Temporale Tabellen für den Support der Beibehaltungsrichtlinien wurden hinzugefügt.
- Neue DMV SYS.DM_DB_STATS_HISTOGRAM
- Onlinesupport für die Erstellung und Neuerstellung des nicht geclusterten Columnstore-Index wurde hinzugefügt.
- Fünf neue dynamische Verwaltungsansichten, um Informationen zum Linux-Prozess zurückzugeben. Weitere Informationen finden Sie unter [Linux-Prozess dynamische Verwaltungssichten](../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md).   
- [Sys.dm_db_stats_histogram (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) wird zum Untersuchen von Statistiken hinzugefügt.

### <a name="sql-server-analysis-services-ssas-ctp-13"></a>SQL Server Analysis Services (SSAS) (CTP 1.3)
- Codierungshinweise: eine erweiterte Funktion, die zur Optimierung der Verarbeitung (Datenaktualisierung) von großen tabellarischen InMemory-Modellen verwendet wird. Weitere Informationen dazu finden Sie unter [Neues in SQL Server Analysis Services vNext](../analysis-services/what-s-new-in-sql-server-analysis-services-vnext.md). 


![horizontal_bar](../sql-server/media/horizontal-bar.png)

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Kontaktaufnahme mit dem SQL Server-Entwicklungsteam 
- [Stapelüberlauf (tag sql-server)](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN-Foren](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect: Meldung von Programmfehlern und Vorschlagen von Features](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit: Allgemeine Diskussion zu R](https://www.reddit.com/r/SQLServer/)

## <a name="see-also"></a>Siehe auch    
 + [![Versionsanmerkungen](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png)] [Versionsanmerkungen zu SQL Server vNext](../sql-server/sql-server-vnext-release-notes.md). 
+ [Von den Editionen unterstützte Funktionen](https://msdn.microsoft.com/library/cc645993.aspx)
 + [Hardware- und Softwareanforderungen für die Installation](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
 + [Installations-Assistent](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
 
 + [Setup und Wartungsinstallation](http://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)
 
 ![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)



