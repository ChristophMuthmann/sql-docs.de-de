---
title: NumericScale-Eigenschaft (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::PutNumericScale
- _Column::GetNumericScale
- _Column::NumericScale
- _Column::put_NumericScale
- _Column::get_NumericScale
helpviewer_keywords:
- NumericScale property [ADOX]
ms.assetid: 573ee5d1-57c7-4a27-be79-a0e12944ad9b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 624d45bf9447263800ba986bfbddda14b8949bbf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="numericscale-property-adox"></a>NumericScale-Eigenschaft (ADOX)
Gibt die Dezimalstellen eines numerischen Werts in der Spalte an.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest, und gibt eine **Byte** -Wert, der die Skalierung der Datenwerte in der Spalte ist bei der [Typ](../../../ado/reference/adox-api/type-property-column-adox.md) Eigenschaft ist **Type** oder **AdDecimal**. **NumericScale** wird für alle anderen Datentypen ignoriert.  
  
## <a name="remarks"></a>Hinweise  
 Der Standardwert ist 0 (null).  
  
 **NumericScale** wird für schreibgeschützte [Spalte](../../../ado/reference/adox-api/column-object-adox.md) Objekte, die bereits an eine Auflistung angefügt.  
  
## <a name="applies-to"></a>Gilt für  
 [Column-Objekt (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ADOX-Codebeispiel: NumericScale und Genauigkeit Eigenschaften-Beispiel (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Type-Eigenschaft (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
