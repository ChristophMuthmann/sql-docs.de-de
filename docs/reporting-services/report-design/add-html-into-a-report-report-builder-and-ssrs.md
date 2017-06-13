---
title: "Hinzufügen von HTML in einem Bericht (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: 30bd631a-f774-48e7-a13a-b6c2eb54d9bb
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 17889109d30d41405b0fa13d694e29930b82a292
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="add-html-into-a-report-report-builder-and-ssrs"></a>Hinzufügen von HTML in einem Bericht (Berichts-Generator und SSRS)
  Mithilfe eines Platzhalters können Sie HTML aus einem Feld im Dataset in einen Bericht importieren. Standardmäßig steht ein Platzhalter für einfachen Text, daher müssen Sie den Markuptyp des Platzhalters zu HTML ändern. Weitere Informationen finden Sie unter [Importieren von HTML in einen Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-html-from-a-field-in-your-dataset-into-a-text-box"></a>So fügen Sie einem Textfeld HTML aus einem Datasetfeld hinzu  
  
1.  Klicken Sie auf der Registerkarte **Einfügen** auf **Liste**. Klicken Sie auf die Entwurfsoberfläche, und erstellen Sie dann durch Ziehen ein Feld mit der gewünschten Größe.  
  
     Das Dialogfeld **Dataseteigenschaften** wird angezeigt. Sie können ein freigegebenes Dataset oder ein im Bericht eingebettetes Dataset verwenden. Weitere Informationen finden Sie unter [Dataseteigenschaften &#40;Dialogfeld, Abfrage, Berichts-Generator&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md) oder [Dataseteigenschaften (Dialogfeld), Abfrage](http://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f).  
  
2.  Klicken Sie auf der Registerkarte **Einfügen** auf **Textfeld**. Klicken Sie in die Liste, und erstellen Sie dann durch Ziehen ein Feld mit der gewünschten Größe.  
  
3.  Ziehen Sie ein HTML-Feld aus dem Dataset in das Textfeld. Es wird ein Platzhalter für das Feld erstellt.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Platzhalter, und klicken Sie anschließend auf **Platzhaltereigenschaften**.  
  
5.  Vergewissern Sie sich, dass auf der Registerkarte **Allgemein** im Feld **Wert** ein Ausdruck steht, der anhand des in Schritt 3 eingefügten Felds ausgewertet wird.  
  
6.  Klicken Sie auf **HTML – HTML-Tags als Formate interpretieren**. Hierdurch wird das Feld als HTML ausgewertet.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Formatieren von Zahlen und Datumsangaben &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Formatieren von Linien, Farben und Bildern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-lines-colors-and-images-report-builder-and-ssrs.md)   
 [Platzhaltereigenschaften (Dialogfeld), Allgemein &#40;Berichts-Generator und SSRS&#41;](http://msdn.microsoft.com/library/7a867736-a3b0-4b5a-b3e5-fe7c8d7618a8)  
  
  
