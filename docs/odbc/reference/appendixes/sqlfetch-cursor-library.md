---
title: SQLFetch (Cursorbibliothek) | Microsoft Docs
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
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d0ba4112900a3d89e74582e3bf3549b196ba2ab
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLFetch** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLFetch**, finden Sie unter [SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Wenn die Cursorbibliothek verwendet wird, Aufrufe von **SQLFetch** kann nicht kombiniert werden, mit der Aufrufe von **SQLFetchScroll** oder **SQLExtendedFetch**.  
  
 Wenn **SQLFetch** heißt mit SQL_ATTR_ROW_ARRAY_SIZE auf einen Wert größer als 1 festgelegt, wird die Cursorbibliothek den Aufruf an den Treiber übergeben. Wenn der Treiber eine ODBC-2 ist. *x* -Treiber die Rowsetgröße wird ignoriert und der Aufruf von **SQLFetch** wird eine einzelne Zeile mit Daten zurückgegeben.  
  
 Wenn die Cursorbibliothek mit einer ODBC 2. verwendet wird. *x* -Treiber verwenden, eine Bindung mit dem offset (gemäß der SQL_ATTR_ROW_BIND_OFFSET_PTR-Anweisungsattribut) wird nicht verwendet, wenn **SQLFetch** aufgerufen wird.  
  
 Eine Anwendung kann nicht aufgerufen, wenn die Cursorbibliothek geladen ist, **SQLFetch** Lesezeichenspalten abgerufen. Die Cursorbibliothek übergibt den Aufruf von **SQLFetch** über den Treiber, aber die Funktion aufruft, zum Aktivieren von Lesezeichen und binden die Lesezeichenspalte abgefangen werden durch die Cursorbibliothek.
