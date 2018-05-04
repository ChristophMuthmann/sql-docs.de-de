---
title: SQLBindCol (Cursorbibliothek) | Microsoft Docs
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
- SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a877b6cade18e59f12abfe807d8efa04363b3dcb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLBindCol** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLBindCol**, finden Sie unter [SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
 Eine Anwendung reserviert eine oder mehrere Puffer für die Cursorbibliothek zum Zurückgeben des aktuellen Rowsets in. Sie ruft **SQLBindCol** ein- oder mehrmals, um diese Puffer auf das Resultset zu binden.  
  
 Eine Anwendung kann Aufrufen **SQLBindCol** Ergebnis erneut binden Resultsetspalten nach aufgerufen wurde **SQLExtendedFetch**, **SQLFetch**, oder **SQLFetchScroll**, solange die C-Datentyp, die Spaltengröße und die Dezimalstellen der gebundenen Spalte unverändert bleiben. Die Anwendung muss nicht den Cursor zum Binden von Spalten mit verschiedenen Adressen zu schließen.  
  
 Die Cursorbibliothek unterstützt das Festlegen von SQL_ATTR_ROW_BIND_OFFSET_PTR-Anweisungsattribut Bind-Offsets zu verwenden. (**SQLBindCol** muss nicht für diese erneute Bindung erfolgen aufgerufen werden.) Wenn die Cursorbibliothek, mit einer ODBC 3. verwendet wird *.x* Treiber, der Bind-Offset ist nicht verwendet werden, wenn **SQLFetch** aufgerufen wird. Der Offset für die Bindung wird verwendet, wenn **SQLFetch** wird aufgerufen, wenn die Cursorbibliothek, mit einer ODBC 2. verwendet wird. *X* Treiber da **SQLFetch** dann zugeordnet wird **SQLExtendedFetch**.  
  
 Die Cursorbibliothek unterstützt Aufrufen **SQLBindCol** die Lesezeichenspalte binden.  
  
 Wenn Sie mit einer ODBC 2. arbeiten zu können. *x* -Treiber verwenden, gibt die Cursorbibliothek SQLSTATE HY090 zurück (ungültige Zeichenfolgen- oder Pufferlänge.) Wenn **SQLBindCol** wird aufgerufen, um die Pufferlänge für eine Lesezeichenspalte auf einen Wert festgelegt wird, der nicht gleich 4. Bei der Arbeit mit einer ODBC 3.*.x* -Treiber die Cursorbibliothek ermöglicht den Puffer, in beliebiger Größe sein.
