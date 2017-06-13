---
title: Drucken von Berichten (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4bad1b6e-7d94-4b17-9502-ccd3dce0fdd9
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e57d90ca72920722ddcf16d5d5708a782db5a71f
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="print-reports-report-builder-and-ssrs"></a>Drucken von Berichten (Berichts-Generator und SSRS)
  Nach dem Speichern eines Berichts auf einem Berichtsserver können Sie diesen mit einem Browser, dem Berichts-Manager oder einer beliebigen Anwendung, die Sie zum Anzeigen eines exportierten Berichts verwenden, anzeigen und drucken. Vor dem Speichern eines Berichts können Sie ihn aus der Vorschau drucken.  
  
 Die vollständige Druckverarbeitung erfolgt bei Bedarf auf dem Clientcomputer. Es ist keine serverseitige Druckfunktionalität vorhanden, mit deren Hilfe Sie einen Druckauftrag direkt von einem Berichtsserver an einen mit dem Webserver verbundenen Drucker weiterleiten könnten. Drucker und Druckoptionen werden von den einzelnen Berichtsbenutzern mithilfe eines Standarddialogfelds **Drucken** ausgewählt.  
  
 Berichtsautoren, die Berichte speziell zur Druckausgabe entwickeln, verwenden Seitenumbrüche, Seitenkopf- und -fußzeilen, Ausdrücke und Hintergrundbilder zum Erstellen eines druckbasierten Entwurfs. Ein Beispiel für Berichtsentwurfselemente für die Druckausgabe können Bedingungen sein, die auf der Rückseite jedes Berichts gedruckt werden, oder Grafik- und Textelemente, die einem Briefkopf entsprechen.  
  
 Aufgrund der Paginierungsimplementierung für unterschiedliche Renderingformate ist es u. U. nicht möglich, für jedes Renderingformat optimale Druckausgabeergebnisse zu erzielen. Die folgende Liste beinhaltet Beispiele:  
  
1.  Berichtsseiten können unterschiedliche Datenmengen enthalten. Berichte mit einer Matrix können z. B. sowohl horizontal als auch vertikal vergrößert werden, wenn ein Benutzer die Zeilen und Spalten interaktiv ein- und ausblendet. Ein Benutzer, der die Matrix nicht erweitert, erhält andere Druckergebnisse als ein Benutzer, der die Matrix erweitert.  
  
2.  Seiten mit Quer- und Hochformat können nicht in einem Bericht kombiniert werden. Auch das Erstellen eines druckbasierten Layouts, das das Layout eines in einem Browser oder einer anderen Anwendung gerenderten Berichts ersetzt oder neben diesem vorhanden ist, ist nicht möglich.  
  
3.  Die meisten Ausdrucke von exportierten Berichten enthalten alle sichtbaren Elemente eines Berichts, die dem Benutzer auf einem Computerbildschirm angezeigt werden. Leerraum auf der Entwurfsoberfläche für Berichte wird beibehalten. Um zusätzliche leere Seiten horizontal hinzuzufügen oder zu entfernen, ändern Sie die Breite der Berichtsseiten.  
  
> [!NOTE]  
>  Berichtsausdrucke im HTML-Format enthalten möglicherweise nur den Inhalt der ersten Seite, wenn der Befehl des Browsers zum Drucken verwendet wird. Es können bessere Ergebnisse erzielt werden, wenn Sie HTML-Berichte mit der Clientdruckfunktionalität von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] drucken. Weitere Informationen finden Sie unter [Drucken von Berichten in einem Browser mit dem Drucksteuerelement &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Drucken von Berichten in einem Browser mit dem Drucksteuerelement &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)  
 Beschreibt die Verwendung des clientseitigen Druckens zum Drucken von Berichten mit dem Webbrowser oder Berichts-Manager.  
  
 [Drucken von Berichten aus anderen Anwendungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/print-reports-from-other-applications-report-builder-and-ssrs.md)  
 Beschreibt das Drucken von in eine andere Anwendung exportierten Berichten.  
  
 [Drucken eines Berichts &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)  
 Enthält schrittweise Anweisungen zum Drucken eines Berichts, Steuern der Ränder einer Seite und Festlegen des Papierformats für Berichte, die von Renderern mit festem Seitenumbruch gerendert werden: PDF, Bild oder Drucken.  
  
## <a name="see-also"></a>Siehe auch  
 [Exportieren von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Seitenkopf- und Seitenfußzeilen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Bilder &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [Paginierung in Reporting Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)  
  
  
