---
title: Mehrere Ergebnisse | Microsoft Docs
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
- SQLMoreResults function [ODBC], multiple results
- row counts [ODBC]
- multiple results [ODBC]
- result sets [ODBC], multiple results
- SQLGetInfo function [ODBC], multiple results
ms.assetid: a3c32e4b-8fe7-4a33-ae39-ae664001f315
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e537a1a767d0789333659d1aa26e57e11c42195e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="multiple-results"></a>Mehrere Ergebnisse
Ein *Ergebnis* ist etwas von der Datenquelle zurückgegeben, nachdem eine Anweisung ausgeführt wird. ODBC verfügt über zwei Arten von Ergebnissen: Resultsets und Zeilen-. *Zeilen-* sind die Anzahl der Zeilen, die von einem Update betroffen löschen oder insert-Anweisung. Batches, in der beschriebenen [Batches von SQL-Anweisungen](../../../odbc/reference/develop-app/batches-of-sql-statements.md), mehrere Ergebnisse generieren können.  
  
 Die folgende Tabelle enthält die **SQLGetInfo** Optionen, die eine Anwendung verwendet, um zu bestimmen, ob eine Datenquelle für jeden anderen Batch mehrere Ergebnisse zurückgibt. Insbesondere eine Datenquelle kann eine einzelne Zeilenanzahl für den gesamten Batch von Anweisungen zurückgeben, oder einzelne Zeilenanzahl für jede Anweisung im Batch. Im Fall einer Ergebnis Satz – generieren-Anweisung mit einem Array von Parametern ausgeführt die Datenquelle kann ein einzelnes Resultset für alle Parametersätze zurückgeben oder einzelne Resultsets für jeden Satz von Parametern.  
  
|Batchtyp|Zeilenanzahl|Resultsets|  
|----------------|----------------|-----------------|  
|Explizite batch|SQL_BATCH_ROW_COUNT [a]|--[b] '.|  
|Verfahren|SQL_BATCH_ROW_COUNT [a]|--[b] '.|  
|Arrays von Parametern|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] Zeile Count – Generieren von Anweisungen in einem Batch möglicherweise unterstützt werden, aber die Rückgabe von der Zeilenanzahl wird nicht unterstützt. Die Option SQL_BATCH_SUPPORT in **SQLGetInfo** gibt an, ob Zeile Count – Generieren von Anweisungen in Batches zulässig sind; die SQL_BATCH_ROW_COUNTS-Option gibt an, ob diese Zeilenanzahl für die Anwendung zurückgegeben werden.  
  
 [b] explizite Batches und Prozeduren immer mehrere Resultsets zurückgeben, wenn sie mehrere Ergebnis Satz – Generieren von Anweisungen enthalten.  
  
> [!NOTE]  
>  Die SQL_MULT_RESULT_SETS-Option in ODBC 1.0 eingeführt bietet nur allgemeine Informationen, ob mehrere Resultsets zurückgegeben werden können. Es wird insbesondere auf "Y" festgelegt, falls die Bits SQL_BS_SELECT_EXPLICIT oder SQL_BS_SELECT_PROC für SQL_BATCH_SUPPORT zurückgegeben werden oder wenn SQL_PAS_BATCH für SQL_PARAM_ARRAYS_SELECT zurückgegeben wird.  
  
 Um mehrere Ergebnisse zu verarbeiten, eine Anwendung ruft **SQLMoreResults**. Diese Funktion verwirft das aktuelle Ergebnis und stellt das nächste Ergebnis zur Verfügung. Es gibt SQL_NO_DATA zurück, wenn keine weiteren Ergebnisse verfügbar sind. Nehmen wir beispielsweise an, dass die folgenden Anweisungen als Batch ausgeführt werden:  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 Nachdem diese Anweisungen ausgeführt werden, die Anwendung ruft Zeilen aus dem Resultset erstellt, indem die **wählen** Anweisung. Wenn dies das Abrufen von Zeilen erfolgt ist, ruft er **SQLMoreResults** um die Anzahl der Teile verfügbar zu machen, die repriced wurden. Bei Bedarf **SQLMoreResults** verwirft nicht abgerufene Zeilen und schließt den Cursor. Die Anwendung ruft dann **SQLRowCount** um zu bestimmen, wie viele Teile von repriced wurden die **UPDATE** Anweisung.  
  
 Es ist treiberspezifische gibt an, ob die gesamte Batch-Anweisung ausgeführt wird, bevor Ergebnisse verfügbar sind. In einigen Implementierungen ist dies der Fall. in anderen Fällen Aufrufen **SQLMoreResults** löst die Ausführung die nächste Anweisung im Batch.  
  
 Wenn einer der Anweisungen in einem Batch fehlschlägt, **SQLMoreResults** SQL_ERROR oder SQL_SUCCESS_WITH_INFO zurück. Wenn der Batch abgebrochen wird, wenn Fehler bei der Anweisung oder die fehlerhafte Anweisung die letzte Anweisung im Batch wurde, **SQLMoreResults** SQL_ERROR zurück. Wenn der Batch nicht abgebrochen wird, wenn Fehler bei der Anweisung und die fehlgeschlagene Anweisung nicht die letzte Anweisung im Batch war **SQLMoreResults** wird SQL_SUCCESS_WITH_INFO zurückgegeben. SQL_SUCCESS_WITH_INFO gibt an, dass mindestens ein Resultset oder Count generiert wurde und der Batch nicht abgebrochen wurde.
