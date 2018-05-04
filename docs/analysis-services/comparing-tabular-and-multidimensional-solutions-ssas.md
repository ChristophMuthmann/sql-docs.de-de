---
title: Vergleichen von tabellarischen und mehrdimensionalen Lösungen (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: multidimensional-tabular
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
caps.latest.revision: 49
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4f7e75c9a5f31d37b32bade54dd9bd108de21e9a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="comparing-tabular-and-multidimensional-solutions"></a>Vergleichen von tabellarischen und mehrdimensionalen Lösungen
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  SQL Server Analysis Services bietet mehrere Ansätze zum Erstellen eines Business Intelligence-Semantikmodells: tabellarische, mehrdimensionale und Power Pivot für SharePoint.
  
 Mehr als ein Ansatz ermöglicht eine Modellierungsumgebung, die auf unterschiedliche Geschäfts- und Benutzeranforderungen zugeschnitten ist. Das mehrdimensionale Modell ist eine auf offenen Standards basierende ausgereifte Technologie, die von zahlreichen Herstellern von BI-Software genutzt wird, aber nur schwer zu meistern ist. Das tabellarische Modell bietet einen relationalen Modellierungsansatz, den viele Entwickler intuitiver finden. Das Power Pivot-Modell ist noch einfacher und bietet eine visuelle Datenmodellierung in Excel sowie Serverunterstützung, die über SharePoint bereitgestellt wird.  
  
 Alle Modelle werden als Datenbanken bereitgestellt, die in einer Analysis Services-Instanz ausgeführt werden. Der Zugriff auf die Modelle erfolgt durch Clienttools unter Verwendung einer einzelnen Gruppe von Datenanbietern. Die Visualisierung erfolgt in interaktiven und statischen Berichten über Excel, Reporting Services, Power BI und BI-Tools anderer Hersteller.  
  
 Tabellarische und mehrdimensionale Lösungen mithilfe von SSDT erstellt und dienen der für Unternehmens-BI-, die auf einem eigenständigen ausgeführt Projekte [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Instanz lokal, und für tabellarische Modelle ein [Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) Server in der die Cloud. Beide Lösungen stellen hochleistungsfähige analytische Datenbanken bereit, die einfach in BI-Clients integriert werden können. Die einzelnen Lösungen unterscheiden sich jedoch darin, wie sie erstellt, verwendet und bereitgestellt werden. Dieses Thema beschäftigt sich hauptsächlich mit diesen beiden Typen, damit Sie den für Sie richtigen Ansatz bestimmen können.  
  
 Bei neuen Projekten empfiehlt es sich im Allgemeinen tabellarische Modelle. Tabellarische Modelle sind schneller zu entwerfen, testen und bereitstellen. und arbeitet reibungsloser mit den neuesten Self-service BI-Anwendungen, und cloud-Dienste von Microsoft.  
  
##  <a name="bkmk_overview"></a> Übersicht über die Modellierungstypen  
 Neu bei Analysis Services? Die folgende Tabelle enthält eine Übersicht über die verschiedenen Modelle, den jeweiligen Ansatz sowie die entsprechende Software, in der das Modell erstmals eingeführt wurde.  
 
 > [!NOTE]  
>  **Azure Analysis Services** tabellarische Modelle mit dem Kompatibilitätsgrad 1200 oder höher unterstützt. Nicht alle in diesem Thema beschriebenen tabellarischer Modelle-Funktionalität wird jedoch in Azure Analysis Services unterstützt. Zwar erstellen und Bereitstellen von tabellarischen Modellen mit Azure Analysis Services ähnlich wie bei einer lokalen, ist es wichtig, die Unterschiede zu verstehen. Weitere Informationen finden Sie unter [was Azure Analysis Services ist?](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview)
  
||||  
|-|-|-|  
|**Typ**|**Beschreibung der Modellierung**|**Eingeführt mit**|  
|Tabellarisch|Relationale Modellierungskonstrukte (Modell, Tabellen, Spalten). Intern werden Metadaten von OLAP-Modellierungskonstrukten (Cubes, Dimensionen, Measures) geerbt. Code und Skripts nutzen OLAP-Metadaten.|SQL Server 2012 und höher (Kompatibilitätsgrade 1050-1103) <sup>1</sup>|  
|Tabellarisch in SQL Server 2016|Relationalen modellierungskonstrukten (Modell, Tabellen, Spalten), gegliedert in Objektdefinitionen in tabellarischen Metadaten [Tabular Model Scripting Language (TMSL)](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) und [tabellarisches Objekt Model (TOM)](../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md) Code.|SQL Server 2016 (Kompatibilitätsgrad 1200)| 
|Tabellarisch in SQLServer 2017|Relationalen modellierungskonstrukten (Modell, Tabellen, Spalten), gegliedert in Objektdefinitionen in tabellarischen Metadaten [Tabular Model Scripting Language (TMSL)](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) und [tabellarisches Objekt Model (TOM)](../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md) Code.|SQL Server-2017 (Kompatibilitätsgrad 1400)| 
|Multidimensional|OLAP-Modellierungskonstrukte (Cubes, Dimensionen, Measures).|SQL Server 2000 und höher|  
|Power Pivot|Ursprünglich ein Add-In, aber nun vollständig in Excel integriert. Nur visuelle Modellierung einer internen tabellarischen Infrastruktur. Sie können ein Power Pivot-Modell in SSDT importieren, um ein neues tabellarisches Modell zu erstellen, das in einer Analysis Services-Instanz ausgeführt wird.|Über Excel und Power Pivot BI Desktop|  
  
 <sup>1</sup> Kompatibilitätsgrade sind von Bedeutung in der aktuellen Version aufgrund von tabellarischen metadatenmoduls und Unterstützung für das Szenario aktivieren Funktionen, die nur auf der höheren Ebene verfügbar sind. Höhere Versionen unterstützen früheren Kompatibilitätsgraden funktionsfähig, aber es wird empfohlen, neue Modelle erstellen oder aktualisieren vorhandene Modelle auf der höchsten Kompatibilitätsgrad, die von der Serverversion unterstützt.
  
##  <a name="bkmk_models"></a> Modellfunktionen  
  In der folgenden Tabelle wird die Funktionsverfügbarkeit auf der Modellebene zusammengefasst. Überprüfen Sie diese Liste, um sicherzustellen, dass das Feature, das Sie verwenden möchten, im Typ des Modells verfügbar ist, das Sie erstellen möchten.  
  
|||| 
|-|-|-|
||Multidimensional|Tabellarisch|
|Aktionen|ja|nein|
|Aggregationen|ja|nein|
|Berechnete Spalte|nein|ja|  
|Berechnete Measures|ja|ja| 
|Berechnete Tabellen|nein|Ja<sup>1</sup>|  
|Benutzerdefinierte Assemblys|ja|nein|
|Benutzerdefinierte Rollups|ja|nein| 
|Standardelement|ja|nein|  
|Anzeigeordner|ja|Ja<sup>1</sup>|  
|Distinct Count|ja|Ja (über DAX)|
|Drillthroughberichte|ja|Ja (hängt mit Client-Anwendung)|
|Hierarchien|ja|ja|
|KPIs (Key Performance Indicators)|ja|ja| 
|Verknüpfte Objekte|ja|Ja (verknüpfte Tabellen)|
|M-Ausdrücke|nein|Ja<sup>1</sup>|
|m:n-Beziehungen|ja|Nein (es gibt jedoch [bidirektionale kreuzfilter](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) Kompatibilitätsgrade 1200 oder höher)| 
|Benannte Mengen|ja|nein| 
|Unregelmäßige Hierarchien|ja|Ja<sup>1</sup>|  
|Über- und untergeordnete Hierarchien|ja|Ja (über DAX)|
|Partitionen|ja|ja| 
|Perspektiven|ja|ja|
|Sicherheit auf Zeilenebene|ja|ja| 
|Sicherheit auf Nachrichtenebene-Objekt|ja|Ja<sup>1</sup>|
|Semiadditive Measures|ja|ja| 
|Übersetzungen|[Ja](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|ja| 
|Benutzerdefinierte Hierarchien|ja|ja|
|Rückschreiben|ja|nein| 
  
 <sup>1</sup> finden Sie unter [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) für Informationen zu funktionalen Unterschieden zwischen den Kompatibilitätsgraden funktionsfähig.  
  
##  <a name="bkmk_ds"></a> Überlegungen zu Daten  
 Tabellarische und mehrdimensionale Modelle verwenden importierte Daten aus externen Quellen. Die Menge und Art der Daten, die Sie importieren müssen, kann ein wichtiger Aspekt bei der Entscheidung sein, welcher Modelltyp am besten für Ihre Daten geeignet ist.  
  
 **Komprimierung**  
  
 Sowohl tabellarische als auch mehrdimensionale Lösungen verwenden die Datenkomprimierung, durch die die Größe der Analysis Services-Datenbank relativ zum Data Warehouse verringert wird, aus dem Sie Daten importieren. Da sich der tatsächliche Komprimierungsgrad nach den Eigenschaften der zugrunde liegenden Daten richtet, lässt sich nicht genau vorhersagen, wie viel Datenträger- und Arbeitsspeicherkapazität von einer Lösung benötigt wird, nachdem die Daten verarbeitet und in Abfragen verwendet wurden.  
  
 Eine Faustregel, die von vielen Analysis Services-Entwicklern angewendet wird, besagt, dass der primäre Speicher einer mehrdimensionalen Datenbank ein Drittel der ursprünglichen Daten ausmachen sollte. Tabellarische Datenbanken können manchmal einen höheren Komprimierungsgrad von etwa einem Zehntel der Größe erzielen. Dies gilt insbesondere dann, wenn die meisten Daten aus Faktentabellen importiert werden.  
  
 **Größe des Modells und Ressourcenbevorzugung (im Arbeitsspeicher oder auf dem Datenträger)**  
  
 Die Größe einer Analysis Services-Datenbank wird nur durch die Ressourcen eingeschränkt, die für ihre Ausführung verfügbar sind. Der Modelltyp und Speichermodus spielen auch eine Rolle, in welchem Umfang die Datenbank anwachsen kann.  
  
 Tabellarische Datenbanken werden entweder im Arbeitsspeicher oder im DirectQuery-Modus ausgeführt, der die Ausführung von Abfragen an eine externe Datenbank verlagert. Für tabellarischen in-Memory-Analysen wird die Datenbank vollständig im Arbeitsspeicher gespeichert, was bedeutet, dass Sie ausreichend Arbeitsspeicher nicht nur geladen werden alle Daten, sondern auch zusätzliche Datenstrukturen, die zur Unterstützung von Abfragen erstellt haben, müssen.  
  
 In SQL Server 2016 überarbeitete DirectQuery hat weniger Einschränkungen als bisher und eine bessere Leistung. Durch das Nutzen der relationalen Back-End-Datenbank für die Speicherung und Ausführung von Abfragen ist das Erstellen eines großen tabellarischen Modells einfacher als bisher zu realisieren.  
  
 In der Vergangenheit befinden sich größten in der Produktion mehrdimensionalen, mit der Verarbeitung als auch das abfragearbeitsauslastungen unabhängig auf dedizierter Hardware, optimiert für den jeweiligen Zweck ausgeführt.  Tabellarische Datenbanken holen rasch auf, und neue Weiterentwicklungen bei DirectQuery helfen, die Lücke noch schneller zu schließen.  
  
 Für mehrdimensionale Verschiebung Datenspeicher und Abfrage ist die Ausführung über ROLAP möglich.   Rowsets können auf einem Abfrageserver im Cache zwischengespeichert werden, veraltete Rowsets können ausgelagert werden. Aufgrund der effizienten und ausgewogenen Nutzung von Arbeitsspeicher- und Datenträgerressourcen entscheiden sich Kunden häufig für mehrdimensionale Lösungen.  
  
 Unter Belastung ist davon auszugehen, dass die Kapazitätsanforderungen sowohl an den Datenträger als auch an den Arbeitsspeicher steigen, weil Daten von Analysis Services zwischengespeichert, gespeichert, durchsucht und abgefragt werden. Weitere Informationen zu Speicherauslagerungsoptionen finden Sie unter [Memory Properties](../analysis-services/server-properties/memory-properties.md)(Speichereigenschaften). Weitere Informationen zum Skalieren finden Sie unter [Hohe Verfügbarkeit und Skalierbarkeit in Analysis Services](../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md).  
  
 Power Pivot für Excel verfügt über eine künstliche Dateigrößenbeschränkung von 2 Gigabytes, damit in Power Pivot für Excel erstellte Arbeitsmappen in SharePoint hochgeladen werden können, da die Größe hochgeladener Dateien auf dieser Plattform beschränkt ist. Einer der Hauptgründe, warum eine Power Pivot-Arbeitsmappe zu einer tabellarischen Lösung auf einer eigenständigen Analysis Services-Instanz migriert werden sollte, liegt darin, dass die Beschränkung der Dateigröße auf diesem Weg umgangen werden kann. Weitere Informationen zum Konfigurieren der maximalen Dateiuploadgröße finden Sie unter [Konfigurieren der maximalen Dateiuploadgröße &#40;PowerPivot für SharePoint&#41;](../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
 **Unterstützte Datenquellen**  
  
 Tabellarische Modelle sind in der Lage, Daten aus relationalen Datenquellen, Datenfeeds und einigen Dokumentformaten zu importieren. Sie können auch OLE DB für ODBC-Anbieter mit tabellarischen Modellen verwenden. Tabellarische Modelle mit Kompatibilitätsgrad 1400 bieten einen beträchtlichen Anstieg der Vielzahl von Datenquellen, die aus denen Sie von importieren können. Dies ist aufgrund der Einführung der moderne abrufen Daten Daten Abfragen und-Importfunktionen in SSDT unter Verwendung der Formel Abfragesprache M.   

  Mehrdimensionale Lösungen sind in der Lage, Daten mit nativen und verwalteten OLE DB-Anbietern aus relationalen Datenquellen zu importieren.  
  
 Die Liste externer Datenquellen, die in jedes Modell importiert werden können, finden Sie in den folgenden Themen:  
  
-   [Unterstützte Datenquellen](../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  

-   [Unterstützte Datenquellen &#40;SSAS – Mehrdimensional&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  

  
##  <a name="bkmk_lang"></a> Unterstützung für Abfrage und Skriptsprache  
 Analysis Services schließen MDX, DMX, DAX, XML/A, ASSL und TMSL ein. Die Unterstützung für diese Sprachen kann je nach Modelltyp variieren. Wenn Anforderungen für die Abfrage und Skriptsprache in Betracht kommen, überprüfen Sie die folgende Liste.  

-   Tabellarische Modelldatenbanken unterstützen DAX-Berechnungen, DAX-Abfragen und MDX-Abfragen. Dies gilt für alle Kompatibilitätsgrade. Skriptsprachen sind ASSL (über XMLA) für die Kompatibilitätsgrade 1050-1103 und TMSL (über XMLA) für den Kompatibilitätsgrad 1200 oder höher. 

-   PowerPivot-Arbeitsmappen verwenden DAX für Berechnungen und DAX oder MDX für Abfragen.  
  
-   Mehrdimensionale modelldatenbanken unterstützen MDX-Berechnungen, MDX-Abfragen, DAX-Abfragen und ASSL. 
  
-   Data Mining-Modelle unterstützen DMX und ASSL.  
  
-   Analysis Services PowerShell wird für tabellarische und mehrdimensionale Modelle und Datenbanken unterstützt.  
  
 Alle Datenbanken unterstützen XML/A. Unter [Abfragen- und Ausdruckssprachreferenz &#40;Analysis Services&#41;](http://msdn.microsoft.com/library/9597533d-35f4-4742-9d8c-7af392163527) und [Entwicklerhandbuch (Analysis Services)](../analysis-services/analysis-services-developer-documentation.md) finden Sie weitere Informationen.  
  
##  <a name="bkmk_sec"></a> Sicherheitsfeatures  
 Alle Analysis Services-Projektmappen können auf Datenbankebene gesichert werden. Präzisere Sicherheitsoptionen variieren je nach Modus. Wenn präzise Sicherheitseinstellungen für die Projektmappe erforderlich sind, überprüfen Sie die folgende Liste, um sicherzustellen, dass die Sicherheitsstufe, die Sie möchten, für den zu erstellenden Projektmappentyp unterstützt wird:  

  
-   Tabellarische modelldatenbanken können Sicherheit auf Zeilenebene mit rollenbasierten Berechtigungen verwenden.  
  
-   Mehrdimensionale modelldatenbanken können Dimension und die Sicherheit auf Zellenebene mit rollenbasierten Berechtigungen verwendet.  

-   [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] -Arbeitsmappen werden mit SharePoint-Berechtigungen auf Dateiebene gesichert.  
  
 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] -Arbeitsmappen können für einen Server im tabellarischen Modus wiederhergestellt werden. Nachdem die Datei wiederhergestellt wurde, wird diese von SharePoint, und Sie können alle tabellarischen Modellierungsfunktionen, einschließlich Sicherheit auf Zeilenebene verwenden entkoppelt.  
  
##  <a name="bkmk_designer"></a> -Entwurftools  
 Fähigkeiten zur Datenmodellierung und technische Kenntnisse können unter Benutzern, die mit dem Erstellen von analytischen Modellen beauftragt sind, stark variieren. Wenn die Vertrautheit mit dem Tool oder Anwender-Know-How eine für die Projektmappe in Betracht kommt, vergleichen Sie die folgenden Erfahrungen für die Modellerstellung.  
  
|Modellierungstool|Verwendung|  
|-------------------|--------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Verwenden Sie zum Erstellen von tabellarischen, mehrdimensionalen und Datamining-Lösungen. Diese Erstellungsumgebung stellt Arbeitsbereiche, Eigenschaftenbereiche und Objektnavigation mithilfe von Visual Studio Shell bereit. Technisch versierte Benutzer, die bereits Visual Studio verwenden, ziehen höchstwahrscheinlich dieses Tool zum Erstellen von Business Intelligence-Anwendungen vor.|  
|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für Excel|Verwenden Sie diese Funktion, um eine [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] -Arbeitsmappe zu erstellen, die Sie später in einer SharePoint-Farm bereitstellen, die über eine Installation von [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für SharePoint verfügt. [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für Excel hat einen separaten Anwendungsarbeitsbereich, der über Excel geöffnet wird. Es werden die gleichen visuellen Metaphern (Seiten im Registerkartenformat, Rasterlayout und Bearbeitungsleiste) wie in Excel verwendet. Benutzer, die in Excel versiert sind, werden dieses Tool gegenüber [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]bevorzugen.|  
  
##  <a name="bkmk_client"></a> Unterstützung für Clientanwendungen  
 Im Allgemeinen, tabellarische und mehrdimensionale Lösungen unterstützen Clientanwendungen, die mit einem oder mehreren der Analysis Services-Clientbibliotheken (MSOLAP, AMOMD, ADOMD). Z. B. Excel, Power BI Desktop und benutzerdefinierten Anwendungen.   
 
 Wenn Sie Reporting Services verwenden, variiert die Verfügbarkeit der Berichtsfunktion je nach Edition und Servermodus. Aus diesem Grund kann sich der zu erstellende Berichtstyp auf den zu installierenden Servermodus auswirken.  
  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], ein neues Reporting Services-Erstellungstool, das in SharePoint ausgeführt wird, ist auf einem Berichtsserver verfügbar, der in einer SharePoint 2010-Farm bereitgestellt wird. Der einzige Datenquellentyp, der mit diesem Bericht verwendet werden kann, ist eine tabellarische Analysis Services-Modelldatenbank oder eine [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] -Arbeitsmappe. Dies bedeutet, dass Sie über einen Server im tabellarischen Modus oder einen [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für SharePoint-Server verfügen müssen, damit die von diesem Berichtstyp verwendete Datenquelle gehostet wird. Sie können kein mehrdimensionales Modell als Datenquelle für einen [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] -Bericht verwenden. Sie müssen eine [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] BI-Semantikmodellverbindung oder eine freigegebene Reporting Services-Datenquelle erstellen, die als Datenquelle für einen [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] -Bericht verwendet wird.  
  
 Beliebige Analysis Services-Datenbanken können vom Berichts-Generator und Berichts-Designer verwendet werden, einschließlich [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] -Arbeitsmappen, die in [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für SharePoint gehostet werden.  
  
 Excel-PivotTable-Berichte werden von allen Analysis Services-Datenbanken unterstützt. Die Excel-Funktionalität ist unabhängig davon identisch, ob Sie eine tabellarische Datenbank, eine mehrdimensionale Datenbank oder eine [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] -Arbeitsmappe verwenden, obwohl das Rückschreiben nur für mehrdimensionale Datenbanken unterstützt wird.  
 
  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services-Instanzverwaltung](../analysis-services/instances/analysis-services-instance-management.md)   
 [Neuigkeiten in Analysis Services](../analysis-services/what-s-new-in-analysis-services.md)     

  
  
