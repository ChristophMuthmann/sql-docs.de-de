---
title: "Unterschiedliche Polygon-, Linien- und Punktanzeigen bei der Verwendung von Regeln und analytischen Daten (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "10538"
  - "10537"
  - "sql13.rtp.rptdesigner.mapembeddedpolygonlayerproperties.general.f1"
  - "MICROSOFT.REPORTDESIGNER.MAPMARKER.MARKERSTYLE"
  - "sql13.rtp.rptdesigner.mapembeddedlinelayerproperties.general.f1"
  - "sql13.rtp.rptdesigner.mapembeddedpointlayerproperties.general.f1"
  - "10531"
  - "10536"
  - "sql13.rtp.rptdesigner.maplinelayerproperties.widthrules.f1"
ms.assetid: 7f1f5584-37b4-4fa2-ae44-8988c5f0c744
caps.latest.revision: 12
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Unterschiedliche Polygon-, Linien- und Punktanzeigen bei der Verwendung von Regeln und analytischen Daten (Berichts-Generator und SSRS)
  Die Anzeigeoptionen für Polygone, Linien und Punkte in einer Kartenebene werden gesteuert, indem Optionen für die Ebene sowie Regeln für die Kartenelemente in der Ebene festgelegt werden oder indem Optionen für bestimmte eingebettete Kartenelemente in einer Ebene überschrieben werden.  
  
 Anzeigeoptionen werden in einer bestimmten Rangfolge angewendet (hier vom niedrigsten zum höchsten Rang aufgeführt):  
  
1.  Für eine Polygonebene, eine Linienebene und eine Punktebene festgelegte Optionen gelten für alle Kartenelemente in dieser Ebene, unabhängig davon, ob die Kartenelemente in die Berichtsdefinition eingebettet sind.  
  
2.  Für Regeln festgelegte Optionen gelten für alle Kartenelemente in einer Ebene. Alle Datenvisualisierungsoptionen gelten nur für Kartenelemente, die räumlichen Daten zugeordnet sind. Bei einer Datenvisualisierungsoption müssen Sie ein Datenfeld angeben, auf dem Anzeigevarianten basieren können. Sie müssen die Übereinstimmungsfelder für die analytischen und räumlichen Daten festlegen, bevor Sie Datenvisualisierungsregeln anwenden. Weitere Informationen finden Sie unter [Karten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
3.  Optionen, die Sie für ausgewählte eingebettete Kartenelemente festlegen. Beachten Sie, dass beim Überschreiben der Ebenenoptionen die an der Berichtsdefinition vorgenommenen Änderungen dauerhaft sind. Sie können die Datenfeldwerte ändern sowie Anzeigeoptionen überschreiben, um anzupassen, wie bestimmte Polygone, Linien und Punkte auf einer Ebene angezeigt werden.  
  
 Zusätzlich zum Steuern der Anzeige von Kartenelementen in einer Ebene können Sie die Ebenentransparenz steuern, damit früher gezeichnete Ebenen durch später gezeichnete Ebenen durchscheinen können. Weitere Informationen zum Ändern von Optionen, die das Schema oder die gesamte Kartenebene beeinflussen, finden Sie unter [Anpassen der Daten und der Anzeige einer Karte oder einer Kartenebene &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Rules"></a> Grundlegendes zu Regeln  
 Sie können vier Typen von Regeln festlegen, mit denen der Berichtsprozessor Anzeigeeigenschaften für Kartenelemente in einer Ebene automatisch anpassen kann. Regeln hängen vom Kartenelementtyp ab: Polygone, Linien oder Punkte.  
  
-   **Polygone.** Verändern Sie Polygonfarbe.  
  
    -   **Polygonmittelpunkte.** Verändern Sie Markerfarbe, Markergröße und Markertyp für Marker, die im Mittelpunkt der einzelnen Polygone angezeigt werden.  
  
-   **Linien.** Verändern Sie Linienfarbe und Linienstärke.  
  
-   **Punkte.** Verändern Sie Markerfarbe, Markergröße und Markertyp für Marker, die für die einzelnen Punkt angezeigt werden.  
  
##  <a name="Color"></a> Grundlegendes zu Farbregeln  
 Farbregeln werden auf Füllfarben für Polygone, Linien und Marker angewendet, die Punkte oder Polygonmittelpunkte darstellen.  
  
 Farbregeln unterstützen vier Optionen:  
  
-   Vorlagenstil anwenden. Das Design, das Sie im Assistenten ausgewählt haben, definiert den Vorlagenstil für die Ebene. Das Design legt das Format für die Schriftart, die Rahmenart und die Palette fest.  
  
-   Daten mithilfe der Farbpalette anzeigen. Sie geben eine Palette anhand ihres Namens an. Der Berichtsprozessor legt die Farbe jedes Kartenelements in einer Ebene fest, indem er alle Farben in der Palette durchläuft und schrittweise hellere Schattierungen jeder Farbe in der Palette anwendet.  
  
-   Daten mithilfe von Farbbereichen anzeigen. Sie geben eine Start-, Mittel- und Endfarbe an. Dann geben Sie Verteilungsoptionen an. Der Berichtsprozessor erstellt mithilfe der Verteilungsoptionswerte einen Satz von Farben, der eine Ansicht ähnlich einer Temperaturverteilungskarte erzeugt. Eine Temperaturverteilungskarte zeigt verschiedene Farben für unterschiedliche Temperaturen an. Auf einer Skala von 0 bis 100 sind niedrige Werte beispielsweise blau, um Kälte darzustellen, und hohe Werte rot, um Hitze zu veranschaulichen.  
  
-   Daten mithilfe benutzerdefinierter Farben anzeigen. Sie geben einen Satz von Farben an. Der Berichtsprozessor legt die Farbe jedes Kartenelements in der Ebene fest, indem er die angegebenen Werte schrittweise durchläuft.  
  
 Die Standardpalette schließt die Farbe Weiß ein. Um den starken Kontrast zwischen Weiß und anderen Farben in der Palette zu vermeiden, geben Sie eine helle Farbe innerhalb der Palette als Startfarbe an.  
  
 Um Kartenelemente, die keinen Daten zugeordnet sind, farblos anzuzeigen, legen Sie als Standardfarbe für die Kartenelemente in der Ebene **Keine Farbe** fest.  
  
### Farbskala  
 Standardmäßig werden alle Farbregelwerte in der Farbskala und in der ersten Legende angezeigt. Die Farbskala zeigt entwurfsbedingt einen einzelnen Bereich von Farben an. Wählen Sie die wichtigsten Daten aus, die in der Farbskala angezeigt werden sollen.  
  
 Um die Werte zu entfernen, die nicht in der Farbskala enthalten sein sollen, deaktivieren Sie die Farbskalaoption für jede Farbregel auf jeder Ebene.  
  
##  <a name="Width"></a> Grundlegendes zu Linienstärkenregeln  
 Regeln für die Linienstärke gelten für Linien. Regeln für die Linienstärke unterstützen zwei Optionen:  
  
-   Standardlinienstärke verwenden. Sie geben die Linienstärke in Punkt an.  
  
-   Daten mithilfe der Linienstärke anzeigen. Sie legen die minimale und maximale Stärke für die Linie fest, geben das Datenfeld an, das verwendet werden soll, um die Stärke zu verändern, und geben dann die Verteilungsoptionen an, die auf diese Daten angewendet werden sollen.  
  
##  <a name="Size"></a> Grundlegendes zu Markergrößenregeln  
 Größenregeln gelten für Marker, die Punkte oder Polygonmittelpunkte darstellen. Größenregeln unterstützen zwei Optionen:  
  
-   Standardmarkergröße verwenden. Sie geben die Größe in Punkt an.  
  
-   Daten mithilfe der Größe anzeigen. Sie legen die minimale und maximale Größe für den Marker fest, geben das Datenfeld an, das verwendet werden soll, um die Größe zu verändern, und geben dann die Verteilungsoptionen an, die auf diese Daten angewendet werden sollen.  
  
##  <a name="Marker"></a> Grundlegendes zu Markertypregeln  
 Markertypregeln gelten für Marker, die Punkte oder Polygonmittelpunkte darstellen. Markertypregeln unterstützen zwei Optionen:  
  
-   Standardmarkertyp verwenden. Sie geben einen der verfügbaren Markertypen an.  
  
-   Daten mithilfe von Markern anzeigen. Sie geben einen Satz von Markern und die Reihenfolge an, in der sie verwendet werden sollen. Markertypen sind: **Circle**(Kreis), **Diamond**(Raute), **Pentagon**(Fünfeck), **PushPin**(Ortsmarke), **Rectangle**(Rechteck), **Star**(Stern), **Triangle**(Dreieck), **Trapezoid**(Trapezoid) und **Wedge**(Sektor).  
  
##  <a name="Distribution"></a> Grundlegendes zu Verteilungsoptionen  
 Um eine Verteilung von Werten zu erstellen, können Sie die Daten in Bereiche unterteilen. Sie geben den Verteilungstyp, die Anzahl der Unterbereiche sowie den minimalen und den maximalen Bereichswert an.  
  
 Nehmen Sie in der folgenden Liste an, dass Sie über drei Kartenelement und sechs verwandte analytische Werte verfügen, die zwischen 1 und 9999 liegen, und zwar: 1, 10, 200, 2000, 4777, 8999.  
  
-   **EqualInterval – Gleiches Intervall.** Erstellt Bereiche, die die Daten in gleiche Bereichsintervalle unterteilen. Im Beispiel sind die drei Bereiche 0-2999, 3000-5999, 6000-8999. Unterbereich 1: 1, 10, 200, 500. Unterbereich 2: 4777. Unterbereich 3: 8999. Diese Methode berücksichtigt nicht, wie die Daten verteilt sind. Sehr große Werte oder sehr kleine Werte können die Verteilungsergebnisse verzerren.  
  
-   **EqualDistribution - Gleichmäßige Verteilung.** Erstellt Bereiche, die diese Daten so aufteilen, dass jeder Bereich eine gleiche Anzahl von Elementen enthält. In den Beispieldaten sind die drei Bereiche 0-10, 11-500, 501-8999. Unterbereich 1: 1. 10. Unterbereich 2: 200, 500. Unterbereich 3: 4777, 8999. Diese Methode kann die Verteilung verzerren, indem sie Unterteilungen erstellt, die sehr große oder sehr kleine Bereiche umfassen.  
  
-   **Optimal** . Erstellt Bereiche, die automatisch die Verteilung so anpassen, dass ausgewogene Unterbereiche erstellt werden. Die Anzahl der Unterbereiche wird vom Algorithmus bestimmt.  
  
-   **Benutzerdefiniert.** Geben Sie Ihre eigene Anzahl von Bereichen an, um die Verteilung von Werten zu steuern. Für die Beispieldaten können Sie 3 Bereiche angeben: 1-2, 3-8, 9.  
  
 Die Verteilungswerte werden von den Regeln verwendet, um unterschiedliche Kartenelementanzeigewerte zu verwenden.  
  
##  <a name="Legends"></a> Grundlegendes zu Legenden und Legendenelementen  
 Legendenelemente werden automatisch aus Regeln erstellt, die Sie für jede Ebene angeben. Mit Regeloptionen wird gesteuert, wie viele Elemente erstellt werden und in welcher Legende sie angezeigt werden. Standardmäßig werden der ersten Legende alle Elemente für alle Regeln hinzugefügt. Um Elemente aus der ersten Legende zu verschieben, erstellen Sie so viele weitere Legenden, wie Sie benötigen, und geben Sie für jede Regel die Legende an, die verwendet werden soll, um die Elemente anzuzeigen, die sich aus der Regel ergeben. Um Elemente auf Grundlage einer Regel auszublenden, geben Sie einen leeren Legendennamen an.  
  
 Um zu steuern, wo eine Legende angezeigt wird, verwenden Sie das Dialogfeld "Legendeneigenschaften", um eine Position relativ zum Kartenviewport anzugeben. Weitere Informationen finden Sie unter [Ändern der Kartenlegenden, Farbskala und zugeordneten Regeln &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  
 Legenden werden automatisch erweitert, um den Legendentitel oder Legendentext anzuzeigen. Um den Text von Legendenelementen zu formatieren, verwenden Sie Kartenlegenden-Schlüsselwörter und benutzerdefinierte Formate. Weitere Informationen finden Sie unter [To change the format of content in a legend](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md#ChangeFormatItems).  
  
 Die folgenden Tabellen zeigen Beispiele für unterschiedliche Formate an, die Sie verwenden können.  
  
|Schlüsselwort und Format|Description|Beispiel für den in der Legende angezeigten Text|  
|------------------------|-----------------|---------------------------------------------------|  
|`#FROMVALUE {C0}`|Zeigt die Währung des Gesamtwerts ohne Dezimalstellen an.|$400|  
|`#FROMVALUE {C2}`|Zeigt die Währung des Gesamtwerts mit zwei Dezimalstellen an.|$400.55|  
|`#TOVALUE`|Zeigt den tatsächlichen numerischen Wert des Datenfelds an.|10000|  
|`#FROMVALUE{N0} - #TOVALUE{N0}`|Zeigt die tatsächlichen numerischen Werte des Anfangs und des Endes des Bereichs an.|10 - 790|  
  
## Siehe auch  
 [Ändern der Kartenlegenden, Farbskala und zugeordneten Regeln &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)   
 [Karten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Karten-Assistent und Kartenebenen-Assistent &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
  
  