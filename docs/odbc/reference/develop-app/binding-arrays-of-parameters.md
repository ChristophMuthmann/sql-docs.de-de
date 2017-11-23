---
title: Binden von Arrays von Parametern | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- binding parameter arrays [ODBC]
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 037afe23-052d-4f3a-8aa7-45302b199ad0
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1964e0ee9903ee673eae3a4cd9710defd40d054f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="binding-arrays-of-parameters"></a>Binden von Arrays von Parametern
Anwendungen, die Arrays von Parametern verwenden, binden die Arrays an die Parameter in der SQL-Anweisung. Es gibt zwei Bindung Formate ein:  
  
-   Binden Sie ein Array an jeden Parameter. Jede Data-Struktur (Array) enthält alle Daten für einen einzelnen Parameter. Hierbei spricht *spaltenbezogene Bindungen* weil sie eine Spalte mit Werten für einen einzelnen Parameter gebunden.  
  
-   Definieren Sie eine Struktur zum Speichern der Parameterdaten für einen ganzen Satz von Parametern und ein Array dieser Strukturen binden. Jede Data-Struktur enthält die Daten für eine einzelne SQL-Anweisung. Hierbei spricht *zeilenbezogene Bindungen* , da es eine Zeile der Parameter bindet.  
  
 Wie bei die Anwendung einzelne Variablen Parameter gebunden wird, ruft **SQLBindParameter** Arrays an Parameter gebunden. Der einzige Unterschied ist, dass die Adressen übergebene Array Adressen, nicht einzelne Variablen Adressen. Die Anwendung legt die SQL_ATTR_PARAM_BIND_TYPE-Anweisungsattribut, um anzugeben, ob es mit spaltenweise (Standard) oder zeilenbezogene Bindung ist. Angibt, ob das spaltenweise oder zeilenweise Binden verwendet, ist weitgehend Anwendung Voreinstellung. Je nachdem, wie der Prozessor Speicherzugriffe möglicherweise zeilenbezogene Bindungen schneller. Die Abweichung ist jedoch wahrscheinlich mit Ausnahme von sehr großen Anzahl von Zeilen der Parameter vernachlässigbar sein.  
  
## <a name="column-wise-binding"></a>Spaltenweises binden  
 Wenn Sie spaltenbezogene Bindungen verwenden, bindet eine Anwendung einem bzw. zwei Arrays an jeden Parameter, für die Daten bereitgestellt werden. Das erste Array enthält die Datenwerte und das zweite Array enthält Längenindikator/Puffer. Jedes Array enthält, so viele Elemente wie Werte für den Parameter vorhanden sind.  
  
 Die spaltenweise Bindung ist die Standardeinstellung. Die Anwendung kann über zeilenbezogene Bindungen auch spaltenbezogene Bindung ändern, indem SQL_ATTR_PARAM_BIND_TYPE-Anweisungsattribut festlegen verwendet wird. Die folgende Abbildung zeigt die Funktionsweise der spaltenbezogenen Bindung.  
  
 ![Zeigt, wie Spalte &#45; hintergrundprüfung Bindung Works](../../../odbc/reference/develop-app/media/pr31.gif "pr31")  
  
 Beispielsweise der folgende Code bindet 10 Elemente umfassende Arrays Parameter für die Spalten PartID, Beschreibung und den Preis und führt eine Anweisung zum Einfügen von 10 Zeilen. Er verwendet spaltenbezogene Bindungen.  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
                                                "VALUES (?, ?, ?)";  
SQLUINTEGER    PartIDArray[ARRAY_SIZE];  
SQLCHAR        DescArray[ARRAY_SIZE][DESC_LEN];  
SQLREAL        PriceArray[ARRAY_SIZE];  
SQLINTEGER     PartIDIndArray[ARRAY_SIZE], DescLenOrIndArray[ARRAY_SIZE],  
               PriceIndArray[ARRAY_SIZE];  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
memset(DescLenOrIndArray, 0, sizeof(DescLenOrIndArray);  
memset(PartIDIndArray, 0, sizeof(PartIDIndArray);  
memset(PriceIndArray, 0, sizeof(PriceIndArray);  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, SQL_PARAM_BIND_BY_COLUMN, 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in column-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  PartIDArray, 0, PartIDIndArray);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  DescArray, DESC_LEN, DescLenOrIndArray);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  PriceArray, 0, PriceIndArray);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartIDArray[i], DescArray[i], &PriceArray[i]);  
   PartIDIndArray[i] = 0;  
   DescLenOrIndArray[i] = SQL_NTS;  
   PriceIndArray[i] = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
}  
```  
  
## <a name="row-wise-binding"></a>Zeilenweise Bindung  
 Wenn Sie zeilenbezogene Bindungen verwenden zu können, definiert eine Anwendung eine Struktur für jeden Satz von Parametern an. Die Struktur enthält ein oder zwei Elemente für jeden Parameter. Das erste Element enthält den Wert des Parameters und das zweite Element enthält die Längen-/Indikatorpuffers. Klicken Sie dann die Anwendung weist ein Array dieser Strukturen enthält, die so viele Elemente wie Werte für jeden Parameter vorhanden sind.  
  
 Die Anwendung wird die Größe der Struktur, um den Treiber mit der SQL_ATTR_PARAM_BIND_TYPE-Anweisungsattribut deklariert. Die Anwendung bindet die Adressen der Parameter in der ersten Struktur des Arrays. Der Treiber kann daher die Adresse der Daten für eine bestimmte Zeile und Spalte als berechnen.  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 Legen Sie die, in denen Zeilen zwischen 1 auf die Größe des Parameters nummeriert sind. Der Offset, sofern definiert, ist das Anweisungsattribut SQL_ATTR_PARAM_BIND_OFFSET_PTR verweist. Die folgende Abbildung zeigt die Funktionsweise der zeilenbezogenen Bindung. Die Parameter in der Struktur in beliebiger Reihenfolge platziert werden können, jedoch in sequenzieller Reihenfolge aus Gründen der Übersichtlichkeit angezeigt.  
  
 ![Zeigt wie Zeile &#45; hintergrundprüfung Bindung Works](../../../odbc/reference/develop-app/media/pr32.gif "pr32")  
  
 Der folgende Code erstellt eine Struktur mit Elementen, für die Werte in den Spalten PartID, Beschreibung und den Preis zu speichern. Anschließend ordnet ein Array mit 10 Elementen dieser Strukturen und bindet sie an die Parameter für die Spalten PartID, Beschreibung und den Preis, verwenden zeilenbezogene Bindungen. Es wird eine Anweisung zum Einfügen von 10 Zeilen ausgeführt.  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
typedef tagPartStruct {  
   SQLREAL       Price;  
   SQLUINTEGER   PartID;  
   SQLCHAR       Desc[DESC_LEN];  
   SQLINTEGER    PriceInd;  
   SQLINTEGER    PartIDInd;  
   SQLINTEGER    DescLenOrInd;  
} PartStruct;  
  
PartStruct PartArray[ARRAY_SIZE];  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  
                Price) "  
               "VALUES (?, ?, ?)";  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, sizeof(PartStruct), 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in row-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartArray[0].PartID, 0, &PartArray[0].PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  PartArray[0].Desc, DESC_LEN, &PartArray[0].DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &PartArray[0].Price, 0, &PartArray[0].PriceInd);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartArray[i].PartID, PartArray[i].Desc, &PartArray[i].Price);  
   PartArray[0].PartIDInd = 0;  
   PartArray[0].DescLenOrInd = SQL_NTS;  
   PartArray[0].PriceInd = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
```
