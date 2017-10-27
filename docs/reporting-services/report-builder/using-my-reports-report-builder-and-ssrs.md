---
title: Verwenden von Meine Berichte (Berichts-Generator und SSRS) | Microsoft Docs
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
ms.assetid: 49c3c1da-b106-41f6-9173-16ff225bade8
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: fc31861f7eef73a2ddb88faa4aa59b1bf289d2ea
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="using-my-reports-report-builder-and-ssrs"></a>Verwenden von Meine Berichte (Berichts-Generator und SSRS)
  Auf einem Berichtsserver, der im einheitlichen Modus konfiguriert ist, ist der Ordner Meine Berichte ein persönlicher Arbeitsbereich, in dem Sie Ihre eigenen Berichte speichern und verwenden können. Andere Berichtsserverordner sind öffentliche Ordner, für die Benutzer in der Regel erweiterte Berechtigungen zum Hinzufügen oder Ändern von Ordnerinhalten benötigen. Demgegenüber ist der Ordner Meine Berichte ein vom Benutzer verwalteter Arbeitsbereich. Mit personalisierten Einstellungen können Sie Berichte und Ordner hinzufügen oder entfernen und verknüpfte Berichte speichern.  
  
 Vom Prinzip her ist der Ordner Meine Berichte mit dem Ordner Meine Dateien des Windows-Dateisystems zu vergleichen. Zwar gibt es für jeden Benutzer einen Ordner Meine Berichte, jeder Benutzer greift jedoch auf einen anderen Ordner zu. Mit Ausnahme der Berichtsserveradministratoren haben andere Benutzer keinen Zugriff auf Ihren Ordner Meine Berichte.  
  
 Die Funktion Meine Berichte ist optional und kann von einem Berichtsserveradministrator deaktiviert werden. Wenn die Funktion aktiviert ist, wird ein Ordner Meine Berichte im Ordner Home angezeigt, den Sie mithilfe des Berichts-Managers oder einem Webbrowser öffnen können. Weitere Informationen finden Sie unter [suchen und Anzeigen von Berichten im Berichts-Manager &#40; Berichts-Generator und SSRS &#41; ](finding-and-viewing-reports-with-a-browser-report-builder-and-ssrs.md).  
  
 Auf einem Berichtsserver, der im integrierten SharePoint-Modus konfiguriert ist, gibt es kein Äquivalent für den Ordner Meine Berichte. Weitere Informationen finden Sie unter [Suchen, Anzeigen und Verwalten von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="ways-to-use-my-reports"></a>Verwendungsmöglichkeiten von Meine Berichte  
 Meine Berichte ist bis zum Hinzufügen von Berichten, Ordnern und sonstigen Elementen leer. Es gibt folgende Möglichkeiten, um Inhalt zu Meine Berichte hinzuzufügen.  
  
-   Erstellen Sie einen persönlichen verknüpften Bericht, und speichern Sie ihn in Meine Berichte. Nicht alle Berichte können verknüpft werden. Weitere Informationen finden Sie unter [Erstellen eines verknüpften Berichts](../../reporting-services/reports/create-a-linked-report.md).  
  
-   Laden Sie eine Berichtsdefinitionsdatei (RDL), Berichtsmodelldatei (SMDL) oder andere Dateien aus dem Dateisystem hoch. Sie können zwar jede beliebige Datei hochladen, der Berichtsserver verarbeitet jedoch nur Berichtsdateien mit der Dateierweiterung .rdl oder.smdl. Weitere Informationen finden Sie unter Berichtsdefinitionen"in der [Reporting Services-Dokumentation](http://go.microsoft.com/fwlink/?linkid=121312) in SQL Server-Onlinedokumentation und [Hochladen einer Datei oder eines Berichts &#40; Berichts-Manager &#41; ](../../reporting-services/reports/upload-a-file-or-report-report-manager.md).  
  
-   Erstellen und veröffentlichen Sie Ihre eigenen Berichte in Meine Berichte. Weitere Informationen finden Sie unter [Berichtsentwurfsansicht &#40; Berichts-Generator &#41; ](../../reporting-services/report-builder/report-design-view-report-builder.md).  
  
 Gewöhnlich können Sie mit Berechtigungen für Meine Berichte den Ordner selbst verwalten. Der Berichtsserveradministrator legt letztlich fest, welche Aufgaben die Benutzer ausführen können. Wenn Sie durch unzureichende Berechtigungen Probleme beim Verwenden von Meine Berichte haben, wenden Sie sich an den Berichtsserveradministrator.  
  
## <a name="searching-my-reports"></a>Durchsuchen von Meine Berichte  
 Beim Durchsuchen einer Berichtsserver-Datenbank werden die Inhalte des Ordners Meine Berichte in die Suche einbezogen, während die Inhalte der Ordner Meine Berichte von anderen Benutzern ausgeschlossen werden. In den Suchergebnissen werden nur die Berichte aufgeführt, auf die Sie Zugriff haben.  
  
## <a name="see-also"></a>Siehe auch  
 [Suchen, Anzeigen und Verwalten von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  

