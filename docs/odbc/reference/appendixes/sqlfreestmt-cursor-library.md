---
title: SQLFreeStmt (Cursorbibliothek) | Microsoft Docs
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
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8b7eea7d0a956543ba765dc7c15cf48102efa9e4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLFreeStmt** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLFreeStmt**, finden Sie unter [SQLFreeStmt-Funktion](../../../odbc/reference/syntax/sqlfreestmt-function.md).  
  
 Wenn eine Anwendung ruft **SQLFreeStmt** mit der Option SQL_UNBIND nach dem Aufruf **SQLExtendedFetch**, **SQLFetch**, oder **SQLFetchScroll**, die Cursorbibliothek gibt einen Fehler zurück. Bevor sie die Resultset-Spalten aufheben kann, muss eine Anwendung aufrufen **SQLCloseCursor** oder **SQLFreeStmt** mit der Option SQL_CLOSE.
