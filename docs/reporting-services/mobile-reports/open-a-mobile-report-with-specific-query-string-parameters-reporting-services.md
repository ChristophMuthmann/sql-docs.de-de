---
title: "Öffnen eines mobilen Berichts mit bestimmten Abfragezeichenfolgenparametern | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/25/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4eeb3204-e207-4ac0-aff3-bfc4926e5754
caps.latest.revision: "5"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6f7b4c90b317cbf31ce1414a9910798e149b5794
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="open-a-mobile-report-with-specific-query-string-parameters--reporting-services"></a>Öffnen eines mobilen Berichts mit bestimmten Abfragezeichenfolgenparametern | Reporting Services
Im Fall eines mobilen [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Berichts mit Parametern und einer [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] - oder [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] -Datenquelle können Sie Abfragezeichenfolgenparameter in die Berichts-URL aufnehmen, sodass der Bericht automatisch mit den von Ihnen angegebenen Werten geöffnet wird. 
1.  Erstellen eines [mobilen Berichts mit Parametern](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md).

2. Öffnen Sie den Bericht im Publisher für mobile Berichte, und wählen Sie die Registerkarte „Daten“ aus. 

2. Suchen Sie den Namen des Datasets und den gewünschten Feldnamen auf der Registerkarte am unteren Tabellenrand. 
    
    ![mobile-report-publisher-parameter-data-view](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-data-view.png)
    
2.  Die Syntax der URL hängt von der Datenquelle ab. 

     **Für eine SQL Server Analysis Services-Datenquelle**: Erstellen Sie eine URL mit einem Abfragezeichenfolgenparameter in diesem Format:

    `http://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.<field-name>=<parameter-value>`

    Zum Beispiel:
    
    `http://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.category=Clothing` 
    
     **Für eine SQL Server-Datenquelle**: Der Abfragezeichenfolgenparameter ist fast identisch, weist jedoch das @-Symbol vor dem Namen des Felds auf:

    `http://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.@<field-name>=<parameter-value>`

    Zum Beispiel:
    
      `http://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.@category=Clothing` 

    
3.  Diese URL öffnet den Bericht auf dem Server mit automatischer Filterung nach dem von Ihnen angegebenen Parameterwert.

    ![mobile-report-publisher-parameter-web-portal-view](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-web-portal-view.png)

### <a name="see-also"></a>Siehe auch

[Hinzufügen von Parametern zu einem mobilen Bericht](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)

