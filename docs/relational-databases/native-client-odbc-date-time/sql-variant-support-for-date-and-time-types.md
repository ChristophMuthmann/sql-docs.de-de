---
title: "Sql_variant-Unterstützung für Datums- und Uhrzeittypen | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: sql_variant data type
ms.assetid: 12ff1ea6-e2cc-40e6-910c-3126974a90b3
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e7df17e376cad6f84580bc2593413a578db0608
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="sqlvariant-support-for-date-and-time-types"></a>Sql_variant-Unterstützung für Datums- und Uhrzeittypen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In diesem Thema wird beschrieben, wie die **Sql_variant** Datentyp unterstützt die verbesserte Datums- und Uhrzeitfunktionalität.  
  
 Das Spaltenattribut SQL_CA_SS_VARIANT_TYPE wird zur Rückgabe des C-Typs einer Variant-Ergebnisspalte verwendet. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]führt zusätzlich das Attribut sql_ca_ss_variant_sql_type eingeführt, mit dem der SQL-Typ einer variant-Ergebnisspalte in den Implementierungszeilendeskriptor (IRD) festgelegt. SQL_CA_SS_VARIANT_SQL_TYPE kann auch in Implementation Parameter Descriptor (Implementierungsparameterdeskriptor, Implementierungszeilendeskriptor) verwendet werden, an die SQL-Typ, der eine SQL_SS_TIME2 oder SQL_SS_TIMESTAMPOFFSET-Parameter, der C-Typ SQL_C_BINARY ist mit dem Typ SQL_SS_VARIANT gebunden.  
  
 Die neuen Typen SQL_SS_TIME2 und SQL_SS_TIMESTAMPOFFSET können vom SQLColAttribute festgelegt werden. SQL_CA_SS_VARIANT_SQL_TYPE kann von SQLGetDescField zurückgegeben werden.  
  
 Für Ergebnisspalten konvertiert der Treiber Daten von Variant- zu Datum-/Uhrzeit-Typen. Weitere Informationen finden Sie unter [Konvertierungen von SQL-in C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md). Wenn Spalten an SQL_C_BINARY gebunden werden, muss die Pufferlänge so groß sein, dass der Puffer die dem SQL-Typ entsprechende Struktur aufnehmen kann.  
  
 Für die SQL_SS_TIME2 und SQL_SS_TIMESTAMPOFFSET-Parameter konvertiert der Treiber C-Werte in **Sql_variant** Werte, wie in der folgenden Tabelle beschrieben. Wenn ein Parameter als SQL_C_BINARY gebunden ist und der Servertyp SQL_SS_VARIANT lautet, dann wird er als Binärwert behandelt, sofern die Anwendung SQL_CA_SS_VARIANT_SQL_TYPE nicht auf einen anderen SQL-Typ festgelegt hat. In diesem Fall hat QL_CA_SS_VARIANT_SQL_TYPE Vorrang; d. h. wenn SQL_CA_SS_VARIANT_SQL_TYPE festgelegt wurde, wird damit das Standardverhalten überschrieben, wonach der SQL-Varianttyp vom C-Typ abgeleitet wird.  
  
|C-Typ|Servertyp|Kommentare|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_WCHAR|nvarcar|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_TINYINT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_STINYINT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_SHORT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_SSHORT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_USHORT|int|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_LONG|int|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_SLONG|int|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_ULONG|bigint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_SBIGINT|bigint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_FLOAT|real|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_DOUBLE|float|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_BIT|bit|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_UTINYINT|tinyint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_BINARY|varbinary|SQL_CA_SS_VARIANT_SQL_TYPE wird nicht festgelegt.|  
|SQL_C_BINARY|Uhrzeit|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> Skalierungsgruppe wird auf SQL_DESC_PRECISION (den *DecimalDigits* Parameter **SQLBindParameter**).|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> Skalierungsgruppe wird auf SQL_DESC_PRECISION (den *DecimalDigits* Parameter **SQLBindParameter**).|  
|SQL_C_TYPE_DATE|Datum|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_TYPE_TIME|time(0)|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_TYPE_TIMESTAMP|datetime2|Skalierungsgruppe wird auf SQL_DESC_PRECISION (den *DecimalDigits* Parameter **SQLBindParameter**).|  
|SQL_C_NUMERIC|Decimal|Genauigkeit ist festgelegt auf SQL_DESC_PRECISION (den *ColumnSize* Parameter **SQLBindParameter**).<br /><br /> Legen Sie die Skalierung auf SQL_DESC_SCALE (den *DecimalDigits* -Parameter von SQLBindParameter).|  
|SQL_C_SS_TIME2|Uhrzeit|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datum und Uhrzeit-Verbesserungen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
