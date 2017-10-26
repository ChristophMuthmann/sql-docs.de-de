---
title: Zuordnen eines Anweisungshandles ODBC | Microsoft Docs
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
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a96868755475c6fd72b2dd977375fbe0d88c22df
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="allocating-a-statement-handle-odbc"></a>Zuordnen eines Anweisungshandles ODBC
Bevor die Anwendung eine Anweisung ausgeführt werden kann, muss sie wie folgt ein Anweisungshandle zuordnen:  
  
1.  Die Anwendung deklariert eine Variable vom Typ Befehls beschäftigt. Er ruft dann **SQLAllocHandle** und übergibt die Adresse dieser Variablen wird das Handle für die Verbindung in der die Anweisung und die Option SQL_HANDLE_STMT zuordnen. Beispiel:  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  Der Treiber-Manager weist eine Struktur zum Speichern von Informationen über die Anweisung und die Aufrufe **SQLAllocHandle** im Treiber mit der Option SQL_HANDLE_STMT auf.  
  
3.  Der Treiber ordnet ihre eigene Struktur zum Speichern von Informationen über die Anweisung und gibt das Anweisungshandle Treiber an den Treiber-Manager.  
  
4.  Der Treiber-Manager gibt das Anweisungshandle-Treiber-Manager für die Anwendung in der Anwendungsvariablen zurück.  
  
 Das Anweisungshandle identifiziert, welche Anweisung beim Aufrufen von ODBC-Funktionen verwenden. Weitere Informationen zu Anweisungshandles, finden Sie unter [Anweisungshandles](../../../odbc/reference/develop-app/statement-handles.md).

