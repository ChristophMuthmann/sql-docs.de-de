---
title: SQLFetchScroll (Cursorbibliothek) | Microsoft Docs
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
helpviewer_keywords: SQLFetchScroll function [ODBC], Cursor Library
ms.assetid: 4417e57c-31dd-475e-8fe9-eab00a459c80
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7e864cf48e199f414d4cb012c5513be0fc844820
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLFetchScroll** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLFetchScroll**, finden Sie unter [SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 Die Cursorbibliothek implementiert **SQLFetchScroll** durch wiederholt aufrufen **SQLFetch** im Treiber. Er überträgt die Daten, die sie aus dem Treiber die Rowset-Puffer, die von der Anwendung bereitgestellte abgerufen wird. Es werden auch die Daten im Arbeitsspeicher und Datenträger Dateien zwischengespeichert. Wenn eine Anwendung eine neue Rowset anfordert, die Cursorbibliothek wird abgerufen nach Bedarf aus dem Treiber (sofern er nicht bereits abgerufen wurde) oder den Cache (sofern sie zuvor abgerufen wurde). Schließlich wird die Cursorbibliothek verwaltet den Status der zwischengespeicherten Daten und gibt diese Informationen an die Anwendung in der zeilenstatusarray zurück.  
  
 Wenn die Cursorbibliothek verwendet wird, Aufrufe von **SQLFetchScroll** kann nicht kombiniert werden, mit der Aufrufe von **SQLFetch** oder **SQLExtendedFetch**.  
  
 Wenn die Cursorbibliothek verwendet wird, Aufrufe von **SQLFetchScroll** sind unterstützt ODBC 2.. *X* und für ODBC 3. *X* Treiber.  
  
## <a name="rowset-buffers"></a>Rowset-Puffer  
 Die Cursorbibliothek optimiert die Übertragung von Daten aus dem Treiber an die Rowset-Puffer, die von der Anwendung bereitgestellt werden, wenn:  
  
-   Die Anwendung verwendet die zeilenweise Bindung.  
  
-   Es sind keine nicht verwendeten Bytes zwischen Feldern in der Struktur, die die Anwendung deklariert wird, um eine Zeile mit Daten zu speichern.  
  
-   Die Felder in der **SQLFetch** oder **SQLFetchScroll** gibt den Längenindikator für eine Spalte den Puffer für diese Spalte folgt und den Puffer für die nächste Spalte vorausgeht. Diese Felder sind optional.  
  
 Wenn die Anwendung ein neues Rowset anfordert, ruft die Cursorbibliothek Daten ab, aus dem Cache und aus dem Treiber nach Bedarf. Wenn die alten und neuen Rowsets überschneiden, kann die Cursorbibliothek die Leistung optimieren, indem Wiederverwenden von Daten aus der überlappenden Bereiche der Rowset-Puffer. Daher sind nicht gespeicherte Änderungen an die Rowset-Puffer verloren, wenn die alten und neuen Rowsets überschneiden, und die Änderungen überlappende Bereiche der Rowset-Puffer werden. Um die Änderungen zu speichern, sendet eine Anwendung eine positionierte Update-Anweisung.  
  
 Beachten Sie, dass die Cursorbibliothek werden immer die Rowset-Puffer mit Daten aus dem Cache aktualisiert, wenn eine Anwendung ruft **SQLFetchScroll** mit der *FetchOrientation* SQL_FETCH_RELATIVE-Argument festgelegt und die *FetchOffset* Argument auf 0 festgelegt.  
  
 Die Cursorbibliothek unterstützt Aufrufen **SQLSetStmtAttr** mit einem *Attribut* von SQL_ATTR_ROW_ARRAY_SIZE, um die Größe des Rowsets zu ändern, während ein Cursor geöffnet ist. Die neue Rowsetgröße wirksam das nächste Mal **SQLFetchScroll** aufgerufen wird.  
  
## <a name="result-set-membership"></a>Resultset  
 Die Cursorbibliothek Ruft Daten aus dem Treiber ab, nur, wenn die Anwendung sie anfordert. Abhängig von der Datenquelle und die Einstellung des Attributs Anweisung SQL_CONCURRENCY hat dies folgende Konsequenzen:  
  
-   Die abgerufenen Daten, indem die Cursorbibliothek können aus den Daten abweichen, die verfügbaren die zum Zeitpunkt der Ausführung die Anweisung. Nachdem der Cursor geöffnet wurde, können z. B. Zeilen an eine Stelle hinter der aktuellen Cursorposition eingefügt durch einige Treiber abgerufen werden.  
  
-   Die Daten in das Resultset möglicherweise durch die Datenquelle für die Cursorbibliothek gesperrt und sind daher nicht für andere Benutzer verfügbar.  
  
 Nachdem die Cursorbibliothek eine Zeile mit Daten zwischengespeichert, kann er nicht Änderungen an dieser Zeile in der zugrunde liegenden Datenquelle (mit Ausnahme von positionierte Update- und Löschvorgänge, die für den gleichen Cursor-Cache) erkennen. Dies tritt auf, weil für Aufrufe von **SQLFetchScroll**, die Cursorbibliothek refetches nie Daten aus der Datenquelle. Stattdessen refetches er Daten aus dem Cache.  
  
## <a name="scrolling"></a>Durchführen eines Bildlaufs  
 Die Cursorbibliothek unterstützt die folgenden Typen von Fetch in **SQLFetchScroll**.  
  
|Cursortyp|FETCH-Typen|  
|-----------------|-----------------|  
|Vorwärtscursor|SQL_FETCH_NEXT|  
|STATIC-Cursor|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>Fehler  
 Wenn **SQLFetchScroll** aufgerufen wird und eine der Aufrufe **SQLFetch** gibt SQL_ERROR zurück, der Cursor Library fortgesetzt, die wie folgt. Nach Abschluss dieser Schritte wird die Cursorbibliothek die Verarbeitung fortgesetzt.  
  
1.  Aufrufe **SQLGetDiagRec** zum Abrufen von Fehlerinformationen aus dem Treiber und übermittelt diese als ein Diagnosedatensatz im Treiber-Manager.  
  
2.  Legt das Feld SQL_DIAG_ROW_NUMBER in dem Diagnosedatensatz auf den entsprechenden Wert fest.  
  
3.  Legt das SQL_DIAG_COLUMN_NUMBER-Feld in der Diagnosedatensatz auf den entsprechenden Wert fest, falls zutreffend; Andernfalls wird er auf 0.  
  
4.  Legt den Wert für die Zeile im Fehler in der zeilenstatusarray, SQL_ROW_ERROR fest.  
  
 Nach dem Cursor Library nennt man **SQLFetch** mehrere Male in seiner Implementierung von **SQLFetchScroll**, Fehler oder eine Warnung, die von einem der Aufrufe zum zurückgegebenen **SQLFetch** werden in ein Diagnosedatensatz und abgerufen werden kann, durch den Aufruf von **SQLGetDiagRec**. Wenn die Daten abgeschnitten wurden, wenn es abgerufen wurde, werden die abgeschnittenen Daten nun in der Cursorbibliothek Cache befinden. Nachfolgende Aufrufe **SQLFetchScroll** Bildlauf zu einer Zeile mit abgeschnittene Daten die abgeschnittenen Daten zurück, und keine Warnung wird ausgelöst, da die Daten aus der Cursorbibliothek Cache abgerufen werden. Zum Nachverfolgen die Länge der Daten zurückgegeben, sodass sie ermitteln kann, ob die Daten in einen Puffer abgeschnitten wurde, sollte eine Anwendung die Längen-/Indikatorpuffers binden.  
  
## <a name="bookmark-operations"></a>Bookmark-Vorgänge  
 Die Cursorbibliothek unterstützt Aufrufen **SQLFetchScroll** mit einem *FetchOrientation* von sql_fetch_bookmark auf. Sie unterstützt auch die Angabe eines Offsets in die *FetchOffset* Argument, das in der Lesezeichen-Vorgang verwendet werden kann. Dies ist der einzige Lesezeichen-Vorgang, den die Cursorbibliothek unterstützt. Die Cursorbibliothek unterstützt keine Aufrufen **SQLBulkOperations**.  
  
 Wenn die Anwendung das Anweisungsattribut SQL_ATTR_USE_BOOKMARKS festgelegt wurde und die Lesezeichenspalte gebunden wurde, wird die Cursorbibliothek ein fester Länge Lesezeichen generiert und an die Anwendung zurückgegeben. Die Cursorbibliothek erstellt und verwaltet die Lesezeichen, die verwendet werden. Es verwendet keine Lesezeichen, die in der Datenquelle verwaltet. Wenn **SQLFetchScroll** wird aufgerufen, um einen Block von Daten abzurufen, die bereits aus der Datenquelle abgerufen wurde, die Daten aus dem Cursor Library-Cache abgerufen. Daher verwendet das Lesezeichen in einem Aufruf von **SQLFetchScroll** mit einem *FetchOrientation* von SQL_FETCH_BOOKMARK erstellt und von der Cursorbibliothek verwaltet werden müssen.  
  
## <a name="interaction-with-other-functions"></a>Interaktion mit anderen Funktionen  
 Muss eine Anwendung aufrufen **SQLFetch** oder **SQLFetchScroll** , bevor sie vorbereitet oder ausführt alle positioniert update oder delete-Anweisungen.
