---
title: Anzahl der abgerufenen Zeilen und Status | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- number of rows fetched [ODBC]
- result sets [ODBC], row status array
ms.assetid: a069b979-5108-4905-932f-8ae8e7905ff2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16bc3a279e2d4565529dd175c16bce01f9431403
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="number-of-rows-fetched-and-status"></a>Anzahl der abgerufenen Zeilen und Status
Wenn das SQL_ATTR_ROWS_FETCHED_PTR-Anweisungsattribut festgelegt wurde, gibt es einen Puffer, der die Anzahl der durch den Aufruf von abgerufenen Zeilen zurückgibt, **SQLFetch** oder **SQLFetchScroll**, und Fehlerzeilen. (Diese Zahl ist die Anzahl aller Zeilen, die nicht den Status SQL_ROW_NO_ROWS verfügen.) Nach einem Aufruf von **SQLBulkOperations** oder **SQLSetPos**, enthält der Puffer die Anzahl der Zeilen, die durch einen Massenvorgang ausgeführt, die von der Funktion betroffen sind. Wenn das SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut festgelegt wurde, **SQLFetch** oder **SQLFetchScroll** gibt die *zeilenstatusarray,* stellt den Status der einzelnen zurückgegebene Zeile. Der Puffer verweist diese Felder von der Anwendung belegt, und vom Treiber aufgefüllt. Eine Anwendung muss sicherstellen, dass diese Zeiger bleibt gültig, bis der Cursor geschlossen wird.  
  
 Einträge im Array dem Zeilenstatus-Status, ob jede Zeile erfolgreich abgerufen wurde, ob sie aktualisiert wurde, hinzugefügt oder gelöscht, seit dem letzten Abruf wurde und ob Fehler beim Abrufen der zeilenupdates werden. Wenn **SQLFetch** oder **SQLFetchScroll** beim Abrufen einer Zeile eines mehrzeiligen Rowsets ein Fehler auftritt oder wenn **SQLBulkOperations** mit einem *Vorgang*  Argument SQL_FETCH_BY_BOOKMARK ein Fehler beim Ausführen eines Abrufs Bulk auftritt, legt den entsprechenden Wert in der zeilenstatusarray, SQL_ROW_ERROR, weiterhin das Abrufen von Zeilen und gibt SQL_SUCCESS_WITH_INFO zurück. Weitere Informationen zur Fehlerbehandlung und die zeilenstatusarray finden Sie unter der [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) und [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) Beschreibungen-Funktion.
