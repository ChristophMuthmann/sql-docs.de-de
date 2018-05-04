---
title: SQLGetConnectOption Zuordnung | Microsoft Docs
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
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ec36a536732299337efde3cf58cc98fbf4c46e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
  
 In den vorhergehenden drei Fällen die *Verbindungshandle* Argument wird festgelegt, auf den Wert in *Hdbc*, *Attribut* Argument wird festgelegt, auf den Wert in *fOption* , und die *ValuePtr* Argument wird festgelegt, auf den gleichen Wert wie *PvParam*.  
  
 Für ODBC definierte Zeichenfolge Verbindungsoptionen, legt der Treiber-Manager die *Pufferlänge* Argument im Aufruf **SQLGetConnectAttr** auf die vordefinierte maximale Länge (SQL_MAX_OPTION_STRING_LENGTH); für eine Verbindungsoption Objektressourcen *Pufferlänge* auf 0 festgelegt ist.  
  
 Für eine ODBC 3.*.x* Treiber, der Treiber-Manager nicht mehr überprüft, ob *Option* zwischen SQL_CONN_OPT_MIN und SQL_CONN_OPT_MAX ist, oder SQL_CONNECT_OPT_DRVR_START größer ist. Der Treiber muss es sich um die Gültigkeit der Optionswerte überprüfen.
