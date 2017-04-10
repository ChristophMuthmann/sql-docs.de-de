---
title: "Erstellen eines Alias f&#252;r eine Modellspalte | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Data Mining [Analysis Services], Themen zur Vorgehensweise"
  - "Miningmodelle [Analysis Services], Spalten"
  - "Spaltennamen [Analysis Services]"
ms.assetid: c80ebe66-a8f8-4f24-9fe8-8288de9d13bc
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 14
---
# Erstellen eines Alias f&#252;r eine Modellspalte
  In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]können Sie einen Alias für eine Modellspalte erstellen. Dies kann hilfreich sein, wenn der Miningstrukturname zu lang ist, um mühelos damit zu arbeiten, oder wenn Sie der Spalte einen aussagekräftigeren Namen im Hinblick auf Inhalt oder Verwendung im Modell geben möchten. Beispiel: wenn Sie eine Kopie einer Strukturspalte erstellen und die Spalte dann für ein bestimmtes Modell unterschiedlich diskretisieren, können Sie die Spalte umbenennen, um den Inhalt genauer anzugeben.  
  
 Zum Erstellen eines Alias für eine Modellspalte verwenden Sie den Bereich **Eigenschaften** und legen [Name](../../analysis-services/scripting/properties/name-element-assl.md) -Eigenschaft der Spalte fest.  
  
 Auf der Registerkarte **Miningmodelle** im Data Mining Designer wird der Alias in Klammern neben der Beschriftung zur Spaltenverwendung angezeigt.  
  
 Informationen zum Festlegen der Eigenschaften eines Miningmodells finden Sie unter [Miningmodellspalten](../../analysis-services/data-mining/mining-model-columns.md).  
  
### So fügen Sie einen Alias einer Miningmodellspalte hinzu  
  
1.  Klicken Sie im Data Mining Designer auf der Registerkarte **Miningmodelle** mit der rechten Maustaste auf die Zelle im Miningmodell für die Miningspalte, die Sie ändern möchten, und wählen Sie dann **Eigenschaften** aus.  
  
2.  Klicken Sie anschließend im Fenster **Eigenschaften** auf der rechten Seite des Fensters auf die Zelle neben der Name-Eigenschaft, und löschen Sie den aktuellen Wert. Geben Sie einen neuen Namen für die Spalte ein.  
  
## Siehe auch  
 [Miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Miningmodelleigenschaften](../../analysis-services/data-mining/mining-model-properties.md)  
  
  