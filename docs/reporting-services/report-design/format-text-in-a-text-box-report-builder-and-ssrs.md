---
title: Formatieren von Text in einem Textfeld (Berichts-Generator und SSRS) | Microsoft Docs
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
ms.assetid: df0794b5-96b0-4034-bd17-1be7f31e29db
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ab1c264ec07230bd81769ab2886177552095e636
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="format-text-in-a-text-box-report-builder-and-ssrs"></a>Formatieren von Text in einem Textfeld (Berichts-Generator und SSRS)
  Sie können beliebige Teile des Texts in einem Textfeld unabhängig voneinander formatieren und Platzhaltertext und statischen Text in einem Textfeld mischen. Durch das Mischen von Formaten und Hinzufügen von Platzhaltertext können Sie im Bericht Seriendrucke oder Vorlagen für Text erstellen. Jeder Ausdruck kann mithilfe eines Platzhalters getrennt definiert und formatiert werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-combine-multiple-formats-in-a-text-box"></a>So kombinieren Sie mehrere Formatierungen in einem Textfeld  
  
1.  Klicken Sie auf der Registerkarte **Einfügen** auf **Textfeld**. Klicken Sie auf die Entwurfsoberfläche, und erstellen Sie dann durch Ziehen ein Feld mit der gewünschten Größe.  
  
2.  Wählen Sie im Textfeld den Text aus, der formatiert werden soll.  
  
3.  Klicken Sie mit der rechten Maustaste auf den markierten Text, und klicken Sie dann auf **Texteigenschaften**.  
  
4.  Legen Sie die Formatierungsoptionen fest. Beispielsweise auf der Registerkarte **Allgemein** :  
  
    -   **QuickInfo:** Geben Sie Text ein oder einen Ausdruck, der zu einer QuickInfo ausgewertet wird. Die QuickInfo wird angezeigt, wenn der Benutzer den Mauszeiger über das Element in einem Bericht hält.  
  
    -   **Markuptyp:** Wählen Sie eine Option aus, um anzugeben, wie der markierte Text gerendert wird:  
  
         **Nur Text:** Zeigt den markierten Text als einfachen Text an. HTML wird als Literaltext behandelt.  
  
         **HTML**  Zeigt den markierten Text als HTML an. Wenn der Ausdruckswert des Platzhalters gültige HTML-Tags enthält, werden diese Tags als HTML gerendert. Weitere Informationen finden Sie unter [Importieren von HTML in einen Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md).  
  
5.  Klicken Sie auf **OK**.  
  
6.  Wiederholen Sie die Schritte 2 bis 5 für den übrigen zu formatierenden Text.  
  
### <a name="to-format-text-and-placeholders-differently-in-the-same-text-box"></a>So formatieren Sie Text und Platzhalter im gleichen Textfeld unterschiedlich  
  
1.  Klicken Sie auf der Registerkarte **Einfügen** auf **Liste**. Klicken Sie auf die Entwurfsoberfläche, und erstellen Sie dann durch Ziehen ein Feld mit der gewünschten Größe. Das Dialogfeld **Dataseteigenschaften** wird angezeigt. Sie können ein freigegebenes Dataset oder ein im Bericht eingebettetes Dataset verwenden. Weitere Informationen finden Sie unter [Dataseteigenschaften &#40;Dialogfeld, Abfrage, Berichts-Generator&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md) oder [Dataseteigenschaften (Dialogfeld), Abfrage](http://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f).  
  
2.  Klicken Sie auf der Registerkarte **Einfügen** auf **Textfeld**. Klicken Sie in die Liste, und erstellen Sie dann durch Ziehen ein Feld mit der gewünschten Größe.  
  
3.  Geben Sie im Textfeld eine Bezeichnung ein - z. B. **Mein Feld**:.  
  
4.  Ziehen Sie ein Feld aus dem Dataset in das Textfeld. Es wird ein Platzhalter für das Feld erstellt.  
  
5.  Wählen Sie für einfache Formatierung den Platzhaltertext aus, und klicken Sie dann auf der Registerkarte **Home** in der Gruppe **Schriftart** auf eine der Formatierungsoptionen. Klicken Sie z. B. auf die Schaltfläche **Fett** .  
  
     Klicken Sie mit der rechten Maustaste auf den Platzhaltertext, und klicken Sie dann auf **Platzhaltereigenschaften**, um weitere Formatierungsoptionen anzuzeigen.  
  
6.  Klicken Sie auf **OK**. Das Textfeld in der Berichtsentwurfsansicht sollte „**Mein Feld**: [*Feldname*]“ enthalten, wobei *Feldname* der Name des Felds ist.  
  
7.  Klicken Sie auf **Ausführen**.  
  
 Die Liste wird für jeden Wert im Feld einmal wiederholt, und der Platzhalter *Feldname* wird jedes Mal durch den Wert dieses Felds im Dataset ersetzt.  
  
## <a name="see-also"></a>Siehe auch  
 [Textfelder &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [Formatieren von Text und Platzhalter &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Ausdrucksverwendungen in Berichten &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Hinzufügen von HTML in einen Bericht &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/add-html-into-a-report-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Formatieren von Zahlen und Datumsangaben &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Im Dialogfeld "Eigenschaften" Platzhalter, Allgemein &#40; Berichts-Generator und SSRS &#41;](http://msdn.microsoft.com/library/7a867736-a3b0-4b5a-b3e5-fe7c8d7618a8)  
  
  
