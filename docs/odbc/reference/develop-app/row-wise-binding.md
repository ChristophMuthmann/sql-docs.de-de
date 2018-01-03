---
title: Zeilenweise Bindung | Microsoft Docs
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
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4f622cf4-0603-47a1-a48b-944c4ef46364
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4dd3d59875f649c7b797d39fa31ac744457d68ef
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="row-wise-binding"></a>Zeilenweise Bindung
Verwenden die zeilenweise Bindung, eine Anwendung definiert eine Struktur, enthält nur ein oder zwei, oder in einigen Fällen mit drei Elemente für jede Spalte, die für die Daten zurückgegeben werden. Das erste Element enthält den Datenwert und das zweite Element enthält die Längen-/Indikatorpuffers. Indikatoren und Längenwerte können in separaten Puffer gespeichert werden, durch die deskriptorfelder SQL_DESC_INDICATOR_PTR und SQL_DESC_OCTET_LENGTH_PTR auf unterschiedliche Werte festlegen; Wenn dies erfolgt, enthält die Struktur ein drittes Element. Klicken Sie dann die Anwendung weist ein Array dieser Strukturen enthält, die so viele Elemente als Zeilen im Rowset vorhanden sind.  
  
 Die Anwendung die Größe der Struktur, um den Treiber mit der SQL_ATTR_ROW_BIND_TYPE-Anweisungsattribut deklariert und bindet die Adresse jedes Elements im ersten Element des Arrays. Der Treiber kann daher die Adresse der Daten für eine bestimmte Zeile und Spalte als berechnen.  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size)  
```  
  
 Zeilen werden, in denen auf die Größe des Rowsets von 1 nummeriert. (Eine wird von die Nummer der Zeile subtrahiert, da Array-Indizierung in C nullbasiert ist.) Die folgende Abbildung zeigt die Funktionsweise der zeilenbezogenen Bindung. Im Allgemeinen werden nur Spalten, die gebunden werden in der Struktur enthalten. Die Struktur kann Felder enthalten, die unabhängig vom stagingstatus sind, um Spalten zu erhalten. Die Spalten in der Struktur in beliebiger Reihenfolge platziert werden können, jedoch in sequenzieller Reihenfolge aus Gründen der Übersichtlichkeit angezeigt.  
  
 ![Zeigt Zeile &#45; hintergrundprüfung Bindung](../../../odbc/reference/develop-app/media/pr22.gif "pr22")  
  
 Im folgenden Code erstellt z. B. eine Struktur mit Elementen in dem Daten für die Spalten OrderID, Verkäufer und den Status und Länge/Indikatoren für die Spalten Verkäufer und Status zurückgegeben. Belegt 10 dieser Strukturen und bindet sie an die Spalten OrderID, Vertriebsmitarbeiter und Status.  
  
```  
#define ROW_ARRAY_SIZE 10  
  
// Define the ORDERINFO struct and allocate an array of 10 structs.  
typedef struct {  
   SQLUINTEGER   OrderID;  
   SQLINTEGER    OrderIDInd;  
   SQLCHAR       SalesPerson[11];  
   SQLINTEGER    SalesPersonLenOrInd;  
   SQLCHAR       Status[7];  
   SQLINTEGER    StatusLenOrInd;  
} ORDERINFO;  
ORDERINFO OrderInfoArray[ROW_ARRAY_SIZE];  
  
SQLULEN    NumRowsFetched;  
SQLUSMALLINT   RowStatusArray[ROW_ARRAY_SIZE], i;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Specify the size of the structure with the SQL_ATTR_ROW_BIND_TYPE  
// statement attribute. This also declares that row-wise binding will  
// be used. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE  
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement  
// attribute to point to the row status array. Set the  
// SQL_ATTR_ROWS_FETCHED_PTR statement attribute to point to  
// NumRowsFetched.  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, sizeof(ORDERINFO), 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, ROW_ARRAY_SIZE, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROWS_FETCHED_PTR, &NumRowsFetched, 0);  
  
// Bind elements of the first structure in the array to the OrderID,  
// SalesPerson, and Status columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &OrderInfoArray[0].OrderID, 0, &OrderInfoArray[0].OrderIDInd);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, OrderInfoArray[0].SalesPerson,  
            sizeof(OrderInfoArray[0].SalesPerson),  
            &OrderInfoArray[0].SalesPersonLenOrInd);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, OrderInfoArray[0].Status,  
            sizeof(OrderInfoArray[0].Status), &OrderInfoArray[0].StatusLenOrInd);  
  
// Execute a statement to retrieve rows from the Orders table.  
SQLExecDirect(hstmt, "SELECT OrderID, SalesPerson, Status FROM Orders", SQL_NTS);  
  
// Fetch up to the rowset size number of rows at a time. Print the actual  
// number of rows fetched; this number is returned in NumRowsFetched.  
// Check the row status array to print only those rows successfully  
// fetched. Code to check if rc equals SQL_SUCCESS_WITH_INFO or  
// SQL_ERRORnot shown.  
while ((rc = SQLFetchScroll(hstmt,SQL_FETCH_NEXT,0)) != SQL_NO_DATA) {  
   for (i = 0; i < NumRowsFetched; i++) {  
      if (RowStatusArray[i] == SQL_ROW_SUCCESS|| RowStatusArray[i] ==   
         SQL_ROW_SUCCESS_WITH_INFO) {  
         if (OrderInfoArray[i].OrderIDInd == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%d\t", OrderInfoArray[i].OrderID);  
         if (OrderInfoArray[i].SalesPersonLenOrInd == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%s\t", OrderInfoArray[i].SalesPerson);  
         if (OrderInfoArray[i].StatusLenOrInd == SQL_NULL_DATA)  
            printf(" NULL\n");  
         else  
            printf("%s\n", OrderInfoArray[i].Status);  
      }  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
