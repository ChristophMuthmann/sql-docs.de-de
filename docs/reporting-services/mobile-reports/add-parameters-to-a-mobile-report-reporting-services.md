---
title: "Hinzufügen von Parametern zu einem mobilen Bericht | Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 11/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 113cb057-deec-40eb-abc8-f35d3900eaa6
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6fad62a6549f4b9752bde07e39f53175768a68cb
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="add-parameters-to-a-mobile-report--reporting-services"></a>Hinzufügen von Parametern zu einem mobilen Bericht | Reporting Services
Sie können mobile [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Berichte mit Parametern erstellen, sodass Sie und die Leser des Berichts Ihre Berichte filtern können. Berichte mit Parametern können auch Ziel eines [Drillthrough aus einem Zielbericht](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)sein. 

Beginnen Sie mit einem freigegebenen Dataset mit mindestens einem Parameter, um einen mobilen Bericht mit Parametern zu erstellen. Erfahren Sie mehr über das [Erstellen von Parametern in einem freigegebenen Dataset](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  

Nachdem Sie einem mobilen Bericht Parameter hinzugefügt haben, erstellen Sie eine URL zum [Öffnen des Berichts mit Abfragezeichenfolgenparametern](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md).

1. Wählen Sie auf der oberen Leiste des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] -Webportals **Neu** > **Mobiler Bericht**aus.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. Wählen Sie in der linken oberen Ecke von **die Registerkarte** Daten [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]aus.   
  
3. Wählen Sie in der oberen rechten Ecke **Daten hinzufügen**aus.  
  
4. Wählen Sie **Berichtsserver**aus, wählen Sie anschließend einen Server aus.  
  
5. Navigieren Sie zu den freigegebenen Datasets auf dem Server, und wählen Sie eines, das über Parameter verfügt.  
  
   Im Raster werden die Daten im Dataset angezeigt. Der grüne Kreis mit Klammern **{ }** kennzeichnet ein Dataset mit einem Parameter.  
     
   ![SSMRP_PforParam](../../reporting-services/mobile-reports/media/ssmrp-pforparam.png)  
  
6. Wählen Sie das Rädchen auf der Registerkarte aus, und wählen Sie dann **Param {}**aus.  
  
   ![SSMRP_ParamWheel](../../reporting-services/mobile-reports/media/ssmrp-paramwheel.png)  
  
7. Wählen Sie das Berichtselement, das Werte an den Parameter übergeben wird.  
  
   ![SSMRP_SetParam](../../reporting-services/mobile-reports/media/ssmrp-setparam.png)  
     
8. Wählen Sie **Vorschau** aus, um zu sehen, wie der Bericht dargestellt wird. In diesem Bericht verwendet die Auswahlliste den „Category“-Parameter.

   ![sql-server-mobile-report-publisher-Selection-List-View-No-Selection](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-view-no-selection.png) 
   
9. Wenn Sie einen Wert in der Auswahlliste auswählen, wird der Bericht nach diesem Wert gefiltert, in diesem Fall „Accessories“.

   ![sql-server-mobile-report-publisher-Selection-List-Category-Selected](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-category-selected.png)   
  
### <a name="see-also"></a>Siehe auch  
-  [Öffnen eines mobilen Berichts mit bestimmten Abfragezeichenfolgenparametern](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md)
-  [Drillthrough zu anderen mobilen Berichten oder URLs aus einem mobilen Bericht hinzufügen](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)
-  [Erstellen eines freigegebenen Datasets oder eingebetteten Datasets (Berichts-Generator und SSRS)](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Erstellen und Veröffentlichen von mobilen Berichten mit dem Publisher für mobile Berichte von SQL Server)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
  
  


