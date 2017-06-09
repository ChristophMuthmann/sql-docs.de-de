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
ms.sourcegitcommit: 5bd0e1d3955d898824d285d28979089e2de6f322
ms.openlocfilehash: 7aaa4c48419bf24357b2bef95c40d721d1ab2f2a
ms.contentlocale: de-de
ms.lasthandoff: 06/05/2017

---
# <a name="download-sql-server-data-tools-ssdt"></a>Herunterladen von SQL Server Data Tools (SSDT)

**[SQL Server Datatools](https://msdn.microsoft.com/mt186501)** ist ein modernes und kostenlos herunterladbares Entwicklungstool für relationale SQL Server-Datenbanken, Azure SQL-Datenbanken, Integration Services-Pakete, Analysis Services-Datenmodelle und Reporting Services-Berichte. Mit SSDT lassen sich Datenbanken und andere Inhaltstypen für SQL Server entwerfen und bereitstellen – und zwar ebenso einfach wie eine Anwendung in Visual Studio. Diese Version unterstützt SQL Server 2005 bis SQL Server 2017 und bietet die Entwurfsumgebung zum Hinzufügen von neuen Features, die in SQL Server 2016 angeboten werden.  
    
    
![Download](../ssdt/media/download.png) [Herunterladen von SQL Server Data Tools 17.1 für Visual Studio 2015](https://go.microsoft.com/fwlink/?linkid=849393)

![Download](../ssdt/media/download.png) [Data-Tier Application Framework 17.1 (DacFx) herunterladen](https://www.microsoft.com/download/details.aspx?id=55255)

## <a name="sql-server-data-tools"></a>SQL Server Data Tools   
**Versionsinformationen**  
  
Versionsnummer: 17.1  
Buildnummer dieser Version: 14.0.61705.170
  
 **What's New in BizTalk Server 2016 (Neuerungen in BizTalk Server 2016)**
 - Offline-Unterstützung für nicht-modellbezogenes IntelliSense in Analysis Services (z.B. Markieren, Anweisungsabschluss und Parameterinformation)
 - Zusatz zum Tabellenmodell-Explorer zur Darstellung von M-Ausdrücken
 - Azure Active Directory-Personenauswahl für die Konfiguration von Rollenmitgliedern in tabellarischen Modellen
 - Support für Codierungshinweise in der Benutzeroberfläche beim Definieren von 1400-Modellen
 - Einige Behebungen von Programmfehlern in AS-Projekten
 - Einige Behebungen von Programmfehlern in DacFx

 **Bekannte Probleme**
 - Beim Erstellen einer neuen Datenquelle in einem AS-Modell mit Kompabilitätsgrad 1400 wird der tabellarische Editor (Model.bim) schreibgeschützt, wenn Sie eine dateibasierte Datenquelle auswählen und „Abbrechen“ klicken, bevor Sie die Datenquelle erstellt haben. Sie können dieses Problem umgehen, indem Sie den tabellarischen Editor einfach schließen und ihn im Projektmappen-Explorer wieder öffnen.

Vollständige Listen der Änderungen sind im [Änderungsprotokoll](changelog-for-sql-server-data-tools-ssdt.md) verfügbar.

 > Informationen zur Verwendung von SQL Server Data Tools in Visual Studio 2017 finden Sie in [diesem Abschnitt](#use-ssdt-in-visual-studio-2017).

  **Verfügbare Sprachen**  
  
 Diese Version von SSDT kann in folgenden Sprachen installiert werden:  
[Chinesisch (Volksrepublik China)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x804) | 
[Chinesisch (Taiwan)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x404) | 
[Englisch (Vereinigte Staaten)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x409) | 
[Französisch]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x40c)  
[Deutsch]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x407) | 
[Italienisch]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x410) | 
[Japanisch]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x411) | 
[Koreanisch]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x412) | 
[Portugiesisch (Brasilien)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x416) | 
[Russisch]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x419) | 
[Spanisch]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x40a)  

**ISO-Images**

Alternativ zur Installation von SSDT oder zur Einrichtung eines Administratorinstallationspunkts kann ein ISO-Image von SSDT verwendet werden. Das ISO-Image ist eine eigenständige Datei, die alle für SSDT erforderlichen Komponenten enthält und mit einem Download-Manager heruntergeladen werden kann, der einen Neustart ermöglicht und besonders für begrenzte oder schwankende Netzwerkbandbreiten geeignet ist. Nach dem Download kann das ISO-Image als Laufwerk eingebunden oder auf eine DVD gebrannt werden.

[Chinesisch (Volksrepublik China)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x804) |
[Chinesisch (Taiwan)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x404) |
[Englisch (Vereinigte Staaten)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x409) |
[Französisch]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x40c)  
[Deutsch]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x407) |
[Italienisch]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x410) |
[Japanisch]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x411) |
[Koreanisch]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x412) |
[Portugiesisch (Brasilien)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x416) |
[Russisch]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x419) |
[Spanisch]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x40a)

## <a name="download-visual-studio"></a>Herunterladen von Visual Studio

* [**Laden Sie Visual Studio Community 2015 herunter**](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)

## <a name="installing-ssdt-without-visual-studio-pre-installed"></a>Installieren von SSDT ohne vorinstalliertes Visual Studio

Wenn Visual Studio auf Ihrem Computer noch nicht installiert ist, wird mit der Installation von SSDT für Visual Studio 2015 auch eine reduzierte „integrierte Shell“-Version von Visual Studio 2015 installiert. Diese Version von Visual Studio kann kostenlos installiert und auf so vielen Computern wie gewünscht verwendet werden. Dadurch erhalten Sie alle Projekttypen von SQL Server sowie den Objektexplorer von SQL Server und weitere SQL-Tools.

Wenn [Visual Studio 2015 Community Edition (oder höher)](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) auf Ihrem Computer installiert ist, wird mit der Installation von SSDT der vollständige Satz an SQL Server-Tools in Ihre vorhandene Installation von Visual Studio eingefügt. In Visual Studio sind viele Features enthalten, die Sie verwenden können – z.B. die Integration der Quellcodeverwaltung und nicht-SQL Sprachunterstützung. Es wird empfohlen, Visual Studio 2015 Community oder höher zu verwenden, um beim Entwickeln von T-SQL die bestmögliche Erfahrung zu haben.

## <a name="supported-sql-versions"></a>Unterstützte SQL-Versionen
  
|Projektvorlagen|Unterstützte SQL-Plattformen|  
|-------------------|--------------------|  
Relationale Datenbanken|  SQL Server 2005* – SQL Server 2017 <br /><br />Azure SQL-Datenbank<br /><br />Azure SQL Data Warehouse (unterstützt nur Abfragen, Datenbankprojekte werden noch nicht unterstützt)<br /><br />  * SQL Server 2005-Support ist veraltet,<br /><br /> wechseln Sie bitte zu einer offiziell unterstützten SQL-Version|
  |Analysis Services-Modelle<br /><br />Reporting Services-Berichte | SQL Server 2008 – SQL Server 2017|
  |Integration Services-Pakete| SQL Server 2012 – SQL Server 2017    |
  
## <a name="next-steps"></a>Nächste Schritte  
Gehen Sie nach der Installation von SSDT die folgenden Tutorials durch, um zu erfahren, wie Sie mithilfe von SSDT Datenbanken, Pakete, Datenmodelle und Berichte erstellen:  
  
-   [Projektorientierte Offlinedatenbankentwicklung](https://msdn.microsoft.com/library/hh272702(v=vs.103).aspx)  
  
-   [SSIS-Tutorial: Erstellen eines einfachen ETL-Pakets](https://msdn.microsoft.com/library/ms169917.aspx)  
  
-   [Analysis Services-Tutorials](https://msdn.microsoft.com/library/hh231701.aspx)  
  
-   [Erstellen eines einfachen Tabellenberichts (SSRS-Lernprogramm)](https://msdn.microsoft.com/library/ms167305.aspx)  
  
## <a name="use-ssdt-in-visual-studio-2017"></a>Verwenden von SSDT in Visual Studio 2017 

* [**Visual Studio 2017 herunterladen** ](https://www.visualstudio.com/) ([Visual Studio 2017-Features nach Edition vergleichen](https://www.visualstudio.com/vs/compare/))

Um relationale Datenbankprojekte zu verwenden, empfehlen wir die Überprüfung der Arbeitsauslastung von **Datenspeicherung und Verarbeitung** während der Installation. Unterstützung für SSDT-Datenbankprojekte ist auch in einigen anderen Arbeitsauslastungen enthalten, darunter *Azure*, *ASP.Net and Web Development* und *.Net Core Cross Platform Development*.

> [!NOTE]
> SSDT-Datenbankprojekte in Visual Studio 2017 unterstützt derzeit bis zu SQL Server 2016.  Die Unterstützung für SQL Server 2017 erscheint bald in einem Visual Studio 2017-Update.

Installieren Sie, wenn Sie SSDT mit Visual Studio 2017 verwenden, die AS- und RS-Komponenten:
* [Analysis Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)
* [Reporting Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)


## <a name="see-also"></a>Siehe auch  
[SQL Server Data Tools in Visual Studio](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN-Forum](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT-Team-Blog](http://blogs.msdn.com/b/ssdt/)  
[SSDT Connect Feedback](https://connect.microsoft.com/SQLServer/Feedback)  
[SSDT-Dokumentation](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[DACFx-API-Referenz](https://msdn.microsoft.com/library/dn645454.aspx)  
[Herunterladen von SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  

