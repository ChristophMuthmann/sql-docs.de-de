---
title: GENAUE SET-Befehls | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c94efa07d23249c9fc3e9d661998419b68f7b624
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
 [SET ANSI-Befehl](../../odbc/microsoft/set-ansi-command.md)

