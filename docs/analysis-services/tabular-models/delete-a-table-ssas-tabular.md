---
title: "Löschen einer Tabelle | Microsoft Docs"
ms.custom: 
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: be4ed45f-fde3-466c-9869-49bd3ddb505e
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a4f9c2850798353cb6e16413f395aad1a370a69e
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="delete-a-table"></a>Löschen einer Tabelle
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Im Modell-Designer können Sie Tabellen in der Arbeitsbereichsdatenbank des Modells löschen, die Sie nicht mehr benötigen. Das Löschen einer Tabelle wirkt sich nicht auf die ursprünglichen Quelldaten aus, sondern nur auf die importierten Daten, mit denen Sie gearbeitet haben. Das Löschen einer Tabelle kann nicht rückgängig gemacht werden.  
  
### <a name="to-delete-a-table"></a>So löschen Sie eine Tabelle  
  
-   Klicken Sie unten im Modell-Designer mit der rechten Maustaste auf die Registerkarte der Tabelle, die gelöscht werden soll, und klicken Sie dann auf **Löschen**.  
  
## <a name="considerations-when-deleting-tables"></a>Überlegungen beim Löschen von Tabellen  
  
-   Wenn Sie eine Tabelle löschen, wird die gesamte Registerkarte gelöscht, auf der sich die Tabelle befand.  
  
-   Wenn dieser Tabelle Measures zugeordnet waren, wird die Definition des Measures ebenfalls gelöscht.  
  
-   Wenn Sie mithilfe dieser Tabelle berechnete Spalten erstellt haben, werden auch die Spalten in dieser Tabelle gelöscht. Berechnete Spalten in anderen Tabellen, die Spalten aus der gelöschten Tabelle verwenden, verursachen einen Fehler.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen und Spalten](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)  
  
  
