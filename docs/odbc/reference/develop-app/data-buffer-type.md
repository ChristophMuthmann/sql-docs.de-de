---
title: Daten Puffertyp | Microsoft Docs
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
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7f2f6e48c4fd01106b1ccf4a371d4e522587db1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-buffer-type"></a>Buffer-Datentyp
Die C-Datentyp eines Puffers wird von der Anwendung angegeben. Mit einer einzigen Variablen geschieht dies, wenn die Anwendung die Variable belegt. Mit generischen Arbeitsspeicher – d. h. Speicher verweist Zeiger vom Typ "void" – Dies tritt auf, wenn die Anwendung den Speicher für eine bestimmte Art umgewandelt. Der Treiber ermittelt dieses Typs auf zwei Arten:  
  
-   **Datentypargument Puffer.** Übertragung von Parameterwerten und Resultsetdaten, verwendet werden, z. B. der Puffer mit gebundenen Puffer *TargetValuePtr* in **SQLBindCol**, haben normalerweise Argument zugeordneten Typ, z. B. die  *TargetType* Argument in **SQLBindCol**. In diesem Argument übergibt die Anwendung die C-Typ-ID, die entspricht, in den Typ des Puffers. Z. B. im folgenden Aufruf **SQLBindCol**, der Wert SQL_C_TYPE_DATE weist den Treiber an, die die *Datum* Puffer ist ein SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     Weitere Informationen zu Typ-IDs finden Sie unter der [Datentypen in ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md) weiter unten in diesem Abschnitt.  
  
-   **Der vordefinierte Typ.** Puffer zum Senden und Abrufen von Optionen oder Attribute, z. B. den Puffer verweist die *InfoValuePtr* Argument in **SQLGetInfo**, haben einen festen Typ, der auf der angegebenen Option abhängig ist. Der Treiber wird davon ausgegangen, dass der Datenpuffer dieses Typs ist; Es ist die Anwendung dafür verantwortlich, um einen Puffer dieses Typs zuzuordnen. Um z. B. im folgenden Aufruf **SQLGetInfo**, der Treiber geht davon aus, der Puffer ist eine 32-Bit-Ganzzahl, da es sich handelt, was die SQL_STRING_FUNCTIONS-Option erforderlich:  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 Der Treiber verwendet die C-Datentyp zum Interpretieren der Daten im Puffer.
