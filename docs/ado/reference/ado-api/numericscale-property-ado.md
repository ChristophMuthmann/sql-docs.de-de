---
title: NumericScale-Eigenschaft (ADO) | Microsoft Docs
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
- _Parameter::NumericScale
- Field20::NumericScale
helpviewer_keywords:
- NumericScale property [ADO]
ms.assetid: 29a02992-64be-4fcd-be13-445cba205893
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 575618ad1760cdca6c32e1b8e2797070583506de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="numericscale-property-ado"></a>NumericScale-Eigenschaft (ADO)
Gibt die Dezimalstellen der numerischen Werte in einer [Parameter](../../../ado/reference/ado-api/parameter-object.md) oder [Feld](../../../ado/reference/ado-api/field-object.md) Objekt.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Byte** Wert, der die Anzahl der Dezimalstellen der numerischen Werte angibt, wird aufgelöst werden.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **NumericScale** -Eigenschaft können Sie bestimmen, wie viele Ziffern rechts vom Dezimaltrennzeichen verwendet werden, zur Darstellung von Werten für eine numerische **Parameter** oder **Feld** Objekt.  
  
 Für **Parameter** Objekte, die **NumericScale** Eigenschaft gilt Lese-/Schreibzugriff.  
  
 Für eine **Feld**Objekt **NumericScale** ist normalerweise schreibgeschützt. Allerdings für neue **Feld** Objekte, die angefügt wurden die [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung von einem [Datensatz](../../../ado/reference/ado-api/record-object-ado.md), **NumericScale** ist Lese-/Schreibzugriff erst nach der [Wert](../../../ado/reference/ado-api/value-property-ado.md) -Eigenschaft für die **Feld** angegeben wurde und der Datenanbieter wurde erfolgreich dem neuen hinzugefügt **Feld** durch Aufrufen der [ Update](../../../ado/reference/ado-api/update-method.md) Methode der [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)|[Field-Objekt](../../../ado/reference/ado-api/field-object.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [NumericScale und Genauigkeit Eigenschaften-Beispiel (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale und Precision-Eigenschaft (VC++-Beispiel)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Precision-Eigenschaft (ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
