---
title: "Ändern der Reihenfolge von Berichtsparametern (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
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
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 68553942ed806f07fe7ef1943c4fdfc846b3e414
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>Ändern der Reihenfolge von Berichtsparametern (Berichts-Generator und SSRS)
  Ändern Sie die Reihenfolge der Berichtsparameter, wenn ein abhängiger Parameter vor dem Parameter angeordnet ist, von dem er abhängt. Die Reihenfolge der Parameter spielt eine wichtige Rolle, wenn Sie mit kaskadierenden Parametern arbeiten, oder wenn Sie möchten, dass der Standardwert für einen Parameter angezeigt wird, bevor die Benutzer Werte für andere Parameter auswählen. Ein abhängiger Berichtsparameter enthält entweder in der Abfrage der Standardwerte oder in der Abfrage der gültigen Werte einen Verweis auf einen Abfrageparameter, der auf einen Berichtsparameter verweist, der in der Parameterliste im Bereich **Berichtsdaten** nach ihm angeordnet ist.  
  
 Die Reihenfolge der Parameter auf der Symbolleiste des Berichts-Viewers beim Ausführen des Berichts hängt von der Reihenfolge der Parameter im Bereich **Berichtsdaten** sowie der Position der Parameter im Bereich der benutzerdefinierten Parameter ab. Weitere Informationen finden Sie unter [Benutzerdefiniertes Anpassen des Parameterbereichs (Berichts-Generator)](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md) erstellen.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-the-order-of-report-parameters"></a>So ändern Sie die Reihenfolge von Berichtsparametern  
  
Wählen Sie eine der folgenden Vorgehensweisen aus, um die Reihenfolge von Berichtsparametern zu ändern:  
  
-   Klicken Sie im Bereich **Berichtsdaten** auf einen Parameter, und verschieben Sie ihn mit den Pfeilschaltflächen in der Liste nach oben oder nach unten (siehe Abbildung unten).  Wenn Sie die Reihenfolge der Parameter im Bereich **Berichtsdaten** ändern, wird die Position des Parameters im Parameterbereich geändert.  
  
     ![Ändern der Parameterreihenfolge im Berichtsdatenbereich](../../reporting-services/report-design/media/ssrs-changeorderofparameters-reportdata.png "Change the order of the parameters in the Report Data pane")  
  
-   Ziehen Sie den Parameter im Parameterbereich in eine neue Spalte oder Zeile des Bereichs. Wenn Sie die Position des Parameters in diesem Bereich ändern, wird die Parameterreihenfolge im Bereich **Berichtsdaten** geändert. Weitere Informationen zum Verschieben der Parameter in diesem Bereich finden Sie unter [Benutzerdefiniertes Anpassen des Parameterbereichs (Berichts-Generator)](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Hilfe zu Dialogfeldern, Bereichen und Assistenten in Berichts-Generator](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [Hinzufügen von kaskadierenden Parametern zu einem Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Tutorial: Add a Parameter to Your Report (Report Builder) (Tutorial: Hinzufügen eines Parameters zu einem Bericht (Berichts-Generator))](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Hinzufügen von Datasetfiltern, Datenbereichsfiltern und Gruppenfiltern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Verweise auf Parameters-Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
