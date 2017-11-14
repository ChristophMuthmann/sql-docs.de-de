---
title: ObjectTypeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ObjectTypeEnum
helpviewer_keywords:
- ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8eb88d7f3df60d8c54782d20af73e3fd5e917db3
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="objecttypeenum"></a>ObjectTypeEnum
Gibt den Typ des Datenbankobjekts für das Berechtigungen oder Besitzer festgelegt.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|Das Objekt ist eine Spalte an.|  
|**adPermObjDatabase**|3|Das Objekt ist eine Datenbank.|  
|**adPermObjProcedure**|4|Das Objekt ist eine Prozedur.|  
|**adPermObjProviderSpecific**|-1|Das Objekt ist ein Typ, der vom Anbieter definiert. Es wird eine Fehlermeldung angezeigt, wenn die *ObjectType* Parameter ist **AdPermObjProviderSpecific** und ein *ObjectTypeId* nicht angegeben wird.|  
|**adPermObjTable**|1|Das Objekt ist eine Tabelle.|  
|**adPermObjView**|5|Das Objekt ist eine Sicht.|  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[GetObjectOwner-Methode (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions-Methode (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner-Methode](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions-Methode (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|

