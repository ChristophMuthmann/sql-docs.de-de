---
title: Zuordnen von in der Treiber-Manager-Funktion | Microsoft Docs
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
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a4af23925a410fba2d1e79691172975a62507472
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="function-mapping-in-the-driver-manager"></a>Funktionszuordnung im Treiber-Manager
Der Treiber-Manager unterstützt zwei Einstiegspunkte für Funktionen, die Zeichenfolgenargumente verwenden. Die Funktion nicht ergänzten (**SQLDriverConnect**) ist die ANSI-Form der Funktion. Unicode-Format mit ergänzt wird eine *W* (**SQLDriverConnectW**.)  
  
 Die ODBC-Headerdatei unterstützt auch Funktionen ergänzt, die mit einer *A,* (**SQLDriverConnectA**) der Übersichtlichkeit halber gemischten ANSI/Unicode-Anwendungen. Aufrufe an die **ein** Funktionen sind tatsächlich Aufrufe in den nicht ergänzten Einstiegspunkt (**SQLDriverConnect**.)  
  
 Wenn die Anwendung, mit der _UNICODE kompiliert wird **#define**, die ODBC-Header-Datei ordnet nicht ergänzten Funktionsaufrufe (**SQLDriverConnect**) auf die Unicode-Version (**SQLDriverConnectW** .)  
  
 Der Treiber-Manager einen Treiber als Unicode-Treiber erkennt, wenn **SQLConnectW** wird vom Treiber unterstützt.  
  
 Wenn der Treiber einen Unicode-Treiber ist, führt der Treiber-Manager Funktionsaufrufe wie folgt aus:  
  
-   Übergibt eine Funktion ohne Zeichenfolgenargumente oder Parameter direkt über den Treiber.  
  
-   Übergeben von Unicode-Funktionen (mit der *W* Suffix) direkt über den Treiber.  
  
-   Konvertiert eine ANSI-Funktion (mit der *ein* Suffix) an eine Unicode-Funktion (mit der *W* Suffix) durch die Zeichenfolgenargumente in Unicode konvertiert Zeichen auf und übergibt Sie an den Treiber Unicode-Funktion.  
  
 Wenn der Treiber eine ANSI-Treiber ist, führt der Treiber-Manager Funktionsaufrufe wie folgt aus:  
  
-   Funktionen ohne Zeichenfolgenargumente oder Parameter, die direkt über übergeben an den Treiber.  
  
-   Konvertiert Unicode-Funktionen (mit der *W* Suffix) in ein ANSI-Funktionsaufruf und übergibt sie an den Treiber.  
  
-   Eine ANSI-Funktion übergeben direkt an den Treiber.  
  
 Der Treiber-Manager ist unicodefähige intern. Daher ist die optimale Leistung durch einer Unicode-Anwendung mit einem Unicode-Treiber arbeiten abgerufen, da der Treiber-Manager Unicode-Funktionen über die an den Treiber übergibt. Wenn eine ANSI-Anwendung mit einem ANSI-Treiber arbeitet, der Treiber-Manager müssen Zeichenfolgen von ANSI in Unicode konvertiert bei der Verarbeitung von einigen Funktionen, wie z. B. **SQLDriverConnect**. Nach der Verarbeitung der Funktion, muss der Treiber-Manager klicken Sie dann die Unicode-Zeichenfolge in ANSI zurückkonvertieren vor dem Senden der Funktion für den ANSI-Treiber.  
  
 Eine Anwendung sollte nicht ändern oder dessen Puffern für gebundene Parameter zu lesen, wenn der Treiber SQL_STILL_EXECUTING oder SQL_NEED_DATA zurückgibt. Der Treiber-Manager bewirkt, dass die Puffer in ANSI gebunden werden, bis der Treiber SQL_SUCCESS, SQL_SUCCESS_WITH_INFO oder SQL_ERROR zurückgegeben. Eine Multithreadanwendung sollte nicht auf alle gebundenen Parameterwerte zugreifen, die ein anderer Thread auf eine SQL-Anweisung ausführt. Der Treiber-Manager die Daten von Unicode in ANSI "Direktes" konvertiert, und der andere Thread möglicherweise ANSI-Daten in diesen Puffern, während der Treiber noch die SQL-Anweisung verarbeitet wird. Anwendungen, die Unicode-Daten an eine ANSI-Treiber zu binden, müssen nicht zwei verschiedene Spalten in die gleiche Adresse binden.
