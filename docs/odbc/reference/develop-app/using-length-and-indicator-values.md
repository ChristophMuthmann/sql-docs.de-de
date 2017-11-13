---
title: "Mit der Länge und Indikatorwerte | Microsoft Docs"
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
- data buffers [ODBC], length
- length/indicator buffers [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 849792f1-cb1e-4bc2-b568-c0aff0b66199
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f615aa92da79c391e84539fdf5cf402d523ab690
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-length-and-indicator-values"></a>Mithilfe der Länge und Indikatorwerte
Die Längen-/Indikatorpuffers wird verwendet, übergeben Sie die Bytelänge der Daten in den Datenpuffer oder einen speziellen Indikator wie z. B. SQL_NULL_DATA gibt an, dass die Daten NULL sind. Abhängig von der Funktion, in der es verwendet wird, wird ein Längen-/Indikatorpuffers definiert, um eine SQLINTEGER oder ein SQLSMALLINT sein. Aus diesem Grund ist ein einzelnes Argument erforderlich, um es zu beschreiben. Dieses Argument enthält die Bytelänge der Daten selbst oder um einen Indikatorwert, wenn Datenpuffer eine nondeferred Eingabepuffer ist. Es wird oft mit dem Namen *StrLen_or_Ind* oder einem ähnlichen Namen. Beispielsweise folgender code ruft **SQLPutData** , übergeben einen Puffer von Daten vollständig; die Bytelänge (*ValueLen*) direkt übergeben wird, da Datenpuffer (*ValuePtr*) ist ein Eingabepuffer.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLen;  
  
// Call local function to place data in ValuePtr. In ValueLen, return the  
// number of bytes of data placed in ValuePtr. If there is not enough  
// data, this will be less than 50.  
FillBuffer(ValuePtr, sizeof(ValuePtr), &ValueLen);  
  
// Call SQLPutData to send the data to the driver.  
SQLPutData(hstmt, ValuePtr, ValueLen);  
```  
  
 Wenn Datenpuffer eine verzögerte Eingabepuffer, eine nondeferred Ausgabepuffer oder einem Ausgabepuffer ist, enthält das Argument die Adresse des Längen-/Indikatorpuffers auf. Es wird oft mit dem Namen *StrLen_or_IndPtr* oder einem ähnlichen Namen. Beispielsweise folgender code ruft **SQLGetData** abzurufenden einen Puffer von Daten; vollständige Länge in Byte an die Anwendung in die Längen-/Indikatorpuffers zurückgegeben wird (*ValueLenOrInd*), ist, dessen Adresse übergeben **SQLGetData** da den entsprechenden Datenpuffer (*ValuePtr*) ist ein nondeferred Ausgabepuffer.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 Es sei denn, sie insbesondere nicht zulässig ist, ein Längenindikator / pufferargument "0" sein (wenn nondeferred Eingabe) oder ein null-Zeiger (wenn Ausgabe- oder Eingabe-verzögerte). Dies verursacht Eingabepuffer wird den Treiber, um die Bytelänge der Daten zu ignorieren. Dies gibt einen Fehler zurück, bei der Übergabe von Daten variabler Länge ist jedoch üblich beim Übergeben von Daten ungleich Null ist, fester Länge, da weder eine Länge noch ein Indikatorwert erforderlich ist. Ausgabepuffer verursacht dies den Treiber nicht die Bytelänge der Daten oder einen Indikatorwert zurückgegeben wird. Dies ist ein Fehler, wenn die Daten, die vom Treiber zurückgegebene NULL ist, ist jedoch üblich beim Abrufen von Daten fester Länge, NULL-Werte zulässt, da weder eine Länge noch ein Indikatorwert erforderlich ist.  
  
 Wie bei der Adresse eines Datenpuffers verzögerte an den Treiber übergeben wird muss die Adresse des verzögerten Längen-/Indikatorpuffers gültig bleiben, bis der Puffer aufgehoben wird.  
  
 Die folgende Länge sind als Längenindikator/Werte gültig:  
  
-   *n*, wobei  *n*  > 0.  
  
-   0.  
  
-   SQL_NTS. Eine Zeichenfolge, die der Treiber in den entsprechenden Datenpuffer gesendet wird, Null-terminierte; Dies ist eine einfache Möglichkeit für C-Programmierer Zeichenfolgen übergeben werden, ohne ihre Bytelänge zu berechnen. Dieser Wert ist gültig, nur, wenn die Anwendung Daten an den Treiber sendet. Wenn der Treiber Daten an die Anwendung zurückgibt, gibt die tatsächliche Bytelänge der Daten immer zurück.  
  
 Die folgenden Werte sind als Längenindikator/Werte gültig. SQL_NULL_DATA wird in das Deskriptorfeld SQL_DESC_INDICATOR_PTR gespeichert. Alle anderen Werte werden in das Deskriptorfeld SQL_DESC_OCTET_LENGTH_PTR gespeichert.  
  
-   SQL_NULL_DATA. Die Daten sind ein NULL-Wert für Daten, und der Wert in den entsprechenden Datenpuffer wird ignoriert. Dieser Wert ist nur für SQL-Daten gesendet oder abgerufen werden, aus dem Treiber zulässig.  
  
-   SQL_DATA_AT_EXEC. Der Datenpuffer enthält keinen Daten. Stattdessen werden die Daten gesendet werden, mit **SQLPutData** , wenn die Anweisung ausgeführt wird oder wenn **SQLBulkOperations** oder **SQLSetPos** aufgerufen wird. Dieser Wert ist nur für SQL-Daten gesendet, um den Treiber zulässig. Weitere Informationen finden Sie unter [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), und [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
-   Ergebnis der SQL_LEN_DATA_AT_EXEC (*Länge*) Makro. Dieser Wert gleicht SQL_DATA_AT_EXEC. Weitere Informationen finden Sie unter [Long-Daten senden](../../../odbc/reference/develop-app/sending-long-data.md).  
  
-   SQL_NO_TOTAL. Der Treiber kann nicht die Anzahl der Bytes der long-Daten weiterhin verfügbar, die in einem Ausgabepuffer zurückgegeben nicht ermittelt werden. Dieser Wert ist nur für SQL-Daten, die abgerufen werden, aus dem Treiber zulässig.  
  
-   SQL_DEFAULT_PARAM. Eine Prozedur ist den Standardwert des input-Parameter in einer Prozedur anstelle des Werts in den entsprechenden Datenpuffer verwenden.  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations** oder **SQLSetPos** ignoriert den Wert im Datenpuffer. Beim Aktualisieren einer Zeile der Daten durch einen Aufruf von **SQLBulkOperations** oder **SQLSetPos** der Spaltenwert nicht geändert wird. Wenn Sie eine neue Zeile mit Daten durch einen Aufruf von einfügen **SQLBulkOperations**, der Spaltenwert auf seinen Standardwert festgelegt ist oder, wenn die Spalte keinen standardmäßig auf NULL.

