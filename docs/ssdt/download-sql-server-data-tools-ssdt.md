---
title: Herunterladen von SQL Server Data Tools (SSDT) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- SSDT installieren, SSDT herunterladen, aktuelle SSDT-Version
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 681ad2f6d7aeb88db45dde3f2e695db672b97dbd
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="download-sql-server-data-tools-ssdt"></a>Herunterladen von SQL Server Data Tools (SSDT)

**[SQL Server Datatools](https://msdn.microsoft.com/mt186501)** ist ein modernes und kostenlos herunterladbares Entwicklungstool für relationale SQL Server-Datenbanken, Azure SQL-Datenbanken, Integration Services-Pakete, Analysis Services-Datenmodelle und Reporting Services-Berichte. Mit SSDT lassen sich Datenbanken und andere Inhaltstypen für SQL Server entwerfen und bereitstellen – und zwar ebenso einfach wie eine Anwendung in Visual Studio. Diese Version unterstützt SQL Server 2005 bis SQL Server 2016 und bietet die Entwurfsumgebung zum Hinzufügen von neuen Features, die in SQL Server 2016 angeboten werden.  
    
    
| ![Download verfügbar ist](../ssdt/media/download.png) Herunterladen von SQL Server Data Tools für Visual Studio 2015  | Data-Tier Application Framework (DacFx) herunterladen ||
|:---|:---|:---|
|**[Laden Sie SQL Server Data Tools (16.5) herunter](https://msdn.microsoft.com/mt186501)**|[**Laden Sie DacFx und SqlPackage.exe (16.5) herunter**](https://www.microsoft.com/download/details.aspx?id=54106) |Aktuelles, allgemein verfügbares Release für den Einsatz in der Produktion.|
|[**Laden Sie SQL Server Data Tools (SSDT) – Release Candidate herunter**](../ssdt/sql-server-data-tools-ssdt-release-candidate.md)| [**Laden Sie DacFx und SqlPackage.exe – Release Candidate herunter**](../ssdt/sql-server-data-tools-ssdt-release-candidate.md) |Enthält Support für SQL Server vNext.|



## <a name="download-visual-studio"></a>Herunterladen von Visual Studio

* [**Laden Sie Visual Studio Community 2015 herunter**](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)

### <a name="use-ssdt-in-visual-studio-2017"></a>Verwenden von SSDT in Visual Studio 2017

* [**Visual Studio 2017 herunterladen** ](https://www.visualstudio.com/) ([Visual Studio 2017-Features nach Edition vergleichen](https://www.visualstudio.com/vs/compare/))

Um relationale Datenbankprojekte zu verwenden, empfehlen wir die Überprüfung der Arbeitsauslastung von **Datenspeicherung und Verarbeitung** während der Installation. Unterstützung für SSDT-Datenbankprojekte ist auch in einigen anderen Arbeitsauslastungen enthalten, darunter *Azure*, *ASP.Net and Web Development* und *.Net Core Cross Platform Development*.

Installieren Sie, wenn Sie SSDT mit Visual Studio 2017 verwenden, die AS- und RS-Komponenten:
* [Analysis Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)
* [Reporting Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)


## <a name="installing-ssdt-without-visual-studio-pre-installed"></a>Installieren von SSDT ohne vorinstalliertes Visual Studio

Wenn Visual Studio auf Ihrem Computer noch nicht installiert ist, wird mit der Installation von SSDT für Visual Studio 2015 auch eine reduzierte „integrierte Shell“-Version von Visual Studio 2015 installiert. Diese Version von Visual Studio kann kostenlos installiert und auf so vielen Computern wie gewünscht verwendet werden. Dadurch erhalten Sie alle Projekttypen von SQL Server sowie den Objektexplorer von SQL Server und weitere SQL-Tools.

Wenn [Visual Studio 2015 Community Edition (oder höher)](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) auf Ihrem Computer installiert ist, wird mit der Installation von SSDT der vollständige Satz an SQL Server-Tools in Ihre vorhandene Installation von Visual Studio eingefügt. In Visual Studio sind viele Features enthalten, die Sie verwenden können – z.B. die Integration der Quellcodeverwaltung und nicht-SQL Sprachunterstützung. Es wird empfohlen, Visual Studio 2015 Community oder höher zu verwenden, um beim Entwickeln von T-SQL die bestmögliche Erfahrung zu haben.

## <a name="supported-sql-versions"></a>Unterstützte SQL-Versionen
  
|Projektvorlagen|Unterstützte SQL-Plattformen|  
|-------------------|--------------------|  
Relationale Datenbanken|  SQL Server 2005* – SQL Server 2016 <br /><br />Azure SQL-Datenbank<br /><br />Azure SQL Data Warehouse (unterstützt nur Abfragen, Datenbankprojekte werden noch nicht unterstützt)<br /><br />  * SQL Server 2005-Support ist veraltet,<br /><br /> wechseln Sie bitte zu einer offiziell unterstützten SQL-Version|
  |Analysis Services-Modelle<br /><br />Reporting Services-Berichte | SQL Server 2008 – SQL Server 2016|
  |Integration Services-Pakete| SQL Server 2012 – SQL Server 2016    |
  
## <a name="next-steps"></a>Nächste Schritte  
Gehen Sie nach der Installation von SSDT die folgenden Tutorials durch, um zu erfahren, wie Sie mithilfe von SSDT Datenbanken, Pakete, Datenmodelle und Berichte erstellen:  
  
-   [Projektorientierte Offlinedatenbankentwicklung](https://msdn.microsoft.com/library/hh272702(v=vs.103).aspx)  
  
-   [SSIS-Tutorial: Erstellen eines einfachen ETL-Pakets](https://msdn.microsoft.com/library/ms169917.aspx)  
  
-   [Analysis Services-Tutorials](https://msdn.microsoft.com/library/hh231701.aspx)  
  
-   [Erstellen eines einfachen Tabellenberichts (SSRS-Lernprogramm)](https://msdn.microsoft.com/library/ms167305.aspx)  
  
## <a name="see-also"></a>Siehe auch  
[SQL Server Data Tools in Visual Studio](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN-Forum](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT-Team-Blog](http://blogs.msdn.com/b/ssdt/)  
[SSDT Connect Feedback](https://connect.microsoft.com/SQLServer/Feedback)  
[SSDT-Dokumentation](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[DACFx-API-Referenz](https://msdn.microsoft.com/library/dn645454.aspx)  
[Herunterladen von SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  

