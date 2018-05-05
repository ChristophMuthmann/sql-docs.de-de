---
title: DateCreated-Eigenschaft (ADOX) | Microsoft Docs
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
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2b1848170421fec72fd6b0e502c015fa5be48f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="datecreated-property-adox"></a>DateCreated-Eigenschaft (ADOX)
Gibt das Datum, an das Objekt erstellt wurde.  
  
## <a name="return-values"></a>Rückgabewerte  
 Gibt eine **Variant** Wert, der das Erstellungsdatum angibt. Der Wert ist null, wenn **DateCreated** wird vom Anbieter nicht unterstützt.  
  
## <a name="remarks"></a>Hinweise  
 Die **DateCreated** -Eigenschaft für neu angefügte Objekte null ist. Nach dem Anhängen eines neuen [Ansicht](../../../ado/reference/adox-api/view-object-adox.md) oder [Prozedur](../../../ado/reference/adox-api/procedure-object-adox.md), rufen Sie die [aktualisieren](../../../ado/reference/ado-api/refresh-method-ado.md) Methode der [Ansichten](../../../ado/reference/adox-api/views-collection-adox.md) oder [Prozeduren ](../../../ado/reference/adox-api/procedures-collection-adox.md) Auflistung abzurufenden Werte für die **DateCreated** Eigenschaft.  
  
## <a name="applies-to"></a>Gilt für  
  
||||  
|-|-|-|  
|[Procedure Object (ADOX) (Procedure-Objekt (ADOX))](../../../ado/reference/adox-api/procedure-object-adox.md)|[Table-Objekt (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[View-Objekt (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [DateCreated und DateModified-Eigenschaften-Beispiel (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateModified-Eigenschaft (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)
