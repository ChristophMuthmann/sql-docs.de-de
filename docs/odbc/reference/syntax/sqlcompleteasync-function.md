---
title: SQLCompleteAsync Funktion | Microsoft Docs
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
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 93a6362bf0a0f7870d1fed5dfeafa5cdf1885cd3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.8  
  
 Einhaltung von Standards: keine  
  
 **Zusammenfassung**  
 **SQLCompleteAsync** können verwendet werden, um zu ermitteln, wann eine asynchrone Funktion verwenden entweder Benachrichtigung oder Abruf-basierten Verarbeitung abgeschlossen ist. Weitere Informationen zu asynchronen Vorgängen finden Sie unter [asynchrone Ausführung](../../../odbc/reference/develop-app/asynchronous-execution.md).  
  
 **SQLCompleteAsync** ist nur in der ODBC-Treiber-Manager implementiert.  
  
 Im Modus für asynchrone Verarbeitung der Benachrichtigung basierend **SQLCompleteAsync** muss aufgerufen werden, nachdem der Treiber-Manager das Ereignisobjekt für Benachrichtigungen verwendet ausgelöst. **SQLCompleteAsync** schließt den asynchronen Verarbeitung und die asynchrone-Funktion generiert einen Rückgabecode.  
  
 Im Modus für asynchrone Verarbeitung Abruf basierend **SQLCompleteAsync** ist eine Alternative zum Aufrufen der ursprüngliche asynchrone-Funktion, ohne die Argumente angeben, in den ursprünglichen asynchrone-Funktionsaufruf. **SQLCompleteAsync** kann verwendet werden, unabhängig davon, ob die ODBC-Cursorbibliothek aktiviert ist.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *HandleType*  
 [Eingabe] Der Typ des Handles auf dem asynchronen abgeschlossen verarbeiten. Gültige Werte sind SQL_HANDLE_DBC oder SQL_HANDLE_STMT auf.  
  
 *Handle*  
 [Eingabe] Das Handle auf dem asynchronen abgeschlossen verarbeiten. Wenn *behandeln* ist kein gültiges Handle von den vom angegebenen Typ *HandleType*, **SQLCompleteAsync** gibt SQL_INVALID_HANDLE zurück.  
  
 Wenn *behandeln* ist kein gültiges Handle von den vom angegebenen Typ *HandleType*, **SQLCompleteAsync** gibt SQL_INVALID_HANDLE zurück.  
  
 *AsyncRetCodePtr*  
 [Ausgabe] Zeiger auf einen Puffer, der den Rückgabecode, der die asynchrone API enthalten soll. Wenn *AsyncRetCodePtr* NULL ist, **SQLCompleteAsync** gibt SQL_ERROR zurück.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLCompleteAsync** gibt SQL_SUCCESS zurück, die eine Anwendung sollte den Rückgabecode der asynchronen Funktion abzurufen, aus dem Puffer verweist *AsyncRetCodePtr*. Zugeordnete SQLSTATE, sofern vorhanden, erhalten Sie, indem Aufrufen **SQLGetDiagRec** mit einer *HandleType* von SQL_HANDLE_STMT auf, und ein Anweisungshandle oder ein *HandleType* von SQL_ HANDLE_DBC und ein Verbindungshandle. Diese DiagnoseDatensätze sind mit der asynchronen-Funktion, nicht dadurch verknüpfte **SQLCompleteAsync** Funktion.  
  
 **SQLCompleteAsync** gibt ein anderen Codes als SQL_SUCCESS zurück, um anzugeben, dass **SQLCompleteAsync** ist nicht richtig aufgerufen. **SQLCompleteAsync** alle Diagnosedatensatz nicht in diesem Fall gesendet. Möglicher Rückgabecodes sind:  
  
-   SQL_INVALID_HANDLE: Das Handle erkennbar *HandleType* und *behandeln* ist kein gültiges Handle.  
  
-   SQL_ERROR: *AsyncRetCodePtr* NULL ist oder die asynchrone Verarbeitung auf das Handle nicht aktiviert ist.  
  
-   SQL_NO_DATA: Im Modus "Benachrichtigung" ein asynchroner Vorgang wird nicht ausgeführt, oder der Treiber-Manager wurde die Anwendung nicht benachrichtigt. Im Modus "Abruf" ist ein asynchroner Vorgang nicht ausgeführt.  
  
## <a name="comments"></a>Kommentare  
 Im Modus für asynchrone Verarbeitung Abruf basierend *AsyncRetCodePtr* SQL_STILL_EXECUTING möglicherweise beim **SQLCompleteAsync** gibt SQL_SUCCESS zurück. Anwendung sollte bis abrufen beibehalten *AsyncRetCodePtr* ist kein SQL_STILL_EXECUTING. Im Modus für asynchrone Verarbeitung der Benachrichtigung basierend *AsyncRetCodePtr* werden nie SQL_STILL_EXECUTING.  
  
## <a name="see-also"></a>Siehe auch  
 [Asynchrone Ausführung (Abrufmethode)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
