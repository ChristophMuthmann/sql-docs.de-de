---
title: "Verschieben oder Löschen eines Elements (Berichts-Manager) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- moving items
- items [Reporting Services], moving
ms.assetid: 980a66c7-a18b-4af7-8954-45726fa517d6
caps.latest.revision: "45"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3167bcbe85165f390ab2fd3369abf5511e26cd2b
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="move-or-delete-an-item-report-manager"></a>Verschieben oder Löschen eines Elements (Berichts-Manager)
  Berichte und berichtsbezogene Elemente, die Sie auf einem Berichtsserver veröffentlichen, werden in Ordnern gespeichert. Sie können Elemente in einen anderen Ordner verschieben. Verweise auf diese Elemente werden automatisch vom Berichtsserver verwaltet. Bevor Sie ein Element löschen, ist zu überprüfen, ob Elemente davon abhängen.  
  
## <a name="move-an-item"></a>Verschieben eines Elements  
 Sie können Berichtsserverelemente an andere Speicherorte in der Ordnerhierarchie des Berichtsservers verschieben. Beim Verschieben eines Elements werden auch alle zugehörigen Eigenschaften (einschließlich Sicherheitseinstellungen) an den neuen Speicherort verschoben. Wenn Sie einen Ordner verschieben, werden gleichzeitig alle in diesem Ordner enthaltenen Elemente verschoben.  
  
 Im Berichts-Manager werden die verschiebbaren Elemente in der Ordnerhierarchie angezeigt. In der folgenden Tabelle sind die Symbole für die verschiedenen verschiebbaren Elemente dargestellt.  
  
|Symbol|Verschiebbares Element|  
|----------|-------------------|  
|![Berichtsymbol](../../reporting-services/report-server/media/hlp-16doc.gif "Report icon")|Bericht|  
|![Symbol verknüpfte Berichte](../../reporting-services/report-server/media/hlp-16linked.gif "Linked report icon")|Verknüpfter Bericht|  
|![Ordnersymbol](../../reporting-services/report-server/media/hlp-16folder.gif "Folder icon")|Ordner|  
|![Symbol allgemeine Ressource](../../reporting-services/report-server/media/hlp-16file.gif "generic resource icon")|Allgemeine Ressource|  
|![Symbol freigegebene Datenquelle](../../reporting-services/report-data/media/hlp-16datasource.png "Shared data source icon")|Freigegebene Datenquelle|  
||Freigegebenes Dataset|  
  
 Nicht alle Elemente, mit denen Sie arbeiten, können verschoben werden. Elemente, die einem Bericht zugeordnet sind, z. B. Abonnements oder ein Berichtsverlauf, können nicht verschoben werden. Diese Elemente werden mit den zugehörigen Berichten verschoben. Auch Elemente wie freigegebene Zeitpläne, die außerhalb der Ordnerhierarchie vorhanden sind, können nicht verschoben werden. Sie können ohne die entsprechende Berechtigung keine Elemente verschieben. Die Berechtigung zum Verschieben eines Elements wird erteilt, wenn folgende Tasks in Ihrer Rollenzuweisung für das entsprechende Element ausgewählt sind: "Berichte verwalten", "Modelle verwalten", "Ordner verwalten" und "Datenquellen verwalten".  
  
#### <a name="to-move-an-item-from-within-the-contents-page"></a>So verschieben Sie ein Element auf der Inhaltsseite  
  
1.  Starten Sie den [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Navigieren Sie im Berichts-Manager zur Seite **Inhalt** , und suchen Sie das zu verschiebende Element.  
  
3.  Zeigen Sie auf das Element, und klicken Sie auf den Dropdownpfeil.  
  
4.  Klicken Sie im Dropdownmenü auf **Verschieben**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Geben Sie für **Speicherort**den Ordner an, in den Sie das Element verschieben möchten. Sie können den vollqualifizierten Ordnernamen eingeben oder die Strukturansicht verwenden, um zum gewünschten Ordner zu navigieren.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Alternativ können Sie zum zu verschiebenden Objekt navigieren, auf **Eigenschaften**klicken, und anschließend oben auf der Seite auf **Verschieben** klicken.  
  
## <a name="delete-an-item"></a>Löschen eines Elements  
 Bevor Sie ein Element löschen, ist zu prüfen, ob es von anderen Elementen verwendet wird. Wenn Sie beispielsweise eine freigegebene Datenquelle löschen, werden Berichte und Modelle, die diese Datenquelle verwenden, nicht mehr ausgeführt. Beim Löschen eines Berichts werden auch Abonnements und der Berichtsverlauf, die mit diesem Bericht verknüpft sind, gelöscht. Abhängige Elemente für ein Element finden Sie unter [Abhängige Elemente (Seite) (Berichts-Manager)](http://msdn.microsoft.com/library/4dcfb311-e9c3-4c5d-b2e0-018d79f37d2e).  
  
#### <a name="to-delete-a-report-or-item"></a>So löschen Sie einen Bericht oder ein Element  
  
1.  Starten Sie den [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Navigieren Sie im Berichts-Manager zur Seite **Inhalt** , und suchen Sie das zu löschende Element.  
  
3.  Zeigen Sie auf das Element, und klicken Sie auf den Dropdownpfeil.  
  
4.  Klicken Sie im Dropdownmenü auf **Löschen**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Inhalt &#40;Seite, Berichts-Manager&#41;](http://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)   
 [Suchen, Anzeigen und Verwalten von Berichten (Berichts-Generator und SSRS )](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
