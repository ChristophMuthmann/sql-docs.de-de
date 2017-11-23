---
title: SQLRowCount (Cursorbibliothek) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 586b1f9aa2c246cd410cbb7c56f303cfbea15cc5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLRowCount** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLRowCount**, finden Sie unter [SQLRowCount-Funktion](../../../odbc/reference/syntax/sqlrowcount-function.md).  
  
 Wenn eine Anwendung ruft **SQLRowCount** mit der Anweisung, die dem Cursor zugeordnet ist, gibt die Cursorbibliothek die Anzahl von Zeilen mit Daten, die sie aus dem Treiber abgerufen wurde.  
  
 Wenn eine Anwendung ruft **SQLRowCount** mit der Anweisung, die eine positionierte Update- oder Delete-Anweisung zugeordnet, die Cursorbibliothek gibt die Anzahl der von dieser Anweisung betroffenen Zeilen zurück.  
  
 Wenn eine Anwendung aufruft **SQLRowCount** nach einer **wählen** -Anweisung, die Cursorbibliothek gibt-1 zurück.
