---
title: Treiber für Deskriptoren und Desktop-Datenbank | Microsoft Docs
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
- desktop database drivers [ODBC], descriptors
- Jet-based ODBC drivers [ODBC], descriptors
- descriptors [ODBC], Jet-supported descriptor fields
- ODBC desktop database drivers [ODBC], descriptors
ms.assetid: 9ae2d9b5-365f-4f0a-9116-defe9498b401
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62d827aecfb8b8fdf593291ce179f5c93d638dc1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="descriptors-and-desktop-database-drivers"></a>Deskriptoren und Desktop-Datenbanktreiber
Ein Deskriptor ist eine Datenstruktur, die Informationen zum Spaltendaten oder dynamische Parameter enthält. **SQLGetDescField** können verwendet werden, um die unten aufgeführten unterstützten Deskriptoren abzurufen. Implementierung Parameter Deskriptoren (Implementierungsparameterdeskriptor, Implementierungszeilendeskriptor) werden nicht automatisch aufgefüllt, da **SQLDescribeParam** wird nicht unterstützt. Deskriptorfelder, die über Jet (z. B. SQL_DESC_BASE_TABLE_NAME) nicht verfügbar sind, werden ebenfalls nicht unterstützt.  
  
 Weitere Informationen zu unterstützten Jet deskriptorfelder, finden Sie unter der *Microsoft Jet-Datenbank-Engine-Programmiererhandbuch*.  
  
 Weitere Informationen zu Deskriptoren, finden Sie unter den Themen unter "Deskriptoren" in der *ODBC Programmer's Reference*.  
  
|Deskriptorfelder|Supportebene|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Supported|  
|SQL_DESC_ARRAY_SIZE|Nur für ARD unterstützt|  
|SQL_DESC_ARRAY_STATUS_PTR|Supported|  
|SQL_DESC_BIND_OFFSET_PTR|Supported|  
|SQL_DESC_BIND_TYPE|Supported|  
|SQL_DESC_COUNT|Supported|  
|SQL_DESC_ROWS_PROCESSED_PTR|Nur für ARD unterstützt|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Supported|  
|SQL_DESC_BASE_COLUMN_NAME|Unterstützt (neu)|  
|SQL_DESC_BASE_TABLE_NAME|Unterstützt (neu)|  
|SQL_DESC_CASE_SENSITIVE|Immer "false"|  
|SQL_DESC_CATALOG_NAME|Nicht unterstützt|  
|SQL_DESC_CONCISE_TYPE|Supported|  
|SQL_DESC_DATA_PTR|Supported|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Supported|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Für die Intervall-C-Typen unterstützt|  
|SQL_DESC_DISPLAY_SIZE|Supported|  
|SQL_DESC_FIXED_PREC_SCALE|Unterstützte ("true" für Money)|  
|SQL_DESC_INDICATOR_PTR|Supported|  
|SQL_DESC_LABEL|Supported|  
|SQL_DESC_LENGTH|Supported|  
|SQL_DESC_LITERAL_PREFIX|Supported|  
|SQL_DESC_LITERAL_SUFFIX|Supported|  
|SQL_DESC_LOCAL_TYPE_NAME|Nicht unterstützt (gibt leere Zeichenfolge)|  
|SQL_DESC_NAME|Supported|  
|SQL_DESC_NULLABLE|Supported<br /><br /> **Hinweis** in Versionen vor Jet 4.0 nicht unterstützt|  
|SQL_DESC_NUM_PREC_RADIX|Supported|  
|SQL_DESC_OCTET_LENGTH|Supported|  
|SQL_DESC_OCTET_LENGTH_PTR|Supported|  
|SQL_DESC_PARAMETER_TYPE|Nur Eingabeparameter|  
|SQL_DESC_PRECISION|Supported|  
|SQL_DESC_SCALE|Supported|  
|SQL_DESC_SCHEMA_NAME|Nicht unterstützt|  
|SQL_DESC_SEARCHABLE|Supported|  
|SQL_DESC_TABLE_NAME|Nicht unterstützt|  
|SQL_DESC_TYPE|Supported|  
|SQL_DESC_TYPE_NAME|Supported|  
|SQL_DESC_UNNAMED|Supported|  
|SQL_DESC_UNSIGNED|Supported|  
|SQL_DESC_UPDATABLE|Supported|
