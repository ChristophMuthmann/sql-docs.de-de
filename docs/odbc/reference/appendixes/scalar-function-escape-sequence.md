---
title: Escapesequenz Skalarfunktion | Microsoft Docs
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
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 513df8ccd679ec2236822f780400c3cc39e37609
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="scalar-function-escape-sequence"></a>Escapesequenz Skalarfunktion
Verwendung von ODBC Escapesequenzen für Skalarfunktionen. Die Syntax für diese Escapesequenz lautet wie folgt:  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>Hinweise  
 In BNF-Schreibweise ist die Syntax folgendermaßen:  
  
 *ODBC-Skalar-Funktion-Escape* :: =  
  
 *Initiator der ODBC-esc* fn *Skalarfunktion ODBC-esc-Abschlusszeichen*  
  
 *Skalare Funktion* :: = *Funktionsnamen* (*Argumentliste*)  
  
 (Die Definitionen für die Nichtterminale *Funktionsnamen* und *Funktionsnamen* (*Argumentliste*) abgeleitet werden, aus der Liste von Skalarfunktionen in [ Anhang E: Skalarfunktionen](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *Initiator der ODBC-esc* :: = {}  
  
 *ODBC-esc-Terminator* :: =}  
  
 Um zu bestimmen, ob die Datenquelle, Prozeduren unterstützt und der Treiber die Aufrufsyntax für die ODBC-Prozedur unterstützt, eine Anwendung aufrufen kann **SQLGetInfo**. Weitere Informationen finden Sie unter [Anhang E: Skalarfunktionen](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).
