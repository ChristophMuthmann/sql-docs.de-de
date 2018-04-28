---
title: Große benutzerdefinierte CLR-Typen (OLE DB) | Microsoft Docs
description: Große benutzerdefinierte CLR-Typen (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e3aaddc3ac658c0a7d713933b6594c1c3a27e88f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="large-clr-user-defined-types-ole-db"></a>Große benutzerdefinierte CLR-Typen (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In diesem Thema werden die Änderungen an OLE DB in OLE DB-Treiber für SQL Server zur Unterstützung großer common Language Runtime (CLR) eine benutzerdefinierte Typen (UDTs) erläutert.  
  
 Weitere Informationen zur Unterstützung großer CLR-UDTs in OLE DB-Treiber für SQL Server finden Sie unter [Large CLR User-Defined Typen](../../oledb/features/large-clr-user-defined-types.md). Ein Beispiel finden Sie unter [Verwendung großer CLR-UDTs &#40;OLE DB-&#41;](../../oledb/ole-db-how-to/use-large-clr-udts-ole-db.md).  
  
## <a name="data-format"></a>Datenformat  
 OLE DB-Treiber für SQL Server verwendet ~ 0, um die Länge der Werte darstellen, die keine größenbeschränkung für große Objekttypen (LOB) zugeordnet sind. ~0 stellt auch die Größe von CLR-UDTs dar, die größer als 8.000 Byte sind.  
  
 In der folgenden Tabelle wird die Datentypzuordnung in Parametern und Rowsets dargestellt:  
  
|SQL Server-Datentyp|OLE DB-Datentyp|Speicherlayout|Wert|  
|--------------------------|----------------------|-------------------|-----------|  
|CLR-UDT|DBTYPE_UDT|BYTE [] (Byte-array\)|132 ("OleDb.h")|  
  
 UDT-Werte werden als Bytearrays dargestellt. Konvertierungen zu und von hexadezimalen Zeichenfolgen werden unterstützt. Literalwerte werden mit dem Präfix 0x als hexadezimale Zeichenfolgen dargestellt. Eine Hexadezimalzeichenfolge ist die Textdarstellung der Binärdaten zur Basis 16. Ein Beispiel ist eine Konvertierung vom Servertyp **varbinary(10)** an DBTYPE_STR, was dazu führt, in hexadezimaler Darstellung von 20 Zeichen, wobei jedes Zeichenpaar ein einzelnes Byte darstellt.  
  
## <a name="parameter-properties"></a>Parametereigenschaften  
 Der DBPROPSET_SQLSERVERPARAMETER-Eigenschaftensatz unterstützt UDTs durch OLE DB. Weitere Informationen finden Sie unter [Defined Types](../../oledb/features/using-user-defined-types.md).  
  
## <a name="column-properties"></a>Spalteneigenschaften  
 Der DBPROPSET_SQLSERVERCOLUMN-Eigenschaftensatz unterstützt die Erstellung von Tabellen durch OLE DB. Weitere Informationen finden Sie unter [Defined Types](../../oledb/features/using-user-defined-types.md).  
  
## <a name="data-type-mapping-in-itabledefinitioncreatetable"></a>Datentypzuordnung zu ITableDefinition::CreateTable  
 Die folgende Informationen werden in **DBCOLUMNDESC** Strukturen von itabledefinition:: CreateTable verwendet werden, wenn UDT-Spalten erforderlich sind:  
  
|OLE DB-Datentyp (*wType*)|*pwszTypeName*|SQL Server-Datentyp|*rgPropertySets*|  
|----------------------------------|--------------------|--------------------------|----------------------|  
|DBTYPE_UDT|Wird ignoriert.|UDT|Muss einen DBPROPSET_SQLSERVERCOLUMN-Eigenschaftensatz einschließen.|  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 Informationen zurückgegeben, in der DBPARAMINFO-Struktur durch **PrgParamInfo** lautet wie folgt:  
  
|Parametertyp|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*DwFlags* DBPARAMFLAGS_ISLONG|  
|--------------------|-------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|"DBTYPE_UDT"|*n*|nicht definiert|nicht definiert|Deaktivieren|  
|DBTYPE_UDT<br /><br /> (Länge größer als 8.000 Bytes)|"DBTYPE_UDT"|~0|nicht definiert|nicht definiert|Menge|  
  
## <a name="icommandwithparameterssetparameterinfo"></a>ICommandWithParameters::SetParameterInfo  
 Die in der DBPARAMBINDINFO-Struktur bereitgestellten Informationen müssen Folgendem entsprechen:  
  
|Parametertyp|*pwszDataSourceType*|*ulParamSize*|*bPrecision*|*bScale*|*DwFlags* DBPARAMFLAGS_ISLONG|  
|--------------------|--------------------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|DBTYPE_UDT|*n*|wird ignoriert.|wird ignoriert.|Muss festgelegt werden, wenn der Parameter mit DBTYPE_IUNKNOWN übergeben werden soll.|  
|DBTYPE_UDT<br /><br /> (Länge größer als 8.000 Bytes)|DBTYPE_UDT|~0|wird ignoriert.|wird ignoriert.|wird ignoriert.|  
  
## <a name="isscommandwithparameters"></a>ISSCommandWithParameters  
 Verwenden Sie die Anwendungen **ISSCommandWithParameters** abrufen und die im Abschnitt Parametereigenschaften definierten Parametereigenschaften festlegen.  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 Spalten, die zurückgegeben werden wie folgt:  
  
|Spaltentyp|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE|DBCOLUMN_FLAGS_ISLONG|DBCOLUMNS_ISSEARCHABLE|DBCOLUMN_OCTETLENGTH|  
|-----------------|--------------------|--------------------------|-------------------------|---------------------|-----------------------------|-----------------------------|---------------------------|  
|DBTYPE_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|DBTYPE_UDT|*n*|NULL|NULL|Löschen|DB_ALL_EXCEPT_LIKE|n|  
|DBTYPE_UDT<br /><br /> (Länge größer als 8.000 Bytes)|DBTYPE_UDT|~0|NULL|NULL|Legen Sie|DB_ALL_EXCEPT_LIKE|0|  
  
 Die folgenden Spalten werden ebenfalls für UDTs definiert:  
  
|Spalten-ID|Typ|Description|  
|-----------------------|----------|-----------------|  
|DBCOLUMN_UDT_CATALOGNAME|DBTYPE_WSTR|Für UDT-Spalten der Name des Katalogs, in dem der UDT definiert ist.|  
|DBCOLUMN_UDT_SCHEMANAME|DBTYPE_WSTR|Für UDT-Spalten der Name des Schemas, in dem der UDT definiert ist.|  
|DBCOLUMN_UDT_NAME|DBTYPE_WSTR|Für UDT-Spalten der einteilige Name des UDT.|  
|DBCOLUMN_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Für UDT-Spalten der vollständige Typname des UDT. Mit dem vollqualifizierten Namen des Assemblytyps können Sie ein Objekt dieses Typs mit der Type.GetType-Methode instanziieren.|  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 Die in der DBCOLUMNINFO-Struktur zurückgegebenen Informationen lauten wie folgt:  
  
|Parametertyp|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBCOLUMNFLAGS_ISLONG|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------|  
|DBTYPE_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|DBTYPE_UDT|*n*|~0|~0|Löschen|  
|DBTYPE_UDT<br /><br /> (Länge größer als 8.000 Bytes)|DBTYPE_UDT|~0|~0|~0|Legen Sie|  
  
## <a name="columns-rowset-schema-rowsets"></a>COLUMNS-Rowset (Schemarowsets)  
 Die folgenden Spaltenwerte werden für UDT-Typen zurückgegeben:  
  
|Spaltentyp|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_ISLONG|CHARACTER_OCTET_LENGTH|  
|-----------------|----------------|-----------------------------------------|------------------------------|  
|DBTYPE_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|DBTYPE_UDT|Löschen|*n*|  
|DBTYPE_UDT<br /><br /> (Länge größer als 8.000 Bytes)|DBTYPE_UDT|Legen Sie|0|  
  
 Die folgenden zusätzlichen Spalten werden für UDTs definiert:  
  
|Spalten-ID|Typ|Description|  
|-----------------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Für UDT-Spalten der Name des Katalogs, in dem der UDT definiert ist.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Für UDT-Spalten der Name des Schemas, in dem der UDT definiert ist.|  
|SS_UDT_NAME|DBTYPE_WSTR|Für UDT-Spalten der einteilige Name des UDT.|  
|SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Für UDT-Spalten ist dies der vollständige Typname des UDT. Mit dem vollqualifizierten Namen des Assemblytyps können Sie ein Objekt dieses Typs mit der Type.GetType-Methode instanziieren.|  
  
 Im Hinblick auf das PROCEDURE_PARAMETERS-Rowset enthält DATA_TYPE die gleichen Werte wie das COLUMNS-Schemarowset, und TYPE_NAME enthält den UDT. Es werden die gleichen zusätzlichen Spalten definiert.  
  
 UDTs werden nicht im PROVIDER_TYPES-Schemarowset angezeigt.  
  
## <a name="bindings-and-conversions"></a>Bindungen und Konvertierungen  
  
|Binding-Datentyp|UDT zu Server|Nicht-UDT zu Server|UDT von Server|Nicht-UDT von Server|  
|----------------------|-------------------|------------------------|---------------------|--------------------------|  
|DBTYPE_UDT|Unterstützte (5)|Fehler (1)|Unterstützte (5)|Fehler (4)|  
|DBTYPE_BYTES|Unterstützte (5)|–|Unterstützte (5)|–|  
|DBTYPE_WSTR|Unterstützt (2), (5)|–|Unterstützt (3), (5), (6)|–|  
|DBTYPE_BSTR|Unterstützt (2), (5)|–|Unterstützte (3), (5)|–|  
|DBTYPE_STR|Unterstützt (2), (5)|–|Unterstützte (3), (5)|–|  
|DBTYPE_IUNKNOWN|Unterstützte (6)|–|Unterstützte (6)|–|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|Unterstützt (5)|–|Unterstützte (3), (5)|–|  
|DBTYPE_VARIANT (VT_BSTR)|Unterstützt (2), (5)|–|–|–|  
  
### <a name="key-to-symbols"></a>Aufschlüsselung der Symbole  
  
|Symbol|Bedeutung|  
|------------|-------------|  
|1|Wenn ein anderer Servertyp als DBTYPE_UDT mit Indexparametern **ICommandWithParameters:: SetParameterInfo** und ist der Accessortyp DBTYPE_UDT, ein Fehler auftritt, wenn die Anweisung ausgeführt wird.  Der Fehler lautet DB_E_ERRORSOCCURRED, und der Parameterstatus lautet DBSTATUS_E_BADACCESSOR.<br /><br /> Es tritt ein Fehler auf, wenn ein Parameter des Typs UDT für einen Serverparameter angegeben wird, bei dem es sich nicht um einen UDT handelt.|  
|2|Daten werden von einer hexadezimalen Zeichenfolge in binäre Daten konvertiert.|  
|3|Daten werden von binären Daten in eine hexadezimale Zeichenfolge konvertiert.|  
|4|Überprüfung kann auftreten, wenn mit **CreateAccessor** oder **GetNextRows**. Der Fehler lautet DB_E_ERRORSOCCURRED. Der Bindungsstatus wird auf DBBINDSTATUS_UNSUPPORTEDCONVERSION festgelegt.|  
|5|BY_REF kann verwendet werden.|  
|6|UDT-Parameter können als DBTYPE_IUNKNOWN im DBBINDING gebunden werden. Binden an DBTYPE_IUNKNOWN gibt an, dass die Anwendung wünscht zum Verarbeiten der Daten als Stream mithilfe von ISequentialStream-Schnittstelle. Wenn ein Consumer gibt *wType* in einer Bindung als Typ DBTYPE_IUNKNOWN fest, und der entsprechenden Spalte oder die Ausgabe-Parameter der gespeicherten Prozedur ein UDT ist, OLE DB-Treiber für SQL Server einer ISequentialStream-Schnittstelle zurück. OLE DB-Treiber für SQL Server werden Abfragen für einen Eingabeparameter für das für die ISequentialStream-Schnittstelle.<br /><br /> Sie können auswählen, ob die Länge der UDT-Daten bei Verwendung der DBTYPE_IUNKNOWN-Bindung im Falle großer UDTs gebunden werden soll. Die Länge muss für kleine UDTs jedoch gebunden sein. Ein DBTYPE_UDT-Parameter kann als großer UDT angegeben werden, wenn mindestens eine der folgenden Bedingungen zutrifft:<br />*ulParamParamSize* is ~0.<br />DBPARAMFLAGS_ISLONG ist in der DBPARAMBINDINFO-Struktur festgelegt.<br /><br /> Für Zeilendaten ist die DBTYPE_IUNKNOWN-Bindung nur für große UDTs zulässig. Sie können herauszufinden, ob eine Spalte einen großen UDT-Typ ist, mit der IColumnsInfo:: GetColumnInfo-Methode für ein Rowset oder Befehl IColumnsInfo-Schnittstelle des Objekts. Eine DBTYPE_UDT-Spalte ist eine große UDT-Spalte, wenn mindestens eine der folgenden Bedingungen zutrifft:<br />Das DBCOLUMNFLAGS_ISLONG-Flag wird festgelegt, *DwFlags* -Element der DBCOLUMNINFO-Struktur. <br />*UlColumnSize* -Element von DBCOLUMNINFO ist ~ 0.|  
  
 DBTYPE_NULL und DBTYPE_EMPTY können für Eingabeparameter gebunden werden, jedoch nicht für Ausgabeparameter oder Ergebnisse. Ist der Status für Eingabeparameter gebunden, muss er auf DBSTATUS_S_ISNULL für DBTYPE_NUL oder DBSTATUS_S_DEFAULT für DBTYPE_EMPTY festgelegt werden. DBTYPE_BYREF kann nicht mit DBTYPE_NULL oder DBTYPE_EMPTY verwendet werden.  
  
 DBTYPE_UDT kann auch in DBTYPE_EMPTY und DBTYPE_NULL konvertiert werden. DBTYPE_NULL und DBTYPE_EMPTY können jedoch nicht in DBTYPE_UDT konvertiert werden. Dies stimmt mit DBTYPE_BYTES überein. **ISSCommandWithParameters** Prozess UDTs als Parameter verwendet wird.  
  
 Datenkonvertierungen durch OLE DB-Basisdienste (**IDataConvert**) sind nicht in DBTYPE_UDT anwendbar.  
  
 Es werden keine weiteren Bindungen unterstützt.  
  
## <a name="comparability-for-irowsetfind"></a>Vergleichbarkeit für 'IRowsetFind'  
 Für UDT-Typen werden lediglich die folgenden Vergleiche unterstützt:  
  
-   EQ  
  
-   NE  
  
-   IGNORE  
  
 Beim Versuch eines anderen Vergleichs wird DB_E_BADCOMPAREOP zurückgegeben.  
  
## <a name="bcp-support-for-udts"></a>BCP-Unterstützung für UDTs  
 UDT-Werte importiert, und nur als Zeichen- oder Binärwerte exportiert werden können.  
  
## <a name="down-level-client-behavior-for-udts"></a>Verhalten von Downlevelclients für UDTs  
 Für UDTs gilt die folgende Typzuordnung zu Clients der unteren Ebene:  
  
|Clientversion|DBTYPE_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|DBTYPE_UDT<br /><br /> (Länge größer als 8.000 Bytes)|  
|--------------------|------------------------------------------------------------------|---------------------------------------------------------|  
|SQL Server 2005|UDT|varbinary(max)|  
|SQL Server 2008 und höher|UDT|UDT|  
  
 Wenn **DataTypeCompatibility** (SSPROP_INIT_DATATYPECOMPATIBILITY) auf "80" festgelegt ist, große UDT-Typen für Clients angezeigt werden, auf die gleiche Weise, die sie für Clients der unteren Ebenen angezeigt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Große benutzerdefinierte CLR-Typen](../../oledb/features/large-clr-user-defined-types.md)  
  
  

