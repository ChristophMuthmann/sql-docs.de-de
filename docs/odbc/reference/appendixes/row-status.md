---
title: Zeile Status | Microsoft Docs
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
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3af34355fe5f2e41401643161805117612ab0614
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="row-status"></a>Zeilenstatus
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Die Cursorbibliothek erstellt einen Puffer für den Zeilenstatus im Cache. Die Cursorbibliothek Ruft Werte für die zeilenstatusarray (angegeben mit der SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut) aus dieser Puffer ab. Für jede Zeile wird die Cursorbibliothek auf diesen Puffer festgelegt:  
  
-   SQL_ROW_DELETED, bei der Ausführung eine positionierte delete-Anweisung in der Zeile.  
  
-   SQL_ROW_ERROR bei Erreichen ein Fehlers beim Abrufen der zeilenupdates aus der Datenquelle mit wird **SQLFetch**.  
  
-   SQL_ROW_SUCCESS, wenn sie die Zeile wurde erfolgreich aus der Datenquelle mit abruft **SQLFetch**.  
  
-   SQL_ROW_UPDATED, wenn sie eine positioniertes Update-Anweisung in der Zeile ausgeführt wird.
