---
title: Cursor-Bibliothek Cache | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: d6a91cd6-3905-4e3a-98ab-37fce893dbe1
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0da55a85fa5f8e1fd53656aa1cac37959a4200f7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="cursor-library-cache"></a>Cursor-Bibliothek-Cache
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Für jede Zeile der Daten im Resultset speichert die Cursorbibliothek die Daten für jede gebundene Spalte, die Länge der Daten in jede gebundene Spalte und den Status der Zeile. Die Cursorbibliothek verwendet die Werte in den Cache für die zurückzugebenden über **SQLFetch** und **SQLFetchScroll** und komplexe Anweisungen für positionierte Operationen zu erstellen. Weitere Informationen finden Sie unter [durchsucht-Anweisungen konstruieren](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Spaltendaten](../../../odbc/reference/appendixes/column-data.md)  
  
-   [Länge der Spaltendaten](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [Zeilenstatus](../../../odbc/reference/appendixes/row-status.md)  
  
-   [Ort des Caches](../../../odbc/reference/appendixes/location-of-cache.md)
