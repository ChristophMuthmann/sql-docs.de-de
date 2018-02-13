---
title: SQLSetScrollOptions Zuordnung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 57d4bb7747803f1fe65276ddb86c574763627906
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions-Zuordnung
Wenn eine Anwendung ruft **SQLSetScrollOptions** über einen ODBC 3.*.x* und den Treiber nicht unterstützt **SQLSetScrollOptions**, den Aufruf von  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 führt wie folgt:  
  
-   Ein Aufruf von  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     mit der *Infotyp* Argument festgelegt wird, um einen der Werte in der folgenden Tabelle, abhängig vom Wert der *KeysetSize* Argument in **SQLSetScrollOptions**.  
  
    |*KeysetSize-argument*|*Infotyp-argument*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |Ein Wert größer als die *RowsetSize* Argument|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     Wenn der Wert des der *KeysetSize* Argument ist nicht aufgeführt, in der obigen Tabelle, die den Aufruf von **SQLSetScrollOptions** SQLSTATE S1107 zurückgibt (Zeilenwert außerhalb des gültigen Bereichs) und keines der folgenden Schritte aus ausgeführt.  
  
     Der Treiber-Manager überprüft dann, ob das entsprechende Bit, in festgelegt ist der **InfoValuePtr* vom Aufruf zurückgegebene Wert **SQLGetInfo**, entsprechend dem Wert, der die *Parallelität* Argument in **SQLSetScrollOptions**.  
  
    |*Parallelität* Argument|*Infotyp* Einstellung|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     Wenn die *Parallelität* Argument ist keiner der Werte in der obigen Tabelle, die den Aufruf von **SQLSetScrollOptions** SQLSTATE S1108 zurückgibt (Parallelitätsoption außerhalb des gültigen Bereichs) und keines der folgenden Schritte aus ausgeführt. Wenn das entsprechende Bit (wie in der obigen Tabelle angegeben) nicht, in festgelegt ist **InfoValuePtr* auf einen der Werte für die *Parallelität* Argument, das den Aufruf von  **SQLSetScrollOptions** SQLSTATE S1C00 zurückgibt (Treiber nicht unterstützt) und keines der folgenden Schritte ausgeführt werden.  
  
-   Ein Aufruf von  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     mit  *\*ValuePtr* legen Sie auf einen der Werte in der folgenden Tabelle, entsprechend dem Wert, der die *KeysetSize* Argument in **SQLSetScrollOptions**.  
  
    |*KeysetSize* Argument|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |Ein Wert größer als die *RowsetSize* Argument|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   Ein Aufruf von  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     mit  *\*ValuePtr* legen Sie auf der *Parallelität* Argument in **SQLSetScrollOptions**.  
  
-   Wenn die *KeysetSize* Argument im Aufruf **SQLSetScrollOptions** positiv ist, einen Aufruf von  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     mit  *\*ValuePtr* legen Sie auf der *KeysetSize* Argument in **SQLSetScrollOptions**.  
  
-   Ein Aufruf von  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     mit  *\*ValuePtr* legen Sie auf der *RowsetSize* Argument in **SQLSetScrollOptions**.  
  
    > [!NOTE]  
    >  Wenn der Treiber-Manager ordnet **SQLSetScrollOptions** für eine Anwendung mit dem Arbeiten mit einer ODBC 3.*.x* Treiber, der nicht unterstützt **SQLSetScrollOptions**, den Treiber -Manager setzt die SQL_ROWSET_SIZE setzen-Anweisungsoption nicht das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut, zu der *RowsetSize* Argument in **SQLSetScrollOption**. Folglich **SQLSetScrollOptions** kann nicht von einer Anwendung verwendet werden, wenn mehrere Zeilen durch einen Aufruf zum Abrufen von **SQLFetch** oder **SQLFetchScroll**. Kann verwendet werden, nur dann, wenn durch einen Aufruf an das Abrufen mehrerer Zeilen **SQLExtendedFetch**.
