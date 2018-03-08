---
title: C-Datentypen in ODBC | Microsoft Docs
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
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
ms.assetid: c91bef31-3794-4736-966a-d50997b2233c
caps.latest.revision: "26"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 713b9448ecb70b57f0aace7f05aa9b977511323b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="c-data-types-in-odbc"></a>C-Datentypen in ODBC
ODBC definiert die C-Datentypen, die von Anwendungsvariablen und ihre entsprechenden Typ-IDs verwendet werden. Diese werden von den Puffern verwendet, die an die Resultsetspalten und Anweisungsparameter gebunden sind. Angenommen Sie, dass eine Anwendung wünscht eine zum Abrufen von Daten aus einer Resultsetspalte im Zeichenformat vorliegen. Deklariert eine Variable mit dem SQLCHAR *-Datentyp und bindet diese Variable an die Resultsetspalte mit einem Typbezeichner SQL_C_CHAR. Eine vollständige Liste der C-Datentypen und Typ-IDs, finden Sie unter [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 ODBC definiert auch eine standardzuordnung jeder SQL-Datentyps in einem C-Datentyp. Beispielsweise wird eine 2-Byte-Ganzzahl in der Datenquelle eine 2-Byte-Ganzzahl in der Anwendung zugeordnet. Eine Anwendung für die Verwendung der standardzuordnung gibt an, dass der SQL_C_DEFAULT Typbezeichner. Verwendung von dieser Bezeichner wird jedoch aus Gründen der Interoperabilität abgeraten.  
  
 Alle ganzzahlige C-Datentypen in ODBC 1 definierten*.x* signiert wurden. Ohne Vorzeichen C-Datentypen und ihre entsprechenden Typ-IDs wurden in ODBC 2.0 hinzugefügt. Aus diesem Grund Anwendungen und-Treiber benötigen Sie besonders vorsichtig beim Umgang mit 1 sein*.x* Versionen.  
  
## <a name="c-data-type-extensibility"></a>Erweiterbarkeit von C Daten  
 In ODBC 3.8 können Sie die Treiber-spezifischen C-Datentypen angeben. Dies ermöglicht Ihnen, einen SQL-Typ als ein Treiber-spezifischen C-Typ in ODBC-Anwendungen zu binden, beim Aufrufen [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), oder [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md). Dies kann für die Unterstützung der neuen Servertypen nützlich sein, da vorhandene C-Datentypen richtig die neuen Server-Datentypen möglicherweise nicht genau dargestellt. Mit Treiber-spezifischen C-Typen kann die Anzahl der Konvertierungen erhöhen, die Treiber ausführen können.  
  
 Nehmen wir beispielsweise an eine Datenbank-Managementsystem (DBMS) eingeführt, einen neue SQL-Typ **"DateTimeOffset"**, um das Datum und die Uhrzeit mit Zeitzoneninformationen darzustellen. Gäbe es keine bestimmter C-Typ in ODBC, die auf diesem **"DateTimeOffset"**. Eine Anwendung müsste binden **"DateTimeOffset"** als SQL_C_BINARY und wandelt es mit einem benutzerdefinierten Daten eingeben. In ODBC 3.8 Erweiterbarkeit von C Daten ab, kann ein Treiber einen neuen entsprechenden C#-Typ definieren. Der Treiber für den neuen SQL-Typ "DateTimeOffset" kann z. B. einen entsprechenden neuen C#-Typ z. B. SQL_C_DATETIMEOFFSET definieren. Eine Anwendung kann dann den neuen SQL-Typ als ein Treiber-spezifischen C-Typ binden.  
  
 C-Datentyp wird in den Treiber wie folgt definiert:  
  
-   Die ODBC-Kompatibilitätsstufe für eine Anwendung ODBC-Treiber und Treiber-Manager ist 3.8 (oder höher).  
  
-   Von dem Treiber-spezifischen C-Typ des Datenbereichs liegt zwischen 0 x 4000 und 0x7FFF.  
  
-   Der Treiber definiert die Struktur der Daten in den C-Typ entspricht.  Dies kann im SDK treiberspezifische erfolgen.  
  
 Der Treiber-Manager wird nicht überprüft, ob einen C-Typ, der im Bereich von 0 x 4000 und 0x7FFF definiert; der Treiber führt die Überprüfung und datentypkonvertierung. Wenn des Datenbereichs, der dem C-Typ, der an den Treiber-Manager übergeben zwischen 0 x 0000 und 0x3FFF oder 0 x 8000 bis 0xFFFF ist, der Treiber-Manager wird jedoch überprüft die C-Datentyp.  
  
> [!NOTE]  
>  Treiber-spezifischen C-Datentypen sollten in der Treiberdokumentation beschrieben werden.  
  
 Ruft eine Anwendung zum Angeben einer ODBC-Kompatibilitätsstufe des 3.8 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) -Attribut festgelegt, ist mit der SQL_ATTR_ODBC_VERSION **SQL_OV_ODBC3_80**. So ermitteln Sie die Version des Treibers eine Anwendung ruft **SQLGetInfo** mit SQL_DRIVER_ODBC_VER.  
  
 Weitere Informationen zu ODBC 3.8, finden Sie unter [Neuigkeiten in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
## <a name="see-also"></a>Siehe auch  
 [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md)
