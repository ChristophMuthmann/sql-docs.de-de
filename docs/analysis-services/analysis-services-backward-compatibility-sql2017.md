---
title: "Abwärtskompatibilität von SQL Server 2017 Analysis Services | Microsoft Docs"
ms.date: 07/11/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: analysis-services
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
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 57a03d325a7415f08fd073ea805e022935f3fce7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
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
|Multidimensional|Data Mining|
|Multidimensional|Remoteverknüpfte Measuregruppen|
|Tabellarisch|Modelle mit Kompatibilitätsgrad 1100 und 1103|
|Tabellarisch|Eigenschaften von tabellarischen Objektmodell: Column.TableDetailPosition Column.IsDefaultLabel, Column.IsDefaultImage|


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
|Verwaltungsobjekte für die Ablaufverfolgung und Ablaufverfolgungs-APIs|Microsoft.AnalysisServices.Trace-Objekte (enthält die APIs für Analysis Services Ablauf-und Wiedergabeobjekte). Der Ersatz ist mehrteilig:<br /><br /> -Ablaufverfolgungskonfiguration: Microsoft.SqlServer.Management.XEvent<br />-Ablaufverfolgungslesevorgänge: Microsoft.SqlServer.XEvent.Linq<br />- Ablaufverfolgungswiedergabe: keine Angabe|  

## <a name="breaking-changes"></a>Wichtige Änderungen
Ein *unterbrechende Änderung* bewirkt, dass eine Funktion, Datenmodell, Anwendungscode oder Skript nicht mehr funktioniert nach dem Upgrade auf die aktuelle Version.

Es gibt keine aktuellen Änderungen in dieser Version.

## <a name="behavior-changes"></a>Verändertes Programmverhalten
Ein *verhaltensänderung* wirkt sich auf die gleiche Funktion wie in der aktuellen Version im Vergleich zu der vorherigen Version funktioniert. Es werden nur signifikantem Verhalten ändert sich beschrieben. Änderungen in der Benutzeroberfläche sind nicht eingeschlossen.

Änderungen an MDSCHEMA_MEASUREGROUP_DIMENSIONS und DISCOVER_CALC_DEPENDENCY, detaillierte, der [Neuigkeiten in SQL Server 2017 CTP-Version 2.1 für Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2017/05/18/whats-new-in-sql-server-2017-ctp-2-1-for-analysis-services/) Ankündigung.


## <a name="see-also"></a>Siehe auch
[Analysis Services, Abwärtskompatibilität (SQL Server 2016)](analysis-services-backward-compatibility.md)
