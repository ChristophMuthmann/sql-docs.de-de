---
title: Anweisungsoptionen | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- custom statement options [ODBC]
- statement options [ODBC]
- ODBC driver for Oracle [ODBC], statement options
ms.assetid: cd73b769-c8b5-43e0-9f80-b3011b7a6162
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 75a4eef546e37fea71e88fa5d8926c7b5bd95ac2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="statement-options"></a>Optionen-Anweisung
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Diese Optionen ermöglichen die Anpassung einer bestimmten Ausführung-Anweisung innerhalb einer Anwendung.  
  
|Option-Anweisung|Hinweise|  
|----------------------|-----------|  
|SQL_BIND_TYPE|Darf verfügbaren Arbeitsspeicher oder 2.147.483.647 Bytes nicht überschreiten.|  
|SQL_CONCURRENCY|Zulässige Werte finden Sie unter der [Cursortyp und Parallelität Kombinationen](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_CURSOR_TYPE|Der Treiber lässt keine SQL_CURSOR_DYNAMIC. Finden Sie unter [SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) für Weitere Informationen. Zulässige Werte finden Sie unter der [Cursortyp und Parallelität Kombinationen](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_GET_BOOKMARK|Gibt einen ganze 32-Bit-Wert, der das Lesezeichen für die aktuelle Datensatznummer ist. Nur abgerufen werden. kann nicht festgelegt.|  
|SQL_KEYSET_SIZE|Kann nur auf 0 festgelegt werden.|  
|SQL_MAX_ROWS|Legen Sie die maximale Anzahl von Zeilen aus einem Resultset zurückgegeben.|  
|SQL_ROW_NUMBER|Gibt eine 32-Bit-Ganzzahl, die die Position der aktuellen Zeile im Resultset angeben. Nur abgerufen werden. kann nicht festgelegt.|  
|SQL_ROWSET_SIZE SETZEN|4.294.967.296 Zeilen darf nicht überschreiten; Allerdings benötigen Sie genügend virtuellen Arbeitsspeicher auf dem Computer, um Ihre Anforderung zu verarbeiten.|  
|SQL_USE_BOOKMARKS|Unterstützt das Festlegen von SQL_USE_BOOKMARKS zu SQL_UB_ON und fester Länge Lesezeichen macht.|
