---
title: Zuweisen und Freigeben von Puffern | Microsoft Docs
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
- buffers [ODBC], allocating and freeing
- allocating buffers [ODBC]
- freeing buffers [ODBC]
ms.assetid: 886bc9ed-39d4-43d2-82ff-aebc35b14d39
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e85c2ab4ad25501637ccba2206f85c7895440ade
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="allocating-and-freeing-buffers"></a>Zuweisen und Freigeben von Puffern
Alle Puffer werden reserviert und freigegeben, indem die Anwendung. Wenn Sie ein Puffer nicht verzögert wird, müssen sie nur für die Dauer des Aufrufs einer Funktion vorhanden sein. Beispielsweise **SQLGetInfo** gibt den Wert mit einer bestimmten Option im Puffer, die durch die *InfoValuePtr* Argument. Dieser Puffer kann freigegeben werden, sofort nach dem Aufruf von **SQLGetInfo**, wie im folgenden Codebeispiel gezeigt:  
  
```  
SQLSMALLINT   InfoValueLen;  
SQLCHAR *     InfoValuePtr = malloc(50);   // Allocate InfoValuePtr.  
  
SQLGetInfo(hdbc, SQL_DBMS_NAME, (SQLPOINTER)InfoValuePtr, 50,  
            &InfoValueLen);  
  
free(InfoValuePtr);                        // OK to free InfoValuePtr.  
```  
  
 Da verzögerte Puffer werden in eine bestimmte Funktion angegeben und in einer anderen verwendet, ist es eine Anwendung Programmierfehler um eine verzögerte Puffer freizugeben, während der Treiber noch vorhanden sein, erwartet. Beispielsweise die Adresse des dem \* *ValuePtr* übergebene Puffer ist zu **SQLBindCol** zur späteren Verwendung mit **SQLFetch**. Dieser Puffer kann nicht geleert werden, bis die Spalte aufgehoben, z. B. durch einen Aufruf wird **SQLBindCol** oder **SQLFreeStmt** wie im folgenden Codebeispiel gezeigt:  
  
```  
SQLRETURN    rc;  
SQLINTEGER   ValueLenOrInd;  
SQLHSTMT     hstmt;  
  
// Allocate ValuePtr  
SQLCHAR * ValuePtr = malloc(50);  
  
// Bind ValuePtr to column 1. It is an error to free ValuePtr here.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, 50, &ValueLenOrInd);  
  
// Fetch each row of data and place the value for column 1 in *ValuePtr.  
// Code to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO   
// not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // It is an error to free ValuePtr here.  
}  
  
// Unbind ValuePtr from column 1.  It is now OK to free ValuePtr.  
SQLFreeStmt(hstmt, SQL_UNBIND);  
free(ValuePtr);  
```  
  
 Solche Fehler erfolgt einfach durch den Puffer lokal in einer Funktion deklarieren; der Puffer wird freigegeben, wenn die Anwendung die Funktion verlässt. Beispielsweise verursacht der folgende Code nicht definiert "und" wahrscheinlich schwerwiegend Verhalten im Treiber:  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
BindAColumn(hstmt);  
  
// Fetch each row of data and try to place the value for column 1 in  
// *ValuePtr. Because ValuePtr has been freed, the behavior is undefined  
// and probably fatal. Code to check if rc equals SQL_ERROR or   
// SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {}  
  
   .  
   .  
   .  
  
void BindAColumn(SQLHSTMT hstmt)  // WARNING! This function won't work!  
{  
   // Declare ValuePtr locally.  
   SQLCHAR      ValuePtr[50];  
   SQLINTEGER   ValueLenOrInd;  
  
   // Bind rgbValue to column.  
   SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr),  
               &ValueLenOrInd);  
  
   // ValuePtr is freed when BindAColumn exits.  
}  
```
