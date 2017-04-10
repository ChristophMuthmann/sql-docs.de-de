---
title: "Anpassen der Daten und der Anzeige einer Karte oder einer Kartenebene (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "10521"
  - "sql13.rtp.rptdesigner.mapgroupproperties.filter.f1"
  - "10515"
  - "10512"
  - "10520"
  - "sql13.rtp.rptdesigner.shared.font.f1"
  - "10523"
  - "sql13.rtp.rptdesigner.mapgroupproperties.general.f1"
  - "sql13.rtp.rptdesigner.shared.number.f1"
  - "sql13.rtp.rptdesigner.shared.shadowdv.f1"
  - "sql13.rtp.rptdesigner.mapgroupproperties.variables.f1"
  - "10507"
ms.assetid: fdd9b994-d138-4990-a291-279b0249eb72
caps.latest.revision: 13
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 13
---
# Anpassen der Daten und der Anzeige einer Karte oder einer Kartenebene (Berichts-Generator und SSRS)
  Nachdem Sie einem paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]-Bericht mithilfe eines Assistenten eine Karte oder eine Kartenebene hinzugefügt haben, möchten Sie möglicherweise anpassen, wie die Karte im Bericht angezeigt wird. Sie können Verbesserungen vornehmen, indem Sie die folgenden Ideen beachten:  
  
-   Um den Benutzern zu helfen, zu verstehen, wie die Datenanzeige auf einer Karte interpretiert wird, können Sie Legenden und eine Farbskala sowie Bezeichnungen und QuickInfos hinzufügen.  
  
-   Um die Karte besser lesbar zu machen, ändern Sie den Mittelpunkt und die Zoomstufe, fügen Sie eine Entfernungsskala hinzu, und zeigen Sie ein Hintergrundraster an.  
  
-   Um die Kartenzeichnungszeit beim Ausführen des Berichts zu steuern, können Sie die Auflösung anpassen, um die Kartenelemente zu vereinfachen.  
  
-   Sie können Kartenelemente in die Berichtsdefinition einbetten, und dann ändern, wie einzelne Elemente angezeigt werden. Sie können z. B. den primären Bürostandort mit einer Ortsmarke und andere Bürostandorte mit Kreisen anzeigen.  
  
-   Sie können angepasste Regionen hinzufügen, indem Sie Ihre eigenen Datengruppenausdrücke angeben.  
  
-   Sie können eine benutzerdefinierte Position an einem Punkt hinzufügen, den Sie auf einer Kartenebene angeben, die über eingebettete Punkte verfügt. Sie können den Wert und die Anzeigeeigenschaften für benutzerdefinierte Punkte unabhängig von anderen Punkten auf einer Punktebene festlegen.  
  
-   Um weitere Details bereitzustellen, können Sie Kartenelementen Links auf jeder Ebene hinzufügen, auf die ein Benutzer klicken kann, um verwandte Berichte zu öffnen.  
  
 Weitere Ideen zum Verbessern eines Berichts finden Sie unter [Planen eines Berichts &#40;Berichts-Generator&#41;](../../reporting-services/report-design/planning-a-report-report-builder.md).  
  
 Anzeigeoptionen wirken sich auf die Art und Weise aus, wie eine Karte oder die Teile einer Karte angezeigt werden, wenn Sie den Bericht anzeigen. Einige Optionen steuern die Darstellung der Karte, z. B. die Rahmen und die Schriftarten oder den Bereich, die auf der Karte dargestellt wurden. Andere Optionen steuern den Inhalt jeder Ebene, z. B. Blasengrößen, Markertypen, Bezeichnungen oder QuickInfos.  
  
 Ein Kartenberichtselement schließt die folgenden Teile ein: die Karte selbst, einen Kartenviewport, einen Satz von Titeln, einen Satz von Legenden (Legende, Farbskala und Entfernungsskala), ein Satz von Ebenen, ein Satz von Kartenelementen auf jeder Ebene (Polygone oder Linien oder Punkte). Verwenden Sie die Informationen in den folgenden Abschnitten, um zu erfahren, welches Eigenschaften-Dialogfeld die Anzeigeoptionen für die verschiedenen Teile einer Karte steuert.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Map"></a> Ändern von Optionen für die Karte  
 Auf einem Kartenberichtselement können Sie Folgendes steuern:  
  
-   Fügen Sie mehrere Titel hinzu.  
  
-   Fügen Sie mehrere Legenden hinzu. Um den Inhalt einer Legende zu ändern, müssen Sie weitere Legenden erstellen und dann die Regeln ändern, um anzugeben, in welcher Legende die von jeder Regel erstellten Legendenelemente angegeben werden.  
  
-   Fügen Sie weitere Ebenen hinzu.  
  
-   Blenden Sie die Entfernungs- oder Farbskala ein oder aus.  
  
-   Verwenden Sie einen Tiefeneffekt, indem Sie einen Schatten einfügen.  
  
 Um diese Optionen zu ändern, klicken Sie mit der rechten Maustaste auf die Karte, klicken Sie auf **Karte**, und ändern Sie die Optionen.  
  
##  <a name="Viewport"></a> Ändern von Optionen für den Viewport  
 Verwenden Sie die Viewportoptionen, um die Sicht der Karte zu ändern, die im Bericht angezeigt wird.  
  
 Die Quelle räumlicher Daten könnte mehr Bereiche bereitstellen, als Sie im Bericht angezeigt werden müssen. Sie können den Mittelpunkt, die Zoomstufe mithilfe des Viewports festlegen, und den Bereich für die Karte zuzuschneiden.  
  
 Die folgenden Optionen können für den Viewport festgelegt werden:  
  
-   Wählen Sie das Koordinatensystem aus und wählen Sie für ein geografisches Koordinatensystem die Projektion aus.  
  
-   Wählen Sie das Zentrum für die Karte aus.  
  
-   Schneiden Sie die Sicht für die Karte zu.  
  
-   Legen Sie die Zoomebene fest.  
  
-   Auflösung und Vereinfachung. Wählen Sie ein Gleichgewicht zwischen Zeichnungszeit und ausführlichen Umrissen für Linien und Polygone aus.  
  
 Um diese Optionen zu ändern, klicken Sie mit der rechten Maustaste auf den Kartenviewport, und verwenden Sie die Seite [Eigenschaften des Kartenviewports (Dialogfeld), Allgemein](../Topic/Map%20Viewport%20Properties%20Dialog%20Box,%20General.md) sowie verknüpfte Seiten.  
  
##  <a name="Legends"></a> Ändern von Optionen für die Legenden  
 Legenden helfen Benutzern, die Daten auf einer Karte zu interpretieren.  
  
 Standardmäßig fügen alle Regeln, die Sie auf einer Ebene angeben, Elemente zur ersten Legende hinzu. Außerdem zeigen alle Farbregeln Werte in der Farbskala an.  
  
-   Um die Anzeigeoptionen für die Darstellung der Legende zu ändern, einschließlich seiner Position relativ zum Viewport, legen Sie Optionen auf der Legende selbst fest.  
  
-   Um den Inhalt oder das Format des Inhalts für eine Legende zu ändern, ändern Sie die Legendenoptionen für die entsprechenden Regeln für eine Ebene.  
  
 Weitere Informationen finden Sie unter [Ändern der Kartenlegenden, Farbskala und zugeordneten Regeln &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  
##  <a name="Layer"></a> Ändern von Optionen für die Ebene  
 Um die Ebenen für eine Karte anzuzeigen, klicken Sie zum Auswählen auf die Karte. Das Kartenfenster wird angezeigt. Um Optionen für eine Ebene zu ändern, klicken Sie mit der rechten Maustaste auf die Ebene, und verwenden Sie das Kontextmenü.  
  
 Eine Ebene kann einer von drei Typen auf Grundlage der räumlichen Daten sein, die von der räumlichen Datenquelle zurückgegeben werden: eine Polygonebene, eine Linienebene oder eine Punktebene.  
  
 Die folgenden Optionen können für die Ebene festgelegt werden:  
  
-   Die zugehörigen analytischen Daten und die zugehörigen Übereinstimmungsfelder. Die Quelle der räumlichen Daten ist im Kartenfenster unter dem Namen der Ebene aufgeführt. Wenn die Quelle eingebettet ist, sind die Kartenelemente für die Ebene Teil der Berichtsdefinition. Wenn die Quelle nicht eingebettet wird, dann werden die räumlichen Daten zur Laufzeit abgerufen und der Berichtsprozessor erstellt die Kartenelemente für die Ebene, wenn der Bericht verarbeitet wird. Um Datenoptionen auf der Ebene zu ändern, verwenden Sie die Seite Analytische Daten im Dialogfeld Kartenebene.  
  
-   Überlagern Sie die Zeichnungsreihenfolge. Die Reihenfolge, in der die Ebenen im Kartenfenster angezeigt werden, ist die umgekehrte Zeichnungsreihenfolge für die Ebenen. Die letzte Ebene in der Liste wird zuerst gezeichnet. Wenn z. B. die Punkte auf einer Punktebene oben auf den Polygonen in der Polygonebene angezeigt werden sollen, sollte die Polygonebene auf die Punktebene folgen.  
  
-   Überlagern Sie die Sichtbarkeit, einschließlich der Transparenz. Um eine Ebene über eine andere Ebene anzuzeigen, sollten Sie die Transparenz auf einen Wert höher als 0 festlegen. Ein Wert von 100% bedeutet, dass die Ebene nicht sichtbar ist. Um mit einer einzelnen Ebene zu arbeiten, können Sie die einzelnen Ebenen auf einfache Weise ein- oder ausblenden, indem Sie im Kartenfenster das Symbol **Sichtbarkeit** verwenden. Sie können auch Zoomstufenoptionen festlegen, um anzugeben, wann Kartenelemente auf der Ebene auf Grundlage der Zoomstufe angezeigt oder ausgeblendet werden.  
  
-   Fügen Sie eine Bing-Kartenkachelebene für den aktuellen Viewportmittelpunkt und die Zoomstufe hinzu. Sie müssen die geografischen Koordinaten nicht für eine Kachelebene angeben. Kacheln werden automatisch geladen, um mit dem Viewportbereich übereinzustimmen. Wenn das Koordinatensystem geografisch ist, ist die Projektion Mercator, die Bing Maps-Server sind verfügbar, und der Berichtsserver wurde konfiguriert, um diese Funktion zu unterstützen. Sie können für jeden Bericht festlegen, ob zum Abrufen von Kacheln eine sichere Verbindung verwendet werden soll.  
  
 Weitere Informationen zu Ebenen finden Sie unter [Hinzufügen, Ändern oder Löschen einer Karte oder einer Kartenebene &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
##  <a name="DataGrouping"></a> Ändern der Datengruppierung für die Ebene  
 Sie können anpassen, wie räumliche Daten für Ihre eigenen Formen angepasst werden. Um die Gruppeneigenschaften für eine Ebene festzulegen, wählen Sie die Ebene im Kartenbereich aus, und klicken Sie im Bereich „Eigenschaften“ der Ebene auf **Gruppieren**. Klicken Sie dann auf die Auslassungspunkte (…), um die Gruppeneigenschaften zu öffnen. In diesem Dialogfeld können Sie Gruppenausdrücke angeben, Gruppenvariablen erstellen und für die Gruppierung verwendete Daten filtern.  
  
 Der Gruppenausdruck gibt an, wie analytische Daten, die zu räumlichen Daten in einer Beziehung stehen, für jedes Kartenelement in der Ebene aggregiert werden. Standardmäßig ist der Gruppenausdruck der Satz von Übereinstimmungsfeldern, der für die Beziehung zwischen den räumlichen Daten und den analytischen Daten angegeben wurden. Beispielsweise enthalten für eine Blasendiagrammkarte, die Orte und Einwohnerzahlen für ein Land oder einen Bereich anzeigt, die Übereinstimmungsfelder Ortsnamen [City] und Bereichsnamen [Region], da es mehrere Orte mit dem gleichen Namen geben kann. Der entsprechende Gruppenausdruck schließt zwei Felder ein: [City] und [Region].  
  
 Weitere Informationen finden Sie unter [Map Tips: How To Import Shapefiles Into SQL Server and Aggregate Spatial Data](http://go.microsoft.com/fwlink/?LinkID=214991) (Kartentipps: Importieren von Shape-Dateien in SQL Server und Anpassen räumlicher Daten).  
  
##  <a name="MapElements"></a> Ändern von Optionen für die Kartenelemente auf der Ebene  
 Kartenelemente sind die Punkte, Linien oder Polygone auf einer Ebene, die auf den räumlichen Daten basieren. Für Kartenelemente können die folgenden Optionen festgelegt werden. Diese Optionen gelten für alle Kartenelemente auf der Ebene, egal ob sie eingebettet werden oder nicht:  
  
-   Bezeichnungen, Sichtbarkeit der Bezeichnung, Bezeichnungsoffset, und Formatierung.  
  
-   Rahmen und Füllbereich  
  
-   Drillthroughaktionen  
  
-   Anzeigeoptionen  
  
 Die Anzeigeoptionen für Kartenelemente folgen der Reihenfolge auf Grundlage der Ebene, des Kartenelements sowie den Regeln für das Kartenelement, und überschreiben Optionen für eingebettete Kartenelemente.  
  
 Um diese Optionen zu ändern, klicken Sie mit der rechten Maustaste auf das Kartenelement, und verwenden Sie das eingebettete Eigenschaftendialogfeld. Verwenden Sie beispielsweise für ein eingebettetes Polygon die Seite Allgemein und entsprechende Seiten des Dialogfelds Eigenschaften für eingebettete Polygone der Karte.  
  
##  <a name="Precedence"></a> Grundlegendes zur Reihenfolge der Anzeigeoption  
 Wenn Sie die Darstellung eines Punkts, einer Linie oder eines Polygons auf einer Kartenebene steuern möchten, müssen Sie verstehen, wie Anzeigeoptionen festgelegt werden können und welche Optionen Vorrang haben. Die folgenden Anzeigeoptionen sind aufsteigend von der niedrigsten zur höchsten Priorität aufgelistet. Höhere Anzeigeoptionen überschreiben niedrigere Anzeigeoptionen in dieser Liste:  
  
-   Ebenenoptionen  
  
-   Zeigt Linien- oder Polygonenoptionen auf jeder Ebene an. Dies gilt, wenn der Bericht verarbeitet wird, ob die Kartenelemente dynamisch abgerufen werden, oder ob sie die Kartenelemente in die Berichtsdefinition einbetten. Sie geben z. B. auf einer Ebene eine Füllfarbe für alle Elemente an.  
  
-   Regeln Sie können Regeln festlegen, um Farbe, Größe, Breite oder Markertyp für alle Kartenelemente auf einer Ebene zu steuern. Die Regeln, die Sie festlegen können, hängen vom Typ des Kartenelements ab.  
  
    -   Farbregeln Wird auf Marken für Punkte, Linien, Polygone und Marker für Polygonmittelpunkte angewendet.  
  
    -   Größenregeln Werden auf Marken für Punkte und Marker für Polygonmittelpunkte angewendet.  
  
    -   Regeln für die Linienstärke Gilt für Linienstärken.  
  
    -   Markertypregeln Wird auf Marken für Punkte und Marker für Polygonmittelpunkte angewendet.  
  
-   Überschreiben Sie Optionen für einzelne eingebettete Punkte, Linien oder Polygone auf einer Ebene. Änderungen, die Sie vornehmen, sind dauerhaft. Um diese Änderungen wiederherzustellen, müssen Sie die Daten für die Ebene erneut laden.  
  
 Weitere Informationen finden Sie unter [Unterschiedliche Polygon-, Linien- und Punktanzeigen bei der Verwendung von Regeln und analytischen Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/vary polygon, line, and point display by rules and analytical data.md).  
  
## Siehe auch  
 [Karten-Assistent und Kartenebenen-Assistent &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)   
 [Karten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)  
  
  