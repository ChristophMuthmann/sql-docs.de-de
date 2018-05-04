---
title: MDX-Syntaxelemente (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], syntax
- MDX [Analysis Services], syntax
ms.assetid: f4c16e1a-cf1a-4be0-839a-db018430ff14
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: bdee7d87a71314e9dccb39ffecaecdfcf2d48cf9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-syntax-elements-mdx"></a>MDX-Syntaxelemente (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  MDX (Multidimensional Expressions) hat mehrere Syntaxelemente, die von den meisten Anweisungen verwendet werden bzw. sich auf die meisten Anweisungen auswirken:  
  
|Begriff|Definition|  
|----------|----------------|  
|[Identifiers (Bezeichner)](../mdx/identifiers-mdx.md)|Ein Bezeichner ist der Name eines Objekts (z. B. eines Cubes, einer Dimension, eines Elements oder eines Measures).|  
|**Datentypen**|Definieren die Typen der Daten, die in Zellen, Elementeigenschaften oder Zelleigenschaften enthalten sind. MDX unterstützt nur den OLE VARIANT-Datentyp. Weitere Informationen zur Koersion, Konvertierung und Bearbeitung des VARIANT-Datentyps finden Sie in der Dokumentation für Platform SDK im Abschnitt über VARIANT und VARIANTARG.|  
|[Ausdrücke &#40;MDX&#41;](../mdx/expressions-mdx.md)|Ausdrücke ist eine Syntaxeinheit, die [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] auflösen kann, um die einzelnen (skalaren) Werten oder Objekten. Ausdrücke enthalten Funktionen, die einen einzelnen Wert, einen Mengenausdruck usw. zurückgeben.|  
|[Operatoren](../mdx/operators-mdx-syntax.md)|Operatoren sind Syntaxelemente, die mit einem oder mehreren einfachen MDX-Ausdrücken verwendet werden, um komplexere MDX-Ausdrücke zu erstellen.|  
|[Funktionen](../mdx/functions-mdx-syntax.md)|Funktionen sind Syntaxelemente, die keinen, einen oder mehrere Eingabewerte annehmen und einen Skalarwert oder ein Objekt zurückgeben. Beispiele hierfür sind die [Summe](../mdx/sum-mdx.md) -Funktion zum Hinzufügen mehrerer Werte, die [Elemente](../mdx/members-set-mdx.md) -Funktion zum Zurückgeben einer Menge von Elementen aus einer Dimension oder Ebene, und so weiter.|  
|[Kommentare](../mdx/comments-mdx-syntax.md)|Kommentare sind Texte, die in MDX-Anweisungen oder Skripts eingefügt werden, um den Zweck der Anweisung zu erklären. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Kommentare wird nicht ausgeführt werden.|  
|[Reservierte Schlüsselwörter](../mdx/reserved-keywords-mdx-syntax.md)|Reservierte Schlüsselwörter sind Wörter, die für die Verwendung durch MDX reserviert sind. Sie dürfen nicht für Objektnamen verwendet werden, die in MDX-Anweisungen verwendet werden.|  
|[Elemente, Tupel und Mengen](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)|Elemente, Tupel und Mengen sind Bestandteile des Kernkonzepts für mehrdimensionale Daten. Sie sollten diese Begriffe verstanden haben, bevor Sie eine MDX-Abfrage erstellen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Mehrdimensionale Ausdrücke & #40; MDX & #41; Referenz](../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
