---
title: "Hinzufügen eines Ausdrucks (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a60ee091-b4ed-41e1-9b6a-032c316cd03f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 57cdb0a373d713741216b1cebc8d3d44ff7fceb3
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="add-an-expression-report-builder-and-ssrs"></a>Hinzufügen eines Ausdrucks (Berichts-Generator und SSRS)
  Ausdrücke werden überall in einem Bericht zum Definieren von Berichtselementeigenschaften, Filtern, Gruppen, Sortierreihenfolgen, Verbindungszeichenfolgen und Parameterwerten verwendet. Ausdrücke beginnen mit einem Gleichheitszeichen (=) und werden in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]geschrieben. Sie werden zur Laufzeit vom Berichtsprozessor ausgewertet, der das Auswertungsergebnis mit den Berichtslayoutelementen kombiniert.  
  
 Ausdrücke können einfach oder komplex sein. Einfache Ausdrücke verweisen auf ein einzelnes Element in einer integrierten Auflistung. Komplexe Ausdrücke können Konstanten, Operatoren, globale Auflistungselemente und Funktionsaufrufe enthalten. Weitere Informationen finden Sie unter [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-expression-to-a-text-box"></a>So fügen Sie einem Textfeld einen Ausdruck hinzu  
  
-   Klicken Sie in der Ansicht **Entwurf** auf das Textfeld auf der Entwurfsoberfläche, dem Sie einen Ausdruck hinzufügen möchten.  
  
    -   Geben Sie den Anzeigetext für den Ausdruck in das Textfeld ein, um einen einfachen Ausdruck zu erstellen. Geben Sie zum Beispiel für das Datasetfeld Sales den Text `[Sales]`ein.  
  
    -   Klicken Sie mit der rechten Maustaste auf das Textfeld, und wählen Sie den Befehl **Ausdruck**aus, um einen komplexen Ausdruck einzugeben. Das Dialogfeld **Ausdruck** wird geöffnet. Geben Sie den Ausdruck im Ausdrucksbereich hinter '=' ein, bzw. erstellen Sie den Ausdruck interaktiv, und klicken Sie dann auf OK.  
  
         Der Ausdruck wird auf der Entwurfsoberfläche als `<<Expr>>`angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Formatieren von Text und Platzhalter &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Textfelder &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [Ausdrucksverwendungen in Berichten &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Filtergleichungen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [Beispiele für Gruppierungsausdrücke &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [Ausdruck (Dialogfeld) &#40; Berichts-Generator &#41;](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)   
 [Beispiele für Ausdrücke &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Fügen Sie Code hinzu, um einen Bericht &#40; SSRS &#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md)  
  
  

