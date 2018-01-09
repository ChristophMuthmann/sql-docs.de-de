---
title: DataType-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DataType Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DataType
helpviewer_keywords: DataType element
ms.assetid: efe6f717-8288-4ca2-85ed-9b63d27c02d8
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 34e1e88cef7b608bef7995849a170d8ce6ec8e70
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="datatype-element-assl"></a>DataType-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Definiert den Datentyp des zugeordneten Elements an.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DataItem> <!-- or Measure -->  
   ...  
   <DataType>...</DataType>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md), [Measure](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Hinweise  
 Die Werte für **DataType** definiert sind, der **System.Data.OleDb.OleDbType** Enumeration. Nur die Enumerationswerte in der folgenden Tabelle sind jedoch gültig, in der **DataType** Element.  
  
|value|Description|  
|-----------|-----------------|  
|*BigInt*|Ein 64-Bit-Integer mit Vorzeichen Dieser Datentyp wird dem **Int64** -Datentyp im [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework und dem DBTYPE_I8-Geben Sie in der OLE DB.|  
|*Bool*|Ein boolescher Wert. Dieser Datentyp wird dem **booleschen** -Datentyp in .NET Framework und dem DBTYPE_BOOL-Datentyp in OLE DB.|  
|*Währung*|Ein Währungswert im Bereich von-2<sup>63</sup> (bzw. -922.337.203.685.477,5808) auf 2<sup>63</sup>-1 (bzw. + 922.337.203.685.477,5807) mit einer Genauigkeit von einem Zehntausendstel einer Währungseinheit. Dieser Datentyp wird dem **Decimal** -Datentyp in .NET Framework und dem DBTYPE_CY-Datentyp in OLE DB.|  
|*Datum*|Datumdaten, gespeichert als Gleitkommazahl mit doppelter Genauigkeit. Der ganzzahlige Teil gibt die Anzahl von Tagen seit dem 30. Dezember 1899 wieder, während der Bruchteil ein Teil eines Tages ist. Dieser Datentyp wird dem **"DateTime"** in .NET Framework und dem DBTYPE_DATE-Datentyp in OLE DB-Datentyp.|  
|*Double*|Eine Gleitkommazahl mit doppelter Genauigkeit Zahl innerhalb des Bereichs von - 1,79E + 308 bis 1,79E + 308. Dieser Datentyp wird dem **doppelte** -Datentyp in .NET Framework und dem DBTYPE_R8-Datentyp in OLE DB.|  
|*Integer*|Ein 32-Bit-Integer mit Vorzeichen Dieser Datentyp wird dem **Int32** in .NET Framework und dem DBTYPE_I4-Datentyp in OLE DB-Datentyp.|  
|*Single*|Eine Gleitkommazahl mit einfacher Genauigkeit Zahl innerhalb des Bereichs von - 3,40E + 38 bis 3,40E + 38. Dieser Datentyp wird dem **einzelne** in .NET Framework und dem DBTYPE_R4-Datentyp in OLE DB-Datentyp.|  
|*"Smallint"*|Eine 16-Bit-Ganzzahl mit Vorzeichen. Dieser Datentyp wird dem **Int16** in .NET Framework und dem DBTYPE_I2-Datentyp in OLE DB-Datentyp.|  
|*"Tinyint"*|Eine 8-Bit-Ganzzahl mit Vorzeichen. Dieser Datentyp wird dem **"SByte"** in .NET Framework und dem DBTYPE_I1-Datentyp in OLE DB-Datentyp.|  
|*UnsignedBigInt*|Eine 64-Bit-Ganzzahl ohne Vorzeichen. Dieser Datentyp wird dem **UInt64** in .NET Framework und dem DBTYPE_UI8-Datentyp in OLE DB-Datentyp.|  
|*UnsignedInt*|Eine 32-Bit-Ganzzahl ohne Vorzeichen. Dieser Datentyp wird dem **UInt32** in .NET Framework und dem DBTYPE_UI4-Datentyp in OLE DB-Datentyp.|  
|*UnsignedSmallInt*|Eine 16-Bit-Ganzzahl ohne Vorzeichen. Dieser Datentyp wird dem **UInt16** in .NET Framework und dem DBTYPE_UI2-Datentyp in OLE DB-Datentyp.|  
|*WChar*|Ein mit NULL endender Datenstrom von Unicode-Zeichen. Dieser Datentyp wird dem **Zeichenfolge** in .NET Framework und dem DBTYPE_WSTR-Datentyp in OLE DB-Datentyp.|  
|*Geerbt*|Der Datentyp des der **DataItem** enthalten sind, der [Quelle](../../../analysis-services/scripting/properties/source-element-measure-assl.md) Element von der **Measure** Element.<br /><br /> Hinweis: Gilt nur für **Measure** Elemente.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
