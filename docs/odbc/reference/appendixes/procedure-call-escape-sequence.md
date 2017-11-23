---
title: Call-Escapesequenz Prozedur | Microsoft Docs
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
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c59924e443d738b1bc3e61092a02e617f0d39eff
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="procedure-call-escape-sequence"></a>Prozedur Call-Escapesequenz
ODBC verwendet Escapesequenzen für Prozeduraufrufe an. Die Syntax für diese Escapesequenz lautet wie folgt:  
  
 **{**[? =]**Aufrufen** *Prozedurnamen*[**(**[*Parameter*] [, [*Parameter*]] ... **)**]**}**  
  
 In BNF-Schreibweise ist die Syntax folgendermaßen:  
  
 *ODBC-Prozedur-Escape* :: =  
  
 &#124; *Initiator der ODBC-esc* [? =] aufrufen *Prozedur ODBC-esc-Abschlusszeichen*  
  
 *Prozedur* :: = *Prozedurnamen* &#124; *Prozedurnamen* (*Prozedurparameterliste*)  
  
 *Prozedur-ID* :: = *definiert-Benutzernamens*  
  
 *Prozedurnamen* :: = *Prozedur-ID*  
  
 &#124; *Besitzername*. *Prozedur-ID*  
  
 &#124; *Katalognamen Katalogtrennzeichen* *Prozedur-ID*  
  
 &#124; *Katalognamen Katalogtrennzeichen* [*Besitzername*]. *Prozedur-ID*  
  
 (Die dritte Syntax ist nur gültig, wenn die Datenquelle Besitzer nicht unterstützt.)  
  
 *Besitzername* :: = *definiert-Benutzernamens*  
  
 *Katalogname* :: = *definiert-Benutzernamens*  
  
 *Katalogtrennzeichen* :: = {*implementierungsdefinierte*}  
  
 (Katalogtrennzeichen zurückgegeben wird, über **SQLGetInfo** mit der Option zur Verwaltung SQL_CATALOG_NAME_SEPARATOR.)  
  
 *Prozedurparameterliste* :: = *Prozedurparameter*  
  
 &#124; *Prozedurparameter*, *Prozedurparameterliste*  
  
 *Prozedurparameter* :: = *dynamische Parameter* &#124; *literal* &#124; *leere Zeichenfolge*  
  
 *leere Zeichenfolge* :: =  
  
 *Initiator der ODBC-esc* :: = {}  
  
 *ODBC-esc-Terminator* :: =}  
  
 (Wenn Parameter einer Prozedur eine leere Zeichenfolge ist, verwendet die Prozedur den Standardwert für diesen Parameter.)  
  
 Um zu bestimmen, ob die Datenquelle, Prozeduren unterstützt und der Treiber die Aufrufsyntax für die ODBC-Prozedur unterstützt, eine Anwendung aufrufen kann **SQLGetInfo** mit dem Typ der SQL_PROCEDURES-Informationen.
