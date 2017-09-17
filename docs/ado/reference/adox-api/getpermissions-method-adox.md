---
title: GetPermissions-Methode (ADOX) | Microsoft Docs
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
- _User25::GetPermissions
- _Group25::raw_GetPermissions
- _Group25::GetPermissions
- _User25::raw_GetPermissions
helpviewer_keywords:
- GetPermissions method [ADOX]
ms.assetid: df201c1f-c76a-465d-98f0-83b7fc36e6e3
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 542abb8ab3c8fb5857508b4fafb6f50412c825bb
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getpermissions-method-adox"></a>GetPermissions-Methode (ADOX)
Gibt die Berechtigungen für eine [Gruppe](../../../ado/reference/adox-api/group-object-adox.md) oder [Benutzer](../../../ado/reference/adox-api/user-object-adox.md) auf ein Objekt oder ein Objektcontainer.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **lange** Wert, der angibt, eine Bitmaske, die mit den Berechtigungen, die Gruppe bzw. des Benutzers für das Objekt besitzt. Mögliche Werte sind mindestens die [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) Konstanten.  
  
#### <a name="parameters"></a>Parameter  
 *Name*  
 Ein **Variant** Wert, der den Namen des Objekts, für das zum Festlegen von Berechtigungen angibt. Legen Sie *Namen* auf einen null-Wert, wenn die Berechtigungen für den Container des Objekts abgerufen werden soll.  
  
 *ObjectType*  
 Ein **lange** Wert sein kann von der [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) Konstanten, die angibt, den Typ des Objekts, für das Berechtigungen zu erhalten.  
  
 *ObjectTypeId*  
 Optional. Ein **Variant** Wert, der angibt, die GUID für einen Anbietertyp für das Objekt nicht vom OLE DB-Spezifikation definiert. Dieser Parameter ist erforderlich, wenn *ObjectType* festgelegt ist, um **AdPermObjProviderSpecific**ist, andernfalls ist er nicht verwendet.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Gruppenobjekts (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[User-Objekt (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [GetPermissions und SetPermissions-Methoden (Beispiel) (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Name-Eigenschaft (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [SetPermissions-Methode (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
