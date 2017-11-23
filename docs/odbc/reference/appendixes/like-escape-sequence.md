---
title: Escape-Zeichenfolge wie | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 49004343a4081db0c617b97b09570bd7557f441e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
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
