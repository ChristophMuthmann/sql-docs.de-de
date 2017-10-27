---
title: "Diagnose für Desktop Datenbank Treiber | Microsoft Docs"
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
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 432d311b1f55ff636e8c0b6fedb28509e3d9e6ed
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnose für Desktop-Datenbanktreiber
Alle Fehler und Warnungen nicht oder teilweise ausgecheckt vom Treiber-Manager werden vom Treiber gehandhabt. Der Treiber ordnet auch systemeigene Fehler oder Fehler, die von der Datenquelle an SQLSTATEs zurückgegeben. Jede Funktion aufgeführt, die der *ODBC Programmer's Reference* enthält einen Diagnoseabschnitt "", der angibt, Bedingungen und Nachrichten.  
  
 -Anwendungen rufen **SQLGetDiagRec** SQLSTATE, systemeigener Fehlercode und diagnosemeldungen abgerufen. Aufrufen von **SQLGetDiagField** und Angeben des Felds, einzelne Diagnosefelder abruft. Das Maß an Unterstützung für die Diagnose Bezeichner wird in der folgenden Tabelle aufgeführt.  
  
|DiagIdentifiers|Supportebene|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|Nicht unterstützt|  
|SQL_DIAG_CLASS_ORIGIN|Unterstützt. Immer "ODBC 3.0" für die Versionen 3.0 und späteren Versionen von diesem Treiber.|  
|SQL_DIAG_COLUMN_NUMBER|Unterstützt|  
|SQL_DIAG_CURSOR_ROW_COUNT|Nicht unterstützt|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|Nicht unterstützt|  
|SQL_DIAG_MESSAGE_TEXT|Unterstützt|  
|SQL_DIAG_NATIVE|Unterstützt|  
|SQL_DIAG_NUMBER|Unterstützt|  
|SQL_DIAG_RETURNCODE|Unterstützt, aber vom Treiber-Manager implementiert|  
|SQL_DIAG_ROW_COUNT|Unterstützt|  
|SQL_DIAG_ROW_NUMBER|Unterstützt|  
|SQL_DIAG_SERVER_NAME|Nicht unterstützt|  
|SQL_DIAG_SQLSTATE|Unterstützt|  
|SQL_DIAG_SUBCLASS_ORIGIN|Unterstützt|

