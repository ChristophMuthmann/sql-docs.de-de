---
title: Bookmark-Typen | Microsoft Docs
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
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06f720d61ae8be7b1a2c98ce2c749a4265e630d2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="bookmark-types"></a>Bookmark-Typen
Alle Lesezeichen in ODBC 3.*.x* variabler Länge-Lesezeichen vorliegen. Dadurch wird ein Primärschlüssel oder einen eindeutigen Index einer Tabelle als Lesezeichen verwendet werden zugeordnet. Das Lesezeichen kann auch eine 32-Bit-Wert sein, wie in ODBC 2. verwendet wurde. *x*. Um anzugeben, dass ein Lesezeichen, mit einem Cursor, eine ODBC 3. verwendet wird *.x* Anwendung das Anweisungsattribut SQL_ATTR_USE_BOOKMARK auf SQL_UB_VARIABLE festlegt. Ein Lesezeichen variabler Länge wird automatisch verwendet.  
  
 Eine Anwendung kann Aufrufen **SQLColAttribute** mit der *FieldIdentifier* Argument, die auf SQL_DESC_OCTET_LENGTH festgelegt ist, um die Länge des Lesezeichens zu erhalten. Da ein Lesezeichen variabler Länge einer long-Wert sein kann, sollte eine Anwendung nicht Spalte 0 binden, wenn das Lesezeichen für viele der Zeilen im Rowset verwendet werden.  
  
 Lesezeichen mit fester Länge sind nur für Abwärtskompatibilität unterstützt. Wenn ein ODBC-2. *x* Anwendung arbeiten mit einem ODBC 3.*.x* Treiber ruft **SQLSetStmtOption** SQL_USE_BOOKMARKS auf SQL_UB_ON festlegen möchten, ist es im Treiber-Manager zu SQL_UB_VARIABLE zugeordnet . Ein Lesezeichen variabler Länge wird verwendet, auch wenn nur 32 Bit des Zertifikats aufgefüllt werden. Wenn ein Treiber fester Länge Lesezeichen unterstützt, wird es variabler Länge Lesezeichen unterstützen. Wenn eine ODBC 3.*.x* Anwendung arbeiten mit einer ODBC 2. *X* Treiber ruft **SQLSetStmtAttr** SQL_ATTR_USE_BOOKMARKS auf SQL_UB_VARIABLE festlegen möchten, ist es im Treiber-Manager zu SQL_UB_ON zugeordnet, und ein 32-Bit-Lesezeichen fester Länge verwendet wird. Das SQL_ATTR_FETCH_BOOKMARK_PTR-Anweisungsattribut muss klicken Sie dann auf einem 32-Bit-Lesezeichen verweisen. Wenn das Lesezeichen verwendet z. B. Primärschlüssel als Lesezeichen verwendet werden, der Cursor die tatsächlichen Werte auf 32-Bit-Werte zuordnen muss länger als 32 Bits sind. Es könnten Sie z. B. eine Hashtabelle, die von ihnen erstellt werden. Wenn eine ODBC 3.*.x* Anwendung arbeiten mit einer ODBC 2. *X* Treiber bindet ein Lesezeichen, die Pufferlänge muss 4 sein.
