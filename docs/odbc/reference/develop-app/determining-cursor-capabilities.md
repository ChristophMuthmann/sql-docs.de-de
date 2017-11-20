---
title: "Festlegen der Cursorfähigkeiten | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], capabilities
- cursors [ODBC], scrollable
ms.assetid: 35be486c-8f2d-4cec-beb8-df14151abfef
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 899a0c01994963a95b6b40936f481882e9634927
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="determining-cursor-capabilities"></a>Festlegen der Cursorfähigkeiten
Die folgenden vier Optionen im **SQLGetInfo** beschreiben, welche Arten von Cursorn unterstützt werden und was ihre Funktionen sind:  
  
-   SQL_CURSOR_SENSITIVITY FEST. Gibt an, ob ein Cursor von einem anderen Cursor vorgenommenen Änderungen berücksichtigt wird.  
  
-   SQL_SCROLL_OPTIONS. Listet die unterstützten Cursortypen (Vorwärtscursor, statische, keysetgesteuerte, dynamische oder gemischten). Alle Datenquellen müssen Vorwärtscursor unterstützen.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 oder SQL_STATIC_CURSOR_ATTRIBUTES1 (je nach Typ des Cursors). Listet die Fetch-Typen von bildlauffähige Cursor unterstützt. Die Bits im Rückgabewert entsprechen den Fetch-Typen in **SQLFetchScroll**.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 oder SQL_STATIC_CURSOR_ATTRIBUTES2 (je nach Typ des Cursors). Listet, ob die statische und keysetgesteuerte Cursor eigene Updates, löschungen und einfügungen erkannt werden können.  
  
 Eine Anwendung kann zur Laufzeit cursorfähigkeiten bestimmen, durch den Aufruf **SQLGetInfo** mit diesen Optionen. Dies erfolgt häufig durch allgemeiner Anwendungen. Cursorfähigkeiten können auch in der Anwendung während der Anwendungsentwicklung und ihrer Verwendung, die hartcodierte ermittelt werden. Dies erfolgt häufig durch vertikale und benutzerdefinierten Anwendungen, jedoch kann auch geschehen, indem die generischen Anwendungen, die eine Implementierung von clientseitigen Cursor z. B. den ODBC-Cursorbibliothek verwenden.

