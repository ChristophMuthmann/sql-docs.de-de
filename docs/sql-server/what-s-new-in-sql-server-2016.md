---
title: Was ist neu in SQLServer 2016
ms.custom: ''
ms.date: 07/21/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.technology:
- server-general
ms.tgt_pltfrm: ''
ms.topic: article
keywords:
- Neu SQL Server
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
caps.latest.revision: 224
author: craigg-msft
ms.author: craigg
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0c8b7cbe768aa6c443bf803f3a4fcf65f50dfeb6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="whats-new-in-sql-server-2016"></a>Was ist neu in SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]  
 Mit SQL Server 2016 können Sie intelligente, unternehmenskritische Anwendungen mithilfe einer skalierbaren, hybriden Datenbankplattform erstellen, in der bereits alles Features integriert sind – von arbeitsspeicherinterner Leistung über erweiterte Sicherheit bis hin zu datenbankinternen Analysen. Das SQL Server 2016-Release bietet neue Sicherheitsfunktionen, Abfragemöglichkeiten, Hadoop- und Cloudintegration, R-Analyse und viele weitere Verbesserungen und Erweiterungen. 

Auf dieser Seite finden Sie eine zusammenfassende Übersicht sowie Links zu detaillierten Informationen zu den Neuerungen, die SQL Server 2016 für jede SQL Server-Komponente bietet. 

![SQL Server 2016](../sql-server/media/sql-server-2016.png) 

 **Probieren Sie SQL Server noch heute aus!** 
- Laden Sie die **kostenlose** [**SQL Server 2016 Developer-Edition**](https://www.microsoft.com/en-us/cloud-platform/sql-server-editions-developers) herunter.
- Laden Sie die neueste Version von [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) herunter. 
- Sie haben ein Azure-Konto? Starten Sie einen [virtuellen Computer mit vorinstalliertem SQL Server 2016](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/).

## <a name="sql-server-2016-database-engine"></a>SQL Server 2016-Datenbankmodul
- Sie können jetzt während der Installation und Einrichtung von SQL Server **mehrere tempDB**-Datenbankdateien konfigurieren.
- Der neue **Abfragespeicher** speichert Abfragetexte, Ausführungspläne und Leistungsmetriken in der Datenbank und ermöglicht so eine einfache Leistungsüberwachung und Behebung von Leistungsproblemen. Ein Dashboard zeigt an, welche Abfragen am längsten dauern und am meisten Arbeitsspeicher- oder CPU-Ressourcen verbrauchen.
- **Temporale Tabellen** sind Verlaufstabellen, in denen alle Datenänderungen erfasst werden, einschließlich Datum und Uhrzeit.
- Die neue integrierte **JSON-Unterstützung** in SQL Server unterstützt Import-, Export-, Analyse- und Speichervorgänge in JSON.
- Das neue **PolyBase**-Abfragemodul integriert SQL Server mit externen Daten in Hadoop oder Azure Blob Storage. Sie können Daten importieren und exportieren sowie Abfragen ausführen.
- Mit dem neuen **Stretch Database**-Feature können Sie Daten aus einer lokalen SQL Server-Datenbank dynamisch und sicher in einer Azure SQL-Datenbank in der Cloud archivieren. SQL Server fragt automatisch sowohl die lokalen Daten als auch die Remotedaten in den verknüpften Datenbanken ab. 
- **In-Memory-OLTP:** 
    - Unterstützt jetzt die Einschränkungen FOREIGN KEY, UNIQUE und CHECK sowie die nativen kompilierten gespeicherte Prozeduren OR, NOT, SELECT DISTINCT, OUTER JOIN und Unterabfragen in SELECT.
    - Unterstützt Tabellen mit einer Größe von bis zu 2 TB (bisheriger Maximalwert: 256 GB). 
    - Bietet Erweiterungen des ColumnStore-Index für die Sortierung und die Unterstützung von Always On-Verfügbarkeitsgruppen.
- Neue Sicherheitsfeatures:
    - **Always Encrypted:** Wenn dieses Feature aktiviert ist, kann nur die Anwendung, die über den Verschlüsselungsschlüssel verfügt, auf die verschlüsselten sensiblen Daten in einer SQL Server 2016-Datenbank zugreifen. Der Schlüssel wird nie an SQL Server übergeben.
    - **Dynamische Datenmaskierung:** Wenn dieses Feature in der Tabellendefinition angegeben ist, werden maskierte Daten für die meisten Benutzer ausgeblendet, und nur Benutzer mit einer UNMASK-Berechtigung können alle Daten anzeigen.
    - **Sicherheit auf Zeilenebene:** Der Datenzugriff kann auf Ebene des Datenbankmoduls eingeschränkt werden, sodass Benutzer nur die Daten anzeigen können, die für sie relevant sind. 

Weitere Informationen finden Sie unter [Datenbankmodul](../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md).
## <a name="sql-server-2016-analysis-services-ssas"></a>SQL Server 2016 Analysis Services (SSAS)
SQL Server 2016 Analysis Services bietet eine verbesserte Leistung und Funktionalität für die Erstellung, Datenbankverwaltung, Filterung, Verarbeitung und viele weitere Vorgänge für Tabellenmodelldatenbanken mit **Kompatibilitätsgrad 1200**.
- **[SQL Server R Services](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md)** integrieren die für die statistische Analyse verwendete Programmiersprache R in SQL Server. 
- Der neue **Datenbankkonsistenzprüfung (Database Consistency Checker, DBCC)** wird intern ausgeführt, um potenzielle Probleme durch Datenbeschädigung zu erkennen.
- Die **direkte Abfrage**, die externe Daten live abfragt, anstatt sie vorher zu importieren, unterstützt jetzt weitere Datenquellen einschließlich Azure SQL, Oracle und Teradata. 
- Es gibt eine Vielzahl neuer **DAX-Funktionen (Data Access Expressions)**.
- Der neue Namespace **[Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)** verwaltet Instanzen und Modelle im tabellarischen Modus. 
- [Analysis Services Management Objects (AMO)](http://msdn.microsoft.com/library/mt436122.aspx) wurde überarbeitet und enthält jetzt eine zweite Assembly: **Microsoft.AnalysisServices.Core.dll**.

Weitere Informationen finden Sie unter [Analysis Services-Modul (SSAS)](../analysis-services/what-s-new-in-analysis-services.md). 

## <a name="sql-server-2016-integration-services-ssis"></a>SQL Server 2016 Integration Services (SSIS)
- Unterstützung für **Always On-Verfügbarkeitsgruppen**
- **Inkrementelle Paketbereitstellung**
- Unterstützung für **Always Encrypted**
- Neue **ssis_logreader**-Rolle auf Datenbankebene
- Neuer **benutzerdefinierter Protokolliergrad**
- **Spaltennamen für Fehler** im Datenfluss 
- Neue **Connectors**
- Unterstützung für das **Hadoop-Dateisystem (HDFS)**

Weitere Informationen finden Sie unter [Integration Services (SSIS)](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md).

## <a name="sql-server-2016-master-data-services-mds"></a>SQL Server 2016 Master Data Services (MDS)
- **Verbesserungen bei abgeleiteten Hierarchien**, einschließlich Unterstützung für rekursive und m:n-Beziehungen
- Filtern nach **domänenbasiertem Attribut**
- **Synchronisieren von Entitäten** zur gemeinsamen Nutzung von Entitäten in verschiedenen Modellen
- Genehmigungsworkflows über **Changesets**
- **Benutzerdefinierte Indizes** zur Verbesserung der Abfrageleistung
- Neue **Genehmigungslevel** für mehr Sicherheit
- Neu gestaltete **Geschäftsregelverwaltung**

Weitere Informationen finden Sie unter [Master Data Services (MDS)](../master-data-services/what-s-new-in-master-data-services-mds.md).

## <a name="sql-server-2016-reporting-services-ssrs"></a>SQL Server 2016 Reporting Services (SSRS)
Microsoft hat die Reporting Services in diesem Release sehr gründlich überarbeitet. 
- Neues **webbasiertes Berichtportal** mit KPI-Feature
- Neuer **Publisher für mobile Berichte**
- **Neu gestaltetes Modul zum Rendern von Berichten**, das HTML5 unterstützt 
- Neue **Diagrammtypen**: Treemap und Sunburst 

Weitere Informationen finden Sie unter [Reporting Services (SSRS)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).

## <a name="next-steps"></a>Nächste Schritte   
- [SQL Server-Setup](../database-engine/install-windows/installation-for-sql-server-2016.md)   
- [Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md) 
- [SQL Server 2016-Datenblatt](http://download.microsoft.com/download/C/5/3/C53C3AEF-653C-4598-8721-D522E8AC6A3A/SQL_Server_2016_Everything_Built-In_Datasheet_EN_US.pdf)
- [Von den SQL Server-Editionen unterstützte Funktionen](https://msdn.microsoft.com/library/cc645993.aspx)
- [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
- [Installieren von SQL Server 2016 über den Installations-Assistenten](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
- [Setup und Wartungsinstallation](http://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)
- [Neues SQL PowerShell-Modul](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update/)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]