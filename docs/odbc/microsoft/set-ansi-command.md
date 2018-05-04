---
title: SET ANSI-Befehl | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b713588ba8140b74f19ccb1e9a90b1fa1949754a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="set-ansi-command"></a>SET ANSI-Befehl
Bestimmt, wie Vergleiche zwischen Zeichenfolgen unterschiedlicher Länge verfährt vorgenommen werden, mit den =-Operator in Visual FoxPro-SQL-Befehlen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>Argumente  
 ON  
 (Standard für den Treiber; der Standardwert für Visual FoxPro ist OFF). Füllt die kürzere Zeichenfolge durch die Leerzeichen zu wird benötigt, erleichtern desto länger gleich Zeichenfolgenlänge. Die beiden Zeichenfolgen werden dann verglichenen Zeichen für Zeichen, die für ihre gesamte Länge. Betrachten Sie diesen Vergleich:  
  
```  
'Tommy' = 'Tom'  
```  
  
 Das Ergebnis wird "false" (. F.) Wenn SET ANSI on ist, da beim Auffüllen werden "Tom" wird "Tom" und die Zeichenfolgen "Tom" und "Torsten" stimmen nicht Zeichen für Zeichen überein.  
  
 Der Operator ==-Operator verwendet diese Methode für Vergleiche im Visual FoxPro-SQL-Befehle.  
  
 OFF  
 Gibt an, dass die kürzere Zeichenfolge nicht mit Leerzeichen aufgefüllt werden. Die beiden Zeichenfolgen verglichen werden Zeichen für Zeichen bis Ende die kürzere Zeichenfolge erreicht ist. Betrachten Sie diesen Vergleich:  
  
```  
'Tommy' = 'Tom'  
```  
  
 Das Ergebnis wird "Wahr" (. T.) Wenn SET ANSI deaktiviert ist, da der Vergleich nach "Tom" beendet wird.  
  
## <a name="remarks"></a>Hinweise  
 SET ANSI bestimmt, ob der kürzere der beiden Zeichenfolgen mit Leerzeichen aufgefüllt wird, wenn eine SQL-Zeichenfolgenvergleich vorgenommen wird. SET ANSI hat keine Auswirkungen auf den Operator ==-Operator; Bei Verwendung der Operator ==-Operator, die kürzere Zeichenfolge wird immer mit Leerzeichen für den Vergleich aufgefüllt.  
  
## <a name="string-order"></a>Zeichenfolge-Reihenfolge  
 In SQL-Befehlen, die links-nach-rechts-Reihenfolge der beiden Zeichenfolgen in einem Vergleich ist Irrelevantswitching eine Zeichenfolge auf einer Seite der = oder == Operator, um das andere wirkt sich nicht auf das Ergebnis des Vergleichs.  
  
## <a name="see-also"></a>Siehe auch  
 [Wählen Sie-SQL-Befehl](../../odbc/microsoft/select-sql-command.md)   
 [Befehl SET EXACT](../../odbc/microsoft/set-exact-command.md)
