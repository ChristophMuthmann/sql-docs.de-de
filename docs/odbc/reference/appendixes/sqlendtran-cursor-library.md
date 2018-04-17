---
title: SQLEndTran (Cursorbibliothek) | Microsoft Docs
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
- SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a908fbb43a6c568fd536c7ea2f47a523de287f3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLEndTran** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLEndTran**, finden Sie unter [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
 Die Cursorbibliothek unterstützt keine Transaktionen und übergibt Sie Aufrufe von **SQLEndTran** direkt an den Treiber. Die Cursorbibliothek unterstützt die Commit- und Rollback-Verhalten von Cursorn jedoch von der Datenquelle mit den Typen von SQL_CURSOR_ROLLBACK_BEHAVIOR und SQL_CURSOR_COMMIT_BEHAVIOR Informationen zurückgegeben:  
  
-   Für Datenquellen, die in allen Transaktionen Cursor erhalten, werden Änderungen, die in der Datenquelle zurückgesetzt werden nicht in die Cursorbibliothek Cache zurückgesetzt. Um den Cache, der die Daten in der Datenquelle entsprechen machen zu können, muss die Anwendung schließen und öffnen den Cursor.  
  
-   Für Datenquellen, die am Transaktionsgrenzen Cursor geschlossen wird, die Cursorbibliothek die Cursor schließt und löscht den Cache für alle Anweisungen für die Verbindung.  
  
-   Für Datenquellen, die vorbereitete Anweisungen an den Begrenzungen der Transaktion zu löschen, muss die Anwendung alle vorbereitete Anweisungen für die Verbindung, bevor sie reexecuting reprepare.
