---
title: SQLSetConnectAttrForDbcInfo Funktion | Microsoft Docs
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
- SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c6d7bab7f8c2003c8a48017e7465e200622badf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo-Funktion
**Konformität**  
 Version eingeführt: ODBC 3,81 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLSetConnectAttrForDbcInfo** ist identisch mit **SQLSetConnectAttr**, aber es wird das Attribut auf die Informationen Verbindungstoken statt auf dem Verbindungshandle.  
  
## <a name="syntax"></a>Syntax  
  
```  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>Argumente  
 *hDbcInfoToken*  
 [Eingabe] Tokenhandle.  
  
 *Attribut*  
 [Eingabe] Attribut festlegen. Die Liste der gültigen Attribute ist treiberspezifisch und dem Verhalten von [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 *ValuePtr*  
 [Eingabe] Zeiger auf den Wert zugeordnet werden *Attribut*. Abhängig vom Wert der *Attribut*, *ValuePtr* wird ein 32-Bit-Ganzzahlwert ohne Vorzeichen sein, und zeigen auf eine Null-terminierte Zeichenfolge. Beachten Sie, dass bei der *Attribut* Argument ist eine treiberspezifische-Wert, der Wert im *ValuePtr* möglicherweise eine Ganzzahl mit Vorzeichen.  
  
 *stringLength*  
 [Eingabe] Wenn *Attribut* ist ein ODBC-definierten Attribut und *ValuePtr* zeigt auf eine Zeichenfolge oder einen binären Puffer, in dieses Argument muss die Länge des **ValuePtr*. Für Zeichenfolgendaten sollte dieses Argument die Anzahl der Bytes in der Zeichenfolge enthalten.  
  
 Wenn *Attribut* ist ein ODBC-definierten Attribut und *ValuePtr* ist eine ganze Zahl *StringLength* wird ignoriert.  
  
 Wenn *Attribut* ist ein Attribut treiberdefinierten die Anwendung zeigt die Art des Attributs an den Treiber-Manager an, indem die *StringLength* Argument. *StringLength* können die folgenden Werte aufweisen:  
  
-   Wenn *ValuePtr* ist ein Zeiger auf eine Zeichenfolge *StringLength* ist die Länge der Zeichenfolge oder SQL_NTS.  
  
-   Wenn *ValuePtr* ist ein Zeiger auf einen binären Puffer, und klicken Sie dann die Anwendung das Ergebnis von der SQL_LEN_BINARY_ATTR eingefügt (*Länge*)-Makro im *StringLength*. Dies setzt einen negativen Wert in *StringLength*.  
  
-   Wenn *ValuePtr* ist ein Zeiger auf einen anderen Wert als eine Zeichenfolge oder eine binäre Zeichenfolge *StringLength* müssen den Wert SQL_IS_POINTER.  
  
-   Wenn *ValuePtr* enthält einen Wert fester Länge *StringLength* ist SQL_IS_INTEGER oder SQL_IS_UINTEGER, nach Bedarf.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Identisch mit [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), außer dass der Treiber-Manager verwenden, wird eine **HandleType** von SQL_HANDLE_DBC_INFO_TOKEN und ein **behandeln** von *hDbcInfoToken* .  
  
## <a name="remarks"></a>Hinweise  
 **SQLSetConnectAttrForDbcInfo** ist identisch mit **SQLSetConnectAttr**, aber es wird das Attribut auf das Verbindungstoken für die Informationen, statt aus, auf dem Verbindungshandle. Z. B. wenn **SQLSetConnectAttr** ein Attribut nicht erkennt **SQLSetConnectAttrForDbcInfo** SQL_ERROR für dieses Attribut sollte auch zurück.  
  
 Wenn Treiber SQL_ERROR oder SQL_INVALID_HANDLE zurückgibt, sollte dieses Attribut, um die Pool-ID zu berechnen der Treiber ignoriert werden. Darüber hinaus erhält der Treiber-Manager die Diagnoseinformationen aus *hDbcInfoToken*, und SQL_SUCCESS_WITH_INFO zurückgegeben und auf die Anwendung im [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) und [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). Aus diesem Grund kann eine Anwendung abrufen von Details zu warum einige Attribute festgelegt werden kann.  
  
 Anwendungen sollten diese Funktion nicht direkt aufrufen. Ein ODBC-Treiber, der treiberfähiges Verbindungspooling unterstützt, muss diese Funktion implementieren.  
  
 Schließen Sie sqlspi.h für die Entwicklung von ODBC-Treiber.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln einen ODBC-Treiber](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Treiberfähiges Verbindungspooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Developing Connection-Pool Awareness in an ODBC Driver (Entwickeln von Verbindungspool-Unterstützung in einem ODBC-Treiber)](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
