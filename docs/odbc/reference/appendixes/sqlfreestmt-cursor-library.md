---
title: SQLFreeStmt (Cursorbibliothek) | Microsoft Docs
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
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b648c069c3930e923db8a929f7203807c67b128e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLFreeStmt** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLFreeStmt**, finden Sie unter [SQLFreeStmt-Funktion](../../../odbc/reference/syntax/sqlfreestmt-function.md).  
  
 Wenn eine Anwendung ruft **SQLFreeStmt** mit der Option SQL_UNBIND nach dem Aufruf **SQLExtendedFetch**, **SQLFetch**, oder **SQLFetchScroll**, die Cursorbibliothek gibt einen Fehler zurück. Bevor sie die Resultset-Spalten aufheben kann, muss eine Anwendung aufrufen **SQLCloseCursor** oder **SQLFreeStmt** mit der Option SQL_CLOSE.
