---
title: "Schritt 3: Erstellen und Ausführen einer SQL­Anweisung | Microsoft Docs"
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
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4f213203e7601c79f8f5336756462d6ad344aaa8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Schritt 3: Erstellen und Ausführen einer SQL­Anweisung
Der dritte Schritt ist zum Erstellen und Ausführen einer SQL-Anweisung, wie in der folgenden Abbildung dargestellt. Methoden zum Ausführen dieses Schritts werden wahrscheinlich erheblich variieren. Die Anwendung kann der Benutzer aufgefordert, geben eine SQL-Anweisung ein, und erstellen eine SQL-Anweisung basierend auf Benutzereingaben oder eine hartcodierten SQL-Anweisung verwenden. Weitere Informationen finden Sie unter [SQL-Anweisungen konstruieren](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Erstellen und Ausführen einer SQL­Anweisung zeigt](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 Wenn die SQL-Anweisung Parameter enthält, die Anwendung bindet diese an Anwendungsvariablen durch Aufrufen von **SQLBindParameter** für jeden Parameter. Weitere Informationen finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Nachdem die SQL-Anweisung basiert, und alle Parameter gebunden sind, wird die Anweisung ausgeführt, mit **SQLExecDirect**. Wenn die Anweisung mehrmals ausgeführt wird, können sie mit vorbereiteten **SQLPrepare** und mit ausgeführten **SQLExecute**. Weitere Informationen finden Sie unter [Ausführen einer Anweisung](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 Die Anwendung möglicherweise auch die Ausführung einer SQL-Anweisung komplett verzichten und rufen Sie stattdessen eine Funktion, um ein Resultset mit Kataloginformationen, z. B. die verfügbaren Spalten oder Tabellen zurück. Weitere Informationen finden Sie unter [der Katalogdaten verwendet](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Die Anwendung weiter Aktion hängt vom Typ der SQL-Anweisung ausgeführt wird.  
  
|Typ des SQL-Anweisung|Fahren Sie mit|  
|---------------------------|----------------|  
|**Wählen Sie** oder das Katalog-Funktion|[Schritt 4a: Abrufen der Ergebnisse](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**UPDATE**, **löschen**, oder **einfügen**|[Schritt 4b: Abrufen der Anzahl der Zeilen](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Alle anderen SQL-Anweisungen|Schritt 3: Erstellen und Ausführen einer SQL-Anweisung (dieses Thema) oder [Schritt 5: Commit die Transaktion](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
