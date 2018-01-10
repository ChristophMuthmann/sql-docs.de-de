---
title: "Hinzufügen eines aus mehreren Werten bestehenden Parameters zu einem Bericht | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12ad0e77-4c28-4bbb-ab11-473ae89ec9f1
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f470964c5df5d20d39537f65baf7d20d85f68cc5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="add-a-multi-value-parameter-to-a-report"></a>Hinzufügen eines aus mehreren Werten bestehenden Parameters zu einem Bericht
  Sie können einem Bericht einen Parameter hinzufügen, der dem Benutzer die Auswahl mehrerer Werte für den Parameter ermöglicht.  
  
 Sie können mehrere Parameterwerte innerhalb der Berichts-URL an den Bericht übergeben. Ein URL-Beispiel mit einem mehrwertigen Parameter finden Sie unter [Übergeben von Berichtsparametern innerhalb einer URL](../../reporting-services/pass-a-report-parameter-within-a-url.md).  
  
 Informationen dazu, wie mehrere Parameterwerte an eine gespeicherte Prozedur übergeben werden, finden Sie unter [Verwenden von Mehrfachauswahl-Parametern für SSRS-Berichte](http://go.microsoft.com/fwlink/?LinkId=321529) auf mssqltips.com.  
  
## <a name="to-add-a-multi-value-parameter"></a>So fügen Sie einen aus mehreren Werten bestehenden Parameter hinzu  
  
1.  Öffnen Sie im Berichts-Generator den Bericht, dem Sie den aus mehreren Werten bestehenden Parameter hinzufügen möchten.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Berichtsdataset, und klicken Sie dann auf **Dataseteigenschaften**.  
  
3.  Fügen Sie der Datasetabfrage eine Variable hinzu, indem Sie entweder den Abfragetext im Feld **Abfrage** bearbeiten oder im Abfrage-Designer einen Filter hinzufügen. Weitere Informationen finden Sie unter [Erstellen einer Abfrage im Relationalen Abfrage-Designer (Berichts-Generator und SSRS)](../../reporting-services/report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md).  
  
    ```  
    WHERE  
      Production.ProductInventory.ProductID IN (@ProductID)  
    ```  
  
    > [!IMPORTANT]  
    > *  Der Abfragetext darf keine DECLARE-Anweisung für die Abfragevariable enthalten.  
    > *  Der Text für die Abfragevariable muss den **IN** -Operator enthalten, wie im Beispiel oben veranschaulicht wird.  
    > *  Achten Sie darauf, die Variablen wie oben gezeigt in Klammern einzuschließen. Andernfalls wird der Bericht nicht gerendert und der Fehler „Die Skalarvariable muss deklariert werden“ wird angezeigt.  
  
    Für die Abfragevariable wird automatisch ein Datasetparameter für ein eingebettetes Dataset oder ein freigegebenes Dataset erstellt. Für den Datasetparameter wird automatisch ein Berichtsparameter erstellt.  
  
4.  Erweitern Sie im Bereich **Berichtsdaten** den Knoten **Parameter** , klicken Sie mit der rechten Maustaste auf den Berichtsparameter, der automatisch für den Datasetparameter erstellt wurde, und klicken Sie anschließend auf **Parametereigenschaften**.  
  
5.  Wählen Sie auf der Registerkarte **Allgemein** die Option **Mehrere Werte zulassen** aus, um anzugeben, dass für den Parameter mehr als ein Wert ausgewählt werden darf.  
  
6.  (Optional) Geben Sie auf der Registerkarte **Verfügbare Werte** eine Liste mit verfügbaren Werten an, die dem Benutzer angezeigt werden soll.  
  
     Eine Liste verfügbarer Werte schränkt die Auswahl, die ein Benutzer treffen kann, auf die gültigen Werte für den Parameter ein. Bei mehreren Werten beginnt die Liste mit der Funktion **Alles auswählen** , sodass der Benutzer alle Werte mit einem einzigen Mausklick auswählen oder löschen kann. Wenn Sie die für den Berichtsparameter verfügbaren Werte mit einer Datasetabfrage abrufen möchten, achten Sie darauf, kein Dataset auszuwählen, das die demselben Berichtsparameter zugeordnete Abfragevariable enthält.  
  
     Weitere Informationen finden Sie unter [Hinzufügen, Ändern oder Löschen von verfügbaren Werten für einen Berichtsparameter (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md).  

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Hinzufügen von kaskadierenden Parametern zu einem Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Hinzufügen, Ändern oder Löschen von Berichtsparametern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)  
  
  
