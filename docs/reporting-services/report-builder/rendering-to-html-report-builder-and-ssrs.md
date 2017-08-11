---
title: Rendern in das HTML-Format (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf559b0a-499a-4d74-b520-b382b87e0b17
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a431b5b8c988b981f217353c366bbbe1f1f68699
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="rendering-to-html-report-builder-and-ssrs"></a>Rendern in das HTML-Format (Berichts-Generator und SSRS)
  Die HTML-Renderingerweiterung rendert einen paginierten Bericht im HTML-Format. Die Renderingerweiterung kann außerdem vollständige HTML-Seiten oder HTML-Fragmente zum Einbetten in andere HTML-Seiten erstellen. HTML wird stets mit UTF-8-Codierung erstellt.  
  
 Die HTML-Renderingerweiterung ist die Standardrenderingerweiterung für Berichte, die mit einem Browser angezeigt werden (auch bei der Ausführung im [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Webportal).  
  
 Die HTML-Renderingerweiterung ist die Standardrenderingerweiterung für Berichte, die mit einem Browser angezeigt werden (auch bei der Ausführung im [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Webportal). Die HTML-Renderingerweiterung kann HTML als Fragment oder als vollständiges HTML-Dokument rendern. Falls HTML ein Fragment ist, werden die Tags **HEAD**, **HTML**und **BODY** des HTML-Dokuments entfernt. Nur der Inhalt des **BODY** -Tags wird gerendert. Dies ist hilfreich beim Einbetten des HTML-Codes in den von einer anderen Anwendung erstellten HTML-Code.  
  
 In einigen Szenarien können mit Berichtsparametern Script-Injection-Angriffe gestartet werden, wenn Berichte in HTML gerendert werden. Weitere Informationen zum Schützen von Berichten finden Sie unter [Sichere Berichte und Ressourcen](../../reporting-services/security/secure-reports-and-resources.md).  
  
 Weitere Informationen zu Browsern finden Sie unter [Browserunterstützung für Reporting Services und Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RenderingMHTML"></a> Rendern in das MHTML-Format  
 Die HTML-Renderingerweiterung kann Berichte im MHTML-Format (MIME Encapsulation of Aggregate HTML Documents) rendern. MHTML erweitert HTML, um codierte Objekte in das HTML-Dokument einzubetten, z. B. Bilder. Mit der MHTML-Renderingerweiterung können Sie Ressourcen wie Bilder, Dokumente oder andere Binärdateien als MIME-Strukturen (Multipurpose Internet Mail Extensions) in den Berichts-HTML-Code in einer einzelnen Datei einbetten. Daneben sind MHTML-Berichte zur Einbettung in E-Mail-Nachrichten geeignet, da alle Ressourcen in den Bericht eingeschlossen sind. Zwar rendert eigentlich die HTML-Renderingerweiterung MHTML, aber diese Funktion kann auch als MHTML-Renderingerweiterung bezeichnet werden.  
  
  
##  <a name="BrowserSupport"></a> Browserunterstützung  
 Diese Renderingerweiterung unterstützt die folgenden Browserversionen:  
  
-   Internet Explorer 5.5 und höher  
  
-   Firefox 1.5 und höher  
  
-   Safari 3.0 und höher  
  
 Aufgrund von browserübergreifenden Überlegungen kann der gerenderte Bericht je nach Browser leicht unterschiedlich ausfallen. So enthält z. B. das Textfeld die Eigenschaft „WritingMode“. Diese Eigenschaft wird in Firefox nicht unterstützt.  
  
  
##  <a name="HTMLSpecificRenderingRules"></a> HTML-spezifische Renderingregeln  
 Die folgenden HTML-spezifischen Regeln werden beim Rendern angewendet:  
  
-   Der Renderer erstellt eine HTML-Tabellenstruktur mit allen Elementen in jeder **ReportItems** -Auflistung, falls mehr als eine vorhanden ist.  
  
-   Jedes Element innerhalb der Tabellenstruktur nimmt eine einzelne Zelle ein.  
  
-   Leere Zellen werden so weit wie möglich reduziert, um die Größe der HTML-Datei zu reduzieren.  
  
-   Eine Reihe leerer Zellen wird dem oberen Rand und eine weitere Spalte dem linken Rand hinzugefügt, um die Geschwindigkeit, mit der Browser die Tabelle rendern können, zu erhöhen.  
  
-   Tabellenzeilen oder -spalten, die keine Elemente, sondern nur Lücken zwischen Elementen enthalten, erhalten eine feste Breite und Höhe.  
  
-   Allen anderen Zeilen und Spalten können abhängig von der Größe der einzelnen Berichtselemente zunehmen.  
  
-   Alle Koordinaten und Berichtselementgrößen werden in Millimeter konvertiert. Alle anderen Größen, einschließlich der Stileigenschaften, behalten ihre ursprünglichen Einheiten bei. Größen- und Positionsunterschiede, die kleiner als 0,2 mm sind, werden als 0 mm behandelt.  
  
  
##  <a name="Interactivity"></a> Interaktivität  
 Einige interaktive Elemente werden in HTML unterstützt. Im Folgenden werden spezifische Funktionsweisen beschrieben.  
  
### <a name="show-and-hide"></a>Einblenden und Ausblenden  
 Ein Berichtselement, das ein- und ausgeblendet werden kann, wird mit einem Bild zum Umschalten (+/-) gerendert. Auf dieses Element kann geklickt werden. Wenn auf das Element geklickt wird, erfolgt ein Rückruf an den Server, um die Ausgabe mit dem geänderten aktuellen Ansichtsstatus erneut zu rendern.  
  
### <a name="document-map"></a>Dokumentstruktur  
 Dokumentstrukturbezeichnungen werden gerendert und sind navigierbar. Verwenden Sie dazu die Dokumentstruktur im Steuerelement für den Viewer. Für ausgelassene Datenbereichskopfzeilen werden Bezeichnungen auf der ersten untergeordneten Zelle gerendert. Wenn keine untergeordnete Zelle vorhanden ist, wird die Bezeichnung auf dem untergeordneten Element gerendert, das ihm vorausgeht.  
  
### <a name="bookmarks"></a>Lesezeichen  
 Lesezeichenlinks werden gerendert und als Links angezeigt. Lesezeichenziele werden gerendert. Die Navigation zu diesen Zielen erfolgt durch Klicken auf die Lesezeichenlinks. Beim Klicken auf einen Lesezeichenlink springt der Bericht zum ersten Auftreten der Ziellesezeichenbezeichnung, sofern möglich. Im Browser wird ein Bildlauf durchgeführt, sodass sich der Lesezeichenlink oben im Fenster befindet. HTML-Anker (\<eine >) Tags werden verwendet, um Lesezeichenziele zu markieren.  
  
### <a name="interactive-sorting"></a>Interaktives Sortieren  
 Bei einem Textfeld mit benutzerdefinierter Sortierung rendert die HTML-Renderingerweiterung die Sortiersymbole im Textfeld rechts vom Inhalt. Wenn ein Bericht ein Textfeld mit benutzerdefinierter Sortierung enthält, wird JavaScript gerendert, was zu einem Postback zum Server führt, wenn das Sortiersymbol angeklickt wird.  
  
### <a name="hyperlinks-and-drillthrough"></a>Links und Drillthroughlinks  
 Hyperlinks und Drillthroughlinks werden als Links für die HTML-Anker mit Berichtselemente gerendert (\<eine >) um das Element, auf dem sie definiert sind.  
  
### <a name="search"></a>Suchen  
 Die Suchfunktion ermöglicht es Benutzern, nach einer Textzeichenfolge innerhalb des Berichts zu suchen.  
  
 Zusätzliche Suchfunktionen werden vom ReportViewer Web Forms-Steuerelement bereitgestellt.  
  
  
##  <a name="DeviceInfo"></a> Geräteinformationseinstellungen  
 Sie können einige Standardeinstellungen für diesen Renderer ändern, einschließlich des Modus für das Rendern. Ändern Sie dazu die Geräteinformationseinstellungen. Weitere Informationen finden Sie unter [HTML Device Information Settings](../../reporting-services/html-device-information-settings.md).  
  
  
## <a name="see-also"></a>Siehe auch  
 [Paginierung in Reporting Services &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Renderingverhalten &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Interaktive Funktionalität für verschiedene Bericht Rendern von Erweiterungen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Rendern von Berichtselementen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
