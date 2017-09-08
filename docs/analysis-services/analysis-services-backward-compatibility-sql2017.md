---
title: "Abwärtskompatibilität von SQL Server 2017 Analysis Services | Microsoft Docs"
ms.date: 07/11/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing Analysis Services, backward compatibility
- backward compatibility [Analysis Services]
- compatibility [Analysis Services]
- Analysis Services, backward compatibility
- upgrading Analysis Services
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
ms.assetid: 
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 972ab981eccb6271dfa2f18e0b482f43020ff36b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-backward-compatibility-sql-2017"></a>Analysis Services, Abwärtskompatibilität (2017 SQL)
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

Dieser Artikel beschreibt die Änderungen in der funktionsverfügbarkeit und -Verhalten zwischen der aktuellen Version und der vorherigen Version.

## <a name="deprecated-features"></a>Als veraltet markierte Funktionen
Ein *veraltete Funktion* wird nicht mehr in einer zukünftigen Version aus dem Produkt unterstützt werden, aber wird weiterhin unterstützt und in der aktuellen Version Abwärtskompatibilität enthalten. Es wird empfohlen, dass Sie unterbrechen als veraltet markierte Funktionen in neue und vorhandene Projekte verwenden, um Kompatibilität mit künftigen Freigaben zu gewährleisten.

Die folgenden Features sind in dieser Version veraltet:
  
|||  
|-|-|  
|**/ Eine Kategorie-Modus**|**Feature**|
|Tabellarisch|Remoteverknüpfte Measuregruppen|
|Tabellarisch|Modelle mit Kompatibilitätsgrad 1100 und 1103|
|Tabellarisch|Eigenschaften von tabellarischen Objektmodell: Column.TableDetailPosition Column.IsDefaultLabel, Column.IsDefaultImage|
|Multidimensional|Data Mining|

## <a name="discontinued-features"></a>Nicht mehr unterstützte Funktionen
Ein *nicht mehr unterstützte Funktion* wurde in einer früheren Version als veraltet markiert. Unter Umständen in der aktuellen Version enthalten sein, aber wird nicht mehr unterstützt. Nicht mehr unterstützte Funktionen entfernt werden vollständig in einer zukünftigen Version oder aktualisieren.

Die folgenden Features wurden in einer früheren Version als veraltet markiert und werden in dieser Version nicht mehr unterstützt.
  
|||  
|-|-|  
|**/ Eine Kategorie-Modus**|**Feature**|  
|Tabellarisch|VertipaqPagingPolicy Arbeitsspeicher-Eigenschaftswert (2), aktivieren die Auslagerung auf Datenträger unter Verwendung von Arbeitsspeicher Speicherabbilddateien.|
|Multidimensional|Remotepartitionen|  
|Multidimensional|Remoteverknüpfte Measuregruppen|  
|Multidimensional|Dimensionales Rückschreiben|  
|Multidimensional|Verknüpfte Dimensionen|
|Tools|SQL Server Profiler für die Ablaufverfolgungssammlung<br /><br /> Der Ersatz verwendet den in SQL Server Management Studio eingebetteten Profiler für erweiterte Ereignisse.  <br /> Weitere Informationen finden Sie unter [Überwachen von Analysis Services mit den erweiterten Ereignissen von SQL Server](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).|  
|Tools|Server Profiler für die Ablaufverfolgungswiedergabe <br />Ersatz. Es gibt keinen Ersatz.|  
|Verwaltungsobjekte für die Ablaufverfolgung und Ablaufverfolgungs-APIs|Microsoft.AnalysisServices.Trace-Objekte (enthält die APIs für Analysis Services Ablauf-und Wiedergabeobjekte). Der Ersatz ist mehrteilig:<br /><br /> - Ablaufverfolgungskonfiguration: Microsoft.SqlServer.Management.XEvent<br />- Ablaufverfolgungslesevorgänge: Microsoft.SqlServer.XEvent.Linq<br />- Ablaufverfolgungswiedergabe: keine Angabe|  

## <a name="breaking-changes"></a>Wichtige Änderungen
Ein *unterbrechende Änderung* bewirkt, dass eine Funktion, Datenmodell, Anwendungscode oder Skript nicht mehr funktioniert nach dem Upgrade auf die aktuelle Version.

Es gibt keine aktuellen Änderungen in dieser Version.

## <a name="behavior-changes"></a>Verändertes Programmverhalten
Ein *verhaltensänderung* wirkt sich auf die gleiche Funktion wie in der aktuellen Version im Vergleich zu der vorherigen Version funktioniert. Es werden nur signifikantem Verhalten ändert sich beschrieben. Änderungen in der Benutzeroberfläche sind nicht eingeschlossen.

Es sind keine verhaltensänderungen in dieser Version.


## <a name="see-also"></a>Siehe auch
[Analysis Services, Abwärtskompatibilität (SQL Server 2016)](analysis-services-backward-compatibility.md)
