---
title: "Erstellen und Verwalten von Measures (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: edc1a4b2-96d3-4f34-bb70-6cacec79e819
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 799ada43cebe2f6358c88c0b4aa8719186f67823
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="create-and-manage-measures-ssas-tabular"></a>Erstellen und Verwalten von Measures (SSAS – tabellarisch)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Ein Measure ist eine Formel, die zur Verwendung in einem Bericht oder die Excel-PivotTable (oder PivotChart) erstellt wird. Measures können auf Standardaggregationsfunktionen basieren, z. B. COUNT oder SUM, oder Sie können mit DAX eigene Formeln definieren. In den Tasks in diesem Thema wird beschrieben, wie Measures mithilfe des Measurerasters einer Tabelle erstellt und verwaltet werden.  
  
 Dieses Thema umfasst folgende Aufgaben:  
  
-   [So erstellen Sie ein Measure mithilfe einer Standardaggregationsformel](#bkmk_create_stand)  
  
-   [So erstellen Sie ein Measure mithilfe einer benutzerdefinierten Formel](#bkmk_create_custom)  
  
-   [So bearbeiten Sie Measureeigenschaften](#bkmk_edit)  
  
-   [So benennen Sie ein Measure um](#bkmk_rename)  
  
-   [So löschen Sie ein Measure](#bkmk_delete)  
  
## <a name="tasks"></a>Aufgaben  
 Zum Erstellen und Verwalten von Measures verwenden Sie das Measureraster einer Tabelle. Sie können das Measureraster für eine Tabelle nur in der Datensicht des Modell-Designers anzeigen. In der Diagrammsicht können Sie keine Measures erstellen und kein Measureraster anzeigen. Vorhandene Measures können in der Diagrammsicht jedoch angezeigt werden. Um das Measureraster für eine Tabelle anzuzeigen, klicken Sie auf das Menü **Tabelle** und dann auf **Measureraster anzeigen**.  
  
###  <a name="bkmk_create_stand"></a> So erstellen Sie ein Measure mithilfe einer Standardaggregationsformel  
  
-   Klicken Sie auf die Spalte, für die Sie das Measure erstellen möchten, klicken Sie dann auf das Menü **Spalte** , zeigen Sie auf **AutoSumme**, und klicken Sie dann auf einen Aggregationstyp.  
  
     Das Measure wird automatisch mit einem Standardnamen erstellt, gefolgt von der Formel in der ersten Zelle im Measureraster direkt unterhalb der Spalte.  
  
###  <a name="bkmk_create_custom"></a> So erstellen Sie ein Measure mithilfe einer benutzerdefinierten Formel  
  
-   Klicken Sie im Measureraster unter der Spalte, für die Sie das Measure erstellen möchten, auf eine Zelle, und geben Sie dann in der Bearbeitungsleiste einen Namen gefolgt von einem Doppelpunkt (:), einem Gleichheitszeichen (=) und der Formel ein. Drücken Sie die EINGABETASTE, um die Formel zu übernehmen.  
  
###  <a name="bkmk_edit"></a> So bearbeiten Sie Measureeigenschaften  
  
-   Klicken Sie im Measureraster auf ein Measure, und geben Sie dann im Fenster **Eigenschaften** einen anderen Eigenschaftswert ein, oder wählen Sie ihn aus.  
  
###  <a name="bkmk_rename"></a> So benennen Sie ein Measure um  
  
-   Klicken Sie im Measureraster auf ein Measure, und geben Sie dann im Fenster **Eigenschaften** in **Measurename**einen neuen Namen ein, und drücken Sie die EINGABETASTE.  
  
     Sie können ein Measure auch in der Bearbeitungsleiste umbenennen. Der Measurename ist der Formel gefolgt von einem Doppelpunkt vorangestellt.  
  
###  <a name="bkmk_delete"></a> So löschen Sie ein Measure  
  
-   Klicken Sie im Measureraster mit der rechten Maustaste auf ein Measure, und klicken Sie auf **Löschen**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Measures &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [KPIs &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Berechnete Spalten &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  
