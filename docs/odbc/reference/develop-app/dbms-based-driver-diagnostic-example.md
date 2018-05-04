---
title: DBMS-basierten Treiber diagnostische Beispiel | Microsoft Docs
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
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e688fff2771a14d85a659ae7c69d6a515ce88f8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
