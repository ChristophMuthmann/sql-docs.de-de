---
title: Zuordnen eines Anweisungshandles ODBC | Microsoft Docs
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
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d0f2bd2da071bb690443df9d5c0bdebb5a5e1e6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
