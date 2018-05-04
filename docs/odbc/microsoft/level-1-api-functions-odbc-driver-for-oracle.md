---
title: Ebene-1-API-Funktionen (ODBC-Treiber für Oracle) | Microsoft Docs
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
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e4329f1dc0a22c9bcea27df908bb0ce567fdca7c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>Ebene-1-API-Funktionen (ODBC-Treiber für Oracle)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Auf dieser Ebene bieten Core Schnittstelle Konformität Funktionen sowie zusätzliche Funktionen wie z. B. Transaktionen unterstützen.  
  
|API-Funktion|Hinweise|  
|------------------|-----------|  
|**SQLColumns**|Erstellt ein Resultset für eine Tabelle, also der Spaltenliste für die angegebene Tabelle oder Tabellen. Wenn Sie Spalten für eine öffentliche Synonym anfordern, muss das Verbindungsattribut SYNONYMCOLUMNS festgelegt und als eine leere Zeichenfolge angegeben die *SzTableOwner* Argument. Beim Zurückgeben von Spalten für Öffentliche Synonyme, legt der Treiber die TABELLENNAMEN-Spalte auf eine leere Zeichenfolge. Das Resultset enthält eine zusätzliche Spalte mit der ORDNUNGSZAHL POSITION am Ende jeder Zeile. Dieser Wert ist die Ordnungsposition der Spalte in der Tabelle.|  
|**SQLDriverConnect**|Eine Verbindung mit einer vorhandenen Datenquelle. Weitere Informationen finden Sie unter [Verbindungszeichenfolgenformat und Attribute](../../odbc/microsoft/connection-string-format-and-attributes.md).|  
|**SQLGetConnectOption**|Gibt die aktuelle Einstellung der eine Verbindungsoption fest. Diese Funktion wird teilweise unterstützt. Der Treiber unterstützt alle Werte für die *fOption* Argument, aber einige unterstützt *vParam* Werte für die *fOption* Argument [SQL_TXN_ISOLATION ](../../odbc/microsoft/connect-options.md). Weitere Informationen finden Sie unter [verbinden Optionen](../../odbc/microsoft/connect-options.md).|  
|**SQLGetData**|Ruft den Wert von einem einzelnen Feld im aktuellen Datensatz des angegebenen Resultsets ab.|  
|**SQLGetFunctions**|Gibt "true" für alle unterstützten Funktionen. Implementiert die vom Treiber-Manager.|  
|**SQLGetInfo**|Gibt Informationen, einschließlich SQLHDBC, SQLUSMALLINT SQLPOINTER, SQLSMALLINT und SQLSMALLINT \*, zum ODBC-Treiber für Oracle und der Datenquelle ein Verbindungshandle zugeordneten *Hdbc*.|  
|**SQLGetStmtOption**|Gibt die aktuelle Einstellung der Option-Anweisung eine zurück. Weitere Informationen finden Sie unter [Anweisungsoptionen](../../odbc/microsoft/statement-options.md).|  
|**SQLGetTypeInfo**|Gibt Informationen zu den Datentypen, die von einer Datenquelle unterstützt. Der Treiber zurückgegeben die Informationen in einem SQL-Resultset.|  
|**SQLParamData**|Wird in Verbindung mit **SQLPutData** Parameterdaten während der Ausführung der Anweisung an.|  
|**SQLPutData**|Ermöglicht einer Anwendung zum Senden von Daten für einen Parameter oder eine Spalte an den Treiber während der Ausführung der Anweisung.|  
|**SQLSetConnectOption**|Bietet Zugriff auf Optionen, die Aspekte der Verbindung zu steuern. Diese Funktion wird teilweise unterstützt: der Treiber unterstützt alle Werte für die *fOption* Argument, aber einige nicht unterstützt *vParam* Werte für die *fOption* Argument [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). Weitere Informationen finden Sie unter [verbinden Optionen](../../odbc/microsoft/connect-options.md).|  
|**SQLSetStmtOption**|Legt fest, die im Zusammenhang mit einem Anweisungshandle *Befehls beschäftigt*. Weitere Informationen finden Sie unter [Anweisungsoptionen](../../odbc/microsoft/statement-options.md).|  
|**SQLSpecialColumns**|Ruft ab, die optimale Gruppe von Spalten, die eine Zeile in der Tabelle eindeutig identifiziert.|  
|**SQLStatistics**|Ruft eine Liste von Statistiken über eine einzelne Tabelle und die Indizes oder die Tag-Namen der Tabelle zugeordnet. Der Treiber gibt zurück, die Informationen als ein Resultset.|  
|**SQLTables**|Gibt die Liste der Tabellennamen angegeben durch den Parameter in der **SQLTables** Anweisung. Wenn kein Parameter angegeben wird, gibt die Namen der Tabellen in der aktuellen Datenquelle gespeichert. Der Treiber gibt zurück, die Informationen als ein Resultset.<br /><br /> Enumeration Typs ruft werden einen Ergebnis Set-Eintrag für remote-Ansichten oder lokalen parametrisierte Sichten nicht empfangen. Allerdings einen Aufruf von **SQLTables** durch eine eindeutige Tabelle namenspezifizierer findet eine Entsprechung für eine Sicht angefordertes mit diesem Namen; Dadurch wird die API für Namenskonflikte vor der Erstellung einer neuen Tabelle überprüfen.<br /><br /> Öffentliche Synonyme werden zurückgegeben, mit dem TABLE_OWNER Wert "".<br /><br /> Ansichten, die im Besitz von SYS oder SYSTEM werden als SYSTEMSICHT identifiziert.|
