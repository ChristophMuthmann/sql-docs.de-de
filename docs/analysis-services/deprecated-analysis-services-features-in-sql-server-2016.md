---
title: "Veraltete Analysis Services-Funktionen in SQL Server 2016 | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Analysis Services, Abwärtskompatibilität"
  - "SSAS, Abwärtskompatibilität"
  - "SQL Server Analysis Services, backward compatibility"
  - "Als veraltet markierte Funktionen [Analysis Services]"
ms.assetid: 2c96ecfe-a170-41d0-bee3-74503f880197
caps.latest.revision: 52
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 52
---
# Veraltete Analysis Services-Funktionen in SQL Server 2016
  Eine *veraltete Funktion* ist eine Funktion, die in einem zukünftigen Release aus dem Produkt ausgeschnitten wird, aber weiterhin im aktuellen Release unterstützt und eingeschlossen wird, um die Abwärtskompatibilität zu gewährleisten. In der Regel wird eine veraltete Version in einer Hauptversion entfernt (häufig innerhalb von zwei Releases nach der ursprünglichen Ankündigung). Beispielsweise werden als veraltet markierte Funktionen, die in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] angekündigt sind, wahrscheinlich nicht in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] unterstützt.  
  
 **Nicht unterstützt in der nächsten Hauptversion von SQL Server**  
  
|||  
|-|-|  
|**Kategorie**|**Funktion**|  
|Multidimensional|Remotepartitionen|  
|Multidimensional|Remoteverknüpfte Measuregruppen|  
|Multidimensional|Dimensionales Rückschreiben|  
|Multidimensional|Verknüpfte Dimensionen|  
  
 **Nicht unterstützt in einer zukünftigen Hauptversion von SQL Server**  
  
|||  
|-|-|  
|**Kategorie**|**Funktion**|  
|Multidimensional|SQL Server-Tabellenbenachrichtigungen für proaktives Zwischenspeichern.  <br />Der Ersatz erfolgt durch die Verwendung eines Abrufs für proaktives Zwischenspeichern. <br />Weitere Informationen finden Sie unter [Proaktives Zwischenspeichern &#40;Dimensionen&#41;](../analysis-services/multidimensional-models-olap-logical-dimension-objects/proactive-caching-dimensions.md) und [Proaktives Zwischenspeichern &#40;Partitionen&#41;](../Topic/Proactive%20Caching%20\(Partitions\).md).|  
|Multidimensional|Sitzungscubes. Es gibt keinen Ersatz.|  
|Multidimensional|Lokale Cubes Es gibt keinen Ersatz.|  
|Tabellarisch|Kompatibilitätsgrade für die Tabellenmodelle 1100 und 1103 werden in einer zukünftigen Version nicht unterstützt. Der Ersatz erfolgt durch die Festlegung von Modellen auf Kompatibilitätsebene 1200. Dabei werden die Modelldefinitionen zu tabellarischen Metadaten konvertiert. Weitere Informationen finden Sie unter [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).|  
|Tools|SQL Server Profiler für die Ablaufverfolgungssammlung<br /><br /> Der Ersatz verwendet den in SQL Server Management Studio eingebetteten Profiler für erweiterte Ereignisse.  <br /> Weitere Informationen finden Sie unter [Überwachen von Analysis Services mit den erweiterten Ereignissen von SQL Server](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).|  
|Tools|Server Profiler für die Ablaufverfolgungswiedergabe <br />Ersatz. Es gibt keinen Ersatz.|  
|Verwaltungsobjekte für die Ablaufverfolgung und Ablaufverfolgungs-APIs|Microsoft.AnalysisServices.Trace-Objekte (enthält die APIs für Analysis Services Ablauf-und Wiedergabeobjekte). Der Ersatz ist mehrteilig:<br /><br /> - Ablaufverfolgungskonfiguration: Microsoft.SqlServer.Management.XEvent<br />- Ablaufverfolgungslesevorgänge: Microsoft.SqlServer.XEvent.Linq<br />- Ablaufverfolgungswiedergabe: keine Angabe|  
  
> [!NOTE]  
>  Zuvor als veraltet markierte Ankündigungen von Funktionen aus [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] bleiben wirksam. Da der Code, der diese Funktionen unterstützt, noch nicht aus dem Produkt-entfernt wurde, sind viele dieser Funktionen in dieser Version weiterhin vorhanden. Obwohl auf zuvor als veraltet markierte Funktionen möglicherweise zugegriffen werden kann, gelten sie noch immer als veraltet und könnten zu jedem beliebigen Zeitpunkt zwischen der Veröffentlichung der [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]-Version und der Nachfolgeversion physisch aus dem Produkt gelöscht werden. Es wird dringend empfohlen, dass Sie keine als veraltet markierten Funktionen in neuen Modellen oder Anwendungen basierend auf [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] verwenden.  
  
## Siehe auch  
 [Analysis Services Backward Compatibility](../analysis-services/analysis-services-backward-compatibility.md)   
 [Nicht mehr unterstützte Analysis Services-Funktionalität in SQL Server 2016](../analysis-services/discontinued-analysis-services-functionality-in-sql-server-2016.md)  
  
  