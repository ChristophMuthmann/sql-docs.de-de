---
title: Cursor-Bibliothek Cache | Microsoft Docs
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
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: d6a91cd6-3905-4e3a-98ab-37fce893dbe1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 06b893a857f87c2d6c3911e3d81fd0cd02d89668
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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

