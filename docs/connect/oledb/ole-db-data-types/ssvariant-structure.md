---
title: SSVARIANT-Struktur | Microsoft Docs
description: SSVARIANT-Struktur in OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 797c10dfeabd1361395c5416f65c88a0d6c82176
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="ssvariant-structure"></a>SSVARIANT-Struktur
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Die **SSVARIANT** -Struktur, die in msoledbsql.h definiert ist, entspricht einem DBTYPE_SQLVARIANT-Wert in der OLE DB-Treiber für SQL Server.  
  
 **SSVARIANT** ist eine unterscheidende Vereinigung. Abhängig vom Wert des Elements vt kann der Consumer welches Element gelesen bestimmen. VT-Werte entsprechen den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentypen. Aus diesem Grund die **SSVARIANT** Struktur kann eine beliebige SQL Server-Datentyp enthalten. Weitere Informationen über die Datenstruktur für OLE DB-Standardtypen finden Sie unter [Typindikatoren](http://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Hinweise  
 Wenn DataTypeCompat == 80, mehrere **SSVARIANT** Untertypen werden Zeichenfolgen. Die folgenden vt-Werte beispielsweise erscheint im **SSVARIANT** als VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Wenn DateTypeCompat auf "0" festgelegt ist, werden diese Typen in ihrer systemeigenen Form angezeigt.  
  
 Weitere Informationen zu SSPROP_INIT_DATATYPECOMPATIBILITY finden Sie unter [Schlüsselwörtern für Verbindungszeichenfolgen mit OLE DB-Treiber für SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  
  
 Die Datei msoledbsql.h enthält variant-zugriffsmakros, die das Dereferenzieren der Elementtypen vereinfachen die **SSVARIANT** Struktur. Beispielsweise können Sie V_SS_DATETIMEOFFSET folgendermaßen verwenden:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Für den vollständigen Satz der zugriffsmakros für jedes Mitglied der **SSVARIANT** -Struktur, beziehen sich auf die Datei msoledbsql.h.  
  
 Die folgende Tabelle beschreibt die Elemente der **SSVARIANT** Struktur:  
  
|Member|OLE DB-Typindikator|OLE DB-C-Datentyp|vt-Wert|Kommentare|  
|------------|---------------------------|------------------------|--------------|--------------|  
|VT|SSVARTYPE|||Gibt den Typ des Werts in der **SSVARIANT** Struktur.|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|Unterstützt die **"tinyint"** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|Unterstützt die **"smallint"** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|Unterstützt die **Int** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|Unterstützt die **"bigint"** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|Unterstützt die **echte** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|Unterstützt die **"float"** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|Unterstützt die **Money** und **Smallmoney** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen.|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|Unterstützt die **Bit** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|Unterstützt die **"uniqueidentifier"** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|Unterstützt die **numerischen** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|Unterstützt die **Datum** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|Unterstützt die **Smalldatetime**, **"DateTime"**, und **datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen.|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|Unterstützt die **Zeit** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.<br /><br /> Beinhaltet die folgenden Member:<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**BYTE**) gibt den Maßstab für *tTime2Val* Wert.|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|Unterstützt die **datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.<br /><br /> Beinhaltet die folgenden Member:<br /><br /> *TsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**BYTE**) gibt den Maßstab für *TsDataTimeVal* Wert.|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|Unterstützt die **"DateTimeOffset"** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp.<br /><br /> Beinhaltet die folgenden Member:<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**BYTE**) gibt den Maßstab für *TsoDateTimeOffsetVal* Wert.|  
|NCharVal|Kein entsprechender OLE DB-Typindikator.|**Struktur _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|Unterstützt die **Nchar** und **Nvarchar** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen.<br /><br /> Beinhaltet die folgenden Member:<br /><br /> *sActualLength* (**kurze**) gibt an, die tatsächliche Länge der Zeichenfolge an, auf dem *PwchNCharVal* Punkte. Beinhaltet nicht den abschließenden Nullwert.<br /><br /> *sMaxLength* (**kurze**) gibt die maximale Länge für die Zeichenfolge an, auf die *PwchNCharVal* Punkte.<br /><br /> *PwchNCharVal* (**WCHAR** \*) Zeiger auf die Zeichenfolge.<br /><br /> Nicht verwendete Member: *RgbReserved*, *DwReserved*, und *PwchReserved*.|  
|CharVal|Kein entsprechender OLE DB-Typindikator.|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|Unterstützt die **Char** und **Varchar** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen.<br /><br /> Beinhaltet die folgenden Member:<br /><br /> *sActualLength* (**kurze**) gibt die tatsächliche Länge der Zeichenfolge an, auf dem *PchCharVal* Punkte. Beinhaltet nicht den abschließenden Nullwert.<br /><br /> *sMaxLength* (**kurze**) gibt die maximale Länge der Zeichenfolge an, auf dem *PchCharVal* Punkte.<br /><br /> *PchCharVal* (**CHAR** \*) Zeiger auf die Zeichenfolge.<br /><br /> Nicht verwendete Member:<br /><br /> *RgbReserved*, *DwReserved*, und *PwchReserved*.|  
|BinaryVal|Kein entsprechender OLE DB-Typindikator.|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|Unterstützt die **binäre** und **Varbinary** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen.<br /><br /> Beinhaltet die folgenden Member:<br /><br /> *sActualLength* (**kurze**) gibt die tatsächliche Länge für die Daten auf die *PrgbBinaryVal* Punkte.<br /><br /> *sMaxLength* (**kurze**) gibt die maximale Länge für die Daten auf die *PrgbBinaryVal* Punkte.<br /><br /> *PrgbBinaryVal* (**BYTE** \*) Zeiger auf die Binärdaten.<br /><br /> Nicht verwendete Member: *DwReserved*.|  
|UnknownType|NICHT VERWENDET|NICHT VERWENDET|NICHT VERWENDET|NICHT VERWENDET|  
|BLOBType|NICHT VERWENDET|NICHT VERWENDET|NICHT VERWENDET|NICHT VERWENDET|  
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40; OLE DB &#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
