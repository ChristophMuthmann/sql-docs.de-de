---
title: Lesezeichen (ODBC) | Microsoft Docs
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
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: 1d7cccc5-f847-4321-b240-28570854ee5c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 52921fdcc0c71e771b8427cbf2ce0b2f1e1f1f35
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="bookmarks-odbc"></a>Lesezeichen (ODBC)
Ein Lesezeichen ist ein Wert, der verwendet wird, um eine Zeile mit Daten zu identifizieren. Die Bedeutung des Lesezeichenwerts ist nur dem Treiber oder der Datenquelle bekannt. Der Wert kann so einfach wie eine Zeilennummer oder so komplex wie eine Datenträgeradresse sein. Lesezeichen in ODBC unterscheiden sich etwas von Lesezeichen in der Onlinedokumentation zu real. In einem realen Buch wird der Reader ein Lesezeichen auf einer bestimmten Seite platziert, und sucht dann nach diesem Lesezeichen aus, um zur Seite zurückzukehren. In ODBC fordert die Anwendung ein Lesezeichen für bestimmte Zeilen an, speichert es und gibt es an den Cursor für die Rückgabe an die Zeile zurück. So sind Lesezeichen in ODBC ähnelt einem Reader eine Seitenzahl aufzuschreiben Denken Sie daran, es, und klicken Sie dann die Seite erneut nachschlagen.  
  
 Um einen Treiber Unterstützung von Lesezeichen zu ermitteln, eine Anwendung ruft **SQLGetInfo** mit der Option SQL_BOOKMARK_PERSISTENCE. Die Bits in diesem Wert wird beschrieben, was Vorgänge Lesezeichen überstehen, z. B., ob Lesezeichen noch gültig sind, nachdem der Cursor geschlossen ist.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Lesezeichentypen](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [Abrufen von Lesezeichen](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [Scrollen durch Lesezeichen](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [Aktualisieren, Löschen oder Abrufen nach Lesezeichen](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [Vergleichen von Lesezeichen](../../../odbc/reference/develop-app/comparing-bookmarks.md)
