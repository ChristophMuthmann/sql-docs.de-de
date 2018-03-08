---
title: Datentyp-IDs und Deskriptoren | Microsoft Docs
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
- data types [ODBC], identifiers
- identifiers [ODBC], data types
- descriptors [ODBC], data types
- verbose data types [ODBC]
- data types [ODBC], descriptors
- concise data types [ODBC]
ms.assetid: f0077c9b-8eb2-4b5f-8c4c-7436fdef37ab
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1f54638aa02c885ee0e6fe8d14310d319dafb11c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="data-type-identifiers-and-descriptors"></a>-Datentypbezeichnungen und Deskriptoren
Die Datentypen aufgeführt, der [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md) und [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md) Abschnitten weiter oben in diesem Anhang werden "präzise" Datentypen: jeder Bezeichner verweist auf eine single-Datentyp. Es ist eine 1: 1-Entsprechung zwischen den Bezeichner und den Datentyp aus. Deskriptoren, führen jedoch nicht in allen Fällen einen einzelnen Wert verwenden, um Datentypen zu identifizieren. In einigen Fällen verwenden sie einen Datentyp für "verbose" und einen Typ Subcode. Für alle Datentypen mit Ausnahme der Datentypen "DateTime" und das Intervall der ausführlichen Typbezeichner ist identisch mit der präzise Typbezeichner, und der Wert in SQL_DESC_DATETIME_INTERVAL_CODE gleich 0 ist. Für die Datentypen "DateTime" und das Intervall jedoch ein ausführlichen Typ (SQL_DATETIME oder SQL_INTERVAL) in SQL_DESC_TYPE gespeichert ist, ein präziser in SQL_DESC_CONCISE_TYPE gespeichert wird und eine Subcode für jeden präziser in SQL_DESC_DATETIME_INTERVAL_CODE gespeichert ist. Eines dieser Felder wirkt sich auf die anderen. Weitere Informationen zu diesen Feldern finden Sie unter der [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) funktionsbeschreibung.  
  
 Wenn das Feld SQL_DESC_TYPE oder SQL_DESC_CONCISE_TYPE für einige Datentypen festgelegt ist, werden die Felder SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_LENGTH, SQL_DESC_PRECISION oder SQL_DESC_SCALE automatisch auf die Standardwerte für die Daten ggf. festgelegt Geben Sie ein. Weitere Informationen finden Sie in der Beschreibung des Felds SQL_DESC_TYPE in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Ob alle festgelegten Standardwerte nicht geeignet ist, sollte die Anwendung explizit das Deskriptorfeld durch einen Aufruf von festgelegt **SQLSetDescField**.  
  
 Die folgende Tabelle zeigt die präzise Typbezeichner, ausführlichen Typbezeichner und Typ Subcode für jede "DateTime" und Intervall SQL und C#-Typ-ID. Wie in dieser Tabelle gibt an, für die Datentypen "DateTime" und das Intervall, haben das SQL_DESC_TYPE und SQL_DESC_DATETIME_INTERVAL_CODE Felder die gleichen Manifestkonstanten für SQL-Datentypen (in der Implementierung Deskriptoren) und C-Datentypen (in der Anwendung die Deskriptoren).  
  
|Präzise SQL-Typ|Präzise C-Typ|Ausführliche Typ|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
QL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
QL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|
