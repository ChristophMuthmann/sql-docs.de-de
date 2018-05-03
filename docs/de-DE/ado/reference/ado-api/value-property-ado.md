---
title: Value-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5c1dd26184e4f869cab7edbde5c0de3ca36a03c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="value-property-ado"></a>Value-Eigenschaft (ADO)

Gibt den zugewiesenen Wert an eine [Feld](../../../ado/reference/ado-api/field-object.md), [Parameter](../../../ado/reference/ado-api/parameter-object.md), oder [Eigenschaft](../../../ado/reference/ado-api/property-object-ado.md) Objekt.
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte

Legt fest oder gibt einen **Variant** Wert, der den Wert des Objekts angibt. Standardwert hängt die [Typ](../../../ado/reference/ado-api/type-property-ado.md) Eigenschaft.
  
## <a name="remarks"></a>Hinweise

Verwenden der **Wert** Eigenschaft so festlegen oder Zurückgeben von Daten aus **Feld** -Objekten zum Festlegen oder zurückgeben Parameterwerte mit **Parameter** Objekte oder zum Festlegen oder zurückgeben eigenschafteneinstellungen mit **Eigenschaft** Objekte. Ob die **Wert** Eigenschaft gilt Lese-/Schreibzugriff oder schreibgeschützten hängt von zahlreichen Faktoren ab. finden Sie unter den jeweiligen Objektthemen Weitere Informationen.

ADO ermöglicht das Festlegen und Zurückgeben von lange Binärdaten mit dem **Wert** Eigenschaft.
  
> [!NOTE]
> Für **Parameter** Objekte, ADO-Lesevorgänge der **Wert** -Eigenschaft nur einmal vom Anbieter. Wenn ein Befehl enthält eine **Parameter** , deren **Wert** -Eigenschaft ist leer, und erstellen Sie eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) aus den Befehl ein, stellen Sie sicher, dass Sie zuerst schließen der  **Recordset** vor dem Abrufen der **Wert** Eigenschaft. Einige Anbieter, andernfalls der **Wert** -Eigenschaft können leer sein und wird nicht den richtigen Wert enthalten.
> 
> Für neue **Feld** Objekte, die angefügt wurden die [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung von einer [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) -Objekt, das **Wert** Eigenschaft muss festgelegt werden vor allen anderen **Feld** Eigenschaften können angegeben werden. Zunächst, einen bestimmten Wert für die **Wert** Eigenschaft zugewiesen und [Update](../../../ado/reference/ado-api/update-method.md) auf die **Felder** Auflistung aufgerufen. Klicken Sie dann, um andere Eigenschaften wie z. B. [Typ](../../../ado/reference/ado-api/type-property-ado.md) oder [Attribute](../../../ado/reference/ado-api/attributes-property-ado.md) zugegriffen werden kann.
  
## <a name="applies-to"></a>Gilt für
  
||||  
|-|-|-|  
|[Field-Objekt](../../../ado/reference/ado-api/field-object.md)|[Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)|[Property-Objekt (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|
  
## <a name="see-also"></a>Siehe auch

[Beispiel für Dateneigenschaften (VB)-Wert](../../../ado/reference/ado-api/value-property-example-vb.md)
[Value-Eigenschaft (VC++-Beispiel)](../../../ado/reference/ado-api/value-property-example-vc.md) 
