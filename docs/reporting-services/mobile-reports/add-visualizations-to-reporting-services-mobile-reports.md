---
title: "Hinzufügen von Visualisierungen zu mobilen Reporting Services-Berichten | Microsoft-Dokumentation"
ms.custom: 
ms.date: 09/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3b220b74-9ecd-4084-93fb-545208d5d7a2
caps.latest.revision: "15"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7c068430c44eaad1df894fc5c67849ff438ffcbc
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="add-visualizations-to-reporting-services-mobile-reports"></a>Hinzufügen von Visualisierungen zu mobilen Reporting Services-Berichten
Diagramme sind ein wesentlicher Bestandteil der Visualisierung von Daten. Erfahren Sie mehr über die Diagramme, die Sie in mobilen [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Berichten verwenden können, um eine große Bandbreite von Szenarien abzudecken. 

[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-long.md)] verfügt über drei grundlegende Diagrammtypen: Zeitdiagramme, Kategoriediagramme und Diagramme mit Gesamtwerten. Diese drei Diagrammtypen verfügen über entsprechende Vergleichsdiagramme, die bei dem Vergleich zweier unterschiedlicher Reihensätze hilfreich sind.  

## <a name="shared-chart-properties"></a>Gemeinsame Eigenschaften von Diagrammen

Einige Eigenschaften gelten für alle, andere nur für bestimmte Diagramme. Nachstehend sind einige gemeinsame Eigenschaften aufgeführt.

### <a name="number-format"></a>Das Zahlenformat
Sie können den Zahlen in einem Diagramm in [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] eine Vielzahl von Formatierungen zuweisen: z.B. Allgemein, Währung mit oder ohne Dezimalstellen, Prozentsätze mit und ohne Dezimalstellen usw. In einem Diagramm wird das Zahlenformat sowohl auf Achsenannotationen als auch auf Datenpunkt-Popups angewendet. Zahlenformate werden für jedes Diagramm einzeln, nicht für den gesamten mobilen Bericht festgelegt. 

* Wählen Sie die Registerkarte **Layout** aus, wählen Sie ein Diagramm auf der Entwurfsoberfläche aus, und klicken Sie im Bereich **Eigenschaften visueller Elemente** auf ein **Zahlenformat**, um das Zahlenformat festzulegen. 
  
### <a name="legend"></a>Legende
* Wählen Sie die Registerkarte **Layout** aus, wählen Sie ein Diagramm auf der Entwurfsoberfläche aus, und legen Sie im Bereich **Eigenschaften visueller Elemente** die Option **Legende anzeigen** auf **Ein**fest, um die Legende für ein Diagramm anzuzeigen.
  
### <a name="series"></a>Reihen
Jede einzelne Metrik bzw. jeder Wert, die bzw. der in einem Diagramm angezeigt wird, wird als Reihe bezeichnet. Mehrere Reihen können eine gemeinsame x-Achse und eine gemeinsame y-Achse aufweisen. Reihen werden im Bereich mit den Dateneigenschaften der Datenansicht durch Auswahl von Datentabellen und Feldern definiert. Jedes Feld führt zu einer einzelnen Reihe von Datenpunkten in der Diagrammvisualisierung mit einer eigenen Farbe.  

### <a name="change-aggregation"></a>Ändern der Aggregation 
Die Standardaggregation für numerische Felder in Diagrammen lautet „Summieren“. Sie können sie auf „Average“, „Count“, „Minimum“, „Maximum“, „First“ oder „Last“ ändern.

* Wählen Sie die Registerkarte **Daten** aus, und wählen Sie unter **Dateneigenschaften** neben dem numerischen Feld **Optionen** aus, um eine andere Aggregation auszuwählen.

### <a name="set-or-clear-filters"></a>Festlegen oder Löschen von Filtern

Wenn Sie einen Navigator zum Filtern Ihrer mobilen Bericht hinzufügen, können Sie entscheiden, welche Diagramme Sie filtern möchten.

1. Wählen Sie die Registerkarte **Daten** aus, und wählen Sie unter **Dateneigenschaften** **Optionen**aus.

2. Unter **Filtered by**(Gefiltert nach) finden Sie die Navigatoren, die Sie festlegen oder löschen können.

Erfahren Sie mehr über das [Hinzufügen von Navigatoren zu mobilen Reporting Services-Berichten](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md).
   
## <a name="time-charts"></a>Zeitdiagramme  
  
Das Zeitdiagramm ist das grundlegendste Diagramm in [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]. Die Zeitachse (und die Datumsachse) des Diagramms wird automatisch auf das erste gültige Datums-/Uhrzeitfeld in der Datentabelle festgelegt.  

![mobile-report-time-chart](../../reporting-services/mobile-reports/media/mobile-report-time-chart.png)

1. Ziehen Sie ein **Zeitdiagramm** aus der Registerkarte **Layout** auf die Entwurfsoberfläche, und ändern Sie die Größe.

2. Es handelt sich standardmäßig um ein gestapeltes Balkendiagramm. Sie können dies unter **Serienvisualisierung**ändern.

3. Wenn für das Diagramm Daten erforderlich sind, die noch nicht im Bericht vorhanden sind, wählen Sie die Registerkarte **Daten** > **Daten hinzufügen** aus, um [Daten aus Excel oder einem freigegebenen Dataset](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md) abzurufen.

3. Im Bereich **Dateneigenschaften** ist **SimulatedTable** für **Hauptreihe**festgelegt. Klicken Sie auf dem Pfeil im Feld, und wählen Sie anschließend Ihre Tabelle aus.

5. Wenn Sie die **Datenstruktur** auf die Einstellung **By Columns** (Nach Spalten) festlegen (auf der Registerkarte **Layout** > Bereich **Eigenschaften visueller Elemente**), können Sie im Bereich **Dateneigenschaften** mehrere Spalten mit numerischen Werten auswählen.

   Wenn Sie die **Datenstruktur** auf **Nach Zeilen**festlegen, können Sie im Bereich **Dateneigenschaften** ein **Namensfeld für Reihe** und eine Spalte mit numerischen Werten auswählen.
   
Erfahren Sie mehr über das [Gruppieren von Daten nach Spalten oder Zeilen](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md).
  
## <a name="category-charts"></a>Kategoriediagramme  
  
Im Gegensatz zu einem Zeitdiagramm wird in einem Kategoriediagramm auf der x-Achse nach Feldern gruppiert, ausgenommen Datum/Uhrzeit-Feldern. Diese als *Kategoriekoordinate*bezeichnete Gruppierung wird auf Felder mit Zeichenfolgen und nicht auf numerische Felder angewendet.

![mobile-report-category-chart](../../reporting-services/mobile-reports/media/mobile-report-category-chart.png)   

1. Ziehen Sie ein **Kategoriediagramm** von der Registerkarte **Layout** auf die Entwurfsoberfläche, ändern Sie die Größe, und [rufen Sie die Daten dafür ab](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md), falls erforderlich.

2. Wählen Sie die Registerkarte **Daten** aus, und wählen Sie im Bereich **Dateneigenschaften** unter **Category Coordinate**(Kategoriekoordinate) eine Tabelle und ein Feld aus, nach denen gruppiert werden soll. Dieses Feld wird auf der x-Achse des sich ergebenden Diagramms angezeigt.

3. Wählen Sie unter **Hauptreihe**die Tabelle und die numerischen Felder aus, die für jede Kategorie aggregiert werden sollen. 
  
## <a name="totals-charts"></a>Diagramm mit Gesamtwerten  

![mobile-report-totals-chart](../../reporting-services/mobile-reports/media/mobile-report-totals-chart.png)
  
Das Diagramm mit Gesamtwerten bietet zweierlei Vorteile: 
* Es stellt nicht mehrere Reihen dar, sondern lediglich die Summe oder den Gesamtwert der definierten Hauptreihe. 
* Es bietet die Möglichkeit, Daten nach Spalten oder Zeilen zu gruppieren. Das Gruppieren von Spalten kann beim Umgang mit vereinfachten Daten nützlich sein. Beim Gruppieren von Spalten ist nur die Eigenschaft für die Hauptreihe verfügbar, da die Kategoriespalte automatisch durch die Anzahl der Felder bestimmt wird, die für die Eigenschaft für die Hauptreihe ausgewählt wurden.  

Erfahren Sie mehr über das [Gruppieren von Daten nach Spalten oder Zeilen](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md). 
  
## <a name="comparison-charts"></a>Vergleichsdiagramme  
  
Zeitdiagramme, Kategoriediagramme und Diagramme mit Gesamtwerten sind ebenfalls als *Vergleichsdiagramme*verfügbar. In einem Vergleichsdiagramm können Sie nicht nur eine Hauptreihe, sondern auch eine zweite Vergleichsreihe angeben. Die Haupt- und Vergleichsreihen können auf drei verschiedene Arten angezeigt werden.

![mobile-report-comparison-time-chart](../../reporting-services/mobile-reports/media/mobile-report-comparison-time-chart.png)

1. Ziehen Sie eines der **Vergleichsdiagramme** (Zeit, Kategorie oder Gesamtwerte) von der Registerkarte **Layout** auf die Entwurfsoberfläche, ändern Sie die Größe, und [rufen Sie die Daten dafür ab](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md), falls erforderlich.

2. Wählen Sie im Bereich **Eigenschaften visueller Elemente** unter **Serienvisualisierung**eine der folgenden Optionen aus: 
   * Balken und Balken (dünn)
   * Linie und Balken
   * Balken und Fläche (Stufen) 

Sie können in Vergleichsdiagrammen die gleichen Diagrammfarben für die Haupt- und Vergleichswerte in einer Reihe auswählen.

* Legen Sie im Bereich **Eigenschaften visueller Elemente** **Farben in Vergleichsserien wiederverwenden** auf **Ein**fest.

   Wenn die Option auf **Ein**festgelegt wurde, wird die Farbpalette zwischen dem Zeichnen der Haupt- und Vergleichsreihe neu gestartet, sodass verknüpfte Werte in der Haupt- und Vergleichsreihe eine identische Farbe aufweisen. 

   Mit der Einstellung **Aus**setzt die Farbpalette die normale Rotation fort, wenn die Hauptreihe nach der Vergleichsreihe gezeichnet wird. So wird eine möglicherweise irreführende Farbkoordination zwischen den beiden Sätzen von Reihen verhindert.  
  
## <a name="pie-and-funnel-charts"></a>Kreis- und Trichterdiagramme  
  
Kreis-und Trichterdiagrammen gehören zu den einfachsten Visualisierungen. Sie können die Daten entweder nach Zeilen oder nach Spalten strukturieren. 
* **Kreisdiagramme** können in mobilen [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Berichten Kreise, Ringe oder Ringe mit Gesamtwerten dargestellt werden. Kreisdiagramme eignen sich, um die relative Größe verschiedener Teile eines Ganzen anzuzeigen. Zu viele Slices machen sie schwer lesbar.
* **Trichterdiagramme** werden häufig dazu verwendet, um Phasen in einem Prozess, z.B. dem Vertrieb, anzuzeigen.

![mobile-report-funnel-chart](../../reporting-services/mobile-reports/media/mobile-report-funnel-chart.png)

### <a name="structure-pie-and-funnel-chart-data-by-rows-or-by-columns"></a>Strukturieren von Kreis- und Trichterdiagrammdaten nach Zeilen oder Spalten
1. Ziehen Sie ein **Kreis-** oder **Trichterdiagramm** von der Registerkarte **Layout** auf die Entwurfsoberfläche, ändern Sie die Größe, und [rufen Sie die Daten dafür ab](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md), falls erforderlich.
2. Wählen Sie im Bereich **Eigenschaften visueller Elemente** unter **Datenstruktur**eine der folgenden Optionen aus:
   * **Nach Spalten**
   * **Nach Zeilen**
3. Wenn Sie **Nach Spalten**ausgewählt haben, wechseln Sie in die Registerkarte **Daten** , und wählen Sie im Bereich **Dateneigenschaften** unter **Hauptreihe**die Tabelle und alle Felder aus, die Sie im Kreis- oder Trichterdiagramm aggregieren möchten. Die Feldnamen werden verwendet, um die einzelnen Bereiche im resultierenden Diagramm zu bezeichnen.

   Wenn Sie **Nach Zeilen**ausgewählt haben, wechseln Sie in die Registerkarte **Daten** , und wählen Sie im Bereich **Dateneigenschaften** unter **Kategoriespalte**die Tabelle und Spalte mit den Werten aus, die für die Gruppierung und Beschriftung im Kreisdiagramm verwendet werden sollen. Wählen Sie unter „Main Series Column“ (Hauptreihenspalte) ein numerisches Feld für die Werte im Diagramm aus.

Erfahren Sie mehr über das [Gruppieren von Daten nach Spalten oder Zeilen](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md). 

## <a name="treemaps"></a>Treemap-Diagramme  
  
Treemap-Diagramme zeigen Metriken an, indem sie deren Werte in Flächen und Farben von Kacheln in einem rechteckigen Raster anwenden. 

![mobile-report-group-treemap](../../reporting-services/mobile-reports/media/mobile-report-group-treemap.png)

1. Ziehen Sie ein **Treemap-Diagramme** von der Registerkarte **Layout** auf die Entwurfsoberfläche, ändern Sie die Größe, und [rufen Sie die Daten dafür ab](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md), falls erforderlich.
2.  Wählen Sie die Registerkarte **Daten** aus, und wählen Sie im Bereich **Dateneigenschaften** : 

     * Unter **Größe repräsentiert** ein numerisches Feld für die Größe der Kacheln aus.
     * Unter **Farbe repräsentiert** ein numerisches Feld für die Farbe der Kacheln aus. 
     * [optional] **Benutzerdefinierter Mittenwert**: Sie können die Einstellung **Benutzerdefinierter Mittenwert** nur dann verwenden, wenn als Visualisierungstyp „Wärmebild mit benutzerdefiniertem Mittenwert“ ausgewählt wurde.
     
         Der Mittenwert legt die Farbe einer Kachel fest. Je näher die Metrik dem Mittenwert kommt, desto grüner ist die Kachel. Je weiter die Metrik vom Mittenwert entfernt ist, desto röter ist die Kachel.
     
     * [optional] Unter **Popupbezeichnungen** ein Feld oder Felder aus, um ein Popup anzuzeigen, wenn Benutzer eine Kachel im Raster auswählen. Popups in TreeMap-Diagrammen können sowohl Text als auch numerische Felder anzeigen.  

Standardmäßig sind Treemap-Diagramme hierarchisch angeordnet, d.h. dass die Kacheln zuerst nach Kategorie und dann nach Größe und Farbe gruppiert werden.
* Wählen Sie auf der Registerkarte **Daten** unter **Gruppieren nach** eine Tabelle und Feld aus.

Sie können das Gruppieren deaktivieren, sodass die Kacheln nur nach Größe und Farbe angeordnet werden. 

* Klicken Sie auf die Registerkarte **Layout** , und legen Sie die Einstellung **Treemap mit zwei Ebenen** auf **Aus**fest.   

## <a name="waterfall-charts"></a>Wasserfalldiagramme

Ein Wasserfalldiagramm stellt eine laufende Summe dar, während Werte hinzugefügt oder entfernt werden. Es ist nützlich, um zu verstehen, wie ein Anfangswert (z.B. Nettoeinkommen) durch eine Reihe von positiven und negativen Änderungen beeinflusst wird.

Die Säulen sind für Erhöhungen grün und für Senkungen rot dargestellt, damit Sie beides schnell unterscheiden können. Die Säulen mit dem Anfangs- und dem Endwert beginnen häufig bei null, während die Zwischenwerte veränderliche Säulen sind. Aufgrund dieser Darstellung werden Wasserfalldiagramme auch als Brückendiagramme bezeichnet.

### <a name="when-to-use-a-waterfall-chart"></a>Verwendungsmöglichkeiten für Wasserfalldiagramme

Wasserfalldiagramme sind in folgenden Fällen eine gute Wahl:
* Um bei Änderungen am Measure in einer Zeitreihe oder anderen Kategorien die wichtigsten Änderungen zu überwachen, die zum Gesamtwert beitragen.
* Um den Jahresgewinn Ihres Unternehmens darzustellen, indem Sie verschiedene Umsatzquellen darstellen, die zum Gesamtgewinn (oder -verlust) führen.
* Um die Belegschaft für Ihr Unternehmen am Jahresanfang und -ende zu veranschaulichen.
* Um darzustellen, wie viel Geld Sie jeden Monat verdienen und ausgeben und wo der laufende Saldo für Ihr Konto liegt. 

### <a name="create-a-waterfall-chart"></a>Erstellen eines Wasserfalldiagramms

1. Ziehen Sie ein **Wasserfalldiagramm** von der Registerkarte **Layout** auf die Entwurfsoberfläche, ändern Sie die Größe, und [rufen Sie die Daten dafür ab](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md), falls erforderlich.

    ![mobile-report-waterfall-chart-icon](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart-icon.png)
    
2.  Wählen Sie die Registerkarte **Daten** aus, und wählen Sie im Bereich **Dateneigenschaften** ein Kategoriefeld in den Daten für **Kategoriekoordinate**und ein numerisches Feld für **Hauptreihe**aus: 

    ![mobile-report-waterfall-data](../../reporting-services/mobile-reports/media/mobile-report-waterfall-data.png)
    
3. Wählen Sie die Registerkarte **Layout** aus, um das Wasserfalldiagramm in der Vorschau anzuzeigen.

   ![mobile-report-waterfall-chart](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart.png)
   
   Monate mit einem Verlust, wie Februar, Juni und Juli, sind rot dargestellt. 
   Monate mit einem Gewinn, wie September, Oktober und November, sind grün dargestellt. 

## <a name="see-also"></a>Siehe auch 
* [Karten in mobilen Reporting Services-Berichten](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Hinzufügen von Navigatoren zu mobilen Reporting Services-Berichten](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Datenblätter zu mobilen Berichten hinzufügen](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md)
* [Messgeräte mobilen Berichten hinzufügen](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
  

