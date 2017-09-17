---
title: Binden von Parametermarkierungen | Microsoft Docs
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
- parameter markers [ODBC]
- binding parameter markers [ODBC]
ms.assetid: fe88c1c2-4ee4-45e0-8500-b8c25c047815
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cd8c39160ee6cafbbc9f041565a57ea29680bef7
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="binding-parameter-markers"></a>Binden von Parametermarkierungen
Die Anwendung bindet Parameter durch den Aufruf **SQLBindParameter**. **SQLBindParameter** bindet einen Parameter zu einem Zeitpunkt. Mithilfe dieser Option gibt die Anwendung Folgendes an:  
  
-   Der Parameter mit der Nummer. Parameter werden in zunehmenden Reihenfolge der Parameter in der SQL-Anweisung, beginnend mit der Zahl 1 nummeriert. Es ist zwar zulässig, geben Sie einen Parameter mit der Nummer, die größer ist als die Anzahl von Parametern in der SQL-Anweisung, der Wert des Parameters ignoriert wird, wenn die Anweisung ausgeführt wird.  
  
-   Der Parametertyp (Eingabe-, Eingabe/Ausgabe- oder Ausgabe). Mit Ausnahme von Parametern in Prozeduraufrufen sind alle Parameter Eingabeparameter an. Weitere Informationen finden Sie unter [Prozedurparameter](../../../odbc/reference/develop-app/procedure-parameters.md)weiter unten in diesem Abschnitt.  
  
-   Die C-Daten Typ, Adresse und Byte der Länge der Variablen, die an den Parameter gebunden werden. Der Treiber muss in der Lage, die Daten aus der C-Datentyp in der SQL-Datentyp zu konvertieren, oder ein Fehler zurückgegeben. Eine Liste der unterstützten Konvertierungen, finden Sie unter [Konvertieren von Daten von C-in SQL-Datentypen](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) in Anhang D:-Datentypen.  
  
-   Die SQL-Datentyp, Genauigkeit und Dezimalstellen des Parameters selbst.  
  
-   Die Adresse des ein Längen-/Indikatorpuffers. Stellt die Bytelänge der Binär-oder Zeichendatentypen, gibt an, dass die Daten NULL ist, oder gibt an, dass die Daten mit gesendet werden **SQLPutData**. Weitere Informationen finden Sie unter [mit Längenindikator/Werten](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Im folgenden Codebeispiel beispielsweise bindet *Vertriebsmitarbeiter* und *CustID* Parameter für den Verkäufer und CustID Spalten. Da *Vertriebsmitarbeiter* Zeichendaten variabler Länge ist, enthält der Code gibt an, die Bytelänge der *Vertriebsmitarbeiter* (11) und bindet *SalesPersonLenOrInd* an enthalten die Bytelänge der Daten in *Vertriebsmitarbeiter*. Diese Informationen sind nicht erforderlich für *CustID* , da es Integer-Daten enthält, die feste Länge ist.  
  
```  
SQLCHAR       SalesPerson[11];  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLUINTEGER   CustID;  
  
// Bind SalesPerson to the parameter for the SalesPerson column and  
// CustID to the parameter for the CustID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 10, 0,  
                  SalesPerson, sizeof(SalesPerson), &SalesPersonLenOrInd);  
SQLBindParameter(hstmt1, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &CustID, 0, &CustIDInd);  
  
// Set values of salesperson and customer ID and length/indicators.  
strcpy_s((char*)SalesPerson, _countof(SalesPerson), "Garcia");  
SalesPersonLenOrInd = SQL_NTS;  
CustID = 1331;  
CustIDInd = 0;  
  
// Execute a statement to get data for all orders made to the specified  
// customer by the specified salesperson.  
SQLExecDirect(hstmt1,"SELECT * FROM Orders WHERE SalesPerson=? AND CustID=?",SQL_NTS);  
```  
  
 Wenn **SQLBindParameter** wird aufgerufen, der Treiber speichert diese Informationen in der Struktur für die Anweisung. Wenn die Anweisung ausgeführt wird, verwendet er die Informationen der Parameterdaten abrufen und an die Datenquelle gesendet.  
  
> [!NOTE]  
>  In ODBC 1.0, Parameter gebunden wurden, mit **SQLSetParam**. Der Treiber-Manager ordnet Aufrufe zwischen **SQLSetParam** und **SQLBindParameter**, abhängig von den Versionen von ODBC, die von der Anwendung und Treiber verwendet.
