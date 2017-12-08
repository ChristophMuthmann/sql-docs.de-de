---
title: "Datenzugriff auf mehrdimensionale Modelle (Analysis Services – mehrdimensionale Daten) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSAS, data access interfaces
- objects [Analysis Services], data access interfaces
- Analysis Services data access interfaces
- data retrieval [Analysis Services]
- retrieving data
- metadata [Analysis Services]
- data access interfaces [Analysis Services]
- manipulating objects [Analysis Services]
- Analysis Services data access interfaces, about data access interfaces
ms.assetid: 46388efb-3c78-47a2-b5c9-5a69ff394d03
caps.latest.revision: "46"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: ff56655be72dd63160bcfdbdb27f3c2a978de367
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="multidimensional-model-data-access-analysis-services---multidimensional-data"></a>Datenzugriff auf mehrdimensionale Modelle (Analysis Services – mehrdimensionale Daten)
  Verwenden Sie die Informationen in diesem Thema, um zu erfahren, wie mit programmgesteuerten Methoden, Skript oder Clientanwendungen, die integrierten Support für das Herstellen einer Verbindung zu einem [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Server in Ihrem Netzwerk enthalten, auf mehrdimensionale [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Daten zugegriffen wird.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Clientanwendungen](#bkmk_clientapps)  
  
 [Abfragesprachen](#bkmk_querylang)  
  
 [Befehlsorientierte Benutzerschnittstellen](#bkmk_api)  
  
##  <a name="bkmk_clientapps"></a> Clientanwendungen  
 Obwohl Analysis Services Schnittstellen bieten, mit denen Sie mehrdimensionale Datenbanken programmgesteuert erstellen oder integrieren können, ist es ein gängigerer Ansatz, vorhandene Clientanwendungen von Microsoft und anderen Softwareanbietern zu verwenden, die über integrierten Datenzugriff auf Analysis Services-Daten verfügen.  
  
 Die folgenden Microsoft-Anwendungen unterstützen systemeigene Verbindungen zu mehrdimensionalen Daten.  
  
### <a name="excel"></a>Excel  
 Mehrdimensionale Analysis Services-Daten werden oft mit PivotTables und PivotChart-Steuerelementen in einer Excel-Arbeitsmappe präsentiert. PivotTables passen zu mehrdimensionalen Daten, da die Hierarchien, Aggregationen und Navigationskonstrukte im Modell gut zu den Datenzusammenfassungsfunktionen einer PivotTable passen. Ein Analysis Services-OLE DB-Datenanbieter ist in einer Excel-Installation enthalten, um das Einrichten von Datenverbindungen zu vereinfachen. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit oder Importieren von Daten aus SQL Server Analysis Services](http://go.microsoft.com/fwlink/?linkID=215150).  
  
### <a name="reporting-services-reports"></a>Reporting Services-Berichte  
 Sie können Berichte, die Analysis Services-Datenbanken nutzen, die analytische Daten enthalten, mithilfe des Berichts-Generators oder des Berichts-Designers erstellen. Sowohl Berichts-Generator als auch Berichts-Designer enthalten einen MDX-Abfrage-Designer, den Sie zum Eingeben oder Entwerfen von MDX-Anweisungen verwenden können, die Daten aus einer verfügbaren Datenquelle abrufen. Weitere Informationen finden Sie unter [Von Reporting Services unterstützte Datenquellen &#40;SSRS&#41;](../../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) und unter [Analysis Services-Verbindungstyp für MDX &#40;SSRS&#41;](../../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md).  
  
### <a name="performancepoint-dashboards"></a>PerformancePoint-Dashboards  
 PerformancePoint-Dashboards werden verwendet, um Scorecards in SharePoint zu erstellen, die Geschäftsleistung verglichen mit vordefinierten Maßnahmen übermitteln. PerformancePoint bietet Unterstützung für Datenverbindungen zu mehrdimensionalen Analysis Services-Daten. Weitere Informationen finden Sie unter [Erstellen einer Analysis Services-Datenverbindung (PerformancePoint Services)](http://go.microsoft.com/fwlink/?linkid=232471).  
  
### <a name="sql-server-data-tools"></a>SQL Server Data Tools  
 Modell- und Berichts-Designer erstellen Lösungen, die mehrdimensionale Modelle enthalten, mithilfe von SQL Server Data Tools. Durch die Bereitstellung der Lösung in einer Analysis Services-Instanz wird die Datenbank erstellt, mit der Sie anschließend von Excel, Reporting Services und anderen Business Intelligence-Clientanwendungen ausgehend Verbindungen herstellen.  
  
 SQL Server Data Tools werden auf einer Visual Studio-Shell erstellt und verwenden Projekte, die organisiert werden und das Modell enthalten. Weitere Informationen finden Sie unter [Erstellen mehrdimensionaler Modelle mit SQL Server Data Tools &#40;SSDT&#41;](../../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md).  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 Für Datenbankadministratoren ist SQL Server Management Studio eine integrierte Umgebung zum Verwalten der SQL Server-Instanzen, einschließlich Instanzen von Analysis Services und mehrdimensionalen Datenbanken. Weitere Informationen finden Sie im Artikel über [SQL Server Management Studio](http://msdn.microsoft.com/library/66a6b7b1-de6a-4161-82bd-98ded486947b) und unter [Verbindung mit Analysis Services herstellen](../../../analysis-services/instances/connect-to-analysis-services.md).  
  
##  <a name="bkmk_querylang"></a> Abfragesprachen  
 MDX ist eine Abfrage- und Berechnungssprache nach Branchenstandard, die zum Abrufen von Daten aus OLAP-Datenbanken verwendet wurden. In Analysis Services ist MDX die Abfragesprache, die zum Abrufen von Daten verwendet wird, aber auch Datendefinition und Datenbearbeitung unterstützt. MDX-Editoren werden in SQL Server Management Studio, Reporting Services und SQL Server Data Tools eingebaut. Sie können Ad-hoc-Anfragen oder wiederverwendbare Skripts mithilfe der MDX-Editoren erstellen, wenn der Datenvorgang wiederholbar ist.  
  
 Einige Tools und Anwendungen, z. B. Excel, fragen mithilfe von MDX-Konstrukten intern eine Analysis Services-Datenquelle ab. Sie können MDX auch programmgesteuert verwenden, indem Sie die MDX-Anweisung in eine XMLA-Ausführungs-Anforderung einschließen.  
  
 Die folgenden Links enthalten weitere Informationen über MDX:  
  
 [Abfragen von mehrdimensionalen Daten mit MDX](../../../analysis-services/multidimensional-models/mdx/querying-multidimensional-data-with-mdx.md)  
  
 [Schlüsselkonzepte in MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
 [Grundlegendes zu MDX-Abfragen &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
 [Grundlegendes zu MDX-Skripts &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
##  <a name="bkmk_api"></a> Befehlsorientierte Benutzerschnittstellen  
 Wenn Sie eine benutzerdefinierte Anwendung erstellen, die mehrdimensionale Daten verwendet, wird der Ansatz zum Aufrufen der Daten wahrscheinlich in eine der folgenden Kategorien fallen:  
  
-   **XMLA**. Verwenden Sie XMLA, wenn Kompatibilität mit einer Vielzahl von Betriebssystemen und Protokollen erforderlich ist. XMLA bietet die größte Flexibilität, aber oft auf Kosten einer verbesserten Leistung und der Programmierbarkeit.  
  
-   **Clientbibliotheken**. Verwenden Sie Analysis Services-Clientbibliotheken, wie z. B. ADOMD.NET, AMO und OLE DB, wenn Sie programmgesteuert auf Daten von Clientanwendungen zugreifen, die unter einem Microsoft Windows-Betriebssystem ausgeführt werden. Die Clientbibliotheken umschließen XMLA mit einem Objektmodell und Optimierungen, die bessere Leistung ermöglichen.  
  
     ADOMD.NET- und AMO-Clientbibliotheken sind für in verwaltetem Code geschriebene Anwendungen vorgesehen. Verwenden Sie OLE DB für Analysis Services, wenn die Anwendung in systemeigenen Code geschrieben ist.  
  
 Die folgende Tabelle enthält weitere Details und Links zu den Clientbibliotheken, die zum Verbinden von Analysis Services mit einer benutzerdefinierten Anwendung verwendet werden.  
  
|Schnittstelle|Description|  
|---------------|-----------------|  
|Analysis Services Management Objects (AMO)|AMO ist das primäre Objektmodell zum Verwalten von Analysis Services-Instanzen und mehrdimensionalen Datenbanken in Code. SQL Server Management Studio beispielsweise verwendet AMO zur Unterstützung von Server- und Datenbankverwaltung. Weitere Informationen finden Sie unter [Entwickeln mit Analysis Management Objects &#40;AMO&#41;](../../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md).|  
|ADOMD.NET|ADOMD.NET ist das primäre Objektmodell, das mehrdimensionale Daten in benutzerdefinierten Anwendungen erstellt und aufruft. Sie können ADOMD.NET in einer verwalteten Clientanwendung verwenden, um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Informationen mithilfe der Schnittstellen für den Microsoft .NET Framework-Datenzugriff abzurufen. Weitere Informationen finden Sie unter [Entwickeln mit ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md) und [ADOMD.NET Client-Programmierung](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md).|  
|Analysis Services OLE DB-Anbieter (MSOLAP.dll)|Sie können den systemeigenen OLE DB-Anbieter zum programmgesteuerten Aufrufen von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] von einer nicht verwalteten API verwenden. Weitere Informationen finden Sie unter [OLE DB-Anbieter für Analysis Services &#40; Analysis Services – Mehrdimensionale Data&#41;](http://msdn.microsoft.com/library/cdeecd50-1d91-4162-a4a2-01c7799b02a8).|  
|Schemarowsets|Schemarowsettabellen sind Datenstrukturen, die beschreibende Informationen zu einem mehrdimensionalen Modell, das auf dem Server bereitgestellt wird, sowie Informationen zur aktuellen Aktivität auf dem Server enthalten. Als Programmierer können Sie Schemarowsettabellen in Clientanwendungen abfragen, um Metadaten, die auf einer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Instanz gespeichert sind, zu untersuchen und Unterstützungs- und Überwachungsinformationen abzurufen. Sie können Schemarowsets mit diesen programmgesteuerten Schnittstellen verwenden: OLE DB, OLE DB für Analysis Services, OLE DB für Data Mining oder XMLA. Weitere Informationen finden Sie unter [Analysis Services-Schemarowsets](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md).<br /><br /> Die folgende Liste erläutert mehrere Ansätze zum Verwenden von Schemarowsets:<br /><br /> –Führen Sie DMV-Abfragen in SQL Server Management Studio oder benutzerdefinierten Berichten aus, um mithilfe der SQL-Syntax auf Schemarowsets zuzugreifen. Weitere Informationen finden Sie unter [Verwenden von dynamischen Verwaltungssichten &#40;DMVs&#41; zum Überwachen von Analysis Services](../../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md).<br /><br /> –Schreiben Sie ADOMD.NET-Code, mit dem ein Schemarowset aufgerufen wird.<br /><br /> –Führen Sie die XMLA-Methode **Discover**direkt an einer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]Instanz aus, um Schemarowsetinformationen abzurufen. Weitere Informationen finden Sie unter [Discover-Methode &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-methods-discover.md).|  
|XMLA|XMLA ist die niedrigste Ebene, die einem Analysis Services-Programmierer zur Verfügung steht, und der gemeinsame Nenner, der allen Analysis Services-Datenzugriffsmethoden zugrunde liegt. XMLA ist ein dem Branchenstandard entsprechendes, SOAP-basiertes XML-Protokoll, das über eine HTTP-Verbindung universellen Datenzugriff auf sämtliche standardmäßigen mehrdimensionalen Datenquellen unterstützt. Dabei werden mithilfe von SOAP Anforderungen und Antworten für mehrdimensionale Daten formuliert. Wenn die Anwendung auf einer Nicht-Windows-Plattform ausgeführt wird, können Sie mithilfe von XMLA auf eine mehrdimensionale Datenbank zugreifen, die unter einem Windows-Server in Ihrem Netzwerk ausgeführt wird. Weitere Informationen finden Sie unter [Entwickeln mit XMLA in Analysis Services](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md).|  
|ASSL (Analysis Services Scripting Language)|ASSL ist ein beschreibender Begriff, der auf Analysis Services-Erweiterungen des XMLA-Protokolls zutrifft. Während die Execute- und die Discover-Methode vom XMLA-Protokoll beschrieben werden, fügt ASSL die folgende Funktion hinzu:<br /><br /> –XMLA-Skript<br /><br /> –XMLA-Objektdefinitionen<br /><br /> –XMLA-Befehle<br /><br /> Mit ASSL-Erweiterungen können Analysis Services XMLA-Konstrukte jenseits der grundlegenden Bereitstellungen des Protokolls verwenden und fügen die Unterstützung von Datendefinitionen, Datenbearbeitungen und Datensteuerelementen hinzu. Weitere Informationen finden Sie unter [Entwickeln mit Analysis Services Scripting Language &#40;ASSL&#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [Verbindung mit Analysis Services herstellen](../../../analysis-services/instances/connect-to-analysis-services.md)   
 [Entwickeln mit Analysis Services Scripting Language &#40; ASSL &#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Entwickeln mit XMLA in Analysis Services](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [Zugriff auf Daten im tabellarischen Modell](../../../analysis-services/tabular-models/tabular-model-data-access.md)  
  
  
