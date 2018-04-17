---
title: SQLBindParameter (Cursorbibliothek) | Microsoft Docs
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
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 54ee24f29d425bd24788d005fa8ad8a09d781a28
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLBindParameter** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLBindParameter**, finden Sie unter [SQLBindParameter-Funktion](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Eine Anwendung kann Aufrufen **SQLBindParameter** Parameter erneut binden, solange die C-Datentyp, die Spaltengröße und die Dezimalstellen der gebundenen Spalte unverändert bleiben.  
  
 Die Cursorbibliothek unterstützt das Festlegen von SQL_ATTR_ROW_BIND_OFFSET_PTR-Anweisungsattribut Bind-Offsets zu verwenden. (**SQLBindParameter** muss nicht für diese erneute Bindung erfolgen aufgerufen werden.)  
  
 Die Cursorbibliothek unterstützt Bindung Data-at-Execution-Parameter.
