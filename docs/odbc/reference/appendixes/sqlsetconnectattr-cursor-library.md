---
title: SQLSetConnectAttr (Cursorbibliothek) | Microsoft Docs
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
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bf6a14b8215f981e5e0e9c0ca6e9b2e1a2269f65
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLSetConnectAttr** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLSetConnectAttr**, finden Sie unter [Funktion SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Ruft die Anwendung **SQLSetConnectAttr** mit dem SQL_ATTR_ODBC_CURSORS-Attribut, um anzugeben, ob die Cursorbibliothek immer verwendet wird, verwendet wird, wenn der Treiber bildlauffähige Cursor nicht unterstützt oder nie verwendet. Die Cursorbibliothek wird davon ausgegangen, dass ein Treiber bildlauffähige Cursor unterstützt, wenn es für den Typ der SQL_STATIC_CURSOR_ATTRIBUTES1-Informationen in den SQL_CA1_RELATIVE zurückgibt **SQLGetInfo**.  
  
 Muss die Anwendung aufrufen **SQLSetConnectAttr** die Cursorverwendung für die Bibliothek an, nach dem Aufruf **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_DBC auf, um zuordnen die Verbindung, bevor er sich mit der Datenquelle verbindet. Wenn eine Anwendung ruft **SQLSetConnectAttr** mit Attributs SQL_ATTR_ODBC_CURSORS während die Verbindung weiterhin aktiv ist, ist die Cursorbibliothek gibt einen Fehler zurück.  
  
 Um eine von der Cursorbibliothek für alle Anweisungen, die eine Verbindung zugeordneten unterstützt Anweisungsattribut festzulegen, muss eine Anwendung aufrufen **SQLSetConnectAttr** für dieses Anweisungsattribut, nachdem er mit der Datenquelle und bevor sie eine Verbindung herstellt Öffnet den Cursor. Wenn eine Anwendung ruft **SQLSetConnectAttr** mit einer Anweisung Attribut und ein Cursor geöffnet, in einer Anweisung, die der Verbindung zugeordnet ist, das Anweisungsattribut wird nicht für die Anweisung angewendet werden, bis der Cursor geschlossen wird und erneut geöffnet.
