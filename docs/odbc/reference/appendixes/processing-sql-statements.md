---
title: SQL-Anweisungen verarbeiten | Microsoft Docs
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
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
ms.assetid: 54dad6a3-e86c-477b-ba7c-4e95e0385ec1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3613775e14453c2ed14e70cf122bd527217b2cd7
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="processing-sql-statements"></a>Verarbeiten von SQL-Anweisungen
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Der ODBC-Cursorbibliothek übergibt alle SQL-Anweisungen direkt an den Treiber mit Ausnahme der folgenden:  
  
-   Positioniert Update und delete-Anweisungen  
  
-   **SELECT FOR UPDATE** Anweisungen  
  
-   SQL-Anweisungsbatches  
  
 Zum Ausführen von positionierten Updates und delete-Anweisungen und zur Positionierung des Cursors in einer Zeile aufrufen **SQLGetData** für diese Zeile erstellt die Cursorbibliothek eine gesuchte-Anweisung, die die Zeile identifiziert.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Verarbeitung positioniert, Update- und Delete-Anweisungen](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [Wählen Sie für die UPDATE-Anweisungen verarbeiten](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [Verarbeitung von Batches von SQL-Anweisungen](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [Erstellen von komplexen Anweisungen](../../../odbc/reference/appendixes/constructing-searched-statements.md)

