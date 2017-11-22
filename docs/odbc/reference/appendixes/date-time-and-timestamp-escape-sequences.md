---
title: Date, Time und Timestamp-Escapesequenzen | Microsoft Docs
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
- escape sequences [ODBC]
- escape sequences [ODBC], about escape sequences
- ODBC escape sequences [ODBC], about escape sequences
- ODBC escape sequences [ODBC]
ms.assetid: 67b7dee0-e5b1-4469-a626-0c7767852b80
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e94eb22965a841d514e257fc63045dfaa5ddb757
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="date-time-and-timestamp-escape-sequences"></a>Date, Time und Timestamp-Escapesequenzen
ODBC definiert Escapesequenzen für Date, Time und Timestamp-Literale. Die Syntax dieser Escapesequenzen lautet wie folgt:  
  
```  
  
{d 'value'}  
{t 'value'}  
{ts 'value'}  
```  
  
 In BNF-Schreibweise ist die Syntax folgendermaßen:  
  
```  
  
      ODBC-date-time-escape ::=  
     ODBC-date-escape  
     | ODBC-time-escape  
     | ODBC-timestamp-escapeODBC-date-escape ::=  
     ODBC-esc-initiator d 'date-value' ODBC-esc-terminatorODBC-time-escape ::=  
     ODBC-esc-initiator t 'time-value' ODBC-esc-terminatorODBC-timestamp-escape ::=  
     ODBC-esc-initiator ts 'timestamp-value' ODBC-esc-terminatorODBC-esc-initiator ::= {  
ODBC-esc-terminator ::= }  
date-value ::=   
     years-value date-separator months-value date-separator days-valuetime-value ::=   
     hours-value time-separator minutes-value time-separatorseconds-valuetimestamp-value ::= date-value timestamp-separator time-valuedate-separator ::= -  
time-separator ::= :  
timestamp-separator ::=  
     (The blank character)years-value ::= digit digit digit digitmonths-value ::= digit digitdays-value ::= digit digithours-value ::= digit digitminutes-value ::= digit digitseconds-value ::= digit digit[.digit...]  
```  
  
## <a name="remarks"></a>Hinweise  
 Das literal Escapesequenzen Date, Time und Timestamp werden unterstützt, wenn die Date, Time und Timestamp-Datentypen von der Datenquelle unterstützt werden. Eine Anwendung sollte Aufrufen **SQLGetTypeInfo** um zu bestimmen, ob dieser Datentypen unterstützt werden.
