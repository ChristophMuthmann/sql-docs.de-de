---
title: SQLGetConnectOption Zuordnung | Microsoft Docs
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
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a1be0f632b702083f279723b74f4474c2231bb8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetconnectoption-mapping"></a>SQLGetConnectOption-Zuordnung
Wenn eine Anwendung ruft **SQLGetConnectOption** über einen ODBC 3.*.x* Treiber, den Aufruf von  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 wird wie folgt zugeordnet:  
  
-   Wenn *fOption* gibt an, eine ODBC-definierten Verbindungsoption, die eine Zeichenfolge, die der Treiber-Manager ruft zurückgibt  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Wenn *fOption* gibt an, eine ODBC-definierten Verbindungsoption, die einen ganzzahligen 32-Bit-Wert, der Treiber-Manager ruft zurückgibt.  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Wenn *fOption* gibt eine treiberdefinierten Anweisungsoption Treibermanager-Aufrufe an  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 In den vorhergehenden drei Fällen die *Verbindungshandle* Argument wird festgelegt, auf den Wert in *Hdbc*, *Attribut* Argument wird festgelegt, auf den Wert in *fOption *, und die *ValuePtr* Argument wird festgelegt, auf den gleichen Wert wie *PvParam*.  
  
 Für ODBC definierte Zeichenfolge Verbindungsoptionen, legt der Treiber-Manager die *Pufferlänge* Argument im Aufruf **SQLGetConnectAttr** auf die vordefinierte maximale Länge (SQL_MAX_OPTION_STRING_LENGTH); für eine Verbindungsoption Objektressourcen *Pufferlänge* auf 0 festgelegt ist.  
  
 Für eine ODBC 3.*.x* Treiber, der Treiber-Manager nicht mehr überprüft, ob *Option* zwischen SQL_CONN_OPT_MIN und SQL_CONN_OPT_MAX ist, oder SQL_CONNECT_OPT_DRVR_START größer ist. Der Treiber muss es sich um die Gültigkeit der Optionswerte überprüfen.

