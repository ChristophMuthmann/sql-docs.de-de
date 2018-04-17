---
title: Einschränkungen bei der Verwendung keysetgesteuerter Cursor | Microsoft Docs
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
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6661ca9104e683cdac84cb3d533736d3a02f42f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Einschränkungen bei der Verwendung keysetgesteuerter Cursor
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Sie müssen eine einzelne Spalte der ROWID für die der abgefragten Tabelle abrufen können. Ein keysetgesteuerter Cursor kann nicht verwendet werden, auf Joins, Abfragen oder Anweisungen mit DISTINCT, GROUP BY, UNION, INTERSECT oder MINUS-Klauseln.  
  
 Auch wenn Ihre Anwendung Tabellenaliasnamen verwendet, funktioniert keysetgesteuerte Cursor nicht. Forward-only- oder statische Cursortypen sind erforderlich. Verwenden das Keyset Cursortyp mit Tabellenaliasnamen führt dazu, dass die folgende Fehlermeldung: "[Microsoft] [ODBC-Treiber für Oracle] können keine keysetgesteuerten Cursors auf die Verknüpfung mit Union, intersect oder minus oder einem schreibgeschützten Resultset."  
  
> [!NOTE]  
>  Aufgrund der Art und Weise der Treiber führt die SQL-Anweisung, die mit dem Oracle-Server gesendet wird, gibt Oracle intern die folgende Fehlermeldung angezeigt: "ORA-00964: Tabelle Name nicht in der Liste."
