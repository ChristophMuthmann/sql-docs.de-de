---
title: SQLSetConnectAttr (Cursorbibliothek) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3366ae3e16b75ef1fea3f388f66675ca4c717bc2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLSetConnectAttr** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLSetConnectAttr**, finden Sie unter [Funktion SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Ruft die Anwendung **SQLSetConnectAttr** mit dem SQL_ATTR_ODBC_CURSORS-Attribut, um anzugeben, ob die Cursorbibliothek immer verwendet wird, verwendet wird, wenn der Treiber bildlauffähige Cursor nicht unterstützt oder nie verwendet. Die Cursorbibliothek wird davon ausgegangen, dass ein Treiber bildlauffähige Cursor unterstützt, wenn es für den Typ der SQL_STATIC_CURSOR_ATTRIBUTES1-Informationen in den SQL_CA1_RELATIVE zurückgibt **SQLGetInfo**.  
  
 Muss die Anwendung aufrufen **SQLSetConnectAttr** die Cursorverwendung für die Bibliothek an, nach dem Aufruf **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_DBC auf, um zuordnen die Verbindung, bevor er sich mit der Datenquelle verbindet. Wenn eine Anwendung ruft **SQLSetConnectAttr** mit Attributs SQL_ATTR_ODBC_CURSORS während die Verbindung weiterhin aktiv ist, ist die Cursorbibliothek gibt einen Fehler zurück.  
  
 Um eine von der Cursorbibliothek für alle Anweisungen, die eine Verbindung zugeordneten unterstützt Anweisungsattribut festzulegen, muss eine Anwendung aufrufen **SQLSetConnectAttr** für dieses Anweisungsattribut, nachdem er mit der Datenquelle und bevor sie eine Verbindung herstellt Öffnet den Cursor. Wenn eine Anwendung ruft **SQLSetConnectAttr** mit einer Anweisung Attribut und ein Cursor geöffnet, in einer Anweisung, die der Verbindung zugeordnet ist, das Anweisungsattribut wird nicht für die Anweisung angewendet werden, bis der Cursor geschlossen wird und erneut geöffnet.
