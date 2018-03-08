---
title: "Löschen von Beziehungen | Microsoft Docs"
ms.custom: 
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: multidimensional-tabular
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d40e3f05-54e8-4c4b-807a-0b06f446079b
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 690224c1798494e75f6b26add07d51c3afa7134f
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="delete-relationships"></a>Löschen von Beziehungen 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Sie können vorhandene Beziehungen in der Diagrammsicht des Modell-Designers oder über das Dialogfeld Beziehungen verwalten löschen. Informationen zur Verwendungsweise von Beziehungen in tabellarischen Modellen finden Sie unter [Beziehungen](../../analysis-services/tabular-models/relationships-ssas-tabular.md).  
  
## <a name="considerations-for-deleting-relationships"></a>Überlegungen zum Löschen von Beziehungen  
 Berücksichtigen Sie vor dem Löschen einer Beziehung die folgenden Aspekte:  
  
-   Es gibt keine Möglichkeit, das Löschen einer Beziehung rückgängig zu machen. Sie können die Beziehung neu erstellen, diese Aktion erfordert jedoch eine vollständige Neuberechnung der Formeln im Modell. Führen Sie daher immer zuerst eine Überprüfung durch, bevor Sie eine Beziehung löschen, die in Formeln verwendet wird.  
  
-   Wenn Sie eine Beziehung zwischen zwei Tabellen löschen, kann dies Fehler in Formeln verursachen, die auf diese Tabellen verweisen.  
  
-   Die Data Analysis Expression (DAX)-Funktion RELATED sucht anhand der Beziehungen zwischen Tabellen nach verknüpften Werten in anderen Tabellen. Die Funktion gibt andere Ergebnisse zurück, nachdem die Beziehung gelöscht wurde. Weitere Informationen finden Sie im Thema zur RELATED-Funktion (DAX).  
  
-   Das Erstellen und Löschen von Beziehungen ändert nicht nur die PivotTable und die Formelergebnisse, sondern führt auch dazu, dass die Arbeitsmappe neu berechnet wird. Dies kann einige Zeit in Anspruch nehmen.  
  
## <a name="delete-relationships"></a>Löschen von Beziehungen  
  
#### <a name="to-delete-a-relationship-by-using-diagram-view"></a>So löschen Sie eine Beziehung mithilfe der Diagrammsicht  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf das Menü **Modell** , zeigen Sie auf **Modellansicht**, und klicken Sie dann auf **Diagrammsicht**.  
  
2.  Klicken Sie mit der rechten Maustaste zwischen zwei Tabellen auf eine Beziehungslinie, und klicken Sie dann auf **Löschen**.  
  
#### <a name="to-delete-a-relationship-by-using-the-manage-relationships-dialog-box"></a>So löschen Sie eine Beziehung über das Dialogfeld "Beziehungen verwalten"  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]im Menü **Tabelle** auf **Beziehungen verwalten**.  
  
2.  Wählen Sie im Dialogfeld **Beziehungen verwalten** mindestens eine Beziehung aus der Liste aus.  
  
     Um mehrere Beziehungen auszuwählen, halten Sie die STRG-TASTE gedrückt, während Sie auf die einzelnen Beziehungen klicken.  
  
3.  Klicken Sie auf **Beziehung löschen**.  
  
4.  Klicken Sie im Dialogfeld **Beziehungen verwalten** auf **Schließen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Beziehungen](../../analysis-services/tabular-models/relationships-ssas-tabular.md)   
 [Erstellen einer Beziehung](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)  
  
  
