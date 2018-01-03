---
title: Diagnose | Microsoft Docs
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
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efbc34be3dc532b329863a98305952d90adcc9f5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="diagnostics"></a>Diagnose
Funktionen in ODBC gibt Diagnoseinformationen in zweierlei Art zurück. Gibt der Rückgabecode an den Erfolg oder Fehler bei der Funktion, DiagnoseDatensätze ausführliche Informationen über die Funktion bereitstellen. Mindestens ein Diagnosedatensatz – der Headerdatensatz – wird zurückgegeben, auch wenn die Funktion erfolgreich ausgeführt wird.  
  
 Diagnoseinformationen dient zur Entwicklungszeit zum Abfangen von Programmierfehlern wie ungültigen Handles und Syntaxfehlern in hartcodierten SQL-Anweisungen. Es ist zur Laufzeit verwendet, um Laufzeitfehler und Warnungen, z. B. das Abschneiden von Daten, zugriffsverletzungen und Syntaxfehler in SQL-Anweisungen, die vom Benutzer eingegebenen abzufangen.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Rückgabecodes](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [Diagnosedatensätze](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [Verwenden von SQLGetDiagRec und SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Implementieren von SQLGetDiagRec und SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Beispiele für die Diagnosebehandlung](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
