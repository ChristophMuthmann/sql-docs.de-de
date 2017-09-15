---
title: NumericScale-Eigenschaft (ADOX) | Microsoft Docs
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5f943223be304de56e52f54510bd6d27bac6d15
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
 [Type-Eigenschaft (Spalte) (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
