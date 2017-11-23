---
title: SQLFreeStmt (Cursorbibliothek) | Microsoft Docs
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
helpviewer_keywords: SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 19bae8656d81406116b17847654e21c5ab5c2ca7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLFreeStmt** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLFreeStmt**, finden Sie unter [SQLFreeStmt-Funktion](../../../odbc/reference/syntax/sqlfreestmt-function.md).  
  
 Wenn eine Anwendung ruft **SQLFreeStmt** mit der Option SQL_UNBIND nach dem Aufruf **SQLExtendedFetch**, **SQLFetch**, oder **SQLFetchScroll**, die Cursorbibliothek gibt einen Fehler zurück. Bevor sie die Resultset-Spalten aufheben kann, muss eine Anwendung aufrufen **SQLCloseCursor** oder **SQLFreeStmt** mit der Option SQL_CLOSE.
