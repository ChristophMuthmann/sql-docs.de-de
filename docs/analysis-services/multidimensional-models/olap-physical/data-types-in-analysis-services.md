---
title: Datentypen in Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 910be4f4-3010-41cd-9fdc-f0a79a0ce823
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2310fea62e066c6ad2611a21a8afad3cd48203d4
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="data-types-in-analysis-services"></a>Datentypen in Analysis Services
  Für alle <xref:Microsoft.AnalysisServices.DataItem> Objekte [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] unterstützt die folgende Teilmenge von **System.Data.OleDb.OleDbType**. Verwenden Sie zum Festlegen, oder lesen den Datentyp, [DataItem-Datentyp &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
## <a name="supported-data-types"></a>Unterstützte Datentypen  
  
|||  
|-|-|  
|BigInt|Ein 64-Bit-Integer mit Vorzeichen Die *"bigint"* -Werttyp stellt Ganzzahlen dar, mit Werten, die im Bereich zwischen-9.223.372.036.854.775.808 und + 9.223.372.036.854.775.807 liegen.|  
|Binär (Binary)|Ein Datenstrom von Binärdaten des **Byte** Typ. **Byte** ist ein Werttyp, der Ganzzahlen ohne Vorzeichen darstellt, die zwischen 0 und 255 liegen.|  
|Boolean|Instanzen dieses Typs weisen den Wert **"true"** oder **"false"**.|  
|Währung|Ein *Währung* Wert im Bereich von-922.337.203.685.477,5808 bis + 922.337.203.685.477,5807 mit einer Genauigkeit von einem Zehntausendstel einer Währungseinheit (vier Dezimalstellen).|  
|Datum|Datum und Uhrzeitdaten, die als double-Wert gespeichert werden. Der ganzzahlige Teil gibt die Anzahl von Tagen seit dem 30. Dezember 1899 wieder, während der Bruchteil ein Teil eines Tages oder die Tageszeit ist.|  
|Double|Eine Gleitkommazahl im Bereich von -1,79769313486232E +308 bis 1,79769313486232E +308. Ein double-Wert speichert Informationen zur Zahl mit einer Genauigkeit von bis zu 15 Dezimalstellen.|  
|Integer|Eine 32-Bit-Ganzzahl mit Vorzeichen, die ganze Zahlen mit Vorzeichen darstellt, die zwischen -2.147.483.648 und +2.147.483.647 liegen.|  
|Single|Eine Gleitkommazahl im Bereich von -3,4028235E +38 bis 3,4028235E +38. Ein single-Wert speichert Informationen zur Zahl mit einer Genauigkeit von bis zu 7 Dezimalstellen.|  
|Smallint|Eine 16-Bit-Ganzzahl mit Vorzeichen. Die *"smallint"* Werttyp stellt Ganzzahlen mit Vorzeichen mit Werten, die zwischen-32768 und + 32767 liegen.|  
|Tinyint|Eine 8-Bit-Ganzzahl mit Vorzeichen. Der Tinyint-Werttyp stellt Ganzzahlen dar, die zwischen -128 und +127 liegen.|  
|UnsignedBigInt|Eine 64-Bit-Ganzzahl ohne Vorzeichen. Die *UnsignedBigInt* Werttyp stellt Ganzzahlen ohne Vorzeichen mit Werten, die im Bereich von 0 bis 18.446.744.073.709.551.615 dar.|  
|UnsignedInt|Eine 32-Bit-Ganzzahl ohne Vorzeichen. Die *UnsignedInt* Werttyp stellt Ganzzahlen ohne Vorzeichen mit Werten, die im Bereich von 0 bis 4.294.967.295 dar.|  
|UnsignedSmallInt|Eine 16-Bit-Ganzzahl ohne Vorzeichen. Die *UnsignedSmallInt* Werttyp stellt Ganzzahlen ohne Vorzeichen mit Werten, die im Bereich von 0 bis 65535.|  
|UnsignedTinyInt|Eine 8-Bit-Ganzzahl ohne Vorzeichen. Die *UnsignedTinyInt* Werttyp stellt Ganzzahlen ohne Vorzeichen mit Werten, die im Bereich von 0 bis 255|  
|WChar|Ein mit NULL endender Datenstrom von Unicode-Zeichen. Ein *WChar* ist eine sequenzielle Auflistung von Unicode-Zeichen, die zum Darstellen von Text verwendet wird.|  
  
## <a name="amo-validations-on-data-types"></a>AMO-Überprüfungen von Datentypen  
 In der folgenden Tabelle sind die zusätzlichen Überprüfungen aufgelistet, die AMO (Analysis Management Objects) für bestimmte Bindungen ausführt:  
  
|Objekt|Bindung|Zulässige Datentypen|  
|------------|-------------|------------------------|  
|DimensionAttribute|KeyColumns|Alle bis auf Binary|  
||NameColumn|Nur WChar|  
||SkippedLevelsColumn|Nur ganzzahlige Datentypen: BigInt, Integer, SmallInt, TinyInt, UnsignedBigInt, UnsignedInt, UnsignedSmallInt, UnsignedTinyInt|  
||CustomRollupColumn|Nur WChar|  
||CustomRollupPropertiesColumn|Nur WChar|  
||UnaryOperatorColumn|Nur WChar|  
||ValueColumn|Alle|  
|AttributeTranslation|CaptionColumn|Nur WChar|  
|ScalarMiningStructureColumn|KeyColumns|Alle bis auf Binary|  
||NameColumn|Nur WChar|  
|TableMiningStructureColumn|ForeignKeyColumns|Alle bis auf Binary|  
|MeasureGroupAttribute|KeyColumns|Alle bis auf Binary|  
|Distinct Count Measure|Quelle|BigInt, Currency, Double, Integer, Single, SmallInt, TinyInt, UnsignedBigInt, UnsignedInt, UnsignedSmallInt, UnsignedTinyInt|  
  
  

