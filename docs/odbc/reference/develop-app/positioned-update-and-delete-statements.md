---
title: Positioniert, Update- und Delete-Anweisungen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: 0eafba50-02c7-46ca-a439-ef3307b935dc
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0c39c0081ee0cd671ee31bd7e11c02a72adc7558
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="positioned-update-and-delete-statements"></a>Positionierte Update- und Delete-Anweisungen
Anwendungen können zu aktualisieren oder löschen Sie die aktuelle Zeile in einem Resultset mit ein positioniertes Update oder delete-Anweisung. Positioniert, Update- und Delete-Anweisungen werden von einigen Datenquellen, aber nicht alle von ihnen unterstützt. Um zu bestimmen, ob eine Datenquelle positioniert unterstützt Update- und-Anweisungen DELETE, eine Anwendung ruft **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ ATTRIBUTES1 oder SQL_STATIC_CURSOR_ATTRIBUTES1 *Infotyp* (je nach Typ des Cursors). Beachten Sie, dass die ODBC-Cursorbibliothek simuliert positioniertes Update und delete-Anweisungen.  
  
 Ein positioniertes Update oder delete-Anweisung, muss die Anwendung erstellen, ein Resultset mit einer **für aktualisieren wählen** Anweisung. Die Syntax dieser Anweisung lautet:  
  
 **Wählen Sie** [**alle** & #124; **DISTINCT**] *Select-Liste*  
  
 **VON** *Tabelle Verweisliste*  
  
 [**, In denen** *Suchbedingung*]  
  
 **FÜR die Aktualisierung der** [*Spaltennamen* [**,** *Spaltennamen*]...]  
  
 Die Anwendung dann positioniert den Cursor auf die Zeile aktualisiert oder gelöscht werden. Können dazu **SQLFetchScroll** zum Abrufen eines Rowsets, die die erforderlichen Zeile enthält und Aufrufen **SQLSetPos** um die Rowset-Cursor in dieser Zeile zu positionieren. Die Anwendung führt dann die positionierte Update- oder Delete-Anweisung auf einer anderen Anweisung als die Anweisung, die das Resultset verwendet wird. Die Syntax dieser Anweisungen lautet:  
  
 **UPDATE** *Tabellenname*  
  
 **Legen Sie** *Spaltenbezeichner* ** = ** {*Ausdruck* & #124; **NULL**}  
  
 [**,** *Spaltenbezeichner* ** = ** {*Ausdruck* & #124; **NULL**}]...  
  
 **WHERE CURRENT OF** *Cursorname*  
  
 **DELETE FROM** *Tabellenname* **WHERE CURRENT OF** *Cursorname*  
  
 Beachten Sie, dass diese Anweisungen ein Cursorname erforderlich ist. Die Anwendung kann entweder einen Cursornamen mit angeben **SQLSetCursorName** vor dem Ausführen der Anweisung, die das Ergebnis erstellt, festgelegt oder die Datenquelle automatisch lassen Generieren eines Cursornamen auf, wenn der Cursor erstellt wird. Im letzteren Fall ruft die Anwendung diese Cursorname für die Verwendung in positionierte Update- und Delete-Anweisungen durch den Aufruf **SQLGetCursorName**.  
  
 Der folgende Code kann beispielsweise einen Benutzer Blättern Sie in der Customers-Tabelle und Kundendatensätze löschen oder aktualisieren die Adressen und Telefonnummern. Sie ruft **SQLSetCursorName** einen Cursornamen angeben, bevor sie das Resultset eines Kunden erstellt und drei Anweisungshandles verwendet: *HstmtCust* für das Resultset *HstmtUpdate* für ein positioniertes Update-Anweisung und *HstmtDelete* für eine positionierte delete-Anweisung. Obwohl der Code separate Variablen an die Parameter in die positionierte Update-Anweisung zu binden konnte, aktualisiert die Rowset-Puffer und bindet die Elemente von diesen Puffern. Auf diese Weise die Rowset-Puffer mit den aktualisierten Daten synchronisiert sind.  
  
```  
#define POSITIONED_UPDATE 100  
#define POSITIONED_DELETE 101  
  
SQLUINTEGER    CustIDArray[10];  
SQLCHAR        NameArray[10][51], AddressArray[10][51],   
               PhoneArray[10][11];  
SQLINTEGER     CustIDIndArray[10], NameLenOrIndArray[10],   
               AddressLenOrIndArray[10],  
               PhoneLenOrIndArray[10];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLHSTMT       hstmtCust, hstmtUpdate, hstmtDelete;  
  
// Set the SQL_ATTR_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmtCust, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmtCust, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]),  
            NameLenOrIndArray);  
SQLBindCol(hstmtCust, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
         AddressLenOrIndArray);  
SQLBindCol(hstmtCust, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Set the cursor name to Cust.  
SQLSetCursorName(hstmtCust, "Cust", SQL_NTS);  
  
// Prepare positioned update and delete statements.  
SQLPrepare(hstmtUpdate,  
   "UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust",  
   SQL_NTS);  
SQLPrepare(hstmtDelete, "DELETE FROM Customers WHERE CURRENT OF Cust", SQL_NTS);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmtCust,  
   "SELECT CustID, Name, Address, Phone FROM Customers FOR UPDATE OF Address, Phone",  
   SQL_NTS);  
  
// Fetch and display the first 10 rows.  
SQLFetchScroll(hstmtCust, SQL_FETCH_NEXT, 0);  
DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray, AddressArray,  
            AddressLenOrIndArray, PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
  
// Call GetAction to get an action and a row number from the user.  
while (GetAction(&Action, &RowNum)) {  
   switch (Action) {  
  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmtCust, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray, PhoneArray,  
                     PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case POSITIONED_UPDATE:  
         // Get the new data and place it in the rowset buffers.  
         GetNewData(AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                     PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Bind the elements of the arrays at position RowNum-1 to the   
         // parameters of the positioned update statement.  
         SQLBindParameter(hstmtUpdate, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           50, 0, AddressArray[RowNum - 1], sizeof(AddressArray[0]),  
                           &AddressLenOrIndArray[RowNum - 1]);  
         SQLBindParameter(hstmtUpdate, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           10, 0, PhoneArray[RowNum - 1], sizeof(PhoneArray[0]),  
                           &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned update statement to update the row.  
         SQLExecute(hstmtUpdate);  
         break;  
  
      case POSITIONED_DELETE:  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned delete statement to delete the row.  
         SQLExecute(hstmtDelete);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmtCust);  
```
