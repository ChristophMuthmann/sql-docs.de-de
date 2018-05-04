---
title: Escape-Zeichenfolge wie | Microsoft Docs
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
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37733aadb069cd161427fc8f186647cfba030b6d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="like-escape-sequence"></a>WIE die-Escapesequenz
Verwendung von ODBC Escapesequenzen für die LIKE-Klausel. Die Syntax für diese Escapesequenz lautet wie folgt:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Hinweise  
 In BNF-Schreibweise ist die Syntax folgendermaßen:  
  
 *ODBC-Like-Escape* :: =  
  
 *Initiator der ODBC-esc* Escape '*Escape-Zeichen*" *ODBC-esc-Abschlusszeichen*  
  
 *Escape-Zeichen* :: = *Zeichen*  
  
 *Initiator der ODBC-esc* :: = {}  
  
 *ODBC-esc-Terminator* :: =}  
  
 Um festzustellen, ob der Treiber die LIKE-Escape-unterstützt Sequenz ist, eine Anwendung kann Aufrufen **SQLGetInfo** mit dem Typ der SQL_LIKE_ESCAPE_CLAUSE-Informationen.
