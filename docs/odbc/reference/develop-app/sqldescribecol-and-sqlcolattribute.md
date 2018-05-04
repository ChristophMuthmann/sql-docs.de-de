---
title: SQLDescribeCol und SQLColAttribute | Microsoft Docs
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
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a46107b85766a528fece7968fe812362fddc2de
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol und SQLColAttribute
**SQLDescribeCol** und **SQLColAttribute** werden verwendet, um die resultsetmetadaten abzurufen. Der Unterschied zwischen diesen beiden Funktionen ist, dass **SQLDescribeCol** gibt immer den gleichen fünf Arten von Informationen (einer Spaltenwerts Name, Datentyp, Genauigkeit, Dezimalstellen und NULL-Zulässigkeit), während **SQLColAttribute** gibt ein einzelnes Stück von der Anwendung angeforderten Informationen. Allerdings **SQLColAttribute** zurückgeben eine wesentlich umfassendere Auswahl der Metadaten, einschließlich eines Spaltenwerts Groß-/Kleinschreibung, Größe, aktualisierbarkeit und Suchvorgänge anzeigen können.  
  
 Viele Anwendungen, vor allem solche, die nur Daten anzeigen, erfordern nur die Metadaten, die zurückgegebene **SQLDescribeCol**. Für diese Anwendungen ist es schneller, verwenden Sie **SQLDescribeCol** als **SQLColAttribute** , da die Informationen in einem einzigen Aufruf zurückgegeben wird. Andere Anwendungen, vor allem solche, die Daten zu aktualisieren erfordern die zusätzliche Metadaten zurückgegebenes **SQLColAttribute** und verwendet daher beide Funktionen. Darüber hinaus **SQLColAttribute** unterstützt der Treiber-spezifische Metadaten; Weitere Informationen finden Sie unter [Treiber-spezifische Datentypen, Deskriptor Typen Informationstypen, Diagnosetypen und Attribute](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Eine Anwendung kann die resultsetmetadaten abrufen, zu einem beliebigen Zeitpunkt, nachdem eine Anweisung vorbereitet oder ausgeführt wurde und bevor Sie den Cursor über das Ergebnis Satz geschlossen ist. Nur sehr wenige Anwendungen erfordern Ergebnis Metadaten festgelegt, nachdem die Anweisung vorbereitet ist, und bevor er ausgeführt wird. Wenn möglich, sollten Anwendungen zum Abrufen von Metadaten erst, nachdem die Anweisung ausgeführt wird, da einige Datenquellen können keine Metadaten für vorbereitete Anweisungen zurückgeben und Emulieren von dieser Funktion in der Treiber häufig ein langwieriger Prozess ist, warten. Beispielsweise generiert der Treiber kann ein Resultset von 0 (null) Zeilen durch Ersetzen der **, in denen** -Klausel der eine **auswählen** Anweisung mit der Klausel **WHERE 1 = 2** und Ausführen der ergibt sich folgende Anweisung.  
  
 Metadaten sind häufig teuer, aus der Datenquelle abgerufen werden. Aus diesem Grund sollten Treiber keine Metadaten zwischenspeichern, vom Server abzurufen, und halten, dass es für als der Cursor auf das Resultset geöffnet ist. Darüber hinaus sollten Anwendungen nur die Metadaten anfordern, absolut benötigten.
