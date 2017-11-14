---
title: Escape-Zeichensequenzen in ODBC | Microsoft Docs
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
- escape sequences [ODBC]
- SQL statements [ODBC], escape sequences
- escape sequences [ODBC], about escape sequences
ms.assetid: cf229f21-6c38-4b5b-aca8-f1be0dfeb3d0
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 92fd9745bccacad3d7487c3ed9f1bee58eeb4411
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="escape-sequences-in-odbc"></a>Escape-Zeichensequenzen in ODBC
Eine Anzahl von Funktionen der Programmiersprache, z. B. äußere Joins und Aufrufe von Skalarfunktionen werden häufig von DBMS implementiert. Allerdings sind tendenziell die Syntax für diese Funktionen DBMS-spezifische, selbst wenn der standard-Syntax von verschiedenen normungsinstitutionen definiert sind. Aus diesem Grund definiert ODBC-Escapesequenzen, die standard-Syntax für die folgenden Sprachfunktionen enthalten:  
  
-   Date, Time, Timestamp und Datetime-Intervall-Literale  
  
-   Skalare Funktionen wie z. B. numerische Zeichenfolge und Datentypkonvertierungsfunktionen  
  
-   WIE Prädikat Escape-Zeichen  
  
-   Äußere joins  
  
-   Prozeduraufrufe  
  
 Die von ODBC verwendete Escapesequenz lautet wie folgt:  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Hinweise  
 Die-Escapesequenz ist erkannt und analysiert von Treibern, die die Escapesequenzen durch DBMS-spezifische Grammatik zu ersetzen. Weitere Informationen zu escapesequenzsyntax, finden Sie unter [Escapesequenzen für ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) in Anhang C: SQL-Grammatik.  
  
> [!NOTE]  
>  In ODBC 2. *x*, dies war die Standardsyntax der Escapesequenz: **--(\*Hersteller (***Herstellername***), Product (** *Produktname***)***Erweiterung*  **\*)--**  
>   
>  Zusätzlich zu dieser Syntax eine Kurzsyntax für das Formular definiert wurde: **{***Erweiterung***}**  
>   
>  In ODBC 3. *x*die Langform der Escapesequenz ist veraltet und wird ausschließlich die Kurzform verwendet.  
  
 Da die Escapesequenzen an die DBMS-spezifische Syntax vom Treiber zugeordnet sind, kann eine Anwendung die Escape-Zeichenfolge oder die DBMS-spezifische Syntax verwenden. Anwendungen, die die DBMS-spezifische Syntax verwenden, können jedoch nicht interoperabel sein. Wenn Sie die-Escapesequenz verwenden, sollten Anwendungen sicherstellen, dass es sich bei SQL_ATTR_NOSCAN-Anweisungsattribut ausgeschaltet ist, die Standardeinstellung. Andernfalls wird die-Escapesequenz direkt an die Datenquelle gesendet werden, in denen sie in der Regel einen Syntaxfehler verursacht wird.  
  
 Treiber unterstützen nur Escapesequenzen, die sie zum zugrunde liegenden Sprachfunktionen zuordnen kann. Z. B. wenn die Datenquelle keine äußeren Joins unterstützt, weder wird des Treibers. Um zu bestimmen, welche Escapesequenzen unterstützt werden, eine Anwendung ruft **SQLGetTypeInfo** und **SQLGetInfo**. Weitere Informationen finden Sie im nächsten Abschnitt [Date, Time und Timestamp-Literale](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Date, Time und Timestamp-Literale](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [Aufrufe von Skalarfunktionen](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [WIE Prädikat Escape-Zeichen](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [Äußere Joins](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [Prozeduraufrufe](../../../odbc/reference/develop-app/procedure-calls.md)

