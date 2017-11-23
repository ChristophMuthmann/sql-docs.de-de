---
title: SQLSetStmtOption (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLSetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 76b813e3-c7dc-4bb2-a710-d2aa9dcfdc36
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 77cd6f6f8ddd09a011dba2cbbe39c962d78b4574
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 ODBC-API-Konformität: Ebene 1  
  
 Legt fest, die im Zusammenhang mit einem Anweisungshandle *Befehls beschäftigt*.  
  
|*fOption*|Zulässige Werte|Kommentare|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|Wenn Sie versuchen, diese *fOption*, gibt der Treiber den Fehler: "Treiber nicht unterstützt". Asynchrone Ausführung unterstützt der Visual FoxPro nicht.|  
|SQL_BIND_TYPE|Eine 32-Bit-Wert, der die Länge der Struktur oder eine Instanz eines Puffers, in dem Ergebniszeile Spalten gebunden werden, die angibt, oder SQL_BIND_BY_COLUMN ein.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|Der Treiber ist SQL_CONCUR_ROWVER, nicht möglich, da Visual FoxPro keine zeilenversionsverwaltung auf Grundlage der Zeitstempel.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|Der Treiber lässt keine SQL_CURSOR_KEYSET_DRIVEN oder SQL_CURSOR_DYNAMIC; finden Sie unter [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) für Weitere Informationen.|  
|SQL_KEYSET_SIZE|Fehler: "Treiber nicht unterstützt"|Visual FoxPro unterstützt nicht das Keyset-Cursor-Modell.|  
|SQL_MAX_LENGTH|0|Wenn Sie versuchen, diese *fOption* Wert, gibt der Treiber den Fehler "Treiber nicht unterstützt".|  
|SQL_MAX_ROWS|0|Wenn Sie versuchen, diese *fOption* Wert, gibt der Treiber den Fehler "Treiber nicht unterstützt".|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|Wenn Sie versuchen, diese *fOption* Wert, gibt der Treiber den Fehler "Treiber nicht unterstützt".|  
|SQL_RETRIEVE_DATA|SQL_RD_ON SQL_RD_OFF||  
|SQL_ROWSET_SIZE SETZEN|1 auf 4.294.967.296||  
|SQL_SIMULATE_CURSOR|Fehler: "Treiber nicht unterstützt"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 Weitere Informationen finden Sie unter [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) in der *ODBC Programmer's Reference*.
