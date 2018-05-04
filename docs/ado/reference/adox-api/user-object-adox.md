---
title: User-Objekt (ADOX) | Microsoft Docs
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
- User
helpviewer_keywords:
- User object [ADOX]
ms.assetid: f68e32ce-ef7c-407d-bdb5-d280947ae0e2
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f261b6b2b4d4fb62f7ac3deee3f555acbce3f992
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="user-object-adox"></a>User-Objekt (ADOX)
Stellt ein Benutzerkonto, das über Zugriffsberechtigungen in einer gesicherten Datenbank verfügt.  
  
## <a name="remarks"></a>Hinweise  
 Die [Benutzer](../../../ado/reference/adox-api/users-collection-adox.md) Auflistung von einem [Katalog](../../../ado/reference/adox-api/catalog-object-adox.md) Benutzer alle des Katalogs darstellt. Die **Benutzer** Auflistung für einen [Gruppe](../../../ado/reference/adox-api/group-object-adox.md) nur die Benutzer dieser Gruppe darstellt.  
  
 Mit den Eigenschaften, die Sammlungen und die Methoden eine **Benutzer** -Objekt können Sie:  
  
-   Identifizieren den Benutzer mit der [Namen](../../../ado/reference/adox-api/name-property-adox.md) Eigenschaft.  
  
-   Ändern Sie das Kennwort für einen Benutzer mit der [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) Methode.  
  
-   Bestimmen, ob ein Benutzer gelesen, Schreib- oder Löschberechtigungen mit der [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) und [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) Methoden.  
  
-   Zugriff auf die Gruppen, zu denen ein Benutzer gehört, mit, der [Gruppen](../../../ado/reference/adox-api/groups-collection-adox.md) Auflistung.  
  
-   Zugriff auf die anbieterspezifischen Eigenschaften mit den [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung.  
  
-   Bestimmen der [ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md) für einen Benutzer.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [User-Objekt – Eigenschaften, Methoden und Ereignisse](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [GetPermissions und SetPermissions-Methoden (Beispiel) (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Groups-Auflistung (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Users-Auflistung (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
