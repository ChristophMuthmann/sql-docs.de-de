---
title: Funktionen (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- DMX [Analysis Services], functions
- VBA [DMX]
- stored procedures [DMX]
- functions [DMX]
- Excel [DMX]
- Data Mining Extensions [Analysis Services], functions
ms.assetid: 75ab6346-f4a4-4699-90f3-66d35f930ed7
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: ba4f13bed63954643e6678ca4210400cb91c3b98
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="functions-dmx"></a>Funktionen (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Wenn Sie Data Mining Extensions (DMX) verwenden, um die Abfrageobjekte in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Sie können Funktionen verwenden, um mehr Informationen als nur die Werte in den Spalten im Datamining-Modell oder Eingabedataset zurückzugeben. Beispielsweise können Sie DMX-Abfragen verwenden, um nicht nur den Vorhersagewert einer Spalte, sondern auch die Wahrscheinlichkeit zurückzugeben, dass die Vorhersage richtig ist. Zusätzlich zu den DMX-Funktionen können Sie Funktionen von Microsoft Visual Basic für Applikationen (VBA) und von Microsoft Excel sowie gespeicherte Prozeduren verwenden.  
  
## <a name="dmx-functions"></a>DMX-Funktionen  
 Mit DMX-Funktionen können Sie folgende Aufgaben ausführen:  
  
-   Zurückgeben von Vorhersagen.  
  
-   Zurückgeben von statistischen Informationen zu einer Vorhersage, so z. B. die Wahrscheinlichkeit und den Unterstützungswert.  
  
-   Filtern von Abfrageergebnissen.  
  
-   Umordnen eines Tabellenausdrucks.  
  
 Die meisten DMX-Funktionen geben einen Skalarwert (z. B. ist der Unterstützungswert einer Vorhersage ein Skalarwert), einige Funktionen geben aber ein tabellarisches Ergebnis zurück. Die PredictHistogram-Funktion gibt z. B. eine Tabelle, die Unterstützung und Wahrscheinlichkeit für jeden Status der angegebenen vorhersagbaren Spalte enthält. Die Ergebnisse werden als neue tabellarische Spalte angezeigt.  
  
 **Weitere Informationen:** [allgemeine Vorhersagefunktionen &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md), [Datamining-Erweiterungen &#40;DMX&#41; Verweis-Funktion](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
## <a name="visual-basic-for-applications-vba-and-excel-functions"></a>VBA-Funktionen (Visual Basic für Applikationen) und Excel-Funktionen  
 Zusätzlich zu DMX-Funktionen können Sie aus DMX-Anweisungen eine Vielzahl von VBA- und Excel-Funktionen aufrufen. Die lCase-Funktion können Sie z. B. ändern, wie die Attribute_Name-Spalte im TM_Decision_Tree-Modellinhalt angezeigt wird. Dies ist im folgenden Codebeispiel gezeigt.  
  
```  
SELECT lCase([Attribute_Name])   
FROM [TM_Decision_Tree].CONTENT  
```  
  
 Wenn die gleiche Funktion in VBA und in Excel vorhanden ist, müssen Sie den Namen der Funktion in der DMX-Anweisung mit einem Präfix **VBA** oder **Excel**. Beispielsweise würden Sie `VBA!Log` oder `Excel!Log` verwenden. Wenn es die VBA- oder Excel-Funktion, die Sie verwenden möchten, auch in DMX oder MDX (Mehrdimensional Expressions) gibt oder wenn der Funktionsname ein Dollarzeichen ($) enthält, müssen Sie den Namen in eckige Klammern ([]) setzen. Die Funktion wird dann beispielsweise mit `[VBA!Format]` aufgerufen.  
  
## <a name="stored-procedures"></a>Gespeicherte Prozeduren  
 Mit den üblichen Programmiersprachen für Laufzeitprozeduren können Sie gespeicherte Prozeduren erstellen, die die Funktionalität von DMX erweitern. Z. B. eine regressionsstruktur-Miningmodell Koeffizienten zurück, z. B. A, B, und usw., die die Regressionsformel beschreiben, aber das Modell gibt nicht die Formel selbst, z. B. A + Bx zurück = y. Für einen solchen Fall können Sie eine gespeicherte Prozedur schreiben, in der das Data Mining-Modellobjekt dazu verwendet wird, das Inhaltsschema auszuwerten und die Regressionsgleichung als Ausgabe zurückzugeben. Auf diese Weise kann eine DMX-Anweisung eine Liste der Regressionsgleichungen als Teil eines Abfrageergebnisses zurückgeben.  
  
 **Weitere Informationen:** [mehrdimensionales Modell Assemblys-Verwaltung](../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen & #40; DMX & #41; Referenz](../dmx/data-mining-extensions-dmx-reference.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; Verweis-Funktion](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Datamining-Erweiterungen & #40; DMX & #41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; -Syntaxkonventionen](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; Syntaxelemente](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struktur und die Verwendung von DMX-Vorhersageabfragen](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Understanding the DMX Select Statement (Grundlegendes zur SELECT-Anweisung)](../dmx/understanding-the-dmx-select-statement.md)  
  
  
