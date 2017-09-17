---
title: Append-Methode (ADOX-Gruppen) | Microsoft Docs
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
- Groups::raw_Append
- Groups::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed08c3fc0f871c1e7fb8a5885f44390770d4a7a5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="append-method-adox-groups"></a>Append-Methode (ADOX-Gruppen)
Fügt ein neues [Gruppe](../../../ado/reference/adox-api/group-object-adox.md) -Objekt an die [Gruppen](../../../ado/reference/adox-api/groups-collection-adox.md) Auflistung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>Parameter  
 *Gruppe*  
 Die **Gruppe** anzufügende Objekt oder den Namen der Gruppe, die erstellt oder ergänzt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Gruppen** Auflistung von einem [Katalog](../../../ado/reference/adox-api/catalog-object-adox.md) aller Gruppenkonten des Katalogs darstellt. Die **Gruppen** Auflistung für einen [Benutzer](../../../ado/reference/adox-api/user-object-adox.md) stellt nur die Gruppe, zu der der Benutzer gehört.  
  
 Es wird eine Fehlermeldung angezeigt, wenn der Anbieter das Erstellen von Gruppen nicht unterstützt.  
  
> [!NOTE]
>  Vor dem Anfügen einer **Gruppe** -Objekt an die **Gruppen** Auflistung von eine **Benutzer** -Objekt, eine **Gruppe** Objekt mit dem gleichen [ Namen](../../../ado/reference/adox-api/name-property-adox.md) wie die Vorlage zum anzufügenden im bereits vorhanden sind, muss die **Gruppen** Auflistung von der **Katalog**.  
  
## <a name="applies-to"></a>Gilt für  
 [Groups-Auflistung (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Gruppen und Benutzer für anfügen, ChangePassword-Methoden (Beispiel) (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append-Methode (ADOX-Spalten)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append-Methode (ADOX Indizes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append-Methode (ADOX-Schlüssel)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append-Methode (ADOX Prozeduren)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append-Methode (ADOX-Tabellen)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append-Methode (ADOX-Benutzer)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append-Methode (ADOX Ansichten)](../../../ado/reference/adox-api/append-method-adox-views.md)
