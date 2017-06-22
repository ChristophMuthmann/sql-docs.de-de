---
title: "Hinzufügen von Messgeräten mobile Berichte | Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76d8fc8f-c37f-44d3-ab44-45fbeed4e064
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ec1f4cee1318947e3c1ab730b3e4f7eaa16dd333
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="add-gauges-to-mobile-reports--reporting-services"></a>Hinzufügen von Messgeräten zu mobilen Berichten | Reporting Services
Messgeräte sind die grundlegendsten und häufig genutzten visuellen Elemente in mobilen Berichten. Sie zeigen einen einzelnen Wert in einem Dataset an – lediglich den Wert, oder den Wert im Vergleich mit einem Ziel.

![PBI_SSMRP_Gauges](../../reporting-services/mobile-reports/media/pbi-ssmrp-gauges.png)  
  
*Messgerätvisualisierungen in der Registerkarte „Layout“*  
  
Alle Messgeräte im SQL Server Mobile Report Publisher haben mindestens eine Eigenschaft gemeinsam: main, auf ein numerisches Feld in einer der Datentabellen im mobilen Bericht festgelegten Wert.  

Alle Messgeräte außer „Zahl“ können auch einen Vergleich bzw. *Deltawert*anzeigen –die Beziehung zwischen dem Haupt- und einem Vergleichswert. Der Vergleichswert ist oft das Ziel, und das Messgerät ist eine visuelle Anzeige des Status dieses Ziels oder der Differenz zwischen tatsächlichem Wert und Ziel.

Messgeräte können nur einen aggregierten Wert für ihren Hauptwert und einen aggregierten Wert für ihren Vergleichswert darstellen. Messgerätaggregationen sind standardisiert –Summe, Mittelwert, Minimum, Maximum usw. Standardmäßig ist der Anzeigewert eine Summe. Damit wird die Summe aller Werte innerhalb der aktuellen gefilterten Daten angezeigt, die für das Messgerätsteuerelement verfügbar sind. 

Sie können Anzeigewerte filtern, indem Sie sie mit den Navigatoren des mobilen Berichts verbinden. 

## <a name="set-the-main-and-comparison-values-for-a-gauge"></a>Festlegen des Haupt- und Vergleichswerts für ein Messgerät

1. Ziehen Sie von der Registerkarte **Layout** ein Messgerät in den Entwurfsbereich, und stellen Sie es auf die gewünschte Größe ein.

2. Rufen Sie [Daten aus Excel oder einem freigegebenen Dataset](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)ab.

3. Wählen Sie die Registerkarte **Daten** und im Bereich **Dateneigenschaften** unter **Hauptwert** eine Datentabelle und ein numerisches Feld aus.

3. Wählen Sie bei einem beliebigen Messgerät außer „Zahl“ im Bereich **Dateneigenschaften** unter **Vergleichswert** eine Datentabelle und ein numerisches Feld aus.

4. [optional] Wählen Sie zum Ändern der Aggregation **Optionen** und eine andere Aggregation aus.
   
   >**Hinweis**: Wenn Sie die Aggregation für den Hauptwert ändern, möchten Sie wahrscheinlich auch die Aggregation für den Vergleichswert ändern, obwohl Sie in einigen Fällen vielleicht Aggregationsmethoden kombinieren möchten.  

## <a name="filter-a-gauge"></a>Filtern eines Messgeräts
  
Wenn der mobile Bericht über Navigatoren verfügt, können Sie ein Messgerät zum Filtern an einen oder mehrere binden. Sie können Wert und Vergleichswert eines Messgeräts an einen oder mehrere verschiedene Navigatoren binden, sodass nahezu beliebig viele Optionen für Messgeräte verfügbar sind.  

1. Wählen Sie ein Messgerät, und wählen Sie auf der Registerkarte **Daten** im Bereich **Dateneigenschaften** **Optionen** neben **Hauptwert** oder **Vergleichswert**.

2. Wählen Sie unter „Gefiltert nach“ den Navigator, der das Messgerät filtern soll.

   ![mobile-report-gauge-navigator](../../reporting-services/mobile-reports/media/mobile-report-gauge-navigator.png)
 
## <a name="set-visual-properties-for-a-gauge"></a>Festlegen visueller Eigenschaften für ein Messgerät
  
Zusammen mit den Dateneigenschaften, die Messgerätelemente mit Datenfeldern verbinden, können Sie auch eine Reihe von funktionalen und visuellen Eigenschaften anpassen. 

### <a name="set-value-direction-high-or-low-is-better"></a>Festlegen der Wertrichtung: Höher oder niedriger ist besser
* Wählen Sie ein Messgerät, und legen Sie auf der Registerkarte **Layout** im Bereich **Eigenschaften visueller Elemente** für **Wertrichtung** entweder **Höhere Werte sind besser** oder **Niedrigere Werte sind besser**fest. 

**Höhere Werte sind besser** färbt höhere Werte grün, um eine erwünschte Änderung zum Besseren zu kennzeichnen, oder niedrigere Werte rot, um eine unerwünschte Änderung zum Schlechteren zu kennzeichnen. 

Bei **Niedrige Werte sind besser** werden die Farben umgekehrt verwendet.

Die Eigenschaft „Wertrichtung“ bezieht sich auf die Messgerätelemente, die einen Vergleichswert unterstützen. Die Farbe des Messgeräts wird durch das Vorzeichen der Deltaintegerzahl und die Einstellung der Eigenschaft „Wertrichtung“ bestimmt.  
  
### <a name="set-range-stops-for-a-gauge"></a>Festlegen von Bereichsabgrenzungen für ein Messgerät
Die zweite messgerätspezifische, datenunabhängige Eigenschaft sind Bereichsabgrenzungen. 

* Wählen Sie ein Messgerät, und wählen Sie auf der Registerkarte **Layout** im Bereich **Eigenschaften visueller Elemente** **Bereichsabgrenzungen**.

Mit Bereichsabgrenzungen legen Sie fest, welcher Prozentsatz der Vergleichswertvisualisierung als „Ziel erreicht“ (grün), „neutral“ (gelb) und „Ziel nicht erreicht“ (rot) dargestellt werden soll, wobei der Vergleichswert eines Messgeräts das Ziel ist. Auch hier unterstützen nur Messgeräte mit Vergleichswerten Bereichsabgrenzungen.  

### <a name="format-the-numbers-in-the-gauge"></a>Formatieren von Zahlen im Messgerät  
Eine andere datenunabhängige Eigenschaft des Messgerätelements, die von vielen anderen Elementen genutzt wird, ist das Zahlenformat. 

* Wählen Sie ein Messgerät, und wählen Sie auf der Registerkarte **Layout** im Bereich **Eigenschaften visueller Elemente** **Bereichsabgrenzungen**.

Damit wird bestimmt, wie im Messgerät angezeigte Zahlen formatiert werden – z.B. Währung, Prozentsatz, Uhrzeit oder allgemeine Werte. Sie legen Zahlenformate für jedes Element des mobilen Berichts fest.
  
### <a name="see-also"></a>Siehe auch 

* [Erstellen und Veröffentlichen von mobilen Berichten mit dem Publisher für mobile Berichte von SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
* [Karten in mobilen Reporting Services-Berichten](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Navigationen in mobilen Reporting Services-Berichten](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Visualisierungen in mobilen Reporting Services-Berichten](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Datenraster in mobilen Reporting Services-Berichten](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md) 

