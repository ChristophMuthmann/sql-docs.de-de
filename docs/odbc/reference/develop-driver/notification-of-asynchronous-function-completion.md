---
title: Der asynchrone Funktion Benachrichtigung | Microsoft Docs
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
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9ef152274bd9ceea650ebd3c74f97c51c18500c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="notification-of-asynchronous-function-completion"></a>Benachrichtigung über Abschluss des asynchronen Funktion
Im SDK für Windows 8 hinzugefügt ODBC einen Mechanismus, um Anwendungen zu benachrichtigen, wenn ein asynchroner Vorgang abgeschlossen dem wir als "Benachrichtigung bei Abschluss" bezeichnet werden ist, an. (Siehe [asynchrone Ausführung (Benachrichtigungsmethode)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) für Weitere Informationen.) In diesem Artikel werden einige der Probleme für Entwickler.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>Die Schnittstelle zwischen der Treiber-Manager und -Treiber  
 Der Treiber-Manager bietet intern eine Rückruffunktion [SQLAsyncNotificationCallback Funktion](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md). **SQLAsyncNotificationCallback** kann nur aufgerufen werden vom Treiber – eine Anwendung direkt ihn nicht aufrufen kann. Der Treiber ruft **SQLAsyncNotificationCallback** bei jedem neue Daten vom Server empfangene nach dem letzten zurückgebenden SQL_STILL_EXECUTING.  
  
 Der Treiber-Manager stellt einen Rückrufmechanismus bereit, damit ein Treiber der Treiber-Manager benachrichtigen kann, wenn einige Status vorgenommen wurde, bei der Ausführung eines asynchronen Vorgangs, nachdem die entsprechende Funktion SQL_STILL_EXECUTING zurückgibt  
  
 Der Treiber-Manager wird das SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK-Attribut für ein Verbindungshandle Treiber mit einem Zeiger nicht-NULL-Funktion, mit dem Typ SQL_ASYNC_NOTIFICATION_CALLBACK, für den Treiber in den Benachrichtigungsmodus für arbeiten alle asynchronen Vorgänge für dieses Handle. Auf ähnliche Weise wird der Treiber-Manager das SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK-Attribut für ein Anweisungshandle Treiber mit einem Zeiger nicht-NULL-Funktion, die auch vom Typ SQL_ASYNC_NOTIFICATION_CALLBACK, für den Treiber in den Benachrichtigungsmodus für Arbeiten ist Alle asynchronen Vorgänge in diesem Handle.  
  
 Wenn ein asynchroner Vorgang für ein Handle für die Treiber ausgeführt wird, sollte die asynchrone Treiberfunktionen in einem nicht blockierenden Stil funktionieren. Wenn der Vorgang sofort ausführen kann, sollten die Treiber-Funktion SQL_STILL_EXECUTING zurück. Diese Anforderung gilt für sowohl Abruf und Notification-Modus zur Verfügung.  
  
 Wenn ein Handle im asynchronen Benachrichtigungsmodus ist, muss der Treiber die Benachrichtigung Callback-Funktion, deren Adresse der Wert für das Attribut SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK oder SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK ist, Aufrufen nach Zurückgeben von SQL_STILL_EXECUTING. Das heißt, muss eine Rückgabe SQL_STILL_EXECUTING mit einem Aufruf der Rückruffunktion Benachrichtigung gekoppelt werden. Der Treiber sollte den aktuellen Wert des Attributs Handle SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT oder SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT als Wert verwenden, für den Aufruf zurück-Funktionsparameter *"pContext"*.  
  
 Der Treiber muss nicht zurück im Thread aufrufen, die der Treiber-Funktion aufruft. Es besteht kein Grund Fortschritt benachrichtigt, bevor die Funktion beendet. Der Treiber sollte einen eigenen Thread an Rückruf verwenden. Der Treiber-Manager wird der Treiber Rückrufthread nicht zum Ausführen des umfangreiche Verarbeitungslogik verwenden.  
  
 Der Treiber-Manager wird die ursprüngliche Funktion erneut aufgerufen, nachdem der Treiber wieder aufgerufen. Der Treiber-Manager kann einen Thread verwenden, der weder ein Thread der Anwendung noch ein Treiber-Thread ist. Wenn der Treiber einige Informationen, die dem Thread (z. B. Sicherheits-Token oder Benutzer-ID) zugeordnet verwendet, sollte der Treiber speichern die erforderliche Informationen in der ersten asynchroner Aufruf und verwenden Sie den gespeicherten Wert vor dem gesamten asynchronen Vorgang abgeschlossen ist. In der Regel nur **SQLDriverConnect**, **SQLConnect**, oder **SQLBrowseConnect** müssen diese Art von Informationen verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Developing an ODBC Driver (Entwickeln eines ODBC-Treibers)](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
