---
title: Zeichenfolgenfunktionen (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- ODBC string functions [ODBC]
- string functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], string functions
- FoxPro ODBC driver [ODBC], string functions
ms.assetid: 1974fd26-ef0d-45d5-860b-298917c8e9c3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 482c21b4c9f872490ac9a2d36165fdc3fc9d8246
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>String-Funktionen (Visual FoxPro-ODBC-Treiber)
In der folgenden Tabelle werden die ODBC-Funktionen zur Zeichenfolgenmanipulation von der Visual FoxPro-ODBC-Treiber unterstützt. Wenn die Visual FoxPro-Grammatik für dieselbe Funktion aus der ODBC-Syntax unterscheidet, wird der entsprechende Visual FoxPro aufgeführt.  
  
|ODBC-Grammatik|Visual FoxPro-Grammatik|  
|------------------|---------------------------|  
|ASCII *(String_exp)*|ASC *(String_exp)*|  
|CHAR *(Code)*|CHR *(String_exp)*|  
|CONCAT *(string_exp2 und string_exp1)*|*string_exp1 + string_exp2 und*|  
|Unterschied *(string_exp2 und string_exp1)*||  
|Fügen Sie *(string_exp1, Start, Länge, string_exp2 und)*|STUFF *(string_exp1, Start, Länge, string_exp2 und)*|  
|LCASE *(String_exp)*|NIEDRIGERE *(String_exp)*|  
|Links *(String_exp, Anzahl)*||  
|Länge *(String_exp)*|LEN *(String_exp)*|  
|LTRIM *(String_exp)*||  
|Wiederholen Sie die *(String_exp, Anzahl)*|Replizieren *(String_exp, Anzahl)*|  
|Ersetzen Sie *(string_exp1, string_exp2 und, string_exp3)*|STRTRAN *(string_exp1, string_exp2 und, string_exp3)*|  
|RECHTS *(String_exp, Anzahl)*||  
|RTRIM *(String_exp)*||  
|SOUNDEX *(String_exp)*||  
|Speicherplatz *(Anzahl)*||  
|TEILZEICHENFOLGE *(String_exp, Start, Länge)*|SUBSTR *(String_exp, Start, Länge)*|  
|UCASE *(String_exp)*|OBERE *(String_exp)*|
