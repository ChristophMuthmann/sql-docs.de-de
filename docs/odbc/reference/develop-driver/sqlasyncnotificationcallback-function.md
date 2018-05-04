---
title: SQLAsyncNotificationCallback Funktion | Microsoft Docs
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
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2dc584145ea87b34ecfa9417cc89135b1fbc98d4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.8  
  
 Einhaltung von Standards: keine  
  
 **Zusammenfassung**  
 **SQLAsyncNotificationCallback** können Sie einen Treiber für den Rückruf an den Treiber-Manager an, bei einigen Fortschritt für den aktuellen asynchronen Vorgang, nachdem der Treiber SQL_STILL_EXECUTING zurückgibt. **SQLAsyncNotificationCallback** können nur vom Treiber aufgerufen.  
  
 Rufen Sie Treiber nicht **SQLAsyncNotificationCallback** mit Funktionsnamen **SQLAsyncNotificationCallback**. Der Treiber-Manager übergibt einen Funktionszeiger stattdessen einem Treiberpaket als Wert für die SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK oder SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK-Attribut des entsprechenden Verbindungshandle oder Anweisungshandle, bzw. Andere Handles können andere Funktion Zeigerwerte zugewiesen werden. Der Typ des Funktionszeigers wird als SQL_ASYNC_NOTIFICATION_CALLBACK definiert.  
  
 **SQLAsyncNotificationCallback** ist threadsicher. Ein Treiber können mit mehreren Threads aufgerufen **SQLAsyncNotificationCallback** auf anderen handles gleichzeitig.  
  
## <a name="syntax"></a>Syntax  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>Argumente  
 *pContex*  
 Ein Zeiger auf eine Datenstruktur, die vom Treiber-Manager definiert. Der Wert wird über SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) oder SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT) an den Treiber übergeben.  Der Treiber verfügt nicht über die Zugriffsrechte auf den Wert.  
  
 *fLast*  
 Ein Treiber, gibt an, dass dieser Rückruf-Funktionsaufruf für den aktuellen asynchronen Vorgang zum letzten Blatt wird verwendet. Der Treiber gibt einen anderen Rückgabecode als SQL_STILL_EXECUTING zurück, wenn der Treiber-Manager die Funktion erneut aufgerufen. Der Treiber-Manager kann diese Informationen, z. B. verwenden, um die Anwendung im Voraus zu informieren, die der asynchrone Vorgang abgeschlossen wird.  
  
 Wenn *behandeln* ist kein gültiges Handle von den vom angegebenen Typ *HandleType*, **SQLCancelHandle** gibt SQL_INVALID_HANDLE zurück.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS oder SQL_ERROR zurück.  
  
## <a name="diagnostics"></a>Diagnose  
 **SQLAsyncNotificationCallback** können SQL_ERROR zurück, für die folgenden zwei Fälle, die (diese Werte zeigen einen Implementierungsproblem im Treiber oder Treiber-Manager.  
  
|Fehler|Description|  
|-----------|-----------------|  
|Verbindung oder Anweisung keine Benachrichtigung angefordert.||  
|Ungültige *behandeln*|Der Treiber übergeben eines ungültigen Handles, das nicht die interne Tests zur Überprüfung der Treiber-Manager konnte.|  
  
## <a name="see-also"></a>Siehe auch  
 [Asynchrone Ausführung (Abrufmethode)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
