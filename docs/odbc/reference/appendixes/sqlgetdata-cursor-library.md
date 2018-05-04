---
title: SQLGetData (Cursorbibliothek) | Microsoft Docs
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
helpviewer_keywords:
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2c3e1edf4d37dd49941b5c019d3337eaee5b706
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLGetData** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLGetData**, finden Sie unter [SQLGetData-Funktion](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
 Die Cursorbibliothek implementiert **SQLGetData** indem zuerst ein **wählen** -Anweisung mit einer **, in dem** -Klausel, die in seinem Cache für jede gebundene gespeicherten Werte Listet die Spalte in der aktuellen Zeile. Führt dann die **wählen** Anweisung, um die Zeile und ruft erneut **SQLGetData** im Treiber zum Abrufen der Daten aus der Datenquelle (im Gegensatz zu den Cache).  
  
> [!CAUTION]  
>  Die **, in denen** -Klausel erstellt, indem die Cursorbibliothek zur Identifikation der aktuellen Zeile kann fehlschlagen, um alle Zeilen zu identifizieren, Identifizieren von einer anderen Zeile oder mehr als eine Zeile zu identifizieren. Weitere Informationen finden Sie unter [durchsucht-Anweisungen konstruieren](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Wenn das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE, festgelegt ist **SQLGetData** kann aufgerufen werden, auf die Spalte 0 Lesezeichen Daten zurückgeben.  
  
 Aufrufe von **SQLGetData** unterliegen folgenden Einschränkungen:  
  
-   **SQLGetData** kann nicht für Vorwärtscursor aufgerufen werden.  
  
-   **SQLGetData** kann aufgerufen werden, nur, wenn die folgenden Bedingungen erfüllt sind: eine **wählen** -Anweisung generiert das Resultset; das **wählen** Anweisung enthielt keinen Join ein  **UNION** -Klausel, oder ein **GROUP BY** -Klausel und alle Spalten, die einen Alias oder ein Ausdruck in der Auswahlliste verwendet wurden nicht mit gebundenen **SQLBindCol**.  
  
-   Wenn der Treiber nur eine aktive Anweisung unterstützt, ruft die Cursorbibliothek den Rest des Resultsets, die vor dem Ausführen der **wählen** -Anweisung und der Aufruf **SQLGetData**.
