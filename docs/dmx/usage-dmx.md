---
title: Verwendung (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- column usage [DMX]
- Data Mining Extensions [Analysis Services], column usage types
- DMX [Analysis Services], column usage types
ms.assetid: 6d7ae72a-f5b5-4744-a3a2-46ccd6432c1a
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2acfde9b8d7c9d13fc626b006116e9b3760fd432
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="usage-dmx"></a>Verwendung (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Bei Verwendung von Data Mining Extensions (DMX) definieren Sie ein neues Datamining-Modell in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], müssen Sie angeben, wie der Datamining-Algorithmus, der das Modell erstellt für jede Spalte verwendet werden soll. Sie können für eine Spalte angeben, dass sie einen der folgenden Typen hat:  
  
-   **Key**  
  
-   **Tastenkombination**  
  
-   **Die Schlüsselzeit**  
  
-   **Vorhersagen**  
  
-   **PredictOnly**  
  
 Spalten, für die kein Typ in DMX angegeben ist, werden als Eingabespalten behandelt.  
  
 Damit der Algorithmus ein Modell richtig verarbeiten kann, muss Folgendes angegeben werden: die Schlüsselspalte, mit der jede Zeile eindeutig bestimmt wird, die Zielspalte für das Erstellen von Vorhersagen (wenn Sie ein vorhersagbares Modell erstellen) und die Spalten, die als Eingabespalten verwendet werden sollen, um die Beziehungen zu erstellen, anhand derer die Zielspalte vorhergesagt wird.  
  
 Spalten, die als angegeben sind die **Predict** Typ als Eingabe-und Ausgabespalten verwendet werden. Spalten, die als ausstellerbindung **PredictOnly** dienen nur als Ausgabespalten. Bestimmte Algorithmen behandeln Predict-Spalten möglicherweise anders.  
  
 Weitere Informationen über die Spalte spaltenverwendungstypen, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] unterstützt, finden Sie unter [Mining Model Columns](../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Algorithmen &#40; Analysis Services – Datamining &#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Referenz](../dmx/data-mining-extensions-dmx-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Syntaxelemente](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Syntaxkonventionen](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struktur und die Verwendung von DMX-Vorhersageabfragen](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Grundlegendes zur Select-Anweisung von DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  

