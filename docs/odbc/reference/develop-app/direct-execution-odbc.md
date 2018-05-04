---
title: Direkte Ausführung ODBC | Microsoft Docs
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
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e506f856fff84065b0026e3e3629a4299d14dae2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="direct-execution-odbc"></a>Direkte Ausführung ODBC
Direkte Ausführung ist die einfachste Möglichkeit zum Ausführen einer Anweisung. Wenn die Anweisung zur Ausführung übermittelt wird, wird die Datenquelle in eines Plans kompiliert und führt dann diesen Zugriffsplan.  
  
 Direkte Ausführung ist allgemeiner Anwendungen häufig verwendet, das Erstellen und Ausführen von Anweisungen zur Laufzeit. Der folgende Code wird z. B. eine SQL-Anweisung erstellt und führt es ein einziges Mal:  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 Direkte Ausführung funktioniert am besten geeignet für Anweisungen, die ein einziges Mal ausgeführt werden. Die wichtigsten Nachteil besteht darin, dass die SQL-Anweisung analysiert ist, jedes Mal, wenn er ausgeführt wird. Die Anwendung kann keine darüber hinaus Informationen über das Resultset, das von der Anweisung erstellt (sofern vorhanden) erst nach der Ausführung der Anweisung abrufen; Dies ist möglich, wenn die Anweisung vorbereitet und wird, in zwei separate Schritte ausgeführt.  
  
 Zum Ausführen einer Anweisung direkt, führt die Anwendung die folgenden Aktionen:  
  
1.  Legt die Werte aller Parameter an. Weitere Informationen finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md)weiter unten in diesem Abschnitt.  
  
2.  Aufrufe **SQLExecDirect** und übergibt eine Zeichenfolge, die die SQL-Anweisung enthält.  
  
3.  Wenn **SQLExecDirect** aufgerufen wird, wird den Treiber:  
  
    -   Ändert die SQL-Anweisung, um SQL-Grammatik für die Datenquelle zu verwenden, ohne die Anweisung zu analysieren. Dazu gehören, und Ersetzen Sie dabei die Escapesequenzen, die in beschriebenen [in ODBC-Escapesequenzen](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). Die Anwendung kann rufen Sie die geänderte Form einer SQL-Anweisung durch den Aufruf **SQLNativeSql**. Escapesequenzen werden nicht ersetzt, wenn das SQL_ATTR_NOSCAN-Anweisungsattribut festgelegt ist.  
  
    -   Ruft die aktuellen Parameterwerte ab und konvertiert sie nach Bedarf. Weitere Informationen finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md)weiter unten in diesem Abschnitt.  
  
    -   Sendet die Anweisung und die konvertierten Parameterwerte an die Datenquelle für die Ausführung an.  
  
    -   Gibt Fehlermeldungen zurück. Dazu gehören Sequenzierung oder Status-Diagnose z. B. SQLSTATE 24000 (Ungültiger Cursorstatus), syntaktische Fehler wie z. B. SQLSTATE 42000 (Syntaxfehler oder zugriffsverletzung) und semantische Fehler, z. B. SQLSTATE 42S02 (Basis Tabelle oder-Sicht wurde nicht gefunden).
