---
title: "Überschreiben der Standardwerte für die Genauigkeit und Dezimalstellenanzahl für numerische Datentypen | Microsoft Docs"
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
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 613ec65d838a525251b6682cca477c5c8d24a162
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>Überschreiben der Standardwerte für die Genauigkeit und Dezimalstellenanzahl für numerische Datentypen
Wenn das SQL_DESC_TYPE-Feld in einer ARD auf SQL_C_NUMERIC, durch den Aufruf eines festgelegt ist **SQLBindCol** oder **SQLSetDescField**, Feld SQL_DESC_SCALE in die ARD auf 0 festgelegt ist und das Feld SQL_DESC_PRECISION festgelegt ist Um eine treiberdefinierten standardgenauigkeit. Dies gilt auch, wenn das SQL_DESC_TYPE-Feld in einer APD auf SQL_C_NUMERIC, festgelegt ist, durch den Aufruf eines **SQLBindParameter** oder **SQLSetDescField**. Dies gilt für Eingabe-, Eingabe/Ausgabe oder Output-Parameter.  
  
 Wenn entweder die Standardwerte beschrieben nicht zuvor für eine Anwendung zulässig sind, sollte die Anwendung durch Aufrufen von Feld SQL_DESC_SCALE oder SQL_DESC_PRECISION festgelegt **SQLSetDescField** oder **SQLSetDescRec**.  
  
 Wenn die Anwendung aufruft, **SQLGetData** um Daten in einer Struktur SQL_C_NUMERIC zurückgegeben werden, werden die Standardfelder SQL_DESC_SCALE und SQL_DESC_PRECISION verwendet. Wenn die Standardwerte nicht zulässig sind, muss die Anwendung aufrufen **SQLSetDescRec** oder **SQLSetDescField** legen Sie die Felder aus, und rufen Sie anschließend **SQLGetData** mit einem *TargetType* von SQL_ARD_TYPE, um die Werte in die deskriptorfelder verwenden.  
  
 Wenn **SQLPutData** wird aufgerufen, der Aufruf verwendet die Felder SQL_DESC_SCALE und SQL_DESC_PRECISION der anwendungsparameterdeskriptor-Datensatz, der die Data-at-Execution-Parameter oder eine Spalte entspricht dem handelt es sich um APD Felder für Aufrufe von ** SQLExecute** oder **SQLExecDirect**, oder ARD Felder für Aufrufe von **SQLBulkOperations** oder **SQLSetPos**.
