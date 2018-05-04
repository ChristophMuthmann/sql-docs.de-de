---
title: Durchführen eines Bildlaufs und das Abrufen von Zeilen | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-cursors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- SQLFetchScroll function
- ODBC applications, cursors
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- fetching [ODBC]
- ODBC cursors, scrolling rows
ms.assetid: 9109f10d-326b-4a6d-8c97-831f60da8c4c
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6c7b0d1f850ad554d507a63513d12992c0281c88
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="scrolling-and-fetching-rows"></a>Bildläufe und Abrufen von Zeilen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Um einen bildlauffähigen Cursor zu verwenden, muss eine ODBC-Anwendung folgende Bedingungen erfüllen:  
  
-   Festlegen die cursorfähigkeiten mit [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
-   Öffnen des Cursors mit **SQLExecute** oder **SQLExecDirect**.  
  
-   Scroll und Fetch-Zeilen, die mithilfe von **SQLFetch** oder [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md).  
  
 Beide **SQLFetch** und **SQLFetchScroll** Zeilenblöcke zu einem Zeitpunkt abgerufen werden können. Die Anzahl der zurückgegebenen Zeilen mithilfe von angegeben **SQLSetStmtAttr** Festlegen des SQL_ATTR_ROW_ARRAY_SIZE-Parameters.  
  
 ODBC-Anwendungen können **SQLFetch** , über einen Vorwärtscursor abzurufen.  
  
 **SQLFetchScroll** wird verwendet, um in einem Cursor einen Bildlauf durchführen. **SQLFetchScroll** unterstützt das Abrufen des nächsten, vorherigen, ersten und letzten Rowsets zusätzlich zum relativen abrufen (das Rowset abrufen, *n* Zeilen vom Anfang des aktuellen Rowsets) und absoluten abrufen (Fetch-Rowset angefangen bei Zeile *n*). Wenn *n* ist in einem absoluten Abruf negativ ist, werden Zeilen aus dem Ende des Resultsets gezählt. Ein absoluter Abruf von Zeile -1 bedeutet den Abruf des Rowsets, das mit der letzten Zeile im Resultset beginnt.  
  
 Anwendungen, die **SQLFetchScroll** nur Cursor-Funktionen, z. B. Berichte, sind wahrscheinlich für die Weiterleitung über das Resultset auf eines einzigen Mal und verwenden die Option zum Abrufen des nächsten Rowsets. Bildschirmbasierte Anwendungen andererseits, nutzen die Funktionen des **SQLFetchScroll**. Wenn die Anwendung die Rowsetgröße auf die Anzahl der Zeilen, die auf dem Bildschirm angezeigt legt, und die Bildschirmpuffer an das Resultset bindet, können sie Vorgänge der Bildlaufleiste direkt in Aufrufe an übersetzen **SQLFetchScroll**.  
  
|Bildlaufleistenvorgang|SQLFetchScroll-Bildlaufoption|  
|--------------------------|-------------------------------------|  
|Bild auf|SQL_FETCH_PRIOR|  
|Bild ab|SQL_FETCH_NEXT|  
|Zeile auf|SQL_FETCH_RELATIVE mit FetchOffset gleich-1|  
|Zeile ab|SQL_FETCH_RELATIVE mit FetchOffset gleich 1|  
|Bildlauffeld nach oben|SQL_FETCH_FIRST|  
|Bildlauffeld nach unten|SQL_FETCH_LAST|  
|Zufällige Bildlauffeldposition|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Kennzeichnen von Zeilen in ODBC](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Cursorn & #40; ODBC & #41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
