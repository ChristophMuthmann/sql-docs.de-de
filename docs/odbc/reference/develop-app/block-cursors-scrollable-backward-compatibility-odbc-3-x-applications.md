---
title: "Blocks und bildlauffähigen Cursor-Anwendungskompatibilität für ODBC 3.x | Microsoft Docs"
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
helpviewer_keywords:
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- SQLExtendedFetch function [ODBC], block cursors
- cursors [ODBC], compatibility issues
- SQLFetchScroll function [ODBC], block cursors
ms.assetid: 82f6cf68-cfde-4417-9788-d6382ca14bf8
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bc3b2fa0e72329300f4fb6aa52c274a0ce0f9b83
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>Blockcursor, scrollfähige Cursor und Abwärtskompatibilität für ODBC 3.x-Anwendungen
Das Vorhandensein beider **SQLFetchScroll** und **SQLExtendedFetch** stellt den ersten Clear Teilen in ODBC zwischen der API Application Programming Interface (), die den Satz von Funktionen ist die Ruft Anwendung und der Service Provider-Schnittstelle (SPI), also den Satz von Funktionen der Treiber implementiert. Diese Teilung ist erforderlich, um in ODBC 3. zu meistern. *x*, welche verwendet **SQLFetchScroll**, um den Standards ausgerichtet und mit ODBC-2 kompatibel sein. *X*, welche verwendet **SQLExtendedFetch**.  
  
 Die ODBC 3.*.x* -API, die ist der Satz von Funktionen die Anwendung ruft, umfasst **SQLFetchScroll** und verwandte Anweisungsattribute. Die ODBC 3.*.x* SPI, also den Satz von Funktionen der Treiber implementiert wird, umfasst **SQLFetchScroll**, **SQLExtendedFetch**, und verwandte Anweisungsattribute. Da ODBC Teilung zwischen der API und der SPI nicht formal erzwingt, ist es möglich, ODBC 3.*.x* aufrufen, **SQLExtendedFetch** und verwandte Anweisungsattribute. Es besteht jedoch kein Grund für ODBC 3.*.x* Anwendungen dazu. Weitere Informationen über APIs und SPIs Siehe die Einführung zu [ODBC-Architektur](../../../odbc/reference/odbc-architecture.md).  
  
 Informationen zur Verwendung der ODBC-3. *x* Treibermanager ordnet Aufrufe an ODBC 2.. *X* und ODBC-3. *X* Treiber und welche Funktionen und die Anweisung eine ODBC-3-Attribute. *X* Treiber für Blocks und bildlauffähigen Cursorn implementieren sollten, finden Sie unter [der Treiber Wirkungsweise](../../../odbc/reference/appendixes/what-the-driver-does.md) in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.  
  
 Die folgende Tabelle fasst zusammen, welche Funktionen und Anweisungsattribute eine ODBC-3. *x* Anwendung sollte mit Blocks und bildlauffähigen Cursor verwenden. Außerdem werden Änderungen zwischen ODBC 2. aufgeführt. *x* und ODBC-3. *X* in diesem Bereich dieser ODBC 3.. *X* Anwendungen bewusst sein, die mit ODBC-2 kompatibel sein. *X* Treiber.  
  
|Funktion oder<br /><br /> Anweisungsattribut|Kommentare|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Verweist auf das Lesezeichen für die Verwendung mit **SQLFetchScroll**.<br /><br /> Wenn eine Anwendung dies in einer ODBC 2. festlegt. *x* -Treiber verwenden, muss dies zu einem Lesezeichen fester Länge verweisen.|  
|SQL_ATTR_ROW_STATUS_PTR|Verweist auf die zeilenstatusarray von ausgefüllt **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, und **SQLSetPos**.<br /><br /> Wenn eine Anwendung dies in einer ODBC 2. festlegt. *x* Treiber und Aufrufe **SQLBulkOperation** mit einem *Vorgang* von SQL_ADD vor dem Aufruf **SQLFetchScroll**,  **SQLFetch**, oder **SQLExtendedFetch**, SQLSTATE HY011 (Attribut kann nicht jetzt festgelegt werden) wird zurückgegeben.<br /><br /> Wenn eine Anwendung ruft **SQLFetch** in einer ODBC 2.. *X* -Treiber **SQLFetch** zugeordnet **SQLExtendedFetch** und aus diesem Grund gibt Werte in diesem Array zurück.|  
|SQL_ATTR_ROWS_FETCHED_PTR FEST|Verweist auf den Puffer, in dem **SQLFetch** und **SQLFetchScroll** geben die Anzahl der abgerufenen Zeilen zurück.<br /><br /> Wenn eine Anwendung ruft **SQLFetch** in einer ODBC 2.. *X* -Treiber **SQLFetch** zugeordnet **SQLExtendedFetch** und daher einen Wert zurückgibt, in diesem Puffer.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Legt die Größe des Rowsets fest.<br /><br /> Wenn eine Anwendung ruft **SQLBulkOperations** mit einem *Vorgang* von SQL_ADD in einer ODBC 2.. *X* SQL_ROWSET_SIZE setzen-Treiber wird für den Aufruf nicht SQL_ATTR_ROW_ARRAY_SIZE, verwendet werden, da der Aufruf zugeordnet ist **SQLSetPos** mit einem *Vorgang* der SQL_ADD, der verwendet SQL_ROWSET_SIZE SETZEN.<br /><br /> Aufrufen von **SQLSetPos** mit einer *Vorgang* von SQL_ADD oder **SQLExtendedFetch** in einer ODBC-2. *X* -Treiber verwendet SQL_ROWSET_SIZE setzen.<br /><br /> Aufrufen von **SQLFetch** oder **SQLFetchScroll** in einer ODBC-2. *X* verwendet der Treiber SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLBulkOperations**|Führt Einfüge-und Lesezeichen. Wenn **SQLBulkOperations** mit einem *Vorgang* SQL_ADD genannt wird in einer ODBC 2.. *X* Treiber, zugeordnet, um **SQLSetPos** mit einer *Vorgang* von SQL_ADD. Im folgenden finden Details zur Implementierung:<br /><br /> – Wenn Sie mit einer ODBC 2. arbeiten zu können. *x* -Treiber verwenden, muss eine Anwendung nur die zugeordneten implizit zugeordneten ARD verwenden die *StatementHandle*; kann nicht einem anderen ARD zum Hinzufügen von Zeilen zugeordnet werden, da explizite Deskriptor Vorgänge sind in einer ODBC 2. unterstützt nicht. *x* Treiber. Eine Anwendung verwenden, muss **SQLBindCol** nicht an die ARD binden **SQLSetDescField** oder **SQLSetDescRec**.<br />– Wenn Sie eine ODBC 3. aufrufen. *x* -Treiber verwenden, eine Anwendung kann Aufrufen **SQLBulkOperations** mit einer *Vorgang* von SQL_ADD vor dem Aufruf **SQLFetch** oder **SQLFetchScroll**. Beim Aufrufen einer ODBC 2.. *x* -Treiber verwenden, es muss eine Anwendung aufrufen **SQLFetchScroll** vor dem Aufruf **SQLBulkOperations** mit einem Vorgang SQL_ADD.|  
|**SQLFetch**|Gibt das nächste Rowset zurück. Im folgenden finden Details zur Implementierung:<br /><br /> – Wenn eine Anwendung ruft **SQLFetch** in einer ODBC 2.. *X* Treiber, zugeordnet, um **SQLExtendedFetch**.<br />– Wenn eine Anwendung ruft **SQLFetch** in einer ODBC-3. *X* -Treiber verwenden, gibt die Anzahl der Zeilen, die mit dem SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut angegebenen zurück.|  
|**SQLFetchScroll**|Gibt das angegebene Rowset zurück. Im folgenden finden Details zur Implementierung:<br /><br /> – Wenn eine Anwendung ruft **SQLFetchScroll** in einer ODBC 2.. *X* -Treiber SQLSTATE 01 s 01 zurückgegeben (Fehler in Zeile) vor jedem Fehler, der auf eine einzelne Zeile angewendet wird. Dies geschieht, da die ODBC 3.*.x* Treibermanager ordnet diese Option, um **SQLExtendedFetch** und **SQLExtendedFetch** SQLSTATE zurückgegeben. Wenn eine Anwendung ruft **SQLFetchScroll** in einer ODBC-3. *X* -Treiber verwenden, wird nie zurückgegeben SQLSTATE 01 s 01 (Fehler in Zeile).<br />– Wenn eine Anwendung ruft **SQLFetchScroll** in einer ODBC 2.. *X* Treiber mit *FetchOrientation* festgelegt sql_fetch_bookmark auf, die *FetchOffset* Argument muss auf 0 festgelegt werden. SQLSTATE HYC00 (optionales Feature nicht implementiert) wird zurückgegeben, wenn Offset-basierte Lesezeichen Abrufen von Zeilen mit einer ODBC 2. versucht wird. *x* Treiber.|  
  
> [!NOTE]  
>  ODBC-3. *x* Anwendungen sollten keine verwenden **SQLExtendedFetch** oder das Anweisungsattribut SQL_ROWSET_SIZE setzen. Verwenden sie stattdessen, **SQLFetchScroll** und SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut. ODBC-3. *x* Anwendungen sollte nicht verwendet werden **SQLSetPos** mit einem *Vorgang* der SQL_ADD jedoch die zu verwendende **SQLBulkOperations** mit einer *Vorgang* von SQL_ADD.
