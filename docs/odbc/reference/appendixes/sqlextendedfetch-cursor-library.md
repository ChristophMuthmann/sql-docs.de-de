---
title: SQLExtendedFetch (Cursorbibliothek) | Microsoft Docs
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
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 573cf41aae6e36db05789908d92fa7ef710a341b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLExtendedFetch** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLExtendedFetch**, finden Sie unter [SQLExtendedFetch Funktion](../../../odbc/reference/syntax/sqlextendedfetch-function.md).  
  
 Die Cursorbibliothek implementiert **SQLExtendedFetch** durch wiederholt aufrufen **SQLFetch** im Treiber.  
  
 Die Cursorbibliothek unterstützt Aufrufen **SQLExtendedFetch** mit einem *FetchOrientation* von sql_fetch_bookmark auf.  
  
 Wenn die Cursorbibliothek verwendet wird, Aufrufe von **SQLExtendedFetch** kann nicht kombiniert werden, mit der Aufrufe von **SQLFetchScroll** oder **SQLFetch**.
