---
title: Reporting Services-Anmeldung (Dialogfeld) (SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords: sql13.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
caps.latest.revision: "31"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 46196cc377ff2080250c511fb1c901641e4c84cd
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Reporting Services-Anmeldung (Dialogfeld) (SSRS)
  Verwenden Sie das Dialogfeld **Reporting Services-Anmeldung** , um die Anmeldeinformationen zum Veröffentlichen von Berichten auf dem Berichtsserver bereitzustellen.  
  
-   **Hinweis** : Wenn dies das erste Mal seit Festlegen der Bereitstellungseigenschaft **TargetServerURL** für ein Projekt ist, dass Sie einen Bericht auf einem Berichtsserver veröffentlichen, vergewissern Sie sich, dass der angegebene Servername **Server** anstatt **Berichte**enthält. Beispiel: `http://localhost/reportserver`und nicht das Format `http://localhost/reports`. Durch Angeben des `reports` -Verzeichnisses auf dem lokalen Server anstelle des `reportserver` -Verzeichnisses wird indirekt bewirkt, dass dieses Dialogfeld geöffnet wird. Weitere Informationen zum Festlegen von **TargetServerURL** finden Sie unter [Festlegen von Bereitstellungseigenschaften (Reporting Services)](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
## <a name="options"></a>enthalten  
 **Server**  
 Zeigt den Namen des Berichtsservers an. Beispiel: `http://localhost/reportserver`. Für Berichtsserver, die einen anderen Port verwenden als Standardport 80, schließen Sie die Portnummer ein. Beispiel: `http://localhost:81/reportserver`.  
  
 **Benutzername**  
 Geben Sie den Benutzernamen ein, der beim Anmelden am Webdienst verwendet werden soll.  
  
 **Kennwort**  
 Geben Sie das Kennwort ein, das beim Anmelden am Webdienst verwendet werden soll.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Report Designer F1 Help (Berichts-Designer (F1-Hilfe))](../../reporting-services/tools/report-designer-f1-help.md)  
  
  
