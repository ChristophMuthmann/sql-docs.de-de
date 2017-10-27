---
title: SQLSetConnectOption Zuordnung | Microsoft Docs
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
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e531888390bbe4f625d308ad983059634e84ba2b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption-Zuordnung
Wenn eine ODBC-2. *x* Anwendung ruft **SQLSetConnectOption** über einen ODBC 3.*.x* Treiber, den Aufruf von  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 führt wie folgt:  
  
-   Wenn *fOption* gibt ein ODBC-definierten Verbindungsattribut, das eine Zeichenfolge, die Aufrufe der Treiber-Manager erfordert  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   Wenn *fOption* gibt ein ODBC-definierten Verbindungsattribut, das einen 32-Bit-Ganzzahl-Wert, der Treiber-Manager ruft zurückgibt  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   Wenn *fOption* gibt ein treiberdefinierten Verbindungsattribut Treibermanager-Aufrufe an  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 In den vorhergehenden drei Fällen die *Verbindungshandle* Argument wird festgelegt, auf den Wert in *Hdbc*, *Attribut* Argument wird festgelegt, auf den Wert in *fOption *, und die *ValuePtr* Argument wird festgelegt, auf den gleichen Wert wie *vParam*.  
  
 Da der Treiber-Manager nicht weiß, ob das treiberdefinierten Verbindungsattribut 32-Bit-Ganzzahl-Wert oder eine Zeichenfolge erforderlich, wurde für die Übergabe in einen gültigen Wert für die *Pufferlänge* Argument **SQLSetConnectAttr**. Wenn spezielle Semantik für den treiberdefinierten treiberdefinierten verbinden, Attribute und muss aufgerufen werden. **SQLSetConnectOption**, muss er unterstützen **SQLSetConnectOption**.  
  
 Wenn ein ODBC-2. *x* Anwendung ruft **SQLSetConnectOption** festzulegende treiberspezifische-Anweisungsoption in eine ODBC 3.*.x* Treiber und die Option wurde in einer ODBC 2. definiert.* X* Version des Treibers, eine neue manifestkonstante sollte definiert werden, für die Option in die ODBC 3.*.x* Treiber. Wenn die alten manifestkonstante, in dem Aufruf von verwendet wird **SQLSetConnectOption**, Treiber-Manager **SQLSetConnectAttr** mit der **StringLength** Argument auf 0 festgelegt.  
  
 Für eine ODBC 3.*.x* Treiber, der Treiber-Manager nicht mehr überprüft, ob *fOption* zwischen SQL_CONN_OPT_MIN und SQL_CONN_OPT_MAX ist, oder SQL_CONNECT_OPT_DRVR_START größer ist.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>Festlegen von Optionen auf der Verbindungsebene-Anweisung  
 In ODBC 2. *x*, könnte eine Anwendung aufrufen **SQLSetConnectOption** eine Option-Anweisung festgelegt. Wenn Sie fertig sind, richtet der Treiber die Option-Anweisung als Standard für alle Anweisungen, die für diese Verbindung später zugeordnet. Es ist treiberdefinierten, ob der Treiber mit die Option-Anweisung für alle vorhandenen Anweisungen, die der angegebenen Verbindung zugeordneten setzt.  
  
 Diese Funktion ist veraltet, in ODBC 3.*.x*. ODBC 3.*.x* Treiber müssen nur unterstützt das Festlegen von ODBC 2..* X* Anweisungsattribute auf Verbindungsebene, die mit ODBC 2. arbeiten sollen.* X* Anwendungen, die dazu. ODBC 3.*.x* Anwendungen Anweisungsattribute auf Verbindungsebene darf nicht festgelegt werden. ODBC 3.*.x* Anweisungsattribute können nicht auf Verbindungsebene, mit Ausnahme der SQL_ATTR_METADATA_ID und SQL_ATTR_ASYNC_ENABLE-Attribute, die Verbindungsattribute und Anweisungsattribute sind, und kann nicht festgelegt werden Legen Sie auf der Verbindungsebene oder Anweisungsebene.

