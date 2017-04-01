---
title: "L&#246;schen von Beziehungen (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d40e3f05-54e8-4c4b-807a-0b06f446079b
caps.latest.revision: 13
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 13
---
# L&#246;schen von Beziehungen (SSAS – tabellarisch)
  Sie können vorhandene Beziehungen in der Diagrammsicht des Modell-Designers oder über das Dialogfeld Beziehungen verwalten löschen. Weitere Informationen darüber, wie Beziehungen in tabellarischen Modellen verwendet werden, finden Sie unter [Beziehungen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/relationships-ssas-tabular.md).  
  
## Überlegungen für das Löschen von Beziehungen  
 Berücksichtigen Sie vor dem Löschen einer Beziehung die folgenden Aspekte:  
  
-   Es gibt keine Möglichkeit, das Löschen einer Beziehung rückgängig zu machen. Sie können die Beziehung neu erstellen, diese Aktion erfordert jedoch eine vollständige Neuberechnung der Formeln im Modell. Führen Sie daher immer zuerst eine Überprüfung durch, bevor Sie eine Beziehung löschen, die in Formeln verwendet wird.  
  
-   Wenn Sie eine Beziehung zwischen zwei Tabellen löschen, kann dies Fehler in Formeln verursachen, die auf diese Tabellen verweisen.  
  
-   Die Data Analysis Expression (DAX)-Funktion RELATED sucht anhand der Beziehungen zwischen Tabellen nach verknüpften Werten in anderen Tabellen. Die Funktion gibt andere Ergebnisse zurück, nachdem die Beziehung gelöscht wurde. Weitere Informationen finden Sie im Thema zur RELATED-Funktion (DAX).  
  
-   Das Erstellen und Löschen von Beziehungen ändert nicht nur die PivotTable und die Formelergebnisse, sondern führt auch dazu, dass die Arbeitsmappe neu berechnet wird. Dies kann einige Zeit in Anspruch nehmen.  
  
## Löschen von Beziehungen  
  
#### So löschen Sie eine Beziehung mithilfe der Diagrammsicht  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf das Menü **Modell** , zeigen Sie auf **Modellansicht**, und klicken Sie dann auf **Diagrammsicht**.  
  
2.  Klicken Sie mit der rechten Maustaste zwischen zwei Tabellen auf eine Beziehungslinie, und klicken Sie dann auf **Löschen**.  
  
#### So löschen Sie eine Beziehung über das Dialogfeld "Beziehungen verwalten"  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]im Menü **Tabelle** auf **Beziehungen verwalten**.  
  
2.  Wählen Sie im Dialogfeld **Beziehungen verwalten** mindestens eine Beziehung aus der Liste aus.  
  
     Um mehrere Beziehungen auszuwählen, halten Sie die STRG-TASTE gedrückt, während Sie auf die einzelnen Beziehungen klicken.  
  
3.  Klicken Sie auf **Beziehung löschen**.  
  
4.  Klicken Sie im Dialogfeld **Beziehungen verwalten** auf **Schließen**.  
  
## Siehe auch  
 [Beziehungen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/relationships-ssas-tabular.md)   
 [Erstellen einer Beziehung zwischen zwei Tabellen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)  
  
  