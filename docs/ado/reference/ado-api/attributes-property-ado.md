---
title: Attributes-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Attributes
- Field20::Attributes
- _Parameter::Attributes
helpviewer_keywords:
- Attributes property [ADO]
ms.assetid: acc15d40-68a6-4ba9-85bd-12d331aecaa6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe7d17ab86f7ed60c863d0d3d0f2b32afd9972f3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="attributes-property-ado"></a>Attribute-Eigenschaft (ADO)
Gibt einen oder mehrere Eigenschaften eines Objekts an.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **lange** Wert.  
  
 Für eine [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) -Objekt, das **Attribute** Eigenschaft gilt Lese-/Schreibzugriff, und sein Wert die Summe aus einem oder mehreren [XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md) Werte. Der Standardwert ist 0 (null).  
  
 Für eine [Parameter](../../../ado/reference/ado-api/parameter-object.md) -Objekt, das **Attribute** Eigenschaft gilt Lese-/Schreibzugriff, und sein Wert die Summe aus einem oder mehreren [ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md) Werte. Die Standardeinstellung ist **AdParamSigned**.  
  
 Für eine [Feld](../../../ado/reference/ado-api/field-object.md) -Objekt, das **Attribute** Eigenschaft kann die Summe einer oder mehrerer [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) Werte. Es ist normalerweise schreibgeschützt. Allerdings für neue **Feld** Objekte, die angefügt wurden die [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung von einem [Datensatz](../../../ado/reference/ado-api/record-object-ado.md), **Attribute** ist Lese-/Schreibzugriff Nachdem die [Wert](../../../ado/reference/ado-api/value-property-ado.md) -Eigenschaft für die **Feld** angegeben wurde und die neue **Feld** wurde erfolgreich hinzugefügt vom Datenanbieter durch Aufrufen der [ Update](../../../ado/reference/ado-api/update-method.md) Methode der **Felder** Auflistung.  
  
 Für eine [Eigenschaft](../../../ado/reference/ado-api/property-object-ado.md) -Objekt, das **Attribute** Eigenschaft ist schreibgeschützt, und sein Wert die Summe aus einem oder mehreren [PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md) Werte.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Attribute** Eigenschaft so festlegen oder Zurückgeben von Eigenschaften der **Verbindung** Objekte **Parameter** Objekte **Feld** Objekte, oder **Eigenschaft** Objekte.  
  
 Wenn Sie mehrere Attribute festlegen, können Sie die entsprechenden Konstanten addieren. Wenn Sie den Wert der Eigenschaft auf eine Summe inkompatible Konstanten festlegen, tritt ein Fehler auf.  
  
> [!NOTE]
>  **Remote Datendienstnutzung** diese Eigenschaft ist nicht verfügbar für eine clientseitige **Verbindung** Objekt.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Field-Objekt](../../../ado/reference/ado-api/field-object.md)|  
|[Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)|[Property-Objekt (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Attribute und Eigenschaften Beispiel (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Attribute und Namen Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [AppendChunk-Methode (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [BeginTrans, CommitTrans und RollbackTrans-Methoden (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [GetChunk-Methode (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
