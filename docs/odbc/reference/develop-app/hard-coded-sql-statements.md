---
title: Hartcodierten SQL-Anweisungen | Microsoft Docs
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
- SQL statements [ODBC], hard-coded
- hard-coded SQL statements [ODBC]
- SQL statements [ODBC], constructing
ms.assetid: e355f5f1-4f1a-4933-8c74-ee73e90d2d19
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 60f0ad180a334c1d4ad08f49057bb5598df22f59
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="hard-coded-sql-statements"></a>Hartcodierten SQL-Anweisungen
Anwendungen, die eine feste Aufgabe, in der Regel ausführen enthalten die hartcodierten SQL-Anweisungen. Beispielsweise kann ein bestellungseingabesystem den folgenden Aufruf Liste offener Aufträge verwenden:  
  
```  
SQLExecDirect(hstmt, "SELECT OrderID FROM Orders WHERE Status = 'OPEN'", SQL_NTS);  
```  
  
 Es gibt mehrere Vorteile in hartcodierten SQL-Anweisungen: sie können getestet werden, wenn die Anwendung geschrieben wird; Sie sind einfacher zu implementieren als Anweisungen zur Laufzeit; und sie die Anwendung vereinfacht.  
  
 Verwenden von Anweisungsparametern und Vorbereiten der Anweisungen bieten auch eine bessere Möglichkeiten zum hartcodierten SQL-Anweisungen verwenden. Nehmen Sie beispielsweise an, dass die Parts-Tabelle die Spalten PartID, Beschreibung und Price enthält. Eine Möglichkeit, eine neue Zeile in dieser Tabelle einfügen erstellt und ausgeführt werden würde eine **einfügen** Anweisung:  
  
```  
#define DESC_LEN 51  
#define STATEMENT_LEN 51  
  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN], Statement[STATEMENT_LEN];  
SQLREAL       Price;  
  
// Set part ID, description, and price.  
GetNewValues(&PartID, Desc, &Price);  
  
// Build INSERT statement.  
sprintf_s(Statement, 100, "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (%d, '%s', %f)", PartID, Desc, Price);  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
```  
  
 Eine noch bessere Möglichkeit wird eine hartcodierte, parametrisierte Anweisung verwenden. Dies hat zwei Vorteile gegenüber einer Anweisung mit hartcodierten Datenwerte. Zunächst ist es einfacher, eine parametrisierte Anweisung zu erstellen, da die Datenwerte in ihren systemeigenen Datentypen, z. B. ganze Zahlen und Gleitkommazahlen, anstatt zu konvertieren in Zeichenfolgen gesendet werden können. Zweitens kann eine solche Anweisung mehr als einmal verwendet werden, einfach durch die Parameterwerte ändern, und es reexecuting; Es ist nicht erforderlich, ihn neu erstellen.  
  
```  
#define DESC_LEN 51  
  
SQLCHAR * Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (?, ?, ?)";  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Set part ID, description, and price.  
GetNewValues(&PartID, Desc, &Price);  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
```  
  
 Vorausgesetzt, dass diese Anweisung ist mehr als einmal ausgeführt werden, können sie für noch höhere Effizienz vorbereitet werden:  
  
```  
#define DESC_LEN 51  
  
SQLCHAR *Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (?, ?, ?)";  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Prepare the INSERT statement.  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Loop to continually get new values and insert them.  
while (GetNewValues(&PartID, Desc, &Price))  
   SQLExecute(hstmt);  
```  
  
 Möglicherweise ist die effizienteste mithilfe die Anweisung zum Erstellen einer Prozedur, die die Anweisung enthält, wie im folgenden Codebeispiel wird gezeigt. Da die Prozedur, die zum Zeitpunkt der Entwicklung erstellt und in der Datenquelle gespeichert, muss er nicht zur Laufzeit darauf vorbereitet sein. Ein Nachteil dieser Methode ist, dass die Syntax zum Erstellen von Prozeduren DBMS-spezifische und Prozeduren müssen separat erstellt werden, für jede DBMS an, auf dem die Anwendung ausgeführt werden soll.  
  
```  
#define DESC_LEN 51  
  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Loop to continually get new values and insert them.  
while (GetNewValues(&PartID, Desc, &Price))  
   SQLExecDirect(hstmt, "{call InsertPart(?, ?, ?)}", SQL_NTS);  
```  
  
 Weitere Informationen zu Parametern, vorbereitete Anweisungen und Prozeduren finden Sie unter [Ausführen einer Anweisung](../../../odbc/reference/develop-app/executing-a-statement.md).

