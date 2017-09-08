---
title: "Benutzerdefinierte Rollupoperatoren in über-und untergeordneten Dimensionen | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- child rollup operations
- UnaryOperatorColumn property
- custom rollup operators [Analysis Services]
- unary operators
- parent-child dimensions [Analysis Services]
ms.assetid: a3ddd9fc-5fa3-4227-9322-8c45a5b5c2c3
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 328bd8977389ac39d049d44095c447a2843efdbe
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="parent-child-dimension-attributes---custom-rollup-operators"></a>Über-und untergeordneten Dimensionsattribute – benutzerdefinierte Rollupoperatoren
  Mit benutzerdefinierten Rollup-Operatoren können Sie auf einfache Weise steuern, wie Rollups von Elementwerten zu übergeordneten Werten in einer Hierarchie mit über- und untergeordneten Elementen ausgeführt werden. In einer Dimension mit einer Über-/Unterordnungsbeziehung geben Sie eine Spalte mit unären Operatoren an, die einen Rollup für alle nicht berechneten Elemente des übergeordneten Attributs angeben. Der unäre Operator wird immer dann auf die Elemente angewendet, wenn die Werte des übergeordneten Elements ausgewertet werden.  
  
 Die unären Operatoren werden in der Spalte gespeichert, die durch die **UnaryOperatorColumn** -Eigenschaft des übergeordneten Attributs definiert ist, und werden auf jedes Element des Attributs angewendet. Die durch diese Eigenschaft angegebene Spalte kann sich in der Dimensionstabelle oder in einer Tabelle befinden, die durch einen Fremdschlüssel in der Dimensionstabelle mit der Dimensionstabelle verknüpft ist.  
  
 Benutzerdefinierte Rollup-Operatoren stellen eine Funktionalität bereit, die der von benutzerdefinierten Elementformeln ähnelt, jedoch einfacher ist. Eine benutzerdefinierte Elementformel bestimmt mithilfe von MDX-Ausdrücken (Multidimensional Expressions), wie der Rollup für die Elemente ausgeführt wird. Im Gegensatz dazu bestimmt ein benutzerdefinierter Rollup-Operator mithilfe eines einfachen unären Operators, wie sich der Wert eines Elements auf das übergeordnete Element auswirkt. Benutzerdefinierte Elementformeln der vorherigen Ebene in einer Dimension überschreiben den benutzerdefinierten Rollup-Operator einer Ebene.  
  
## <a name="custom-rollup-precedence"></a>Rangfolge von benutzerdefinierten Rollup-Operatoren  
 Im Hinblick auf die Rangfolge überschreiben die benutzerdefinierten Rollup-Operatoren des Quellattributs für eine Ebene in einer Hierarchie die benutzerdefinierten Elementformeln der vorherigen Ebene Die benutzerdefinierten Elementformeln der vorhergehenden Ebene überschreiben jedoch die benutzerdefinierten Rollup-Operatoren einer Ebene.  
  
## <a name="see-also"></a>Siehe auch  
 [Definieren von benutzerdefinierten Elementformeln](../../analysis-services/multidimensional-models/attribute-properties-define-custom-member-formulas.md)   
 [Unäre Operatoren in über-und untergeordneten Dimensionen](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-unary-operators.md)  
  
  
