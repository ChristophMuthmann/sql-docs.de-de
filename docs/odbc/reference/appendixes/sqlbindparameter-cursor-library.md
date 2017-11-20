---
title: SQLBindParameter (Cursorbibliothek) | Microsoft Docs
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
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 45b3a0355edb0c9fbd37f7047aa0a1e6ff9a1fe8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLBindParameter** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLBindParameter**, finden Sie unter [SQLBindParameter-Funktion](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Eine Anwendung kann Aufrufen **SQLBindParameter** Parameter erneut binden, solange die C-Datentyp, die Spaltengröße und die Dezimalstellen der gebundenen Spalte unverändert bleiben.  
  
 Die Cursorbibliothek unterstützt das Festlegen von SQL_ATTR_ROW_BIND_OFFSET_PTR-Anweisungsattribut Bind-Offsets zu verwenden. (**SQLBindParameter** muss nicht für diese erneute Bindung erfolgen aufgerufen werden.)  
  
 Die Cursorbibliothek unterstützt Bindung Data-at-Execution-Parameter.

