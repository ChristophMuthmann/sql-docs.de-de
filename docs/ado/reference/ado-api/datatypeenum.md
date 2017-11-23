---
title: DataTypeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: DataTypeEnum
helpviewer_keywords: DataTypeEnum enumeration [ADO]
ms.assetid: 2c57eca6-9336-4b06-ba10-9fef5926b1d0
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a50a4efc0c84e3d18fad287ba31a0ebaf0705dd0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="datatypeenum"></a>DataTypeEnum
Gibt den Datentyp, der eine [Feld](../../../ado/reference/ado-api/field-object.md), [Parameter](../../../ado/reference/ado-api/parameter-object.md), oder [Eigenschaft](../../../ado/reference/ado-api/property-object-ado.md). Die entsprechende OLE DB-Typindikator wird in Klammern in der Spalte "Beschreibung" der folgenden Tabelle aufgeführt.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**AdArray**|0x2000|Ein Flagwert, immer zusammen mit anderen Datentypkonstante, die ein Array von den anderen Datentyp angibt. Gilt nicht für ADOX.|  
|**adBigInt**|20|Gibt eine 8-Byte-Ganzzahl mit Vorzeichen (DBTYPE_I8) an.|  
|**adBinary**|128|Gibt einen Binärwert (DBTYPE_BYTES) an.|  
|**adBoolean**|11|Gibt eine **booleschen** Wert (DBTYPE_BOOL).|  
|**adBSTR**|8|Gibt ein Null-terminierte Zeichenfolge (Unicode) (DBTYPE_BSTR) an.|  
|**adChapter**|136|Gibt einen 4-Byte-Kapitelwert, der eine Zeile in einem untergeordneten Rowset (DBTYPE_HCHAPTER) identifiziert.|  
|**adChar**|129|Gibt einen Zeichenfolgenwert (DBTYPE_STR) an.|  
|**adCurrency**|6|Gibt einen Currency-Wert (DBTYPE_CY). Währung ist eine Festkommazahl mit vier Ziffern rechts vom Dezimaltrennzeichen an. Er wird in eine 8-Byte-Ganzzahl mit Vorzeichen, skaliert mit 10.000 gespeichert.|  
|**adDate**|7|Gibt einen Datumswert (DBTYPE_DATE) an. Ein Datum wird gespeichert als Double-Wert, der ganzzahlige Teil von denen die Anzahl der Tage seit dem 30. Dezember 1899 wieder, und der Bruchteil der ist der Teil eines Tages.|  
|**adDBDate**|133|Gibt einen Datumswert (JJJJMMTT) (DBTYPE_DBDATE) an.|  
|**adDBTime**|134|Gibt einen Zeitwert (Hhmmss) (DBTYPE_DBTIME) an.|  
|**adDBTimeStamp**|135|Gibt einen Datum/Uhrzeit-Zeitstempel (JJJJMMTThhmmss sowie eine Bruchzahl in Milliarden) (DBTYPE_DBTIMESTAMP).|  
|**adDecimal**|14|Gibt einen genauen numerischen Wert mit einer festen Genauigkeit und festen Dezimalstellen (DBTYPE_DECIMAL) an.|  
|**adDouble**|5|Gibt einen Gleitkommawert mit doppelter Genauigkeit (DBTYPE_R8) an.|  
|**adEmpty**|0|Gibt keinen Wert an (DBTYPE_EMPTY).|  
|**adError**|10|Gibt einen 32-Bit-Fehlercode (DBTYPE_ERROR) an.|  
|**adFileTime**|64|Gibt einen 64-Bit-Wert, die die Anzahl der 100-Nanosekunden-Intervalle seit dem 1. Januar 1601 (DBTYPE_FILETIME) darstellt.|  
|**adGUID**|72|Gibt einen global eindeutigen Bezeichner (GUID) (DBTYPE_GUID) an.|  
|**adIDispatch**|9|Gibt einen Zeiger auf eine **IDispatch** Schnittstelle für ein COM-Objekt (DBTYPE_IDISPATCH).<br /><br /> **Hinweis** dieser Datentyp wird von ADO derzeit nicht unterstützt. Verwendung kann zu unvorhersehbaren Ergebnissen führen.|  
|**adInteger**|3|Gibt eine vier-Byte-Ganzzahl mit Vorzeichen (DBTYPE_I4) an.|  
|**adIUnknown**|13|Gibt einen Zeiger auf eine **IUnknown** Schnittstelle für ein COM-Objekt (DBTYPE_IUNKNOWN).<br /><br /> **Hinweis** dieser Datentyp wird von ADO derzeit nicht unterstützt. Verwendung kann zu unvorhersehbaren Ergebnissen führen.|  
|**adLongVarBinary**|205|Gibt einen langen Binärwert.|  
|**adLongVarChar**|201|Gibt einen langen Zeichenfolgenwert an.|  
|**adLongVarWChar**|203|Gibt eine lange Null-terminierte Unicode-Zeichenfolgenwert an.|  
|**Type**|131|Gibt einen genauen numerischen Wert mit einer festen Genauigkeit und festen Dezimalstellen (DBTYPE_NUMERIC) an.|  
|**adPropVariant**|138|Gibt eine Automatisierung PROPVARIANT (DBTYPE_PROP_VARIANT) an.|  
|**adSingle**|4|Gibt einen Gleitkommawert mit einfacher Genauigkeit (DBTYPE_R4) an.|  
|**adSmallInt**|2|Gibt eine 2-Byte-Ganzzahl mit Vorzeichen (DBTYPE_I2) an.|  
|**adTinyInt**|16|Gibt eine 1-Byte-Ganzzahl mit Vorzeichen (DBTYPE_I1) an.|  
|**adUnsignedBigInt**|21|Gibt eine 8-Byte-Ganzzahl ohne Vorzeichen (DBTYPE_UI8) an.|  
|**adUnsignedInt**|19|Gibt eine vier-Byte-Ganzzahl ohne Vorzeichen (DBTYPE_UI4) an.|  
|**adUnsignedSmallInt**|18|Gibt eine 2-Byte-Ganzzahl ohne Vorzeichen (DBTYPE_UI2) an.|  
|**adUnsignedTinyInt**|17|Gibt eine 1-Byte-Ganzzahl ohne Vorzeichen (DBTYPE_UI1) an.|  
|**adUserDefined**|132|Gibt eine benutzerdefinierte Variable (DBTYPE_UDT) an.|  
|**adVarBinary**|204|Gibt einen Binärwert an.|  
|**adVarChar**|200|Gibt einen Zeichenfolgenwert an.|  
|**adVariant**|12|Gibt an, eine Automatisierung **Variant** (DBTYPE_VARIANT).<br /><br /> **Hinweis** dieser Datentyp wird von ADO derzeit nicht unterstützt. Verwendung kann zu unvorhersehbaren Ergebnissen führen.|  
|**adVarNumeric**|139|Gibt einen numerischen Wert an.|  
|**adVarWChar**|202|Gibt ein Null-terminierte Unicode-Zeichenfolge an.|  
|**adWChar**|130|Gibt ein Null-terminierte Unicode-Zeichenfolge (DBTYPE_WSTR) an.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.DataType.ARRAY|  
|AdoEnums.DataType.BIGINT|  
|AdoEnums.DataType.BINARY|  
|AdoEnums.DataType.BOOLEAN|  
|AdoEnums.DataType.BSTR|  
|AdoEnums.DataType.CHAPTER|  
|AdoEnums.DataType.CHAR|  
|AdoEnums.DataType.CURRENCY|  
|AdoEnums.DataType.DATE|  
|AdoEnums.DataType.DBDATE|  
|AdoEnums.DataType.DBTIME|  
|AdoEnums.DataType.DBTIMESTAMP|  
|AdoEnums.DataType.DECIMAL|  
|AdoEnums.DataType.DOUBLE|  
|AdoEnums.DataType.EMPTY|  
|AdoEnums.DataType.ERROR|  
|AdoEnums.DataType.FILETIME|  
|AdoEnums.DataType.GUID|  
|AdoEnums.DataType.IDISPATCH|  
|AdoEnums.DataType.INTEGER|  
|AdoEnums.DataType.IUNKNOWN|  
|AdoEnums.DataType.LONGVARBINARY|  
|AdoEnums.DataType.LONGVARCHAR|  
|AdoEnums.DataType.LONGVARWCHAR|  
|AdoEnums.DataType.NUMERIC|  
|AdoEnums.DataType.PROPVARIANT|  
|AdoEnums.DataType.SINGLE|  
|AdoEnums.DataType.SMALLINT|  
|AdoEnums.DataType.TINYINT|  
|AdoEnums.DataType.UNSIGNEDBIGINT|  
|AdoEnums.DataType.UNSIGNEDINT|  
|AdoEnums.DataType.UNSIGNEDSMALLINT|  
|AdoEnums.DataType.UNSIGNEDTINYINT|  
|AdoEnums.DataType.USERDEFINED|  
|AdoEnums.DataType.VARBINARY|  
|AdoEnums.DataType.VARCHAR|  
|AdoEnums.DataType.VARIANT|  
|AdoEnums.DataType.VARNUMERIC|  
|AdoEnums.DataType.VARWCHAR|  
|AdoEnums.DataType.WCHAR|  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Append-Methode (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[CreateParameter-Methode (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|  
|[CreateRecordset-Methode (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)|[Type-Eigenschaft (ADO)](../../../ado/reference/ado-api/type-property-ado.md)|
