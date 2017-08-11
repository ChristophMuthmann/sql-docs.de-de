---
title: Drilldownaktion (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10249"
- "10186"
- "10092"
- "10167"
- "10174"
- sql13.rtp.rptdesigner.charttitleproperties.visibility.f1
- "10155"
- sql13.rtp.rptdesigner.chartproperties.visibility.f1
- sql13.rtp.rptdesigner.pictureproperties.visibility.f1
- sql13.rtp.rptdesigner.majorgridlineproperties.visibility.f1
- "10123"
- "10425"
- sql13.rtp.rptdesigner.axisproperties.visibility.f1
- "10217"
- "10161"
- "10215"
- sql13.rtp.rptdesigner.legendproperties.visibility.f1
- "10258"
- "10144"
- sql13.rtp.rptdesigner.subreportproperties.visibility.f1
- sql13.rtp.rptdesigner.textboxproperties.visibility.f1
- "10062"
- sql13.rtp.rptdesigner.serieslabelproperties.visibility.f1
- sql13.rtp.rptdesigner.rectangleproperties.visibility.f1
- sql13.rtp.rptdesigner.calculatedseriesproperties.visibility.f1
- sql13.rtp.rptdesigner.chartareaproperties.visibility.f1
- "10053"
- sql13.rtp.rptdesigner.minorgridlineproperties.visibility.f1
- sql13.rtp.rptdesigner.seriesproperties.visibility.f1
ms.assetid: 1f8d1ef2-0daf-40c6-9ba7-3b391249bcd4
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 10cbda042d03d5405c136894017418e341665c99
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="drilldown-action-report-builder-and-ssrs"></a>Drilldownaktion (Berichts-Generator und SSRS)
  Durch die Bereitstellung von Plus- oder Minussymbolen für ein Textfeld können Sie Benutzern das interaktive Aus- und Einblenden von Elementen ermöglichen. Dies wird als *Drilldownaktion* bezeichnet. Für eine Tabelle oder Matrix können Sie statische Zeilen und Spalten oder Zeilen und Spalten ein- und ausblenden, die Gruppen zugeordnet sind.  
  
 ![Rs_drilldown](../../reporting-services/report-design/media/rs-drilldown.gif "Rs_drilldown")  
  
 In dieser Abbildung klickt der Benutzer im Bericht auf die Pluszeichen (+), um Detaildaten anzuzeigen.  
  
 Sie können für eine Tabelle mit Zeilengruppen z. B. anfänglich alle Zeilen mit Ausnahme der äußeren Gruppenzusammenfassungszeile ausblenden. Fügen Sie für jede innere Gruppe (einschließlich der Detailgruppe) der Gruppierungszelle der enthaltenden Gruppe ein Symbol zum Erweitern/Reduzieren hinzu. Beim Rendern des Berichts kann der Benutzer auf das Textfeld klicken, um die Detaildaten zu erweitern und zu reduzieren. Weitere Informationen finden Sie unter [Tabellen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md).  
  
 Zu diesem Zweck legen Sie die Sichtbarkeitseigenschaften eines Elements fest, das von Benutzern erweitert oder reduziert werden soll.  
  
> [!NOTE]  
>  Wenn Sie einen Bericht mit einer Drilldownaktion erstellen, müssen die Sichtbarkeitsinformationen nicht nur für ein einzelnes Textfeld in der Zeile oder Spalte, sondern für die auszublendende Gruppe, Zeile oder Spalte und festgelegt werden. Darüber hinaus muss sich das für die Umschaltfläche verwendete Textfeld in einem enthaltenden Bereich befinden, der das aus- bzw. einzublendende Element steuert.  
>   
>  Wenn Sie z. B. eine Zeile ausblenden möchten, die einer geschachtelten Gruppe zugeordnet ist, muss sich das Textfeld in einer Zeile befinden, die der übergeordneten Gruppe oder einem Element an höherer Stelle in der Kapselungshierarchie zugeordnet ist.  
>   
>  Informationen zum Festlegen der Sichtbarkeitsinformationen für die Gruppe, Zeile oder Spalte, finden Sie unter [Hinzufügen einer Erweiterungs- oder Reduzieraktion zu einem Element &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)  
  
 Weitere Informationen zum Ausblenden von Berichtselementen finden Sie unter [Ausblenden eines Elements &#40; Berichts-Generator und SSRS &#41; ](../../reporting-services/report-builder/hide-an-item-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="comparing-drilldown-and-drillthrough-reports"></a>Vergleichen von Drilldown- und Drillthroughberichten  
 In einem Drilldownbericht klickt ein Benutzer auf eine Plus- oder Minusschaltfläche, um einen Abschnitt eines Berichts zu erweitern oder zu reduzieren und so Detaildaten anzuzeigen. In einem Drillthroughbericht klickt der Benutzer auf einen Link für einen Zusammenfassungswert, wodurch ein separater, zugehöriger Bericht zum Anzeigen von Detaildaten geöffnet wird. Die Detaildaten werden nur abgerufen, wenn der Detailbericht ausgeführt wird. Drillthroughberichte erfordern normalerweise weniger Ressourcen als Drilldownberichte. Weitere Informationen finden Sie unter [Drillthrough, Drilldown, Unterberichte und geschachtelte Datenbereiche &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md).  
  
## <a name="rendering-extension-support-for-hidden-report-items"></a>Unterstützung ausgeblendeter Berichtselemente durch Renderingerweiterungen  
 Die Umschaltfläche zum Ein- und Ausblenden von Berichtselementen wird nur von Renderingerweiterungen mit Unterstützung für Benutzerinteraktivität unterstützt, z. B. die beim Ausführen eines Berichts im Berichts-Generator und Berichts-Manager verwendete HTML-Renderingerweiterung. Bei anderen Renderingerweiterungen werden ausgeblendete Elemente angezeigt. In der folgenden Liste wird die Unterstützung von Berichtselementen mit bedingter Sichtbarkeit beschrieben:  
  
-   Wenn Elemente in HTML ausgeblendet sind, sind sie in der HTML-Quelle nicht sichtbar.  
  
-   Die XML-Renderingerweiterung zeigt alle Berichtselemente an, unabhängig davon, ob sie ausgeblendet sind.  
  
-   Die Excel-Renderingerweiterung zeigt ausgeblendete Zeilen und Spalten für eine Tabelle, Matrix oder Liste an und erweitert diese. Alle Zeilen und Spalten sind sichtbar.  
  
 Weitere Informationen finden Sie unter [Renderingverhalten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Drillthrough, Drilldown, Unterberichte und geschachtelte Datenbereiche &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)   
 [Interaktive Sortierung, Dokumentstrukturen, und Links &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
