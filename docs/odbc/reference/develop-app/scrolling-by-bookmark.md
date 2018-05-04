---
title: Durchführen eines Bildlaufs durch Lesezeichen | Microsoft Docs
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
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 823929a98b3fc7b016f8bc1dc3fa1c2ed982b9c0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="scrolling-by-bookmark"></a>Durchführen eines Bildlaufs durch Lesezeichen
Beim Abrufen von Zeilen mit **SQLFetchScroll**, eine Anwendung kann einem Lesezeichen als Basis für die Auswahl der Startzeile verwenden. Dies ist eine Form der absoluten Adressierung, da sie nicht von der aktuellen Cursorposition abhängt. Um einen Bildlauf zu einer Lesezeichen versehenen Zeile, die Anwendung ruft **SQLFetchScroll** mit einem *FetchOrientation* von sql_fetch_bookmark auf. Dieser Vorgang verwendet das Lesezeichen, das das SQL_ATTR_FETCH_BOOKMARK_PTR-Anweisungsattribut verweist. Es gibt das Rowset zurück, das mit der Zeile beginnt, die von diesem Lesezeichen identifiziert wird. Eine Anwendung kann einen Offset für diesen Vorgang im Angeben der *FetchOffset* Argument des Aufrufs von **SQLFetchScroll**. Wenn ein Offset angegeben wird, wird die erste Zeile des zurückgegebenen Rowsets durch Hinzufügen der Zahl in bestimmt die *FetchOffset* Argument für die Anzahl der Zeilen, die vom Lesezeichen identifiziert. Diese Verwendung von der *FetchOffset* Argument wird nicht unterstützt, bei der Verwendung mit ODBC 2. *X* Treiber; Wenn eine Anwendung ruft **SQLFetchScroll** in einer ODBC 2. *X* Treiber mit *FetchOrientation* festgelegt sql_fetch_bookmark auf, die *FetchOffset* Argument muss auf 0 festgelegt werden.
