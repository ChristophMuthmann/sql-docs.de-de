---
title: SQLGetData | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetData function
ms.assetid: 204848be-8787-45b4-816f-a60ac9d56fcf
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7f7b4d844c1ab15d50c15b23981fdc0c0c5d4b2d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdata"></a>SQLGetData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLGetData** wird verwendet, um Resultsetdaten ohne bindende Spaltenwerte abzurufen. **SQLGetData** kann nacheinander aufgerufen werden, auf die gleiche Spalte abzurufenden große Mengen von Daten aus einer Spalte mit einem **Text**, **Ntext**, oder **Image** -Datentyp.  
  
 Es wird nicht vorausgesetzt, dass eine Anwendung Variablen binden muss, um Resultsetdaten abrufen zu können. Die Daten einer beliebigen Spalte abgerufen werden können, aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber mit **SQLGetData**.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt nicht die Verwendung **SQLGetData** zum Abrufen von Daten in beliebigen Spaltenreihenfolge. Alle ungebundene Spalten mit verarbeitet **SQLGetData** benötigen höhere Spaltenordnungszahlen als die gebundenen Spalten im Resultset. Die Anwendung muss die Daten vom niedrigsten nicht gebundenen ordinalen Spaltenwert zum höchsten Spaltenwert verarbeiten. Der Versuch, Daten aus einer Spalte mit einer niedrigeren Ordnungszahl abzurufen, führt zu einem Fehler. Wenn die Anwendung Servercursor zur Ausgabe von Resultsetzeilen verwendet, kann die Anwendung erneut die aktuelle Zeile abrufen und dann den Wert einer Spalte abrufen. Wenn eine Anweisung für den Standardcursor, schreibgeschützte Vorwärtscursor ausgeführt wird, müssen Sie die Anweisung zu sichernden erneut ausführen **SQLGetData**.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber gibt genau die Länge der **Text**, **Ntext**, und **Image** mit abgerufenen Daten **SQLGetData** . Die Anwendung kann stellen gute Verwendung für die *StrLen_or_IndPtr* Parameter zurück, um lange Daten schnell abzurufen.  
  
> [!NOTE]  
>  Für große Werttypen *StrLen_or_IndPtr* SQL_NO_TOTAL zurück, in die Daten abgeschnitten.  
  
## <a name="sqlgetdata-support-for-enhanced-date-and-time-features"></a>SQLGetData-Unterstützung für verbesserte Funktionen für Datum/Uhrzeit  
 Ergebnisspaltenwerte von Datum-/Uhrzeit-Typen werden konvertiert, wie in beschrieben [Konvertierungen von SQL-in C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md).  
  
 Weitere Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgetdata-support-for-large-clr-udts"></a>SQLGetData-Unterstützung für große CLR-UDTs  
 **SQLGetData** unterstützt große CLR-benutzerdefinierte Typen (UDTs). Weitere Informationen finden Sie unter [Large CLR User-Defined Datentypen & #40; ODBC & #41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="example"></a>Beispiel  
  
```  
SQLHDBC     hDbc = NULL;  
SQLHSTMT    hStmt = NULL;  
long        lEmpID;  
PBYTE       pPicture;  
SQLINTEGER  pIndicators[2];  
  
// Get an environment, connection, and so on.  
...  
  
// Get a statement handle and execute a command.  
SQLAllocHandle(SQL_HANDLE_STMT, hDbc, &hStmt);  
  
if (SQLExecDirect(hStmt,  
    (SQLCHAR*) "SELECT EmployeeID, Photo FROM Employees",  
    SQL_NTS) == SQL_ERROR)  
    {  
    // Handle error and return.  
    }  
  
// Retrieve data from row set.  
SQLBindCol(hStmt, 1, SQL_C_LONG, (SQLPOINTER) &lEmpID, sizeof(long),  
    &pIndicators[0]);  
  
while (SQLFetch(hStmt) == SQL_SUCCESS)  
    {  
    cout << "EmployeeID: " << lEmpID << "\n";  
  
    // Call SQLGetData to determine the amount of data that's waiting.  
    if (SQLGetData(hStmt, 2, SQL_C_BINARY, pPicture, 0, &pIndicators[1])  
        == SQL_SUCCESS_WITH_INFO)  
        {  
        cout << "Photo size: " pIndicators[1] << "\n\n";  
  
        // Get all the data at once.  
        pPicture = new BYTE[pIndicators[1]];  
        if (SQLGetData(hStmt, 2, SQL_C_DEFAULT, pPicture,  
            pIndicators[1], &pIndicators[1]) != SQL_SUCCESS)  
            {  
            // Handle error and continue.  
            }  
  
        delete [] pPicture;  
        }  
    else  
        {  
        // Handle error on attempt to get data length.  
        }  
    }  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQLGetData-Funktion](http://go.microsoft.com/fwlink/?LinkId=59350)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
