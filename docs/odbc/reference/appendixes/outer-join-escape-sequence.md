---
title: Escapesequenz für äußere Joins | Microsoft Docs
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
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31d7ea1f4a349e2a0207481cb85ab898548bd98d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="outer-join-escape-sequence"></a>Escapesequenz für äußere Joins
Verwendung von ODBC-Escapesequenzen für äußere Joins. Die Syntax für diese Escapesequenz lautet wie folgt:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Hinweise  
 In BNF-Schreibweise ist die Syntax folgendermaßen:  
  
 *ODBC-outer-Joins-Escape* :: =  
  
 *Initiator der ODBC-esc* ABl. *äußerer Join ODBC-esc-Abschlusszeichen*  
  
 *Äußerer Join* :: = *Tabellenname* [*Korrelationsname*] {Links &#124; rechts &#124; vollständige}  
  
 ÄUßERER JOIN {*Tabellenname* [*Korrelationsname*] &#124; *äußerer Join*} ON  
  
 *Search-*  
  
 *Bedingung*  
  
 *Korrelationsname* :: = *definiert-Benutzernamens*  
  
 *Initiator der ODBC-esc* :: = {}  
  
 *ODBC-esc-Terminator* :: =}  
  
 Um zu bestimmen, welche Teile der diese Anweisung unterstützt werden, eine Anwendung ruft **SQLGetInfo** mit dem Typ der SQL_OJ_CAPABILITIES-Informationen. Für äußere Joins *Suchbedingung* darf nur die Join-Bedingung zwischen dem angegebenen *Tabellennamen*.
