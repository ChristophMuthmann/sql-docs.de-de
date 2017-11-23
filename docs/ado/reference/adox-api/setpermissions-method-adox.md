---
title: SetPermissions-Methode (ADOX) | Microsoft Docs
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
- User25::SetPermissions
- User25::raw_SetPermissions
- _Group25::SetPermissions
- _Group25::raw_SetPermissions
helpviewer_keywords: SetPermissions method [ADOX]
ms.assetid: b7f925d7-b05c-4376-bb49-f8d2c17b8b24
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 068de529cd2319b846f013dab8ae399135623fd7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="setpermissions-method-adox"></a>SetPermissions-Methode (ADOX)
Gibt die Berechtigungen für eine [Gruppe](../../../ado/reference/adox-api/group-object-adox.md) oder [Benutzer](../../../ado/reference/adox-api/user-object-adox.md) für ein Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parameter  
 *Name*  
 Ein **Zeichenfolge** Wert, der den Namen des Objekts, für das zum Festlegen von Berechtigungen angibt.  
  
 *ObjectType*  
 Ein **lange** Wert sein kann von der [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) Konstanten, die angibt, den Typ des Objekts, für das Berechtigungen zu erhalten.  
  
 *Aktion*  
 Ein **lange** Wert sein kann von der [ActionEnum](../../../ado/reference/adox-api/actionenum.md) Konstanten, die den Typ der Aktion, die ausgeführt wird, beim Festlegen von Berechtigungen angibt.  
  
 *Rechte*  
 Ein **lange** Wert, der eine Bitmaske sein kann aus einem oder mehreren der der [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) Konstanten, die die festzulegenden Rechte angibt.  
  
 *Erben*  
 Optional. Ein **lange** Wert sein kann von der [InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md) Konstanten, der angibt, wie Objekte erben diese Berechtigungen. Der Standardwert ist **AdInheritNone**.  
  
 *ObjectTypeId*  
 Optional. Ein **Variant** Wert, der die GUID für einen Anbietertyp für das Objekt angibt, die nicht vom OLE DB-Spezifikation definiert ist. Dieser Parameter ist erforderlich, wenn *ObjectType* festgelegt ist, um **AdPermObjProviderSpecific**ist, andernfalls ist er nicht verwendet.  
  
## <a name="remarks"></a>Hinweise  
 Es wird eine Fehlermeldung angezeigt, wenn der Anbieter das Festlegen von Zugriffsrechten für Gruppen oder Benutzer nicht unterstützt.  
  
> [!NOTE]
>  Beim Aufrufen von **SetPermissions**, Festlegen von Aktionen auf **AdAccessRevoke** überschreibt alle Einstellungen von der *Rechte* Parameter. Legen Sie nicht *Aktionen* auf **AdAccessRevoke** ggf. die Berechtigungen, die im angegebenen der *Rechte* Parameter wirksam werden.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Group-Objekt (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[User-Objekt (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [GetPermissions und SetPermissions-Methoden (Beispiel) (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [GetPermissions-Methode (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [Name-Eigenschaft (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)
