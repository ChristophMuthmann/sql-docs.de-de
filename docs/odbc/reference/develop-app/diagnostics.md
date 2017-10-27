---
title: Diagnose | Microsoft Docs
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
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: adb6f66ecfbff558fd163437a56453efb4265185
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="diagnostics"></a>Diagnose
Funktionen in ODBC gibt Diagnoseinformationen in zweierlei Art zurück. Gibt der Rückgabecode an den Erfolg oder Fehler bei der Funktion, DiagnoseDatensätze ausführliche Informationen über die Funktion bereitstellen. Mindestens ein Diagnosedatensatz – der Headerdatensatz – wird zurückgegeben, auch wenn die Funktion erfolgreich ausgeführt wird.  
  
 Diagnoseinformationen dient zur Entwicklungszeit zum Abfangen von Programmierfehlern wie ungültigen Handles und Syntaxfehlern in hartcodierten SQL-Anweisungen. Es ist zur Laufzeit verwendet, um Laufzeitfehler und Warnungen, z. B. das Abschneiden von Daten, zugriffsverletzungen und Syntaxfehler in SQL-Anweisungen, die vom Benutzer eingegebenen abzufangen.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Rückgabecodes](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [DiagnoseDatensätze](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [Verwenden von SQLGetDiagRec und SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Implementieren von SQLGetDiagRec und SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Beispiele für die Diagnose Behandlung](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)

