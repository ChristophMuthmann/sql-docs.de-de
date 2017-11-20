---
title: "Escapesequenz für äußere Joins | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d208b7de815f090e5f61d3d807912c53c4253e31
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
  
 *Äußerer Join* :: = *Tabellenname* [*Korrelationsname*] {links &#124; RECHTS &#124; VOLLSTÄNDIGE}  
  
 OUTER JOIN {*Tabellenname* [*Korrelationsname*] &#124; *äußerer Join*} ON  
  
 *Search-*  
  
 *Bedingung*  
  
 *Korrelationsname* :: = *definiert-Benutzernamens*  
  
 *Initiator der ODBC-esc* :: = {}  
  
 *ODBC-esc-Terminator* :: =}  
  
 Um zu bestimmen, welche Teile der diese Anweisung unterstützt werden, eine Anwendung ruft **SQLGetInfo** mit dem Typ der SQL_OJ_CAPABILITIES-Informationen. Für äußere Joins *Suchbedingung* darf nur die Join-Bedingung zwischen dem angegebenen *Tabellennamen*.

