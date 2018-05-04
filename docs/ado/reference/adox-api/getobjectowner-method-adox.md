---
title: GetObjectOwner-Methode (ADOX) | Microsoft Docs
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
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49c25e4171602d760a54c70ed9bba80d5d6eac96
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner-Methode (ADOX)
Gibt den Besitzer eines Objekts in einem [Katalog](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **Zeichenfolge** Wert, der angibt, der [Name](../../../ado/reference/adox-api/name-property-adox.md) von der [Benutzer](../../../ado/reference/adox-api/user-object-adox.md) oder [Gruppe](../../../ado/reference/adox-api/group-object-adox.md) , besitzt das Objekt.  
  
#### <a name="parameters"></a>Parameter  
 *ObjectName*  
 Ein **Zeichenfolge** Wert, der den Namen des für den Besitzer des zurückzugebenden Objekts angibt.  
  
 *ObjectType*  
 Ein **lange** Wert sein kann von der [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) Konstanten, die den Typ des Objekts, für das Abrufen des Besitzers angibt.  
  
 *ObjectTypeId*  
 Optional. Ein **Variant** Wert, der angibt, die GUID für einen Anbietertyp für das Objekt nicht vom OLE DB-Spezifikation definiert. Dieser Parameter ist erforderlich, wenn *ObjectType* festgelegt ist, um **AdPermObjProviderSpecific**ist, andernfalls ist er nicht verwendet.  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Anbieter keine Rückgabe Objektbesitzer unterstützt, wird eine Fehlermeldung angezeigt.  
  
## <a name="applies-to"></a>Gilt für  
 [Katalogobjekt (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Siehe auch  
 [GetObjectOwner- und SetObjectOwner Methoden Beispiel (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner-Methode](../../../ado/reference/adox-api/setobjectowner-method.md)
