---
title: Hinweise zur Implementierung | Microsoft Docs
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
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 017c58b72d1b190d8d11f08cf7ecce5ff58f65b1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="implementation-notes"></a>Hinweise zur Implementierung
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Abschnitt wird beschrieben, wie die ODBC-Cursorbibliothek implementiert wird. Es wird beschrieben, wie die Cursorbibliothek verwaltet seine Cache, führt SQL-Anweisungen und ODBC-Funktionen implementiert.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Cursorbibliothek-Cache](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [Erstellen von SQL-Anweisungen](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [ODBC-Funktionen und die Cursorbibliothek](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
