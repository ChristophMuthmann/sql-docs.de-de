---
title: Prozedurparameter | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- procedure parameters [ODBC]
ms.assetid: 54fd857e-d2cb-467d-bb72-121e67a8e88d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc7e82b134ef578907dc0b5e84aa0e1ed7224027
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="procedure-parameters"></a>Prozedurparameter
In Prozeduraufrufen können eingegeben werden, Eingabe/Ausgabe- oder Ausgabeparameter enthalten. Dies unterscheidet sich von Parametern in allen anderen SQL-Anweisungen, die immer Eingabeparameter sind.  
  
 Eingabeparameter werden verwendet, um Werte an die Prozedur zu senden. Angenommen Sie, dass die Parts-Tabelle die Spalten PartID, Beschreibung und Preis hat. Die Prozedur InsertPart möglicherweise einen Eingabeparameter für jede Spalte in der Tabelle. Beispiel:  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 Ein Treiber sollte nicht den Inhalt der Eingabepuffer bis ändern **SQLExecDirect** oder **SQLExecute** SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE oder SQL_NO_DATA zurückgibt. Der Inhalt des Eingabepuffers sollte nicht geändert werden während **SQLExecDirect** oder **SQLExecute** gibt SQL_NEED_DATA oder SQL_STILL_EXECUTING zurück.  
  
 Eingabe/Ausgabe-Parameter werden verwendet, um Werte an Prozeduren senden und Abrufen von Werten aus Prozeduren. Mit dem gleichen Parameter als sowohl Eingabe-als auch ein Output-Parameter tendenziell verwirrend sein und sollte vermieden werden. Nehmen wir beispielsweise an eine Prozedur akzeptiert eine Auftrags-ID und gibt die ID des Kunden zurück. Dies kann mit einem einzelnen Eingabe-/Ausgabeparameter definiert werden:  
  
```  
{call GetCustID(?)}  
```  
  
 Es könnte besser sein, verwenden Sie zwei Parameter: einen Eingabeparameter für die Bestell-ID und eines Ausgabe- oder Eingabe-/Ausgabeparameter für die Kunden-ID:  
  
```  
{call GetCustID(?, ?)}  
```  
  
 Output-Parameter den Prozedur zurückgegebene Wert abrufen und Abrufen von Werten aus Prozedurargumente verwendet; Prozeduren, die Werte zurückgeben werden manchmal als bezeichnet *Funktionen*. Nehmen wir beispielsweise an die **GetCustID** erwähnten Prozedur gibt einen Wert, der angibt, ob die Reihenfolge gefunden werden konnte. Im folgenden Aufruf der erste Parameter ist ein Output-Parameter, die zum Abrufen von des Prozedur zurückgegebene Wert, der zweite Parameter ist ein Eingabeparameter verwendet, um die Bestell-ID anzugeben, und der dritte Parameter ist ein Output-Parameter verwendet, um die Kunden-ID abzurufen:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 Treiber Behandeln von Werten für die Eingabe und Eingabe/Ausgabe-Parameter in Prozeduren nicht anders als Eingabeparameter in anderen SQL­Anweisungen. Wenn die Anweisung ausgeführt wird, sie rufen Sie die Werte der Variablen für diese Parameter gebunden und mit der Datenquelle zu senden.  
  
 Nachdem die Anweisung ausgeführt wurde, speichern Treiber zurückgegebenen Werte der e/a und Output-Parameter in der Variablen, die an diese Parameter gebunden. Diese zurückgegebenen Werte sind nicht unbedingt erst festgelegt werden, nachdem alle von der Prozedur zurückgegebene Ergebnisse abgerufen wurden und **SQLMoreResults** SQL_NO_DATA zurückgegeben hat. Wenn die Anweisung einen Fehler ergibt, werden den Inhalt des Puffers Eingabe-/Ausgabeparameter oder Ausgabepuffer-Parameter nicht definiert.  
  
 Ruft die Anwendung **SQLProcedure** bestimmen, ob eine Prozedur einen Rückgabewert verfügt. Sie ruft **SQLProcedureColumns** zum Bestimmen des Typs (Rückgabewert, Eingabe-, Eingabe/Ausgabe- oder Ausgabeparameter) der einzelnen Prozedurparameter.
