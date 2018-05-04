---
title: Außerkraftsetzung der führende und Sekunden Genauigkeit für Intervalldatentypen | Microsoft Docs
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
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca22fe0d3153fc5ea4f0c5594ff537d65d60c066
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>Überschreiben Standard führende und Sekunden Genauigkeit für die Interval-Datentypen
Wenn das SQL_DESC_TYPE-Feld ein ARD durch Aufrufen von entweder um einen "DateTime" oder "Intervall C" festgelegt ist **SQLBindCol** oder **SQLSetDescField**, Feld SQL_DESC_PRECISION (enthält das Intervall (Sekunden) Genauigkeit) wird auf die folgenden Standardwerte festgelegt:  
  
-   6 für Zeitstempel und alle Intervalldatentypen mit einer zweiten Komponente.  
  
-   0 für alle anderen Datentypen.  
  
 Für alle Interval-Datentypen wird das Deskriptorfeld SQL_DESC_DATETIME_INTERVAL_PRECISION, das das Intervall führende Feld Genauigkeit enthält, auf den Standardwert 2 festgelegt.  
  
 Wenn das SQL_DESC_TYPE-Feld in einer APD durch Aufrufen von entweder um einen "DateTime" oder "Intervall C" festgelegt ist **SQLBindParameter** oder **SQLSetDescField**, die SQL_DESC_PRECISION und SQL_DESC_DATETIME_INTERVAL_ Genauigkeit Felder im APD werden auf der zuvor angegebenen Standardwert festgelegt. Dies gilt für Eingabeparameter, jedoch nicht für Eingabe/Ausgabe-oder Ausgabeparameter.  
  
 Ein Aufruf von **SQLSetDescRec** legt die Genauigkeit für anführenden Intervallwert auf den Standardwert aber legt die Intervall-Sekunden-Genauigkeit (in das Feld "SQL_DESC_PRECISION") auf den Wert von dessen *Genauigkeit* Argument.  
  
 Wenn entweder die angegebenen Standardwerte zuvor nicht zulässig ist, eine Anwendung, sollte die Anwendung durch Aufrufen von Feld SQL_DESC_PRECISION oder SQL_DESC_DATETIME_INTERVAL_PRECISION festgelegt **SQLSetDescField**.  
  
 Wenn die Anwendung aufruft, **SQLGetData** Daten in eine "DateTime" oder das Intervall C-Typ zurück, die führende standardgenauigkeit für Intervall und Intervall Sekunden Genauigkeit verwendet werden. Wenn entweder Standard nicht zulässig ist, muss die Anwendung aufrufen **SQLSetDescField** entweder Deskriptorfeld festlegen oder **SQLSetDescRec** SQL_DESC_PRECISION festlegen. Der Aufruf von **SQLGetData** sollte eine *TargetType* von SQL_ARD_TYPE, um die Werte in die deskriptorfelder verwenden.  
  
 Wenn **SQLPutData** aufgerufen wird, wird die für anführenden Intervallwert, Genauigkeit und Intervall Sekunden Genauigkeit werden die Felder der Deskriptordatensatz, die entsprechen gelesen, in die Data-at-Execution-Parameter oder eine Spalte, die APD Felder für Aufrufe sind um **SQLExecute** oder **SQLExecDirect**, oder ARD Felder für Aufrufe von **SQLBulkOperations** oder **SQLSetPos**.
