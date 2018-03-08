---
title: Call-Escapesequenz Prozedur | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
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
ms.openlocfilehash: 080c74baca0cd641b14de3746657b4bfb09bc6dc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
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
