---
title: "Level-2-API-Funktionen (ODBC-Treiber für Oracle) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb35e0e2dde90261e913ffd9ba3dc28e5859e012
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>Level-2-API-Funktionen (ODBC-Treiber für Oracle)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Funktionen, die auf dieser Ebene bieten Schnittstelle-Konformität für Ebene 1 plus zusätzliche Funktionen wie z. B. Unterstützung für Lesezeichen, die dynamischen Parameter und die asynchrone Ausführung der ODBC-Funktionen.  
  
|API-Funktion|Hinweise|  
|------------------|-----------|  
|**SQLBindParameter**|Ordnet einen Puffer mit einer parametermarkierung in einer SQL­Anweisung.|  
|**SQLBrowseConnect**|Gibt die aufeinander folgenden Ebenen der Attribute und Attributwerte.|  
|**SQLDataSources**|Listet die Datenquellennamen. Implementiert die vom Treiber-Manager.|  
|**SQLDescribeParam**|Gibt die Beschreibung des eine parametermarkierung eine vorbereitete SQL­Anweisung zugeordnet.<br /><br /> Gibt eine Schätzung der welche der Parameter ist, basierend auf die Anweisung analysieren, zurück. Wenn der Parametertyp kann nicht bestimmt werden, gibt SQL_VARCHAR mit Länge 2000 zurück.|  
|**SQLDrivers**|Implementiert die vom Treiber-Manager.|  
|**SQLExtendedFetch**|Ähnlich wie **SQLFetch** jedoch mehrere Zeilen mit einem Array für jede Spalte zurückgegeben. Das Resultset ist Forward bildlauffähige und rückwärts bildlauffähige, wenn der Cursor definiert ist, werden statische, nicht Vorwärtscursor vorgenommen werden kann. Für Vorwärtscursor mit der standardbindung für die Spalte werden die Spaltendaten aus Datasets, die größer als das Verbindungsattribut BUFFERSIZE direkt in Datenpuffer abgerufen. Unterstützt keine Lesezeichen variabler Länge und Abrufen eines Rowsets mit einem Offset (ungleich 0) in einem Lesezeichen nicht unterstützt.|  
|**SQLForeignKeys**|Gibt eine Liste von Fremdschlüsseln in einer einzelnen Tabelle oder eine Liste von Fremdschlüsseln in anderen Tabellen, die auf einer einzelnen Tabelle verweisen.|  
|**SQLMoreResults**|Bestimmt, ob weitere Ergebnisse ausstehen, die für ein Anweisungshandle Befehls beschäftigt, SELECT, UPDATE, INSERT oder DELETE-Anweisungen enthält, und wenn dies der Fall ist, initialisiert die Verarbeitung für diese Ergebnisse.<br /><br /> Oracle unterstützt mehrere Resultsets nur über gespeicherte Prozeduren beim {Resultset...} Escape-Sequenzen.|  
|**SQLNativeSql**|Informationen zur Verwendung finden Sie unter [zurückgeben Arrayparameter von gespeicherten Prozeduren](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLNumParams**|Gibt die Anzahl von Parametern in einer SQL-Anweisung zurück. Die Anzahl der Parameter sollte die Anzahl der Fragezeichen in der SQL-Anweisung übergeben, um gleich **SQLPrepare**.|  
|**SQLPrimaryKeys**|Gibt die Spaltennamen, die den Primärschlüssel für eine Tabelle bilden.|  
|**SQLProcedureColumns**|Gibt eine Liste der Input und Output-Parameter, der Rückgabewert, die Spalten im Resultset einer einzelnen Prozedur und zwei zusätzliche Spalten ÜBERLADUNG und ORDINAL_POSITION zurück. ÜBERLADUNG ist die ÜBERLADUNG Spalte aus der Tabelle ALL_ARGUMENTS der Oracle-Wörterbuch an. ORDINAL_POSITION ist der SEQUENCE-Spalte aus der Tabelle ALL_ARGUMENTS der Oracle-Wörterbuch an. Für App-Pakete Prozeduren den PROZEDURNAMEN Spalte befindet sich im *packagename.procedurename* Format. Die Prozedur Spalten eines Synonyms erstellt, der auf eine Prozedur oder Funktion verweist, werden nicht zurückgegeben werden.|  
|**SQLProcedures**|Gibt eine Liste der Verfahren in der Datenquelle zurück. Für App-Pakete Prozeduren den PROZEDURNAMEN Spalte befindet sich im *packagename.procedurename* Format.<br /><br /> Da Oracle eine Möglichkeit, Paketfunktionen gepackte Prozeduren unterscheiden nicht bereitstellt, kehrt der Treiber SQL_PT_UNKNOWN für die Spalte PROCEDURE_TYPE zurück.|  
|**SQLSetPos**|Legt die Cursorposition in einem Rowset. Sie können **SQLSetPos** mit **SQLGetData** zum Abrufen von Zeilen aus ungebundene Spalten nach dem Positionieren des Cursors an einer bestimmten Zeile im Rowset. Das Resultset mit hinzugefügten Zeilen *fOption* SQL_ADD werden hinzugefügt, nachdem die letzte Zeile im Resultset.|  
|**SQLSetScrollOptions**|Legt Optionen für die Steuerung des Verhaltens von Cursor ein Anweisungshandle Befehls beschäftigt zugeordnet. Weitere Informationen finden Sie unter [Cursortyp und Parallelität Kombinationen](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|

