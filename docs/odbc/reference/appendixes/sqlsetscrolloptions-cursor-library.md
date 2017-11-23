---
title: SQLSetScrollOptions (Cursorbibliothek) | Microsoft Docs
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
helpviewer_keywords: SQLSetScrollOptions function [ODBC], Cursor Library
ms.assetid: c5c0ac6d-a6c1-4077-8186-1644df1944f8
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f97c24e12dd7a5ea0108eb791cb03a2c405bd205
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLSetScrollOptions** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLSetScrollOptions**, finden Sie unter [SQLSetScrollOptions Funktion](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md).  
  
 Unterstützt die Cursorbibliothek **SQLSetScrollOptions** nur für Abwärtskompatibilität; Anwendungen sollten stattdessen die SQL_ATTR_CURSOR_TYPE, SQL_ATTR_CONCURRENCY und SQL_ATTR_ROW_ARRAY_SIZE Anweisungsattribute.
