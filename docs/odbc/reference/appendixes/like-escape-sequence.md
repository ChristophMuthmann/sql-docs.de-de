---
title: Escape-Zeichenfolge wie | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 678f2f8f720823ef5658ba7ee1e1391bbebc1c50
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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

