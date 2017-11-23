---
title: Precision-Eigenschaft (ADO) | Microsoft Docs
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
f1_keywords:
- _Parameter::Precision
- Field20::Precision
helpviewer_keywords: Precision property [ADO]
ms.assetid: 1fa38e78-6b5b-414d-ba0a-3dd26b29b766
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 866d9db49e2aeb487d38ebde085ca4ae9da197dc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="precision-property-ado"></a>Precision-Eigenschaft (ADO)
Gibt den Grad der Genauigkeit für numerische Werte in einer [Parameter](../../../ado/reference/ado-api/parameter-object.md) Objekt oder für numerische [Feld](../../../ado/reference/ado-api/field-object.md) Objekte.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Byte** Wert, der die maximale Anzahl von Ziffern für Werte darstellen angibt.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Genauigkeit** Eigenschaft, um zu bestimmen, die maximale Anzahl von Ziffern für Werte für eine numerische Darstellung **Parameter** oder **Feld** Objekt.  
  
 Der Wert ist Lese-/Schreibzugriff auf eine **Parameter** Objekt.  
  
 Für eine **Feld**Objekt **Genauigkeit** ist normalerweise schreibgeschützt. Allerdings für neue **Feld** Objekte, die angefügt wurden die [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung von einer [Datensatz](../../../ado/reference/ado-api/record-object-ado.md), **Genauigkeit** ist Lese-/Schreibzugriff Nachdem die [Wert](../../../ado/reference/ado-api/value-property-ado.md) -Eigenschaft für die **Feld** angegeben wurde und der Datenanbieter wurde erfolgreich dem neuen hinzugefügt **Feld** durch Aufrufen der [Update](../../../ado/reference/ado-api/update-method.md) Methode der **Felder** Auflistung.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Field-Objekt](../../../ado/reference/ado-api/field-object.md)|[Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [NumericScale und Genauigkeit Eigenschaften-Beispiel (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale und Precision-Eigenschaft (VC++-Beispiel)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [NumericScale-Eigenschaft (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)
