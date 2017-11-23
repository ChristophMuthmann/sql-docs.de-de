---
title: Behandelt | Microsoft Docs
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
- handles [ODBC]
- driver handles [ODBC]
- driver manager [ODBC], handles
- handles [ODBC], about handles
ms.assetid: f663101e-a4cc-402b-b9d7-84d5e975be71
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 499f62ecd8e053ef0776873dcdf4fe20cac1fa96
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="handles"></a>Ziehpunkte
Handles sind nicht transparenten, 32-Bit-Werte, die ein bestimmtes Element identifizieren. in ODBC kann dieses Element aus einer Umgebung, Verbindung, Anweisung oder Deskriptor sein. Wenn die Anwendung aufruft, **SQLAllocHandle**der Treiber-Manager oder der Treiber erstellt ein neues Element vom angegebenen Typ und dessen Handle an die Anwendung zurückgegeben. Die Anwendung später verwendet das Handle zum Identifizieren dieses Elements beim Aufrufen von ODBC-Funktionen. Der Treiber-Manager und der Treiber verwenden das Handle, um Informationen über das Element zu suchen.  
  
 Der folgende Code verwendet beispielsweise zwei Anweisungshandles (*HstmtOrder* und *HstmtLine*) um die Anweisungen zu identifizieren, für die Erstellung von Resultsets von Sales Orders und Sales Zeilennummern Order. Später wird mit diesen Handles verwendet, um zu identifizieren, welche Resultset zum Abrufen von Daten aus.  
  
```  
SQLHSTMT      hstmtOrder, hstmtLine; // Statement handles.  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
SQLRETURN     rc;  
  
// Prepare the statement that retrieves line number information.  
SQLPrepare(hstmtLine, "SELECT * FROM Lines WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter in the preceding statement.  
SQLBindParameter(hstmtLine, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
               &OrderID, 0, &OrderIDInd);  
  
// Bind the result sets for the Order table and the Lines table. Bind  
// OrderID to the OrderID column in the Orders table. When each row is  
// fetched, OrderID will contain the current order ID, which will then be  
// passed as a parameter to the statement tofetch line number  
// information. Code not shown.  
  
// Create a result set of sales orders.  
SQLExecDirect(hstmtOrder, "SELECT * FROM Orders", SQL_NTS);  
  
// Fetch and display the sales order data. Code to check if rc equals  
// SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmtOrder)) != SQL_NO_DATA) {  
   // Display the sales order data. Code not shown.  
  
   // Create a result set of line numbers for the current sales order.  
   SQLExecute(hstmtLine);  
  
   // Fetch and display the sales order line number data. Code to check  
   // if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLFetch(hstmtLine)) != SQL_NO_DATA) {  
      // Display the sales order line number data. Code not shown.  
   }  
  
   // Close the sales order line number result set.  
   SQLCloseCursor(hstmtLine);  
}  
  
// Close the sales order result set.  
SQLCloseCursor(hstmtOrder);  
```  
  
 Handles sind sinnvoll, nur für die ODBC-Komponente, die sie erstellt wurden. der Treiber-Manager kann Treibermanager-Handles interpretieren und nur ein Treiber kann eine eigene Handles interpretieren.  
  
 Nehmen wir beispielsweise an der Treiber im vorhergehenden Beispiel weist eine Struktur zum Speichern von Informationen zu einer Anweisung und gibt den Zeiger auf diese Struktur als das Anweisungshandle zurück. Wenn die Anwendung aufruft, **SQLPrepare**, eine SQL-Anweisung übergibt und das Handle der Anweisung für die Bestellnummern Zeile verwendet. Der Treiber sendet die SQL-Anweisung mit der Datenquelle, die vorbereitet werden kann, und gibt einen Zugriff Plan Bezeichner zurück. Der Treiber verwendet das Handle, um die Struktur zum Speichern dieser Bezeichner zu suchen.  
  
 Wenn die Anwendung aufruft, später **SQLExecute** um das Resultset der Zeilennummern für einen bestimmten Verkaufsauftrag zu generieren, die dasselbe Handle übergibt. Der Treiber verwendet das Handle der Bezeichner für den Zugriff aus der Struktur abrufen. Den Bezeichner gesendet an die Datenquelle mitteilen, ist das ausführen möchten.  
  
 ODBC verfügt über zwei Ebenen von Handles: Treibermanager-Handles und Treiber behandelt. Die Anwendung verwendet Treibermanager-Handles beim ODBC-Funktionen aufrufen, da sie diese Funktionen in der Treiber-Manager aufruft. Der Treiber-Manager verwendet dieses Handle der entsprechende Treiber Handle gefunden und das Handle des Treibers beim Aufrufen der Funktion im Treiber. Ein Beispiel dafür, wie der Treiber und Treiber-Manager-Handles verwendet werden, finden Sie unter [Treiber-Manager-Rolle in der Verbindungsprozess](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).  
  
 Es gibt zwei Arten von Handles ist ein Artefakt der ODBC-Architektur; in den meisten Fällen ist es nicht relevant für die Anwendung oder den Treiber. Obwohl in der Regel kein Grund besteht dazu, es ist möglich, für die Anwendung aus, um zu bestimmen, die Treiber-Handles durch Aufrufen von **SQLGetInfo**.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Umgebungshandles](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [Verbindungshandles](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [Anweisungshandles](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [Deskriptorhandles](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [Statusübergänge](../../../odbc/reference/develop-app/state-transitions.md)
