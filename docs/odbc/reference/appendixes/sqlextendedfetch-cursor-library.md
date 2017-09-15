---
title: SQLExtendedFetch (Cursorbibliothek) | Microsoft Docs
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
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9c39b299dc2f42fdf1eb51010e7b4fac2bb9bcfd
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLExtendedFetch** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLExtendedFetch**, finden Sie unter [SQLExtendedFetch Funktion](../../../odbc/reference/syntax/sqlextendedfetch-function.md).  
  
 Die Cursorbibliothek implementiert **SQLExtendedFetch** durch wiederholt aufrufen **SQLFetch** im Treiber.  
  
 Die Cursorbibliothek unterstützt Aufrufen **SQLExtendedFetch** mit einem *FetchOrientation* von sql_fetch_bookmark auf.  
  
 Wenn die Cursorbibliothek verwendet wird, Aufrufe von **SQLExtendedFetch** kann nicht kombiniert werden, mit der Aufrufe von **SQLFetchScroll** oder **SQLFetch**.
