---
title: Aktualisieren von Daten mit SQLSetPos | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb89d4a2220c487f2e126b50ecf8cbedd20857cc
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="updating-data-with-sqlsetpos"></a>Aktualisieren von Daten mit SQLSetPos
Anwendungen können aktualisieren oder löschen Sie eine beliebige Zeile im Rowset mit **SQLSetPos**. Aufrufen von **SQLSetPos** ist eine praktische Alternative zum Erstellen und Ausführen einer SQL-Anweisung. Sie können einen ODBC-Treiber positionierte Updates zu unterstützen, auch wenn die Datenquelle positionierte SQL-Anweisungen nicht unterstützt. Es ist Teil des dem Paradigma vollständige Datenbankzugriff durch Funktionsaufrufe erreichen.  
  
 **SQLSetPos** ausgeführt wird, auf das aktuelle Rowset und kann verwendet werden, nur nach einem Aufruf von **SQLFetchScroll**. Die Anwendung gibt die Nummer der Zeile zu aktualisieren, löschen oder einfügen, und ruft der Treiber die neuen Daten für diese Zeile aus dem Rowset-Puffer. **SQLSetPos** kann auch verwendet werden, um eine angegebene Zeile als die aktuelle Zeile festzulegen oder eine bestimmte Zeile im Rowset aus der Datenquelle zu aktualisieren.  
  
 Rowsetgröße wird durch einen Aufruf von **SQLSetStmtAttr** mit einem *Attribut* SQL_ATTR_ROW_ARRAY_SIZE-Argument. **SQLSetPos** verwendet eine neue Rowsetgröße, jedoch nur nach einem Aufruf von **SQLFetch** oder **SQLFetchScroll**. Wenn die Rowsetgröße geändert wird, z. B. **SQLSetPos** wird aufgerufen, und klicken Sie dann **SQLFetch** oder **SQLFetchScroll** aufgerufen wird, und der Aufruf von **SQLSetPos** verwendet die alte Rowsetgröße beim **SQLFetch** oder **SQLFetchScroll** neue Rowsetgröße verwendet.  
  
 Die erste Zeile im Rowset ist die Zeile 1. Die *RowNumber* Argument in **SQLSetPos** muss eine Zeile im Rowset; identifizieren, also muss sein Wert im Bereich zwischen 1 und die Anzahl der zuletzt abgerufenen Zeilen (was u. u. nicht kleiner als der Rowsetgröße). Wenn *RowNumber* gleich 0 ist, der Vorgang gilt für jede Zeile im Rowset.  
  
 Da die meisten Interaktion mit relationalen Datenbanken über SQL "oder" erfolgt **SQLSetPos** wird nicht unterstützt. Allerdings ein Treiber kann problemlos emulieren sie erstellen und Ausführen einer **UPDATE** oder **löschen** Anweisung.  
  
 Um zu bestimmen, welche Vorgänge **SQLSetPos** unterstützt werden, eine Anwendung ruft **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ ATTRIBUTES1 oder SQL_STATIC_CURSOR_ATTRIBUTES1 Informationsoption (je nach Typ des Cursors).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Aktualisieren von Zeilen im Rowset mit SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [Löschen von Zeilen im Rowset mit SQLSetPos](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)

