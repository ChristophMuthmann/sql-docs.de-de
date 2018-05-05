---
title: GENAUE SET-Befehls | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6f5576ec5a1275914ee0558cf3fcd151ee3c3cc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="set-exact-command"></a>GENAUE SET-Befehl
Legt die Regeln zum Vergleichen von zwei Zeichenfolgen unterschiedlicher Länge verfährt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>Argumente  
 ON  
 Gibt an, dass Ausdrücke Zeichen für Zeichen Äquivalenz entsprechen müssen. Jeder nachfolgenden Leerzeichen in den Ausdrücken werden für den Vergleich ignoriert. Für den Vergleich wird die kürzere der beiden Ausdrücke auf der rechten Seite mit Leerzeichen, entsprechend der Länge des längeren Ausdrucks aufgefüllt.  
  
 OFF  
 (Standard). Gibt an, um entsprechende werden Ausdrücke entsprechen müssen Zeichen für Zeichen bis das Ende des Ausdrucks auf der rechten Seite erreicht ist.  
  
## <a name="remarks"></a>Hinweise  
 Die genauen festlegen Einstellung hat keine Auswirkungen, wenn beide Zeichenfolgen die gleiche Länge aufweisen.  
  
## <a name="string-comparisons"></a>Vergleich von Zeichenfolgen  
 Visual FoxPro verfügt über zwei relationalen Operatoren, die auf Gleichheit zu testen.  
  
 Die = Operator führt einen Vergleich zwischen zwei Werten desselben Typs. Dieser Operator wird zum Vergleichen von Zeichen, numerischen, Datums- und logischer Daten geeignet.  
  
 Wenn Sie jedoch Zeichenausdrücke mit Vergleichen der =-Operator, die Ergebnisse möglicherweise nicht genau den erwarteten. Zeichenausdrücke verglichen werden Zeichen für Zeichen von links nach rechts, bis einer der Ausdrücke bis zum Ende des Ausdrucks auf der rechten Seite der nicht gleich dem anderem ist den =-Operator (SET genaue OFF), erreicht ist oder bis die Enden der beiden Ausdrücke sind erreicht (SET EXACT ON).  
  
 Der Operator ==-Operator kann verwendet werden, wenn ein genaue Vergleich mit Zeichendaten benötigt wird. Wenn zwei Zeichenausdrücken mit verglichen werden die == Operator, der Ausdrücke auf beiden Seiten des dem == Operator darf genau dieselben Zeichen, einschließlich Leerzeichen als gleich betrachtet werden. Die genaue festgelegt Einstellung wird ignoriert, wenn Zeichenfolgen verglichen werden mit ==.  
  
 Die folgende Tabelle zeigt, wie die Wahl des Operators und die Einstellung SET EXACT Vergleiche auswirken. (Ein Unterstrich stellt ein Leerzeichen dar.)  
  
|Vergleich|= GENAUE DEAKTIVIEREN|= GENAUE AUF|== GENAUE ON oder OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"Abc" = "Abc"|Übereinstimmung|Übereinstimmung|Übereinstimmung|  
|"Ab" = "Abc"|Keine Übereinstimmung|Keine Übereinstimmung|Keine Übereinstimmung|  
|"Abc" = "Ab"|Übereinstimmung|Keine Übereinstimmung|Keine Übereinstimmung|  
|"Abc" = "Ab_"|Keine Übereinstimmung|Keine Übereinstimmung|Keine Übereinstimmung|  
|"Ab" = "Ab_"|Keine Übereinstimmung|Übereinstimmung|Keine Übereinstimmung|  
|"Ab_" = "Ab"|Übereinstimmung|Übereinstimmung|Keine Übereinstimmung|  
|"" = "Ab"|Keine Übereinstimmung|Keine Übereinstimmung|Keine Übereinstimmung|  
|"Ab" = ""|Übereinstimmung|Keine Übereinstimmung|Keine Übereinstimmung|  
|"__" = ""|Übereinstimmung|Übereinstimmung|Keine Übereinstimmung|  
|"" = "___"|Keine Übereinstimmung|Übereinstimmung|Keine Übereinstimmung|  
|TRIM("___") = ""|Übereinstimmung|Übereinstimmung|Übereinstimmung|  
|"" = TRIM("___")|Übereinstimmung|Übereinstimmung|Übereinstimmung|  
  
## <a name="see-also"></a>Siehe auch  
 [Befehl SET ANSI](../../odbc/microsoft/set-ansi-command.md)
