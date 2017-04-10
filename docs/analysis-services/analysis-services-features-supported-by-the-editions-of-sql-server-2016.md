---
title: "Analysis Services-Funktionen, die von den Editionen von SQLServer 2016 unterst&#252;tzt werden | Microsoft Docs"
ms.custom: ""
ms.date: "09/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
  - "analysis-services/multidimensional-tabular"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f09d7be1-bd63-43f8-b91c-bf19166b4457
caps.latest.revision: 4
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 3
---
# Analysis Services-Funktionen, die von den Editionen von SQLServer 2016 unterst&#252;tzt werden
Dieses Thema bietet detaillierte Informationen zu den von verschiedenen [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]-Versionen unterstützten Funktionen.  
  
 SQL Server Evaluation Edition steht für einen Testzeitraum von 180 Tagen zur Verfügung.  
  
 Die neuesten Versionshinweise finden Sie unter [SQL Server 2016 Release Notes](../sql-server/sql-server-2016-release-notes.md). Die letzten Informationen zu Neuigkeiten finden Sie unter [Neuigkeiten in Analysis Services](../analysis-services/what-s-new-in-analysis-services.md).
    
 **SQL Server 2016 R2 ausprobieren!**    
    
 > [![Download aus dem Evaluation Center](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) Laden Sie SQL Server 2016 aus dem **[Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) herunter.**    
    
> ![Virtueller Azure-Computer (klein)](../analysis-services/media/azure-virtual-machine-small.png) **[Starten eines virtuellen Computers, auf dem SQL Server 2016 bereits installiert ist](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    
    
  
 Informationen über Funktionen, die von den Evaluation- und Developer-Editionen unterstützt werden, finden Sie unter „SQL Server Enterprise Edition“.
  
 Um zur Tabelle für eine SQL Server-Technologie zu navigieren, klicken Sie auf den zugehörigen Link: 
 
 -  [Analysis Services](#SSAS)  
  
-   [BI-Semantikmodell (mehrdimensional)](#BIMD)  
  
-   [BI-Semantikmodell (tabellarisch)](#BIT)  
  
-   [PowerPivot für SharePoint](#PPSP)  
  
-   [Data Mining](#DM)  
  
-   [Business Intelligence-Clients](#BIC)  

##  <a name="SSAS"></a> Analysis Services  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Skalierbare, freigegebene Datenbanken|ja||||||Ja|  
|Sichern/Wiederherstellen und Anfügen/Trennen von Datenbanken|Ja|Ja|||||ja|  
|Synchronisieren von Datenbanken|ja||||||ja|  
|AlwaysOn-Failoverclusterinstanzen|ja<br /><br /> Anzahl der Knoten ist das Maximum des Betriebssystems|ja<br /><br /> Unterstützung für 2 Knoten|||||ja<br /><br /> Anzahl der Knoten ist das Maximum des Betriebssystems|  
|Programmierbarkeit (AMO, ADOMD.NET, OLEDB, XML/A, ASSL, TMSL)|Ja|Ja|||||Ja|  
  
##  <a name="BIMD"></a> BI-Semantikmodell (mehrdimensional)  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Semiadditive Measures|Ja|Nein <sup>1</sup>|||||ja|  
|Hierarchien|ja|Ja|||||ja|  
|KPIs (Key Performance Indicators)|ja|Ja|||||ja|  
|Perspektiven|ja||||||ja|  
|Aktionen|ja|Ja|||||ja|  
|Kontointelligenz|ja|Ja|||||ja|  
|Zeitintelligenz|ja|Ja|||||ja|  
|Benutzerdefinierte Rollups|ja|Ja|||||ja|  
|Cube-Rückschreiben|ja|Ja|||||ja|  
|Rückschreiben von Dimensionen|ja||||||ja|  
|Rückschreibezellen|ja|Ja|||||ja|  
|Drillthrough ausführen|ja|Ja|||||Ja|  
|Erweiterte Hierarchietypen (Übergeordnet-Untergeordnet- und unregelmäßige Hierarchien)|Ja|Ja|||||Ja|  
|Erweiterte Dimensionen (Bezugsdimensionen, m:n-Dimensionen)|Ja|Ja|||||ja|  
|Verknüpfte Measures und Dimensionen|Ja|Ja <sup>2</sup> |||||Ja|  
|Übersetzungen|ja|Ja|||||ja|  
|Aggregationen|ja|Ja|||||ja|  
|Mehrere Partitionen|ja|Ja, bis zu 3|||||ja|  
|Proaktives Zwischenspeichern|ja||||||Ja|  
|Benutzerdefinierte Assemblys (gespeicherte Prozeduren)|Ja|Ja|||||ja|  
|MDX-Abfragen und Skripts|ja|Ja|||||ja|  
|DAX-Abfragen|ja|Ja|||||Ja|  
|Rollenbasiertes Sicherheitsmodell|Ja|Ja|||||Ja|  
|Sicherheit auf Dimensions- und Zellenebene|Ja|Ja|||||ja|  
|Skalierbarer Zeichenfolgenspeicher|ja|Ja|||||ja|  
|MOLAP-, ROLAP- und HOLAP-Speichermodelle|ja|Ja|||||ja|  
|Binärer und komprimierter XML-Transport|ja|Ja|||||Ja|  
|Pushmodus-Verarbeitung|Ja||||||ja|  
|Direktes Rückschreiben|ja||||||ja|  
|Measureausdrücke|ja||||||Ja|  
  
 <sup>1</sup> Das semiadditive LastChild-Measure wird in der Standard Edition unterstützt, während andere semiadditive Measures, z. B. None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren und ByAccount, nicht unterstützt werden. Additive Measures, z. B. Sum, Count, Min, Max und nicht additive Measures (DistinctCount) werden in allen Editionen unterstützt.  
  <sup>2</sup> Die Standard Edition unterstützt Verknüpfen von Measures und Dimensionen innerhalb derselben Datenbank, jedoch nicht aus anderen Datenbanken oder Instanzen.
   
##  <a name="BIT"></a> BI-Semantikmodell (tabellarisch)  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Hierarchien|ja|Ja|||||ja|  
|KPIs (Key Performance Indicators)|ja|Ja|||||ja|  
|Perspektiven|ja||||||ja|  
|Übersetzungen|ja|Ja|||||ja|  
|DAX-Berechnungen, DAX-Abfragen, MDX-Abfragen|ja|Ja|||||Ja|  
|Sicherheit auf Zeilenebene|Ja|Ja|||||ja|  
|Mehrere Partitionen|ja||||||Ja|  
|InMemory-Speichermodus|Ja|Ja|||||ja|  
|DirectQuery-Speichermodus|ja||||||ja|  
  
##  <a name="PPSP"></a> PowerPivot für SharePoint  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|SharePoint-Farmintegration auf Grundlage der Shared Services-Architektur|ja||||||ja|  
|Verwendungsberichte|ja||||||ja|  
|Systemüberwachungsregeln|ja||||||ja|  
|Power Pivot-Katalog|ja||||||ja|  
|PowerPivot-Datenaktualisierung|ja||||||ja|  
|Power Pivot-Datenfeeds|ja||||||ja|  
  
##  <a name="DM"></a> Data Mining  
  
|Funktionsname|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Standardalgorithmen|ja|Ja|||||Ja|  
|Data Mining-Tools (Assistenten, Editoren, Abfrage-Generatoren)|Ja|Ja|||||ja|  
|Kreuzvalidierung|ja||||||ja|  
|Modelle für gefilterte Teilmengen von Daten der Miningstruktur|ja||||||ja|  
|Zeitreihen: benutzerdefinierte Kombination von ARTXP- und ARIMA-Methoden|ja||||||ja|  
|Zeitreihen: Vorhersage mit neuen Daten|ja||||||ja|  
|Unbegrenzte gleichzeitige Data Mining-Abfragen|ja||||||ja|  
|Erweiterte Konfigurations- und Optimierungsoptionen für Data Mining-Algorithmen|ja||||||Ja|  
|Unterstützung für Plug-In-Algorithmen|Ja||||||ja|  
|Parallele Modellverarbeitung|ja||||||Ja|  
|Zeitreihen: reihenübergreifende Vorhersage|Ja||||||ja|  
|Unbegrenzte Attribute für Zuordnungsregeln|ja||||||ja|  
|Sequenzvorhersage|ja||||||ja|  
|Mehrere Vorhersageziele für Naïve BaJa, neuronale Netzwerke und logistische Regression|ja||||||Ja|  
  
##  <a name="BIC"></a> Business Intelligence-Clients  
 Die folgenden Softwareclientanwendungen sind im Microsoft Download Center verfügbar und bieten Unterstützung beim Erstellen von Business Intelligence-Dokumenten, die in einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz ausgeführt werden. Wenn Sie diese Dokumente in einer Serverumgebung hosten, verwenden Sie eine Edition von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], die diesen Dokumenttyp unterstützt. In der folgenden Tabelle wird dargestellt, welche [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Editionen die Serverfunktionen zum Hosten der in den Clientanwendungen erstellten Dokumente besitzen.  
  
|Name des Tools|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|---------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Data Mining-Add-Ins für Excel und Visio 2010 (.xlsx, .vsdx)|Ja|Ja|||||Ja|  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010 und 2013 (.xlsx)|Ja||||||Ja|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] (.xlsx)|Ja||||||Ja|  
  
> [!NOTE]  
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] ist ein Excel-Add-In zum Erstellen von Arbeitsmappen mit einem Datenmodell.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] hängt nicht von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ab, aber [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] ist für die Freigabe von sowie für die Zusammenarbeit an Excel-Arbeitsmappen mit einem Datenmodell in SharePoint erforderlich. Diese Funktion steht als Teil der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition zur Verfügung.  
>   
>      In Excel 2016 ist die Power Pivot-Funktion integriert, daher benötigen Sie das Power Pivot-Add-In nicht mehr.  
> 2.  In der oben aufgeführten Tabelle sind die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Editionen angegeben, die zur Aktivierung dieser Clienttools erforderlich sind. Über diese Tools kann jedoch auf Daten zugegriffen werden, die von beliebigen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Editionen gehostet werden.  
  
 ## Siehe auch  
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
 [Produktspezifikationen für SQL Server 2016](../Topic/Product%20Specifications%20for%20SQL%20Server%202016.md)   
 [Installation für SQLServer 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)  

