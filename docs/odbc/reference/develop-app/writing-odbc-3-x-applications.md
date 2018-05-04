---
title: Schreiben von ODBC 3.x-Clientanwendungen | Microsoft Docs
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
- application upgrades [ODBC], about upgrading
- ODBC drivers [ODBC], backward compatibility
- upgrading applications [ODBC]
- compatibility [ODBC], upgrading applications
- application upgrades [ODBC]
- upgrading applications [ODBC], about upgrading
- backward compatibility [ODBC], upgrading applications
ms.assetid: 19c54fc5-9dd6-49b6-8c9f-a38961b40a65
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61809072272ae91c32d4780971735c29c53fe977
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="writing-odbc-3x-applications"></a>Schreiben von ODBC 3.x-Anwendungen
Wenn eine ODBC-2. *x* Anwendung wird aktualisiert, um ODBC 3. *X*, sodass Funktionsweise mit ODBC-2 geschrieben werden soll. *X* und 3. *X* Treiber. Die Anwendung soll bedingten Code aus, um die ODBC 3. voll ausnützen integrieren. *x* Funktionen.  
  
 Das Attribut der SQL_ATTR_ODBC_VERSION-Umgebung sollte auf SQL_OV_ODBC2 festgelegt werden. Dadurch wird sichergestellt, dass der Treiber wie einer ODBC 2. verhält *.x* Treiber in Bezug auf die Änderungen, die im Abschnitt beschriebenen [Verhaltensänderungen](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Wenn keines der Features finden Sie im Abschnitt die Anwendung verwenden [Funktionsumfang](../../../odbc/reference/develop-app/new-features.md), bedingter Code sollte verwendet werden, um festzustellen, ob der Treiber eine ODBC-3 ist. *X* oder ODBC 2.*.x* Treiber. Die Anwendung verwendet **SQLGetDiagField** und **SQLGetDiagRec** zum Abrufen von ODBC 3. *X* SQLSTATEs während der Durchführung der Verarbeitung auf die bedingte Codefragmente Fehler. Die folgenden Punkte bezüglich der neuen Funktionalität sollten berücksichtigt werden:  
  
-   Eine Anwendung, die von der Änderung im Verhalten der Rowset-Größe betroffene vorsichtig nicht aufzurufenden **SQLFetch** Wenn die Arraygröße ist größer als 1. Ersetzen Sie diese Anwendungen sollten Aufrufe **SQLExtendedFetch** durch Aufrufe von **SQLSetStmtAttr** SQL_ATTR_ARRAY_STATUS_PTR-Anweisungsattribut festgelegt und **SQLFetchScroll**, sodass sie allgemeine Code aufweisen, die mit den beiden ODBC 3. arbeitet. *x* und ODBC 2. *X* Treiber. Da **SQLSetStmtAttr** mit SQL_ATTR_ROW_ARRAY_SIZE zugeordnet **SQLSetStmtAttr** mit SQL_ROWSET_SIZE setzen ODBC 2. *X* Treiber, Anwendungen können die SQL_ATTR_ROW_ARRAY_SIZE für ihre mehrzeilige Abrufvorgänge einfach setzen.  
  
-   Die meisten Anwendungen, die ein Upgrade durchführen, sind nicht tatsächlich von Änderungen in SQLSTATE-Codes betroffen. Bei Anwendungen, die betroffen sind, können sie mechanische suchen und Ersetzen Sie in den meisten Fällen verwenden die Konvertierungstabelle Fehler im Abschnitt "SQLSTATE-Zuordnungen" ODBC 3. konvertieren. *x* Fehlercodes mit ODBC 2.*.x* Codes. Da die ODBC 3.*.x* -Treiber-Manager führt Zuordnung von ODBC 2. *X* SQLSTATEs ODBC-3. *X* SQLSTATEs diese Anwendungsentwickler benötigen nur die Kontrollkästchen für die ODBC 3. *X* SQLSTATEs und sich keine Sorgen einschließlich ODBC 2. *X* SQLSTATEs in bedingten Code.  
  
-   Wenn eine Anwendung hervorragende Date, Time und Timestamp-Datentypen verwendet, kann die Anwendung selbst werden von einer ODBC 2. deklarieren. *x* Anwendung, und verwenden Sie ihren vorhandenen code anstatt Aufbereitung Code.  
  
 Die Aktualisierung sollte auch die folgenden Schritte umfassen:  
  
-   Rufen Sie **SQLSetEnvAttr** vor dem Zuordnen von eine Verbindung zur SQL_OV_ODBC2 SQL_ATTR_ODBC_VERSION Umgebung Attributs fest.  
  
-   Ersetzen Sie alle Aufrufe **SQLAllocEnv**, **SQLAllocConnect**, oder **SQLAllocStmt:** durch Aufrufe von **SQLAllocHandle** mit dem entsprechenden *HandleType* Argument SQL_HANDLE_ENV auf, SQL_HANDLE_DBC oder SQL_HANDLE_STMT auf.  
  
-   Ersetzen Sie alle Aufrufe **SQLFreeEnv** oder **SQLFreeConnect** durch Aufrufe von **SQLFreeHandle** mit dem entsprechenden *HandleType* Argument der SQL_HANDLE_DBC oder SQL_HANDLE_STMT auf.  
  
-   Ersetzen Sie alle Aufrufe **SQLSetConnectOption** durch Aufrufe von **SQLSetConnectAttr**. Wenn festlegen ein Attribut, dessen Wert eine Zeichenfolge ist, legen Sie die *StringLength* Argument entsprechend. Änderung *Attribut* Argument von SQL_XXXX in SQL_ATTR_XXXX.  
  
-   Ersetzen Sie alle Aufrufe **SQLGetConnectOption** durch Aufrufe von **SQLGetConnectAttr**. Wenn eine Zeichenfolge oder den binary-Attribut zu erhalten, legen Sie *Pufferlänge* mit dem entsprechenden Wert und übergeben Sie eine *StringLength* Argument. Änderung *Attribut* Argument von SQL_XXXX in SQL_ATTR_XXXX.  
  
-   Ersetzen Sie alle Aufrufe **SQLSetStmtOption** durch Aufrufe von **SQLSetStmtAttr**. Wenn festlegen ein Attribut, dessen Wert eine Zeichenfolge ist, legen Sie die *StringLength* Argument entsprechend. Änderung *Attribut* Argument von SQL_XXXX in SQL_ATTR_XXXX.  
  
-   Ersetzen Sie alle Aufrufe **SQLGetStmtOption** durch Aufrufe von **SQLGetStmtAttr**. Wenn eine Zeichenfolge oder den binary-Attribut zu erhalten, legen Sie *Pufferlänge* mit dem entsprechenden Wert und übergeben Sie eine *StringLength* Argument. Änderung *Attribut* Argument von SQL_XXXX in SQL_ATTR_XXXX.  
  
-   Ersetzen Sie alle Aufrufe **SQLTransact** durch Aufrufe von **SQLEndTran**. Wenn der äußersten rechten gültiges Handle in die **SQLTransact** Aufruf ist ein Umgebungshandle eine *HandleType* Argument SQL_HANDLE_ENV sollte verwendet werden, der **SQLEndTran** telefonisch mit die entsprechende *behandeln* Argument. Wenn der äußersten rechten gültiges Handle in Ihre **SQLTransact** Aufruf ist ein Verbindungshandle ein *HandleType* Argument SQL_HANDLE_DBC auf sollte verwendet werden, der **SQLEndTran** telefonisch mit die entsprechende *behandeln* Argument.  
  
-   Ersetzen Sie alle Aufrufe **SQLColAttributes** durch Aufrufe von **SQLColAttribute**. Wenn die *FieldIdentifier* -Argument SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE oder SQL_COLUMN_LENGTH, verändern sich etwas anderes als den Namen der Funktion nicht. Ändern Sie ggf. *FieldIdentifier* aus SQL_COLUMN_XXXX auf SQL_DESC_XXXX. Wenn *FieldIdentifier* SQL_DESC_CONCISE_TYPE ist und der Datentyp ist ein Datetime-Datentyp, wechseln Sie in der entsprechenden ODBC 3.*.x* -Datentyp.  
  
-   Wenn Blockcursor, scrollfähige Cursor oder beides verwenden, geht die Anwendung wie folgt:  
  
    -   Legt die Rowsetgröße Cursortyp und Parallelität mithilfe **SQLSetStmtAttr**.  
  
    -   Aufrufe **SQLSetStmtAttr** festzulegende SQL_ATTR_ROW_STATUS_PTR auf ein Array von statusdatensätzen verweisen.  
  
    -   Aufrufe **SQLSetStmtAttr** festzulegende SQL_ATTR_ROWS_FETCHED_PTR fest, um auf eine SQLINTEGER zu verweisen.  
  
    -   Führt die erforderlichen Bindungen und die SQL-Anweisung ausführt.  
  
    -   Aufrufe **SQLFetchScroll** in einer Schleife, um Zeilen abzurufen, und Navigieren in das Ergebnis festgelegt.  
  
    -   Wenn es durch Lesezeichen abrufen möchte, die Anwendung aufruft, **SQLSetStmtAttr** SQL_ATTR_FETCH_BOOKMARK_PTR einer Variablen festlegen, die das Lesezeichen für die Zeile, die abgerufen werden sollen, und ruft enthält **SQLFetchScroll** mit einem *FetchOrientation* Argument von sql_fetch_bookmark auf.  
  
-   Wenn Sie Arrays von Parametern verwenden, führt die Anwendung Folgendes aus:  
  
    -   Aufrufe **SQLSetStmtAttr** das Attribut verweist SQL_ATTR_PARAMSET_SIZE auf die Größe des Parameterarrays festlegen.  
  
    -   Aufrufe **SQLSetStmtAttr** SQL_ATTR_ROWS_PROCESSED_PTR auf eine interne UDWORD Variable festlegen.  
  
    -   Führt vorbereiten, binden und Vorgänge nach Bedarf ausführen.  
  
    -   Wenn aus irgendeinem Grund (z. B. SQL_NEED_DATA) die Ausführung angehalten wird, kann die "aktuelle" Zeile von Parametern finden es durch Überprüfen der Speicherstelle SQL_ATTR_ROWS_PROCESSED_PTR.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Zuordnen von Ersatzfunktionen für die Abwärtskompatibilität von Anwendungen](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [Aufrufen von SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [Aufrufen von SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [Aufrufen von SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [Cursorbibliotheksvorgänge](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Zuordnen der Informationstypen „Cursor Attributes1“](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
