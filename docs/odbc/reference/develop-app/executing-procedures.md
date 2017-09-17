---
title: "Ausführen von Prozeduren | Microsoft Docs"
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
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fa215150c483776f9188ed16044b59500cb257e7
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="executing-procedures"></a>Ausführen von Prozeduren
ODBC definiert eine standard-Escapesequenz für das Ausführen von Prozeduren an. Die Syntax dieser Sequenz sowie ein Codebeispiel, die verwendet werden, finden Sie unter [Prozeduraufrufe](../../../odbc/reference/develop-app/procedure-calls.md).  
  
 Um eine Prozedur auszuführen, führt eine Anwendung die folgenden Aktionen aus:  
  
1.  Legt die Werte aller Parameter an. Weitere Informationen finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md)weiter unten in diesem Abschnitt.  
  
2.  Aufrufe **SQLExecDirect** und übergibt eine Zeichenfolge, enthält die SQL-Anweisung, die die Prozedur ausgeführt wird. Diese Anweisung können die Escape-Zeichenfolge, die von ODBC oder DBMS-spezifische Syntax definiert. Anweisungen, die DBMS-spezifische Syntax verwenden, sind nicht interoperabel.  
  
3.  Wenn **SQLExecDirect** aufgerufen wird, wird den Treiber:  
  
    -   Ruft die aktuellen Parameterwerte ab und konvertiert sie nach Bedarf. Weitere Informationen finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md)weiter unten in diesem Abschnitt.  
  
    -   Ruft die Prozedur in der Datenquelle und sendet sie die konvertierte Parameterwerte. Wie der Treiber die Prozedur aufruft, ist treiberspezifische. Beispielsweise kann es für die Verwendung von SQL-Grammatik für die Datenquelle, und senden diese Anweisung für die Ausführung die SQL-Anweisung ändern, oder es möglicherweise rufen Sie die Prozedur, die direkt mit einem Remoteprozeduraufruf (RPC)-Mechanismus, der im Data Stream-Protokoll des DBMS definiert ist.  
  
    -   Gibt die Werte von jeder Eingabe/Ausgabe- oder Output-Parameter oder den Rückgabewert der Prozedur, vorausgesetzt, dass die Prozedur erfolgreich ausgeführt wird. Diese Werte werden möglicherweise nicht erst verfügbar, nachdem alle anderen Ergebnisse (Zeilenanzahl und Resultsets) generiert, die von der Prozedur verarbeitet wurden. Wenn die Prozedur fehlschlägt, kehrt der Treiber Fehler zurück.
