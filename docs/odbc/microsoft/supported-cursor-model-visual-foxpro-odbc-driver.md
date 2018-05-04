---
title: Cursormodell (Visual FoxPro-ODBC-Treiber) unterstützt | Microsoft Docs
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
- Visual FoxPro ODBC driver [ODBC], cursors
- cursors [ODBC], Visual FoxPro ODBC driver
- FoxPro ODBC driver [ODBC], cursors
- static cursors [ODBC]
- block cursors [ODBC]
- rowset cursors [ODBC]
ms.assetid: be95bbb2-6886-491e-a5a7-f58028d19c1e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f12ee1bae3ae4b10b546801bf35ebbf370e1eaba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>Unterstützte Cursormodell (Visual FoxPro-ODBC-Treiber)
Der Visual FoxPro-ODBC-Treiber unterstützt sowohl *Block* (*Rowset*) und *statische* Cursor. Statische Cursor werden für alle Treiber unterstützt, die Ebene-1-ODBC-Kompatibilität entspricht. Der Treiber unterstützt keine dynamischen, keysetgesteuerten oder gemischt (keysetgesteuerte und dynamische) Cursor.  
  
 Rufen Sie Ihre Anwendung kann [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) mit einer Option SQL_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY (Blockcursor) oder SQL_CURSOR_STATIC (statische Cursor).  
  
> [!NOTE]  
>  Beim Aufrufen **SQLSetStmtOption** mit der Option SQL_CURSOR_TYPE als SQL_CURSOR_FORWARD_ONLY oder SQL_CURSOR_STATIC, gibt die Funktion mit ein SQLSTATE von 01 s 02 SQL_SUCCESS_WITH_INFO zurück (Optionswert wurde geändert). Der Treiber setzt alle nicht unterstützten Cursor-Modi zu SQL_CURSOR_STATIC.  
  
 Weitere Informationen zu Cursortypen und über **SQLSetStmtOption**, finden Sie unter der [ODBC Programmer's Reference](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="block-cursor"></a>Blockcursor  
 Ein Bildlauf vorwärts, schreibgeschützt zurückgegebene Resultset an den Client, der zum Verwalten von Speicher für die Daten zuständig ist.  
  
## <a name="static-cursor"></a>Statischer Cursor  
 Eine Momentaufnahme eines Datasets, die von der Abfrage definiert. Statische Cursor spiegeln nicht in Echtzeit Änderungen der zugrunde liegenden Daten von anderen Benutzern. Arbeitsspeicherpuffer des Cursors wird von der ODBC-Cursorbibliothek verwaltet, wodurch Bildlauf vorwärts und rückwärts.  
  
## <a name="rowset"></a>Rowset  
 Blöcke von Daten in einem Cursor, die aus einer Datenquelle abgerufene Zeilen darstellt.
