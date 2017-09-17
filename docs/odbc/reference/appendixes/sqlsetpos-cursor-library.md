---
title: SQLSetPos (Cursorbibliothek) | Microsoft Docs
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
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b195ca1dbb138b21fcf107150832288df8317196
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLSetPos** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLSetPos**, finden Sie unter [SQLSetPos-Funktion](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 Die Cursorbibliothek unterstützt den SQL_POSITION Vorgang nur für die *Vorgang* Argument in **SQLSetPos**. Es unterstützt die SQL_LOCK_NO_CHANGE Wert nur für die *LockType* Argument.  
  
 Wenn der Treiber Massenvorgänge nicht unterstützt, gibt die Cursorbibliothek SQLSTATE HYC00 (Treiber nicht unterstützt) beim **SQLSetPos** aufgerufen wird und *RowNumber* gleich 0. Dieses Verhalten wird nicht empfohlen.  
  
 Die Cursorbibliothek unterstützt nicht die SQL_UPDATE und SQL_DELETE Vorgänge in einem Aufruf von **SQLSetPos**. Der Cursor-Bibliothek implementiert eine positionierte aktualisieren oder löschen die SQL-Anweisung durch das Erstellen einer durchsuchten aktualisieren oder delete-Anweisung mit einer WHERE-Klausel, die in seinem Cache für jede gebundene Spalte gespeicherten Werte auflistet. Weitere Informationen finden Sie unter [Verarbeitung positioniert Update und Delete-Anweisungen](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md).  
  
 Eine Anwendung mit der Cursorbibliothek arbeiten sollten aufrufen, wenn der Treiber statische Cursor werden nicht unterstützt, **SQLSetPos** nur für ein Rowset, das vom abgerufen **SQLExtendedFetch** oder **SQLFetchScroll **, nicht von **SQLFetch**. Die Cursorbibliothek implementiert **SQLExtendedFetch** und **SQLFetchScroll** durch wiederholte Aufrufe von **SQLFetch** (mit einer Rowsetgröße von 1) im Treiber. Die Cursorbibliothek übergibt Aufrufe **SQLFetch**, auf die andere hingegen über den Treiber. Wenn **SQLSetPos** wird aufgerufen, in einem mehrzeiligen Rowset abgerufen, indem **SQLFetch** Wenn statische Cursor mit der Treiber nicht unterstützt wird, schlägt der Aufruf fehl, da **SQLSetPos** funktioniert nicht mit Vorwärtscursor. Dies geschieht auch, wenn eine Anwendung wurde erfolgreich aufgerufen wurde **SQLSetStmtAttr** für SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC, festzulegen, die die Cursorbibliothek unterstützt, auch wenn der Treiber statische Cursor werden nicht unterstützt.
