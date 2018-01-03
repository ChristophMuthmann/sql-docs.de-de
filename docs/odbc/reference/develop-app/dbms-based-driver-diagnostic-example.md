---
title: DBMS-basierten Treiber diagnostische Beispiel | Microsoft Docs
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
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 84fa35f438b3dc852d2b8b7ae043e5c1f6402ec5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="dbms-based-driver-diagnostic-example"></a>DBMS-basierten Treiber Diagnostic-Beispiel
Ein DBMS-basierten Treiber sendet Anforderungen an ein DBMS und Informationen in der Anwendung über den Treiber-Manager zurück. Da der Treiber die Komponente, das mit der Treiber-Manager kommuniziert ist, formatiert und gibt die Argumente für **SQLGetDiagRec**.  
  
 Z. B. Wenn Sie SQL/Diensttypen, eine Microsoft-Treiber verwenden, für die Oracle-Rdb einen Ungültiger Cursorname gefunden, es möglicherweise die folgenden Werte zurückgeben von **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 Aufgrund des Fehlers im Treiber hinzugefügt Präfixe, die diagnosemeldung für den Anbieter (Microsoft) und der Treiber ([ODBC-Treiber Rdb]).  
  
 Wenn das DBMS die EMPLOYEE-Tabelle nicht finden konnte, der Treiber formatieren und die folgenden Rückgabewerte von möglicherweise **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 Aufgrund des Fehlers in der Datenquelle, mit der Treiber die diagnosemeldung ein Präfix für den datenquellenbezeichner ([Rdb]) hinzugefügt. Wurde der Treiber die Komponente, die mit der Datenquelle verbunden, werden die diagnosemeldung Präfixe für die Anbieter (Microsoft) und den Bezeichner ([ODBC-Treiber Rdb]) hinzugefügt.
