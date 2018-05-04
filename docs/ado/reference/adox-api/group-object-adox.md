---
title: Group-Objekt (ADOX) | Microsoft Docs
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
- Group
helpviewer_keywords:
- group object [ADOX]
ms.assetid: 55ef0ade-68ea-4da5-8aa5-4cd27d1f6d1e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d08fc69680dbd4126073435b6267dd0cb0dd5ca7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="group-object-adox"></a>Gruppenobjekts (ADOX)
Stellt ein Gruppenkonto, das über Zugriffsberechtigungen in einer gesicherten Datenbank verfügt.  
  
## <a name="remarks"></a>Hinweise  
 Die [Gruppen](../../../ado/reference/adox-api/groups-collection-adox.md) Auflistung von einem [Katalog](../../../ado/reference/adox-api/catalog-object-adox.md) Gruppenkonten alle des Katalogs darstellt. Die **Gruppen** Auflistung für einen [Benutzer](../../../ado/reference/adox-api/user-object-adox.md) stellt nur die Gruppe, zu der der Benutzer gehört.  
  
 Mit den Eigenschaften, die Sammlungen und die Methoden eine **Gruppe** -Objekt können Sie:  
  
-   Identifizieren Sie die Gruppe mit den [Namen](../../../ado/reference/adox-api/name-property-adox.md) Eigenschaft.  
  
-   Bestimmen, ob eine Gruppe gelesen, Schreib- oder Löschberechtigungen mit der [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) und [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) Methoden.  
  
-   Zugreifen auf die Benutzerkonten, die Mitgliedschaften in der Gruppe mit den [Benutzer](../../../ado/reference/adox-api/users-collection-adox.md) Auflistung.  
  
-   Zugriff auf die anbieterspezifischen Eigenschaften mit den [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Group-Objekt – Eigenschaften, Methoden und Ereignisse](../../../ado/reference/adox-api/group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Groups-Auflistung (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Users-Auflistung (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
