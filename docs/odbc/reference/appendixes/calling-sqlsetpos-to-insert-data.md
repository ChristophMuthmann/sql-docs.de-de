---
title: "Durch Aufrufen von SQLSetPos zum Einfügen von Daten | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e9d768ea5c16b199dc316726cb425b75d409bf1f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="calling-sqlsetpos-to-insert-data"></a>Durch Aufrufen von SQLSetPos zum Einfügen von Daten
Wenn eine ODBC-2. *x* Anwendung arbeiten mit einem ODBC 3.*.x* Treiber ruft **SQLSetPos** mit einem *Vorgang* Argument SQL_ADD der Treiber-Manager Dieser Aufruf ist nicht zugeordnet **SQLBulkOperations**. Wenn eine ODBC 3.*.x* Treiber sollte mit einer Anwendung, die Aufrufe funktionieren **SQLSetPos** mit SQL_ADD, unterstützt der Treiber sollte diesen Vorgang.  
  
 Ein wesentlicher Unterschied im Verhalten beim **SQLSetPos** aufgerufen wird und SQL_ADD tritt auf, wenn sie sich im Zustand a6 aufgerufen wird. In ODBC 2. *x*, der Treiber zurückgegebenen S1010 beim **SQLSetPos** SQL_ADD Status a6 aufgerufen wurde (nach dem mit der Cursor erstellt wurde **SQLFetch**). In ODBC 3.*.x*, **SQLBulkOperations** mit einem *Vorgang* von SQL_ADD kann im Zustand a6 aufgerufen werden. Ein zweite wesentliche Unterschied im Verhalten besteht darin, die **SQLBulkOperations** mit einer *Vorgang* von SQL_ADD kann zwar im Zustand S5 aufgerufen, **SQLSetPos** mit einer  **Vorgang** von SQL_ADD nicht möglich. Für die Anweisung Übergänge, die für den gleichen Aufruf in ODBC 3. auftreten können*.x*, finden Sie unter [Anhang B: ODBC-Übergang-Statustabellen](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).

