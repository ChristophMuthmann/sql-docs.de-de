---
title: Drucken von Berichten in einem Browser mit dem Drucksteuerelement (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 10054250-d915-4bcb-8a1d-26837db4e932
caps.latest.revision: "13"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 99405d9622cc89a1605c6aa9ee821f15844bc9ef
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs"></a>Drucken von Berichten in einem Browser mit dem Drucksteuerelement (Berichts-Generator und SSRS)
  Ein Browser ist zwar die am häufigsten verwendete Clientanwendung zum Anzeigen von Berichten, die Druckfunktionen des Browsers sind jedoch für das Drucken von Berichten nicht ideal. Die Druckfunktionen eines Browsers sind zum Drucken von Webseiten konzipiert. In der Regel enthalten die von einem Browser gedruckten Seiten alle visuellen Elemente einer Webseite, dazu Kopf- und Fußzeileninformationen zur Identifikation der Seite oder Website. Beim Drucken über einen Browser wird der Inhalt des aktuellen Fensters gedruckt. Bei mehrseitigen Berichten wird maximal die erste Seite gedruckt, möglicherweise sogar weniger, wenn die Berichtsseite die Dimensionen der gedruckten Seite übersteigt.  
  
 Wenn Sie die Druckqualität der in einem Browser angezeigten Berichte verbessern und mehrere Seiten drucken möchten, können Sie die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]bereitgestellte clientseitige Druckfunktionalität verwenden. Die clientseitige Druckfunktion stellt ein Standarddialogfeld **Drucken** bereit, das zum Auswählen eines Druckers, Angeben von Seiten und Rändern sowie zum Anzeigen einer Vorschau des Berichts vor dem Drucken verwendet wird. Verwenden Sie die clientseitige Druckfunktion anstelle des Befehls **Drucken** im Menü **Datei** des Browsers. Beim Verwenden dieser Funktion wird der Bericht gemäß seines Entwurfs gedruckt, ohne zusätzliche Elemente, die im Ausdruck einer Webseite zu finden sind.  
  
 Für den clientseitigen Druck müssen Sie ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] -ActiveX-Steuerelement installieren. Weitere Informationen finden Sie unter [Aktivieren und Deaktivieren des clientseitigen Drucks für Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="print-options"></a>Druckoptionen  
 Sie können Druckeigenschaften für Ihren Bericht konfigurieren, indem Sie im Dialogfeld **Drucken** auf die Schaltfläche **Eigenschaften** klicken. Der Wert für**Papierformat** wird durch die Standardhöhe und -breite der Berichtsseitengröße gemäß Berichtsdefinition bestimmt. Die verfügbaren Werte sind vom Druckertyp und seinen Funktionen abhängig. Für Breite und Höhe werden Standardwerte angezeigt, die durch die auf dem Computer konfigurierten Druckertreiber bestimmt werden. Nach dem Ändern dieser Werte wird der Bericht mit den neuen Abmessungen gedruckt. Die Seitenbreite und -höhe wird durch **Ausrichtung**bestimmt. Mögliche Werte sind **Hochformat** oder **Querformat**. Die angezeigte Standardausrichtung ist von der Seitenbreite und Seitenhöhe des Berichts abhängig.  
  
> [!NOTE]  
>  Das Dialogfeld **Drucken** und die Standarddruckereinstellungen für Breite, Höhe und Seitenausrichtung werden von der Berichtsdefinition bestimmt.  
  
### <a name="print-preview"></a>Seitenansicht  
 Sie können die Vorschau eines Berichts anzeigen, indem Sie im Dialogfeld **Drucken** auf die Schaltfläche **Vorschau** klicken. Durch Klicken auf Vorschau wird die erste Seite des Berichts in einem separaten Vorschaufenster geöffnet. Weitere Seiten werden beim Rendern des Berichts auf dem Berichtsserver verfügbar. Ein als Vorschau angezeigter Bericht wird im EMF-Format gerendert. Sie können zur vorherigen oder nächsten Seite navigieren, bis die letzte Seite erreicht ist. Dann ist die Schaltfläche **Weiter** deaktiviert.  
  
### <a name="adjusting-print-margins"></a>Anpassen der Druckränder  
 Sie können die Druckränder im gerenderten EMF-Bericht vor dem Drucken des Berichts ändern. Klicken Sie hierzu im Dialogfeld **Drucken** auf die Schaltfläche **Vorschau** . Klicken Sie oben auf der Vorschauseite auf die Schaltfläche **Ränder** . Das Dialogfeld Ränder wird angezeigt. Konfigurieren Sie bei Bedarf den oberen, unteren, rechten und linken Rand. [!INCLUDE[clickOK](../../includes/clickok-md.md)] Das Dialogfeld wird geschlossen, und die Einstellungen werden für die Renderingvorschau und den Druckvorgang gespeichert.  
  
## <a name="see-also"></a>Siehe auch  
 [Drucken von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [Drucken eines Berichts &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)  
  
  
