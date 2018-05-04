---
title: SQLSetScrollOptions (Cursorbibliothek) | Microsoft Docs
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
- SQLSetScrollOptions function [ODBC], Cursor Library
ms.assetid: c5c0ac6d-a6c1-4077-8186-1644df1944f8
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 96041fdfcf9dbad53513f402faad8b2aeaf37cf3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLSetScrollOptions** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLSetScrollOptions**, finden Sie unter [SQLSetScrollOptions Funktion](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md).  
  
 Unterstützt die Cursorbibliothek **SQLSetScrollOptions** nur für Abwärtskompatibilität; Anwendungen sollten stattdessen die SQL_ATTR_CURSOR_TYPE, SQL_ATTR_CONCURRENCY und SQL_ATTR_ROW_ARRAY_SIZE Anweisungsattribute.
