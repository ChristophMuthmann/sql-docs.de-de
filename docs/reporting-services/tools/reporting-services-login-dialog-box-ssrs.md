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
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords: sql13.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
caps.latest.revision: "31"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: db595388a1970fa37cf19dca00a58b4c4f2704ed
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Reporting Services-Anmeldung (Dialogfeld) (SSRS)
  Verwenden Sie das Dialogfeld **Reporting Services-Anmeldung** , um die Anmeldeinformationen zum Veröffentlichen von Berichten auf dem Berichtsserver bereitzustellen.  
  
-   **Hinweis** : Wenn dies das erste Mal seit Festlegen der Bereitstellungseigenschaft **TargetServerURL** für ein Projekt ist, dass Sie einen Bericht auf einem Berichtsserver veröffentlichen, vergewissern Sie sich, dass der angegebene Servername **Server** anstatt **Berichte**enthält. Beispiel: `http://localhost/reportserver`und nicht das Format `http://localhost/reports`. Durch Angeben des `reports` -Verzeichnisses auf dem lokalen Server anstelle des `reportserver` -Verzeichnisses wird indirekt bewirkt, dass dieses Dialogfeld geöffnet wird. Weitere Informationen zum Festlegen von **TargetServerURL** finden Sie unter [Festlegen von Bereitstellungseigenschaften (Reporting Services)](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
## <a name="options"></a>Tastatur  
 **Server**  
 Zeigt den Namen des Berichtsservers an. Beispiel: `http://localhost/reportserver`. Für Berichtsserver, die einen anderen Port verwenden als Standardport 80, schließen Sie die Portnummer ein. Beispiel: `http://localhost:81/reportserver`.  
  
 **User name**  
 Geben Sie den Benutzernamen ein, der beim Anmelden am Webdienst verwendet werden soll.  
  
 **Kennwort**  
 Geben Sie das Kennwort ein, das beim Anmelden am Webdienst verwendet werden soll.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen (Berichts-Generator und SSRS)](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Report Designer F1 Help (Berichts-Designer (F1-Hilfe))](../../reporting-services/tools/report-designer-f1-help.md)  
  
  
