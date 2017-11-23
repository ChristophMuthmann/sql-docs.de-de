---
title: Bookmark-C-Datentyp | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 698e450fbb816c5fb7e3caf3786f4b8d469af50c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="bookmark-c-data-type"></a>Bookmark-C-Datentyp
Das Lesezeichen C-Datentyp kann eine Anwendung ein Lesezeichen abrufen. Die Lesezeichen C-Typen werden verwendet, nur für Lesezeichenwerte abrufen, die variabler Länge werden können; Sie sollten nicht in andere Datentypen konvertiert werden. Eine Anwendung ruft ein Lesezeichen, das Festlegen von Spalte 0 des Ergebnisses mit **SQLBulkOperations** (mit einem Vorgang des SQL_ADD), **SQLFetch**, **SQLFetchScroll**, oder **SQLGetData**. Weitere Informationen finden Sie unter [Lesezeichen](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
 Die folgende Tabelle enthält den Wert der *CType* für die Lesezeichen C-Datentyp, der ODBC-C-Datentyp, der das Lesezeichen C-Datentyp und die Definition dieser Daten implementiert, geben Sie von SQL. H.  
  
> [!NOTE]  
>  Der Datentyp SQL_C_BOOKMARK wurde als veraltet markiert. ODBC 3.*.x* Anwendungen sollten keine SQL_C_BOOKMARK verwenden. ODBC 3.*.x* Treiber müssen SQL_C_BOOKMARK unterstützen nur, wenn sie mit ODBC 2. arbeiten möchten. *X* Anwendungen, die sie verwenden. Der Treiber-Manager SQL_C_BOOKMARK SQL_C_VARBOOKMARK zugeordnet, wenn eine Anwendung mit einer ODBC 2. arbeitet. *x* Treiber.  
  
|C-Typ-ID|ODBC C-Typdefinition|C-Typ|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(Veraltet)|LESEZEICHEN|unsigned long int|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned Char *|
