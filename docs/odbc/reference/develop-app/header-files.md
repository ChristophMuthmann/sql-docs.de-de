---
title: Header-Dateien | Microsoft Docs
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
- header files [ODBC]
ms.assetid: b4a03273-5e30-4d7b-826e-02f8f28ba078
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62d31cdda9e97ba72374c60c551f37ecfeccd71c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="header-files"></a>Headerdateien
Die Headerdatei Sql.h enthält die Prototypen für die Funktionen und Funktionen in der ODBC-Kernschnittstelle Konformitätsgrad. Die Sqlext.h-Header-Datei enthält die Prototypen für die Funktionen und Funktionen in der Ebene 1 und Level 2-API-Übereinstimmungsebenen. Die Headerdatei Sqltypes.h enthält Typdefinitionen und Indikatoren für die SQL-Datentypen.  
  
 Die Headerdateien alle enthalten einem **#define**, ODBCVER, die eine Anwendung oder Treiber festlegen können, für verschiedene Versionen von ODBC kompiliert werden.  
  
 Um mit der ISO-CLI und Open Group CLI auszurichten, enthalten die Headerdateien Aliase für die Typen von Informationen in Aufrufen verwendet **SQLGetInfo**. In der folgenden Tabelle gibt der ODBC-Name für den Typ der Informationen in die Spalte "ODBC-Name" an [ODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md). Die Spalte "Alias in der Headerdatei" gibt an, den Namen, der in der ISO-CLI und der Open Group CLI verwendet wird. Die tatsächliche numerische Wert dieser manifest Namen entspricht in ODBC und die standard-CLIs. Mit Standards kompatible Anwendung oder Treiber mit der ODBC 3. kompiliert diese Aliase ermöglichen *.x* Headerdateien.  
  
 Diese Aliasnamen enthalten Erweiterungen von Abkürzungen in den ODBC-Namen, damit die Namen leichter verständlich sind. "MAX" ist auf "MAXIMUM", "LEN" auf "LENGTH", "MULT", "Mehrere", "ABl.", "OUTER_JOIN" und "Überschreitungstransaktion", "TRANSACTION". erweitert  
  
|ODBC-name|Alias in der Headerdatei.|  
|---------------|--------------------------|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAXIMUM_CATALOG_NAME_LENGTH|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAXIMUM_COLUMN_NAME_LENGTH|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAXIMUM_COLUMNS_IN_GROUP_BY|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAXIMUM_COLUMNS_IN_ORDER_BY|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAXIMUM_COLUMNS_IN_SELECT|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAXIMUM_COLUMNS_IN_TABLE|  
|SQL_MAX_CONCURRENT_ACTIVITIES|SQL_MAXIMUM_CONCURRENT_ACTIVITIES|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAXIMUM_CURSOR_NAME_LENGTH|  
|SQL_MAX_DRIVER_CONNECTIONS|SQL_MAXIMUM_DRIVER_CONNECTIONS|  
|SQL_MAX_IDENTIFIER_LEN|SQL_MAXIMUM_IDENTIFIER_LENGTH|  
|SQL_MAX_SCHEMA_NAME_LEN|SQL_MAXIMUM_SCHEMA_NAME_LENGTH|  
|SQL_MAX_STATEMENT_LEN|SQL_MAXIMUM_STATEMENT_LENGTH|  
|SQL_MAX_TABLE_NAME_LEN|SQL_MAXIMUM_TABLE_NAME_LENGTH|  
|SQL_MAX_TABLES_IN_SELECT|SQL_MAXIMUM_TABLES_IN_SELECT|  
|SQL_MAX_USER_NAME_LEN|SQL_MAXIMUM_USER_NAME_LENGTH|  
|SQL_MULT_RESULT_SETS|SQL_MULTIPLE_RESULT_SETS|  
|SQL_OJ_CAPABILITIES|SQL_OUTER_JOIN_CAPABILITIES|  
|SQL_TXN_CAPABLE|SQL_TRANSACTION_CAPABLE|  
|SQL_TXN_ISOLATION_OPTION|SQL_TRANSACTION_ISOLATION_OPTION|
