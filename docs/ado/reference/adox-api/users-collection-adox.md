---
title: Users-Auflistung (ADOX) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords:
- Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e063db5cd8fa810a1729b0591883b9dda0f9bc2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="users-collection-adox"></a>Users-Auflistung (ADOX)
Enthält alle gespeicherten [Benutzer](../../../ado/reference/adox-api/user-object-adox.md) Objekte von einem [Katalog](../../../ado/reference/adox-api/catalog-object-adox.md) oder [Gruppe](../../../ado/reference/adox-api/group-object-adox.md).  
  
## <a name="remarks"></a>Hinweise  
 Die **Benutzer** Auflistung von einem [Katalog](../../../ado/reference/adox-api/catalog-object-adox.md) Benutzer alle des Katalogs darstellt. Die **Benutzer** Auflistung für einen [Gruppe](../../../ado/reference/adox-api/group-object-adox.md) stellt nur die Benutzer, die eine Mitgliedschaft in der bestimmten Gruppe haben.  
  
 Die [Append](../../../ado/reference/adox-api/append-method-adox-users.md) Methode für eine **Benutzer** Auflistung für ADOX eindeutig ist. Folgende Aktionen sind möglich:  
  
-   Hinzufügen eines neuen Benutzers auf die Auflistung mit den **Append** Methode.  
  
 Die übrigen Eigenschaften und Methoden sind standard in ADO-Auflistungen. Folgende Aktionen sind möglich:  
  
-   Zugreifen auf einen Benutzer in der Auflistung mit den [Element](../../../ado/reference/ado-api/item-property-ado.md) Eigenschaft.  
  
-   Zurückgeben der Anzahl der Benutzer in der Auflistung mit den [Anzahl](../../../ado/reference/ado-api/count-property-ado.md) Eigenschaft.  
  
-   Entfernen eines Benutzers aus der Auflistung mit den [löschen](../../../ado/reference/adox-api/delete-method-adox-collections.md) Methode.  
  
-   Aktualisieren Sie die Objekte in der Auflistung entsprechend der aktuellen Datenbank-Schema mit dem [aktualisieren](../../../ado/reference/ado-api/refresh-method-ado.md) Methode.  
  
> [!NOTE]
>  Vor dem Anfügen einer **Benutzer** -Objekt an die **Benutzer** Auflistung von eine **Gruppe** -Objekt, eine **Benutzer** Objekt mit dem gleichen [Name ](../../../ado/reference/adox-api/name-property-adox.md) wie die Vorlage zum anzufügenden im bereits vorhanden sind, muss die **Benutzer** Auflistung von der **Katalog**.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Users Collection Properties, Methods, and Events (Users-Auflistung – Eigenschaften, Methoden und Ereignisse)](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [GetPermissions und SetPermissions-Methoden (Beispiel) (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Katalogobjekt (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [User-Objekt (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
