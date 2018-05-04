---
title: Datentypen in Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 47a60c89372ed3bacc62e6d57fbcb46b35f472da
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-types-in-analysis-services"></a>Datentypen in Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Für alle <xref:Microsoft.AnalysisServices.DataItem> Objekte [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] unterstützt die folgende Teilmenge von **System.Data.OleDb.OleDbType**. Verwenden Sie zum Festlegen, oder lesen den Datentyp, [DataItem-Datentyp &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
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
  
  
