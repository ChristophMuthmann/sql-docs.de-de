---
title: "Comparing Tabular and Multidimensional Solutions (SSAS) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
caps.latest.revision: 49
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 47
---
# Comparing Tabular and Multidimensional Solutions (SSAS)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] stellt verschiedene Ansätze zum Erstellen eines Business Intelligence-Semantikmodells bereit: das mehrdimensionale, tabellarische und Power Pivot-Modell.  
  
 Mehr als ein Ansatz ermöglicht eine Modellierungsumgebung, die auf unterschiedliche Geschäfts- und Benutzeranforderungen zugeschnitten ist. Das mehrdimensionale Modell ist eine auf offenen Standards basierende ausgereifte Technologie, die von zahlreichen Herstellern von BI-Software genutzt wird, aber nur schwer zu meistern ist. Das tabellarische Modell bietet einen relationalen Modellierungsansatz, den viele Entwickler intuitiver finden. Das Power Pivot-Modell ist noch einfacher und bietet eine visuelle Datenmodellierung in Excel sowie Serverunterstützung, die über SharePoint bereitgestellt wird.  
  
 Alle Modelle werden als Datenbanken bereitgestellt, die in einer Analysis Services-Instanz ausgeführt werden. Der Zugriff auf die Modelle erfolgt durch Clienttools unter Verwendung einer einzelnen Gruppe von Datenanbietern. Die Visualisierung erfolgt in interaktiven und statischen Berichten über Excel, Reporting Services, Power BI und BI-Tools anderer Hersteller.  
  
 Aufgrund der Unterschiede bei Speicherarchitektur und Metadaten sind die Modelltypen nicht austauschbar. Sie können jedoch mühelos ein Upgrade von einem tabellarischen Modell des Typs 1050-1103 zum tabellarischen Modell 1200 vornehmen. Außerdem können Sie Power Pivot importieren, um ein völlig neues Modell als tabellarisches Projekt zu erstellen.  
  
 Tabellarische und mehrdimensionale Lösungen werden mit [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] erstellt und sind für BI-Unternehmensprojekte bestimmt, die auf einer eigenständigen [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]-Instanz ausgeführt werden. Beide Lösungen stellen hochleistungsfähige analytische Datenbanken bereit, die einfach in BI-Clients integriert werden können. Die einzelnen Lösungen unterscheiden sich jedoch darin, wie sie erstellt, verwendet und bereitgestellt werden. Dieses Thema beschäftigt sich hauptsächlich mit diesen beiden Typen, damit Sie den für Sie richtigen Ansatz bestimmen können.  
  
 Für neue Entwicklungsprojekte empfehlen wir in der Regel das tabellarische Modell. Es bietet schnellere Entwicklung, Testverfahren und Bereitstellung und arbeitet reibungsloser mit den neuesten Self-Service-BI-Anwendungen und Clouddiensten von Microsoft zusammen.  
  
##  <a name="a-namebkmkoverviewa-overview-of-modeling-types"></a><a name="bkmk_overview"></a> Übersicht über die Modellierungstypen  
 Neu bei Analysis Services? Die folgende Tabelle enthält eine Übersicht über die verschiedenen Modelle, den jeweiligen Ansatz sowie die entsprechende Software, in der das Modell erstmals eingeführt wurde.  
  
||||  
|-|-|-|  
|**Typ**|**Beschreibung der Modellierung**|**Eingeführt mit**|  
|Multidimensional|OLAP-Modellierungskonstrukte (Cubes, Dimensionen, Measures).|SQL Server 2000 und höher|  
|Tabellarisch|Relationale Modellierungskonstrukte (Modell, Tabellen, Spalten).<br /><br /> Intern werden Metadaten von OLAP-Modellierungskonstrukten (Cubes, Dimensionen, Measures) geerbt. Code und Skripts nutzen OLAP-Metadaten.|SQL Server 2012 und höher (Kompatibilitätsgrade 1050-1103) <sup>1</sup>|  
|Tabellarisch in SQL Server 2016|Relationale Modellierungskonstrukte (Modell, Tabellen, Spalten), gegliedert in Objektdefinitionen mit tabellarischen Metadaten in Skripts und Code.|SQL Server 2016 (Kompatibilitätsgrad 1200)|  
|Power Pivot|Ursprünglich ein Add-In, aber nun vollständig in Excel integriert. Nur visuelle Modellierung einer internen tabellarischen Infrastruktur. Sie können ein Power Pivot-Modell in SSDT importieren, um ein neues tabellarisches Modell zu erstellen, das in einer Analysis Services-Instanz ausgeführt wird.|Über Excel und Power Pivot BI Desktop|  
  
 <sup>1</sup>. In SQL Server 2012 eingeführte Kompatibilitätsgrade sind in der aktuellen Version besonders wichtig, und zwar aufgrund des neuen tabellarischen Metadatenmoduls und der Unterstützung für Features zum Ermöglichen von Szenarien, die nur auf dem höheren Grad verfügbar sind. Zu den besonderen Weiterentwicklungen gehören DirectQuery, Skripts und Programmierbarkeit. Unter [Neuigkeiten in Analysis Services](../analysis-services/what-s-new-in-analysis-services.md) finden Sie weitere Details.  
  
##  <a name="a-namebkmkmodelsa-model-features"></a><a name="bkmk_models"></a> Modellfunktionen  
  In der folgenden Tabelle wird die Funktionsverfügbarkeit auf der Modellebene zusammengefasst. Überprüfen Sie diese Liste, um sicherzustellen, dass das Feature, das Sie verwenden möchten, im Typ des Modells verfügbar ist, das Sie erstellen möchten.  
  
|||||  
|-|-|-|-|  
||Multidimensional|Tabellarisch|Power Pivot|  
|Aktionen|Ja|Nein|Nein|  
|Aggregationen|Ja|Nein|Nein|  
|Berechnete Spalte|Nein|Benutzerkontensteuerung|Ja|  
|Berechnete Measures|Ja|Benutzerkontensteuerung|Ja|  
|Berechnete Tabellen|Nein|Ja <sup>1</sup>|Nein|  
|Benutzerdefinierte Assemblys|Ja|Nein|Nein|  
|Benutzerdefinierte Rollups|Ja|Nein|Nein|  
|Standardelement|Ja|Nein|Nein|  
|Anzeigeordner|ja|Ja <sup>1</sup>|Nein|  
|Distinct Count|Ja|Ja (über DAX)|Ja (über DAX)|  
|Drillthrough ausführen|Ja|Ja (Detail wird in separatem Arbeitsblatt geöffnet)|Ja|  
|Hierarchien|ja|Benutzerkontensteuerung|ja|  
|KPIs (Key Performance Indicators)|ja|Benutzerkontensteuerung|Ja|  
|Verknüpfte Objekte|Ja|Ja (verknüpfte Tabellen)|Nein|  
|m:n-Beziehungen|Ja|Nein (es gibt jedoch [bidirektionale Kreuzfilter](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) bei Kompatibilitätsgrad 1200)|Nein|  
|Benannte Mengen|Ja|Nein|Nein|  
|Über- und untergeordnete Hierarchien|Ja|Ja (über DAX)|Ja (über DAX)|  
|Partitionen|Ja|Benutzerkontensteuerung|ja|  
|Perspektiven|ja|Benutzerkontensteuerung|Ja|  
|Semiadditive Measures|ja|Benutzerkontensteuerung|ja|  
|Translations|[Ja](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|Ja|[Ja](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)|  
|Benutzerdefinierte Hierarchien|Ja|Benutzerkontensteuerung|Ja|  
|Rückschreiben|Ja|Nein|Nein|  
  
 <sup>1</sup> Unter [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) finden Sie Informationen zu funktionalen Unterschieden im tabellarischen Bereich.  
  
##  <a name="a-namebkmkdsa-data-considerations"></a><a name="bkmk_ds"></a> Überlegungen zu Daten  
 Tabellarische und mehrdimensionale Modelle verwenden aus externen Quellen importierte Daten. Die Menge und Art der Daten, die Sie importieren müssen, kann ein wichtiger Aspekt bei der Entscheidung sein, welcher Modelltyp am besten für Ihre Daten geeignet ist.  
  
 **Komprimierung**  
  
 Sowohl tabellarische als auch mehrdimensionale Lösungen verwenden die Datenkomprimierung, durch die die Größe der Analysis Services-Datenbank relativ zum Data Warehouse verringert wird, aus dem Sie Daten importieren. Da sich der tatsächliche Komprimierungsgrad nach den Eigenschaften der zugrunde liegenden Daten richtet, lässt sich nicht genau vorhersagen, wie viel Datenträger- und Arbeitsspeicherkapazität von einer Lösung benötigt wird, nachdem die Daten verarbeitet und in Abfragen verwendet wurden.  
  
 Eine Faustregel, die von vielen Analysis Services-Entwicklern angewendet wird, besagt, dass der primäre Speicher einer mehrdimensionalen Datenbank ein Drittel der ursprünglichen Daten ausmachen sollte. Tabellarische Datenbanken können manchmal einen höheren Komprimierungsgrad von etwa einem Zehntel der Größe erzielen. Dies gilt insbesondere dann, wenn die meisten Daten aus Faktentabellen importiert werden.  
  
 **Größe des Modells und Ressourcenbevorzugung (im Arbeitsspeicher oder auf dem Datenträger)**  
  
 Die Größe einer Analysis Services-Datenbank wird nur durch die Ressourcen eingeschränkt, die für ihre Ausführung verfügbar sind. Der Modelltyp und Speichermodus spielen auch eine Rolle, in welchem Umfang die Datenbank anwachsen kann.  
  
 Tabellarische Datenbanken werden entweder im Arbeitsspeicher oder im DirectQuery-Modus ausgeführt, der die Ausführung von Abfragen an eine externe Datenbank verlagert. Für tabellarische Datenanalysen im Arbeitsspeicher wird die Datenbank vollständig im Arbeitsspeicher gespeichert. Das bedeutet, dass Sie über ausreichend Arbeitsspeicher nicht nur zum Laden aller Daten, sondern auch für zusätzliche Datenstrukturen verfügen müssen, die zum Unterstützen von Abfragen erstellt werden müssen.  
  
 Das für diese Version überarbeitete DirectQuery hat weniger Einschränkungen und eine bessere Leistung als zuvor. Durch das Nutzen der relationalen Back-End-Datenbank für die Speicherung und Ausführung von Abfragen ist das Erstellen eines großen tabellarischen Modells einfacher als bisher zu realisieren.  
  
 Bislang waren die größten [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]-Produktionsdatenbanken mehrdimensional, wobei Verarbeitungs- und Abfragearbeitsauslastungen unabhängig auf dedizierter Hardware ausgeführt werden, die für den jeweiligen Zweck entsprechend optimiert war.  Tabellarische Datenbanken holen rasch auf, und neue Weiterentwicklungen bei DirectQuery helfen, die Lücke noch schneller zu schließen.  
  
 Beim mehrdimensionalen Modell ist das Auslagern von Datenspeicherung und Abfrageausführung über ROLAP möglich.   Rowsets können auf einem Abfrageserver im Cache zwischengespeichert werden, veraltete Rowsets können ausgelagert werden. Aufgrund der effizienten und ausgewogenen Nutzung von Arbeitsspeicher- und Datenträgerressourcen entscheiden sich Kunden häufig für mehrdimensionale Lösungen.  
  
 Unter Belastung ist davon auszugehen, dass die Kapazitätsanforderungen sowohl an den Datenträger als auch an den Arbeitsspeicher steigen, weil Daten von Analysis Services zwischengespeichert, gespeichert, durchsucht und abgefragt werden. Weitere Informationen zu Speicherauslagerungsoptionen finden Sie unter [Memory Properties](../analysis-services/server-properties/memory-properties.md) (Speichereigenschaften). Weitere Informationen zum Skalieren finden Sie unter [Hohe Verfügbarkeit und Skalierbarkeit in Analysis Services](../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md).  
  
 Power Pivot für Excel verfügt über eine künstliche Dateigrößenbeschränkung von 2 Gigabytes, damit in Power Pivot für Excel erstellte Arbeitsmappen in SharePoint hochgeladen werden können, da die Größe hochgeladener Dateien auf dieser Plattform beschränkt ist. Einer der Hauptgründe, warum eine Power Pivot-Arbeitsmappe zu einer tabellarischen Lösung auf einer eigenständigen Analysis Services-Instanz migriert werden sollte, liegt darin, dass die Beschränkung der Dateigröße auf diesem Weg umgangen werden kann. Weitere Informationen zum Konfigurieren der maximalen Dateiuploadgröße finden Sie unter [Konfigurieren der maximalen Dateiuploadgröße &#40;PowerPivot für SharePoint&#41;](../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
 **Unterstützte Datenquellen**  
  
 Mehrdimensionale Lösungen sind in der Lage, Daten mit nativen und verwalteten OLE DB-Anbietern aus relationalen Datenquellen zu importieren.  
  
 Tabellarische Modelle sind in der Lage, Daten aus relationalen Datenquellen, Datenfeeds und einigen Dokumentformaten zu importieren. Für tabellarische Modelle können Sie auch OLE DB für ODBC-Anbieter verwenden.  
  
 Die Liste externer Datenquellen, die in jedes Modell importiert werden können, finden Sie in den folgenden Themen:  
  
-   [Unterstützte Datenquellen &#40;SSAS – Mehrdimensional&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
-   [Unterstützte Datenquellen &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
##  <a name="a-namebkmklanga-query-and-scripting-language-support"></a><a name="bkmk_lang"></a> Unterstützung für Abfrage und Skriptsprache  
 Analysis Services schließen MDX, DMX, DAX, XML/A, ASSL und TMSL ein. Die Unterstützung für diese Sprachen kann je nach Modelltyp variieren. Wenn Anforderungen für die Abfrage und Skriptsprache in Betracht kommen, überprüfen Sie die folgende Liste.  
  
-   PowerPivot-Arbeitsmappen verwenden DAX für Berechnungen und DAX oder MDX für Abfragen.  
  
-   Tabellarische Modelldatenbanken unterstützen DAX-Berechnungen, DAX-Abfragen und MDX-Abfragen. Dies gilt für alle Kompatibilitätsgrade. Skriptsprachen sind ASSL (über XMLA) für die Kompatibilitätsgrade 1050-1103 und TMSL (über XMLA) für den Kompatibilitätsgrad 1200.  
  
-   Mehrdimensionale Modelldatenbanken unterstützen MDX-Berechnungen und MDX-Abfragen sowie ASSL.  
  
-   Data Mining-Modelle unterstützen DMX und ASSL.  
  
-   Analysis Services PowerShell wird für tabellarische und mehrdimensionale Modelle und Datenbanken unterstützt.  
  
 Alle Datenbanken unterstützen XML/A. Unter [Abfragen- und Ausdruckssprachreferenz &#40;Analysis Services&#41;](../Topic/Query%20and%20Expression%20Language%20Reference%20\(Analysis%20Services\).md) und [Entwicklerhandbuch (Analysis Services)](../analysis-services/analysis-services-developer-documentation.md) finden Sie weitere Informationen.  
  
##  <a name="a-namebkmkseca-security-features"></a><a name="bkmk_sec"></a> Sicherheitsfeatures  
 Alle Analysis Services-Projektmappen können auf Datenbankebene gesichert werden. Präzisere Sicherheitsoptionen variieren je nach Modus. Wenn präzise Sicherheitseinstellungen für die Projektmappe erforderlich sind, überprüfen Sie die folgende Liste, um sicherzustellen, dass die Sicherheitsstufe, die Sie möchten, für den zu erstellenden Projektmappentyp unterstützt wird:  
  
-   [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Arbeitsmappen werden mit SharePoint-Berechtigungen auf Dateiebene gesichert.  
  
-   Für tabellarische Modelldatenbanken kann Sicherheit auf Zeilenebene mit rollenbasierten Berechtigungen in Analysis Services verwendet werden.  
  
-   Für mehrdimensionale Modelldatenbanken kann Sicherheit auf Dimensions- und Zellenebene verwendet werden, wobei rollenbasierte Berechtigungen in Analysis Services verwendet werden.  
  
 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Arbeitsmappen können für einen Server im tabellarischen Modus wiederhergestellt werden. Nachdem die Datei wiederhergestellt wurde, wird sie von SharePoint entkoppelt, und Sie können alle tabellarischen Modellierungsfeatures verwenden, einschließlich Sicherheit auf Zeilenebene.  
  
##  <a name="a-namebkmkdesignera-design-tools"></a><a name="bkmk_designer"></a>-Entwurftools  
 Fähigkeiten zur Datenmodellierung und technische Kenntnisse können unter Benutzern, die mit dem Erstellen von analytischen Modellen beauftragt sind, stark variieren. Wenn die Vertrautheit mit dem Tool oder Anwender-Know-How eine für die Projektmappe in Betracht kommt, vergleichen Sie die folgenden Erfahrungen für die Modellerstellung.  
  
|Modellierungstool|Verwendung|  
|-------------------|--------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Verwenden Sie diese, um tabellarische, mehrdimensionale und Data Mining-Projektmappen zu erstellen. Diese Erstellungsumgebung stellt Arbeitsbereiche, Eigenschaftenbereiche und Objektnavigation mithilfe von Visual Studio Shell bereit. Technisch versierte Benutzer, die bereits Visual Studio verwenden, ziehen höchstwahrscheinlich dieses Tool zum Erstellen von Business Intelligence-Anwendungen vor.|  
|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für Excel|Verwenden Sie diese Funktion, um eine [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Arbeitsmappe zu erstellen, die Sie später in einer SharePoint-Farm bereitstellen, die über eine Installation von [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für SharePoint verfügt. [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für Excel hat einen separaten Anwendungsarbeitsbereich, der über Excel geöffnet wird. Es werden die gleichen visuellen Metaphern (Seiten im Registerkartenformat, Rasterlayout und Bearbeitungsleiste) wie in Excel verwendet. Benutzer, die in Excel versiert sind, werden dieses Tool gegenüber [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] bevorzugen.|  
  
##  <a name="a-namebkmkclienta-client-application-support"></a><a name="bkmk_client"></a> Unterstützung für Clientanwendungen  
 Wenn Sie Reporting Services verwenden, variiert die Verfügbarkeit der Berichtsfunktion je nach Edition und Servermodus. Aus diesem Grund kann sich der zu erstellende Berichtstyp auf den zu installierenden Servermodus auswirken.  
  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], ein neues Reporting Services-Erstellungstool, das in SharePoint ausgeführt wird, ist auf einem Berichtsserver verfügbar, der in einer SharePoint 2010-Farm bereitgestellt wird. Der einzige Datenquellentyp, der mit diesem Bericht verwendet werden kann, ist eine tabellarische Analysis Services-Modelldatenbank oder eine [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Arbeitsmappe. Dies bedeutet, dass Sie über einen Server im tabellarischen Modus oder einen [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für SharePoint-Server verfügen müssen, damit die von diesem Berichtstyp verwendete Datenquelle gehostet wird. Sie können kein mehrdimensionales Modell als Datenquelle für einen [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]-Bericht verwenden. Sie müssen eine [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] BI-Semantikmodellverbindung oder eine freigegebene Reporting Services-Datenquelle erstellen, die als Datenquelle für einen [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]-Bericht verwendet wird.  
  
 Beliebige Analysis Services-Datenbanken können vom Berichts-Generator und Berichts-Designer verwendet werden, einschließlich [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Arbeitsmappen, die in [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für SharePoint gehostet werden.  
  
 Excel-PivotTable-Berichte werden von allen Analysis Services-Datenbanken unterstützt. Die Excel-Funktionalität ist unabhängig davon identisch, ob Sie eine tabellarische Datenbank, eine mehrdimensionale Datenbank oder eine [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Arbeitsmappe verwenden, obwohl das Rückschreiben nur für mehrdimensionale Datenbanken unterstützt wird.  
  
 PerformancePoint-Dashboards können eine Verbindung mit allen Analysis Services-Datenbanken herstellen, einschließlich [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Arbeitsmappen. Weitere Informationen finden Sie unter [Erstellen von Datenverbindungen (PerformancePoint Services)](http://go.microsoft.com/fwlink/?linkdID=218155).  
  
##  <a name="a-namebkmkdeploymentmodea-server-deployment-modes-for-multidimensional-and-tabular-solutions"></a><a name="bkmk_deploymentmode"></a> Serverbereitstellungsmodi für mehrdimensionale und tabellarische Lösungen  
 Eine Analysis Services-Instanz ist in einem der drei Modi installiert, die den operativen Kontext des Servers festlegen. Der Servermodus, den Sie installieren, bestimmt den Typ von Projektmappen, die auf diesem Server bereitgestellt werden können. Die Speicher- und Arbeitsspeicherarchitektur sind die primären Unterschiede zwischen den Modi, zusätzliche Unterschiede sind jedoch vorhanden. Die drei Servermodi werden in der folgenden Tabelle kurz beschrieben. Weitere Informationen finden Sie unter [Bestimmen des Servermodus einer Analysis Services-Instanz](../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
|Bereitstellungsmodus|Beschreibung|  
|---------------------|-----------------|  
|0 - Mehrdimensionaler Modus und Data Mining-Modus|Ausführung mehrdimensionaler Lösungen und Data Mining-Lösungen, die Sie auf einer Standardinstanz von Analysis Services bereitstellen. Der Bereitstellungsmodus 0 ist der Standardmodus für eine Analysis Services-Installation.|  
|1 – [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für SharePoint|Beim [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Datenzugriff fungiert Analysis Services als eine interne Komponente einer [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für SharePoint-Installation. Analysis Services wird im Bereitstellungsmodus 1 installiert und ausschließlich von [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Diensten in einer SharePoint-Umgebung verwendet.|  
|2 - Tabellarischer Modus|Ausführung tabellarischer Lösungen auf einer eigenständigen Analysis Services-Instanz, die für den Bereitstellungsmodus 2 konfiguriert wurde.|  
  
 Weitere Informationen finden Sie unter [Installieren von Analysis Services](../analysis-services/instances/install-windows/install-analysis-services.md).  
  
##  <a name="a-namebkmksharepointa-sharepoint-requirements"></a><a name="bkmk_sharePoint"></a> SharePoint-Anforderungen  
 SQL Server ist in SharePoint integriert, da Unterstützung für [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Datenzugriff und den Zugriff auf tabellarische Daten hinzugefügt wurde. Die Investitionskosten einer integrierten SharePoint- und SQL Server-Lösung sind umso höher, je mehr Funktionen für die einzelnen Produkte verfügbar sind. Wenn Sie über SharePoint verfügen, können Sie SQL Server [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für SharePoint installieren, um den [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Datenzugriff zu ermöglichen und die BISM-Verbindungsdateien von [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] zu nutzen. Diese werden für den Zugriff auf tabellarische Datenbanken verwendet, die in einer externen Analysis Services-Instanz auf einem Netzwerkserver ausgeführt werden.  
  
 Die Power View-Berichterstellung, die [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] und tabellarische Datenbanken als Datenquelle verwendet, ist ein von SQL Server bereitgestelltes SharePoint-Feature und ein integriertes Feature von Excel. Obwohl die tabellarischen Datenbanken auf einer Analysis Services-Instanz außerhalb von SharePoint ausgeführt werden, werden diese Daten von Power View-Berichten, die in SharePoint ausgeführt werden, genutzt.  
  
 Wenn Sie SharePoint nicht verwenden, können Sie [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für Excel trotzdem zum Erstellen von [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Arbeitsmappen verwenden. Dabei steht Ihnen jedoch keine kohäsive Datenvisualisierung zur Verfügung. Jeder Benutzer, der die Arbeitsmappe verwendet, muss jede Arbeitsmappe mit dem [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für Excel-Add-In herunterladen und in Excel anzeigen, um die Dateninteraktion und -analyse mit Slicern, Filtern und Pivots nutzen zu können. Andernfalls ist die Visualisierung von Arbeitsmappen auf statische Daten beschränkt, so wie sie beim Öffnen der Arbeitsmappe angezeigt werden.  
  
 Tabellarische, mehrdimensionale und Data Mining-Lösungen können auf Analysis Services-Instanzen in einem Netzwerk ausgeführt werden, ohne dass eine SharePoint-Abhängigkeit besteht.  
  
##  <a name="a-namebkmkexta-programmability-and-extensibility-support"></a><a name="bkmk_ext"></a> Unterstützung für Programmier- und Erweiterbarkeit  
 Obwohl Entwicklerunterstützung für Power BI geboten wird, gibt es keine Entwicklerunterstützung für [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Arbeitsmappen. Wenn Sie [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Arbeitsmappen verwenden, müssen Sie den integrierten Client und die Serveranwendungen als Teil der Projektmappe verwenden. Als einzige Optionen stehen die Excel-Programmierung und die SharePoint-Programmierung zur Verfügung.  
  
 Informationen zu Power BI finden Sie unter [Power BI Embedded](https://azure.microsoft.com/services/power-bi-embedded/).  
  
 Tabellarische Lösungen unterstützen nur eine model.bim-Datei pro Lösung. Das bedeutet, dass die gesamte Arbeit in einer einzelnen Datei erledigt werden muss. Entwicklungsteams, die daran gewöhnt sind, mit mehreren Projekten in einer einzelnen Lösung zu arbeiten, müssen ihre Arbeitsweise bei der Erstellung einer freigegebenen tabellarischen Lösung möglicherweise überdenken.  
  
 Tabellarische Lösungen mit Kompatibilitätsgrad 1200 werden einem neuen Objektmodell zugeordnet, das tabellarische Metadaten verwendet. Ältere tabellarische und alle mehrdimensionalen Modelle verwenden mehrdimensionale Metadaten als Deskriptoren. Es wird empfohlen, ältere tabellarische Modelle auf den Kompatibilitätsgrad 1200 zu aktualisieren, damit Sie die tabellarischen Namespaces in AMO für benutzerdefinierten Code und Skripts verwenden können.  
  
 Weitere Informationen finden Sie in der [Dokumentation für Analysis Services-Entwickler](https://msdn.microsoft.com/library/bb500153.aspx).  
  
##  <a name="a-namebkmknexta-next-step-build-a-solution"></a><a name="bkmk_Next"></a> Nächster Schritt: Erstellen einer Lösung  
 Nachdem Sie jetzt ein grundlegendes Verständnis der Unterschiede zwischen den Lösungen gewonnen haben, können Sie die folgenden Lernprogramme ausführen, um sich mit den Schritten zur Erstellung der einzelnen Lösungen vertraut zu machen. Über die folgenden Links gelangen Sie zu den Lernprogrammen, in denen die Schritte erklärt sind.  
  
-   Erstellen eines [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Modells. Informationen finden Sie unter [Erste Schritte mit Power Pivot in Microsoft Excel](https://support.office.com/article/Get-started-with-Power-Pivot-in-Microsoft-Excel-fdfcf944-7876-424a-8437-1a6c1043a80b).  
  
-   Erstellen eines tabellarischen Modells Informationen finden Sie unter [Tabellenmodellierung &#40;Adventure Works-Tutorial&#41;](../analysis-services/tabular-modeling-adventure-works-tutorial.md).  
  
-   Erstellen eines mehrdimensionalen Modells Informationen finden Sie unter [Mehrdimensionale Modellierung &#40;Adventure Works-Tutorial&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md).  
  
-   Erstellen eines Data Mining-Modells Informationen finden Sie unter [Data Mining-Grundlagen – Tutorial](../Topic/Basic%20Data%20Mining%20Tutorial.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services-Instanzverwaltung](../analysis-services/instances/analysis-services-instance-management.md)   
 [Neuigkeiten in Analysis Services](../analysis-services/what-s-new-in-analysis-services.md)     
 [Neuerungen in Power Pivot](http://go.microsoft.com/fwlink/?LinkId=238141)   
 [PowerPivot-BI-Semantikmodell-Verbindung &#40;.bism&#41;](../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [Erstellen und Verwalten von freigegebenen Datenquellen &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../Topic/Create%20and%20Manage%20Shared%20Data%20Sources%20\(Reporting%20Services%20in%20SharePoint%20Integrated%20Mode\).md)  
  
  