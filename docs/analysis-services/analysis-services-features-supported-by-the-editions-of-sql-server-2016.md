---
title: "Analysis Services-Funktionen, die von den Editionen von SQLServer 2016 unterstützt | Microsoft Docs"
ms.custom: 
ms.date: 06/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
- analysis-services/multidimensional-tabular
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f09d7be1-bd63-43f8-b91c-bf19166b4457
caps.latest.revision: 4
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 064715ecd2a47b3c6034deefb5281f2745a601ae
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-features-supported-by-the-editions-of-sql-server-2016"></a>Analysis Services-Funktionen, die von den Editionen von SQLServer 2016 unterstützt werden
[!INCLUDE[ssas-appliesto-sql2016-later](../includes/ssas-appliesto-sql2016-later.md)]

Dieses Thema enthält Details zu Features, die von den verschiedenen Editionen von SQL Server 2016 Analysis Services unterstützt. Funktionen, die von den Evaluation- und Developer-Editionen unterstützt werden finden Sie in der Enterprise Edition.

## <a name="analysis-services-servers"></a>Analysis Services (Server)
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Skalierbare, freigegebene Datenbanken|ja||||||ja|  
|Sichern/Wiederherstellen und Anfügen/Trennen von Datenbanken|ja|ja|||||ja|  
|Synchronisieren von Datenbanken|ja||||||ja|  
|Always On-Failoverclusterinstanzen|ja<br /><br /> Anzahl der Knoten ist das Maximum des Betriebssystems|ja<br /><br /> Unterstützung für 2 Knoten|||||ja<br /><br /> Anzahl der Knoten ist das Maximum des Betriebssystems|  
|Programmierbarkeit (AMO, ADOMD.NET, OLEDB, XML/A, ASSL, TMSL)|ja|ja|||||ja|  
  
## <a name="tabular-models"></a>Tabellarische Modelle 
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Hierarchien|ja|ja|||||ja|  
|KPIs (Key Performance Indicators)|ja|ja|||||ja|  
|Perspektiven|ja||||||ja|  
|Übersetzungen|ja|ja|||||ja|  
|DAX-Berechnungen, DAX-Abfragen, MDX-Abfragen|ja|ja|||||ja|  
|Sicherheit auf Zeilenebene|ja|ja|||||ja|  
|Mehrere Partitionen|ja||||||ja|  
|InMemory-Speichermodus|ja|ja|||||ja|  
|DirectQuery-Speichermodus|ja||||||ja|  

## <a name="multidimensional-models"></a>Mehrdimensionale Modelle 
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Semiadditive Measures|ja|Nein <sup>1</sup>|||||ja|  
|Hierarchien|ja|ja|||||ja|  
|KPIs (Key Performance Indicators)|ja|ja|||||ja|  
|Perspektiven|ja||||||ja|  
|Aktionen|ja|ja|||||ja|  
|Kontointelligenz|ja|ja|||||ja|  
|Zeitintelligenz|ja|ja|||||ja|  
|Benutzerdefinierte Rollups|ja|ja|||||ja|  
|Cube-Rückschreiben|ja|ja|||||ja|  
|Rückschreiben von Dimensionen|ja||||||ja|  
|Rückschreibezellen|ja|ja|||||ja|  
|Drillthrough ausführen|ja|ja|||||ja|  
|Erweiterte Hierarchietypen (Übergeordnet-Untergeordnet- und unregelmäßige Hierarchien)|ja|ja|||||ja|  
|Erweiterte Dimensionen (Bezugsdimensionen, m:n-Dimensionen)|ja|ja|||||ja|  
|Verknüpfte Measures und Dimensionen|ja|Ja  <sup>2</sup> |||||ja|  
|Übersetzungen|ja|ja|||||ja|  
|Aggregationen|ja|ja|||||ja|  
|Mehrere Partitionen|ja|Ja, bis zu 3|||||ja|  
|Proaktives Zwischenspeichern|ja||||||ja|  
|Benutzerdefinierte Assemblys (gespeicherte Prozeduren)|ja|ja|||||ja|  
|MDX-Abfragen und Skripts|ja|ja|||||ja|  
|DAX-Abfragen|ja|ja|||||ja|  
|Rollenbasiertes Sicherheitsmodell|ja|ja|||||ja|  
|Sicherheit auf Dimensions- und Zellenebene|ja|ja|||||ja|  
|Skalierbarer Zeichenfolgenspeicher|ja|ja|||||ja|  
|MOLAP-, ROLAP- und HOLAP-Speichermodelle|ja|ja|||||ja|  
|Binärer und komprimierter XML-Transport|ja|ja|||||ja|  
|Pushmodus-Verarbeitung|ja||||||ja|  
|Direktes Rückschreiben|ja||||||ja|  
|Measureausdrücke|ja||||||ja|  
  
 <sup>1</sup> Das semiadditive LastChild-Measure wird in der Standard Edition unterstützt, während andere semiadditive Measures, z. B. None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren und ByAccount, nicht unterstützt werden. Additive Measures, z. B. Sum, Count, Min, Max und nicht additive Measures (DistinctCount) werden in allen Editionen unterstützt.  
  <sup>2</sup> standard Edition unterstützt Verknüpfen Measures und Dimensionen innerhalb derselben Datenbank, jedoch nicht von anderen Datenbanken oder Instanzen.
  
## <a name="power-pivot-for-sharepoint"></a>PowerPivot für SharePoint  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|SharePoint-Farmintegration auf Grundlage der Shared Services-Architektur|ja||||||ja|  
|Verwendungsberichte|ja||||||ja|  
|Systemüberwachungsregeln|ja||||||ja|  
|Power Pivot-Katalog|ja||||||ja|  
|PowerPivot-Datenaktualisierung|ja||||||ja|  
|Power Pivot-Datenfeeds|ja||||||ja|  
  
## <a name="data-mining"></a>Data Mining  
  
|Funktionsname|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Standardalgorithmen|ja|ja|||||ja|  
|Data Mining-Tools (Assistenten, Editoren, Abfrage-Generatoren)|ja|ja|||||ja|  
|Kreuzvalidierung|ja||||||ja|  
|Modelle für gefilterte Teilmengen von Daten der Miningstruktur|ja||||||ja|  
|Zeitreihen: benutzerdefinierte Kombination von ARTXP- und ARIMA-Methoden|ja||||||ja|  
|Zeitreihen: Vorhersage mit neuen Daten|ja||||||ja|  
|Unbegrenzte gleichzeitige Data Mining-Abfragen|ja||||||ja|  
|Erweiterte Konfigurations- und Optimierungsoptionen für Data Mining-Algorithmen|ja||||||ja|  
|Unterstützung für Plug-In-Algorithmen|ja||||||ja|  
|Parallele Modellverarbeitung|ja||||||ja|  
|Zeitreihen: reihenübergreifende Vorhersage|ja||||||ja|  
|Unbegrenzte Attribute für Zuordnungsregeln|ja||||||ja|  
|Sequenzvorhersage|ja||||||ja|  
|Mehrere Vorhersageziele für Naïve BaJa, neuronale Netzwerke und logistische Regression|ja||||||ja|  
  
 ## <a name="see-also"></a>Siehe auch  
 [Produktspezifikationen für SQL Server 2016](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [Installation für SQLServer 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)  



