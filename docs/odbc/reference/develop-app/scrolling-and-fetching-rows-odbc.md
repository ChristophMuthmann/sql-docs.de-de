---
title: Durchführen eines Bildlaufs und das Abrufen von Zeilen (ODBC) | Microsoft Docs
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
helpviewer_keywords:
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 273046a04849b0b1501e2dd4be476c9abb540c5f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="scrolling-and-fetching-rows-odbc"></a>Durchführen eines Bildlaufs und das Abrufen von Zeilen (ODBC)
Wenn Sie einen bildlauffähigen Cursor verwenden, rufen Anwendungen **SQLFetchScroll** , positionieren Sie den Cursor und Fetch-Zeilen. **SQLFetchScroll** relative Bildlauf unterstützt (Weiter, die vor und die Relative *n* Zeilen), absolute Durchführen eines Bildlaufs (First-und last und Zeile *n*), und die Positionierung von Lesezeichen. Die *FetchOrientation* und *FetchOffset* Argumente **SQLFetchScroll** wo Rowsetanbieter, abzurufen, geben Sie wie in den folgenden Diagrammen dargestellt.  
  
 ![Abrufen des nächsten, vor der ersten und letzten Rowsets](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **Abrufen des nächsten, vorherigen, ersten und letzten Rowsets**  
  
 ![Abrufen eines Absolute, Relative und Lesezeichen versehenen Rowsets](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **Abrufen von Absolute, Relative und Lesezeichen versehenen Rowsets**  
  
 **SQLFetchScroll** platziert den Cursor in die angegebene Zeile und gibt die Zeilen im Rowset, beginnend mit dieser Zeile zurück. Wenn das angegebene Schemarowset überschneidet sich mit dem Ende des Resultsets, wird eine partielle Rowset zurückgegeben. Wenn das angegebene Schemarowset Beginn des Ergebnisses überlappt festgelegt ist, wird das erste Rowset im Ergebnis wird in der Regel zurückgegeben; Ausführliche Informationen finden Sie unter der [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) funktionsbeschreibung.  
  
 In einigen Fällen kann die Anwendung soll den Cursor zu positionieren, ohne das Abrufen von Daten. Angenommen, möchten sie testen, ob eine Zeile vorhanden ist, oder nur das Lesezeichen für die Zeile abrufen, ohne andere Daten über das Netzwerk eingebunden. Zu diesem Zweck wird das SQL_ATTR_RETRIEVE_DATA-Anweisungsattribut auf SQL_RD_OFF. Die Variable an die Lesezeichenspalte (sofern vorhanden) gebunden werden unabhängig von der Einstellung dieses Attributs Anweisung immer aktualisiert.  
  
 Nachdem das Rowset abgerufen wurde, kann die Anwendung aufrufen **SQLSetPos** zu einer bestimmten Zeile im Rowset oder aktualisieren Sie Zeilen im Rowset positioniert. Weitere Informationen zur Verwendung von **SQLSetPos**, finden Sie unter [Aktualisieren von Daten mit SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
> [!NOTE]  
>  Durchführen eines Bildlaufs wird in ODBC 2. unterstützt. *x* Treiber durch **SQLExtendedFetch**. Weitere Informationen finden Sie unter [Blockcursor, scrollfähige Cursor und Abwärtskompatibilität](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.
