---
title: SQLCloseCursor_ODBC | Microsoft Docs
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
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fcc680ec815afa700c00c9d8a69c5826944153a4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlclosecursorodbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLCloseCursor** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLCloseCursor**, finden Sie unter [SQLCloseCursor-Funktion](../../../odbc/reference/syntax/sqlclosecursor-function.md).  
  
 Die Cursorbibliothek unterstützt keine Aufrufen **SQLCloseCursor** ohne einem geöffneten Cursor. Versuchen Dies wird SQLSTATE 24000 (Ungültiger Cursorstatus) zurückgegeben. Aufrufen von **SQLFreeStmt** mit einem *Option* von SQL_CLOSE, wenn keine Cursor geöffnet ist, wird von der Cursorbibliothek unterstützt.

