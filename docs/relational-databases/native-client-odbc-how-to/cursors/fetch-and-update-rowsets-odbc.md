---
title: Abrufen und Aktualisieren von Rowsets (ODBC) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6fb264cc841109a9bb7c973560e3c285b60e7d76
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="fetch-and-update-rowsets-odbc"></a>Abfragen und Aktualisieren von Rowsets (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-fetch-and-update-rowsets"></a>So können Sie Rowsets abfragen und aktualisieren  
  
1.  Rufen Sie optional [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) mit SQL_ROW_ARRAY_SIZE so ändern Sie die Anzahl der Zeilen (R) im Rowset.  
  
2.  Rufen Sie [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) oder [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) um ein Rowset abzurufen.  
  
3.  Bei der Verwendung von gebundenen Spalten verwenden Sie die Datenwerte und Datenlängen, die nun in den Puffern mit gebundenen Spalten für das Rowset verfügbar sind.  
  
     Bei der Verwendung von ungebundenen Spalten rufen Sie für jede Zeile [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) mit SQL_POSITION auf, um die Cursorposition festzulegen. Gehen Sie anschließend bei jeder ungebundenen Spalte wie folgt vor:  
  
    -   Rufen Sie [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) ein- oder mehrmals zum Abrufen der Daten für ungebundene Spalten nach der letzten Spalte des Rowsets gebundenen. Aufrufe von [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) sollte in der Reihenfolge der spaltenzahlfolge sein.  
  
    -   Rufen Sie [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) mehrere Male auf, um Daten aus einer text- oder image-Spalte abzurufen.  
  
4.  Richten Sie alle Data-at-Execution-text- oder Data-at-Execution-image-Spalten ein.  
  
5.  Rufen Sie [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) oder [SQLBulkOperations](http://go.microsoft.com/fwlink/?LinkId=58398) auf, um die Cursorposition festzulegen und Zeilen im Rowset zu aktualisieren, zu löschen oder hinzuzufügen.  
  
     Data-at-Execution-text- oder Data-at-Execution-image-Spalten, die zum Aktualisieren oder Hinzufügen verwendet werden, müssen verarbeitet werden.  
  
6.  Führen Sie optional eine positionierte Update- oder DELETE-Anweisung, dabei den Cursornamen angeben (Nächten [SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)) und ein anderes Anweisungshandle über dieselbe Verbindung verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Cursorn Gewusst-wie-Themen zur Vorgehensweise &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
  
