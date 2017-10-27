---
title: "Entwurf oder erst Daten zuerst für die Erstellung in der mobilen Reporting Services-Berichte | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 02/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7b355fa-312b-4074-bc9b-776269d4fb51
caps.latest.revision: 17
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8cf203f17ac149825e0e4d79ed7f6f6041700ae4
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="design-first-or-data-first-when-creating-in-reporting-services-mobile-reports"></a>Beim Erstellen von mobilen Reporting Services-Berichten wahlweise mit Entwurf oder Daten beginnen
  
Mit [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)]können Sie schnell mobile Berichte erstellen, die sich problemlos an jede Bildschirmgröße anpassen. Das Tool bietet eine Entwurfsoberfläche mit anpassbaren Rasterzeilen und flexiblen Elementen für mobile Berichte.   
  
Beim Erstellen von mobilen Berichten können Sie zwischen zwei grundlegenden Ansätzen wählen: beginnen Sie mit den Daten, oder beginnen Sie mit dem Entwurf. [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] unterstützt beides.   
  
## <a name="design-first"></a>Erst Entwurf  
  
Die folgende Abbildung zeigt die Komponenten der Layoutansicht von [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] :   
  
![SS_MRP_LayoutTab](../../reporting-services/mobile-reports/media/ss-mrp-layouttab.png)  
  
Wenn Sie erst den Entwurf erstellen, erstellen Sie zunächst ein Layout für den mobilen Bericht, ohne Daten zu importieren. Dies ist eine gute Möglichkeit, um einen mobilen Bericht zu erstellen, wenn Sie nicht sicher sind, ob die Daten korrekt formatiert sind. Ohne echte Daten sind Katalogelemente automatisch an generierte simulierte Daten gebunden. Diese können Sie exportieren und als Vorlage verwenden, um die erforderlichen Daten zu beschreiben.  
  
## <a name="data-first"></a>Erst Daten  
Wenn Sie erst die Daten verarbeiten, importieren Sie zunächst alle erforderlichen Daten. Entwerfen Sie anschließend den mobilen Bericht, und legen Sie Dateneigenschaften auf die Elemente des mobilen Berichts fest. Dies hat den Vorteil, dass jedes Element mit echten Daten verknüpft werden kann, wenn Sie es dem Layout hinzufügen. Wenn Sie zuerst Daten verarbeiten, stellen Sie sicher, dass Ihre echten Daten für die Verwendung mit [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)]korrekt formatiert sind.   
  
 Die folgende Abbildung zeigt alle Komponenten der Datenansicht von [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] :  
  
![SS_MRP_DataTab](../../reporting-services/mobile-reports/media/ss-mrp-datatab.png)  
  
### <a name="see-also"></a>Siehe auch  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Erstellen und Veröffentlichen von mobilen Berichten mit dem Publisher für mobile Berichte von SQL Server)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  Anzeigen von [mobilen SQL Server-Berichten und KPIs in der iPad-App](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI für iOS)  
-  Anzeigen von [mobilen SQL Server-Berichten und KPIs in der iPhone-App](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI für iOS)  
  
  
  
  


