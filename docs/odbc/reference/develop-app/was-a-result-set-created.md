---
title: Wurde ein Resultset erstellt? | Microsoft-Dokumentation
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
- result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 213fa7b4c8a46966fa7054c6c20fbf79c5896d74
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="was-a-result-set-created"></a>Wurde ein Resultset erstellt?
In den meisten Fällen wissen Anwendungsprogrammierer an, ob die Anweisungen, die ihre Anwendung ausgeführt wird, ein Resultset erstellt werden. Dies ist der Fall, wenn die Anwendung hartcodiert SQL-Anweisungen durch den Programmierer verwendet. Es ist normalerweise der Fall, wenn die Anwendung SQL-Anweisungen zur Laufzeit erstellt: der Programmierer kann problemlos Code enthalten, der kennzeichnet, ob eine **wählen** Anweisung oder ein **einfügen** Anweisung wird erstellt. In einigen Situationen kann nicht der Programmierer wissen, ob eine Anweisung ein Resultset erstellt. Dies ist "true", wenn die Anwendung bietet eine Möglichkeit für den Benutzer zur Eingabe und eine SQL­Anweisung ausführen. Es ist auch "true", wenn die Anwendung eine Anweisung zur Laufzeit zum Ausführen einer Prozedur erstellt wird.  
  
 In solchen Fällen wird die Anwendung aufruft, **SQLNumResultCols** bestimmt die Anzahl der Spalten im Resultset. Wenn dies 0 ist, die Anweisung ein Resultset; nicht erstellt werden Wenn sie jede andere Zahl ist, hat die Anweisung ein Resultset erstellt.  
  
 Die Anwendung kann Aufrufen **SQLNumResultCols** jederzeit nach der Anweisung vorbereitet oder ausgeführt wird. Jedoch, da das Resultset mit Vorwärtscursor problemlos einige Datenquellen beschreiben können nicht durch die vorbereiteten Anweisungen erstellte Leistung wird beeinträchtigt werden, wenn **SQLNumResultCols** wird aufgerufen, nachdem eine Anweisung vorbereitet wurde, aber bevor er ausgeführt wird.  
  
 Einige Datenquellen unterstützen auch das Bestimmen der Anzahl von Zeilen, die eine SQL-Anweisung in einem Resultset zurückgibt. Ruft die Anwendung dazu **SQLRowCount**. Genau wie die Anzahl der Zeilen darstellt wird, wenn die Einstellung der Option "SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 oder SQL_STATIC_CURSOR_ATTRIBUTES2" (je nach Typ des Cursors) angegeben werden. durch einen Aufruf zurückgegebene **SQLGetInfo**. Bitmaske für jeden Cursortyp gibt an, ob die Anzahl der Zeilen zurückgegeben, exakten, ungefähren wird, oder es ist gar nicht verfügbar. Ob die Zeilenanzahl für statische oder keysetgesteuerte Cursor werden von vorgenommenen Änderungen betroffen **SQLBulkOperations** oder **SQLSetPos**, oder durch positionierte Update- oder Delete-Anweisungen, abhängig von anderen Bits von den gleichen Option-Argumenten, die zuvor genannten zurückgegeben. Weitere Informationen finden Sie unter der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung.
