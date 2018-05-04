---
title: Katalogfunktionen in ODBC | Microsoft Docs
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
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7297b87ec5ce8bdbf706fa35b5ebef6ba580a49e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="catalog-functions-in-odbc"></a>In ODBC-Katalogfunktionen
ODBC enthält die folgenden Katalogfunktionen:  
  
|Funktion|Description|  
|--------------|-----------------|  
|**SQLTables**|Gibt eine Liste der Kataloge, Schemas, Tabellen und Tabellentypen in der Datenquelle zurück.|  
|**SQLColumns**|Gibt eine Liste der Spalten in einer oder mehreren Tabellen zurück.|  
|**SQLStatistics**|Gibt eine Liste der Statistiken zu einer einzelnen Tabelle zurück. Außerdem gibt eine Liste der Indizes dieser Tabelle zugeordnet.|  
|**SQLSpecialColumns**|Gibt eine Liste der Spalten, die eine Zeile in einer einzelnen Tabelle eindeutig identifiziert. Außerdem gibt eine Liste der Spalten in dieser Tabelle, die automatisch aktualisiert werden.|  
|**SQLPrimaryKeys**|Gibt eine Liste der Spalten, die den Primärschlüssel einer Tabelle zu erstellen.|  
|**SQLForeignKeys**|Gibt eine Liste von Fremdschlüsseln in einer einzelnen Tabelle oder eine Liste von Fremdschlüsseln in anderen Tabellen, die auf einer einzelnen Tabelle verweisen.|  
|**SQLTablePrivileges**|Gibt eine Liste von Berechtigungen, die einer oder mehreren Tabellen zugeordnet.|  
|**SQLColumnPrivileges**|Gibt eine Liste von Berechtigungen, die eine oder mehrere Spalten in einer einzelnen Tabelle zugeordnet.|  
|**SQLProcedures**|Gibt eine Liste der Verfahren in der Datenquelle zurück.|  
|**SQLProcedureColumns**|Gibt eine Liste der Eingabe-und Ausgabeparameter, der Rückgabewert und die Spalten im Resultset einer einzelnen Prozedur zurück.|  
|**SQLGetTypeInfo**|Gibt eine Liste der SQL-Datentypen, die von der Datenquelle unterstützt. Diese Datentypen werden in der Regel verwendet, **CREATE TABLE** und **ALTER TABLE** Anweisungen.|  
  
 Da **SQLTables**, **SQLColumns**, **SQLStatistics**, und **SQLSpecialColumns** entsprechen der Open Group-CLI und **SQLGetTypeInfo** entspricht dem ISO-92-CLI, die sie von den meisten-Treibern implementiert werden. Die verbleibenden Katalogfunktionen sind in der ODBC-Konformitätsgrad.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Daten, die von Katalogfunktionen zurückgegeben werden](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [Argumente in Katalogfunktionen](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [Schemaansichten](../../../odbc/reference/develop-app/schema-views.md)
