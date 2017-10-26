---
title: "Fehlercodes für ODBC Cursor Library | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 308ad8ed54aacb9ab7bc169efd9dad020e2f2b66
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-cursor-library-error-codes"></a>ODBC Cursor Library-Fehlercodes
> [!IMPORTANT]  
>  Dieses Feature wird in einer zukünftigen Version von Microsoft Data Access-Komponente entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Verwenden Sie stattdessen die Treiber und Server-Cursor.  
  
 Der ODBC-Cursorbibliothek gibt die folgenden SQLSTATEs neben den aufgeführten [ODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
> [!NOTE]  
>  Die Cursorbibliothek sortiert Statusdatensätze nicht; der Treiber-Manager und der ODBC-3. *x* Treiber sind verantwortlich für die Anordnung der Statusdatensätze.  
  
|SQLSTATE|Description|Kann von zurückgegeben werden|  
|--------------|-----------------|--------------------------|  
|01000|Cursor kann nicht aktualisiert werden.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|Die Cursorbibliothek nicht verwendet. Fehler beim Laden.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Die Cursorbibliothek nicht verwendet. Nicht genügend treiberunterstützung.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Die Cursorbibliothek nicht verwendet. Versionskonflikt mit Treiber-Manager.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Treiber hat SQL_SUCCESS_WITH_INFO zurückgegeben. Die Warnung wurde unterbrochen.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|Allgemeiner Fehler: kann nicht erstellt werden Dateipuffers.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Allgemeiner Fehler: kann nicht aus Dateipuffer gelesen werden.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Allgemeiner Fehler: kann nicht in Datei schreiben.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Allgemeiner Fehler: nicht schließen, oder Entfernen des Dateipuffers.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|Positionierte Anforderung kann nicht ausgeführt werden, da keine durchsuchbaren Spalten gebunden wurden.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|Positionierte Anforderung konnte nicht ausgeführt werden, da Resultset mit einer Join-Bedingung erstellt wurde.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|Gebundene Puffer überschreitet die maximale Segmentgröße.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|Resultset wurde nicht generiert, indem eine **wählen** Anweisung.|**SQLGetData**|  
|SL005|**Wählen Sie** -Anweisung enthält eine GROUP BY-Klausel.|**SQLGetData**|  
|SL006|Parameterarrays werden mit positionierten Anforderungen nicht unterstützt.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** ist nicht in einem Vorwärtscursor (gepuffertes) Cursor zulässig.|**SQLGetData**|  
|SL009|Keine Spalten gebunden wurden, vor dem Aufruf **SQLFetch** oder **SQLFetchScroll**.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** SQL_ERROR zurückgegeben, bei dem Versuch, auf einen internen Puffer zu binden.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|Option-Anweisung gültig ist, nur nach dem Aufruf **SQLFetch** oder **SQLFetchScroll**.|**SQLGetStmtAttr**|  
|SL012|Anweisung Bindungen darf nicht geändert werden, während ein Cursor geöffnet ist.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|Eine positionierte Anforderung ausgestellt wurde, und nicht alle Spaltenfelder Anzahl wurden gepuffert.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** und **SQLFetchScroll** kann nicht kombiniert werden.|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|

