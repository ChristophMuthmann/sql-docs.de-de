---
title: "Servereigenschaften (Seite Ausführung) | Microsoft Docs"
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
f1_keywords:
- sql13.swb.reportserver.serverproperties.execution.f1
ms.assetid: 53b77db1-b013-4dac-82dd-30c0de276639
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 933f3287d8e02df8aeadf93bbd7ce39f20aff268
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="server-properties-execution-page"></a>Servereigenschaften (Seite Ausführung)
  Verwenden Sie diese Seite zum Festlegen eines Timeoutwertes für die Berichtsausführung. Dieser Wert gilt für alle Berichte, die von der aktuellen Berichtsserverinstanz verarbeitet werden. Sie können diesen Wert für einzelne Berichte überschreiben. Der von Ihnen angegebene Wert muss die gesamte Berichtsverarbeitung auf dem Berichtsserver berücksichtigen, plus der Abfrageverarbeitung, die auf dem Datenbankserver durchgeführt wird, wenn der Berichtsserver die im Bericht verwendeten Daten abruft.  
  
 Öffnen Sie diese Seite, indem Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]starten und eine Verbindung mit einer Berichtsserverinstanz herstellen. Klicken Sie mit der rechten Maustaste auf den Namen des Berichtsservers, und wählen Sie dann **Eigenschaften**aus. Klicken Sie auf **Ausführung** , um diese Seite zu öffnen.  
  
## <a name="options"></a>enthalten  
 **Kein Timeout für eine Berichtsausführung**  
 Stellt einem Berichtsserver eine uneingeschränkte Zeitspanne für die Berichtsverarbeitung zur Verfügung.  
  
 **Berichtsausführung auf die folgende Anzahl von Sekunden beschränken**  
 Legt eine Zeitbeschränkung für die Berichtsausführung fest. Diese Zeitspanne beginnt, wenn der Bericht angefordert wird. Wenn diese Zeitspanne endet, bevor der Bericht vollständig verarbeitet wurde, bricht der Berichtsserver den Vorgang und alle in Bearbeitung befindlichen Abfragen externer Datenquellen ab.  
  
## <a name="see-also"></a>Siehe auch  
 [Festlegen von Berichtsservereigenschaften &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Vorgehensweise: Herstellen einer Verbindung mit einem Berichtsserver in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Festlegen von Berichtsverarbeitungseigenschaften](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Festlegen von Timeoutwerten für die Verarbeitung von Berichten und freigegebenen Datasets &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)   
 [Berichtsserver im Management Studio (F1-Hilfe)](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
