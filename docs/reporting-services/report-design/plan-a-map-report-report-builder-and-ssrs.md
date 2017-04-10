---
title: "Planen eines Kartenberichts (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dc0c27a4-7e31-4a15-a0bc-3a02479d5b02
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 9
---
# Planen eines Kartenberichts (Berichts-Generator und SSRS)
Gute Berichte enthalten Informationen, die als Grundlage für Aktionen oder Verständniszugewinn dienen können. Um Analytische Daten, wie z. B. Gesamtumsätze oder demografische Daten, mit einem geografischen Hintergrund zu präsentieren, können Sie dem paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]-Bericht eine Karte hinzufügen. Eine Karte kann mehrere Ebenen enthalten, wobei jede Ebene Kartenelemente anzeigt, die von einem bestimmten Typ räumlicher Daten definiert werden: Punkte, die Positionen darstellen, Linien, die Routen darstellen, oder Polygone, die Flächen darstellen. Sie können den analytischen Daten auf jeder Ebene Kartenelemente zuordnen.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="MapPurpose"></a> Angeben des Zweckes der Karte  
 Ein gut entworfener Bericht stellt Informationen bereit, die Benutzern helfen, sich ihren Anliegen zu widmen. Um eine nützliche, leicht verständliche Kartenansicht zu erstellen, entscheiden Sie, welchen Fragen Sie mit der Karte beantworten wollen. Sie können beispielsweise auf einer Karte die folgenden Arten von Daten visuell darstellen, um Marktchanchen zu identifizieren:  
  
-   Anteilige Verkäufe in jedem Laden.  
  
-   Nach Kundendemografie kategorisierte Verkäufe auf Grundlage des Kundenstandorts in Relation zu den Standorten der Läden.  
  
-   Umsätze oder andere finanzielle Daten im Vergleich nach Vertriebsgebiet.  
  
-   Umsätze im Vergleich für unterschiedliche Rabattstrategien in mehreren Läden.  
  
 Nachdem Sie den Zweck der Kartenansicht identifiziert haben, müssen Sie analysieren, welche Daten Sie benötigen. Analytische Daten stammen aus Berichtsdatasets. Standortdaten stammen aus räumlichen Datenquellen, die Sie angeben müssen.  
  
##  <a name="Data"></a> Angeben der räumlichen und analytischen Daten  
 Sie müssen angeben, welche räumlichen und analytischen Daten Sie benötigen.  
  
 Analytische Daten können aus einem Berichtsdataset, aus Beispieldaten einer Karte aus dem Kartenkatalog oder aus analytischen Daten, die in den räumlichen Daten einer ESRI-Shape-Datei enthalten sind, stammen.  
  
 Es gibt drei Formen von räumlichen Daten: Punkte, Linien und Polygone.  
  
-   **Punkte.** Punkte geben Standorte an, z. B. eine Stadt oder die Adresse eines Ladens, Restaurants oder Tagungszentrums. Für jeden Standort, den Sie auf einer Karte anzeigen möchten, müssen Sie die räumlichen Daten bereitstellen. Nachdem Sie einer Karte Punkte hinzugefügt haben, können Sie an der Punktposition einen Marker anzeigen, dessen Typ, Größe und Farbe Sie anpassen können.  
  
-   **Linien.** Linien geben Pfade oder Routen an, z. B. Lieferrouten oder Flugstrecken. Nachdem Sie einer Karte eine Linie hinzugefügt haben, können Sie die Linienfarbe und die Linienstärke verändern.  
  
-   **Polygone.** Polygone geben Bereiche an, wie z. B. Regionen, Gebiete, Länder, Bundesländer, Provinzen, Landkreise, Orte oder Bereiche, die Regierungsbezirken, Postleitzahlen, Telefonvorwahlen oder Volkszählungsbezirken entsprechen. Nachdem Sie einer Karte Polygone hinzugefügt haben, können Sie den Umriss sowie einen Marker im Mittelpunkt des Polygonbereichs anzeigen.  
  
 Nachdem Sie identifiziert haben, welche räumlichen Daten Sie benötigen, müssen Sie eine Quelle für diese Daten suchen.  
  
### Suchen einer Quelle für räumliche Daten  
 Sie können räumliche Daten, die in der Karte verwendet werden sollen, in folgenden Quellen suchen:  
  
-   ESRI-Shape-Dateien, einschließlich öffentlich verfügbarer Shape-Dateien, nach denen Sie im Internet suchen können.  
  
-   Räumliche Daten aus räumlichen Datenquellen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Karten aus Berichten im Kartenkatalog.  
  
-   Drittanbieterwebsites, die räumliche Daten in Form von ESRI-Shape-Dateien oder räumlichen Daten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anbieten.  
  
-   Bing-Kartenkacheln, die einen Hintergrund für die Kartenansicht bereitstellen. Wenn Sie in einer Karte Kacheln anzeigen möchten, muss der Berichtsserver zur Unterstützung der Bing Maps-Webdienste konfiguriert werden.  
  
 Weitere Informationen finden Sie unter "Wo finde ich ESRI-Shape-Dateien?" in [Karten-Assistent und Kartenebenen-Assistent &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md).  
  
 Räumliche Daten können aus politischen Gründen vertraulich sein; sie können auch urheberrechtlich geschützt sein. Überprüfen Sie die Nutzungsbedingungen und die Datenschutzbestimmungen für räumliche Datenquellen, um sich darüber zu informieren, wie Sie räumliche Daten im Bericht verwenden können.  
  
 Nachdem Sie die gewünschten Daten gefunden haben, können Sie sie in die Berichtsdefinition einbetten oder sie während der Berichtsverarbeitung dynamisch abrufen. Weitere Informationen finden Sie weiter unten unter [Finden eines Gleichgewichts zwischen Definitionsgröße und Verarbeitungszeit des Berichts](#Embedding) .  
  
### Bestimmen der räumlichen Daten und der Übereinstimmungsfelder für räumliche Daten  
 Um analytische Daten auf einer Karte anzuzeigen und Größe, Farbe oder Typ des Markers zu verändern, müssen Sie Felder angeben, die die räumlichen Daten und die analytischen Daten verknüpfen.  
  
 Räumliche Daten müssen die folgenden Felder enthalten:  
  
-   **anbieten.** Ein Feld für räumliche Daten, das die Koordinatensätze enthält, die die einzelnen Punkte, Linien und Polygone definieren.  
  
-   **Übereinstimmungsfelder.** Mindestens ein Feld, das jedes räumliche Datenfeld eindeutig identifiziert. Beispielsweise können Sie für einen Punkt, der einen Ladenstandort darstellt, den Namen des Ladens verwenden. Wenn der Name des Ladens in den räumlichen Daten nicht eindeutig ist, können Sie zusätzlich den Namen des Ortes einschließen.  
  
 Die Übereinstimmungsfelder werden verwendet, um die räumlichen Daten mit den analytischen Daten zu verknüpfen.  
  
### Bestimmen der analytischen Daten und der zugehörigen Übereinstimmungsfelder  
 Nachdem Sie die räumlichen Daten identifiziert haben, müssen Sie die analytischen Daten identifizieren. Folgende Quellen für analytische Daten sind möglich:  
  
-   Ein vorhandenes Berichtsdataset. Felder werden als einfache Feldausdrücke angegeben, z. B. [Sales] oder =Fields!Sales.Value.  
  
-   Datenfelder, die von der räumlichen Datenquelle bereitgestellt werden. Felder werden als Schlüsselwörter angegeben, die mit # beginnen, gefolgt vom Feldnamen aus der räumlichen Datenquelle.  
  
 Sie müssen dann die Namen der Übereinstimmungsfelder bestimmen:  
  
-   Übereinstimmungsfelder. Mindestens ein Feld, das die gleichen Informationen wie die Übereinstimmungsfelder für die räumlichen Daten angibt, um eine Beziehung zwischen den räumlichen Daten und den analytischen Daten zu erstellen. Übereinstimmungsfelder sollten eine Übereinstimmung mit dem Datentyp sowie der Formatierung herstellen.  
  
 Wenn Sie die räumliche Datenquelle, die räumlichen Daten, die analytische Datenquelle, die analytischen Daten und die Übereinstimmungsfelder identifiziert haben, sind Sie bereit, zu entscheiden, welcher Typ von Karte dem Bericht hinzugefügt werden soll.  
  
##  <a name="MapType"></a> Auswählen eines Kartentyps  
 Bei der Ausführung des Karten-Assistenten fügen Sie dem Bericht eine Karte und die erste Kartenebene hinzu. Mit dem Assistenten können Sie dem Bericht einen der folgenden Typen von Karten hinzufügen:  
  
-   Eine Standardkarte, die Standorte ohne zugeordnete analytische Daten anzeigt.  
  
-   Eine Karte, bei der jedem Kartenelement genau ein analytischer Wert zugeordnet ist, z. B. jedem Ladenstandort sein Gesamtumsatz.  
  
-   Eine Karte, bei der jedem Kartenelement mehr als ein analytischer Wert zugeordnet ist, wie z. B. jedem Ladenstandort die Anzahl seiner Kunden und sein Gesamtumsatz.  
  
 In der folgenden Tabelle werden die einzelnen Kartentypen beschrieben. Bei allen Kartentypen können Sie ein Design auswählen, um Palette, Rahmenart und Schriftart zu steuern sowie Bezeichnungen anzeigen.  
  
|Assistentensymbol|Ebenenformat|Ebenentyp|Beschreibung und Optionen|  
|-----------------|-----------------|----------------|-----------------------------|  
|![rs_MapType_Polygon_Basic](../../reporting-services/report-design/media/rs-maptype-polygon-basic.png "rs_MapType_Polygon_Basic")|Standardkarte|Polygon|Eine Karte, die nur Bereiche anzeigt, wie z. B. Vertriebsgebiete.<br /><br /> Optionen: Verändern Sie Farben anhand der Palette, oder verwenden Sie eine einzelne Farbe. Eine Palette ist ein vordefinierter Satz von Farben. Wenn alle Farben in einer Palette zugewiesen wurden, werden Farbschattierungen zugewiesen.|  
|![rs_MapType_Polygon_ColorAnalytical](../../reporting-services/report-design/media/rs-maptype-polygon-coloranalytical.png "rs_MapType_Polygon_ColorAnalytical")|Analytische Farbkarte|Polygon|Eine Karte, die analytische Daten mithilfe unterschiedlicher Farben anzeigt, wie z. B. Umsatzdaten nach Bereich.|  
|![rs_MapType_Polygon_Bubble](../../reporting-services/report-design/media/rs-maptype-polygon-bubble.png "rs_MapType_Polygon_Bubble")|Blasendiagrammkarte|Polygon|Eine Karte, die analytische Daten durch unterschiedliche Blasengrößen für unterschiedliche Bereiche anzeigt, wie z. B. Umsatzdaten nach Bereich.<br /><br /> Optionen: Verändern Sie die Farben von Bereichen anhand eines zweiten analytischen Felds, und geben Sie Farbregeln an.|  
|![rs_MapType_Line_Basic](../../reporting-services/report-design/media/rs-maptype-line-basic.png "rs_MapType_Line_Basic")|Standardkarte (Linien)|Linie|Eine Karte, die nur Linien anzeigt, wie z. B. Lieferrouten.<br /><br /> Optionen: Verändern Sie Farben anhand der Palette, oder verwenden Sie eine einzelne Farbe.|  
|![rs_MapType_Line_Analytical](../../reporting-services/report-design/media/rs-maptype-line-analytical.png "rs_MapType_Line_Analytical")|Analytische Karte (Linien)|Linie|Eine Karte, die unterschiedliche Linienfarben und -breiten enthält, wie z. B. für die Anzahl gelieferter Pakete und für Pünktlichkeitsmetriken nach Route.<br /><br /> Optionen: Verändern Sie Linienstärke anhand eines analytischen Felds, verändern Sie die Linienfarbe anhand eines zweiten analytischen Felds, und geben Sie Farbregeln an.|  
|![rs_MapType_Marker_Basic](../../reporting-services/report-design/media/rs-maptype-marker-basic.png "rs_MapType_Marker_Basic")|Einfache Markerkarte|Punkt|Eine Karte, die für jeden Standort einen Marker anzeigt, z. B. für Städte.<br /><br /> Optionen: Verändern Sie Farben anhand der Palette, oder verwenden Sie eine einzelne Farbe, und ändern Sie das Markerformat.|  
|![rs_MapType_Marker_Bubble](../../reporting-services/report-design/media/rs-maptype-marker-bubble.png "rs_MapType_Marker_Bubble")|Blasendiagramm-Markerkarte|Punkt|Eine Karte, die eine Blase für jeden Standort anzeigt, wobei die Blasengröße von einem analytischen Datenfeld abhängt, z. B. Umsatzdaten nach Stadt.<br /><br /> Optionen: Verändern Sie die Blasenfarbe anhand eines zweiten analytischen Felds, und geben Sie Farbregeln an.|  
|![rs_MapType_Marker_Analytical](../../reporting-services/report-design/media/rs-maptype-marker-analytical.png "rs_MapType_Marker_Analytical")|Analytische Markerkarte|Punkt|Eine Karte, die an jedem Standort einen Marker anzeigt, wobei Farbe, Größe und Typ der Marker auf analytischen Daten basieren, wie z. B. Produkte mit den besten Verkaufszahlen, Gewinnspanne und Rabattstrategie.<br /><br /> Optionen: Verändern Sie den Markertyp anhand eines analytischen Felds, verändern Sie die Markergröße anhand eines zweiten analytischen Felds, verändern Sie die Markerfarbe anhand eines dritten analytischen Felds, und geben Sie Farbregeln an.|  
  
 Nachdem Sie mit dem Karten-Assistenten eine Karte hinzugefügt haben, können Sie mit dem Ebenen-Assistenten zusätzliche Ebenen erstellen oder die Optionen für eine Ebene ändern. Weitere Informationen zu Assistenten finden Sie unter [Karten-Assistent und Kartenebenen-Assistent &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md).  
  
 Sie können die Anzeige oder die Datenoptionen für jede Ebene unabhängig anpassen. Weitere Informationen zum Anpassen einer Karte nach Ausführung des Assistenten finden Sie unter [Anpassen der Daten und der Anzeige einer Karte oder einer Kartenebene &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
##  <a name="Legend"></a> Planen von Legenden  
 Um den Benutzern die Interpretation einer Karte zu erleichtern, können Sie mehrere Kartenlegenden, eine Farbskala und eine Entfernungsskala hinzufügen. Planen Sie beim Entwerfen einer Karte, wo die Legenden angezeigt werden sollen. Sie können die folgenden Informationen zu jeder Legende angeben:  
  
-   **Ort der Legende.** Legenden können beispielsweise innerhalb oder außerhalb des Viewports angezeigt werden, sowie an 12 diskreten Orten relativ zum Viewport.  
  
-   **Legendenarten**. Sie können beispielsweise Eigenschaften für den Schriftschnitt, die Rahmenart, Trennlinien und die Füllung angeben.  
  
-   **Legendentitel.** Sie können beispielsweise den Titeltext angeben und unabhängig steuern, ob der Titel für eine Kartenlegende oder die Farbskala angezeigt werden soll.  
  
-   **Kartenlegendenlayout.** Kartenlegenden können beispielsweise als hohe oder breite Tabellen angezeigt werden.  
  
 Der Inhalt der Legende wird während der Berichtsverarbeitung auf der Grundlage von Regeloptionen automatisch erstellt, die Sie für jede Ebene festlegen.  
  
 Standardmäßig zeigen alle Ebenen die Ergebnisse von Regeln in der ersten Kartenlegende an. Sie können mehrere Legenden erstellen und dann für jede Regel zuweisen, welche Legende beim Anzeigen der Ergebnisse verwendet werden soll.  
  
 Weitere Informationen finden Sie unter [Unterschiedliche Polygon-, Linien- und Punktanzeigen bei der Verwendung von Regeln und analytischen Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/vary polygon, line, and point display by rules and analytical data.md) und [Ändern der Kartenlegenden, Farbskala und zugeordneten Regeln &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  
##  <a name="Embedding"></a> Finden eines Gleichgewichts zwischen Definitionsgröße und Verarbeitungszeit des Berichts  
 Um Berichte für Karten gut zu entwerfen, müssen Sie ein Gleichgewicht zwischen den Optionen finden, die die Leistung und die Definitionsgröße des Berichts steuern. Kartenelemente, die auf räumlichen Daten oder Bing-Kartenkacheln basieren, können statisch sein und in die Berichtsdefinition eingebettet werden oder dynamisch sein und bei jeder Verarbeitung des Berichts erstellt werden. Sie müssen die Zielkonflikte für statische und dynamische Kartendaten bewerten und das für Ihre Situation angemessene Gleichgewicht suchen. Beachten Sie die folgenden Informationen, um diese Entscheidung zu treffen:  
  
-   Eingebettete Kartenelemente können die Größe der Berichtsdefinition bedeutend erhöhen, aber reduzieren die Zeit, die erforderlich ist, um die Karte im Bericht anzuzeigen. Möglicherweise gelten für den Berichtsserver Größenbeschränkungen, die Sie berücksichtigen müssen.  
  
-   Die Berichtsdefinition gibt Grenzen für die Anzahl räumlicher Datenpunkte an, die verarbeitet werden können, sowie einen separaten Wert, der angibt, wie viele Kartenelemente in der Berichtsdefinition enthalten sein können.  
  
-   Dynamische Kartenelemente verringern die Größe der Berichtsdefinition, aber erhöhen die Zeit, die erforderlich ist, um den Kartenbericht zu verarbeiten und zu rendern.  
  
-   Wenn sich die Quelle räumlicher Daten auf Ihrem Computer befindet, werden Kartenelemente immer in die Berichtsdefinition eingebettet. Dies schließt räumliche Daten aus dem Kartenkatalog sowie aus ESRI-Shape-Dateien ein, die lokal installiert wurden.  
  
 Um dynamische räumliche Daten zu verwenden, muss sich die räumliche Datenquelle auf dem Berichtsserver befinden. Wenn Berichte in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]entworfen werden, können einem Projekt räumliche Datenquellen hinzugefügt werden und zusammen mit der Berichtsdefinition auf dem Berichtsserver veröffentlicht werden. Wenn Sie Berichte mithilfe des Berichts-Generators entwerfen, müssen Sie zuerst die räumlichen Daten auf den Berichtsserver hochladen, und dann im Assistenten oder in den Ebeneneigenschaften diese Quelle räumlicher Daten für die Kartenebene angeben.  
  
## Siehe auch  
 [Anpassen der Daten und der Anzeige einer Karte oder einer Kartenebene &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [Tutorial: Kartenbericht &#40;Berichts-Generator&#41;](../../reporting-services/tutorial-map-report-report-builder.md)   
 [Karten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Problembehandlung bei Berichten: Kartenberichte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  