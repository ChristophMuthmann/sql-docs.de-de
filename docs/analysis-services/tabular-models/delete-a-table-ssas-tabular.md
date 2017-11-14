---
title: "Löschen einer Tabelle (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: be4ed45f-fde3-466c-9869-49bd3ddb505e
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1d3437449a05b5e1f60083135e020171b3d1e916
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="delete-a-table-ssas-tabular"></a>Löschen einer Tabelle (SSAS – tabellarisch)
  Im Modell-Designer können Sie Tabellen in der Arbeitsbereichsdatenbank des Modells löschen, die Sie nicht mehr benötigen. Das Löschen einer Tabelle wirkt sich nicht auf die ursprünglichen Quelldaten aus, sondern nur auf die importierten Daten, mit denen Sie gearbeitet haben. Das Löschen einer Tabelle kann nicht rückgängig gemacht werden.  
  
### <a name="to-delete-a-table"></a>So löschen Sie eine Tabelle  
  
-   Klicken Sie unten im Modell-Designer mit der rechten Maustaste auf die Registerkarte der Tabelle, die gelöscht werden soll, und klicken Sie dann auf **Löschen**.  
  
## <a name="considerations-when-deleting-tables"></a>Überlegungen beim Löschen von Tabellen  
  
-   Wenn Sie eine Tabelle löschen, wird die gesamte Registerkarte gelöscht, auf der sich die Tabelle befand.  
  
-   Wenn dieser Tabelle Measures zugeordnet waren, wird die Definition des Measures ebenfalls gelöscht.  
  
-   Wenn Sie mithilfe dieser Tabelle berechnete Spalten erstellt haben, werden auch die Spalten in dieser Tabelle gelöscht. Berechnete Spalten in anderen Tabellen, die Spalten aus der gelöschten Tabelle verwenden, verursachen einen Fehler.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen und Spalten &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)  
  
  

