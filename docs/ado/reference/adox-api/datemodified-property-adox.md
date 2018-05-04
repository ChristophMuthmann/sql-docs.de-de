---
title: DateModified-Eigenschaft (ADOX) | Microsoft Docs
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
- _Table::get_DateModified
- _Table::DateModified
- _Table::GetDateModified
helpviewer_keywords:
- DateModified property [ADOX]
ms.assetid: fed09266-1547-4bda-9088-c254d81cc738
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e9b10f7241f568b38b07e41c8343780ae4379b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="datemodified-property-adox"></a>DateModified-Eigenschaft (ADOX)
Gibt das Datum, an das Objekt zuletzt geändert wurde.  
  
## <a name="return-values"></a>Rückgabewerte  
 Gibt eine **Variant** Wert, der das Datum der Änderung angibt. Der Wert ist null, wenn **DateModified** wird vom Anbieter nicht unterstützt.  
  
## <a name="remarks"></a>Hinweise  
 Die **DateModified** -Eigenschaft für neu angefügte Objekte null ist. Nach dem Anhängen eines neuen [Ansicht](../../../ado/reference/adox-api/view-object-adox.md) oder [Prozedur](../../../ado/reference/adox-api/procedure-object-adox.md), rufen Sie die [aktualisieren](../../../ado/reference/ado-api/refresh-method-ado.md) Methode der [Ansichten](../../../ado/reference/adox-api/views-collection-adox.md) oder [Prozeduren ](../../../ado/reference/adox-api/procedures-collection-adox.md) Auflistung abzurufenden Werte für die **DateModified** Eigenschaft.  
  
## <a name="applies-to"></a>Gilt für  
  
||||  
|-|-|-|  
|[Procedure Object (ADOX) (Procedure-Objekt (ADOX))](../../../ado/reference/adox-api/procedure-object-adox.md)|[Table-Objekt (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[View-Objekt (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [DateCreated und DateModified-Eigenschaften-Beispiel (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated-Eigenschaft (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
