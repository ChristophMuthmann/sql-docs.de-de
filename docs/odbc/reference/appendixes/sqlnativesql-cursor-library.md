---
title: SQLNativeSql (Cursorbibliothek) | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f9ce0357981dbc7a499bf0dc0cefc52313a2596a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLNativeSql** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLNativeSql**, finden Sie unter [SQLNativeSql-Funktion](../../../odbc/reference/syntax/sqlnativesql-function.md).  
  
 Wenn der Treiber diese Funktion unterstützt wird, ruft die Cursorbibliothek **SQLNativeSql** im Treiber und übergibt sie die SQL-Anweisung. Positioniertes Update positioniert "Delete" und **für aktualisieren wählen** -Anweisungen, die Cursorbibliothek ändert die Anweisung vor der Übergabe an den Treiber.  
  
> [!NOTE]  
>  Die Cursorbibliothek gibt fälschlicherweise SQLSTATE 34000 (Ungültiger Cursorname) zurück, wenn der Name des Cursors ist ungültig in eine positionierte Update- oder Delete-Anweisung, die übergeben wird die *InStatementText* Argument **SQLNativeSql** . **SQLNativeSql** nicht Syntaxfehler, zurückgeben, die erst nach der Vorbereitung der Anweisung oder der Ausführung zurückgegeben werden soll.
