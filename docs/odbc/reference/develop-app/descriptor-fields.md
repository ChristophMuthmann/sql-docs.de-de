---
title: Deskriptorfelder | Microsoft Docs
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
- descriptors [ODBC], fields
- header fields [ODBC]
- record fields [ODBC]
ms.assetid: f38623c8-fdd4-4601-b1f0-97c593d31177
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed9b26cf9af0bd6b0a0a81faad62e446f01f03fd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="descriptor-fields"></a>Deskriptorfelder
Deskriptoren enthalten *Header* und *Datensatz* Felder, die Spalten oder Parametern vollständig zu beschreiben.  
  
 Ein Deskriptor enthält eine einzelne Kopie der folgenden Headerfelder. Ändern ein Headerfeld wirkt sich auf alle Spalten oder Parametern.  
  
|||  
|-|-|  
|SQL_DESC_ALLOC_TYPE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_COUNT|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 Ein Deskriptor enthält null oder mehr deskriptordatensätze. Jeder Datensatz beschreibt eine Spalte oder einen Parameter je nach Art des Deskriptors. Wenn eine neue Spalte oder Parameter gebunden ist, wird ein neuer Datensatz der Deskriptor hinzugefügt. Wenn eine Spalte oder Parameter aufgehoben wird, wird ein Datensatz aus den Deskriptor entfernt. Jeder Datensatz enthält eine einzelne Kopie die folgenden Felder:  
  
|||  
|-|-|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_DESC_LOCAL_TYPE_NAME|  
|SQL_DESC_BASE_COLUMN_NAME|SQL_DESC_NAME|  
|SQL_DESC_BASE_TABLE_NAME|SQL_DESC_NULLABLE|  
|SQL_DESC_CASE_SENSITIVE|SQL_DESC_OCTET_LENGTH|  
|SQL_DESC_CATALOG_NAME|SQL_DESC_OCTET_LENGTH_PTR|  
|SQL_DESC_CONCISE_TYPE|SQL_DESC_PARAMETER_TYPE|  
|SQL_DESC_DATA_PTR|SQL_DESC_PRECISION|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_DESC_SCALE|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQL_DESC_SCHEMA_NAME|  
|SQL_DESC_DISPLAY_SIZE|SQL_DESC_SEARCHABLE|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_DESC_TABLE_NAME|  
|SQL_DESC_INDICATOR_PTR|SQL_DESC_TYPE|  
|SQL_DESC_LABEL|SQL_DESC_TYPE_NAME|  
|SQL_DESC_LENGTH|SQL_DESC_UNNAMED|  
|SQL_DESC_LITERAL_PREFIX|SQL_DESC_UNSIGNED|  
|SQL_DESC_LITERAL_SUFFIX|SQL_DESC_UPDATABLE|  
  
 Ein Deskriptor, der das Headerfeld entsprechen viele Anweisungsattribute. Diese Attribute durch einen Aufruf von festlegen **SQLSetStmtAttr** und zum Festlegen der entsprechenden deskriptorheaderfeld durch Aufrufen von **SQLSetDescField** den gleichen Effekt. Dasselbe gilt für **SQLGetStmtAttr** und **SQLGetDescField**, beide über die gleichen Informationen abrufen. Die Funktionen aufrufen, Anweisung anstelle der Deskriptor Funktionen hat den Vorteil, die eine Deskriptorhandles nicht abgerufen werden sollen.  
  
 Die folgenden Headerfelder können festgelegt werden, indem Anweisungsattribute festlegen:  
  
|||  
|-|-|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Anzahl der Datensätze](../../../odbc/reference/develop-app/record-count.md)  
  
-   [Gebundene Deskriptordatensätze](../../../odbc/reference/develop-app/bound-descriptor-records.md)  
  
-   [Zurückgestellte Felder](../../../odbc/reference/develop-app/deferred-fields.md)  
  
-   [Konsistenzprüfung](../../../odbc/reference/develop-app/consistency-check.md)
