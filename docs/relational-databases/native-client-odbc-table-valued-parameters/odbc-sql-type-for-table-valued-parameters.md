---
title: ODBC-SQL-Typ für Tabellenwertparameter | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 87436164f2a1177bc19ca80f2bfa53079120aa63
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>ODBC-SQL-Typ für Tabellenwertparameter
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Unterstützung für Tabellenwertparameter wird von einem neuen ODBC-SQL-Typ, SQL_SS_TABLE, bereitgestellt.  
  
## <a name="remarks"></a>Hinweise  
 SQL_SS_TABLE kann nicht konvertiert werden, in einen anderen ODBC- oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp.  
  
 Wenn SQL_SS_TABLE, als C-Datentyp in verwendet wird der *ValueType* -Parameter von SQLBindParameter oder den Versuch erfolgt SQL_DESC_TYPE in einem anwendungsparameterdeskriptor (APD)-Datensatz auf SQL_SS_TABLE festgelegt, wird SQL_ERROR zurückgegeben und ein Diagnosedatensatz generiert, mit der Meldung SQLSTATE = HY003, "Ungültiger Anwendungspuffertyp".  
  
 Wenn SQL_DESC_TYPE in einem IPD-Datensatz auf SQL_SS_TABLE festgelegt wird, und der entsprechende Anwendungsparameterdeskriptor-Datensatz nicht SQL_C_DEFAULT ist, wird SQL_ERROR zurückgegeben, und ein Diagnosedatensatz mit der Meldung SQLSTATE=HY003, "Ungültiger Anwendungspuffertyp" wird generiert. Dies kann auftreten, mit der *ParameterType* eines SQLSetDescField, SQLSetDescRec oder SQLBindParameter.  
  
 Wenn die *TargetType* Aufrufen von SQLGetData-Parameter SQL_SS_TABLE ist, wird SQL_ERROR zurückgegeben, und ein Diagnosedatensatz mit SQLSTATE generiert = HY003, "Ungültiger Anwendungspuffertyp".  
  
 Eine Tabellenwertparameter-Spalte kann nicht als SQL_SS_TABLE-Datentyp gebunden werden. Wenn der **SQLBindParameter** -Parameter aufgerufen wird und *ParameterType* auf SQL_SS_TABLE festgelegt ist, wird SQL_ERROR zurückgegeben, und ein Diagnosedatensatz mit der Meldung SQLSTATE=HY004, "Ungültiger SQL-Datentyp" generiert. Dies kann auch mit SQLSetDescField und SQLSetDescRec auftreten.  
  
 Tabellenwertparameter-Spaltenwerte verfügen über dieselben Datenkonvertierungsoptionen wie Parameter und Ergebnisspalten.  
  
 Bei einem Tabellenwertparameter kann es sich nur um einen Eingabeparameter in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder höher handeln. Wenn versucht wird, SQL_DESC_PARAMETER_TYPE auf einen anderen Wert als SQL_PARAM_INPUT über SQLBindParameter oder SQLSetDescField festgelegt, dann SQL_ERROR zurückgegeben wird und ein Diagnosedatensatz mit SQLSTATE-Anweisung hinzugefügt = HY105 und der Meldung "Ungültiger parameter Geben Sie".  
  
 Tabellenwertparameter-Spalten können SQL_DEFAULT_PARAM nicht in *StrLen_or_IndPtr*verwenden, da Standardwerte pro Zeile nicht mit Tabellenwertparametern unterstützt werden. Stattdessen kann eine Anwendung das Spaltenattribut SQL_CA_SS_COL_HAS_DEFAULT_VALUE auf 1 festlegen. Dies bedeutet, dass die Spalte Standardwerte für alle Zeilen aufweist. Wenn *StrLen_or_IndPtr* ist festgelegt auf SQL_DEFAULT_PARAM, SQLExecute oder SQLExecDirect SQL_ERROR zurück, und wird ein Diagnosedatensatz mit SQLSTATE-Anweisung hinzugefügt werden = HY090 und der Meldung "Ungültige Zeichenfolgen- oder Pufferlänge".  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellenwertparameter &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
