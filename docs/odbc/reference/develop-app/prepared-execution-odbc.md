---
title: Vorbereitete Ausführung ODBC | Microsoft Docs
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
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e03123e34834033b4c53fb1eb5818f6c78def82
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="prepared-execution-odbc"></a>Die vorbereitete Ausführung ODBC
Die vorbereitete Ausführung ist eine effiziente Möglichkeit, eine Anweisung mehrmals auszuführen. Die Anweisung zuerst kompiliert wird, oder *vorbereitet,* in eines Plans. Der Access-Plan wird dann ausgeführt wird, eine oder mehrere Male zu einem späteren Zeitpunkt. Weitere Informationen zu Access Pläne, finden Sie unter [eine SQL-Anweisung verarbeiten](../../../odbc/reference/processing-a-sql-statement.md).  
  
 Vorbereitete Ausführung häufig vertikale und benutzerdefinierter Anwendungen wird von der gleichen, parametrisierte SQL-Anweisung wiederholt auszuführen. Beispielsweise wird der folgende Code eine Anweisung zum Aktualisieren der Preise verschiedener Teile vorbereitet. Es wird die Anweisung mehrmals mit verschiedenen Parameterwerten jedes Mal ausgeführt.  
  
```  
SQLREAL       Price;  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0, PriceInd = 0;  
  
// Prepare a statement to update salaries in the Employees table.  
SQLPrepare(hstmt, "UPDATE Parts SET Price = ? WHERE PartID = ?", SQL_NTS);  
  
// Bind Price to the parameter for the Price column and PartID to  
// the parameter for the PartID column.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &PartID, 0, &PartIDInd);  
  
// Repeatedly execute the statement.  
while (GetPrice(&PartID, &Price)) {  
   SQLExecute(hstmt);  
}  
```  
  
 Vorbereitete Ausführung ist schneller als eine direkte Ausführung für Anweisungen, die mehr als einmal ausgeführt, in erster Linie verwendet werden, da die Anweisung nur einmal kompiliert wird. direkt ausgeführte Anweisungen werden jedes Mal kompiliert, wenn sie ausgeführt werden. Vorbereitete Ausführung kann auch bereitstellen, dass eine Reduzierung des Netzwerkverkehrs, da der Treiber der Bezeichner für einen Zugriff auf die Datenquelle jedes Mal die Anweisung senden kann, anstatt eine gesamte SQL-Anweisung ausgeführt wird, wenn der Datenquellenzugriff unterstützt Bezeichner planen.  
  
 Die Metadaten für das Resultset nach dem die Anweisung vorbereitet wurde und bevor er ausgeführt wird, kann die Anwendung abrufen. Allerdings Zurückgeben von Metadaten für vorbereitete, nicht ausgeführte Anweisungen ist für einige Treiber teuer und sollte vermieden werden, indem interoperablen Anwendungen ausführen können, wenn möglich. Weitere Informationen finden Sie unter [Ergebnismetadaten festgelegt](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 Die vorbereitete Ausführung sollte nicht für Anwendungen verwendet werden, die nur einmal ausgeführt werden. Für solche Anweisungen ist etwas langsamer als eine direkte Ausführung, da es sich um einen weiteren ODBC-Funktionsaufruf erfordert.  
  
> [!IMPORTANT]  
>  Ein Commit oder Rollback einer Transaktion, entweder durch explizites Aufrufen **SQLEndTran** oder im Autocommit Modus arbeiten, bewirkt, dass einige Datenquellen, um die Zugriffspläne für alle Anweisungen für eine Verbindung zu löschen. Weitere Informationen finden Sie unter der SQL_CURSOR_COMMIT_BEHAVIOR und SQL_CURSOR_ROLLBACK_BEHAVIOR Optionen in der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung.  
  
 Zum Vorbereiten und Ausführen einer Anweisung, die Anwendung:  
  
1.  Aufrufe **SQLPrepare** und übergibt eine Zeichenfolge, die die SQL-Anweisung enthält.  
  
2.  Legt die Werte aller Parameter an. Parameter können vor oder nach der Vorbereitung der Anweisung tatsächlich festgelegt werden. Weitere Informationen finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md)weiter unten in diesem Abschnitt.  
  
3.  Aufrufe **SQLExecute** und führt zusätzliche Verarbeitung, die erforderlich sind, z. B. das Abrufen von Daten.  
  
4.  Wiederholt die Schritte 2 und 3 nach Bedarf.  
  
5.  Wenn **SQLPrepare** aufgerufen wird, wird den Treiber:  
  
    -   Ändert die SQL-Anweisung, um SQL-Grammatik für die Datenquelle zu verwenden, ohne die Anweisung zu analysieren. Dazu gehören, und Ersetzen Sie dabei die Escapesequenzen, die in beschriebenen [in ODBC-Escapesequenzen](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). Die Anwendung kann rufen Sie die geänderte Form einer SQL-Anweisung durch den Aufruf **SQLNativeSql**. Escapesequenzen werden nicht ersetzt, wenn das SQL_ATTR_NOSCAN-Anweisungsattribut festgelegt ist.  
  
    -   Sendet die Anweisung mit der Datenquelle für die Vorbereitung.  
  
    -   Der Bezeichner für den zurückgegebenen Zugriff zur späteren Ausführung speichert, (wenn es sich bei die Vorbereitung erfolgreich war) oder Fehler (sofern es sich um eine die Vorbereitung nicht erfüllt) zurück. Zu diesen Fehlern zählen syntaktische Fehler wie z. B. SQLSTATE 42000 (Syntaxfehler oder zugriffsverletzung) und semantische Fehler, z. B. SQLSTATE 42S02 (Basis Tabelle oder-Sicht wurde nicht gefunden).  
  
        > [!NOTE]  
        >  Einige Treiber Fehler an diesem Punkt zurückgeben, sondern stattdessen bei der Ausführung der Anweisung oder beim Aufrufen von Katalogfunktionen zurückzugeben. Folglich **SQLPrepare** scheinen keine erfolgreich ausgeführt wurden, wenn in der Tat es fehlgeschlagen ist.  
  
6.  Wenn **SQLExecute** aufgerufen wird, wird den Treiber:  
  
    -   Ruft die aktuellen Parameterwerte ab und konvertiert sie nach Bedarf. Weitere Informationen finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md)weiter unten in diesem Abschnitt.  
  
    -   Sendet die Bezeichner für den Zugriff und die konvertierten Parameterwerte an die Datenquelle an.  
  
    -   Gibt Fehlermeldungen zurück. Hierbei handelt es sich um in der Regel zur Laufzeit Fehler wie z. B. SQLSTATE 24000 (Ungültiger Cursorstatus). Allerdings einige Treiber syntaktische und semantische Fehler zurück zu diesem Zeitpunkt.  
  
 Wenn die Datenquelle die Vorbereitung der Anweisung nicht unterstützt, muss der Treiber im größtmöglichen emulieren. Z. B. der Treiber möglicherweise keine beim **SQLPrepare** wird aufgerufen, und führen Sie dann die direkte Ausführung der Anweisung beim **SQLExecute** aufgerufen wird.  
  
 Wenn die Datenquelle ohne Ausführung überprüft die Syntax unterstützt, kann der Treiber die Anweisung für die Überprüfung beim Übermitteln **SQLPrepare** wird aufgerufen, und senden Sie die Anweisung für die Ausführung beim **SQLExecute** ist wird aufgerufen.  
  
 Wenn der Treiber anweisungsvorbereitung emulieren nicht möglich, speichert Sie die Anweisung beim **SQLPrepare** aufgerufen wird, und übergibt sie zur Ausführung beim **SQLExecute** aufgerufen wird.  
  
 Da "emuliert" anweisungsvorbereitung nicht perfekt, **SQLExecute** kann normalerweise zurückgegebene Fehler zurückgeben **SQLPrepare**.
