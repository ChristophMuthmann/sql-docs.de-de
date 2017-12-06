---
title: Angeben von Pfaden zu externen Elementen (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4fe513da-f3c5-479c-9fec-8662b91a0d6d
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: d6f12f023e98f410af92939af08e993df7f0d3c0
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="specifying-paths-to-external-items-report-builder-and-ssrs"></a>Angeben von Pfaden zu externen Elementen (Berichts-Generator und SSRS)
  Sie geben Pfade in Berichtselementeigenschaften an, um auf Elemente wie Drillthroughberichte, Unterberichte und Bilddateien zu verweisen, die nicht in der Berichtsdefinitionsdatei enthalten und auf einem Berichtsserver gespeichert sind (externe Elemente).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
> [!NOTE]  
>  Im Berichts-Generator müssen in den Pfaden zu Elementen Elemente auf einem Berichtsserver angegeben werden. Pfade zu Elementen in einem Dateisystem werden nicht unterstützt. Sie können einen Bericht mit diesen Elementen nur in der Vorschau anzeigen, wenn Sie mit dem Berichtsserver mit den Elementen verbunden sind.  
  
 Wenn Sie Pfade für ein externes Element in einem Dialogfeld für Aktionen, Unterberichte oder Bilder angeben, können Sie direkt zu dem Berichtsserver navigieren und das Element auswählen. Zum Angeben von Drillthroughberichten oder Unterberichten wird empfohlen, direkt zu einem Element zu navigieren und es auszuwählen. Auf diese Weise werden die richtigen Parameternamen in einer Dropdownliste angezeigt, wenn Sie Berichts- oder Unterberichtsparameter angeben. Wenn Sie einen Elementpfad ändern, damit er auf ein anderes Element zeigt, müssen Sie den korrekten Parameternamen und die Parameterwerte ggf. manuell aktualisieren.  
  
 Auf einem im einheitlichen Modus konfigurierten Berichtsserver geben Sie den Namen für einen Drillthroughbericht ohne die Dateinamenerweiterung ".rdl" an.  
  
 Bei einem im integrierten SharePoint-Modus konfigurierten Berichtsserver müssen Sie die Dateinamenerweiterung ".rdl" einschließen. Folgende Pfade sind möglich:  
  
-   **Ein relativer Pfad zu dem Element aus dem Hauptbericht.** Beispiel: ../AllSubreports/Subreport1. In diesem Beispiel gibt **..** den Ordner über dem Ordner an, in dem der Hauptbericht gespeichert ist.  
  
    > [!NOTE]  
    >  Relative Pfade werden nicht unterstützt, wenn der Bericht in Berichts-Generator ausgeführt wird. Wenn Sie einen Bericht anzeigen möchten, in dem relative Pfade zu externen Elementen verwendet werden, speichern Sie den Bericht auf dem Berichtsserver, und führen Sie den Bericht von dort aus.  
  
-   **Ein vollständiger Pfad zum Element.**  
  
    -   **Auf einem Berichtsserver:** Der Pfad beginnt mit **/**, dem Basisordner. Beispiel: /Reports/AllSubreports/Subreport1.  
  
    -   **Auf einer SharePoint-Website:** Sie müssen den Berichtsnamen in einem Ausdruck angeben, mit der vollständigen URL des Elements und der Dateierweiterung ".rdl". Beispiel: `="http://server/site/library/folder/Report1.rdl"`.  
  
## <a name="see-also"></a>Siehe auch  
 [Hinzufügen eines externen Bilds &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)   
 [Hinzufügen eines Unterberichts und Hinzufügen von Parametern (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md)   
 [Hinzufügen einer Drillthroughaktion für einen Bericht (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)  
  
  
