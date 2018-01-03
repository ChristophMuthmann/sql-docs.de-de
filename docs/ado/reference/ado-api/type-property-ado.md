---
title: Type-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::Type
- Field20::Type
helpviewer_keywords: Type property [ADO]
ms.assetid: 8a4c079f-9f4f-4545-801d-85983b8db71e
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 635a1ad2cae9e9e698bebdbf479a3b542af4d953
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="type-property-ado"></a>Type-Eigenschaft (ADO)
Gibt an, die betriebliche Typ oder den Datentyp einer [Parameter](../../../ado/reference/ado-api/parameter-object.md), [Feld](../../../ado/reference/ado-api/field-object.md), oder [Eigenschaft](../../../ado/reference/ado-api/property-object-ado.md) Objekt.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) Wert.  
  
## <a name="remarks"></a>Hinweise  
 Für **Parameter** Objekte, die **Typ** Eigenschaft gilt Lese-/Schreibzugriff. Für das neue **Feld** Objekte, die angefügt wurden die [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung von einem [Datensatz](../../../ado/reference/ado-api/record-object-ado.md), **Typ** ist Lese-/Schreibzugriff erst nach der [ Wert](../../../ado/reference/ado-api/value-property-ado.md) -Eigenschaft für die **Feld** angegeben wurde und der Datenanbieter wurde erfolgreich dem neuen hinzugefügt **Feld** durch Aufrufen der [aktualisieren](../../../ado/reference/ado-api/update-method.md)Methode der **Felder** Auflistung.  
  
 Für alle anderen Objekte die **Typ** Eigenschaft ist schreibgeschützt.  
  
## <a name="applies-to"></a>Gilt für  
  
||||  
|-|-|-|  
|[Field-Objekt](../../../ado/reference/ado-api/field-object.md)|[Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)|[Property-Objekt (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel für Eigenschaft (Feld) (VB)](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [Type-Eigenschaft (Beispiel) (VC++)](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [RecordType-Eigenschaft (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type-Eigenschaft (ADO Stream)](../../../ado/reference/ado-api/type-property-ado-stream.md)
