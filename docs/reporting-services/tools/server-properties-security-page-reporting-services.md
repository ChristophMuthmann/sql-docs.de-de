---
title: "Servereigenschaften (Seite „Sicherheit“) – Reporting Services | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/10/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
caps.latest.revision: "11"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9fd7681e1628b493fa7c1864d2b6010e7d78d62d
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="server-properties-security-page---reporting-services"></a>Servereigenschaften (Seite Sicherheit) – Reporting Services
  Verwenden Sie diese [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Seite in [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] , um Funktionen zu deaktivieren, die potenziell einen Berichtsserver gefährden können. Die Deaktivierung dieser Funktionen führt zu einigen Funktionseinschränkungen, kann jedoch die Gesamtsicherheit durch Verringerung bestimmter Bedrohungen erhöhen.  
  
 So öffnen Sie diese Seite
 1) Starten Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2) Stellen Sie eine Verbindung mit einer Berichtsserverinstanz her.
 3) Klicken Sie mit der rechten Maustaste auf den Berichtsservernamen, und wählen Sie **Eigenschaften**aus. 
 4) Klicken Sie auf **Sicherheit** , um diese Seite zu öffnen.  
  
## <a name="options"></a>Tastatur  
 **Integrierte Sicherheit von Windows für Berichtsdatenquellen-Verbindungen aktivieren**  
 Geben Sie an, ob eine Verbindung mit einer Berichtsdatenquelle mithilfe des Windows-Sicherheitstokens des Benutzers hergestellt werden kann, der den Bericht angefordert hat.  
  
 Wenn Sie diese Funktion deaktivieren, ist die Funktion Integrierte Sicherheit von Windows in der Eigenschaftenseite der Berichtsdatenquelle nicht mehr verfügbar. Wenn Berichtsdatenquellen für die integrierte Sicherheit von Windows konfiguriert werden, und Sie dann diese Funktion deaktivieren, aktualisiert der Berichtsserver sofort die Datenverbindungseigenschaften aller Datenquellen so, dass sie Anmeldeinformationen anfordern.  
  
 **Ad-hoc-Berichterstellung aktivieren**  
 Geben Sie an, ob Benutzer Ad-hoc-Abfragen von einem Bericht des Berichts-Generators ausführen können, wodurch automatisch neue Berichte generiert werden, sobald ein Benutzer auf die ihn interessierenden Daten klickt.  
  
 Durch Festlegen dieser Option wird bestimmt, ob der Wert der **EnableLoadReportDefinition** -Eigenschaft auf **True** oder **False**festgelegt wird. Wenn Sie diese Option deaktivieren, wird die Eigenschaft auf **False** festgelegt, und der Berichtsserver generiert keine Berichte mit Durchklicken für Berichte, die während des Durchsuchens der Daten erstellt werden. Alle Aufrufe der **LoadReportDefinition** -Methode werden blockiert.  
  
 Die Deaktivierung dieser Option führt zu einem Sicherheitsrisiko, weil böswillige Benutzer einen Denial-of-Service-Angriff ausführen können, bei dem der Berichtsserver mit **LoadReportDefinition** -Anforderungen überlastet wird.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Festlegen von Berichtsservereigenschaften &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Vorgehensweise: Herstellen einer Verbindung mit einem Berichtsserver in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Berichtsserver im Management Studio (F1-Hilfe)](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
