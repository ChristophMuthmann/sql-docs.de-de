---
title: Diagnose | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f51d8e70d4f9bc4e855079c61ed431931bdb8da
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
