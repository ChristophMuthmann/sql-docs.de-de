---
title: Prozeduraufrufe | Microsoft Docs
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
- escape sequences [ODBC], procedure calls
- procedure calls [ODBC]
ms.assetid: 145130cc-40e7-4722-8417-dff131084752
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f907cf8700a683988277e84b93f9fc3bdae11317
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="procedure-calls"></a>Prozeduraufrufe
Ein *Prozedur* ein ausführbares Objekt in der Datenquelle gespeichert ist. In der Regel handelt es sich dabei um eine oder mehrere vorkompilierte SQL-Anweisungen. Ist die-Escapesequenz zum Aufrufen einer Prozedur  
  
 **{**[**? =**]**Aufrufen** *Prozedurnamen*[**(**[*Parameter*] [**,**[*Parameter*]]... **)**]**}**  
  
 wobei *Prozedurnamen* gibt den Namen einer Prozedur und *Parameter* gibt einen Prozedurparameter an.  
  
 Weitere Informationen über die Prozedur Call-Escapesequenz finden Sie unter [Prozedur Call-Escapesequenz](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md) in Anhang C: SQL-Grammatik.  
  
 Eine Prozedur kann 0 (null) oder mehr Parameter haben. Sie können auch einen Wert zurückgeben, wie angegeben durch die optionale parametermarkierung **? =** am Anfang der Syntax. Wenn *Parameter* ist eine Eingabe oder ein Eingabe-/Ausgabeparameter kann ein Literal oder eine parametermarkierung. Interoperable Anwendungen ausführen sollte jedoch immer parametermarkierungen verwenden, da einige Datenquellen nicht literal Parameterwerte akzeptieren. Wenn *Parameter* ist ein Output-Parameter muss er eine parametermarkierung. Müssen gebundene parametermarkierungen mit **SQLBindParameter** vor dem Aufruf der Prozedur-Anweisung ausgeführt wird.  
  
 Eingabe- und Eingabe-/Ausgabeparameter müssen in Prozeduraufrufen nicht angegeben werden. Wenn eine Prozedur mit Klammern aber ohne Parameter, wie z. B. aufgerufen wird, {Aufrufen *Prozedurnamen*()}, der Treiber angewiesen, die Datenquelle auf den Standardwert für den ersten Parameter zu verwenden. Wenn die Prozedur keine Parameter aufweist, kann dies dazu führen, dass die Prozedur fehlschlägt. Wenn eine Prozedur ohne Klammern, wie z. B. aufgerufen wird {aufrufen *Prozedurnamen*}, sendet der Treiber keine Parameterwerte.  
  
 Literalwerte können in Prozeduraufrufen für Eingabe- und Eingabe-/Ausgabeparameter angegeben werden. Nehmen wir beispielsweise an die Prozedur **InsertOrder** fünf Eingabeparameter aufweisen. Beim folgenden Aufruf **InsertOrder** der erste Parameter und stellt ein Literal für den zweiten Parameter verwendet eine parametermarkierung für den dritten, vierten und fünften Parameter:  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 Beachten Sie, dass wenn ein Parameter nicht angegeben ist, muss das Komma, begrenzen es von anderen Parametern weiterhin angezeigt. Wenn ein Eingabe- oder ein Eingabe-/Ausgabeparameter ausgelassen wird, verwendet die Prozedur den Standardwert des Parameters. Alternative Möglichkeit zum angeben, dass der Standardwert eines Eingabe- oder e/a-Parameters wird zum Festlegen des Werts des Längen-/Indikatorpuffers, die an den Parameter auf SQL_DEFAULT_PARAM gebunden sind.  
  
 Wenn ein Eingabe-/Ausgabeparameter ausgelassen wird oder ein Literal für den Parameter angegeben ist, verwirft der Treiber den Ausgabewert an. Entsprechend verwirft der Treiber den Rückgabewert, wenn die Parametermarkierung für den Rückgabewert einer Prozedur ausgelassen wird. Wenn eine Anwendung den Parameter des Rückgabewerts für eine Prozedur angibt, die keinen Wert zurückgibt, legt der Treiber den Wert des an den Parameter gebundenen Längen-/Indikatorpuffers auf SQL_NULL_DATA fest.  
  
 Nehmen Sie an, dass die Prozedur PARTS_IN_ORDERS ein Resultset erstellt, die eine Liste der Aufträge enthält, die eine bestimmten Teilenummer enthalten. Der folgende Code ruft dieses Verfahren für die Teilenummer 544:  
  
```  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_SLONG, SQL_INTEGER, 0, 0,  
                  &PartID, 0, PartIDInd);  
  
// Place the department number in PartID.  
PartID = 544;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "{call PARTS_IN_ORDERS(?)}", SQL_NTS);  
```  
  
 Um zu bestimmen, ob eine Datenquelle Prozeduren unterstützt, eine Anwendung ruft **SQLGetInfo** mit der Option SQL_PROCEDURES.  
  
 Weitere Informationen zu Verfahren finden Sie unter [Prozeduren](../../../odbc/reference/develop-app/procedures-odbc.md).

