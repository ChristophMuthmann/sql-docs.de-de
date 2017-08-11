---
title: Drucken eines Berichts (Reporting Services im SharePoint-Modus) | Microsoft Docs
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
helpviewer_keywords:
- printing reports, SharePoint Web application
- printing reports
ms.assetid: 026784f7-8cb4-4351-93ee-230b2ab0f8f5
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f89c8f0d330561aacd678e4556fdaf2910b5dcc7
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="print-a-report-reporting-services-in-sharepoint-mode"></a>Drucken eines Berichts (Reporting Services im SharePoint-Modus)
  Bei einem Berichtsserver, der im SharePoint-Modus ausgeführt wird, gibt es drei Möglichkeiten zum Drucken eines Berichts aus einer SharePoint-Webanwendung:  
  
-   **Von einer SharePoint-Website** Wählen Sie im Menü **Aktionen** , das nach dem Öffnen des Berichts in der Berichtssymbolleiste angezeigt wird, die Option **Drucken** aus. Dadurch wird die Druckfunktionalität in Reporting Services bereitgestellt, die ein standardmäßiges Dialogfeld **Drucken** einschließt, das zum Auswählen eines Druckers, zum Angeben von Seiten und Rändern und zum Anzeigen einer Vorschau des Berichts verwendet wird. Diese Druckfunktionen kann anstelle des Befehls Drucken im Browsermenü Datei verwendet werden. Beim Verwenden dieses Funktionen wird der Bericht gemäß seines Entwurfs gedruckt, ohne zusätzliche Elemente, die im Ausdruck einer Webseite zu finden sind.  
  
-   **Aus einem Browser** Die Druckfunktionen eines Browsers eignen sich am besten für HTML-Berichte, die auf eine einzelne Seite passen. In der Regel enthalten die von einem Browser gedruckten Seiten alle visuellen Elemente einer Webseite, dazu Kopf- und Fußzeileninformationen zur Identifikation der Seite oder Website. Beim Drucken von einem Browser aus wird nur der Inhalt des aktuellen Fensters gedruckt. Wenn der Bericht umfangreich ist, wird vom Browser nur ein Teil des Berichts gedruckt (in der Regel nur die erste Seite).  
  
-   **Aus einer Zielanwendung** Sie können einen Bericht exportieren, um die Druckfunktionen einer Zielanwendung (z. B. Microsoft Office Excel oder Adobe Acrobat Reader) zu verwenden. Einige Anwendungsformate (z. B. TIFF oder PDF) eignen sich hervorragend zum Drucken von mehrseitigen Berichten. Wenn Sie einen Bericht in eine Desktopanwendung exportieren, können Sie beliebige spezialisierte Druckfunktionen verwenden, die von der Anwendung bereitgestellt werden. Wählen Sie im Menü **Aktionen** , das nach dem Öffnen des Berichts auf der Berichtssymbolleiste angezeigt wird, die Option **Exportieren** aus, um einen Bericht zu exportieren.  
  
> [!NOTE]  
>  Wenn Sie einen Bericht drucken möchten, müssen Sie über Berechtigungen zum Anzeigen des Berichts verfügen.  
  
 Verwenden Sie im Menü **Aktionen** die Option **Drucken** , um bestmögliche Ergebnisse beim Drucken eines Berichts von einer Webseite zu erzielen. Die Aktion **Drucken** ist an ein Clientdrucksteuerelement gebunden, das vom Berichtsserver heruntergeladen wird. Der Download erfolgt, wenn Sie **Drucken**zum ersten Mal auswählen.  
  
 Berichtsautoren können Berichte speziell für die Druckausgabe oder für ein bestimmtes Anwendungsformat entwerfen. Beachten Sie, dass aufgrund der Art, wie die Paginierung für unterschiedliche Anwendungsformate implementiert ist, u. U. nicht für jeden Bericht in jedem Anwendungsformat optimale Druckausgabeergebnisse erzielt werden können. Im Gegensatz zu Berichten, die für die Druckausgabe entworfen wurden, können für die Bildschirmausgabe entworfene Berichtsseiten unterschiedliche Mengen von Daten enthalten. Beispielsweise kann eine Seite in Berichten mit einer Matrix sowohl horizontal als auch vertikal vergrößert werden, wenn Sie die Zeilen und Spalten erweitern. Beim Drucken eines Berichts mit variabler Größe erhält ein Benutzer, der die Matrix nicht erweitert, andere Druckergebnisse als ein Benutzer, der die Matrix erweitert. Die meisten Ausdrucke von exportierten Berichten enthalten alle sichtbaren Elemente eines Berichts, die dem Benutzer auf einem Computerbildschirm angezeigt werden.  
  
### <a name="how-to-print-reports-from-the-actions-menu"></a>Drucken von Berichten mithilfe des Menüs Aktionen  
  
1.  Öffnen Sie den Bericht.  
  
2.  Klicken Sie im Menü **Aktionen** auf **Drucken**. Wenn das Menü **Aktionen** nicht angezeigt wird, ist die Berichtssymbolleiste ausgeblendet, und Sie können die auf ihr bereitgestellten Funktionen nicht verwenden. Wenn das Menü **Aktionen** angezeigt wird, aber die Option **Drucken** nicht verfügbar ist, wurde die Druckfunktionalität auf dem Berichtsserver deaktiviert, und Sie können sie nicht verwenden.  
  
3.  Wählen Sie im Dialogfeld **Drucken** den gewünschten Drucker und die gewünschten Optionen aus, und klicken Sie auf **OK**.  
  
     Klicken Sie auf die Schaltfläche **Eigenschaften** , um die Standardeinstellungen zu ändern. Die Seitengröße wird durch die Standardhöhe und -breite der Berichtsseitengröße gemäß der Berichtsdefinition bestimmt. Wie weit Sie die Seitendimensionen ändern können, hängt von den Möglichkeiten des verwendeten Druckers ab.  
  
     Klicken Sie auf die Schaltfläche **Vorschau** , um den Bericht vor dem Drucken anzuzeigen. Dadurch wird die erste Seite des Berichts in einem separaten Vorschaufenster geöffnet. Weitere Seiten werden beim Rendern des Berichts auf dem Berichtsserver verfügbar. Ein als Vorschau angezeigter Bericht wird im EMF-Format gerendert. Sie können zur vorherigen oder nächsten Seite navigieren, bis die letzte Seite erreicht ist. Dann ist die Schaltfläche **Weiter** deaktiviert. Klicken Sie auf die Schaltfläche **Ränder** , um die Druckränder auf der Vorschauseite zu ändern. Das Dialogfeld **Ränder** wird angezeigt. Konfigurieren Sie den oberen, unteren, rechten und linken Rand, und klicken Sie auf **OK**. Das Dialogfeld wird geschlossen, und die Einstellungen werden für die Renderingvorschau und den Druckvorgang gespeichert.  
  
## <a name="see-also"></a>Siehe auch  
 [Aktivieren Sie und deaktivieren Sie des clientseitige Drucks für Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)  
  
  
