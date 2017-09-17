---
title: "Treiber für Deskriptoren und Desktop-Datenbank | Microsoft Docs"
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
- desktop database drivers [ODBC], descriptors
- Jet-based ODBC drivers [ODBC], descriptors
- descriptors [ODBC], Jet-supported descriptor fields
- ODBC desktop database drivers [ODBC], descriptors
ms.assetid: 9ae2d9b5-365f-4f0a-9116-defe9498b401
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 67f656acd349419d7fc3d1c264985beeb36298ce
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="descriptors-and-desktop-database-drivers"></a>Deskriptoren und Desktop-Datenbanktreiber
Ein Deskriptor ist eine Datenstruktur, die Informationen zum Spaltendaten oder dynamische Parameter enthält. **SQLGetDescField** können verwendet werden, um die unten aufgeführten unterstützten Deskriptoren abzurufen. Implementierung Parameter Deskriptoren (Implementierungsparameterdeskriptor, Implementierungszeilendeskriptor) werden nicht automatisch aufgefüllt, da **SQLDescribeParam** wird nicht unterstützt. Deskriptorfelder, die über Jet (z. B. SQL_DESC_BASE_TABLE_NAME) nicht verfügbar sind, werden ebenfalls nicht unterstützt.  
  
 Weitere Informationen zu unterstützten Jet deskriptorfelder, finden Sie unter der *Microsoft Jet-Datenbank-Engine-Programmiererhandbuch*.  
  
 Weitere Informationen zu Deskriptoren, finden Sie unter den Themen unter "Deskriptoren" in der *ODBC Programmer's Reference*.  
  
|Deskriptorfelder|Supportebene|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Unterstützt|  
|SQL_DESC_ARRAY_SIZE|Nur für ARD unterstützt|  
|SQL_DESC_ARRAY_STATUS_PTR|Unterstützt|  
|SQL_DESC_BIND_OFFSET_PTR|Unterstützt|  
|SQL_DESC_BIND_TYPE|Unterstützt|  
|SQL_DESC_COUNT|Unterstützt|  
|SQL_DESC_ROWS_PROCESSED_PTR|Nur für ARD unterstützt|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Unterstützt|  
|SQL_DESC_BASE_COLUMN_NAME|Unterstützt (neu)|  
|SQL_DESC_BASE_TABLE_NAME|Unterstützt (neu)|  
|SQL_DESC_CASE_SENSITIVE|Immer "false"|  
|SQL_DESC_CATALOG_NAME|Nicht unterstützt|  
|SQL_DESC_CONCISE_TYPE|Unterstützt|  
|SQL_DESC_DATA_PTR|Unterstützt|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Unterstützt|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Für die Intervall-C-Typen unterstützt|  
|SQL_DESC_DISPLAY_SIZE|Unterstützt|  
|SQL_DESC_FIXED_PREC_SCALE|Unterstützte ("true" für Money)|  
|SQL_DESC_INDICATOR_PTR|Unterstützt|  
|SQL_DESC_LABEL|Unterstützt|  
|SQL_DESC_LENGTH|Unterstützt|  
|SQL_DESC_LITERAL_PREFIX|Unterstützt|  
|SQL_DESC_LITERAL_SUFFIX|Unterstützt|  
|SQL_DESC_LOCAL_TYPE_NAME|Nicht unterstützt (gibt leere Zeichenfolge)|  
|SQL_DESC_NAME|Unterstützt|  
|SQL_DESC_NULLABLE|Unterstützt<br /><br /> **Hinweis** in Versionen vor Jet 4.0 nicht unterstützt|  
|SQL_DESC_NUM_PREC_RADIX|Unterstützt|  
|SQL_DESC_OCTET_LENGTH|Unterstützt|  
|SQL_DESC_OCTET_LENGTH_PTR|Unterstützt|  
|SQL_DESC_PARAMETER_TYPE|Nur Eingabeparameter|  
|SQL_DESC_PRECISION|Unterstützt|  
|SQL_DESC_SCALE|Unterstützt|  
|SQL_DESC_SCHEMA_NAME|Nicht unterstützt|  
|SQL_DESC_SEARCHABLE|Unterstützt|  
|SQL_DESC_TABLE_NAME|Nicht unterstützt|  
|SQL_DESC_TYPE|Unterstützt|  
|SQL_DESC_TYPE_NAME|Unterstützt|  
|SQL_DESC_UNNAMED|Unterstützt|  
|SQL_DESC_UNSIGNED|Unterstützt|  
|SQL_DESC_UPDATABLE|Unterstützt|
