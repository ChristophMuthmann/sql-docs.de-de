---
title: FieldAttributeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- FieldAttributeEnum
helpviewer_keywords:
- FieldAttributeEnum enumeration [ADO]
ms.assetid: 6e34d886-005a-40dc-bd5c-6adcbf81e5cd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dfac02887d8f66066a11674ca6dded410df709aa
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
Gibt einen oder mehrere Attribute eines eine [Feld](../../../ado/reference/ado-api/field-object.md) Objekt.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|Gibt an, dass der Anbieter Feldwerte zwischenspeichert und nachfolgende Lesevorgänge aus dem Cache erfolgen.|  
|**adFldFixed**|0x10|Gibt an, dass das Feld Daten fester Länge enthält.|  
|**adFldIsChapter**|0x2000|Gibt an, dass das Feld einen Kapitelwert enthält, der einem bestimmten untergeordneten Recordset im Zusammenhang mit diesem übergeordneten Felds angibt. Kapitel Felder werden in der Regel mit Daten zu strukturieren oder Filtern verwendet.|  
|**adFldIsCollection**|0x40000|Gibt an, dass das Feld angibt, dass die Ressource durch den Eintrag dargestellt eine Auflistung von anderen Ressourcen, z. B. einen Ordner, anstatt eine einfache Ressource, z. B. eine Textdatei.|  
|**adFldKeyColumn**|0x8000|Gibt an, dass das Feld ein Dokument oder einen Teil des Primärschlüssels ist die Spalte angibt.|  
|**adFldIsDefaultStream**|0x20000|Gibt an, dass das Feld den Standarddatenstrom für die Ressource, dargestellt durch den Eintrag enthält. Beispielsweise kann den Standarddatenstrom der HTML-Inhalt einem Stammordner für eine Website, die automatisch bereitgestellt wird, wenn die Stamm-URL angegeben wird.|  
|**adFldIsNullable**|0x20|Gibt an, dass das Feld null-Werte akzeptiert.|  
|**adFldIsRowURL**|0x10000|Gibt an, dass das Feld die URL enthält, die den Namen die Ressource aus dem Datenspeicher, der durch den Eintrag dargestellt wird.|  
|**adFldLong**|0x80|Gibt an, dass das Feld eine lange binäre Feld ist. Gibt außerdem an, dass Sie verwenden können, die [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) und [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) Methoden.|  
|**adFldMayBeNull**|0x40|Gibt an, dass Sie null-Werte aus dem Feld lesen können.|  
|**adFldMayDefer**|0x2|Gibt an, dass das Feld verzögert ist – d. h. die Feldwerte aus der Datenquelle mit dem gesamten Datensatz, jedoch nur, wenn Sie explizit Zugriff nicht abgerufen werden.|  
|**adFldNegativeScale**|0x4000|Gibt an, dass das Feld einen numerischen Wert aus einer Spalte darstellt, die negative Skalierungswerte unterstützt. Die Skalierung wird angegeben, indem die [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) Eigenschaft.|  
|**adFldRowID**|0x100|Gibt an, dass das Feld einen permanenten Zeilenbezeichner, der nicht geschrieben werden kann, und hat keinen sinnvollen Wert enthält außer die Zeile (z. B. eine Datensatznummer, eindeutiger Bezeichner usw.) zu identifizieren.|  
|**adFldRowVersion**|0x200|Gibt an, dass das Feld eine Art von Datum oder Uhrzeit Stempel, die zur nachverfolgung von Updates enthält.|  
|**adFldUnknownUpdatable**|0x8|Gibt an, dass der Anbieter nicht bestimmen kann, wenn Sie in das Feld schreiben können.|  
|**adFldUnspecified**|-1 0xFFFFFFFF|Gibt an, dass der Anbieter die Feldattribute nicht angegeben werden.|  
|**adFldUpdatable**|0x4|Gibt an, dass Sie in das Feld schreiben können.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.FieldAttribute.CACHEDEFERRED|  
|AdoEnums.FieldAttribute.FIXED|  
|AdoEnums.FieldAttribute.ISNULLABLE|  
|AdoEnums.FieldAttribute.LONG|  
|AdoEnums.FieldAttribute.MAYBENULL|  
|AdoEnums.FieldAttribute.MAYDEFER|  
|AdoEnums.FieldAttribute.NEGATIVESCALE|  
|AdoEnums.FieldAttribute.ROWID|  
|AdoEnums.FieldAttribute.ROWVERSION|  
|AdoEnums.FieldAttribute.UNKNOWNUPDATABLE|  
|AdoEnums.FieldAttribute.UNSPECIFIED|  
|AdoEnums.FieldAttribute.UPDATABLE|  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Append-Methode (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Attribute-Eigenschaft (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)|

