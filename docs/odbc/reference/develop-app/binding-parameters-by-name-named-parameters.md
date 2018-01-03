---
title: Binden von Parametern anhand des Namens (Parameter genannt) | Microsoft Docs
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
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a9548f671ce082d41423c1f85eb543c55b6194a2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="binding-parameters-by-name-named-parameters"></a>Binden von Parametern anhand des Namens (benannten Parametern)
Bestimmte Datenbankmanagementsysteme ermöglichen eine Anwendung, die Parameter an eine gespeicherte Prozedur nach Namen anstelle von anhand der Position im Aufruf Prozedur anzugeben. Solche Parameter heißen *benannte Parameter*. ODBC unterstützt die Verwendung benannter Parameter. In ODBC benannte Parameter werden nur in Aufrufen von gespeicherten Prozeduren verwendet und können nicht in anderen SQL­Anweisungen verwendet werden.  
  
 Der Treiber überprüft den Wert des Felds SQL_DESC_UNNAMED, der die IPD, zu bestimmen, ob der benannte Parameter verwendet werden. Wenn SQL_DESC_UNNAMED SQL_UNNAMED nicht festgelegt ist, verwendet der Treiber den Namen in der SQL_DESC_NAME-Felds den IPD zur Identifizierung des Parameters an. Eine Anwendung kann zum Binden des Parameters aufrufen **SQLBindParameter** , geben Sie die Parameterinformationen und anschließend können Aufrufen **SQLSetDescField** SQL_DESC_NAME-Felds den IPD festlegen. Wenn benannte Parameter verwendet werden, wird die Reihenfolge der Parameter im Aufruf Prozedur ist nicht wichtig, und Datensatznummer der Parameter wird ignoriert.  
  
 Der Unterschied zwischen unbenannte Parameter und benannte Parameter ist in der Beziehung zwischen der Datensatznummer, des Deskriptors und die Parameteranzahl in der Prozedur. Wenn unbenannte Parameter verwendet werden, die erste parametermarkierung des ersten Datensatzes in den Parameterdeskriptor bezieht sich auf die wiederum auf den ersten Parameter (in der Reihenfolge der Erstellung) im Prozeduraufruf verknüpft ist. Wenn benannte Parameter verwendet werden, die erste parametermarkierung bezieht sich immer noch auf den ersten Eintrag des Deskriptors Parameter, aber die Beziehung zwischen der Datensatznummer, des Deskriptors und die Parameteranzahl in der Prozedur ist nicht mehr vorhanden. Benannte Parameter verwenden Sie die Zuordnung der Nummer des Deskriptors nicht an die Prozedur Parameterposition; Stattdessen wird der Datensatz Deskriptorname den Namen der Prozedur zugeordnet.  
  
> [!NOTE]  
>  Wenn automatischer Auffüllung der die IPD aktiviert ist, wird der Treiber Deskriptors aufgefüllt, dass die Reihenfolge der deskriptordatensätze die Reihenfolge der Parameter in der Prozedurdefinition übereinstimmt, selbst wenn benannten Parameter verwendet werden.  
  
 Wenn Sie ein benannter Parameter verwendet wird, müssen alle Parameter Parameter benannt werden. Wenn ein der Parameter keinen benannten Parameter ist, werden klicken Sie dann keines der Zertifizierungsstelle Parameter benannte Parameter. Wäre eine Kombination von benannten Parametern und unbenannte Parameter, würde das Verhalten Treiber abhängig sein.  
  
 Nehmen Sie beispielsweise benannter Parameter an eine SQL-Server, die gespeicherte Prozedur wie folgt definiert wurde:  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 In diesem Verfahren wird der erste Parameter @title_id, hat den Standardwert 1. Eine Anwendung kann den folgenden Code verwenden, um diese Prozedur aufzurufen, dass es nur einen dynamischen Parameter gibt an. Dieser Parameter ist ein benannter Parameter mit dem Namen "@quote".  
  
```  
// Prepare the procedure invocation statement.  
SQLPrepare(hstmt, "{call test(?)}", SQL_NTS);  
  
// Populate record 1 of ipd.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                  30, 0, szQuote, 0, &cbValue);  
  
// Get ipd handle and set the SQL_DESC_NAMED and SQL_DESC_UNNAMED fields  
// for record #1.  
SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
// Assuming that szQuote has been appropriately initialized,  
// execute.  
SQLExecute(hstmt);  
```
