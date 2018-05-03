---
title: Erstellen eines Alias für eine Modellspalte | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c08cce1946d46d4d0d5837f4983e9e773a87c746
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-an-alias-for-a-model-column"></a>Erstellen eines Alias für eine Modellspalte
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]können Sie einen Alias für eine Modellspalte erstellen. Dies kann hilfreich sein, wenn der Miningstrukturname zu lang ist, um mühelos damit zu arbeiten, oder wenn Sie der Spalte einen aussagekräftigeren Namen im Hinblick auf Inhalt oder Verwendung im Modell geben möchten. Beispiel: wenn Sie eine Kopie einer Strukturspalte erstellen und die Spalte dann für ein bestimmtes Modell unterschiedlich diskretisieren, können Sie die Spalte umbenennen, um den Inhalt genauer anzugeben.  
  
 Zum Erstellen eines Alias für eine Modellspalte verwenden Sie den Bereich **Eigenschaften** und legen [Name](../../analysis-services/scripting/properties/name-element-assl.md) -Eigenschaft der Spalte fest.  
  
 Auf der Registerkarte **Miningmodelle** im Data Mining Designer wird der Alias in Klammern neben der Beschriftung zur Spaltenverwendung angezeigt.  
  
 Informationen zum Festlegen der Eigenschaften eines Miningmodells finden Sie unter [Miningmodellspalten](../../analysis-services/data-mining/mining-model-columns.md).  
  
### <a name="to-add-an-alias-to-a-mining-model-column"></a>So fügen Sie einen Alias einer Miningmodellspalte hinzu  
  
1.  Klicken Sie im Data Mining Designer auf der Registerkarte **Miningmodelle** mit der rechten Maustaste auf die Zelle im Miningmodell für die Miningspalte, die Sie ändern möchten, und wählen Sie dann **Eigenschaften**aus.  
  
2.  Klicken Sie anschließend im Fenster **Eigenschaften** auf der rechten Seite des Fensters auf die Zelle neben der Name-Eigenschaft, und löschen Sie den aktuellen Wert. Geben Sie einen neuen Namen für die Spalte ein.  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodelltasks und Anweisungen Mining](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Miningmodelleigenschaften](../../analysis-services/data-mining/mining-model-properties.md)  
  
  
