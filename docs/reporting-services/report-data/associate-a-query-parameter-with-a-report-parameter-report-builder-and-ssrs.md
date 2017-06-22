---
title: Zuordnen eines Abfrageparameters zu einem Berichtsparameter (Berichts-Generator und SSRS) | Microsoft Docs
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
helpviewer_keywords:
- queries [Reporting Services], parameters
- parameters [Reporting Services], queries
ms.assetid: 6d297e1a-ff71-472a-addc-349e863092b5
caps.latest.revision: 49
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6a1efe67725037c9d47f20209c2831db3faef65e
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs"></a>Zuordnen eines Abfrageparameters zu einem Berichtsparameter (Berichts-Generator und SSRS)
  Wenn Sie eine Datasetabfrage definieren, die eine Abfragevariable enthält, wird der Abfragebefehl analysiert. Für jede Abfragevariable werden ein entsprechender Datasetparameter und ein Berichtsparameter erstellt. Der Datasetparameter verweist auf den Berichtsparameter. Dies ermöglicht einem Benutzer, einen Wert anzugeben, der direkt an die Abfrage übergeben wird. Bei jeder Bearbeitung des Abfragebefehls findet der gleiche Prozess statt.  
  
 Wenn Sie einen Berichtsparameter umbenennen, der an einen Abfrageparameter gebunden ist, müssen Sie die Abfrageparameter manuell mit dem umbenannten Berichtsparameter verknüpfen. Gehen Sie hierzu wie in diesem Thema beschrieben vor.  
  
> **HINWEIS:** [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-associate-a-query-parameter-with-a-report-parameter"></a>So ordnen Sie einen Abfrageparameter einem Berichtsparameter zu  
  
1.  Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf das Dataset, klicken Sie auf **Dataseteigenschaften**, und klicken Sie anschließend auf **Parameter**.  
  
    > **HINWEIS:** Zum Anzeigen des Berichtsdatenbereichs klicken Sie im Menü **Ansicht** auf **Berichtsdaten** .  
  
2.  In der Spalte **Parametername**finden Sie den Namen des Abfrageparameters. Parameternamen werden automatisch basierend auf der Abfrage ausgefüllt. Jedes Mal, wenn Sie die Abfrage ändern, wird diese auf neue Abfrageparameter überprüft. Abfrageparameter, die Sie manuell erstellen, werden nicht geändert, wenn sich die Abfrage ändert.  
  
    -   Geben Sie unter **Parametername**den Abfrageparameternamen so ein, wie er in der Abfrage angegeben ist. Sie können auch manuell einen neuen Abfrageparameter hinzufügen und einen Namen eingeben.  
  
    -   Geben Sie unter **Parameterwert**einen Ausdruck ein, der zu dem Wert ausgewertet wird, der an den Abfrageparameter übergeben werden soll, oder wählen Sie einen entsprechenden Ausdruck aus. Dies ist in der Regel der Name des Berichtsparameters.  
  
        > **HINWEIS:** Bei den Werten für die Abfrageparameter sind Sie nicht auf Berichtsparameter beschränkt. Sie können jeden beliebigen Ausdruck verwenden, der auf einen Wert für den Parameterwert ausgewertet wird.  
  
3.  Wiederholen Sie Schritt 2 für jeden weiteren Abfrageparameter.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   

  
  
