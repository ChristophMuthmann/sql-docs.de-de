---
title: Groups-Auflistung (ADOX) | Microsoft Docs
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
- Groups
- User::Groups
- Catalog::Groups
helpviewer_keywords:
- Groups collection [ADOX]
ms.assetid: 09aa7b0a-69d5-4564-80a7-20ad8189670f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3dfb8a9e2f75fb11caf64b06e34016474d7b9fa7
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="groups-collection-adox"></a>Groups-Auflistung (ADOX)
Enthält alle gespeicherten [Gruppe](../../../ado/reference/adox-api/group-object-adox.md) Objekte eines Katalogs oder Benutzers.  
  
## <a name="remarks"></a>Hinweise  
 Die **Gruppen** Auflistung von einem [Katalog](../../../ado/reference/adox-api/catalog-object-adox.md) aller Gruppenkonten des Katalogs darstellt. Die **Gruppen** Auflistung für einen [Benutzer](../../../ado/reference/adox-api/user-object-adox.md) stellt nur die Gruppe, zu der der Benutzer gehört.  
  
 Die [Append](../../../ado/reference/adox-api/append-method-adox-groups.md) Methode für eine **Gruppen** Auflistung für ADOX eindeutig ist. Folgende Aktionen sind möglich:  
  
-   Fügen Sie eine neue Sicherheitsgruppe in der Auflistung der **Append** Methode.  
  
 Die übrigen Eigenschaften und Methoden sind standard in ADO-Auflistungen. Folgende Aktionen sind möglich:  
  
-   Zugreifen auf eine Gruppe in der Auflistung mit den [Element](../../../ado/reference/ado-api/item-property-ado.md) Eigenschaft.  
  
-   Zurückgeben der Anzahl der Gruppen, die in der Auflistung mit den [Anzahl](../../../ado/reference/ado-api/count-property-ado.md) Eigenschaft.  
  
-   Entfernen Sie eine Gruppe aus der Auflistung mit den [löschen](../../../ado/reference/adox-api/delete-method-adox-collections.md) Methode.  
  
-   Aktualisieren Sie die Objekte in der Auflistung entsprechend das Schema der aktuellen Datenbank mit der [aktualisieren](../../../ado/reference/ado-api/refresh-method-ado.md) Methode.  
  
> [!NOTE]
>  Vor dem Anfügen einer **Gruppe** -Objekt an die **Gruppen** Auflistung von eine **Benutzer** -Objekt, eine **Gruppe** Objekt mit dem gleichen [ Namen](../../../ado/reference/adox-api/name-property-adox.md) wie die Vorlage zum anzufügenden im bereits vorhanden sind, muss die **Gruppen** Auflistung von der **Katalog**.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Gruppen Auflistungseigenschaften, Methoden und Ereignisse](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogobjekt (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Gruppenobjekts (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)

