---
title: Neue Uhrzeitfunktionen zu Datum und mit früheren SQL Server-Versionen (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5cb50889a9cb584e5f22d5f2e77960dba567fda1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>Neue Uhrzeitfunktionen zu Datum und mit früheren SQL Server-Versionen (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Dieses Thema beschreibt das erwartete Verhalten, bei der Kommunikation einer Clientanwendung, die verbesserte Datums- und Uhrzeitfunktionen verwendet mit einer Version von zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], und wenn ein Client mit einer Version von kompiliert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client vor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] sendet Befehle an einen Server, der verbesserte Datums- und Uhrzeitfunktionen unterstützt.  
  
## <a name="down-level-client-behavior"></a>Downlevelclient-Verhalten  
 Clientanwendungen, die eine von Version [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client vor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] finden Sie unter der neuen Datums-/Uhrzeittypen als **Nvarchar** Spalten. Die Spalten enthalten literale Darstellungen. Weitere Informationen finden Sie im Abschnitt "Datenformate: Zeichenfolgen und Literale" [Datentypunterstützung für OLE DB-Datum und Uhrzeit-Verbesserungen](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md). Die Spaltengröße ist die maximale Literallänge für die Genauigkeit, die für die Spalte festgelegt wurde.  
  
 Katalog-APIs geben Metadaten zurück konsistent mit der niedrigeren datentypcode an den Client zurückgegeben (z. B. **Nvarchar**) und der zugeordneten Darstellung früherer (z. B. das entsprechende Literalformat). Der zurückgegebene Datentypname ist jedoch der echte [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]-Typname.  
  
 Wenn eine kompatibler Client-Anwendung ausgeführt wird, anhand einer [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (oder höher) Server, an dem schemaänderungen an Datums-/Uhrzeittypen vorgenommen wurden, das erwartete Verhalten lautet wie folgt:  
  
|OLE DB-Clienttyp|SQL Server 2005-Typ|SQL Server 2008 (oder höher)-Typ|Ergebniskonvertierung (Server zu Client)|Parameterkonvertierung (Client zu Server)|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|Datetime|Datum|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Zeitfelder werden auf 0 (Null) festgelegt.|IRowsetChange schlägt auch fehl, weil die Zeichenfolge abgeschnitten, wenn das Zeitfeld ungleich 0 (null) ist.|  
|DBTYPE_DBTIME||Time(0)|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Datumsfelder werden auf das aktuelle Datum festgelegt.|IRowsetChange schlägt auch fehl, weil die Zeichenfolge abgeschnitten, wenn Sekundenbruchteile ungleich NULL sind.<br /><br /> Datum wird ignoriert.|  
|DBTYPE_DBTIME||Time(7)|Fehler. Ungültiges Zeitliteral.|OK|  
|DBTYPE_DBTIMESTAMP|||Fehler. Ungültiges Zeitliteral.|OK|  
|DBTYPE_DBTIMESTAMP||Datetime2(3)|OK|OK|  
|DBTYPE_DBTIMESTAMP||Datetime2(7)|OK|OK|  
|DBTYPE_DBDATE|Smalldatetime|Datum|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Zeitfelder werden auf 0 (Null) festgelegt.|IRowsetChange schlägt auch fehl, weil die Zeichenfolge abgeschnitten, wenn das Zeitfeld ungleich 0 (null) ist.|  
|DBTYPE_DBTIME||Time(0)|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Datumsfelder werden auf das aktuelle Datum festgelegt.|IRowsetChange schlägt auch fehl, weil die Zeichenfolge abgeschnitten, wenn Sekundenbruchteile ungleich NULL sind.<br /><br /> Datum wird ignoriert.|  
|DBTYPE_DBTIMESTAMP||Datetime2(0)|OK|OK|  
  
 'OK' bedeutet, dass sich die Funktionsweise von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (oder höher) nicht unterscheidet.  
  
 Nur die folgenden allgemeinen Schemaänderungen wurden berücksichtigt:  
  
-   Verwenden eines neuen Typs, wenn eine Anwendung logisch nur einen Datums- oder Zeitwert erfordert. Die Anwendung musste jedoch mit **"DateTime"** oder **Smalldatetime** da separate Datums- und Uhrzeittypen waren nicht verfügbar.  
  
-   Verwenden eines neuen Typs, um zusätzliche Genauigkeit in Sekundenbruchteilen zu erzielen.  
  
-   Wechsel zu **datetime2** , da dies der bevorzugte Datentyp für Datum und Uhrzeit ist.  
  
 Anwendungen, die über ICommandWithParameters:: GetParameterInfo oder Schema Rowsets bezogenen Metadaten zu verwenden, um Informationen zum Parametertyp über ICommandWithParameters:: SetParameterInfo festzulegen werden schlagen bei clientkonvertierungen fehl, auf dem die Zeichenfolge Darstellung eines Datentyps für die Quelle ist größer als die Zeichenfolgendarstellung des Zieltyps. Wenn eine Clientbindung DBTYPE_DBTIMESTAMP verwendet und die Serverspalte Date, beispielsweise [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client wandelt den Wert "Yyyy-Dd-mm-ss.fff", jedoch werden die Metadaten als zurückgegeben **nvarchar(10)**. Der resultierende Überlauf löst DBSTATUS_E_CATCONVERTVALUE aus. Ähnliche Probleme treten bei datenkonvertierungen durch IRowsetChange, da die rowsetmetadaten von den resultsetmetadaten festgelegt ist.  
  
### <a name="parameter-and-rowset-metadata"></a>Metadaten für Parameter und Rowsets  
 Dieser Abschnitt beschreibt die Metadaten für Parameter, Ergebnisspalten und Schemarowsets für Clients, die mit einer Version kompiliert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client vor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 Die DBPARAMINFO-Struktur gibt die folgende Informationen über die *PrgParamInfo* Parameter:  
  
|Parametertyp|wType|ulParamSize|bPrecision|bscale|  
|--------------------|-----------|-----------------|----------------|------------|  
|Datum|DBTYPE_WSTR|10|~0|~0|  
|Uhrzeit|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
 Beachten Sie, dass einige dieser Wertbereiche nicht fortlaufend sind; z. B. fehlt 9 in 8,10..16. Der Grund dafür ist das Hinzufügen eines Dezimaltrennzeichens, wenn die Genauigkeit von Bruchteilen größer als 0 (NULL) ist.  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 Folgende Spalten werden zurückgegeben:  
  
|Spaltentyp|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|Datum|DBTYPE_WSTR|10|NULL|NULL|  
|Uhrzeit|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 Die DBCOLUMNINFO-Struktur gibt die folgende Informationen zurück:  
  
|Parametertyp|wType|ulColumnSize|bPrecision|bscale|  
|--------------------|-----------|------------------|----------------|------------|  
|Datum|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
### <a name="schema-rowsets"></a>Schemarowsets  
 In diesem Abschnitt werden Metadaten für Parameter, Ergebnisspalten und Schemarowsets für neue Datentypen beschrieben. Diese Informationen sind nützlich ist, stehen Ihnen einen Client-Anbieter entwickelt wurde, mithilfe der Tools vor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
#### <a name="columns-rowset"></a>COLUMNS-Rowset  
 Die folgenden Spaltenwerte werden für date/time-Typen zurückgegeben:  
  
|Spaltentyp|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|Datum|DBTYPE_WSTR|10|20|NULL|  
|Uhrzeit|DBTYPE_WSTR|8, 10..16|16,20..32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|NULL|  
  
#### <a name="procedureparameters-rowset"></a>PROCEDURE_PARAMETERS-Rowset  
 Die folgenden Spaltenwerte werden für date/time-Typen zurückgegeben:  
  
|Spaltentyp|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|Datum|DBTYPE_WSTR|10|20|Datum|  
|Uhrzeit|DBTYPE_WSTR|8, 10..16|16,20..32|Uhrzeit|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|datetime|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|datetimeoffset|  
  
#### <a name="providertypes-rowset"></a>PROVIDER_TYPES-Rowset  
 Die folgenden Zeilen werden für date/time-Typen zurückgegeben:  
  
|Typ -><br /><br /> Column|Datum|Uhrzeit|smalldatetime|datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|Datum|Uhrzeit|smalldatetime|datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_WSTR|DBTYPE_WSTR|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_WSTR|DBTYPE_WSTR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|Datum|Uhrzeit|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_TRUE|VARIANT_FALSE|VARIANT_FALSE|  
|IS_FIXEDLENGTH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
  
## <a name="down-level-server-behavior"></a>Downlevelserver-Verhalten  
 Beim Verbinden mit einem Server einer früheren Version als [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], führt jeder Versuch, verwenden die neuen servertypnamen (z. B. mit ICommandWithParameters:: SetParameterInfo oder itabledefinition:: CreateTable) db_e_badtypename.  
  
 Wenn neue Typen für Parameter oder Ergebnisse ohne Verwendung eines Typnamens gebunden werden, und entweder der neue Typ verwendet wird, um den Servertyp implizit festzulegen, oder keine gültige Konvertierung vom Servertyp zum Clienttyp vorhanden ist, wird DB_E_ERRORSOCCURRED zurückgegeben, und DBBINDSTATUS_UNSUPPORTED_CONVERSION wird als Bindungsstatus für den bei der Ausführung verwendeten Accessor festgelegt.  
  
 Alle Clientpuffertypen können verwendet werden, wenn eine Clientkonvertierung vom Puffertyp zum Servertyp für die Serverversion dieser Verbindung unterstützt wird. In diesem Kontext *Servertyp* bedeutet, dass der Typ von ICommandWithParameters:: SetParameterInfo angegeben ist oder von dem Puffertyp impliziert wird, wenn ICommandWithParameters:: SetParameterInfo nicht aufgerufen wurde. Das bedeutet, dass DBTYPE_DBTIME2 und DBTYPE_DBTIMESTAMPOFFSET mit Servern früherer Versionen verwendet werden können, wenn DataTypeCompatibility auf 80 festgelegt und die Clientkonvertierung zu einem unterstützten Servertyp erfolgreich ist. Wenn der Servertyp inkorrekt ist, gibt der Server einen Fehler zurück, wenn er eine implizite Konvertierung in den tatsächlichen Servertyp nicht durchführen kann.  
  
## <a name="sspropinitdatatypecompatibility-behavior"></a>SSPROP_INIT_DATATYPECOMPATIBILITY-Verhalten  
 Wenn SSPROP_INIT_DATATYPECOMPATIBILITY auf SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000 festgelegt ist, die neuen Datums-/Uhrzeittypen und die zugeordneten Metadaten angezeigt werden für Clients für Downlevelclients, erscheinen in beschriebenen [Massenkopieränderungen für Erweiterte Datums- und Uhrzeittypen &#40;OLE DB- und ODBC-&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
## <a name="comparability-for-irowsetfind"></a>Vergleichbarkeit für 'IRowsetFind'  
 Alle Vergleichsoperatoren sind für die neuen Datums-/Uhrzeittypen zulässig, da Sie als Zeichenfolgetypen anstatt als Datums-/Uhrzeittypen angezeigt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Datum und Uhrzeit-Verbesserungen & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
