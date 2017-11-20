---
title: SQLGetFunctions (Cursorbibliothek) | Microsoft Docs
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
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6d8ca656e63183df424de2ec45c823ac275ef69f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLGetFunctions** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLGetFunctions**, finden Sie unter [SQLGetFunctions-Funktion](../../../odbc/reference/syntax/sqlgetfunctions-function.md).  
  
 Beim Aufruf **SQLGetFunctions**, die Cursorbibliothek zurückgibt, die Unterstützung der **SQLExtendedFetch**, **SQLFetchScroll**, **SQLSetPos**, und **SQLSetScrollOptions**, zusätzlich zu den Funktionen, die vom Treiber unterstützt werden.

