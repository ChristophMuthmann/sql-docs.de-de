---
title: Datum und Uhrzeit und Schemarowsets | Microsoft Docs
description: Datum und Uhrzeit und Schema rowsets
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5d345da0ec86ecbc92d43bc355b0f1376934cb0b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="metadata---date-and-time-and-schema-rowsets"></a>Metadaten: Datum und Uhrzeit und Schemarowsets
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Dieses Thema enthält Informationen über das COLUMNS-Rowset und das PROCEDURE_PARAMETERS-Rowset. Diese Informationen beziehen sich auf die OLE DB-Verbesserungen in [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] in Bezug auf Datum und Uhrzeit.  
  
## <a name="columns-rowset"></a>COLUMNS-Rowset  
 Die folgenden Spaltenwerte werden für date/time-Typen zurückgegeben:  
  
|Spaltentyp|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_SS_ISVARIABLESCALE|DATETIME_PRECISION|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|Datum|DBTYPE_DBDATE|Löschen|0|  
|Uhrzeit|DBTYPE_DBTIME2|Legen Sie|0..7|  
|smalldatetime|DBTYPE_DBTIMESTAMP|Löschen|0|  
|datetime|DBTYPE_DBTIMESTAMP|Löschen|3|  
|datetime2|DBTYPE_DBTIMESTAMP|Legen Sie|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|Legen Sie|0..7|  
  
 In COLUMN_FLAGS hat DBCOLUMNFLAGS_ISFIXEDLENGTH für Datum-/Uhrzeittypen stets den Wert TRUE, und die folgenden Flags haben immer den Wert FALSE:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 Die übrigen Flags (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE und DBCOLUMNFLAGS_WRITEUNKNOWN) können festgelegt werden. Dies hängt von der Definition der Spalte ab.  
  
 Das neue DBCOLUMNFLAGS_SS_ISVARIABLESCALE-Flag wird in COLUMN_FLAGS bereitgestellt, damit eine Anwendung den Servertyp der Spalten bestimmen kann, wobei DATA_TYPE = DBTYPE_DBTIMESTAMP ist. DATETIME_PRECISION muss ebenfalls verwendet werden, um den Servertyp zu identifizieren.  
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE ist nur gültig, wenn es sich bei einer Verbindung mit einem [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Server oder höher. DBCOLUMNFLAGS_SS_ISFIXEDSCALE ist nicht definiert, wenn eine Verbindung mit einem Downlevelserver besteht.  
  
## <a name="procedureparameters-rowset"></a>PROCEDURE_PARAMETERS-Rowset  
 DATA_TYPE enthält die gleichen Werte wie das COLUMNS-Schemarowset, und TYPE_NAME enthält den Servertyp.  
  
 Die neue Spalte SS_DATETIME_PRECISION wurde hinzugefügt, um die Genauigkeit des Typs wie in der DATETIME_PRECISION-Spalte zurückzugeben, ähnlich wie beim COLUMNS-Rowset.  
  
## <a name="providertypes-rowset"></a>PROVIDER_TYPES-Rowset  
 Die folgenden Zeilen werden für date/time-Typen zurückgegeben:  
  
|Typ -><br /><br /> Column|Datum|Uhrzeit|smalldatetime|datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|Datum|Uhrzeit|smalldatetime|datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_DBDATE|DBTYPE_DBTIME2|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|scale|NULL|NULL|scale|scale|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|Datum|Uhrzeit|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|0|NULL|NULL|0|0|  
|MAXIMUM_SCALE|NULL|7|NULL|NULL|7|7|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE, außer wenn eine der folgenden Aussagen zutrifft:<br /><br /> Der Client ist mit einem Downlevelserver verbunden.<br /><br /> Die Verbindungseigenschaft für die Datentypkompatibilität gibt einen Kompatibilitätsgrad von 80 an.|VARIANT_TRUE, außer wenn eine der folgenden Aussagen zutrifft:<br /><br /> Der Client ist mit einem Downlevelserver verbunden.<br /><br /> Die Verbindungseigenschaft für die Datentypkompatibilität gibt einen Kompatibilitätsgrad von 80 an.|VARIANT_TRUE|  
|IS_FIXEDLENGTH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
  
 OLE DB definiert lediglich MINIMUM_SCALE und MAXIMUM_SCALE für numerische und Dezimaltypen Typen, also OLE DB-Treiber für SQL Server Verwendung dieser Spalten für Time, datetime2 und Datetimeoffset nicht standardmäßige.  
  
## <a name="see-also"></a>Siehe auch  
 [Metadaten &#40;OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
  
  
