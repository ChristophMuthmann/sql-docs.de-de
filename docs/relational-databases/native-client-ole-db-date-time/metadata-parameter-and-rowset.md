---
title: Parameter und Rowsetmetadaten | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- metadata [OLE DB]
ms.assetid: 31b318a4-20e7-4db0-b367-eb9938859029
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7d7d4ee439ff2695ab2094c3e1e4784506173b27
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="metadata---parameter-and-rowset"></a>Metadaten - Parameter und Rowsets
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Dieses Thema enthält Informationen über den folgenden Typ und die folgenden Typelemente in Verbindung mit den OLE DB-Datums- und Uhrzeitverbesserungen.  
  
-   DBBINDING-Struktur  
  
-   **ICommandWithParameters::GetParameterInfo**  
  
-   **ICommandWithParameters::SetParameterInfo**  
  
-   **IColumnsRowset::GetColumnsRowset**  
  
-   **IColumnsInfo::GetColumnInfo**  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 Die folgende Informationen zurückgegeben, in der DBPARAMINFO-Struktur durch *PrgParamInfo*:  
  
|Parametertyp|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|-------------------|------------------|--------------|-----------------------------------------------------|  
|Datum|DBTYPE_DBDATE|6|10|0|Löschen|  
|Uhrzeit|DBTYPE_DBTIME2|10|8, 10..16|0..7|Legen Sie|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Löschen|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|Löschen|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19,21..27|0..7|Legen Sie|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26,28..34|0..7|Legen Sie|  
  
 Beachten Sie, dass in einigen Fällen Wertbereiche nicht kontinuierlich sind. Der Grund dafür ist das Hinzufügen eines Dezimaltrennzeichens, wenn die Genauigkeit von Bruchteilen größer als 0 (NULL) ist.  
  
 DBPARAMFLAGS_SS_ISVARIABLESCALE ist nur gültig, wenn es sich bei einer Verbindung mit einem [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (oder höher) Server. Beim Verbinden mit downlevelserver ist DBPARAMFLAGS_SS_ISVARIABLESCALE nie festgelegt.  
  
## <a name="icommandwithparameterssetparameterinfo-and-implied-parameter-types"></a>ICommandWithParameters::SetParameterInfo und implizite Parametertypen  
 Die in der DBPARAMBINDINFO-Struktur bereitgestellten Informationen müssen Folgendem entsprechen:  
  
|*pwszDataSourceType*<br /><br /> (anbieterspezifisch)|*pwszDataSourceType*<br /><br /> (OLE DB-generisch)|*ulParamSize*|*bScale*|  
|----------------------------------------------------|-------------------------------------------------|-------------------|--------------|  
||DBTYPE_DATE|6|Wird ignoriert.|  
|Datum|DBTYPE_DBDATE|6|Wird ignoriert.|  
||DBTYPE_DBTIME|10|Wird ignoriert.|  
|Uhrzeit|DBTYPE_DBTIME2|10|0..7|  
|smalldatetime||16|Wird ignoriert.|  
|datetime||16|Wird ignoriert.|  
|datetime2 oder DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|16|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|0..7|  
  
 Die *bPrecision* Parameter wird ignoriert.  
  
 Beim Senden von Daten an den Server wird DBPARAMFLAGS_SS_ISVARIABLESCALE ignoriert. Anwendungen können die Verwendung von älteren tabular Data Stream (TDS) Typen erzwingen, indem Sie mithilfe der anbieterspezifischen Typnamen "**" DateTime "**"und"**Smalldatetime**". Beim Verbinden mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (oder höher)-Servern "**datetime2**"-Format verwendet und eine implizite serverkonvertierung wird durchgeführt, sofern erforderlich, wenn der Typname"**datetime2**" oder "DBTYPE_ DBTIMESTAMP". *bScale* wird ignoriert, wenn der anbieterspezifische Typname "**" DateTime "**"oder"**Smalldatetime**" verwendet werden. Andernfalls müssen Anwendungen sicherstellen, die *bScale* ordnungsgemäß festgelegt ist. Anwendungen, die ein Upgrade von MDAC und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] "DBTYPE_DBTIMESTAMP" fehl schlägt, wenn sie nicht festlegen, bei denen *bScale* ordnungsgemäß. Beim Verbinden mit Server-Instanzen vor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], *bScale* Wert ungleich 0 oder 3 mit "DBTYPE_DBTIMESTAMP" ist ein Fehler, und E_FAIL wird zurückgegeben.  
  
 ICommandWithParameters:: SetParameterInfo nicht aufgerufen wird, geben Sie die Anbieter-Imples Server wie folgt vom Bindungstyp, entsprechend den Angaben in IAccessor:: CreateAccessor:  
  
|Bindungstyp|*pwszDataSourceType*<br /><br /> (anbieterspezifisch)|  
|------------------|----------------------------------------------------|  
|DBTYPE_DATE|datetime2(0)|  
|DBTYPE_DBDATE|Datum|  
|DBTYPE_DBTIME|time(0)|  
|DBTYPE_DBTIME2|time(7)|  
|DBTYPE_DBTIMESTAMP|datetime2(7)|  
|DBTYPE_DBTIMESTAMPOFFSET|datetimeoffset(7)|  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 **IColumnsRowset:: GetColumnsRowset** gibt die folgenden Spalten zurück:  
  
|Spaltentyp|DBCOLUMN_TYPE|DBCOLUM_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|DBCOLUMN_FLAGS, DBCOLUMNFLAGS_SS_ISVARIABLESCALE|  
|-----------------|--------------------|-------------------------|-------------------------|--------------------------------------------------|---------------------------------------------------------|  
|Datum|DBTYPE_DBDATE|6|10|0|Löschen|  
|Uhrzeit|DBTYPE_DBTIME2|10|8, 10..16|0..7|Legen Sie|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Löschen|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|Löschen|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Legen Sie|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Legen Sie|  
  
 In DBCOLUMN_FLAGS hat DBCOLUMNFLAGS_ISFIXEDLENGTH für Datum-/Uhrzeit-Typen stets den Wert TRUE, und die folgenden Flags haben immer den Wert FALSE:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 Die übrigen Flags (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE und DBCOLUMNFLAGS_WRITEUNKNOWN) können festgelegt werden. Dies hängt von der Definition der Spalte und von der eigentlichen Abfrage ab.  
  
 Ein DBCOLUMNFLAGS_SS_ISVARIABLESCALE-Flag wird in DBCOLUMN_FLAGS zur Verfügung gestellt, damit eine Anwendung den Servertyp der Spalten bestimmen kann, wobei DBCOLUMN_TYPE DBTYPE_DBTIMESTAMP ist. DBCOLUMN_SCALE oder DBCOLUMN_DATETIMEPRECISION muss auch verwendet werden, um den Servertyp zu identifizieren.  
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE ist nur gültig, wenn es sich bei einer Verbindung mit einem [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (oder höher) Server. DBPARAMFLAGS_SS_ISVARIABLESCALE ist nicht definiert, wenn eine Verbindung mit einem Downlevelserver besteht.  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 Die DBCOLUMNINFO-Struktur gibt die folgenden Informationen zurück:  
  
|Parametertyp|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------------------|  
|Datum|DBTYPE_DBDATE|6|10|0|Löschen|  
|time(1..7)|DBTYPE_DBTIME2|10|8, 10..16|0..7|Legen Sie|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Löschen|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|Löschen|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Legen Sie|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Legen Sie|  
  
 In *DwFlags*, DBCOLUMNFLAGS_ISFIXEDLENGTH ist immer "true" für Datum/Uhrzeit-Typen und die folgenden Flags haben immer "false":  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER, MAYDEFER  
  
 Die übrigen Flags (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE und DBCOLUMNFLAGS_WRITEUNKNOWN) können festgelegt werden.  
  
 Neue Flag DBCOLUMNFLAGS_SS_ISVARIABLESCALE Sie im finden *DwFlags* auf eine Anwendung den Servertyp der Spalten bestimmen kann, in denen *wType* DBTYPE_DBTIMESTAMP ist. *bScale* muss ebenfalls verwendet werden, um den Servertyp zu identifizieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Metadaten &#40;OLE DB&#41;](http://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
  
  
