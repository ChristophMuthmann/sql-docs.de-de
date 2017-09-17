---
title: SQLGetInfo-Support | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], SQLGetInfo
- backward compatibility [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], support
ms.assetid: 57326f57-daba-46b6-b0be-6c97213b9ef1
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb9afa5b40ffa7628e04ee85e5ddc4f752e98935
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinfo-support"></a>SQLGetInfo-Unterstützung
Wenn eine ODBC-2. *x* Anwendung ruft **SQLGetInfo** auf eine ODBC 3.*.x* -Treiber die *Infotyp* Argumente in der folgenden Tabelle unterstützt werden müssen.  
  
|*Infotyp*|Rückgabewert|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0) **Hinweis:** dieses Typs wird nicht als veraltet markiert; die Bitmasken in der Spalte rechts sind veraltet.|Eine SQLINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **ALTER TABLE** Anweisung, die von der Datenquelle unterstützt.<br /><br /> Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:<br /><br /> SQL_AT_DROP_COLUMN = die Fähigkeit zum Löschen von Spalten wird unterstützt. Ob dies führt zu Cascade oder Einschränken von Verhalten ist treiberdefinierten. (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = die Möglichkeit zum Hinzufügen mehrerer Spalten in einer einzelnen ALTER TABLE-Anweisung wird unterstützt. Dieses Bit ist nicht mit anderen SQL_AT_ADD_COLUMN_XXX Bits oder SQL_AT_CONSTRAINT_XXX Bits kombiniert werden. (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> Der Typ der Informationen wurde in ODBC 1.0 eingeführt. Jede Bitmaske ist mit der Version mit der Bezeichnung eingeführt wurde.|Eine SQLINTEGER-Bitmaske, die beim Aufzählen der unterstützten Abrufoptionen Richtung.<br /><br /> Die folgenden Bitmasken werden in Verbindung mit dem Flag verwendet, um zu bestimmen, welche Optionen unterstützt werden:<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|Eine SQLINTEGER-Bitmaske, die die unterstützten Sperre beim Aufzählen der Typen für die *Bestand* Argument in **SQLSetPos**.<br /><br /> Die folgenden Bitmasken werden in Verbindung mit dem Flag verwendet, um zu bestimmen, welche Typen von Sperren unterstützt werden:<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|Ein SQLSMALLINT-Wert, der angibt, der Ebene der ODBC-Konformität.<br /><br /> SQL_OAC_NONE = keine<br /><br /> SQL_OAC_LEVEL1 = Ebene-1 unterstützt<br /><br /> SQL_OAC_LEVEL2 = Ebene-2 unterstützt|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|Ein SQLSMALLINT-Wert, der angibt, SQL-Grammatik, die vom Treiber unterstützt werden. Finden Sie unter [Anhang C: SQL-Grammatik](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) eine Definition der SQL-Übereinstimmungsebenen.<br /><br /> SQL_OSC_MINIMUM = Minimum-Grammatik unterstützt<br /><br /> SQL_OSC_CORE = Core-Grammatik unterstützt<br /><br /> SQL_OSC_EXTENDED = erweiterte-Grammatik unterstützt|  
|SQL_POS_OPERATIONS (ODBC 2.0)|Eine SQLINTEGER-Bitmaske, die beim Aufzählen der unterstützten Vorgänge im **SQLSetPos**.<br /><br /> Die folgenden Bitmasken werden verwendet, in Verbindung mit dem Flag um zu bestimmen, welche Optionen unterstützt werden:<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|Eine SQLINTEGER-Bitmaske, die beim Aufzählen der unterstützten positioniert SQL-Anweisungen.<br /><br /> Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Anweisungen unterstützt werden:<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|Eine SQLINTEGER-Bitmaske, die beim Aufzählen der das Steuerelement Parallelitätsoptionen für Cursor unterstützt.<br /><br /> Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Optionen unterstützt werden:<br /><br /> SQL_SCCO_READ_ONLY = Cursor ist schreibgeschützt. Es sind keine Updates zulässig.<br /><br /> SQL_SCCO_LOCK = Cursor verwendet die niedrigste Ebene von Sperren ausreichend, um sicherzustellen, dass die Zeile aktualisiert werden kann.<br /><br /> SQL_SCCO_OPT_ROWVER = Cursor verwendet Steuerung durch vollständige Parallelität, Vergleichen von Zeilenversionen, z. B. SQLBase ROWID oder Sybase TIMESTAMP.<br /><br /> SQL_SCCO_OPT_VALUES = Cursor verwendet Steuerung durch vollständige Parallelität, Vergleichen von Werten.|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|Eine SQLINTEGER Bitmaske auflisten, ob von einer Anwendung auf eine statische oder keysetgesteuerte Cursor über Änderungen **SQLSetPos** oder positionierte Update- oder Delete-Anweisungen von der Anwendung erkannt werden können.<br /><br /> SQL_SS_ADDITIONS = Added Zeilen sind sichtbar, bis zum Cursor; der Cursor kann auf diese Spalten einen Bildlauf durchführen. In denen diese Zeilen hinzugefügt werden, bis zum Cursor ist Treiber abhängig.<br /><br /> SQL_SS_DELETIONS = der gelöschte Zeilen sind nicht mehr verfügbar, bis zum Cursor und lassen sich nicht auf ein "Loch" in das Resultset; Nachdem der Cursor aus einer gelöschten Zeile einen Bildlauf durchführt, können keine Zeile zurückgegeben.<br /><br /> SQL_SS_UPDATES = Updates von Zeilen sind sichtbar, bis zum Cursor; Wenn der Cursor führt einen Bildlauf aus, und es zu einer aktualisierten Zeile zurückgibt, ist die vom Cursor zurückgegebenen Daten die aktualisierten Daten, nicht die ursprünglichen Daten. Diese Option gilt nur für statische Cursor oder Updates auf keysetgesteuerte Cursor, die die Schlüssel nicht aktualisieren. Diese Option gilt nicht für einen dynamischen Cursor oder im Fall, den Wenn ein Schlüssel in einem gemischten Cursor geändert wird.<br /><br /> Ob eine Anwendung Änderungen an das Resultset von anderen Benutzern, einschließlich anderer Cursor in der gleichen Anwendung erkennen kann, hängt von den Cursortyp ab.|  
  
 Eine ODBC 3.*.x* Anwendung arbeiten mit einem ODBC 3.*.x* Treiber sollte nicht aufrufen **SQLGetInfo** mit der *Infotyp* Argumente beschrieben, der vorangehenden Tabelle, aber die ODBC 3. die zu verwendende*.x* *Infotyp* Argumente, die im folgenden Abschnitt aufgelistet. Es ist keine 1: 1-Entsprechung zwischen *Infotyp* in ODBC 2. verwendeten Argumente.* X* und denen in ODBC 3.*.x*. Eine ODBC 3.*.x* Anwendung arbeiten mit einer ODBC 2..* X* Treiber, andererseits, die zu verwendende der *Infotyp* Argumente zuvor beschrieben.  
  
 Einige der Typen von Informationen in der vorherigen Tabelle sind zugunsten der Cursortypen für Attribute Informationen veraltet. Diese als veraltet markierten Typen SQL_FETCH_DIRECTION, SQL_LOCK_TYPES SQL_POS_OPERATIONS, SQL_POSITIONED_STATEMENTS, SQL_SCROLL_CONCURRENCY und SQL_STATIC_SENSITIVITY werden Informationen aus. Die neue Attribute Cursortypen sind SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2, wobei XXX DYNAMIC, FORWARD_ONLY, KEYSET_DRIVEN oder statische entspricht. Alle neuen Typen gibt der Treiber-Funktionen für eine einzelnes Cursortyp an. Weitere Informationen zu diesen Optionen finden Sie unter der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung.
