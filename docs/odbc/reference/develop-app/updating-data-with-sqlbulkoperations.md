---
title: Aktualisieren von Daten mit SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b1acf3d788381f32d892432c0834cc5ee130680
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="updating-data-with-sqlbulkoperations"></a>Aktualisieren von Daten mit SQLBulkOperations
Anwendungen können Vorgänge Bulk Update, Delete, Fetch oder Einfügen auf die zugrunde liegende Tabelle in der Datenquelle mit einem Aufruf von **SQLBulkOperations**. Aufrufen von **SQLBulkOperations** ist eine praktische Alternative zum Erstellen und Ausführen einer SQL-Anweisung. Sie können einen ODBC-Treiber positionierte Updates zu unterstützen, auch wenn die Datenquelle positionierte SQL-Anweisungen nicht unterstützt. Es ist Teil des dem Paradigma vollständige Datenbankzugriff durch Funktionsaufrufe erreichen.  
  
 **SQLBulkOperations** ausgeführt wird, auf das aktuelle Rowset und kann verwendet werden, nur nach einem Aufruf von **SQLFetch** oder **SQLFetchScroll**. Die Anwendung gibt der Zeilen, um zu aktualisieren, löschen oder aktualisieren, indem Sie ihre Lesezeichen Zwischenspeichern. Der Treiber Ruft ab, die neuen Daten für die zu aktualisierenden Zeilen oder die neuen Daten in der zugrunde liegenden Tabelle, aus dem Rowset-Puffer eingefügt werden soll.  
  
 Die Rowsetgröße von zu verwendende **SQLBulkOperations** festgelegt ist, durch den Aufruf von **SQLSetStmtAttr** mit einer *Attribut* Argument des SQL_ATTR_ROW_ARRAY_SIZE. Im Gegensatz zu **SQLSetPos**, die eine neue Rowsetgröße verwendet, nur nach einem Aufruf von **SQLFetch** oder **SQLFetchScroll**, **SQLBulkOperations** verwendet die neue Rowsetgröße nach dem Aufruf von **SQLSetStmtAttr**.  
  
 Da die meisten Interaktion mit relationalen Datenbanken über SQL "oder" erfolgt **SQLBulkOperations** wird nicht unterstützt. Allerdings ein Treiber kann problemlos emulieren sie erstellen und Ausführen einer **UPDATE**, **löschen**, oder **einfügen** Anweisung.  
  
 Um zu bestimmen, welche Vorgänge **SQLBulkOperation** unterstützt werden, eine Anwendung ruft **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR _ATTRIBUTES1 oder SQL_STATIC_CURSOR_ATTRIBUTES1 Informationsoption (je nach Typ des Cursors).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Aktualisieren von Zeilen durch Lesezeichen mit SQLBulkOperations](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Löschen von Zeilen durch Lesezeichen mit SQLBulkOperations](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Einfügen von Zeilen mit SQLBulkOperations](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [Abrufen von Zeilen mit SQLBulkOperations](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
