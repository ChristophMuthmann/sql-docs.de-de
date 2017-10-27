---
title: SQL-Anweisungen, die zur Laufzeit | Microsoft Docs
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
- run time constructed SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], building at run time
ms.assetid: f6554486-d49c-436a-82e3-4c158d26acd8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ccd79048c250c73867752ebaf0b2b7060a6c19b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sql-statements-constructed-at-run-time"></a>SQL-Anweisungen, die zur Laufzeit
Anwendungen, die ad-hoc-Analyse häufig ausführen werden SQL-Anweisungen zur Laufzeit erstellen. Eine Tabelle kann z. B. einen Benutzer die Auswahl von Spalten, aus denen Daten abgerufen zulassen:  
  
```  
// SQL_Statements_Constructed_at_Run_Time.cpp  
#include <windows.h>  
#include <stdio.h>  
#include <sqltypes.h>  
  
int main() {  
   SQLCHAR *Statement = 0, *TableName = 0;  
   SQLCHAR **TableNamesArray, **ColumnNamesArray = 0;  
   BOOL *ColumnSelectedArray = 0;  
   BOOL  CommaNeeded;  
   SQLSMALLINT i = 0, NumColumns = 0;  
  
   // Use SQLTables to build a list of tables (TableNamesArray[]). Let the  
   // user select a table and store the selected table in TableName.  
  
   // Use SQLColumns to build a list of the columns in the selected table  
   // (ColumnNamesArray). Set NumColumns to the number of columns in the  
   // table. Let the user select one or more columns and flag these columns  
   // in ColumnSelectedArray[].  
  
   // Build a SELECT statement from the selected columns.  
   CommaNeeded = FALSE;  
   Statement = (SQLCHAR*)malloc(8);  
   strcpy_s((char*)Statement, 8, "SELECT ");  
  
   for (i = 0 ; i = NumColumns ; i++) {  
      if (ColumnSelectedArray[i]) {  
         if (CommaNeeded)  
            strcat_s((char*)Statement, sizeof(Statement), ",");  
         else  
            CommaNeeded = TRUE;  
         strcat_s((char*)Statement, sizeof(Statement), (char*)ColumnNamesArray[i]);  
      }  
   }  
  
   strcat_s((char*)Statement, 15, " FROM ");  
   // strcat_s((char*)Statement, 100, (char*)TableName);  
  
   // Execute the statement . It will be executed once, do not prepare it.  
   // SQLExecDirect(hstmt, Statement, SQL_NTS);  
}  
```  
  
 Eine andere Klasse von Anwendungen, die SQL-Anweisungen zur Laufzeit häufig erstellt werden Anwendung entwicklungsumgebungen. Die Anweisungen, die sie erstellen sind jedoch hartcodiert in der Anwendung, die sie erstellen, in dem sie in der Regel optimiert und getestet werden können.  
  
 Anwendungen, die SQL-Anweisungen zur Laufzeit konstruiert können enorme Flexibilität für Benutzer bereitstellen. Wie aus dem vorherigen Beispiel angesehen werden kann, wodurch die allgemeine Vorgänge wie das auch nicht unterstützte **, in denen** Klauseln **ORDER BY** -Klauseln oder Joins, Erstellen von SQL-Anweisungen zur Laufzeit ist erheblich komplexer als eine feste Programmierung-Anweisungen. Darüber hinaus ist das Testen von solchen Anwendungen problematisch, da sie eine beliebige Anzahl von SQL-Anweisungen erstellen können.  
  
 Erstellung von SQL-Anweisungen zur Laufzeit ein potenzieller Nachteil ist, dass das dauert wesentlich mehr Zeit, eine Anweisung zu erstellen, als eine hartcodierte-Anweisung verwenden. Glücklicherweise ist dies meist nicht relevant. Solche Anwendungen sind tendenziell Benutzeroberfläche Intensive und die Uhrzeit, an die Anwendung, Erstellen von SQL-Anweisungen ist im Allgemeinen gering im Vergleich zu der Zeit, die der Benutzer zum Eingeben Kriterien benötigt.

