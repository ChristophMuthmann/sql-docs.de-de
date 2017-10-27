---
title: "Haupt-Level-API-Funktionen (ODBC-Treiber für Oracle) | Microsoft Docs"
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
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d3bc36063659da3cf0cd6b2b837be0c4fce46c6f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>Core Level-API-Funktionen (ODBC-Treiber für Oracle)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Funktionen, die auf dieser Ebene bilden die minimale Stufe der Schnittstelle-Konformität für ODBC-Treiber.  
  
|API-Funktion|Hinweise|  
|------------------|-----------|  
|**SQLAllocConnect**|Belegt Speicher für ein Verbindungshandle *Hdbc*, in der Umgebung identifizierten *Henv*. Der Treiber-Manager verarbeitet diese Aufruf und des Treibers ruft **SQLAllocConnect** -Funktion bei jedem **SQLConnect**, **SQLBrowseConnect**, oder ** SQLDriverConnect** aufgerufen wird.|  
|**SQLAllocEnv**|Zeigt das Dialogfeld die Notwendigkeit von Oracle-Clientsoftware angeben, und versetzt dann SQL_NULL_HANDLE. Wenn die Oracle-Clientsoftware nicht installiert ist, diese Funktion weist Speicher für ein Umgebungshandle *Henv*, und die ODBC Call-Level-Interface für die Verwendung durch eine Anwendung initialisiert.|  
|**SQLAllocStmt:**|Belegt Speicher für ein Anweisungshandle, und ordnet das Anweisungshandle von Hdbc angegebene Verbindung. Der Treiber-Manager übergibt diesen Aufruf an den Treiber, der den Speicher für die Struktur des Befehls beschäftigt belegt wird.|  
|**SQLBindCol**|Speicherplatz für eine Ergebnisspalte zugewiesen, und gibt den Typ des Ergebnisses.|  
|**SQLCancel**|Bricht die Verarbeitung auf einem Anweisungshandle Befehls beschäftigt ab. In einigen Fällen lässt Oracle keine Abbruch einer ausgeführten Anweisung. Dies bedeutet, dass eine ausgeführte Anweisung weiterhin Oracle Abschluss des Prozesses, zu diesem Zeitpunkt die Ergebnisse aus der Anweisung durch ODBC-Treiber für Oracle abgebrochen werden.|  
|**SQLColAttributes**|Gibt die Deskriptorinformationen für eine Spalte in einem Resultset zurück. Deskriptorinformationen wird als eine Zeichenfolge, einen 32-Bit-Deskriptor abhängiges-Wert oder einen ganzzahligen Wert zurückgegeben.|  
|**SQLConnect**|Eine Verbindung mit einer Datenquelle. Oracle-Authentifizierung verwenden, geben Sie "/" als die *SzUID* Parameter und "" als die *SzAuthStr* Parameter.|  
|**SQLDescribeCol**|Gibt den Namen, Typ, Genauigkeit, Dezimalstellen und NULL-Zulässigkeit der Spalte angegebenen Ergebnis. **Hinweis:****SQLDescribeCol** meldet berechnete Spalten als SQL_VARCHAR.  |  
|**SQLDisconnect**|Schließt eine Verbindung Wenn Verbindungspooling, für die einer freigegebenen Umgebung aktiviert ist und eine Anwendung ruft **SQLDisconnect** für eine Verbindung in der Umgebung, die Verbindung an den Verbindungspool zurückgegeben und ist weiterhin verfügbar, mit anderen Komponenten verwenden die gleichen freigegebenen Umgebung.|  
|**SQLError**|Fehler oder Status Informationen zu den letzten Fehler zurückgegeben. Der Treiber behält einen Stapel oder eine Liste von Fehlern, die für zurückgegeben werden, können die *Befehls beschäftigt*, *Hdbc*, und *Henv* Argumente, je nachdem, wie der Aufruf von **SQLError ** erfolgt. Die Fehlerwarteschlange wird nach jeder Anweisung geleert. In der Regel ruft eine Oracle-Fehlermeldung ab, und andernfalls leer ist.|  
|**SQLExecDirect**|Führt eine neue, nicht vorbereiteter SQL­Anweisung. Der Treiber verwendet die aktuellen Werte der Variablen Marker Parameter auf, wenn alle Parameter in der Anweisung vorhanden sind. Wenn die Tabelle, Sicht oder Feldnamen Leerzeichen enthalten, schließen Sie die Namen wieder in Anführungszeichen eingeschlossen. Wenn Ihre Datenbank eine Tabelle namens enthält z. B. *Meine Tabelle* und das Feld *mein Feld*, schließen Sie jedes Element des Bezeichners wie folgt:<br /><br /> Wählen Sie \`Meine Tabelle\`. \`Meine "Field1"\`, \`Meine Tabelle\`.\` Meine "Field2"\` FROM \`Meine Tabelle "|  
|**SQLExecute**|Führt eine vorbereitete SQL­Anweisung (eine Anweisung, die bereits vorbereitet, indem **SQLPrepare**). Der Treiber verwendet die aktuellen Werte der Variablen Marker Parameter auf, wenn alle Parameter in der Anweisung vorhanden sind.|  
|**SQLFetch**|Ruft eine Zeile aus einem Resultset in die Speicherorte, die von der vorherigen Aufrufe von angegebenen **SQLBindCol**. Bereitet den Treiber für einen Aufruf **SQLGetData** für ungebundenen Spalten.|  
|**SQLFreeConnect**|Ein Verbindungshandle frei, und alle für das Handle reserviert Speicher freigegeben wird.|  
|**SQLFreeEnv**|Schließt den ODBC-Treiber für Oracle und alle mit dem Treiber zugeordnete Speicherplatz frei.|  
|**SQLFreeStmt**|Beendet die Verarbeitung mit einer bestimmten Befehls beschäftigt verknüpft ist, schließt alle geöffneten Cursor verknüpft ist, mit der Befehls beschäftigt ausstehende Ergebnisse verworfen und optional alle das Anweisungshandle zugeordnete Ressourcen frei.|  
|**SQLGetCursorName**|Gibt den Namen des mit der angegebenen Befehls beschäftigt verknüpften Cursors zurück.|  
|**SQLNumResultCols**|Gibt die Anzahl der Spalten in ein resultsetcursor zurück.|  
|**SQLPrepare**|Bereitet eine SQL-Anweisung durch das Planen der Verwendung zu optimieren, und führen Sie die Anweisung vor. Die SQL-Anweisung kompiliert wird, für die Ausführung von **SQLExecDirect**.<br /><br /> Wenn die Tabelle, Sicht oder Feldnamen Leerzeichen enthalten, schließen Sie die Namen wieder in Anführungszeichen eingeschlossen. Wenn Ihre Datenbank eine Tabelle namens enthält z. B. *Meine Tabelle* und das Feld *mein Feld*, schließen Sie jedes Element des Bezeichners wie folgt:<br /><br /> Wählen Sie \`Meine Tabelle\`.\` Mein Feld\` FROM \`Meine Tabelle "<br /><br /> Informationen zur Verwendung von Resultsets, die Arrays als formalen Parameter auftreten, finden Sie unter [zurückgeben Arrayparameter von gespeicherten Prozeduren](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLRowCount**|Oracle bietet keine Möglichkeit zum Bestimmen der Anzahl von Zeilen in einem Resultset bis nach der letzten Zeile abgerufen werden, sodass – 1 zurückgegeben.|  
|**SQLSetCursorName**|Ein Handle aktive Anweisung ordnet einen Cursornamen *Befehls beschäftigt*.|  
|**SQLSetParam**|Durch SQLBindParameter in ODBC 2 ersetzt. *x*.|  
|**SQLTransact**|Fordert einen Commit oder Rollback-Vorgang für alle aktiven Vorgänge für alle Anweisungshandles (Hstmts) eine Verbindung zugeordnet oder für alle Verbindungen, die das Umgebungshandle zugeordnet *Henv*. Die Transaktion bleibt aktiv, wenn ein Commit im manuellen Modus fehlschlägt, Sie können auswählen, um ein Rollback der Transaktion, oder wiederholen den Commitvorgang. Wenn ein Commitvorgang im Transaktionsmodus für automatische fehlschlägt, wird die Transaktion automatisch zurückgesetzt; die Transaktion darf nicht inaktiv sein.|

