---
title: SQLGetTypeInfo (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
- SQLGetTypeInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5f25e20b-a4ef-42da-aeb6-00e0510fb1cc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9bbf3983ccdeb2c320f4776d608b73e362f0a479
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 ODBC-API-Konformität: Ebene 1  
  
 Gibt Informationen zu den Datentypen, die von einer Datenquelle unterstützt. Der Treiber zurückgegeben die Informationen in einem SQL-Resultset. Die folgende Tabelle enthält die ODBC-Datentypen und den entsprechenden Visual FoxPro-Datentyp.  
  
|ODBC-Typ|Visual FoxPro-Typ|  
|---------------|------------------------|  
|SQL_BIGINT|Nicht unterstützt. Es ist kein 64-Bit-Visual FoxPro-Typ.|  
|SQL_BIT|Logische Operatoren|  
|SQL_CHAR|Zeichen|  
|SQL_DATE|Datum|  
|SQL_DECIMAL|Numerisch|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Integer|  
|SQL_LONGVARBINARY|Memo (binär)|  
|SQL_LONGVARCHAR|Memo|  
|SQL_NUMERIC|Numerische *, Währung, "float"|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Integer|  
|SQL_TIME|Nicht unterstützt. Es ist keine Visual FoxPro *Zeit* Typ.|  
|SQL_TIMESTAMP|datetime|  
|SQL_TINYINT|Integer|  
|SQL_VARBINARY|Memo (binär) *, Allgemein|  
|SQL_VARCHAR|Zeichen|  
  
 * Standardtyp  
  
 Weitere Informationen zum Visual FoxPro-Datentypen finden Sie unter [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md). Weitere Informationen zu dieser Funktion finden Sie unter [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) in der *ODBC Programmer's Reference*.
