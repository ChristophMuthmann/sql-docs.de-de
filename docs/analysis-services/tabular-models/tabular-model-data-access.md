---
title: Zugriff auf tabellarische Modelldaten | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6ae74a8b-0025-450d-94a5-4e601831d420
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 6b535c1eba06e7f023ef9a1f7b00476e7be39eb4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="tabular-model-data-access"></a>Zugriff auf Daten im tabellarischen Modell
  Auf tabellarische Modelldatenbanken in Analysis Services kann mit den meisten Clients, Schnittstellen und Sprachen zugegriffen werden, mit denen Sie auch Daten oder Metadaten aus einem mehrdimensionalen Modell abrufen. Weitere Informationen finden Sie unter [Datenzugriff auf mehrdimensionale Modelle &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md).  
  
 In diesem Thema werden die Clients, Abfragesprachen und befehlsorientierten Benutzerschnittstellen beschrieben, die mit tabellarischen Modellen verwendet werden können.  
  
## <a name="clients"></a>Clients  
 Die folgenden Microsoft-Clientanwendungen unterstützen systemeigene Verbindungen mit tabellarischen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Modelldatenbanken.  
  
### <a name="power-bi"></a>Power BI
Sie können eine Verbindung zu einer lokalen Datenbank für ein tabellarisches Analysis Services-Modell von [Power BI](https://powerbi.microsoft.com/)herstellen. Power BI ist eine Sammlung von Business Analytics-Tools zum Analysieren von Daten und zum Freigeben von Einblicken. 

### <a name="excel"></a>Excel  
 Sie können in Excel eine Verbindung mit tabellarischen Modelldatenbanken herstellen und die Datenvisualisierungs- und Analysefunktionen in Excel verwenden, um mit den Daten zu arbeiten. Um auf die Daten zuzugreifen, definieren Sie eine Analysis Services-Datenverbindung, geben einen Server an, der im tabellarischen Servermodus ausgeführt wird, und wählen dann die gewünschte Datenbank aus. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit oder Importieren von Daten aus SQL Server Analysis Services](http://go.microsoft.com/fwlink/?linkID=215150).  
  
 Excel ist auch die empfohlene Anwendung zum Durchsuchen von tabellarischen Modellen in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Das Tool beinhaltet eine Option **In Excel analysieren** , die eine neue Instanz von Excel startet, eine Excel-Arbeitsmappe erstellt und in der Arbeitsmappe eine Datenverbindung mit der Arbeitsbereichsdatenbank des Modells öffnet. Beim Durchsuchen von tabellarischen Modelldaten in Excel ist zu beachten, dass Excel Abfragen für das Modell mit dem Excel PivotTable-Client ausgibt. Entsprechend führen Vorgänge innerhalb der Excel-Arbeitsmappe zu MDX-Abfragen, die an die Arbeitsbereichsdatenbank gesendet werden. DAX-Abfragen werden nicht erstellt. Wenn Sie Abfragen mit SQL-Profiler oder einem anderen Überwachungstool überwachen, wird in der Profiler-Ablaufverfolgung voraussichtlich MDX angezeigt und nicht DAX. Weitere Informationen zur Funktion „In Excel analysieren“ finden Sie unter [In Excel analysieren &#40;SSAS Tabular&#41;](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
### <a name="power-view"></a>Power View  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] ist eine Reporting Services-Clientanwendung zur Berichtserstellung, die in einer SharePoint 2010-Umgebung ausgeführt wird. Sie kombiniert das Durchsuchen von Daten, den Abfrageentwurf und das Präsentationslayout in einer integrierten Ad-hoc-Berichtsumgebung. [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] kann tabellarische Modelle als Datenquellen verwenden, und zwar unabhängig davon, ob das Modell auf einer im tabellarischen Modus ausgeführten Analysis Services-Instanz gehostet wird oder Daten im DirectQuery-Modus aus einem relationalen Datenspeicher abgerufen werden. Um in [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]eine Verbindung mit einem tabellarischen Modell herzustellen, müssen Sie eine Verbindungsdatei erstellen, die den Serverspeicherort und den Datenbanknamen enthält. Sie können eine freigegebene Reporting Services-Datenquelle oder eine BI-Semantikmodell-Verbindungsdatei in SharePoint erstellen. Weitere Informationen zu BI-Semantikmodellverbindungen finden Sie unter [PowerPivot-BI-Semantikmodell-Verbindung &#40;.bism&#41;](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md).  
  
 Der [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] -Client bestimmt die Struktur des angegebenen Modells, indem er eine Anforderung an die angegebene Datenquelle sendet, die ein Schema zurückgibt, das vom Client verwendet werden kann, um Abfragen für das Modell als Datenquelle zu erstellen und Vorgänge auf Grundlage der Daten auszuführen. Nachfolgende Vorgänge in der [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] -Benutzeroberfläche, um Daten zu filtern, Berechnungen oder Aggregationen auszuführen und zugeordnete Daten anzuzeigen, werden vom Client gesteuert und können nicht programmgesteuert bearbeitet werden.  
  
 Die Abfragen, die vom [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] -Client an das Modell gesendet werden, werden als DAX-Anweisungen ausgegeben, die Sie überwachen können, indem Sie eine Ablaufverfolgung auf dem Modell festlegen.  Der Client gibt auch eine Anforderung an den Server für die ursprüngliche Schemadefinition aus, die entsprechend der konzeptionellen Schemadefinitionssprache (CSDL) präsentiert wird. Weitere Informationen finden Sie unter [CSDL-Anmerkungen für Business Intelligence &#40;CSDLBI&#41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 Mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] können Sie Instanzen verwalten, die tabellarische Modelle hosten, sowie die darin enthaltenen Metadaten und Daten abfragen. Sie können die Modelle oder die Objekte in einem Modell verarbeiten, Partitionen erstellen und verwalten sowie die Sicherheit festlegen, die zum Verwalten des Datenzugriffs verwendet werden kann. Weitere Informationen finden Sie in folgenden Themen:  
  
-   [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
-   [Verbindung mit Analysis Services herstellen](../../analysis-services/instances/connect-to-analysis-services.md)  
  
-   [Überwachen einer Instanz von Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
 Sie können die MDX- und XMLA-Abfragefenster in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwenden, um Daten und Metadaten aus einer tabellarischen Modelldatenbank abzurufen. Beachten Sie dabei jedoch folgende Einschränkungen:  
  
-   Anweisungen mit MDX und DMX werden nicht für Modelle unterstützt, die im DirectQuery-Modus bereitgestellt wurden. Wenn Sie für ein tabellarisches Modell im DirectQuery-Modus eine Abfrage erstellen müssen, sollten Sie stattdessen ein Fenster für die **XMLA-Abfrage** verwenden.  
  
-   Sie können den Datenbankkontext des XMLA-Abfragefensters nicht ändern, nachdem Sie das **Abfrage** fenster geöffnet haben. Wenn Sie eine Abfrage an eine andere Datenbank oder eine andere Instanz senden müssen, müssen Sie diese Datenbank oder Instanz mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] öffnen und ein neues Fenster für die **XMLA-Abfrage** innerhalb dieses Kontexts öffnen.  
  
 Sie können Ablaufverfolgungen für ein tabellarisches [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Modell erstellen, wie Sie es bei einer mehrdimensionalen Projektmappe tun würden. In dieser Version stellt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viele neue Ereignisse bereit, die verwendet werden können, um Speicherauslastung, Abfrage- und Verarbeitungsvorgänge und Dateiverwendung nachzuverfolgen. Weitere Informationen finden Sie unter [Analysis Services-Ablaufverfolgungsereignisse](../../analysis-services/trace-events/analysis-services-trace-events.md).  
  
> [!WARNING]  
>  Wenn Sie eine Ablaufverfolgung für eine tabellarische Modelldatenbank festlegen, könnten Sie einige Ereignisse sehen, die als DMX-Abfragen kategorisiert werden. Data Mining wird jedoch nicht für tabellarische Modelldaten unterstützt, und die in der Datenbank ausgeführten DMX-Abfragen sind auf SELECT-Anweisungen in den Modellmetadaten beschränkt. Die Ereignisse werden nur als DMX kategorisiert, da das gleiche Parserframework für MDX verwendet wird.  
  
## <a name="query-languages"></a>Abfragesprachen  
 Die tabellarischen Modelle von Analysis Services unterstützen die meisten Abfragesprachen, die für den Zugriff auf mehrdimensionale Modelle bereitgestellt werden. Die Ausnahme sind tabellarische Modelle, die im DirectQuery-Modus bereitgestellt wurden und keine Daten von einem Analysis Services-Datenspeicher abrufen, sondern Daten direkt von einer SQL Server-Datenquelle abrufen. Sie können diese Modelle nicht mit MDX abfragen. Die Verwendung eines Clients ist erforderlich, der die Konvertierung von DAX-Ausdrücken in Transact-SQL-Anweisungen unterstützt, z.B. der [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] -Client.  
  
### <a name="dax"></a>DAX  
 Sie können DAX zum Erstellen von Ausdrücken und Formeln für alle tabellarischen Modelltypen verwenden, unabhängig davon, ob das Modell auf SharePoint als eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-aktivierte Excel-Arbeitsmappe oder auf einer Instanz von Analysis Services gespeichert wird.  
  
 Sie können darüberhinaus Abfragen mithilfe von DAX-Ausdrücken innerhalb des Kontexts einer XMLA EXECUTE-Befehlsanweisung an ein tabellarisches Modell senden, das im DirectQuery-Modus bereitgestellt wurde.  
  
 Beispiele für Abfragen auf einem tabellarischen Modell mithilfe von DAX finden Sie in der [Syntaxreferenz für DAX-Abfragen](http://msdn.microsoft.com/en-us/4dd0cf0e-191d-411d-987c-f606813fc39e).  
  
### <a name="mdx"></a>MDX  
 Sie können Abfragen für tabellarische Modelle, die den speicherinternen Cache als bevorzugte Abfragemethode verwenden (Modelle, die nicht im DirectQuery-Modus bereitgestellt wurden), mithilfe von MDX erstellen. Obwohl Clients wie [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] DAX sowohl zum Erstellen von Aggregationen als auch zum Abfragen des Modells als Datenquelle verwenden, kann DAX, wenn Sie mit MDX vertraut sind, auch als Verknüpfung zum Erstellen von Beispielabfragen in MDX dienen (siehe [Erstellen von Measures in MDX](../../analysis-services/multidimensional-models/mdx/mdx-building-measures.md)).  
  
### <a name="csdl"></a>CSDL  
 Die konzeptionelle Schemadefinitionssprache ist an sich keine Abfragesprache, sie kann aber verwendet werden, um Informationen zum Modell und den Modellmetadaten abzurufen, die später verwendet werden können, um Berichte oder Abfragen für das Modell zu erstellen.  
  
 Informationen darüber, wie CSDL in tabellarischen Modellen verwendet wird, finden Sie unter [CSDL-Anmerkungen für Business Intelligence &#40;CSDLBI&#41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md).  
  
## <a name="programmatic-interfaces"></a>Befehlsorientierte Benutzerschnittstellen  
 Die Hauptschnittstellen, die zum Interagieren mit tabellarischen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Modellen verwendet werden, sind die Schemarowsets, XMLA- und Abfrageclients sowie Abfragetools, die von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]zur Verfügung gestellt werden.  
  
### <a name="data-and-metadata"></a>Daten und Metadaten  
 Sie können Daten und Metadaten von tabellarischen Modellen in verwalteten Anwendungen mit ADOMD.NET abrufen. 
  
-   [Verwenden von dynamischen Verwaltungssichten &#40;DMVs&#41; zum Überwachen von Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
 In nicht verwalteten Clientanwendungen können Sie den OLE DB-Anbieter für Analysis Services 9.0 zur Unterstützung des OLE DB-Zugriffs auf tabellarische Modelle verwenden. Eine aktualisierte Version des OLE DB-Anbieters für Analysis Services ist erforderlich, um den Zugriff auf tabellarische Modelle zu aktivieren. Weitere Informationen zu Anbietern, die mit tabellarischen Modellen verwendet werden, finden Sie unter [Installieren des OLE DB-Anbieters für Analysis Services auf SharePoint-Servern](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859) .  
  
 Sie können auch Daten aus einer Analysis Services-Instanz direkt im XML-basierten Format abrufen. Sie können das Schema des tabellarischen Modells mit dem DISCOVER_CSDL_METADATA-Rowset abrufen, oder Sie können einen EXECUTE- oder DISCOVER-Befehl mit vorhandenen ASSL-Elementen, -Objekten oder -Eigenschaften verwenden. Weitere Informationen finden Sie in den folgenden Ressourcen:  
  
-   [CSDL-Anmerkungen für Business Intelligence &#40;CSDLBI&#41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
### <a name="manipulate-analysis-services-objects"></a>Bearbeiten von Analysis Services-Objekten  
 Sie können tabellarische Modelle und darin enthaltene Objekte, einschließlich Tabellen, Spalten, Perspektiven, Measures und Partitionen, mit XMLA-Befehlen oder mit AMO erstellen, ändern, löschen und verarbeiten. Sowohl AMO als auch XMLA wurden aktualisiert, um zusätzliche Eigenschaften, die in tabellarischen Modellen zur verbesserten Berichterstellung und Modellierung verwendet werden, zu unterstützen.  
  
  
### <a name="schema-rowsets"></a>Schemarowsets  
 Clientanwendungen können die Schemarowsets verwenden, um die Metadaten von tabellarischen Modellen zu untersuchen und Unterstützungs- und Überwachungsinformationen vom [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server abzurufen. In dieser Version von SQL Server wurden neue Schemarowsets hinzugefügt und vorhandene Schemarowsets erweitert, um Funktionen zu unterstützen, die sich auf tabellarische Modelle beziehen und die Überwachung und Leistungsanalyse in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]optimieren.  
  
-   [DISCOVER_CALC_DEPENDENCY-Rowset](../../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md)  
  
     Neues Schemarowset zum Nachverfolgen von Abhängigkeiten in den Spalten und Verweisen in einem tabellarischen Modell  
  
-   [DISCOVER_CSDL_METADATA-Rowset](../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)  
  
     Neues Schemarowset zum Abrufen der CSDL-Darstellung eines tabellarischen Modells  
  
-   [DISCOVER_XEVENT_TRACE_DEFINITION-Rowset](http://msdn.microsoft.com/library/e1ce2d2d-f994-4318-801a-ee0385aecd84)  
  
     Neues Schemarowset zum Überwachen von erweiterten SQL Server-Ereignissen Weitere Informationen finden Sie unter [Überwachen von Analysis Services mit den erweiterten Ereignissen von SQL Server](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).  
  
-   [DISCOVER_TRACES-Rowset](../../analysis-services/schema-rowsets/xml/discover-traces-rowset.md)  
  
     Mit der neuen Spalte **Type** können Sie Ablaufverfolgungen nach Kategorie filtern. Weitere Informationen finden Sie unter [Erstellen von Profilerablaufverfolgungen für Replay &#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md).  
  
-   [MDSCHEMA_HIERARCHIES-Rowset](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)  
  
     Die neue **STRUCTURE_TYPE** -Enumeration unterstützt die Identifikation benutzerdefinierter Hierarchien, die in tabellarischen Modellen erstellt wurden. Weitere Informationen finden Sie unter [Hierarchien &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md).  
  
 Es gibt keine Updates zum OLE DB für Data Mining-Schemarowsets in dieser Version.  
  
> [!WARNING]  
>  Sie können MDX oder DMX-Abfragen nicht in einer Datenbank verwenden, die im DirectQuery-Modus bereitgestellt wurde. Wenn Sie in einem DirectQuery-Modell mithilfe des Schemarowsets eine Abfrage ausführen müssen, sollten Sie XMLA und nicht die zugeordnete DMV verwenden. Für DMVs, die Ergebnisse für den Server als Ganzes zurückgeben, z. B. SELECT * von $system.DBSCHEMA_CATALOGS oder DISCOVER_TRACES, können Sie die Abfrage im Inhalt einer Datenbank ausführen, die in einem Modus mit Zwischenspeicherung bereitgestellt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Herstellen einer Verbindung mit einer tabellarischen Modelldatenbank &#40;SSAS&#41;](../../analysis-services/tabular-models/connect-to-a-tabular-model-database-ssas.md)   
 [PowerPivot-Datenzugriff](../../analysis-services/power-pivot-sharepoint/power-pivot-data-access.md)   
 [Verbindung mit Analysis Services herstellen](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
