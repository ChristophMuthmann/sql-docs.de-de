---
title: Cursorverhalten | Microsoft Docs
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- version-based optimistic concurrency
- cursors [ODBC], cursor behaviors
- ODBC applications, cursors
- SQL_ATTR_CURSOR_SENSITIVITY option
- SQL_ATTR_CURSOR_SCROLLABLE option
- sensitivity behavior of cursor
- ODBC cursors, cursor behaviors
ms.assetid: 742ddcd2-232b-4aa1-9212-027df120ad35
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d53686929a5e6973006c812f309ddf43ea892cbf
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="cursor-behaviors"></a>Verhalten von Cursorn
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC unterstützt die ISO-Optionen für die Definition des Verhaltens von Cursorn durch Angabe ihrer Bildlauffähigkeit und Sensitivität. Diese Verhaltensweisen werden angegeben, indem Sie die Optionen SQL_ATTR_CURSOR_SCROLLABLE und SQL_ATTR_CURSOR_SENSITIVITY bei einem Aufruf von [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber implementiert diese Optionen, indem er Servercursor mit den folgenden Eigenschaften anfordert.  
  
|Einstellungen für das Cursorverhalten|Angeforderte Servercursoreigenschaften|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE und SQL_SENSITIVE|Keysetgesteuerter Cursor und versionsbasierte vollständige Parallelität|  
|SQL_SCROLLABLE und SQL_INSENSITIVE|Statischer Cursor und Parallelität READ_ONLY|  
|SQL_SCROLLABLE und SQL_UNSPECIFIED|Statischer Cursor und Parallelität READ_ONLY|  
|SQL_NONSCROLLABLE und SQL_SENSITIVE|Vorwärtscursor und versionsbasierte vollständige Parallelität|  
|SQL_NONSCROLLABLE und SQL_INSENSITIVE|Standardresultset (Vorwärts, schreibgeschützt)|  
|SQL_NONSCROLLABLE und SQL_UNSPECIFIED|Standardresultset (Vorwärts, schreibgeschützt)|  
  
 Versionsbasierte vollständige Parallelität erfordert eine **Zeitstempel** Spalte in der zugrunde liegenden Tabelle. Wenn versionsbasierte vollständige parallelitätssteuerung für eine Tabelle angefordert wird, die keine **Zeitstempel** Spalte, die der Server verwendet Werten basierende vollständige Parallelität.  
  
## <a name="scrollability"></a>Bildlauffähigkeit  
 Wenn SQL_ATTR_CURSOR_SCROLLABLE auf SQL_SCROLLABLE festgelegt ist, unterstützt der Cursor alle verschiedenen Werte für die *FetchOrientation* Parameter [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). Wenn SQL_ATTR_CURSOR_SCROLLABLE auf SQL_NONSCROLLABLE festgelegt ist, unterstützt der Cursor nur eine *FetchOrientation* -Wert SQL_FETCH_NEXT.  
  
## <a name="sensitivity"></a>Sensitivität  
 Wenn SQL_ATTR_CURSOR_SENSITIVITY auf SQL_SENSITIVE festgelegt ist, spiegelt der Cursor Datenänderungen wider, die vom aktuellen Benutzer oder über Commitvorgänge anderer Benutzer ausgeführt werden. Wenn SQL_ATTR_CURSOR_SENSITIVITY auf SQL_INSENSITIVE festgelegt ist, spiegelt der Cursor keine Datenänderungen wider.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Cursorn (ODBC)](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md) [Cursoreigenschaften](properties/cursor-properties.md) 
  
  
